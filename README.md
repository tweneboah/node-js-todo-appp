# KEY POINTS / STEPS FOR THIS PROJECT

## STEP 1
1. I required all the moduls i needed for this project
```javascript
const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');

const app = express();
app.set('view engine', 'ejs');
app.use(bodyParser.urlencoded({extended:true}));
```
## STEP 2 - Connecting to MOnogoDB
1. Firts i coonected to the momgoDB Server using this path
```javascript
/users/emmanuel/mongodb/bin/mongod --dbpath=/users/emmanuel/mongodb-data
```

## STEP 3 - Connect to the DB and Node JS
1. Firts i coonected to the momgoDB Server using this path

2. This connect and Create todo-app-DB
```javascript
mongoose.connect('mongodb://127.0.0.1:27017/todo-app-DB', {
    useNewUrlParser: true, 
    useCreateIndex: true,//help us to quickly access our database
    useFindAndModify: false
  });
```

## STEP 4 CREATED MY BUSSINESS LOGIC / TODO SCHEMA
1. This defines the structure of my application

```javascript
//TODO SCHEMMA
const itemSchema = new mongoose.Schema({
    name: {
        type: String,
        required: [true, 'Description cannot be empty'],
        min: 4
    }
});
```

## STEP 5 I CREATED MY TODO MODEL
1. This is used to create the instance of the todo

```javascript
const Item = new mongoose.model('Item', itemSchema);
```

## STEP 6 CREATING THE REAL TODO USING THE MODEL
1. To create real todo, create instance of the model

```javascript
//Creating items
const item1 = new Item ({
    name: 'Going Home'
})

const item2 = new Item ({
    name: 'Learning'
})

const item3 = new Item ({
    name: 'Dinner'
})


const item4 = new Item ({
    name: 'lesson plan'
})
```


## STEP 7 PASSING JS VALUE TO WEBPAGE
1. I created js function to display date of the day

2. I created a route to display the value




```javascript
app.get('/', (req, res) => {

    let today = new Date();
 
    let options = {
         weekday: 'long',
         day: 'numeric',
         month: 'long'
    };
    let day  = today.toLocaleString('en-US', options)
        //Rendering to webpage
        res.render('list', {kindOfDay: day})
   
        })
})
```

3. The res.render() accept two arguements: 1. The ejs file which will display the value , 2. Objects.

 res.render('list', {kindOfDay: day}) Means assign the value of day from the function above and assign it to a varriable called kindOfDay, This holds the value of the function.

 After that i passed the the varriable kindOfDay to the ejs file for displaying  <h1>It's a <%=kindOfDay%> </h1>

4. To display any value to webpage pass it to this res.renderres.render('list', {kindOfDay: day, newListItem: foundItem




