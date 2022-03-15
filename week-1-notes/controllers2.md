# Lecture 3.15.22

## controllers and models

- controllers don't have sql language, it is easier to read. It is where the response and request go out to the backend
- models have the sql language that work with the database

## Models

- has a constructor that will construct the object to invoke a new Object (whatever you call it, in the example it was called Dog) according to the instance.
  - uses for ex. this.id = row.id (database row's id)
- rows are (usually) an array of objects in the database (like how in supabase, each row was an object with keys and values)
- pool.query -> the format that the postgres node module package we have uses

## Classes

- use the word "class" to define your class, then use the word "new" to create an instance of your class
- "class" is the blueprint and "new" is like using the blueprint to create the object
- res.send vs res.json -> the content type is different. Whatever you send with res.send is going to be what the header says you sent out for ex. text if you used a string. res.json uses send under the hood BUT it explicitly sets it as a json
