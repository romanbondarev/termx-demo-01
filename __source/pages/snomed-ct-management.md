TermX offers tight integration with [Snowstorm server](page:snowstorm) using its internal [API](https://snowstorm.kodality.dev/swagger-ui.html).

## Editions
SNOMED CT is managed and distributed by various organizations and national bodies in different countries, and they may create their own editions of SNOMED CT to meet their specific needs. 
These editions are typically based on the international version of SNOMED CT but may include additional language translations, extensions, or customizations to suit the requirements of a particular region or healthcare system.

Using TermX [SNOMED CT management](/integration/snomed/management) you can get overview of existing editions on your local snowstorm server including edition versions and create a new edition. 
![editions](files/109/snomed-edition-list.png)


## Branches

### Daily build branches
Each SNOMED CT edition will have its own specific release cycle and updates. Daily build branches allow to manage editions: add new descriptions, inactivate and reactivate synonyms. List of daily build branches can be found in [SNOMED CT management](/integration/snomed/management) component.

Daily build branch will appear in the list if edition has 'Daily build available' property. This value can be changed in edition edit form.
![Daily build list](files/109/snomed-daily-build-list.png)


### Working branches
Working branches are another way to make changes. This process of developing snomed terminology is less automatic compared to daily build branches. List of working branches can be found in [SNOMED CT management](/integration/snomed/management) component.

Branch will appear in working branch list if it is developed from edition and is not a version.
![Working branch list](files/109/working-branch-list.png)

### Authoring stats
Each daily build or working branch has information about authoring stats (new changes compared to latest version of edition). 

Authoring stats result is influenced from differnent places:
- New descriptions: all approved translations that are connected to current branch. New translations can be added in [SNOMED CT browser](page:snomed-ct-browser). If wrong decription was approved then it is possible to remove the new description in autoring stats list. After that it will apper in 'Ulinked translations' list. All unliked translations can be added to autoring stats again.  
- New synonyms: translations with type synonym that are connected to current branch.
- Inactivated synonyms: can be defined from mangement component. Clicking on dropdown modal form will appear for inactive synonym description number insertion.
- Reactionated synonyms: same process as synonym inactivation. Inactivated synonyms can be reverted using this function.

![Autoring stats](files/109/authoring-stats.png)

When changes are collected and need to be versioned the way to upload them from working branch and daily build branch are different.

Daily build branch allow more automatic way of new release creation. Clicking on 'Version changes' will appear a modal form, where edition name and new release effective date should be specified. After new release creation authoring stats will be empty.

![Version changes modal](files/109/version-chages-modal.png){width=500}.

Working branch changes can be uplaoded using RF2 file. 
1. RF2 file export on working branch (using tye SNAPSHOT)
2. Check effectiveDate fields in exported file. In next step while import effectiveDate will impact the release version name.
3. RF2 file import on edition (using type SNAPSHOT)


