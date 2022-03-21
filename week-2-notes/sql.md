# Lecture on SQL 3.21.22

### Join:

- Left: starting with the left hand side (for ex, whatever first table we queried), join in the one that comes next. This includes everything on the left side regardless of whether they share the same venn diagram
- Inner join: middle part of the venn diagram - so whatever they share
- Right join: opposite of left join. For ex, if you selected from table dogs then owner, and you do a right join, you will get back all the owners and which ones they have dogs
  - syntax would be SELECT \* from a LEFT JOIN b ON a.key = b.key

## Let's build a SQL table!

- Cascade: if one deletes, it will delete the other (order based)
  - allows us to remove the table and its dependent objects
- FOREIGN KEY (owner_id) REFERENCES owners(id) -> "FOREIGN KEY" shows that you are referencing a key in another table
- you can also write it as owner_id BIGINT UNIQUE REFERENCES owners(id)
- the UNIQUE keyword is what gives something a 1:1 relationship
- ON keyword shows us which field you want to join the two tables on
- you can give something an alias if you want a different name back when you join the two tables for ex dogs.name AS dogs_name

### Junction table

- for many to many relationships, you need a junction which is a table that stores mutual information to connect the two table
- for ex:
  CREATE TABLE dog_owners (
  dog_id BIGINT REFERENCES dogs(id), owner_id BIGINT REFERENCES owners(id)
  );
- Then you can connect it using VALUES for ex. INSERT INTO dog_owners (dog_id, owner_id) VALUES (1, 1);
