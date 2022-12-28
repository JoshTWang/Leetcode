#### Basic conditions

- `=` not `==`
- `<`
- `>`
- `<>` or `==`



#### NULL

- `IS NULL`
- `IS NOT NULL`



#### Multiple conditions

- `AND`
- `OR`



#### Range conditions

- `IN`

```sql
SELECT * FROM `new_schema`.`users` WHERE `id` IN (1, 3);
```

- `BETWEEN`

```sql
SELECT * FROM `new_schema`.`users` WHERE height BETWEEN 160 AND 190;
```

- `LIKE`

```sql
SELECT * FROM `new_schema`.`users` WHERE name LIKE '%a%';
```

