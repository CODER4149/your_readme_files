### Create and insert into collection
```javascript
db.test.insertOne({ name: "John", age: 30 })
Find all documents in the collection
javascript
Copy code
db.test.find()
Insert data into the database using insertMany
javascript
Copy code
db.test.insertMany([
   { item: "journal", qty: 25, tags: ["blank", "red"], dim_cm: [ 14, 21 ] },
   { item: "notebook", qty: 50, tags: ["red", "blank"], dim_cm: [ 14, 21 ] },
   { item: "paper", qty: 100, tags: ["red", "blank", "plain"], dim_cm: [ 14, 21 ] },
   { item: "planner", qty: 75, tags: ["blank", "red"], dim_cm: [ 22.85, 30 ] },
   { item: "postcard", qty: 45, tags: ["blue"], dim_cm: [ 10, 15.25 ] }
])
Find documents matching tags key with "blank" (unordered)
javascript
Copy code
db.test.find({ tags: { $all: ["blank"] } })
Find documents matching tags key with "red" (ordered)
javascript
Copy code
db.test.find({ tags: "red" })
Find documents where dim_cm key is greater than 25
javascript
Copy code
db.test.find({ dim_cm: { $gt: 25 } })
Find documents matching tags key with "red" and "blank" (ordered)
javascript
Copy code
db.test.find({ tags: ["red", "blank"] })
Find documents matching dim_cm key with values greater than 22 and less than 30 using $elemMatch
javascript
Copy code
db.test.find({ dim_cm: { $elemMatch: { $gt: 22, $lt: 30 } } })
Find documents where the first element of dim_cm array is greater than 25
javascript
Copy code
db.test.find({ "dim_cm.1": { $gt: 25 } })
Find documents where the tags array has a length of 3
javascript
Copy code
db.test.find({ "tags": { $size: 3 } })
Insert data into the collection with nested arrays
javascript
Copy code
db.test.insertMany([
   { item: "journal", instock: [ { warehouse: "A", qty: 5 }, { warehouse: "C", qty: 15 } ] },
   { item: "notebook", instock: [ { warehouse: "C", qty: 5 } ] },
   { item: "paper", instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 15 } ] },
   { item: "planner", instock: [ { warehouse: "A", qty: 40 }, { warehouse: "B", qty: 5 } ] },
   { item: "postcard", instock: [ { warehouse: "B", qty: 15 }, { warehouse: "C", qty: 35 } ] }
])
Find documents where instock matches warehouse "A" and qty 5
javascript
Copy code
db.test.find({ "instock": { warehouse: "A", qty: 5 } })
Find documents where instock matches qty 5 and warehouse "A"
javascript
Copy code
db.test.find({ "instock": { qty: 5, warehouse: "A" } })
Find documents where instock array has a qty greater than 20
javascript
Copy code
db.test.find({"instock.qty":{$gt:20}})
Find documents where the first element of instock array has qty less than or equal to 20
javascript
Copy code
db.test.find({ 'instock.0.qty': { $lte: 20 } })
Find documents where instock array matches with qty: 5 and warehouse: "A"
javascript
Copy code
db.test.find({ "instock": { $elemMatch: { qty: 5, warehouse: "A" } } })
Find documents where instock array matches with qty between 10 and 20
javascript
Copy code
db.inventory.find({ "instock": { $elemMatch: { qty: { $gt: 10, $lte: 20 } } } })
Find documents where instock array qty is greater than 10 and less than or equal to 20
javascript
Copy code
db.inventory.find({ "instock.qty": { $gt: 10,  $lte: 20 } })
Find documents where instock array matches with qty: 5 and warehouse: "A"
javascript
Copy code
db.inventory.find({ "instock.qty": 5, "instock.warehouse": "A" })
Insert data with nested objects into the collection
javascript
Copy code
db.test.insertMany([
   { item: "journal", status: "A", size: { h: 14, w: 21, uom: "cm" }, instock: [ { warehouse: "A", qty: 5 } ] },
   { item: "notebook", status: "A",  size: { h: 8.5, w: 11, uom: "in" }, instock: [ { warehouse: "C", qty: 5 } ] },
   { item: "paper", status: "D", size: { h: 8.5, w: 11, uom: "in" }, instock: [ { warehouse: "A", qty: 60 } ] },
   { item: "planner", status: "D", size: { h: 22.85, w: 30, uom: "cm" }, instock: [ { warehouse: "A", qty: 40 } ] },
   { item: "postcard", status: "A", size: { h: 10, w: 15.25, uom: "cm" }, instock: [ { warehouse: "B", qty: 15 }, { warehouse: "C", qty: 35 } ] }
])
Find documents with status key equal to "A"
javascript
Copy code
db.test.find({ status: "A" })


# MongoDB Operations and Documentation

## Query Documents

### Find documents matching "status" key with value "A" and select "item" and "status" fields
```shell
db.test.find({ status: "A" }, { item: 1, status: 1 })
This query retrieves documents in the test collection where the "status" field is "A" and projects the "item" and "status" fields.

Find documents matching "status" key with value "A," select "item" and "status" fields, and remove "_id" field
shell
Copy code
db.test.find({ status: "A" }, { item: 1, status: 1, _id: 0 })
This query is similar to the previous one but excludes the "_id" field from the result.

Find documents matching "status" key with value "A" and exclude "status," "instock," and "_id" fields
shell
Copy code
db.test.find({ status: "A" }, { status: 0, instock: 0, _id: 0 })
This query retrieves documents with "status" equal to "A" and excludes "status," "instock," and "_id" fields from the result.

