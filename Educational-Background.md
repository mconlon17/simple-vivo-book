# Managing Educational Background

VIVO can be used to represent the education backgrounds of your people.  Each person can have one or degrees.  These will
be displayed on profile pages and can be used in queries.  Simple VIVO can be used to manage 
educational backgrounds.

To add education backgrounds to VIVO, we need to know several pieces of information for each degree:

1. Who obtained the degree?
1. What degree was obtained?
1. From what institution?
1. What is the date of the degree?
1. What is the field of study for the degree?

Each of these attributes is optional.  

## Managing Enumerations

Each is represented by an enumeration.  This guarantees that all the information regarding education in VIVO is 
"coded" -- there are no open-ended text fields associated with educational background, and "linked" -- we can 
  easily find all the people with a particular degree, all the people who have degrees from particular institutions,
  and all other combinations of attributes.  If a value for one of the attributes can not be 
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

The field of study enumeration is managed by hand -- if you have fields of study that you would like to be able to 
represent in VIVO, edit the `field_enum.txt` file with a text editor and add a row for each such field of study.

## get and update as always

1. Edit the `sv.cfg` file to provide the query parameters for your VIVO.  Your system administrator can help you 
with this.
1. Run get:  `python sv.py -a get`
The result will be a `degrees.txt` file which you can open in a spreadsheet to edit the degrees for your people. 
Every value you enter in each of the columns should be a value in one of the enumerations.  Each column has its 
own enumeration.
1. Edit your enumerations as needed to provide additional values for degrees and fields of study.  To add 
universities or other schools to your VIVO and make them available for your education work, use the orgs example 
to add the organizations, then run make_enum to update your enumerations.  The new schools are now available for 
putting educational background in VIVO.
1. Run update  `python sv.py -a update`  The information in your `degrees.txt` file will be used to update degree 
information in VIVO.

