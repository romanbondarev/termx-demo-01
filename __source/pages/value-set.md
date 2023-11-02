

## Value set
![value-set-main.png](https://wiki.kodality.dev/terminology-server/value-set-main.png){width=600}
The value set landing page is similar to the code system landing page. It consists of identifiers, names (in several languages), URI, descriptions, versions, contacts, and narratives (in a separate tab).
When code systems are used to create terminology, value sets are used to create sets of values required to solve a business problem. Typically it is done by picking the code system concepts or using the expressions to include the list of concepts in the final selection or to exclude the concepts. 
### Rules
You can specify these rules within the **draft** version of the value set.
![value-set-version-edit.png](https://wiki.kodality.dev/terminology-server/value-set-version-edit.png){width=600}
The rule definition consists of rules for concept inclusion and rules for concept exclusion. All rules work additively (like UNION in SQL language). Every rule is based on the exact code system and code system version. If you don't specify any limitations all concepts from the code system will be included in a value set. 
> Use the "eye" icon to review the list of concepts that belong to the rule.
{.is-info}

![value-set-rule.png](https://wiki.kodality.dev/terminology-server/value-set-rule.png){width=600}
You can also pick only some concepts from the code system or specify expressions that are based on code system properties.



