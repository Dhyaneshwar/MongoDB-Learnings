# Find

The find commands are used to retrieve one or more documents from a collection.

### Find commands

The available find commands are:-

1.  `findOne`
2.  `find`

## Reference Table

| Database => Shop | Collection => Products |
| ---------------- | ---------------------- |

| \_id | name  | price | description      |
| ---- | ----- | ----- | ---------------- |
| 1    | Chair | $120  | A comfy chair    |
| 2    | Book  | $50   | Exciting book    |
| 3    | Car   | $5000 | Good looking car |

## db.collection.find()

### Syntax

`db.collection.find(query, projection)`

- To return all documents in a collection, omit this parameter or pass an empty document ({}).
  - `find()` or `find({})`
- The find() method returns a cursor to the documents instead of the actual document itself.

### Example

```
db.Products.find({},{_id:0,description:0})
```

##### Result:

_[{ name:"Chair", price: "$120" }, { name:"Book", price: "$50" }, { name:"Car", price: "$5000" }]_

### Projections

The `projection` parameter determines which fields are returned in the matching documents.
As we can see in the above example the projection parameter was set for _\_id_ and _description_ as 0. This refers to exclusion.
Thats why the _\_id_ and _description_ are not present in the result.

#### `_id` Field Projection

The `_id` field is included in the returned documents by default unless you explicitly specify `_id: 0` in the projection to suppress the field.

#### Inclusion or Exclusion

A `projection` _cannot_ contain _both_ include and exclude specifications, with the exception of the `_id` field:

- In projections that _explicitly include_ fields, the `_id` field is the only field that you can _explicitly exclude_.

  ![Inclusion](/Assests/Images/InclusionProjection.jpg)
- In projections that _explicitly excludes_ fields, the `_id` field is the only field that you can _explicitly include_; however, the `_id` field is included by default.

  ![Exclusion](/Assests/Images/ExclusionProjection.jpg)

## Understanding CURSOR

- The `db.collection.find()` method returns a **cursor**.
  This mean, that when we use the `find()` query it will not return all the documents in the collection. Instead, it will return a cursor pointer.
- If the returned cursor is not assigned to a variable, then the cursor is automatically iterated up to 20 times to print the first 20 documents.
  The 21st document and above will be displayed when the user types `it`.

### Manually iterating the cursor

`let myCursor = db.products.find({},{description:0})`

1. When the stored variable is entered in the shell, then the documents will be displayed.
   > \> myCursor
   >
   > ##### Result:-
   >
   > {\_id: 1 , name: "Chair", price: $120},
   > {\_id: 2, name: "Book", price: $50},
   > {\_id: 3, name: "Car", price: $5000}
2. If the collection is having more than 20 documents, then when we type `myCursor` in the shell, we get:-
   > ... (first 20 documents are displayed)
   >
   > \>Type **it** for more
3. Now, if we either type **`it`** or once again type the user cursor variable, `myCursor`, the remaining document will be printed.
   Once all the document that are returned by `find()` is displayed, then the cursor point will be exhausted, i.e. it will be pointing to the index after the last document.
   So now if you enter `myCursor` nothing will be displayed.
4. **while**

```
	while(myCursor.hasNext()){
		printjson(myCursor.next())
	}
```

5. **forEach**

```
	myCursor.forEach(cursor=>{
		printjson(cursor)
	})
```

By using the above 2 iterators, we will be able to point to all the values (even more than 20) at a time.
After this iteration, the `myCursor` will be exhausted, so nothing will be displayed when queried again.

7. **toArray**

   This is used to iterate the cursor and return the document in an array.

```
	let documentArray = myCursor.toArray()
	> documentArray[3] (will display the index 3 of document)
```

Since `toArray` loads all the documents returned by the cursor to the RAM, the stored variable (documentArray), can be used repeatedly unlike the cursor itself.

## db.collection.findOne()

### Syntax

`db.collection.findOne(query, projection)`

- Returns one document that satisfies the specified query criteria on the collection or view.

- If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.

> **Note:**
>
> 1.  The `_id` field is included in the returned documents by default unless you explicitly specify \_id: 0 in the projection to suppress the field.
> 2.  Although similar to the find() method, the findOne() method returns a document rather than a cursor.

### Example

```
db.Products.findOne({_id:1},{_id:0,description:0})
```

##### Result:

_{ name:"Chair", price: "$120" }_
