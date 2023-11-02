## Platforms {.tabset}

### Helm <i class="mdi mdi-ubuntu"></i>
Snowstorm Server can be installed by [Helm chart](https://gitlab.com/kodality-public/kodality-helm/-/tree/master/charts/snowstorm).

**NB!** This is not official chart. It's made only for testing purposes.

### Docker-compose <i class="mdi mdi-docker"></i>

docker-compose.yml [Original file](https://github.com/IHTSDO/snowstorm/blob/master/docker-compose.yml)
```
version: '2.1'
services:
  elasticsearch:
    restart: unless-stopped
    image: docker.elastic.co/elasticsearch/elasticsearch:7.10.2
    container_name: elasticsearch
    environment:
      - node.name=snowstorm
      - cluster.name=snowstorm-cluster
      - discovery.type=single-node
      - "ES_JAVA_OPTS=-Xms4g -Xmx4g"
    volumes:
      - /opt/snomed/data:/usr/share/elasticsearch/data
    networks:
      elastic:
        aliases:
          - es
    healthcheck:
      test: ["CMD", "curl", "-f", "http://elasticsearch:9200"]
      interval: 1s
      timeout: 1s
      retries: 60
    ports:
      - 127.0.0.1:9200:9200
    mem_reservation: 5g

  snowstorm:
    restart: unless-stopped
    image: snomedinternational/snowstorm:latest
    container_name: snowstorm
    depends_on:
      elasticsearch:
        condition: service_healthy
    entrypoint: java -Xms2g -Xmx2g -cp @/app/jib-classpath-file org.snomed.snowstorm.SnowstormApplication --elasticsearch.urls=http://elasticsearch:9200
    networks:
      - elastic
    ports:
      - 8080:8080

networks:
  elastic:
```

We recommend to protect Snowstorm endpoints using username and password as shown in the next block. Secured Snowstorm instance and TermX server should be installed in the same DMZ.
```
    entrypoint: java -Xms2g -Xmx4g -jar snowstorm.jar --elasticsearch.urls=http://elasticsearch:9200  --spring.security.user.name=termserver-app --spring.security.user.password=termserver-pwd
```

You can also setup additional Snowstorm instance for open access.
```
  snowstorm_public:
    restart: unless-stopped
    image: snomedinternational/snowstorm:latest
    container_name: snowstorm
    depends_on:
      elasticsearch:
        condition: service_healthy
    entrypoint: java -Xms2g -Xmx2g -cp @/app/jib-classpath-file org.snomed.snowstorm.SnowstormApplication --elasticsearch.urls=http://elasticsearch:9200 --snowstorm.rest-api.readonly=true
    networks:
      - elastic
    ports:
      - 8082:8080
```

In case of the external volume Elasticsearch requires additional permissions
```bash
chown -R 1000:1000 /opt/snomed/data/
```

You can also install public SNOMED Browser
```
  snomed_browser:
    restart: unless-stopped
    image: docker.kodality.com/snomedct-browser:latest
    container_name: snomed-browser
    environment:
      - API_HOST=http://snowstorm_pub:8080/
    networks:
      - elastic
    ports:
      - 9000:80
```


### Nginx configuration <i class="mdi mdi-web"></i>
Implements basic authentication for snowstorm service.

Example configuration:
```
server {
    server_name snowstorm.kodality.dev;

    auth_basic           "Authenticate yourself!";
    auth_basic_user_file /etc/nginx/.htpasswd; #user-password credentials
    client_max_body_size 6G; # allow huge file uploads, like initial Snomed International release

    add_header Strict-Transport-Security "max-age=0";
    #allow 80.235.85.70;  # Limitation of access by IP

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for
        proxy_set_header X-Forwarded-Proto $scheme;   # for https in Swagger
        proxy_pass http://localhost:8080/;
    }
#    location /snomed-ct/ {
#        proxy_set_header Host $host;
#        proxy_set_header X-Forwarded-Host $host;
#        proxy_set_header X-Real-IP $remote_addr;
#        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
#        proxy_pass http://localhost:8080/;
#    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate .../fullchain.pem; # managed by Certbot
    ssl_certificate_key .../privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
    if ($host = snowstorm.kodality.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    server_name snowstorm.kodality.dev;
    listen 80;
    return 404; # managed by Certbot
}
```
[htpasswd](https://httpd.apache.org/docs/2.4/programs/htpasswd.html) tool was used to create basic credentials file.

To change password use `htpasswd /etc/nginx/.htpasswd username` where 'username' is replaced with actual value.


## Import of the SNOMED RF2 files<i class="mdi mdi-file"></i>
#### Prerequisites
- Download SNOMED RF2 files from [SNOMED MLDS](https://mlds.ihtsdotools.org).
> If you don't have acces contact the [National Release Center](https://www.snomed.org/our-stakeholders/members) or become a member of SNOMED .
{.is-info}
- Ensure that Snowstorm is running.

#### Import of International Edition
1. Start the import process by creating a new import job. You can use Snowstorm Swagger API or curl.
Within Swagger UI open `POST: /imports` the endpoint, insert it into the body
```json
{
  "branchPath": "MAIN",
  "createCodeSystemVersion": true,
  "type": "SNAPSHOT"
}
```
and press "Try it now".

Within curl
```json
curl -v -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "branchPath": "MAIN",
  "createCodeSystemVersion": true,
  "type": "SNAPSHOT"
}' 'http://localhost:8080/imports'
```
Where 'http://localhost:8080/imports' is the address of Snowstorm server.

Store the identifier of the import (it will look like this - d0b30d96-3714-443e-99a5-2f282b1f1b0). It will be needed for the next steps.

2. Upload SNOMED archive to the Snowstorm.
Within Swagger UI select `POST imports/archive` the endpoint and specify the import identifier from the previous step and the file name.
Within curl 
```json
curl -X POST --header 'Content-Type: multipart/form-data' \
--header 'Accept: application/json' \
-F file=@init/'1. SnomedCT_InternationalRF2_PRODUCTION_20200731T120000Z.zip' \
'http://localhost:8080/imports/<import-id>/archive'
```

#### Import of the local edition or extension
1. On the Swagger interface in the ‘Code Systems’ section look for the `Create a code system` endpoint. 
Use the following in the request to create the CodeSystem. 
```json
{
  "branchPath": "MAIN/SNOMEDCT-EE",
  "shortName": "SNOMEDCT-EE"
}
```
or within curl
```json
curl -v -X POST --header 'Content-Type: application/json' \
--header 'Accept: application/json' -d '{
  "branchPath": "MAIN/SNOMEDCT-EE",
  "shortName": "SNOMEDCT-EE"
}' 'http://localhost:8080/codesystems'
```

2. You now need to import the local extension or edition. Create a new import job. 
Look for the `Import` endpoint in Swagger UI and then create a new import using:
```json
{
  "branchPath": "MAIN/SNOMEDCT-EE",
  "createCodeSystemVersion": true,
  "type": "SNAPSHOT"
}
```
or use curl
```json
curl -v -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "branchPath": "MAIN/SNOMEDCT-EE",
  "createCodeSystemVersion": true,
  "type": "SNAPSHOT"
}' 'http://localhost:8080/imports'
```

3. Import extension.

Within Swagger UI select `POST imports/archive` the endpoint and specify the import identifier from the previous step and the file name.

Within curl
```json
curl -v -X POST --header 'Content-Type: multipart/form-data' --header 'Accept: application/json' \
-F file=@SnomedCT_ManagedServiceEE_PRODUCTION_EE1000181_20200530T120000Z.zip \
'http://localhost:8080/imports/<importid>/archive'
```

