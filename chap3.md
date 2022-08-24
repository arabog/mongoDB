# Creating and Manipulating Documents
## Inserting New Documents - ObjectId
Every document must have a unique _id value and it's required in every MongoDB document.  

## Inserting New Documents - insert() and errors
```
mongoimport --uri="mongodb+srv://<username>:<password>@<cluster>.mongodb.net/sample_supplies" sales.json

mongo "mongodb+srv://<username>:<password>@<cluster>.mongodb.net/admin"  

use sample_training

db.inspections.findOne();
```

## Inserting New Documents - insert() order: insert, order
```
Insert three test documents:
db.inspections.insert([ { "test": 1 }, { "test": 2 }, { "test": 3 } ])

Insert three test documents but specify the _id values:
db.inspections.insert([{ "_id": 1, "test": 1 },{ "_id": 1, "test": 2 }, { "_id": 3, "test": 3 }]) 

Find the documents with _id: 1
db.inspections.find({ "_id": 1 })

Insert multiple documents specifying the _id values, and using the "ordered": false option.
db.inspections.insert([{ "_id": 1, "test": 1 },{ "_id": 1, "test": 2 }, { "_id": 3, "test": 3 }],{ "ordered": false })

Insert multiple documents with _id: 1 with the default "ordered": true setting
db.inspection.insert([{ "_id": 1, "test": 1 },{ "_id": 3, "test": 3 }])

View collections in the active db
show collections

Switch the active db to training
use training

View all available databases
show dbs
```
Which of the following commands will successfully insert 3 new documents into an empty pets collection?
```
db.pets.insert([{ "_id": 1, "pet": "cat" },
                { "_id": 2, "pet": "dog" },
                { "_id": 3, "pet": "fish" },
                { "_id": 3, "pet": "snake" }])

db.pets.insert([{ "_id": 1, "pet": "cat" },
                { "_id": 1, "pet": "dog" },
                { "_id": 3, "pet": "fish" },
                { "_id": 4, "pet": "snake" }], { "ordered": false })

db.pets.insert([{ "pet": "cat" }, { "pet": "dog" },
                { "pet": "fish" }
```

## Updating Documents - Data Explorer
Select any invalid MongoDB documents from the given choices:

```
{ 
    "_id": 1,
    "pet": "cat",
    "attributes": [ 
        { "coat": "fur", "type": "soft" },
        { "defense": "claws", "location": "paws", "nickname": "murder mittens" } 
    ],
    "name": "Furball" 
}

{ 
    "_id": 1,
    "pet": "cat",
    "fur": "soft",
    "claws": "sharp",
    "name": "Furball" 
}

{ 
    "_id": 1,
    "pet": "cat",
    "attributes": { 
        "coat": "soft fur",
        "paws": "cute but deadly" 
    },
    "name": "Furball" 
}

NONE
```
## Updating Documents - mongo shell: $inc, $set, $push
updateOne(): If there are multiple docs that match a given criteria, only one of them will be updated, wcever one ds operation finds first.  

updateMany(): update all docs dt match a given query.  
**Fields:**    
**$inc** Increments the value of the field by the specified amount.  
**$set** Sets the value of a field in a document.  

**Arrays:**   
**$pop** Removes the first or last item of an array.  
**$pull** Removes all array elements that match a specified query.  
**$push** Adds an item to an array. 

Update **all** documents in the zips collection where the city field is equal to "HUDSON" by adding 10 to the current value of the "pop" field.
```
db.zips.updateMany({ "city": "HUDSON" }, { "$inc": { "pop": 10 } })
```
Update **a single** document in the zips collection where the zip field is equal to "12534" by setting the value of the "pop" field to 17630. Notice population is use instead of pop. Hence, a `new` key-pair value of "population": 17630  will be created.
	
```
db.zips.updateOne({ "zip": "12534" }, { "$set": { "population": 17630 } })
```

Update one document in the grades collection where the student_id is ``250`` *, and the class_id field is 339 , by adding a document element to the "scores" array.
Here push is used to update a particular field (incase of sub-document obj/arr)
```
db.grades.updateOne(
    { "student_id": 250, "class_id": 339 }, 
    { "$push": { "scores": { "type": "extra credit", "score": 100 }}}
)
```
Given a pets collection where each document has the following structure and fields:
```
{
 "_id": ObjectId("5ec414e5e722bb1f65a25451"),
 "pet": "wolf",
 "domestic?": false,
 "diet": "carnivorous",
 "climate": ["polar", "equatorial", "continental", "mountain"]
}
```
Which of the following commands will add new fields to the updated documents?
```
db.pets.updateMany(
    { "pet": "cat" },
    { "$push": { "climate": "continental", "look": "adorable" } }
)

db.pets.updateMany(
    { "pet": "cat" },
    { "$set": { "type": "dangerous", "look": "adorable" }}
)

These will not:
db.pets.updateMany(
    { "pet": "cat" },
    { "$set": { "climate": "continental" }}
)

db.pets.updateMany(
    { "pet": "cat" },
    {"$set": { "domestic?": true, "diet": "mice" }}
)
```
## Deleting Documents and Collections
Delete all the documents that have test field equal to 1.
```
db.inspections.deleteMany({ "test": 1 })
```
Delete one document that has test field equal to 3.
```
db.inspections.deleteOne({ "test": 3 })
```

Inspect what is left of the inspection collection.
```
db.inspection.find().pretty()
```

Drop the inspection collection. (i.e delete)
```
db.inspection.drop()
```
Use the inspection collection.
```
use inspection
```
Does removing all collections in a database also remove the database? **YES**  

Which of the following commands will delete a collection named villains?  
db.villains.drop();



