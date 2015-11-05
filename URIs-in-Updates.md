# URIs in Updates

The `uri` column in your spreadsheet indicates to Simple VIVO how each row should be handled.  There are
several cases:

uri | Simple VIVO result
---|----
blank | The data on the row will be added.  A uri will be created by Simple VIVO using the `uriprefix`.  The data on the row will be added to VIVO referring to the new uri.
found uri | The data on the row will update the entity with the found uri.  
not found uri | The data on the row will be added.  The uri you specified, that was not found in VIVO, will be used.
invalid uri | If the value in the uri is not a valid uri, Simple VIVO will stop with an error message.  In particular, the word "None" is not valid in the the uri column.

## Additional Notes

1.  The uri column is not like other data columns.  blank means "create a uri".  None is an invalid uri and will
result in an error.  A found uri indicates an update.  An unfound uri indicates an add.
1.  The way uris are used in update supports 'round tripping'.  A get will return all the entities in VIVO along
with their uri.  A subsequent update using the uri found by get will result in updates to the uri in VIVO.  And
if you choose to add new rows with blank uri to the spreadsheet returned by a get, these rows will be assigned
new uri.  Everything works as expected.
1.  The way uris are used in update supports loading data sets produced by others that contain their uri.  If the uri in these datasets will not be generated by your `uriprefix`, then they can be added safely. if the dataset
 produced by others does not have uri, then they can be added safely -- Simple VIVO will generate uri using your 
 `uriprefix`
 
## A cautionary note

Perhaps you have noticed a potentially dangerous consequence of the uri processing rules.  If your spreadsheet has
URI in it that are URI of entities in your VIVO, **they will be treated as updates**.  If you intended to add
entities, you must make sure that the uri you specify will not _collide_ with uri already in your VIVO.  

Data sets created by others can have uri they create that will not be created by your `uriprefix`, or they can have 
no uri at all and Simple VIVO will create new ones that are not in your VIVO.  But if a dataset created by others
has uri in it, and those uri could be generated by your `uriprefix`, you could have a bad result, with the
data produced by others being used to update existing VIVO entities rather than creating new ones.

Be sure that the uri used in your spreadsheet are not in your VIVO if you expect Simple VIVO to add them.
 
 