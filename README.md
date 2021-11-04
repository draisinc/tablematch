# Tablematch Function
A usefull function to save easy rules inside a table and only change the table instead your code.
Easy usability also enables non-it users to write and update rules.
# Possible Rules
There are different rules for Strings, Numbers and Boolean possible
## Numeric Rules
No spaces allowed between Operator and Value
The following operator are supported:
- **<:** Smaller than Tablematch-Value 
- **\>:** Greater than Tablematch-Value
- **\>=:** Equal or greater than Tablematch-Value
- **<=:** Equal or smaller than Tablematch-Value
- **=:** Equal to Tablematch-Value
- **==:** Equal to Tablematch-Value
- **!=:** Not equal to Tablematch-Value
## String Rules
The following operator are supported:
- **String\*:** Starts with String
- **!String\*:** Not starts with String
- **\*String:** Ends with String
- **!\*String:** Not ends with String
- **\*String\*:** Contains String
- **!\*String\*:** Not contains String
- **String:** Equals String
- **!String:** Not equals String
## Boolean Rules
Boolean Values are getting converted to Strings and compared as it.
# Open issues / Not implemented
- BLANK not supported
- Comparison of Dates not working
- Combined Operations on the same Columns
    - Current Workaround: Copy Column and write seperate rule for the new column
- Correct Error throwing
- More Checks to prevent errors
- Caching Tablematch Dataframe to save Preprocess steps
- Risk of Code Injection
- Output column is always dtype = object
- Decimal only '.' allowed
- Include variable for other seperator
- No Support of Dates