# Tablematch Function
A usefull pandas function to save easy rules inside a table and only change the table instead your code.
Easy usability also enables non-it users to write and update rules.
# Possible Rules
There are different rules for Strings, Numbers, Boolean, empty / blank Columns and Dates possible  
Rules can be seperated with a delimiter char (Default = ',') to get the equivalence of OR.
## Numeric Rules
No spaces allowed between Operator and Value. Float numbers are only allowed with a '.' dot.
The following operator are supported:
|Operator|Action|
|--------|------|
|**<Value**|smaller than Tablematch-Value|
|**\>Value**| Greater than Tablematch-Value|
|**\>=Value**| Equal or greater than Tablematch-Value|
|**<=Value**| Equal or smaller than Tablematch-Value|
|**=Value**| Equal to Tablematch-Value|
|**==Value**| Equal to Tablematch-Value|
|**!=Value**| Not equal to Tablematch-Value|
## String Rules
The following operator are supported:
|Operator|Action|
|--------|------|
|**String\***| Starts with String|
|**!String\***| Not starts with String|
|**\*String**| Ends with String|
|**!\*String**| Not ends with String|
|**\*String\***| Contains String|
|**!\*String\***| Not contains String|
|**String**| Equals String|
|**!String**| Not equals String|
## Boolean Rules
Boolean Values are getting converted to Strings and compared as it.
## Blank Rules
With 'BLANK' and '!BLANK' it is possible to test for Null Values
|Operator|Action|
|--------|------|
|**BLANK**| Cell is Null / None|
|**!BLANK**| Cell has a value|
## Date Rules
The following Operator are supported, the Date needs to be in Quotation Marks.
|Operator|Action|
|--------|------|
|**<'Date'**|smaller than Date-Value|
|**\>'Date'**| Greater than Date-Value|
|**\>='Date'**| Equal or greater than Date-Value|
|**<='Date'**| Equal or smaller than Date-Value|
|**='Date'**| Equal to Date-Value|
|**=='Date'**| Equal to Date-Value|
|**!='Date'**| Not equal to Date-Value|
# Open issues / Not implemented
- Combined Operations on the same Columns
    - Current Workaround: Copy Column and write seperate rule for the new column
- **Risk of Code Injection**
- Correct Error throwing
- Output column is always dtype = object