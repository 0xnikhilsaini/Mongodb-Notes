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

```javascript

db.collection.aggregate(
    [
        {
            $addFields: {
                formattedDate: { // An extra field "formattedDate" is added in each document which can be compared later through pipeline using $match
                    $dateToString: {
                        format: "%Y-%m-%d",
                        date: "$date" // in "$date" date is variable from db
                    }
                }
            }
        },
        {
            $match: {
                formattedDate: {
                    $eq: "2020-07-12" // here you can provide your input date yyyy-mm-dd
                }
            }
        }
    ]
)

```


- The **$group** operator groups documents by the age field, creating a new document for each unique age value.
- The _id field in the group stage specifies the field based on which the docuemtns will be grouped.

## Group teachers by age and show all teachers names per age group
```javascript
$group:{_id:expression,field1:expression, field2:expression, ...}
```

    MongoDB aggregation is a process in which data is grouped together and transformed into a single, more meaningful data set. It enables users to perform a variety of operations on their data, including filtering, transforming, and summarizing data, as well as creating new virtual fields. Here are some notes on MongoDB aggregation:

Pipelining: MongoDB aggregation uses a pipeline approach, where the input documents are transformed through a series of stages to produce the desired result. Each stage operates on the result set of the previous stage.

Aggregation stages: The most commonly used stages in MongoDB aggregation are $match, $project, $group, $sort, $skip, and $limit.

$match stage: The $match stage is used to filter the input documents based on certain criteria.

$project stage: The $project stage is used to transform the input documents by selecting only the desired fields and reshaping the data.

$group stage: The $group stage is used to group input documents based on a specified expression and produce summary statistics for each group.

$sort stage: The $sort stage is used to sort the documents based on a specified field or expression.

$skip and $limit stages: The $skip stage is used to skip a specified number of documents, while the $limit stage is used to limit the number of documents that are returned.

Aggregation expressions: MongoDB supports a variety of aggregation expressions, such as arithmetic, string, and conditional expressions, that can be used to perform calculations and transformations on the input data.

These are some of the basic concepts of MongoDB aggregation. It is a powerful tool for data analysis and can help you to quickly generate insights from your data.

