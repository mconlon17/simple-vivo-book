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

The serialize methods produces a string version of the instance variables and update definition.

```python
p = Pump()
print p.serialize() 
```

Future:  Should be suitable for round tripping back into the Pump as a state.  

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