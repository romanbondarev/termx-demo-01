FHIR [specify](https://github.com/FHIR/fhir-test-cases/blob/master/tx/requirements.md) several criteria applicable to any terminology server.
The current page describe how FHIR requirements covered in TermX.

# Metadata
> The server SHALL return a CapabilityStatement from {root}/metadata

✅ TermX provide FHIR [CapabilityStatement](/api/fhir/metadata).

> This SHALL be returned without authentication (note: it may include more information when returned to an authenticated client)

✅ Supported

> It SHALL populate the CapabilityStatement.fhirVersion and CapabilityStatement.rest[mode = server].security.service properties

✅ Supported.
+++ See the extract of metadata
~~~json
"fhirVersion": "5.0.0",
    {
      "mode": "server",
      "documentation": "RESTful Terminology Server",
      "security": {
        "cors": true,
        "service": [
          {
            "coding": [
              {
                "system": "http://terminology.hl7.org/CodeSystem/restful-security-service",
                "code": "Certificates"
              }
            ]
          }
        ]
      },
~~~
+++

> It SHALL include CapabilityStatement.instantiates value of http://hl7.org/fhir/CapabilityStatement/terminology-server

✅ Supported.
+++ See the extract of metadata

~~~json
  "instantiates": [
    "http://hl7.org/fhir/CapabilityStatement/terminology-server"
  ],
~~~
+++

> The server SHALL return a TerminologyCapabilities statement from {root}/metadata?mode=terminology

✅ TermX provide FHIR [TerminologyCapabilities](/api/fhir/metadata?mode=terminology) statement.

> The TerminologyCapabilities SHALL list all the code systems that the server supports in TerminologyCapabilities.codeSystem.uri, and all the versions in 
TerminologyCapabilities.codeSystem.version.code. Code systems SHALL be listed here whether or not they are available through code system search.

✅ Supported.
+++ See the extract of TerminologyCapabilities
~~~json
  "codeSystem": [
    {
      "uri": "http://hl7.org/fhir/administrative-gender",
      "content": "complete",
      "version": "4.3.0"
    },
~~~
+++

# Reading Code Systems and Value Sets
> The server SHOULD make all the code systems and value sets it supports available through the /CodeSystem and /ValueSet endpoints.

> The service must support:
> - read on CodeSystem, ValueSet, and ConceptMap
> - search on CodeSystem, ValueSet, and ConceptMap by canonical URL


✅ Supported [/CodeSystem](/api/fhir/CodeSystem) and [/ValueSet](/api/fhir/ValueSet) endpoints.

> CodeSystems MAY have content = not-present; the tools will not consider this when choosing whether to try using the code system (uses TerminologyCapabilities.codeSystem.uri)

✅ Supported.

> The server SHOULD ensure that all code systems and value sets conform to the Shareable* Profiles

✅ Supported required [ShareableCodeSystem](http://hl7.org/fhir/shareablecodesystem.html) and [ShareableValueSet](http://hl7.org/fhir/shareablevalueset.html) profiles, and also [PublishableCodeSystem](http://hl7.org/fhir/publishablecodesystem.html), [ExecutableValueSet](http://hl7.org/fhir/executablevalueset.html), [PublishableValueSet](http://hl7.org/fhir/publishablevalueset.html) profiles.

> The server need not support history or track or report version tags on the resources (Resource.meta.version)

✅ Supported.
+++ Example
[/api/fhir/ValueSet/address-use@4.3.0](https://termx.kodality.dev/api/fhir/ValueSet/address-use@4.3.0)
+++

> Servers SHOULD generally allow multiple resources for the same canonical URL with different Resourve.version, but this is subject to business rules on the server

✅ Supported.
+++ Example
[CodeSystem/danik@0.0.1](https://termx.kodality.dev/api/fhir/CodeSystem/danik@0.0.1)
[CodeSystem/danik@0.0.2](https://termx.kodality.dev/api/fhir/CodeSystem/danik@0.0.2)
+++


# Accessing code systems and value sets

> All code systems and value sets SHALL have a web representation that is appropriate for a human to look at. The content on that page MAY be static or active; it is at the discretion of the server to decide what's on the page, but it SHOULD be more than just the json/xml for the resource (and it isn't limited to information in the resource either e.g. the server MAY choose to make additional process/provenance/context information available)

✅ Supported. Advance managements of the code systems and value sets are available.

> The server MAY choose to make this content available at the end-point for the relevant resource. e.g. aa request for {root}/CodeSystem/123 with an Accept header of 'application/fhir+json' returns the resource, and the same URL with an Accept header of 'text/html' returns a web page suitable for human consumption. Servers are not required to do this; they MAY choose to make the content available elsewhere.

✅ Accept header of 'application/fhir+json' and human-readable preview of URI are supported.
+++ Example
JSON preview [https://termx.kodality.dev/api/fhir/CodeSystem/appointment-type@1](https://termx.kodality.dev/api/fhir/CodeSystem/appointment-type@1).
Preview page automatically generated for code systems. For example, URI [https://termx.kodality.dev/fhir/CodeSystem/appointment-type](https://termx.kodality.dev/fhir/CodeSystem/appointment-type).
+++
✅ Accept header of 'text/html' is not supported.


> If the server chooses to make them available elsewhere, it SHALL populate the extension http://hl7.org/fhir/tools/StructureDefinition/web-source with a valueUrl where the web view can be found. This SHALL be populated when the CodeSystem and ValueSet are read, and also in any $expand of the value set (just for the root valueset).

ℹ Included into roadmap.

# Common Parameters
> The server SHALL
> - support $expand, $validate-code, $lookup (if code systems are hosted), and $translate (if ConceptMaps are hosted). $subsumes is highly recommended but not required
> - support for $validate-code in a batch (potentially very large number)

✅ Supported.

+++ Follow OpenAPI
- [FHIR Terminology API](/swagger/?urls.primaryName=termx-fhir)
+++

> The server SHALL support the [tx-resource](https://jira.hl7.org/browse/FHIR-33944) parameter for passing related value sets, concept maps, naming systems, code system supplements and if relevant, code systems.

🔴 Not yet.

> The server SHOULD support the [cache-id](https://jira.hl7.org/browse/FHIR-33946) parameter. If it does, it SHALL report so in TerminologyCapabilities.expansion.parameter.name.

🔴 Not yet.

> The server SHALL support supplements for the purposes of designations in different languages

✅ Supported.

> For the expand operation:
> - The server SHALL support the count parameter (offset is used, but will always be 0)
> - The server SHOULD return hierarchical expansions when possible (this is not a technical requirement, but comes up as important to authors)
> - The server SHALL support system-version, check-system-version, and force-system-version
> - The server SHALL echo all parameters (including assumed values) in the expansion parameters
> - The server SHALL report with all versions of code systems used (in 'version') (this may be renamed)
> - The server SHALL Support language correctly (both displayLanguage and accept-language header)
> - The server SHALL support the excludeNested, includeDesignations, activeOnly, includeDefinition and property parameters

✅ Supported.

> For the validate-code operation:
> - The server SHALL support validating code+system(+version)(+display), Coding, and CodeableConcept
> - The server SHALL support the mode/valueSetMode parameter
> - The server SHALL Support language correctly (both displayLanguage and accept-language header)
> - The server SHALL support the implySystem parameter
> - The server SHALL return an issues parameter
> - The server SHALL return system, code and display for the code that it considered valid, along with the version if this is known
> - The server SHOULD return a x-caused-by-unknown-system parameter for each code system it did not support

✅ Supported.

 
> The following extensions should be supported:
> - http://hl7.org/fhir/StructureDefinition/codesystem-alternate - if code system has alternate codes
> - http://hl7.org/fhir/StructureDefinition/codesystem-conceptOrder - if code system has order
> - http://hl7.org/fhir/StructureDefinition/codesystem-label - if code system supports 'labels'
> - http://hl7.org/fhir/StructureDefinition/coding-sctdescid - if sct is in scope (exact use cases need discussion)
> - http://hl7.org/fhir/StructureDefinition/itemWeight - echo in value set if defined in code system or value set
> - http://hl7.org/fhir/StructureDefinition/rendering-style - echo in value set if defined in code system or value set
> - http://hl7.org/fhir/StructureDefinition/rendering-xhtml - echo in value set if defined in code system or value set
> - http://hl7.org/fhir/StructureDefinition/valueset-concept-definition - populate if requested in expansion request
> - http://hl7.org/fhir/StructureDefinition/valueset-deprecated - populate if code system concept is deprecated
> - http://hl7.org/fhir/StructureDefinition/valueset-supplement - check for this, blow up if supplement is properly supported
> - http://hl7.org/fhir/StructureDefinition/valueset-label - echo in value set if defined in code system or value set
> - http://hl7.org/fhir/StructureDefinition/valueset-conceptOrder - echo in value set if defined in code system or value set
> Note that some of these extensions may be supported by rejecting instances that contain them, depending on the specific use cases that the server supports. E.g. if the server does not support externally derived code systems then the code system extensions are not relevant.

✅ Supported


# Swagger
In addition to common requirements TermX provides an OpenAPI interface available through Swagger UI.
- [TermX API](/swagger/?urls.primaryName=termx)
- [FHIR Terminology API](/swagger/?urls.primaryName=termx-fhir)
- [Snowstorm API](https://snowstorm-public.kodality.dev/swagger-ui.html)

