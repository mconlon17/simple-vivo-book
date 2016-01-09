# Managing Educational Background

Simple VIVO can be used to represent the educational backgrounds of your people.  Each person can have one or 
degrees.  These degrees will
be displayed on profile pages and can be used in queries.

To add educational backgrounds to VIVO, we need to know several pieces of information for each degree:

1. Who was awarded the degree?  This person must already be in your VIVO.  See the People example in Simple VIVO 
regarding managing people in your VIVO.
1. What degree was obtained?  For example, PhD, BA, MS, etc.  These degrees must already be in your VIVO.  VIVO is 
delivered with more than 100 common degrees.  If you need to add more, you can use the System Admin web interface.
1. From what institution?  The institution awarding the degree must already be in your VIVO. See Organizations
for examples of adding organizations to your VIVO.
1. What is the date of the degree?  The date must already in in your VIVO.  See the Dates example in Simple VIVO.
1. What is the field of study for the degree?  The field of study must be listed in the `field_enum.txt` file
provided in the `education` folder of Simple VIVO.  More than 800 common fields of study are provided.  Edit this
file using a text editor to add additional fields of study.

Each of these attributes is optional. 
 
## Edit the Configuration File

Edit the `sv.cfg` file to provide the query parameters for your VIVO.  Your system administrator can help you 
with this.

## Managing Enumerations

Each attribute of the degree is represented by an enumeration.  This guarantees that all the information regarding 
education in VIVO is "coded" -- there are no open-ended text fields associated with educational background, and 
"linked" -- we can easily find all the people with a particular degree, all the people who have degrees from 
particular institutions, and all other combinations of attributes.  If a value for one of the attributes can not be 
found in the enumerations, it will need to be added before the degree will be added to VIVO.  

Five enumerations are used for the five attributes:  

1. `person_enum.txt` for who
1. `degree_enum.txt` for what
1. `school_enum.txt` for where
1. `date_enum.txt` for when
1. `field_enum.txt` for field of study

The python program `make_enum.py` can be used to update four of these enumerations from your VIVO.  To run 
`make_enum.py` use:

    python make_enum.py
    
### Fields of Study

The field of study enumeration is managed by hand -- if you have fields of study that you would like to be able to 
represent in VIVO, edit the `field_enum.txt` file with a text editor and add a row for each such field of study. If
there are fields of study in the provided enumeration that you do not wish to allow ion your VIVO, remove these rows
from the enumeration.

You will notice that the short form of the field of study and the VIVO form are identical.  Field of study is a 
text field, but one which we would like to control -- that is, we do not want arbitrary text to appear in the fields
of study.  The field of study enumeration is used to look up each attempt to add a filed of study value, and confirm
that the field of study is on the list.  Any list of fields of study can be controlled in this manner.

## Procedure

1. Get the existing educational backgrounds from your VIVO into a spreadsheet.  To do this, 
run get:  `python sv.py -a get` The result will be a `degrees.txt` file.
1. Edit your enumerations as needed to provide additional values for degrees and fields of study.  To add 
universities or other schools to your VIVO and make them available for your education work, use the orgs example 
to add the organizations, then run `make_enum` to update your enumerations.  The new schools are now available for 
putting educational backgrounds in VIVO.
1. Edit `degrees.txt` in a spreadsheet program to update the values of existing degrees, or add new degrees -- one
degree per row. Every value you enter in each of the columns must be a value in one of the enumerations.  Each column 
has its own enumeration.
1. Run update  `python sv.py -a update`  The information in your `degrees.txt` file will be used to update degree 
information in VIVO.

