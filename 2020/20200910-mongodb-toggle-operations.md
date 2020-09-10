## mongodb toggle operations

1. mongodb toggle update a field with the `$bit` operator to result `0 -> 1 or 1 -> 0`.
    The `$bit` operator supports bitwise and, bitwise or, and bitwise xor (i.e. exclusive or) operations, only use this operator with integer fields (either 32-bit     integer or 64-bit integer).
    ```
    { $bit: { <field>: { <and|or|xor>: <int> } } }

    example: 
    source data:  { _id: 1, is_hidden: NumberInt(0) }

    you can toggle update the is_hidden field with `xor operation` to the result of a bitwise xor operation between the current value.

    db.switches.update(
       { _id: 3 },
       { $bit: { is_hidden: { xor: NumberInt(1) } } }
    )
    ```

2. mongodb toggle update a field with the `$switch` operator update with Aggregation Pipeline . 
    but right now i can't run pass through the demo supplied by the  [Mongodb manual example](https://docs.mongodb.com/manual/tutorial/update-documents-with-aggregation-pipeline/#example-2)

### References
- https://docs.mongodb.com/v2.6/reference/operator/update/bit/
- https://docs.mongodb.com/manual/tutorial/update-documents-with-aggregation-pipeline/
- https://docs.mongodb.com/manual/reference/operator/aggregation/switch/
