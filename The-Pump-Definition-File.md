# The Pump Definition File Reference

Every use of the Pump is defined by a pump definition file, which describes the correspondence between the data
in the spreadsheet and the data in VIVO.  Rows in the spreadsheet correspond to entities in VIVO.  The rows in a 
spreadsheet might represent people, for example.  Columns in the spreadsheet represent "paths" to attributes in VIVO.  This will become clearer as we see examples of how paths are used to define the way in which the Pump will
get or update values in VIVO.  The cells in the spreadsheet represent attribute values in VIVO.

The pump definition file is always in JSON format.

## Minimum definition

A minimum definition includes the required elements (marked with an asterisk below) in the required structure.

The definition file shown below is for a simple example maintaining cities (VIVO calls these PopulatedPlaces) each with two columns -- a name and a US state.  For example, Chicago is in Illinois.  

The entity_def defines the rows of the spreadsheet.  The column_defs define the columns of the spreadsheet.  Each
column def is a list of "paths."  Each path is a dictionary.  Each dictionary has two named elements -- "predicate" and
"object".  The predicate element is also a dictionary, as is the object element.  This is the required structure.
In some cases, a definition will require "closures" to define additional relationships between columns.

The remainder of this document describes the elements, their purpose and whether they are required.

    {
        "entity_def": {
            "entity_sparql": "?uri a vivo:PopulatedPlace .",
            "type": "vivo:PopulatedPlace"
        }, 
        "column_defs": {
            "name": [
                {
                    "predicate": {
                        "single": true,
                        "ref": "rdfs:label"
                    },
                    "object": {
                        "literal": true
                    }
                }
            ],
            "state": [
                {
                    "predicate": {
                        "single": true,
                        "ref": "obo:BFO_0000050"
                    },
                    "object": {
                        "literal": false,
                        "enum": "states_enum.txt"
                    }
                }
            ]
        }
    }

## entity_def\*

The entity_def includes elements used to describe the rows of the spreadsheet.

### entity_sparql\*

Entity sparql will be used by the Pump to select the entities to represent the rows in your spreadsheet.  You may have a simple entity_sparql such as:

    ?uri a foaf:Person .

The rows in your spreadsheet will be all people in your VIVO.

But you may need further restriction, as in:

    ?uri a vivo:FacultyMember . ?uri ufVivo:homeDept <http://vivo.ufl.edu/ndividual/n123123> .

where we are asking for all faculty members in the Chemistry department.  Using a restricted `entity_def`, you can limit the number of rows in your spreadsheet, or partition the data management task into pieces to be done by different people.

`entity_sparql` always refers to the entities to be select as "`?uri`.  `entity_sparql` must be valid SPARQL statements, each ending with a period as shown above.

### type\*
Indicates the rdf:type of each row of the spreadsheet.  In an update, each new entity will have this type.  The VIVO
inferencer will supply "parent" types from the ontology.  So, for example, indicating that the rows are type
PopulatedPlace, the inferencer will supply the parents: Continuant (obo), Entity (obo), Geographic Location (vivo), 
Geographic Region (vivo), Geopolitical Entity (vivo), Immaterial Entity (obo), Independent Continuant (obo), 
Location (vivo), Populated Place (vivo), Spatial Region (obo), Thing.

### order_by

Indicates the name of a column or columns that will be used to order the resulting spreadsheet.  If no order by is
given, the resulting data will be provided in URI order.

## column_defs\*

The column_defs specify the columns of the spreadsheet.  There is one column name for each column in the spreadsheet.

Two column names are reserved words, used by the Pump:

Name   | Purpose
-------|--------
uri    | will contain the URI of the entity.
remove | The remove column is optional.  

If present, it can be used to remove entities from VIVO during an update by
putting the word "remove" on a row in the spreadsheet in the remove column.

For a get, the column_defs define the output spreadsheet.  The resulting spreadsheet will contain one column for each
column_def, plus a URI column.  The columns in the spreadsheet will appear in the order of the column_defs in the
definition file.

