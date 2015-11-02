# Pump Test Cases

The VIVO Pump is deceptively simple.  A spreadsheet is used to update elements in VIVO.  What could go wrong?  Here we provide an overview of tests cases of various kinds.

# Entity Level Tests

1. No-op.  Round trip the entities by doing a get and an an update from the resulting spreadsheet.  Nothing should be added or subtracted.  NOTE: If filters are used, the get will "improve" the data and the first round trip will make
filter improvements to the data.  Subsequent round trips will be operating on the improved data and should then be a no-op.
1. Add entity.  Create new entities as per the definition.
1. Change entities.  See below.  Changes are at the element level.
1. Delete entities.  This is done using the "remove" column in the spreadsheet.

# Element level Tests

Individual elements in the spreadsheet are identified by row (entity) and column (path definition).  Path definitions lead to objects in VIVO triples.  Tests are conducted with and without qualifiers.

Unique|	Length|  ADC  | Qual |Examples
------|-------|-------|------|------
 Yes  |    1  |   Add | No   | Building Abbreviation
 Yes  |    1  | Change| No   | Building Abbreviation
 Yes  |    1  | Delete| No   | Building Abbreviation
 Yes  |    2  |   Add | No   | Grant start date
 Yes  |    2  | Change| No   | Grant start date
 Yes  |    2  | Delete| No   | Grant start date
 Yes  |    3  |   Add | No   | Org zip code
 Yes  |    3  | Change| No   | Org zip code
 Yes  |    3  | Delete| No   | Org zip code
 No   |    1  |   Add | No   | Person type(s); Person Research Area(s)
 No   |    1  | Change| No   | Person type(s); Person Research Area(s)
 No   |    1  | Delete| No   | Person type(s); Person Research Area(s)
 No   |    2  |   Add | No   | Grant Investigators
 No   |    2  | Change| No   | Grant Investigators
 No   |    2  | Delete| No   | Grant Investigators
 No   |    3  |   Add | No   | No example
 No   |    3  | Change| No   | No example
 No   |    3  | Delete| No   | No example

# Functional and component tests

The definitions support various functions through components of the software.  Examples include enumeration and filtering.  Each must be tested.

 1. Component tests.  Each software component needs unit tests.
 1. Filter tests.  Unit tests of filters.  Round trip testing of filters.
 1. Enumeration tests.  Unit tests of enumerations.  Round trip testing of enumerations.
 1. Handler tests.  Each handler (photo, PubMed, DOI) will need unit and integration tests.