Find documents matching "status" key with value "A" and select "item," "status," and "size.uom" fields
shell
Copy code
db.test.find({ status: "A" }, { item: 1, status: 1, "size.uom": 1 })
This query retrieves documents with "status" equal to "A" and selects "item," "status," and "size.uom" fields.

Find documents matching "status" key with value "A" and exclude "size.uom" field
shell
Copy code
db.test.find({ status: "A" }, { "size.uom": 0 })
This query retrieves documents with "status" equal to "A" and excludes the "size.uom" field.

Find documents matching "status" key with value "A" and select "item" and "status" fields with the last element of "instock" array
shell
Copy code
db.test.find({ status: "A" }, { item: 1, status: 1, instock: { $slice: -1 } })
This query retrieves documents with "status" equal to "A" and selects "item" and "status" fields, along with the last element of the "instock" array.

Insert Documents
Insert multiple documents into the "test" collection
shell
Copy code
db.test.insertMany([
   { _id: 1, item: null },
   { _id: 2 }
])
This inserts two documents into the "test" collection, one with a null "item" and another without the "item" field.

Find Documents by Field Value and Type
Find documents with "item" key having a null value
shell
Copy code
db.test.find({ item: null })
This query retrieves documents where the "item" field is null.

Find documents with "item" key having a BSON type of 10
shell
Copy code
db.test.find({ item: { $type: 10 } })
This query retrieves documents where the "item" field has a BSON type of 10.

Find documents without an "item" key
shell
Copy code
db.test.find({ item: { $exists: false } })
This query retrieves documents where the "item" key does not exist.

Find documents with an "item" key
shell
Copy code
db.test.find({ item: { $exists: true } })
This query retrieves documents where the "item" key exists.

Update Documents
Update a document in the "students" collection
shell
Copy code
db.students.updateOne({ _id: 3 }, [{ $set: { "test3": 98, modified: "$$NOW" } }])
This query updates a document in the "students" collection by setting the "test3" field to 98 and updating the "modified" field to the current timestamp.

Update multiple documents in the "students2" collection
shell
Copy code
db.students2.updateMany(
  {},
  [
    {
      $replaceRoot: {
        newRoot: {
          $mergeObjects: [{ quiz1: 10, quiz2: 10, test1: 10, test2: 10 }, "$$ROOT"]
        }
      }
    },
    { $set: { modified: "$$NOW" } }
  ]
)
This query updates multiple documents in the "students2" collection by merging specified fields with the existing document and updating the "modified" field to the current timestamp.

Update documents in the "students3" collection
shell
Copy code
db.students3.updateMany(
  {},
  [
    {
      $set: {
        average: { $trunc: [{ $avg: "$tests" }, 0] },
        modified: "$$NOW"
      }
    },
    {
      $set: {
        grade: {
          $switch: {
            branches: [
              { case: { $gte: ["$average", 90] }, then: "A" },
              { case: { $gte: ["$average", 80] }, then: "B" },
              { case: { $gte: ["$average", 70] }, then: "C" },
              { case: { $gte: ["$average", 60] }, then: "D" }
            ],
            default: "F"
          }
        }
      }
    }
  ]
)
This query updates documents in the "students3" collection by calculating the average of the "tests" array, updating the "modified" field to the current timestamp, and assigning a grade based on the average score.






db.students4.insertMany( [
  { "_id" : 1, "quizzes" : [ 4, 6, 7 ] },
  { "_id" : 2, "quizzes" : [ 5 ] },
  { "_id" : 3, "quizzes" : [ 10, 10, 10 ] }
] )


db.students4.find()


db.students4.updateOne( { _id: 2 },
  [ { $set: { quizzes: { $concatArrays: [ "$quizzes", [ 8, 6 ]  ] } } } ]
)


db.temperatures.insertMany( [
  { "_id" : 1, "date" : ISODate("2019-06-23"), "tempsC" : [ 4, 12, 17 ] },
  { "_id" : 2, "date" : ISODate("2019-07-07"), "tempsC" : [ 14, 24, 11 ] },
  { "_id" : 3, "date" : ISODate("2019-10-30"), "tempsC" : [ 18, 6, 8 ] }
] )


db.temperatures.find()


db.temperatures.updateMany( { },
  [
    { $addFields: { "tempsF": {
          $map: {
             input: "$tempsC",
             as: "celsius",
             in: { $add: [ { $multiply: ["$$celsius", 9/5 ] }, 32 ] }
          }
    } } }
  ]
)


db.inventory.insertMany( [
   { item: "journal", qty: 25, size: { h: 14, w: 21, uom: "cm" }, status: "A" },
   { item: "notebook", qty: 50, size: { h: 8.5, w: 11, uom: "in" }, status: "P" },
   { item: "paper", qty: 100, size: { h: 8.5, w: 11, uom: "in" }, status: "D" },
   { item: "planner", qty: 75, size: { h: 22.85, w: 30, uom: "cm" }, status: "D" },
   { item: "postcard", qty: 45, size: { h: 10, w: 15.25, uom: "cm" }, status: "A" },
] );

db.inventory.deleteMany({})
db.inventory.find()

db.inventory.deleteOne( { status: "D" } )

db.pizzas.insertMany( [
   { _id: 0, type: "pepperoni", size: "small", price: 4 },
   { _id: 1, type: "cheese", size: "medium", price: 7 },
   { _id: 2, type: "vegan", size: "large", price: 8 }
] )
