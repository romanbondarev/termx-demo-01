## Docker-compose <i class="mdi mdi-docker"></i>

Docker-compose installation contains 3 components: backend server, frontend application and database.


In case you have your own DB instance you may omit **terminology-postgres** service from the YAML file and configure DB user/password for terminology server application in the **server.env** file.




### Reserved ports & paths
|         Service | Port | Path             |
|----------------:|------|------------------|
|        Postgres | 5432 | &nbsp;           |
|       TermX web | 9000 | `/`              |
|    TermX server | 8200 | `/api`           |
|         Swagger | 8000 | `/swagger`       |
|            Chef | 8500 | `/chef`          |
| PlantUML Server | 8501 | `/plantuml`      |
|      FML Editor | 8502 | `/fml-editor`    |
|           MinIO | 9100 | &nbsp;           |
|   MinIO console | 9101 | `/minio-console` |
{.dense}

### Example docker-compose file


+++*docker-compose.yml*

```yaml
version: '3.9'
services:
  termx-server:
    restart: unless-stopped
    image: docker.kodality.com/termx-server:latest
    container_name: termx-server
    depends_on:
      - termx-postgres
    env_file:
      - server.env
    environment:
      - DB_URL=jdbc:postgresql://termx-postgres:5432/termserver
    healthcheck:
      test: [ "CMD", "curl", "-f", "http://termx-server:8200/health" ]
      interval: 1s
      timeout: 5s
      retries: 60
    ports:
      - 8200:8200
    mem_reservation: 2g

  termx-web:
    restart: unless-stopped
    image: docker.kodality.com/termx-web:latest
    container_name: termx-web
    depends_on:
      - termx-server
    env_file:
      - web.env
    ports:
      - 9000:80

  termx-postgres:
    restart: unless-stopped
    image: postgres:14
    shm_size: 1g
    container_name: termx-postgres
    volumes:
      - ./pgdata:/var/lib/postgresql/data
    env_file:
      - pg.env
    ports:
      - 5432:5432

  termx-swagger:
    restart: unless-stopped
    image: swaggerapi/swagger-ui
    container_name: termx-swagger
    volumes:
      - ./swagger-config.json:/usr/share/nginx/html/swagger-config.json
    env_file:
      - swagger.env
    ports:
      - 8000:8080

  termx-minio:
    restart: unless-stopped
    image: quay.io/minio/minio
    container_name: termx-minio
    command: server /data --console-address ":9001"
    volumes:
      - ./minio-data:/data
    environment:
      - MINIO_ROOT_USER=minio-user
      - MINIO_ROOT_PASSWORD=minio-password
      - MINIO_CONSOLE_SUBPATH=/minio/
      - MINIO_BROWSER_REDIRECT_URL=http://localhost/minio
    ports:
      - 9100:9000
      - 9101:9001
  
  fsh-chef:
    restart: unless-stopped
    image: docker.kodality.com/fsh-chef:latest
    container_name: fsh-chef
    ports:
      - 8500:3000

  plantuml-server:
    restart: unless-stopped
    image: plantuml/plantuml-server:jetty
    container_name: plantuml-server
    environment:
      - BASE_URL=plantuml
    ports:
      - 8501:8080

  termx-fml-editor:
    restart: unless-stopped
    image: docker.kodality.com/termx-fml-editor:latest
    container_name: termx-fml-editor
    environment:
      - BASE_HREF=/fml-editor/
    ports:
      - 8502:80
```

**terminology-server** and **terminology-web** docker tags are equal to version from release notes. TODO add link

+++

## Configuration files
## {.tabset}
### pg.env
Postgres-related configuration for initial setup. You a free to change those values.

```plaintext
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=postgres
```

### server.env
Server environment variables.

```plaintext
DB_URL=jdbc:postgresql://terminology-postgres:5432/termserver #should be changed when postgres database is not defined in docker-compose.yml
DB_APP_PASSWORD=test #change to whatever you like
DB_ADMIN_PASSWORD=test #change to whatever you like
DB_POOL_SIZE=10 #default pool size
JAVA_OPTS=-Xmx1800m #default max heap size
OAUTH_JWKS_URL=https://auth.kodality.dev/realms/terminology/protocol/openid-connect/certs #JWKS url of your oauth SSO server
MICRONAUT_SERVER_CORS_ENABLED=true# for development only
MICRONAUT_SERVER_CORS_CONFIGURATIONS_UI_ALLOWED_ORIGINS=https://termx.kodality.dev

SNOWSTORM_URL=https://snowstorm.kodality.dev/ #base url of snowstorm server
SNOWSTORM_USER=termserver-app #basic-auth username
SNOWSTORM_PASSWORD=xxxx #basic-auth password

GITHUB_CLIENT_ID=xxxx
GITHUB_CLIENT_SECRET=xxxx
GITHUB_APP_ID=xxxx
GITHUB_APP_NAME=xxxx

KEYCLOAK_URL=https://auth.kodality.dev/admin/realms/terminology
KEYCLOAK_SSO_URL=https://auth.kodality.dev/realms/terminology/protocol/openid-connect
KEYCLOAK_CLIENT_ID=term-service
KEYCLOAK_CLIENT_SECRET=xxxx

BOB_MINIO_URL=http://172.17.0.1:9100
BOB_MINIO_ACCESS_KEY=xxxx
BOB_MINIO_SECRET_KEY=xxxx
```

