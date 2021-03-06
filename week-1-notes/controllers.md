# Lecture BackEnd 3.14.2022

## Example in app.js with imports, routes, middleware

```
//Built in middleware
app.use(express.json());

// App routes
app.post('/', (req, res) => {
    res.send('Hit root route')
});

app.post('/api/v1/dogs', (req, res, next) => {
    const newDog = { ...req.body };
    res.send(newDog)
});

// "next" is optional

// Error handling & 404 middleware for when a request doesn't match any app routes
app.use(require('./middleware/not-found));
app.use(requre('./middleware/error));


 -> just sending back api data, and v1 is the first version you will be putting back
(remember .post is creating)

```

## Having one controller by using Router

- const dogsController = requre('./controllers/dogs');
- for any request, you can use app.use() which will look for any request
- app.use('/api/v1/dogs', dogsController); -> so any request that has this path, it will use dogsController

```
const { Router } = requre('express');
module.exports = Router()
.post('/', (req, res) => {
    const newDog = { ...req.body };
    res.send(newDog)
});
```

For a Get api

```
.get('/', (req, res) => {
    res.send(dogs);
})

.get('/:id', (req, res) => {
const foundDog = dogs.find((dog) => dog.id === Number(req.params.id))
res.send(foundDog);
})

.get('/treats', (req, res) => {
    res.send('This is where all the treats are!');
})

.patch = updating

.patch('/:id', (req, res) => {
const updatedDogs = dogs.map((dog) => {
    if (dog.id === Number(req.params.id)) {
        const updatedDog = { ...dog, ...req.body };
        return updatedDog;
    } else {
        return dog;
    }
}
res.send(updatedDogs);
})
```

## setting up pool in Dog.js

- define what properties the object has
- remember a class is an object which shape is defined for later use aka object with rules
- define the properties in this way:
  - module.exports = class Dog {
    id; (id will be generated by database)
    name;
    age;
    favoriteTreat;
    }
- constructor(row) {
  this.id = row.id;
  } - in this case, row is referencing the object of row that is in your postgres. - you want the id of the instance to equal the id of the row object. - the constructor is called when we invoke new Dog()

## Static vs instance

- instance methods are methods that require an object of its class to be created before it can be called
- static are methods that can be called without creating an object of class

## Setting up SQL

1. DROP TABLE IF EXISTS dogs; (this gives us a fresh start)
2. CREATE TABLE dogs (this is the name of the table that we are creating) (
   // the different fields that your table will have aka names of columns
   id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY(generated is a keyword that will tell postgres to generate, and always = when to generate),
   name TEXT NOT NULL,
   age INT NOT NULL,
   favorite_treat (remember that postgres is case insensitive) TEXT (optional field so "not null" is not required)
   );

   INSERT INTO
   dogs (name, age, favorite_treat)
   VALUES
   ('Ruby', 11, 'Chicken'),
   ('Rusty', 12, 'Tuna');
