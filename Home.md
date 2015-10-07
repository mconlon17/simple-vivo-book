# Introduction to the Pump

The VIVO Pump (under development), provides a means for managing VIVO data using spreadsheets.  Rows and columns in 
spreadsheets represent data in VIVO.  The Pump update method takes spreadsheet data, and a definition file, and 
returns VIVO RDF (add and subtract) for updating VIVO with the values in the spreadsheet.  The Pump get method
uses the definition file and the data in VIVO to create a spreadsheet.  Schematically:

    update method:  Spreadsheet Data    =>   The Pump      =>    VIVO RDF   =>   VIVO
                                           + definition file
    
    get method:     Spreadsheet Data    <=   The Pump      <=    VIVO RDF   <=   VIVO
                                           + definition file
  
The same definition file can be used for get and update, and the spreadsheet resulting from a get can be used in a
subsequent update, providing a "round trip" capability.  That is, you can "get" data, improve it manually or
programmatically, and use it to "update" VIVO.

## Work in Progress

The Pump is under active development, and beta testing at the University of Florida.  

See [Issues](https://github.com/mconlon17/vivo-pump/issues) for work in progress, features to be added, and bugs to be 
addressed.

## Testing the Pump

* [Pump Test Cases](Pump-Test-Cases.md)
* [Simple VIVO Tests](Simple-VIVO-Test-Cases.md)

## Pump References

* [The Pump API](The-Pump-API.md)
* [The Pump Definition File](The-Pump-Definition-File.md)
