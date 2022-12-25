## CRUD

---



#### Create

```sql
INSERT INTO `new_schema`.`users` (`id`, `name`, `age`) VALUES (4, 'Harry', 33);

INSERT INTO `new_schema`.`users` (`id`, `name`, `age`) VALUES (4, 'Harry', 33), (5, 'Tom', 30);
```



#### Read

```sql
SELECT `id`, `name` FROM `new_schema`.`users`;

SELECT * FROM `new_schema`.`users`;
# conditions
SELECT * FROM `new_schema`.`users` WHERE `id` = 2;
```



#### Update

```sql
UPDATE `new_schema`.`users` SET `name` = 'Andy', `age` = 100 WHERE `id` = 2;
```



#### Delete

```sql
DELETE FROM `new_schema`.`users` WHERE `id` = 1;
```

