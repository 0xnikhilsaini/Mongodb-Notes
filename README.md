# Mongodb-Notes# Mongodb Aggregator Notes
## This is mongodb aggregator notes

- It groups the data from multiple documents into a single documents based on the specified expression

### AGGREGATION PIPELINE

- The aggregation process in MongoDB consists of several stages, each stage transforming the data in some way.
- The output of one stage is fed as the input to the next stage, and so on, until the final stage produces the desired result.
- MongoDb provides serveral built-in aggregation pipeline stages to perform various operations on the data, such as **$group**, **$sum**, **$avg**,**$min**,**$max**, etc.


```javascript
db.collection.aggregate(pipeline, options)
```

```javascript
collage> db.teachers.aggregate([$match:{gender:"male"}])
```
## Group teachers by age
```javascript
collage> db.teachers.aggregate([$group:{_id:"$age"}])
```
- The **$group** operator groups documents by the age field, creating a new document for each unique age value.
- The _id field in the group stage specifies the field based on which the docuemtns will be grouped.

## Group teachers by age and show all teachers names per age group
```javascript
$group:{_id:expression,field1:expression, field2:expression, ...}
```

