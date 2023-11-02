## FHIR Terminology module
A FHIR terminology service is simply a set of functions built on the definitions provided by a collection of CodeSystem, ValueSet, and ConceptMap resources, with additional inherently known terminologies providing support. The terminology service is based on the basic principles of using FHIR terminology.
The FHIR terminology service is described in the FHIR specification:
- [Introduction](http://hl7.org/fhir/terminology-module.html) 
- [Using codes](http://hl7.org/fhir/terminologies.html)
- List of [CodeSystems](http://hl7.org/fhir/terminologies-systems.html), [ValueSets](http://hl7.org/fhir/terminologies-valuesets.html), [ConcepMaps](http://hl7.org/fhir/terminologies-conceptmaps.html), and [Identifier Systems](http://hl7.org/fhir/identifier-registry.html). 

FHIR terminology (CodeSystem, ValueSet, and ConceptMap) is based on a simplified CTS2 model. The main idea of FHIR services is to present released versions of terminology when standard development is a part of the Terminology Server and workflows in the Terminology Server ecosystem. 
An example of a request of Administrative gender:
```http
GET http://terminology.hl7.org/CodeSystem/v3-AdministrativeGender
```
will return object with resource CodeSystem with 1 parameter, 3 concepts, where every concept has one parameter:

```json
{
  "id": "v3-AdministrativeGender",
  "resourceType": "CodeSystem",
  "url": "http://terminology.hl7.org/CodeSystem/v3-AdministrativeGender",
  "version": "2.1.0",
  "name": "AdministrativeGender",
  "status": "draft",
  "date": "2019-03-20T00:00:00Z",
  "publisher": "Health Level 7",
  "contact": [
    {
      "name": "Health Level Seven"
    }
  ],
  "description": "The gender of a person used for adminstrative purposes (as opposed to clinical gender)",
  "caseSensitive": true,
  "content": "complete",
  "property": [
    {
      "code": "status",
      "description": "Designation of a concept's state. Normally is not populated unless the state is retired.",
      "type": "code"
    }
  ],
  "concept": [
    {
      "code": "F",
      "display": "Female",
      "definition": "Female",
      "property": [
        {
          "code": "status",
          "valueCode": "active"
        }
      ]
    },
    {
      "code": "M",
      "display": "Male",
      "definition": "Male",
      "property": [
        {
          "code": "status",
          "valueCode": "active"
        }
      ]
    },
    {
      "code": "UN",
      "display": "Undifferentiated",
      "definition": "En: The gender of a person could not be uniquely defined as male or female, such as intersex.",
      "property": [
        {
          "code": "status",
          "valueCode": "active"
        }
      ]
    }
  ]
}
```
CodeSystem with ICD10 diagnosis (or localized version of ICD-10) is another use-case of usage of the clinical terminology. But request 
```http
GET https://kodality.org/fhir/CodeSystem/icd10-uz
```
will return more than 40 000 concepts and more than 200 000 properties. Processing of such value sets is time, memory and CPU consuming. As a result of this, such requests are usually not made in real-time applications. Terminology operators are used instead.

## FHIR Terminology operators
### $lookup
Get additional details about the concept, including definition, status, designations, and properties. 
```http
GET [base]/CodeSystem/$lookup?system=http://loinc.org&code=1963-8
```
 or
```http 
POST [base]/CodeSystem/$lookup
[other headers]
```
will return
```json
<Parameters xmlns="http://hl7.org/fhir">
  <parameter>
    <name value="coding"/>
  <valueCoding>
    <system value="http://loinc.org"/>
    <code value="1963-8"/>
  </valueCoding>
  </parameter>
</Parameters>
```

### $validate-code
Validate that a coded value is in the code system. 
```http
GET [base]/CodeSystem/loinc/$validate-code?code=1963-8&display=test
```
```json
Body:
{
  "resourceType" : "Parameters",
  "parameter" : [
    {
    "name" : "result",
    "valueBoolean" : "false"
  },
  {
    "name" : "message",
    "valueString" : "The display \"test\" is incorrect"
  },
  {
    "name" : "display",
    "valueString" : "Bicarbonate [Moles/volume] in Serum"
  }
  ]
}
```

### $subsumes
Test the subsumption relationship between code/Coding A and code/Coding B given the semantics of subsumption in the underlying code system (validate a value in the hierarchy).
```http
GET [base]/CodeSystem/$subsumes?system=http://snomed.info/sct&codeA=3738000&codeB=235856003
```
```json
Body:
{
  "resourceType" : "Parameters",
  "parameter" : [
    {
    "name" : "outcome",
    "valueCode" : "subsumed-by"
  }
}
```

### Other operators in the FHIR specification

| Resource    | Operator        | Description |
|:-----------:|:---------------:|:-----------:|
| CodeSystem  | $find-matches   | Returns one or more possible matching codes for a given set of properties (and text).      |
| ValueSet    | $expand         | Creates a simple collection of concepts based on value set definition.|
| ValueSet    | $validate-code  | Similar to $validate-code at CodeSystem.|
| ConceptMap    | $translate | Translates/converts a code from one value set to another, based on the existing value set and concept maps resources, and/or other additional knowledge available to the server.|
| ConceptMap    | $closure | Creates transitive closure tables based on server-side terminological logic.|


### Custom operators
FHIR server (or FHIR API interface in terminology server) may propose a custom operator for a specific purpose.
For example, the TermX server proposes operator $sync which performs a smart merge of code systems and value sets instead of hard overriding.



