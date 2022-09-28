# Queries

## Joins

1. Get all batch names along with their instructor names.

```sql
  SELECT 
      b.name as 'BATCH NAME', i.first_name, i.last_name
  FROM
      `batches` b
          LEFT JOIN
      `instructors` i ON b.`instructor_id` = i.`id`;
```

2. Get all students along with their batch names if present else `NULL`.

```sql
  SELECT 
      s.first_name, s.last_name, b.name AS 'Batch Name'
  FROM
      `students` s
          LEFT JOIN
      `batches` b ON s.batch_id = b.id;
```
3. Get all students along with their batch names. Also, fetch all the batches which have no students.

```sql
  SELECT 
      s.first_name, s.last_name, b.name AS 'Batch Name'
  FROM
      `students` s
          RIGHT JOIN
      `batches` b
  ON
      s.`batch_id` = b.`id`;
```
4. Get all the combinations of batches and instructors.

```sql
  SELECT 
      *
  FROM
      `instructors` i,
      `batches` b;
```
5. Get all students with their instructors. If a student has no instructor, then show `NULL` for the instructor's name.

```sql
  SELECT 
    s.first_name, s.last_name, i.first_name, i.last_name
  FROM
    `students` s
        LEFT JOIN
    `batches` b ON s.batch_id = b.id
        LEFT JOIN
    `instructors` i ON b.`instructor_id` = i.`id`; 
```

## Aggregation
1. Get the maximum IQ in all students (Try without aggregation first).

```sql
  SELECT 
      `iq`
  FROM
      `students`
  ORDER BY `iq` DESC
  LIMIT 1;
```

2. Get the maximum IQ in all students (With aggregation).

```sql
  SELECT 
      MAX(iq)
  FROM
      `students`;
```

3. Get the oldest batch from the batches table.

```sql
SELECT 
    MIN(start_date)
FROM
    `batches`;
```

4. Fetch the number of batches that start with the word `Jedi`.

```sql
SELECT 
    COUNT(*)
FROM
    `batches`
WHERE
    `name` LIKE 'Jedi%';
```

5. Get the average IQ of all students (Without using `AVG`)

```sql
SELECT 
    SUM(iq) / COUNT(iq)
FROM
    `students`;
```

6. Get the average IQ of students in all batches.

```sql
SELECT 
    AVG(iq)
FROM
    `students`;
```
7. Find the average IQ of students in each batch.

```sql
SELECT 
    `batch_id`, AVG(iq)
FROM
    `students`
WHERE
    `batch_id` IS NOT NULL
GROUP BY `batch_id`;
```

8. Find the total number of students in each batch.

```sql
SELECT 
    `batch_id`, COUNT(*)
FROM
    `students`
WHERE
    `batch_id` IS NOT NULL
GROUP BY `batch_id`;
```

9. Get the total number of batches taught by each instructor.

```sql'
SELECT 
    `instructor_id`, COUNT(*) AS 'No. Batches'
FROM
    `batches`
WHERE
    `instructor_id` IS NOT NULL
GROUP BY `instructor_id`;
```

10. Find the average IQ of students in batches with batch ID `1` and `2`.

```sql
SELECT 
    `batch_id`, AVG(iq)
FROM
    `students`
WHERE
    `batch_id` IN (1,2)
GROUP BY `batch_id`;
```

11. Find count of students that are part of batches that have average IQ greater than `120`.

```sql
SELECT 
    `batch_id`, COUNT(id) AS 'No. Students'
FROM
    `students`
WHERE
    `batch_id` IS NOT NULL
GROUP BY `batch_id` HAVING AVG(IQ)>120 ;
```
