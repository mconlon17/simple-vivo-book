# Managing Organizations

You will want to have organizations in your VIVO.  Here are some reasons:

1. Your colleges, academic departments, administrative units, and laboratories are organizations in VIVO. VIVO can represent the organizational chart of your institution.
1. Organizations are where your people had positions before being at your institution.
1. Your people received degrees from organizations.
1. Organizations provided grant funding to your organization.
1. Your faculty have collaborators at other organizations.
1. Organizations are employers of your graduates.

Reports and visualizations use organizational data.

Create a spreadsheet of the organizations that you can use to manage the organizational data.  As organizations come and go, add and remove them from your spreadsheet.  As contact information changes, update your spreadsheet.  Use Simple VIVO to update VIVO using the values in your spreadsheet (see below).

Simple VIVO always allows three things to appear in a cell in a spreadsheet containing attributes for an organization:

1.  The value of the attribute.  See below.  The cell contains a name, or a phone number, or a zip code.
1.  The word None.  When None appears are the value of an attribute, Simple VIVO is directed to remove whatever attribute value it finds in VIVO.  For examples, see [[Simple VIVO|]]
1.  An empty cell, that is, nothing is in the cell. When Simple VIVO sees nothing in the cell, it does nothing -- it neither adds nor subtracts a value.  If your spreadsheet is mostly empty, it tells VIVO to mostly do nothing.  

Only filled cells are acted upon.  Cells with values are checked against VIVO.  If the value in the cell is different than the value in VIVO, the value in VIVO is replaced with the value in the cell.  If the value in the cell is the same as the value in VIVO, nothing is done. Cells withe the word None act to erase values from VIVO.  Whatever value is found in VIVO is removed, and no new value is provided.

# examples/orgs

