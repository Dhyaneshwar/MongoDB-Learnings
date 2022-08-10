# Find

The find commands are used to retrieve one or more documents from a collection.

### Find commands

The available find commands are:-

1. `findOne`
2. `find`

## db.collection.findOne()

### Syntax

    > db.collection.findOne(query, projection)

- Returns one document that satisfies the specified query criteria on the collection or view.

- If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.

  > Note:

1. The `_id` field is included in the returned documents by default unless you explicitly specify \_id: 0 in the projection to suppress the field.
2. Although similar to the find() method, the findOne() method returns a document rather than a cursor.
