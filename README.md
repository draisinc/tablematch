# Tablematch Function
A pandas function to save easy rules inside a table and only change the table instead your code.
Easy usability also enables non-IT users to write and update rules.

# Usage

## General Example
There are different rules for Strings, Numbers, Boolean, empty / blank Columns and Dates possible.
|Numeric_Example|String_Example|Boolean_Example|Blank_Example|Date_Example|Result|
|---|---|---|---|---|---|
|>0|Hello*|True|!BLANK|>'2021-01-13'|Hello World|

The above tablematch can be read as the following pandas code:

```python
df_main_table.loc[
    (df_main_table['Result'].isna()) & 
    (df_main_table["Numeric_Example"] > 0) & 
    (df_main_table["String_Example"].str.startswith("Hello")) & 
    (df_main_table["Boolean_Example"] == "True") & 
    (df_main_table["Blank_Example"].notna()) & 
    (df_main_table["Date_Example"] > '2021-01-13'), 'Result'] = 'Hello World'
```
## OR
Rules can be seperated with a `rule_delimiter` char (Default = `,`) to get the equivalence of OR.
|Numeric_Example|String_Example|Boolean_Example|Blank_Example|Date_Example|Result|
|---|---|---|---|---|---|
|>0|Hello*, *World||||Hello World|

The above tablematch will be split into the following pandas code:
```python
df_main_table.loc[
    (df_main_table['Result'].isna()) &
    (df_main_table["Numeric_Example"] > 0) & 
    (df_main_table["String_Example"].str.startswith("Hello")), 'Result'] = 'Hello World'

df_main_table.loc[
    (df_main_table['Result'].isna()) &
    (df_main_table["Numeric_Example"] > 0) & 
    (df_main_table["String_Example"].str.endswith("World")), 'Result'] = 'Hello World'
```
## AND
Conjuctions (AND) is also possible by using Brackets and the `and_delimiter` (Default = `&`)
|Numeric_Example|String_Example|Boolean_Example|Blank_Example|Date_Example|Result|
|---|---|---|---|---|---|
|(>0&<200)|Hello*||||Hello World|

```python
df_main_table.loc[
    (df_main_table['Result'].isna()) & 
    (
        ((df_main_table["Numeric_Example"] > 0) & 
        (df_main_table["Numeric_Example"] < 100))
    ) & 
    (df_main_table["String_Example"].str.startswith("Hello")), 'Result'] = 'Hello World'
```
# Best Practice
## Don't delete rules
Old rules can be set to inactive by using a column for `tm_active`. By setting them to `False` they will not be used
## Fallback rule
Add an empty rule at the end of the rules table as a Fallback Rule. This visualize that all other rules where not accepted and new rules need to be added.  
Example: 
|Numeric_Example|String_Example|Boolean_Example|Blank_Example|Date_Example|Result|
|---|---|---|---|---|---|
|>0|Hello*, *World||||Other Rule|
||||||Fallback Rule|
## Order rules
The rules will be applied Top to Bottom. By using the `tm_order` column, all rules will be sorted before applying them. 
## Categorize rules
It is possible to include a lot of rules inside one rules table. The rules can be filtered by defining the category column (`tm_category`) and giving a List of Categories to the `input_category` variable.
# Possible Rules
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
# Impossible Rules
## Starting Chars
The following chars / strings are not possible to use at the start of a field becuase they are getting used to detect the rules:
- `!`
- `<`
- `>`
- `<=`
- `>=`
- `=`
- `==`
- `!=`
- `(` and `)`
- `*`
- `!*`
- `BLANK`
- `!BLANK`
## Ending Chars
The following chars / strings are not possible to use at the end of a field becuase they are getting used to detect the rules:
- `*`
## Delimiter chars
The following chars are not possible to use inside the field because they are getting used to detect the rules:
- `&`
- `,`

**They can be used by changing the char for the delimiter beforehand.**
# Open issues / Not implemented
- **Risk of Code Injection!**
- RegEx not implemented