# Fluent Bit + SQL

Fluent Bit stream processor uses common SQL to perform record queries. The following section describe the features available and examples of it.

## Statements

### SELECT

#### Synopsis

```sql
SELECT select_expression
  FROM [STREAM:stream_name | TAG:match_rule]
  [WHERE condition]
```

#### Description

Select records from a stream or records matching a specific Tag pattern. Note that a simple SELECT statement __not__ associated from a stream creation will send the results to the standard output interface (stdout), useful for debugging purposes.

#### Examples

Select all records and keys coming from a stream called _apache_:

```sql
SELECT * FROM STREAM:apache;
```

Select all records which Tag starts with _apache._:

```sql
SELECT * FROM 'TAG:apache.*';
```

> Since the TAGselector allows the use wildcards we put the value between single quotes.

### CREATE STREAM

#### Synopsis

```sql
CREATE STREAM stream_name
  [WITH (property_name=value, [...])]
  AS SELECT select_expression
  FROM [STREAM:stream_name | TAG:match_rule]
  [WHERE condition]
```

#### Description

Create a new stream of data using the results from the SELECT statement. New stream created can be optionally re-ingested back into Fluent Bit pipeline if the property _Tag_ is set in the WITH statement. 

#### Examples

Create a new stream called _hello_ from stream called _apache_:

```sql
CREATE STREAM hello AS SELECT * FROM STREAM:apache;
```

Create a new stream called hello for all records which original Tag starts with _apache_:

```sql
CREATE STREAM hello AS SELECT * FROM 'TAG:apache.*';
```









 



| Command       | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| SELECT        | Indicate that the execution of the query will do keys selection. |
| CREATE STREAM | Create a new stream of data using results from a given query. |
| FROM          | Used to specify from which Stream or Tags select data from.  |
| WHERE         | This clause is used to extract only those records that fulfill a specified condition. |

### Aggregation Functions

| Function | Description                                |
| -------- | ------------------------------------------ |
| AVG()    | calculates the average of a set of values. |
| COUNT()  | counts records.                            |
| MIN()    | gets the minimum value in a set of values. |
| MAX()    | gets the maximum value in a set of values. |
| SUM()    | calculates the sum of values.              |

### Filtering

| 

