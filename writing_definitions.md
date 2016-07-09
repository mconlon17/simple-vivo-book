# Writing Definitions
The Pump uses a definition file to define how data can be retrieved from VIVO to a spreadsheet, and how data in a spreadsheet can be updated in VIVO.  A single definition file defines both the get action and the update action.

Round tripping is the ability to get data from VIVO to a spreadsheet, edit that spreadsheet and use the same definition to update VIVO.  You can also start from the update -- adding new data to VIVO, and then using the same definition to get the data from VIVO.

In this chapter we will see simple examples first.  You should try these simple examples.  And you should check your work.  See [The Pump Definition File Reference](The-Pump-Definition-File.md) for all definition file features.

## A simple definition file
Definition files are written using JSON syntax. JSON is a popular file format, but can be difficult to write by hand.  You should have a text editor that understands JSON format.  The text editor will help you make sure that the definitions you write are correct JSON syntax.

### Rows and Columns
To write a definition file, you need to think about the spreadsheet you will use to manage your VIVO data.  What do the rows in your spreadsheet represent? Do you have one row per person?  Per publication?  Per academic degree?  VIVO is capable of storing many kinds of data -- actually, VIVO is capable of managing all kinds of data.  VIVO manages whatever its ontologies define.  The rows in your spreadsheet may represent any of the kinds of things that your ontologies define.

Second, you will need to consider what data are stored in the columns of your spreadsheet.  Each column represents an attribute of the entity represented by the row.

Suppose you are managing data about people.  For each person, you have their name, and their academic department.

| name                 | department           | 
| -------------------- |----------------------| 
| Conlon, Michael      | Statistics           | 
| Barnes, Christopher  | Informatics          |  
 
The rows of your spreadsheet represent people.  The first column represents the name of the person.  The second column represents the department[^1] of the person.

## Writing an entity_def
## Writing a simple column_def
### Literals
### Objects and Enumerations
## Writing a two step column_def
## Writing a three step column_def
## Writing a closure_def
## More features of definition files

[^1]: In universities, identifying the department of the person may not be straightforward.  There is the concept of "tenure department," and "appointment department," and "department paying the majority of salary," and "department where the person resides.  Many faculty have appointments in multiple departments.  For the purpose of the example, we will consider department "knowable."