For an update, the the source spreadsheet may contain columns not defined in the definition file.  These columns are 
ignored.  The definition file may contain column_defs not found in the source file.  These column_defs are ignored.
RDF is generated only for columns found in *both* the column_defs and the columns of the source spreadsheet.

### Column name\*

Column names are specified in the definition file as shown in the example ("name" and "state").  Column names can
be any length, upper and or lower case, with or without punctuation and spaces.  

Whatever appears as a column name
in the definition file will appear as a column name in the output spreadsheet produced by get.
  
In an update, the column name in the source must match the column name in the definition file *exactly*.  Simple
column names are preferred as a consequence.

#### The column_def is a list\*

Each column_def is a list, as indicated by the brackets \[ \].  These lists describe the "path" from the entity to 
the attribute represented by the column value.  Paths may be of length 0, 1, 2 or 3.  Lists of length zero are used
to specify desired columns that will not be processed.  For example:

    notes: [
    ]
    
is valid and indicates that the spreadsheet has (update) or will have (get) a column called "notes".  Nothing will be done with this column.

A length one list indicates that the entity has a predicate which has an object. Many VIVO attributes can be specified using length one paths.  A common example is label.  The label of an entity is specified using a triple of the form

    <entity_uri>  rdfs:label  "label_literal_value"
    
See the cities example above.  It specified that the first column of the spreasheet will be called "name".  This 
column is then defined to be a length 1 path (the list has one element).  The element is a dictionary as indicated by 
the brackets.  The dictionary has two key values, "predicate" and "object".  This is *required*.  Every column
definition is a list, every list element is a dictionary, every dictionary has two key values, "predicate" and object".

So for a length one path, this looks like:

    "name": [
        {
            "predicate": {
            },
            "object": {
            }
        }
    ]
    
So for a length two path, this looks like:

    "name": [
        {
            "predicate": {
            },
            "object": {
            }
        },
        {
            "predicate": {
            },
            "object": {
            }
        }
    ]
    
There are two dictionaries in the list.  Each dictionary has exactly two elements.  One element must have the 
key "predicate," the other has the key "object."  The length two path definition indicates that the entity
has a predicate that refers to an intermediary object, and that object in turn has a predicate and that the object 
of the second predicate is the attribute that appears in the spreadsheet.  While this appears to be complex
at first, it becomes clearer as examples are studied, and figures showing these relationships are examined.

Length three paths are similar.  The length three column_def looks like:

    "name": [
        {
            "predicate": {
            },
            "object": {
            }
        },
        {
            "predicate": {
            },
            "object": {
            }
        },
        {
            "predicate": {
            },
            "object": {
            }
        }
    ]
    
And the meaning is analogous to the length two path.  The entity has a predicate the refers to an intermediate
object that in turn has a predicate referring to a second intermediate object that in turns refers to an object that
is the attribute that appears in the spreadsheet.  VIVO has a number of three length paths attributes as you will see
in the examples. 

There are no four length paths in VIVO and length four paths are not supported by the Pump.  Definition files with
length four paths will be flagged as invalid.


#### predicate\*

The "predicate" key name is required in each element of the path.  See above.  By setting values of the predicate (see below) you can define the path from the entity to the value in the spreadsheet.

##### ref\*

Used to specify the uri of the predicate.  

Example:  You wish to manage people.  You have a column in the spreadsheet called "name."  You want to associate values in that column to the `rdfs:label` of the person entity.  To do this, you set the "ref" attribute of the
"predicate" entry to "rdf:label"  You may use all the prefixes that you are supplying to the Pump through its `prefix` argument.

##### single\*

Used to indicate whether the predicate is single valued (true), multi-valued (false), or boolean.

If you specify "true" for single, the Pump will warn you if it finds multi-valued values for the predicate.  Your value will replace *all* the values in VIVO.

If you specify "false" for single, the Pump will expect you to supply all the values for the predicate.  If you specify one value, *all* the values in VIVO will be replaced with the value you specify.  If you specify 3 values and VIVO has two, the Pump will compare the values you specify with the values in VIVO and add and remove values as needed to insure that the values you specify are the values with that will be in VIVO.

