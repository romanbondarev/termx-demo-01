## Markdown 
Comments are supported on pages with the `markdown` content type.

A comment is created by simply selecting the text. A round icon button should appear above the selection. Clicking on this icon opens a popover with a textarea for commenting.

The button may not appear if the selection contains multiple sources. Almost every element is sourced from some Markdown (MD) line. Visually, elements may look like one thing, but in MD, they are on different lines.

Active comments appear on the right, below the "Contents", "Relations", etc., sections.

From the comment container you can:
* mark as resolved *aka. hide without deletion*
* edit
* delete *aka. forget that it ever existed*
* reply

### Replies

You can reply to a comment by clicking on the comment container, and a textarea input should appear below.

A comment or its reply can be deleted only by **its author** or by the **author of the original comment**.


### Example

Red rectangle shows the bounds of referenced element that has single source line.

*Displayed line numbers are for the demo.*

![](files/134/2023-09-11_15-22.png)


### Task intergration

When a comment is created, a task is automatically created with a "requested" status. When the task's status is changed to "completed", the comment is marked resolved and gets hidden from the comments section. If the task is "cancelled," the comment is deleted. The same applies in reverse.

Comments can be edited and deleted. 
* When the comment is edited, the task content is updated (in one direction). 
* When comment reply is created, it appears in task activity.
* If the comment is deleted, the task status changes to "cancelled".
* If the reply is delete, the task activity is deleted too.


 