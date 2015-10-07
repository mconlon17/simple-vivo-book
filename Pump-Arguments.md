# Pump Arguments

All Pump arguments are keyword.  Each has a default.  They can appear in any order.

`queryuri` gives the URI of the SPARQL API interface to your VIVO.  That is, the URI that will be used to make queries to your VIVO.  This URI is new in VIVO 1.6.  The Pump requires VIVO 1.6 or later.  The sample value is for a VIVO Vagrant, a test instance.

`username`  gives the username (VIVO may call this "email") for an account that is authorized on your VIVO to execute the VIVO SPARQL API.

`password`  gives the password of the account that is authorized on your VIVO to execute the VIVO SPARQL API.  That is, the password to the account specified by the `username`

`prefix`  gives the SPARQL prefix for your VIVO.  SPARQL queries typically use PREFIX statements to simplify the specification of URI in SPARQL statements.  The value of the prefix parameter should be the collection of PREFIX statements used at your VIVO.  Note that formatting of the parameter -- each PREFIX statement begins on a new line, including the first one.  Each is indented by four spaces.  This is recommended.
 
`action` is the desired Pump action.  There are four choices:  update, get, summarize and serialize.  Often these are specified on the command line to override the value in the config file and make explicit what action Simple VIVO is performing.

`verbose` is set to `true` to have the Pump produce output regarding the status and progress of its actions.  The default is `false` which produces limited output showing the the datetime the action started, the number of entities effected, and the datetime the action was completed.

`inter` is the inter field separator character used for your spreadsheets.  a CSV file would have `inter = ,`, a tab separated spreadsheet (recommended) would have `inter = tab`.  Note the word "tab".  the Simple VIVO config file uses this to specify a tab as a field separator.  Another popular choice for field separator is the "pipe" character "|".  Pipe and tab are used as separators because these characters do not appear in literal values in VIVO.

`intra` is the intra field separator character used to separate multiple values in a single spreadsheet cell.  The default is a semicolumn.

`nofilters`  set to `true` indicates that filters specified in the definition file should not be used.  Set to `false` indicates filters are to be used as normal.

`defn`  specifies the name of the file that contains the definition file, in JSON format, to be used by Simple VIVO.

`src`  specifies the name of the input source file (for update) or output file (for get).

`uriprefix`  indicates the format of any URI to be created by the update process.  URI will have random digits following the prefix.  So, for example, if your prefix is `http://vivo.school.edu/n`, Simple VIVO will create 
new entities with URI that look like `http://vivo.school.edu/nxxxxxxxx` where `xxxxxxxx` are random digits.