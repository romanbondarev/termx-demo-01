## Introduction

In healthcare, the constant necessity of data transformation between various interoperability standards, such as HL7 V2, HL7 V3 and CDA, and HL7 FHIR, along with their diverse versions, is prevalent. Most of these transformations occur within programmatic code, using specific programming languages that are often inaccessible or unclear to business analysts. 

## FML transformations

HL7 developed the platform-agnostic and implementation-independent [FHIR Mapping Language (FML)](http://hl7.org/fhir/mapping-language.html) for data transformation from one model to another. 
The technical specification of FML has been published as an integral component of the FHIR specification. 
FML transformation requires (see Figure below):
- One input model;
- One input instance that corresponds to the input model in JSON or XML format;
- At least one output model;
- Mapping directives that outline how to transform input into output;
- Transformation engine that will execute transformation of input instance to the output instance based on models and map.
![](files/131/FML.png){width=400}

The input and output models should be described as instances of StructureDefinition resource. The transformation map should be represented as an instance of the StructureMap resource. The StructureMap resource defines a detailed set of rules that outline the relationship between one structure and another and provides sufficient detail to allow for automated instance conversion. 


## FML transformations in TermX
TermX provides a sandbox for the creation and testing of the FML transformation. 
It provides the ability: 
- To define and preview used models, imports and concept maps.
![](files/131/Screenshot%202023-10-17%20at%2010.52.39.png){width=500}
- Generate boilerplate code for transformation and input instance.
- Compile, execute and test transformations in one place.
![](files/131/Screenshot%202023-10-17%20at%2011.01.28.png){width=500}
- Use visual [FML Editor](page:fml-editor).

TermX uses HAPI FHIR implementation to work with [StructureMap](http://hl7.org/fhir/structuremap.html) and transform data instances. 

## FML Editor

TermX provides a visual [FML Editor](page:fml-editor) as a designer of FML transformations explicitly designed for business analysts. The core purpose of the FML editor is to visualize transformations, hide the subtleties of the FML language, and enable analysts to adapt to its usage quickly.
