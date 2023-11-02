IHTSDO [Snowstorm](https://github.com/IHTSDO/snowstorm) is an open source terminology server with special support for SNOMED CT. It is built on top of Elasticsearch, with a focus on performance and enterprise scalability.

### APIs
Snowstorm has two APIs:
- HL7 FHIR API 🔥
  - Implements the Terminology Module
  - Recommended for implementers
  - Supports SNOMED CT, LOINC, ICD-10, ICD-10-CM and other code systems
- Specialist SNOMED CT API
  - Supports the management of SNOMED CT code systems
  - Supports the SNOMED CT Browser
  - Supports authoring SNOMED CT editions

### TermX
TermX utilize Snowstorm SNOMED CT API including 
- search, 
- management of concepts and descriptions, 
- release management, 
- import and export. 

The Snowstorm SNOMED CT API useed in the TermX development environment are available through [Swagger UI](https://snowstorm.kodality.dev/swagger-ui.html).
[Notes](page:snowstorm-server) on Snowstorm server installation.

### Learn more about Snowstorm
- SNOMED CT Terminology Services [Course Guide](https://elearning.ihtsdotools.org/mod/book/view.php?id=6135&chapterid=1809)
- Snowstorm [@SNOMED eLearning site](https://snowstorm-training.snomedtools.org/snowstorm/snomed-ct/swagger-ui.html)
- Snowstorm FHIR API [Postman collection](https://documenter.getpostman.com/view/462462/S1TVXJ3k).





