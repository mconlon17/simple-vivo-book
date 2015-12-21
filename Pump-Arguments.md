# Pump Arguments

The Pump has two arguments.  Each has a default.  They can appear in any order.

`defn` gives the name of the JSON definition file.  The default is `pump.json`

`src` gives the name of the file containing the CSV data to be used for an update, or, for a get action, the name
of the file that will be created by the pump.  The default is `pump.txt`

## Pump instance variables

Any of the following can be set to further define the work of the Pump.

`queryuri` gives the URI of the SPARQL API interface to your VIVO.  That is, the URI that will be used to make 
queries to your VIVO.  This URI is new in VIVO 1.6.  The Pump requires VIVO 1.6 or later.  The sample value is for 
a VIVO Vagrant, a test instance.

`username`  gives the username (VIVO may call this "email") for an account that is authorized on your VIVO to execute 
the VIVO SPARQL API.

`password`  gives the password of the account that is authorized on your VIVO to execute the VIVO SPARQL API.  That 
is, the password to the account specified by the `username`

`prefix`  gives the SPARQL prefix for your VIVO.  SPARQL queries typically use PREFIX statements to simplify the 
specification of URI in SPARQL statements.  The value of the prefix parameter should be the collection of PREFIX 
statements used at your VIVO.
 
`action` is the desired Pump action.  There are five choices:  test, update, get, summarize and serialize.  When the
pump is used by Simple VIVO, the action is typically specified on the command line to override the value in the 
config file and make explicit what action Simple VIVO is performing.

`inter` is the inter field separator character used for your spreadsheets.  a CSV file would have `inter = ,`, a 
tab separated spreadsheet (recommended) would have `inter = tab`.  Note the word "tab".  the Simple VIVO config file 
uses this to specify a tab as a field separator.  Another popular choice for field separator is the "pipe" 
character "|".  Pipe and tab are used as separators because these characters do not appear in literal values in VIVO.

`intra` is the intra field separator character used to separate multiple values in a single spreadsheet cell.  
The default is a semi-column.

`filter`  (default `true`) set to `true` indicates that filters specified in the definition file should be used.  Set to `false` 
indicates filters are not to be used.

`rdfprefix` indicates the naming convention to be used by the pump when creating RDF files.  The Pump will create
add and sub RDF with the names `rdfprefix`_add.rdf and `rdfprefix`_sub.rdf

`uriprefix`  indicates the format of any URI to be created by the update process.  URI will have random digits 
following the prefix.  So, for example, if your uriprefix is `http://vivo.school.edu/n`, Simple VIVO will create 
new entities with URI that look like `http://vivo.school.edu/nxxxxxxxx` where `xxxxxxxx` are random digits.