If you specify "boolean" for single, the Pump will process the column according to the value property in the object.  
For a `get`, if the value is found, the column will contain a '1', otherwise a '0'.  For an `update`, a '1' indicates
that the value should be added if not present.  A '0' indicates the value should be removed if found.  'None' can be
used as always to remove the value.  Blank, as always, indicates do nothing.

Example:  VIVO has values "a" and "b" for an attribute.  You specify the attribute is "single": false. You specify values "b";"c";"d"  VIVO will remove "a", leave "b" as is, and add "c" and "d" as values for the attribute.

A common case for multiple values is type of an entity.  Many entities have multiple types.  An organization may be a funding organization and a research organization, for example.  When specifying "single": false, you must specify all the values.

"boolean" is used to indicate that the column is a simple indicator of whether the predicate and the object value should be added or removed from VIVO.  If '' appears in the column, no action is taken.  If '0' or 'None' or 'n'
or 'no' or 'false' appears in a boolean column, the object value is removed from VIVO if present.  If any other
value is found in the column, the object value is added to VIVO if not currently in VIVO.  Whenever "boolean" is
specified, the "object" (see below) must have a "value" (see below).  Failure to provide a value for an object with a boolean predicate is considered an invalid definition.

##### include

Used to specify values that must be included by default in a multi-valued predicate.

include is optional.  Use include when you want to be sure that the multi-valued predicate always includes the
values you give in include.  include is a list.  You can specify as many values as you need in an include list.

Not: You do not need to include inferred values in an include list.  The VIVO inferencer will supply additional types for entities.  

#### object\*

The "object" key name is required in each element of the path.  See above.  The "object" key name may contain one
or more of the parameters described below.

##### datatype

Specifies the datatype of the literal object.  xsd datatypes are supported:

datatype    |  Usage
------------|---------------
xsd:integer | When literal values must be integers.  Ranks, for example.
xsd:string  | When literal values are strings.
xsd:datetime| For all VIVO dates and date times
xsd:boolean | Rare
xsd:decimal | For decimal numbers suh as dollar amounts
xsd:anyURI  | For literal values that are URI, wuch as web page addresses

##### literal\*

True if the object is a literal value, False if the object is a reference to an entity.

##### enum

Used to specify enumerations that are used to substitute one value for another.  Enumerations are very handy in VIVO 
data management.

##### filter

Filters are simple functions that take the value supplied and "improve" it, typically by correcting misspellings,
formatting, expanding abbreviations, improving the use of upper and lower case, and other simple improvements.

The Pump provides filters which can be used to improve the data quality of VIVO.

Filter                      |  Usage
----------------------------|------------------------------------------------------------------
improve_title               |  Used on publication and grant titles
improve_course_title        |  SPEC TOP IN AGRIC => Special Topics in Agriculture
improve_jobcode_description |  AST PROF => Assistant Professor
improve_email               |  Returns RFC standard email addresses
improve_phone_number        |  Returns ITU standard phone numbers
improve_date                |  Returns yyyy-mm-dd
improve_dollar_amount       |  Strings which should contain dollar amounts (two decimal digits)
improve_sponsor_award_id    |  For NIH style sponsor award ids
improve_deptid              |  For department identifiers (eight digits, may start with zero)
improve_display_name        |  When displaying the whole name (not name parts) of a person
improve_org_name            |  Organization labels

Example for publication titles:

    "title": [
        {
            "predicate": {
                "single": true, 
                "ref": "rdf:label"
            }, 
            "object": {
                "filter": "improve_title", 
                "literal": true
            }
        }
    ]

##### handler (future)

A handler can be added to an object to indicate that special processing is required in addition to the normal 
operation of the pump.  An example is photo processing.  The name of the photo file is the object literal value,
but this is not sufficient for a photo to appear in VIVO.  The photo file must be copied to a specific location 
on the VIVO server.  A photo handler can perform this action.

*Note:  Handlers are a future feature and are not available in the current version of the Pump.*

##### type

