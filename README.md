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

## STEP 8 ADDING DATA FROM A FORM TO DATABASE
1. I created a post route. This will send request to a form for processing the data


2. I created a form to receive the request from the post route for the processing

```javascript
app.post('/', (req, res) => {
    const  itemName = req.body.newItem;
      const item = new Item ({
          name: itemName
      });

      item.save()

     res.redirect('/');
})
```
```javascript
 <form class="item" action="/" method="POST">
            <input type="text" name="newItem" placeholder="Enter todo">
            <button type="submit" name="list">+</button>
 </form>
```

## HOW THE FORM AND THE ROUTE COMMUNICATE
1. The input field has a name variable called newItem

2. When a user visit th above route which is the home route, a form will display, and when a user submit the form data, since the form has an action = '/' and method method="POST", it will move to that route, and any functions declared in that route will be executed.

3. When a user submit a form, the data from that field can be found in the route as and stored inside the itemName variable, This is achieved with the help of body-parser module
```javascript
 const  itemName = req.body.newItem;
```
4. The 'newItem' is the name varible from the field


## STEP 8 NOW LET'S ADD DATA TO DATABASE
1. Grab the value from the form and assign it to a variable 
```javascript
 const  itemName = req.body.newItem;
```

2. Create instance of the model and assign the value from the form to respective properties of the model, after that redirect the user to homepage 

3. Use this to save to the DB
```javascript
 item.save()
```
```javascript
 const item = new Item ({
          name: itemName
      });

      res.redirect('/');
```

## OVERALL CODE
```javascript
app.post('/', (req, res) => {
    const  itemName = req.body.newItem;
      const item = new Item ({
          name: itemName
      });

      item.save()
     res.redirect('/');
})
```