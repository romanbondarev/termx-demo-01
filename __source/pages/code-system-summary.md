## Code system summary

Every code system has a summary dashboard. Dashboard are devided to header and cards. 

![CS summary](files/156/cs-summary.png)

Header provides code system name, links:
- Edit. Navigates to code system form, where code system data could be changed.
- Concepts. Navigates to [list of all code system concepts](page:code-system-concepts).
- Provenance. Navigates to provenace component where data about changes within selected code system could be seen.
- All versions. Shows dropdown of all versions. Version selection navigates to version summary.
- Close button (next to version selection). Closes code system summary and navigates you back to [code system list](page:code-system-list).

Dashboard cards:
- **Code system**. Code system information: id, description, properties, case sensitivity and content type.
- **Versions**. All code system versions sorted by effective date. Basic version information: code, validity period, concept count, status, languages. Possibility to add new or duplicate previous version, compare two version's contents, delete version (if more than 1 version exists). Click on version row navigates to version summury component. Concept link redirects to [concept list component](page:code-system-concepts). 
- **Unlinked concepts**. All concept versions that are not connected to any of the code system version (see [code system versioning](page:code-system) form more information). Possibility to add a new unliked concept and to link concept with one of versions.
- **Opened tasks | All tasks**. By default only active tasks are shown, to see full list of tasks click on 'All tasks'. List of task contains tasks that are connected to selected code system. Tasks can appear in the list on code system version approval/review request or on concept linkage request.
- **Related artifactes**. Here are listed resources that use reference to selected code system.


## Code system version summary

Every versino of code system has a summary dashboard. Data on this dash board a relevant in context of selected version. Same as code system summary, version summary dashboard are devided to header and cards. 

![CS version summary](files/156/cs-version-summary.png)

Header provides code system name, links:
- Edit. Navigates to code system form, where code system data could be changed.
- Concepts. Navigates to [list of code system version concepts](page:code-system-concepts).
- Provenance. Navigates to provenace component where data about changes within selected code system version could be seen.
- Code of selected version.
- Close button (next to version selection). Closes code system version summary and navigates you back to code system summary.

Dashboard cards:
- **Code system version**. Code system version information, possibility to dowload json, xml and fsh representaions and go to [fhir definition component](page:code-system-fhir-definition-component), change status, edit version.
- **Opened tasks | All tasks**. By default only active tasks are shown, to see full list of tasks click on 'All tasks'. List of task contains tasks that are connected to selected code system version. Tasks can appear in the list on code system version approval/review request or on concept linkage request.
