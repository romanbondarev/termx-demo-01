TermX provide special processing of SNOMED CT terminology as an external terminology. TermX use  [Snowstorm](page:snowstorm) server for storing of SNOMED releases and components.
Whenever TermX provides own graphical [browser](https://termx.kodality.dev/integration/snomed/dashboard) for searching and managing SNOMED CT components, that represents the current selected branch state used by TermX.
![SNOMED CT browser](files/88/snomed-browser.png){title="SNOMED CT browser"}

With **TermX SNOMED CT browser** you can
- Browse in the concept taxonomy
- Lookup refsets and their values
- Execute [ECL](https://confluence.ihtsdotools.org/display/DOCECL) expressions

Every concept provides information about
- Concept descriptions
- Relationships / attributes
- Associations with another terminologies


### Translations

TermX also provides translation widget. You can add new translations of concept. Each translation is connected with the installed language module and the working/daily branch.

![Translation status](files/88/snomed-proposed-translation.png){width=500}

#### Translations: task flow

Every translation of SNOMED concept create a **concept review** task.

The task number and status is visible in the SNOMED CT browser and in the [task management software](page:task-management).

Translation task contains information about conceptID, existing designations, new translation and working or daily build branch where it will be added. The user may use the context links to switch between task and SNOMED CT browser.
![Translation task](files/88/translation-task.png)

Task status change impacts futher behaviour: 
- 'accepted' -> concept translations will be added to connected snomed branch
- in other cases history of proposed translation will remain, but this translation will not appear in snomed server


#### Translations: language module

Configuration of language modules is defined using Code System 'snomed-module'. To add a new language module you have to add a new concept.
- concept code: language code
- concept desugnation 'display': language module name (will be shown in modules selection)
- concept property 'language': language of module
- concept property 'refsetId': snomed id of language refset
- concept property 'moduleId': snomed id of language module
  
![Snomed language module](files/88/snomed-module.png)



