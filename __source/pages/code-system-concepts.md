## Concept list

A concept list in a code system refers to a structured collection of individual medical or clinical concepts, each associated with a unique identifier.

![Cocnept list](files/157/cs-concept-list.png)

In the page header code system version can be selected. If version selected only correspondent concepts will be shown. If code system has defined 'hierarchy meaning' and concepts have associations pointing at each other then hierrachy view will be provided. To return back to plain concept list view opened folder icon should be presssed. 

Properties that are shown in the list can be configured at the code system edit by activating SHOW IN LIST value for needed property. Also you can limit showing designations and property values by selecting languages or properties.

Concept list provide possibility to: 
- add new concept
- add sub concept to build a hierarchy
- propaget parent concept properties to children
- open [fhir lookup component](page:code-system-fhir-definition-component)
- clicking on code redirects to concept edit/view 


## Concept add/edit/view

Concept dashboard has three different modes depending on concept state: 
- add: new concept
- edit: draft concept
- view: active or retired concept


![Concept view](files/157/cs-concept-view.png)