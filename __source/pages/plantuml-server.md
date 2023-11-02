## Installation Guide

See [official docs](https://plantuml.com/sequence-diagram) for more information and usages.


### Docker

```yaml
version: '3.9'
services:
  plantuml-server:
    restart: unless-stopped
    image: plantuml/plantuml-server:jetty
    container_name: plantuml-server
    environment:
      - BASE_URL=plantuml
    ports:
      - 8501:8080
```



### NGINX

```
server {
    ... your usual stuff here

    location /plantuml {
        proxy_pass http://localhost:8501;
    }
}
```



Navigate to [PlantUML diagrams browser](/plantuml).