Intermediate objects in multi-length paths will be generated as needed by an update.  These new intermediate objects
will be given the type as specified.  The VIVO inferencer will supply all parent types.

#### value

value is used when the predicate processing is boolean. A value for the object is specified using the value parameter.  
If the column contains a '0' or 'None' or 'false' or 'n' or 'no', the value is removed from VIVO if present.  
If any other value is found in the column, the value is added to VIVO if not currently there.  Blank
column values are not processed.

Example:  A new research area 'x85' is created and 50 faculty are identified that have the research area.  A 
spreadsheet of faculty members and an x85 column is defined as boolean with the value 'http://definitionsource/x85'.  
The spreadsheet contains a '1' in the x85 column for each of the faculty members with the x85 research area.  
All other data for the faculty members is unchanged.  The pump will add hasResearchArea assertions for each of the 
fifty faculty.  The definition is shown below:

    "x85": [
        {
            "predicate": {
                "single": "boolean",
                "ref": "vivo:hasResearchArea"
            },
            "object": {
                "literal": false,
                "value": "http://definitionsource/x85"
            }
        }
    ],

##### lang

The RDF Lang attribute can be specified for the object.  An example is shown below

    "name": [
        {
            "predicate": {
                "single": true,
                "ref": "http://www.w3.org/2000/01/rdf-schema#label"
            },
            "object": {
                "literal": true,
                "lang": "en-US"
            }
        }
    ],
    
Object literal values will have the lang attribute in the RDF.

##### qualifier

Use a qualifier to specify an additional condition which must be met to specify the path to the attribute.

##### label

Use label to specify a label to be added to the intermediate object constructed by the Pump during an update.

## closure_defs

Closures are used to define additional paths required to specify the semantic relationships between between entities.  
In most cases, closures are not needed -- paths from the row entity can be defined through the column_defs from row 
entity to the column value, whether literal or reference.  But in some cases, there are
relationships between entities referred to from the row entity.

Closure definitions are identical in all ways to column_defs.  They are processed after all column_defs regardless 
of where they appear in the definition file.

For example, in teaching, the row entity, TeacherRole, has a clear path to the teacher and to the course.  But there
is also a relationship to be defined between the person and the course.  One might argue that this relationship is
unnecessary and that would be correct. The relationship could be inferred.  But our semantic inference is not yet
capable of making the inference between person and course, given the relationships between TeacherRole and person, 
and TeacherRole and course.  A closure is to to make the assertion between Person and Course.

Just as with any normal column_def, the closure defines a path from the row entity to the column value.  In the
teaching example, we could define a closure from the TeachingRole to the Course through the Person, thereby
defining the relationship between the Course and the Person.  Or we could define the closure a length 2 path
from TeacherRole to Person through the Course, thereby defining the relationship between the Person and the Course.
The two paths produce the same result -- the Person participates in the Course and the Course has a participant of 
the Person.  The Closure defines this relationship.

The syntax of the closure_def is identical to the syntax of the column_def.  Any number of closures can appear and
in any order. All elements of the column_def are available in closure_defs and work the same way.  

The closure_def is just a second chance to use the column data to define additional paths required to represent
the relationships between the entities.

For the teaching example, the closure defines a second path from the TeachingRole (row entity) to the course 
(column entity) through the instructor.  The `closure_def` is shown below:

    "closure_defs": {
        "course": [
            {
                "predicate": {
                    "single": true,
                    "ref": "obo:RO_0000052"
                },
                "object": {
                    "literal": false,
                    "type": "foaf:Person",
                }
            },
            {
                "predicate": {
                    "single": true,
                    "ref": "obo:BFO_0000056"
                },
                "object": {
                    "literal": false,
                    "enum": "data/course_enum.txt"
                }
            }
        ]
    },

### Notes

1.  The course is "reused" by the closure to define a second path from the TeacherRole to the course.  See the 
column_def for the first path.
2.  The first step in the path is through the instructor.
3.  The instructor step in the path does not need a qualifier.  It is coming from the row entity and there is only 
one entity that has the predicate relationship to the row entity. 