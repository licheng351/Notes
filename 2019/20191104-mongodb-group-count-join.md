## mongodb group count join
### keywords: group count aggregate lookup unwind arrayElemAt
```
db.getCollection("teachers").aggregate([
    {
        
        "$group": {
            _id: {
                schoolId: "$schoolId",
                level: "$level"
            },
            count: {
                $sum: 1
            }
        }
    },
    {
        $lookup: {
            from: 'schools',  // collection to join
            localField: '_id.schoolId',// field from the input documents
            foreignField: '_id',// field from the documents of the "from" collection
            as: 'schoolInfo' // output array field
        }
    },
    {
        $unwind: "$schoolInfo"
    },
    {
        $project: {
            "_id": 0,
            "schoolName": "$schoolInfo.name",
            "level": "$_id.level"
            "count": 1
        }
    }
])
```

```
db.getCollection("teachers").aggregate([
    {
        
        "$group": {
            _id: {
                schoolId: "$schoolId",
                level: "$level"
            },
            count: {
                $sum: 1
            }
        }
    },
    {
        $lookup: {
            from: 'schools',  // collection to join
            localField: '_id.schoolId',// field from the input documents
            foreignField: '_id',// field from the documents of the "from" collection
            as: 'schoolInfo' // output array field
        }
    },
    {
        $project: {
            "_id": 0,
            "schoolName": {
                $arrayElemAt: ["$schoolInfo.name", 0]
            },
            "level": "$_id.level",
            "count": 1
        }
    }
])
```


### References
- https://docs.mongodb.com/manual/reference/operator/aggregation/arrayElemAt/index.html
- https://github.com/Automattic/mongoose/issues/5735
