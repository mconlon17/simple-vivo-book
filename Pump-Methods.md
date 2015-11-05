# Pump Methods

The methods and instance variables of the Pump are used by programmers to define and perform the work of the pump.

## Pump Methods

The Pump has four methods.  None of the pump methods have parameters.  Each is called simply by name.  See below.

### summarize

The summarize() method describes the operation that will be performed by the Pump as configured.  It lists the values of the instance variables, the enumerations, the get_query, and the update_def. A single string with newlines is produced.

```python
p = Pump()
print p.summarize()
```

### serialize

The serialize() method produces a string version of the instance variables and update definition.

```python
p = Pump()
print p.serialize() 
```

Future:  Should be suitable for round tripping back into the Pump as a state. 

### test

The test() method uses the current configuration to test the connection to your VIVO.

```python
p = Pump()
print p.test()
```

A sample output is shown below:

```
2015-11-05 09:17:06.206090 Test results
Update definition	pump_def.json read.
Source file name	pump_data.txt.
Enumerations read.
Filters	True
Verbose	False
Intra field separator	;
Inter field separator		
VIVO SPARQL API URI	http://localhost:8080/vivo/api/sparqlQuery
VIVO SPARQL API username	vivo_root@school.edu
VIVO SPARQL API password	v;bisons
VIVO SPARQL API prefix	
PREFIX rdf:      <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs:     <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd:      <http://www.w3.org/2001/XMLSchema#>
PREFIX owl:      <http://www.w3.org/2002/07/owl#>
PREFIX swrl:     <http://www.w3.org/2003/11/swrl#>
PREFIX swrlb:    <http://www.w3.org/2003/11/swrlb#>
PREFIX vitro:    <http://vitro.mannlib.cornell.edu/ns/vitro/0.7#>
PREFIX wgs84:    <http://www.w3.org/2003/01/geo/wgs84_pos#>
PREFIX bibo:     <http://purl.org/ontology/bibo/>
PREFIX c4o:      <http://purl.org/spar/c4o/>
PREFIX cito:     <http://purl.org/spar/cito/>
PREFIX event:    <http://purl.org/NET/c4dm/event.owl#>
PREFIX fabio:    <http://purl.org/spar/fabio/>
PREFIX foaf:     <http://xmlns.com/foaf/0.1/>
PREFIX geo:      <http://aims.fao.org/aos/geopolitical.owl#>
PREFIX obo:      <http://purl.obolibrary.org/obo/>
PREFIX ocrer:    <http://purl.org/net/OCRe/research.owl#>
PREFIX ocresd:   <http://purl.org/net/OCRe/study_design.owl#>
PREFIX skos:     <http://www.w3.org/2004/02/skos/core#>
PREFIX uf:       <http://vivo.school.edu/ontology/uf-extension#>
PREFIX vcard:    <http://www.w3.org/2006/vcard/ns#>
PREFIX vitro-public: <http://vitro.mannlib.cornell.edu/ns/vitro/public#>
PREFIX vivo:     <http://vivoweb.org/ontology/core#>
PREFIX scires:   <http://vivoweb.org/ontology/scientific-research#>
Prefix for RDF file names	pump
Uriprefix for new uri	http://vivo.school.edu/individual/n
Sample new uri	http://vivo.school.edu/individual/n3171760016
Simple VIVO is ready for use.
2015-11-05 09:17:06.812863 Test end
2015-11-05 09:17:06.812952 Finish
```

### get

get() performs the Pump get operation, querying VIVO according to the definition, creating a spreadsheet data structure, and writing that structure to the output file specified by the Pump instance variables.  get() returns the number of rows in the output spreadsheet.

```python
p = Pump()
nrows = p.get()

### update

update() performs the Pump update operation, using source data provided in a spreadsheet and a definition file supplied as JSON.  The update queries VIVO for current values, adds and removes entities as directed in 
the spreadsheet and adds, removes and updates attributes values as supplied in the spreadsheet.  update() returns an add graph and a subtract graph, which can be serialized using rdflib.  For example:

```python
[add_graph, sub_graph] = p.update()
add_file = open(args.rdfprefix + '_add.rdf', 'w')
print >>add_file, add_graph.serialize(format='nt')
add_file.close()
```