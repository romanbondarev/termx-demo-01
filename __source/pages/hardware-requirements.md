
## Server Requirements

TermX runs virtually on any system where Docker is supported.
This means it runs on **Linux**, **macOS**, and **Windows** as well as container solutions such as **Docker / Kubernetes**.

### Database
TermX requires a PostgreSQL server as data storage. You may use the existing server or install a new instance using the docker image.

- :elephant: PostgreSQL **12 or later**
{.grid-list}

> It's recommended you use the latest version of PostgreSQL when possible.
{.is-success}

### **Using Docker** :whale:
Java and web applications are packaged into Docker containers and may run from the command line or inside any Docker container orchestration tool. 


### **Web Server** :cloud:
KTS web application is web server agnostic, you can use your favourite web server (such as Nginx or Apache) or run it w/o a web server. However, you might need to put a reverse proxy in front of the web app if you require SSL offload or advanced network / DNS configuration.

### Domain
We recommend using a dedicated sub-domain / domain *(e.g. `termx.example.com`)* for the TermX web app.

### CPU
KTS may run on a single CPU core. However, **2 cores or more are recommended** to fully make use of the background workers.
We recommend 2 cores for a database server, and 1 core for the application and web applications.

### RAM
Linux systems should have **at least 4GB of RAM** to run TermX components. Windows and macOS systems usually require a bit more RAM.
If you use the separate virtual machines give at least 2BG RAM to the database server and 2GB to the application and web server.

### Storage
Storage requirements are based on the content you will enter. The size of the code systems may vary in size from several kilobytes (in case of your small code systems) to 3 GB (in case of SNOMED).

At least 10 GB of storage dedicated to KTS is needed and 20 GB is recommended.

### Additional requirements depends on the options you use
However additional modules require additional resources. Here the list of references to the pages with requirements:
- Snowstorm - [Getting Started](https://github.com/IHTSDO/snowstorm/blob/master/docs/getting-started.md)
- Minio - [Recommended Configuration](https://min.io/product/reference-hardware)
- PlantUML - [Server installation](https://plantuml.com/server), ~256MB RAM, ~20 Mb SSD.
- KeyCloak - [System requirements](https://wjw465150.gitbooks.io/keycloak-documentation/content/server_installation/topics/installation/system-requirements.html)
- [Sushi](https://github.com/FHIR/sushi) and [GoFSH](https://github.com/FHIR/GoFSH)

| Component         | CPU      | RAM        | SSD          |
|:------------------|---------:|-----------:|-------------:|
| Mandatory components                                  ||||
| TermX database    | 1-2       | 1-2 Gb    | 20 Gb        |
| TermX backend and web | 1-2   | 2 Gb      | 10 Gb        |
| Optional components                                   ||||
| TermX swagger     | 0         | 256 Mb    | 100 Mb       |
| Snowstorm backend | 2-4       | 6-8 Gb    | 5 Gb         |
| KeyCloak server   | 1         | 512 Mb    | 10 Gb        |
| Minio server      | 1         | 512 Mb    | 20 Gb        |
| PlantUML server   | 0         | 256 Mb    | 100 Mb       |
| Chef              | 0         | 512 Mb    | 50 Mb        |

## Supported Browsers

The following browsers are supported:
- Google Chrome (including the Android version)
- Mozilla Firefox
- Microsoft Edge
- Apple Safari (including the iOS version)

Note that only the latest stable version of these browsers are supported. All browsers are automatically updated in the background by default.

