 - [Roadmap *See planned features / improvements for future releases.*](page:roadmap)
 {.links-list}

# 2.3 SNOMED authoring, synchronization with external servers
> Released on **November 3d, 2023**
{.is-info}
- The SNOMED release management was redone. Support for Snowstorm daily builds workflow. Upgrade to Snowstorm 8.3.
- Integration with SNOMED [browser](https://github.com/IHTSDO/sct-browser-frontend).
- New component for preview FHIR API
- Improved synchronization of terminology with external FHIR terminology servers
- Support of HTTP headers and OAuth flow for an external server component
- FHIR $comparator operator for the code system.
- Improvements in FML Editor.
- Health check and info endpoints.

# 2.2 Guest access, FML Editor and import enhancements
> Released on **October 6th, 2023**
{.is-info}
- You can configure publically accessible resources (terminology, structure definitions, transformations, wiki, spaces, ...).
- FML Editor. Added the support of groups, import of StructureMaps, switch between FHIRPath and native FML syntaxes.    
- FML transformation UI are more user-friendly.
- Added the import of the value sets and code system associations
- New options for CodeSystem import
- Added the ability to create FHIR IG files in the GitHub project.


# 2.1 FML Editor, Github, Capability statement
> Released on **September 1st, 2023**
{.is-info}
- FML Editor. Added ability to design FML transformations through graphical interface
- GitHub support. Added ability to synchronize Wiki and vocabulary with GitHub
- 100% support of [Capability statement](/wiki/termx-tutorial/capability-statement) and TerminologyCapabilities
- Added property-based view of the concepts in the code system
- Added defined entity properties
- Export of results of SNOMED ECL queries
- Bulk management of the concepts in value set rules
- Improved 
  - speed of value set expansion
  - import (better configuration, support of defined properties, Orphanet import reviewed)

# 2.0 TermX
> Released on **July 14th, 2023**
{.is-info}
- New web interface for terminology management
  - Landing page
  - Enhanced code system and value set management
  - New concept management interface
- Terminology
  - Authoring flow
  - Comparator of the code system versions
  - Swagger support for all FHIR Terminology endpoints and operations
- Wiki
  - New navigation
  - Support for enhanced markdown 
  - Isolation between the spaces
- Task management
  - Projects, workflows, Tasks
- SNOMED
  - Enhancements of SNOMED browser
  - Support for the translation of SNOMED concepts
  - Management of SNOMED releases
- Support for observation definitions  
- Provenance support
- Data transformation
  - Support for FHIR Mapping Language (FML)
- Rebranding (from KTS to TermX)

# 1.8 Native support for LOINC
> Released on **May 9th, 2023**
{.is-info}

> References: LIETUVOS MEDICINOS BIBLIOTEKA
- LOINC viewer
- Special LOINC importer
- Sequences
- Semantic versioning

# 1.7 Projects
> Released on **Feb 14th, 2023**
{.is-info}

> References: Navoiy state of the Respublic Uzbekistan

- Ability to group resources into the project
- Ability to compare resources in projects with another terminology server

# 1.6 Logical models and mappings
> Released on **December 16th, 2022**
{.is-info}


- Support for logical models
- Transformation of structure definitions beyween FSH and JSON formats
- Mappings
- Graphical model builder

# 1.5 SMART-on-FHIR support
> Released on **November 3rd, 2022**
{.is-info}
- Integration with SMART-on-FHIR apps

# 1.4 Thesaurus
> Released on **September 30, 2022**
{.is-info}
- Wiki editor to create clinical knowledge base and describe clinical processes.
- Key features
	- Markdown and WYSWIG editor support
  - Multilingual support
  - Templates for concepts and informational model
  - Visualization of dependencies
  - Visualization of FHIR profiles
  - Visualization of code systems and value sets from terminology


# 1.3
> Released on **August 29nd, 2022**
{.is-info}
- Hierarchical presentation of the code systems and value sets that include the 'is-a' property.

# 1.2
> Released on **August 29nd, 2022**
{.is-info}
- The support for ORPHANET ontologies
- The automatic hierarchy detecter during plain file import for the terminologies with semantical meaning in the codes (such as ATC or ICD10).

# 1.1
> Released on **August 12th, 2022**
{.is-info}
- Add alternative way to manage the concepts of code system to reduce the number of "clicks".

# 1.0.0-stable

> Released on **July 22nd, 2022**
{.is-info}

A new web page (wiki.kodality.dev) with the KTS documentation is available!

This brings new features:
- Import of the custom code systems and value sets using plain text files
- Import of the custom concept maps using plain text files
- Import of the units of measurements (UCUM)
- Import of LOINC codes
- Support for Snowstorm
- Compatibility with OWASP ASVS requirements

Web app:
- Global search over codes and designations of the code systems, value sets and concept maps
- UCUM component
- Code system concepts redesigned


# 0.4.0-beta

> Released on **June 17th, 2022**
{.is-info}

This build brings new modules:
- Swagger UI
- OpenID SSO support
- Keycloack authentication
	- Check out the [docs](/terminology-server/guide/authentication) on how to set it up.
and functionalities:
- WCAG 2.1 AA support in web application




# 0.3.0-beta

> Released on **May 27th, 2022**
{.is-info}

This build brings new modules:
- Web application for view, management and import of the code systems, value sets and set maps



# 0.2.0-beta

> Released on **March 18th, 2022**
{.is-info}

## Improvements of KTS core

This build brings new modules:

- FHIR Terminology Module API
- Imports of WHO and Estonian ATC classifiers
- Imports of WHO and Estonian ICD10 classifiers


# 0.1.0-alpha

> Released on **February 23th, 2022**
{.is-info}

## KTS2 core

Reference implementation of CTS2 specification. The following modules are supported:

- Support for CTS2 entities:
	- Code system 
  - Value set
  - Set map
  - Concepts
  - Versioning
- Service Layer
- Management API
- PostgreSQL

# Previous releases
Terminology server development began in early 2019 and has been tested on multiple installations in production environments. After a successful implementation, Terminology Server was packaged as a standalone open source product.

