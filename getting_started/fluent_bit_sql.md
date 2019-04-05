# Fluent Bit + SQL

Fluent Bit stream processor uses common SQL to perform record queries. The following section describe the features available and examples of it.

## Language Description

### Statements

| Statements    | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| SELECT        | Indicate that the execution of the query will do keys selection. |
| CREATE STREAM | Create a new stream of data using results from a given query query. |

### Aggregation Functions

| Function | Description                                |
| -------- | ------------------------------------------ |
| AVG()    | calculates the average of a set of values. |
| COUNT()  | counts records.                            |
| MIN()    | gets the minimum value in a set of values. |
| MAX()    | gets the maximum value in a set of values. |
| SUM()    | calculates the sum of values.              |