[examples/orgs](https://github.com/mconlon17/vivo-pump/tree/master/examples/orgs) contains the files you need to manage organizations using Simple VIVO.

Your spreadsheet data will have the columns shown in the table below.  If you need more or fewer columns, your VIVO site administrator should be able to help you modify the `org_def.json` file distributed with Simple VIVO to provide the organizational attributes you need.

Column name  | Purpose
-------|-------
uri | The VIVO uri of the organization.  VIVO assigns a uri to every organization in VIVO.
remove | Used to remove organizations from your VIVO.
name | The name of the organization precisely as it will appear in VIVO
home_page | the URL of the home page of the organization
email | The email address of the organization
phone | The phone number of the organization
within | The name of another organization which is the parent of this one
address1 | Address line 1 for the organization
address2 | Address line 2 for the organization
city | The name of the city of the organization
state | The name of the state of the organization
zip | the sip code (postal code) of the organization
abbreviation | An abbreviation for the organization.  "NIH" for the National Institutes of Health, for example
overview | A paragraph of text regarding the organization
type| The organization's types.  See below.  Many organizations have multiple types.
successor | The name of the successor to the organization if it no longer exists

## Creating `org_enum.txt`

Run `make_enum.py` using:

    python make_enum.py

## Updating org values in VIVO

1. Get your orgs from vivo using `python sv.py -a get`
1. Edit `orgs.txt` using a text editor or a spreadsheet.  The file is delimited using the inter field delimiter, which defaults to the tab character.
1. Update your orgs using ``python sv.py -a update`
1. Add `org_add.rdf` to VIVO using the Site Admin Load RDF feature
1. Remove `org_sub.rdf` from VIVO using the Site Admin Remove RDF feature
1. Update the enumeration using `python make_enum.py`
1. Repeat these steps to make changes to your organizational data


## Adding orgs to VIVO

Adding orgs is simple -- just edit your spreadsheet to add a row.  Put as much data about the organization as you
have on the row in the appropriate columns.  Leave the rest of the columns blank.  In particular, leave the `uri` column blank.  Simple VIVO will assign a uri to your organization when it is added.

Follow the rest of the steps described for updating yourorg values.  Adds and updates can be combined in the same spreadsheet.

## Removing orgs from VIVO

Removing orgs is also very simple -- just edit your spreadsheet and put the word "remove" in the `action` column.
Each organization that has `remove` in the action column will be removed from VIVO.

## Maintaining subsets of orgs

You may find that you would like to have different kinds of organizations in different spreadsheets to simplify data management.  For example, you may wish to have your internal organizations in one spreadsheet and external organizations in another.  

To maintain subsets, follow the steps below:

1.  Create appropriate folders for your work.  You may want to manage the two collections from two different folders.
1. Copy the def file into each folder
1. Modify the def file to select the orgs of interest.
1. Copy the sv.cfg file into each folder
1. Modify the sv.cfg file to use the name of the definition file for your subset.  Modify the rdfprefix and source file name as appropriate to help you manage the subset.
1. Run your gets and updates as above in each folder for each subset.


## Frequently Asked Questions

*Do I need to have all the possible columns in my spreadsheet?*

No.  The only columns you need are the name column and the columns you want to update.

*Do I need to have all the organizations in my spreadsheet?*

No.  The only rows you need are for the organizations you want to update.

*So if I wanted to update email addresses for the departments in my college all I would need is the names of the departments and their email addresses?*

Yes.

*But sometimes two organizations might have the same name -- the chemistry department at my school and the chemistry department at Berkeley, for example. How do I handle that?*

There are two approaches.  

The first is simple -- include the name of the school in the name of the org for any org outside your institution.  So, for example, at your school, you would name the chemistry department "Chemistry" and the chemistry department at Berkeley would be called "Chemistry (UC Berkeley)"

The second approach is more complex, but will allow you to avoid having to put the name of the school in the name of the organization.  When using Simple VIVO, the spreadsheet provided by Simple VIVO contains an additional column that you did not enter.  That column is called "uri."  VIVO supplies a uri for each thing in VIVO.  Every org has a uri.  You can use uri instead of name to identify your organizations.  If you use a spreadsheet with uri as a column, Simple VIVO will use the uri (instead of name!) to find and update organizations.  Two organizations can have the same name since they have different uri.

*What if I use a column name that Simple VIVO does not know?*

Nothing will be done.  The log will contain messages indicating which columns were unknown.  Always check the log after every run to see what Simple VIVO has done.  Only column names that are in your spreadsheet **and** in the definition file are processed.  All other columns are ignored.  

For a `get` this means that Simple VIVO will get all the columns defined in the definition file and return them as columns in a spreadsheet.

For an `update` this means that if a column appears in your spreadsheet that is not defined in the definition file, it will be ignored during the update.  You can have a "notes" column, for example, where you leave notes to yourself regarding additional research that should be done regarding a particular entity.

For an `update` in which all the columns in the spreadsheet are defined, all the columns in the spreadsheet will be processed.  If there are additional column definitions in the definition file and those columns are not in your spreadsheet, these additional definitions will not be used.   This makes it easy to have a definition file that defines many columns and then only use a few columns in a particular spreadsheet.  You might have a spreadsheet that updates organizational contact information and a separate spreadsheet that updates `within` and `successor` information, for example.

*What if I give a new organization name -- one that VIVO hasn't seen before?*

Simple VIVO will add the organization to VIVO and give it all the data you have on the the row in your spreadsheet.  It will assign a new URI.  The next time you do a `get`, Simple VIVO will show all your organizations, including the ones you added.

*How do I remove an organization?*

Create a spreadsheet with two columns.  In the uri column, give the URI of the organization to be removed.  Create a second column with the column heading "action".  On the row under action, put "remove".

*How do I remove values for some organizations and not others?*

Use "None" to remove a value from an organization.  

*What happens if I leave the value in a column for an organization blank?*

Nothing happens.  This is different from specifying a value, or specifying "None" to remove a value.  So three things can appear in a column and Simple VIVO takes three different actions:

* If a value appears in the column, the value in VIVO is replaced with the value you specify.
* If the value "None" appears in the column, Simple VIVO removes the value in VIVO.  The org in VIVO will have no value for the column containing "None".
* If the value is blank, Simple VIVO does nothing.  The value in VIVO, if there is one, remains unchanged.


