# Merging Entities

On occasion, you may find that the same "thing" appears in VIVO twice -- the same person, the same organization, 
the same paper.  This may happen when two different processes are being used to manage data -- automated processes
are loading people while manual edits are also adding people.  Or duplicates may occur because one or more of the 
entities is not completely identified.  You may expect people to have ORCID identifiers, but perhaps a person
has been added without one, and added again with one.  Whatever the cause, you may find that when reviewing the
rows in a spreadsheet, two or more of the rows are referring the same thing.

A merge is a way for you to combine two or more entities into a single entity.  You will specify which entity you
wish to keep (the primary entity) and which you wish to combine (the secondary entities) to the primary.

To specify a merge, you will need to designate a primary, and one or more secondaries to merge to the primary.  If you
do not specify a primary, no merge will occur.  If you do not specify one or more secondaries, no merge will occur.

## Specifying Primary and Secondary entities for Merge

To specify the primary and secondary entities for a merge, you will use the `action` column in your update spreadsheet.
In the action column, use any text you like to specify the primary entity for the merge.  You may choose to use the
letter `a` for example.  To specify the secondaries to merge to the primary, use the very same text followed by the
digit `1`.  So if you used `a` for the primary, you will use `a1` to indicate the secondary entities to merge to the
primary.

You can specify as many primary entities for merging as you wish.  And you may specify any number of secondaries to 
merge to the primary.  And primaries and secondaries may appear in an any order in your spreadsheet.

## An Example of Merging Organizations

Suppose your organizational data looks like:

uri | name
----|----
http://vivo.yourschool.edu/n8828 | Harvard University
http://vivo.yourschool.edu/n8910 | University of Iowa
http://vivo.yourschool.edu/n1402 | Harvard University
http://vivo.yourschool.edu/n2245 | Stanford University
http://vivo.yourschool.edu/n2249 | Cambridge University
http://vivo.yourschool.edu/n8991 | Harvard University
http://vivo.yourschool.edu/n9012 | University of Toronto
http://vivo.yourschool.edu/n9000 | Cambridge University
http://vivo.yourschool.edu/n9234 | Bucknell University
http://vivo.yourschool.edu/n9231 | Louisiana State University
http://vivo.yourschool.edu/n9432 | Harvard University

We see that there are several copies of Harvard and two copies of Cambridge.  Upon inspection we determine that
`http://vivo.yourschool.edu/n1402` should be the primary and all others secondary for a merge of the Harvard
entities and that `http://vivo.yourschool.edu/n9000` should be the primary for Cambridge and the other the secondary.

Your update spreadsheet will look like the one below.  We use `a` to indicate the entities involved in the Harvard 
merge, and `b` to indicate the Cambridge entity merge participants.  There are four Harvard rows.  One is the primary
the other three are secondary.  There are two Cambirgde rows.  One is the primary and the other is secondary.

All other rows have a blank in the action column.  As always in Simple VIVO, blank means "do nothing."  These rows will
not be involved in the merge.

uri | name | action
----|----|----
http://vivo.yourschool.edu/n8828 | Harvard University | a1
http://vivo.yourschool.edu/n8910 | University of Iowa |
http://vivo.yourschool.edu/n1402 | Harvard University | a
http://vivo.yourschool.edu/n2245 | Stanford University |
http://vivo.yourschool.edu/n2249 | Cambridge University | b1
http://vivo.yourschool.edu/n8991 | Harvard University | a1
http://vivo.yourschool.edu/n9012 | University of Toronto |
http://vivo.yourschool.edu/n9000 | Cambridge University | b
http://vivo.yourschool.edu/n9234 | Bucknell University | 
http://vivo.yourschool.edu/n9231 | Louisiana State University |
http://vivo.yourschool.edu/n9432 | Harvard University | a1

You use the spreadsheet with the action column to update VIVO as always:

    python sv.py -a update
    
You add and remove RDF from VIVO.  Use a get to see the result:

    python sv.py -a get
    
Your spreadsheet will looks like the one below:

uri | name
----|----
http://vivo.yourschool.edu/n8910 | University of Iowa
http://vivo.yourschool.edu/n1402 | Harvard University
http://vivo.yourschool.edu/n2245 | Stanford University
http://vivo.yourschool.edu/n9012 | University of Toronto
http://vivo.yourschool.edu/n9000 | Cambridge University
http://vivo.yourschool.edu/n9234 | Bucknell University
http://vivo.yourschool.edu/n9231 | Louisiana State University

The duplicate Harvard secondary entities have been merged to the primary Harvard entity and are no longer found in VIVO.
Anything associated with those entities is now associated with the primary (and only) Harvard entity.  The same
has happened for the secondary Cambridge entity.

## The Difference Between Merge and Remove

We might have used `Remove` in the `action` column to remove all the secondary entities and leave only the primaries.  
What is the difference remove and merge?

The difference has to do with things associated with the secondary entities.  Organizations might have addresses, or 
phone numbers, web pages, sub organizations or other data.  In a merge, all the data from the secondaries is associated
the primary.  Nothing is lost.  In a remove, all the data from the secondaries is removed as well.  Associations and
data values associated with the secondary are removed.

Both operations may have negative consequences:

1. In a remove, data may be lost.
1. In a merge, multiple values for the same attribute may be associated with the primary.  You may need to "clean up"
the primary after a merge to insure it has the data values you want, and only the data values you want.

In general, use `remove` only in very simple cases where the entity to be removed has *no* data of interest.

Use `merge` to combine partial copies of entities.  But always be prepared to clean up the resulting primary entity.



