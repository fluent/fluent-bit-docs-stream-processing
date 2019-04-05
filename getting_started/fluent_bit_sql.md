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

> Since the TAG selector allows the use wildcards we put the value between single quotes.

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

## Aggregation Functions

Aggregation functions allows to perform data calculation on groups of records.

### AVG

#### Synopsis

```sql
SELECT AVG(key) FROM STREAM:apache;
```

#### Description

Calculates the average of a set of values.

### COUNT

#### Synopsis

```sql
SELECT COUNT(*) FROM STREAM:apache;
```

#### Description

Count the number of records

### MIN

#### Synopsis

```sql
SELECT MIN(key) FROM STREAM:apache;
```

#### Description

Gets the minimum value of a key in a set of records.

### MAX

#### Synopsis

```sql
SELECT MIN(key) FROM STREAM:apache;
```

#### Description

Gets the maximum value of a key in a set of records.

### SUM

#### Synopsis

```sql
SELECT SUM(key) FROM STREAM:apache;
```

#### Description

Calculates the sum of all values of key in a set of records.

## Time Functions

Time functions adds a new key into the record with timing data

### NOW

#### Synopsis

```sql
SELECT NOW() FROM STREAM:apache;
```

#### Description

Add system time using format: %Y-%m-%d %H:%M:%S. Output example: 2019-03-09 21:36:05.

### UNIX_TIMESTAMP

#### Synopsis

```sql
SELECT UNIX_TIMESTAMP() FROM STREAM:apache;
```

#### Description

Add current Unix timestamp to the record. Output example: 1552196165.

