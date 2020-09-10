## mongodb toggle operations for update

1. mongodb toggle update a field with the `$bit` operator to result `0 -> 1 or 1 -> 0`.
    The `$bit` operator supports bitwise and, bitwise or, and bitwise xor (i.e. exclusive or) operations, only use this operator with integer fields (either 32-bit     integer or 64-bit integer).
    ```
    { $bit: { <field>: { <and|or|xor>: <int> } } }

    example: 
    prepare data:  
    db.demo.insert([ { "_id": 1, "is_hidden": NumberInt(0) }, { "_id": 2, "is_hidden": NumberInt(1) }, { "_id": 3, "is_hidden": NumberInt(1) } ]);

    you can toggle update the is_hidden field with `xor operation` to the result of a bitwise xor operation between the current value.

    db.demo.update(
       { _id: 3 },
       { $bit: { is_hidden: { xor: NumberInt(1) } } }
    )
    ```

2. mongodb toggle update a field with the `$switch` operator update with Aggregation Pipeline. Since MongoDB 4.2, you can use the aggregation pipeline for update operations. 
    ```
    db.demo.updateMany(
       { },
       [
         { $set: { is_hidden: { $switch: {
                               branches: [
                                   { case: { $eq: [ "$is_hidden", 1 ] }, then: 0 },
                                   { case: { $eq: [ "$is_hidden", 0 ] }, then: 1 }
                               ],
                               default: 0
         } } } }
       ]
    )
    ```


### References
- https://docs.mongodb.com/v2.6/reference/operator/update/bit/
- https://docs.mongodb.com/manual/reference/method/db.collection.update/
- https://docs.mongodb.com/manual/tutorial/update-documents-with-aggregation-pipeline/
- https://docs.mongodb.com/manual/reference/operator/aggregation/switch/