### web.env
Frontend environment variables.

```plaintext
OAUTH_ISSUER=https://auth.kodality.dev/realms/terminology
OAUTH_CLIENT_ID=term-client
```


### swagger.env
```plaintext
CONFIG_URL=https://termx.kodality.dev/swagger/swagger-config.json
OAUTH_CLIENT_ID=term-client
OAUTH_REALM=terminology
OAUTH_USE_PKCE=true
PERSIST_AUTHORIZATION=true
BASE_URL=/swagger
```


### swagger-config.json
```json
{
  "urls": [
    {
      "url": "https://termx.kodality.dev/api/swagger/termx.yml",
      "name": "termx"
    },
    {
      "url": "https://termx.kodality.dev/api/fhir-swagger",
      "name": "termx-fhir"
    }
  ],
  "plugins": [
    "topbar"
  ]
}
```



## Running docker-compose.yml

Run docker-compose with `docker-compose up -d`

It's expected that only Postgres service will be up and running since the terminology server has no connection to the database (it's not created). Let's connect to it and create database\\users using the following command. Be sure to change admin and app user passwords according to **server.env** properties. 

```plaintext
docker exec -i termx-postgres psql -U postgres <<-EOSQL
CREATE ROLE termserver_admin LOGIN PASSWORD 'test' NOSUPERUSER INHERIT NOCREATEDB CREATEROLE NOREPLICATION;
CREATE ROLE termserver_app   LOGIN PASSWORD 'test' NOSUPERUSER INHERIT NOCREATEDB CREATEROLE NOREPLICATION;
CREATE ROLE termserver_viewer NOLOGIN NOSUPERUSER INHERIT NOCREATEDB NOCREATEROLE NOREPLICATION;
CREATE DATABASE termserver WITH OWNER = termserver_admin ENCODING = 'UTF8' TABLESPACE = pg_default CONNECTION LIMIT = -1;
grant temp on database termserver to termserver_app;
grant connect on database termserver to termserver_app;
CREATE EXTENSION IF NOT EXISTS hstore schema public;
EOSQL
```

In case you are using an existing database, run SQL commands between **EOSQL** via sql console.

##  **Checking everything is ok**

After DB is created, run `docker-compose restart` and check for application server logs via `docker logs -f terminology-server` . There should not be any errors or java stack traces. If you see a log line similar to this

```plaintext
13:08:57.472 [main] INFO  io.micronaut.runtime.Micronaut - Startup completed in 7037ms. Server Running: http://2048db663c4b:8200
```

then the application is ready to receive requests from the browser.

## Serving the application

+++NGINX reverse proxy config example

```plaintext
server {
    server_name termx.kodality.dev;

    location / {
        add_header Content-Security-Policy "default-src 'self' 'unsafe-inline' 'unsafe-eval'; img-src *; style-src 'self' 'unsafe-inline'; connect-src auth.kodality.dev terminology.kodality.dev termx.kodality.dev" always;
        proxy_pass http://localhost:9000/;
    }

    location /api/ {
        client_max_body_size 900M;
        proxy_pass http://localhost:8200/;
    }

    location /swagger {
        proxy_pass http://localhost:8000;
    }
   
    location /chef/ {
        client_max_body_size 100M;
        add_header 'Access-Control-Allow-Origin' "*" always;
        add_header 'Access-Control-Allow-Credentials' 'true' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
        add_header 'Access-Control-Allow-Headers' 'Accept,Authorization,Cache-Control,Content-Type,DNT,If-Modified-Since,Keep-Alive,Origin,User-Agent,X-Requested-With' always;
        proxy_pass http://localhost:8500/;
    }
    
    location /plantuml {
        proxy_pass http://localhost:8501;
    }

    location /fml-editor/ {
        proxy_pass http://localhost:8502/;
    }

    location /minio-console/ {
        rewrite   ^/minio-console/(.*) /$1 break;
        proxy_pass http://localhost:9101;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-NginX-Proxy true;

        # This is necessary to pass the correct IP to be hashed
        real_ip_header X-Real-IP;

        proxy_connect_timeout 300;

        # To support websockets in MinIO versions released after January 2023
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        chunked_transfer_encoding off;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/termx.kodality.dev/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/termx.kodality.dev/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
    if ($host = termx.kodality.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    server_name termx.kodality.dev;
    listen 80;
    return 404; # managed by Certbot
}
```

`server_name` value is the application domain where the application is running.
+++

Please make sure you are using SSL. Please change **\*.kodality.dev** domain configurations with your own domain. **80 → 443** redirect is a must.
 ***auth.kodality.dev** in this example is an SSO server domain.* {.is-success}

SSL certificates are managed by [Certbot](auth.kodality.dev).


