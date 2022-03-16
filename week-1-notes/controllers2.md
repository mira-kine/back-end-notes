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
- you call the constructor everytime you make a new class, and classes are called using the word "new"
- you can set defaults in your constructor for ex:
  constructor({
  crust = 'Hand Tossed',
  sauce = 'Robust Tomato',
  toppings = ['Cheese'],
  })
- this way, if someone does not input a crust you can have a default so that the code won't crash
- Whenever you access those values, you can know that the values will be there in the format that you are anticipating regardless of user input
- static method: gets used on the class itself -> methods that are used on all objects we make. You can access its attributes from the object itself
- nonstatic instance method: only called when we have an instance on which to call it. If you want to see attributes youd have to call the method first before you can see what it has
- if a method is not defined by a static keyword,
- "this" is a stand-in for the entire object. so when you refer to "this.crust" for ex, you are referring to the crust of the pizza that you are working with at the moment
- instance = an object created using a particular constructor function
- if you call super() in your constructor, it will call wherever you are extended to
