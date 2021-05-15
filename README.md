# reactjs

# BASIC TEMPLATE FOR REACTJS

```js
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

    <title>Hello, world!</title>
    <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.26.0/babel.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>



  </head>
  <body>
    <div class="container-fluid" id="root">
    </div>



    <script type="text/babel">

  const { useState } = React
  const { useEffect } = React

  function App(props) { 
    // state hooks

    // Hooks are a new addition in React 16.8. They let you use state and other
    // React features without writing a class.

    // useState syntax
    // https://kentcdodds.com/blog/react-hooks-array-destructuring-fundamentals
    //The syntax here is called "array destructuring" and it was introduced into
    //JavaScript in the infamous (more than famous) ES6 release.

    // https://www.freecodecamp.org/news/how-to-destructure-the-fundamentals-of-react-hooks-d13ff6ea6871/
    // Eg:
    // const [ one, two ] = [ 1, 2 ];
    // console.log(one); // 1
    // console.log(two); // 2

    // or

    // const [ two, one ] = [ 1, 2 ];
    // console.log(two); // 1
    // console.log(one); // 2

    // useState is a function that returns an array that we're destructuring for
    // use within our component.

    const [text, setText] = useState('hello');

    // ALL TIMES
    useEffect(() => {
        document.title = `${text}`;
    }); //useEffect runs by default after every render of the component (thus causing an effect).

    // ONLY ONCE
    //If we want it to run only once then useEffect with empty array
    // useEffect(
    //   function () {
    //     document.title = "".concat(text);
    //   }, 
    //   []
    // ); //useEffect runs by default after every render of the component (thus causing an effect).

    // ONCE AND WHENEVER VALUE CHANGES
    //React will run the callback after the first render and every time one of the elements in the array is changed
    // useEffect(
    //   function () {
    //     document.title = "".concat(text);
    //   }, 
    //   [test]
    // );


    return (
        <div class="row">
          <div class="col-12">
            <h1>{text}</h1>
            <input type="text" value={text} onChange={(e) => setText(e.target.value)} />
          </div>
        </div>
    );
  }

  const rootElement = document.getElementById('root')
  ReactDOM.render(<App />, rootElement)



    </script>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
  </body>
</html>
```













# How to call loading function with React useEffect only once
https://stackoverflow.com/a/55481525

**TL;DR**

`useEffect(yourCallback, [])` - will trigger the callback only after the first render.

**Detailed explanation**

`useEffect` runs by default after **every** render of the component (thus causing an effect).

When placing `useEffect` in your component you tell React you want to run the callback as an effect. React will run the effect after rendering and after performing the DOM updates.

If you pass only a callback - the callback will run after each render.

If passing a second argument (array), React will run the callback after the first render and every time one of the elements in the array is changed. for example when placing `useEffect(() => console.log('hello'), [someVar, someOtherVar])` - the callback will run after the first render and after any render that one of `someVar` or `someOtherVar` are changed.

By passing the second argument an empty array, React will compare after each render the array and will see nothing was changed, thus calling the callback only after the first render.

# Basic template for reactjs with state variable name


```
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

    <title>Hello, world!</title>
    <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.26.0/babel.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>



  </head>
  <body>
    <div class="container-fluid" id="root">
    </div>



    <script type="text/babel">

  const { useState } = React
  const { useEffect } = React

  // in chrome we cant see the state vairable name so we use this way
  const { useDebugValue } = React

  function App(props) { 
    // state hooks

    // Hooks are a new addition in React 16.8. They let you use state and other
    // React features without writing a class.

    // useState syntax
    // https://kentcdodds.com/blog/react-hooks-array-destructuring-fundamentals
    //The syntax here is called "array destructuring" and it was introduced into
    //JavaScript in the infamous (more than famous) ES6 release.

    // https://www.freecodecamp.org/news/how-to-destructure-the-fundamentals-of-react-hooks-d13ff6ea6871/
    // Eg:
    // const [ one, two ] = [ 1, 2 ];
    // console.log(one); // 1
    // console.log(two); // 2

    // or

    // const [ two, one ] = [ 1, 2 ];
    // console.log(two); // 1
    // console.log(one); // 2

    // useState is a function that returns an array that we're destructuring for
    // use within our component.

    // in chrome we want to see the varaible name so we use this
    function useStateWithLabel(initialValue, name) {
      const [value, setValue] = useState(initialValue);
      useDebugValue(`${name}: ${value}`);
      return [value, setValue];
    }



    //const [text, setText] = useState('hello');
    // in chrome we want to see the varaible name so we use this
    const [text, setText] = useStateWithLabel('hello',"text");

    // ALL TIMES
    useEffect(() => {
        document.title = `${text}`;
    }); //useEffect runs by default after every render of the component (thus causing an effect).

    // ONLY ONCE
    //If we want it to run only once then useEffect with empty array
    // useEffect(
    //   function () {
    //     document.title = "".concat(text);
    //   }, 
    //   []
    // ); //useEffect runs by default after every render of the component (thus causing an effect).

    // ONCE AND WHENEVER VALUE CHANGES
    //React will run the callback after the first render and every time one of the elements in the array is changed
    // useEffect(
    //   function () {
    //     document.title = "".concat(text);
    //   }, 
    //   [test]
    // );


    return (
        <div class="row">
          <div class="col-12">
            <h1>{text}</h1>
            <input type="text" value={text} onChange={(e) => setText(e.target.value)} />
          </div>
        </div>
    );
  }

  const rootElement = document.getElementById('root')
  ReactDOM.render(<App />, rootElement)



    </script>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
  </body>
</html>
```

then in the components in the developer tool we see

```
hooks
   StateWithLabel "text: hello"
   StateWithLabel "params_general_state: [object Object]"
   StateWithLabel "response_state: [object Object]"
```



# Why React setState/useState does not update immediately

> React this.setState, and React.useState create queues for React core to update the state object of a React component.

> So the process to update React state is asynchronous for performance reasons. That’s why changes don’t feel immediate.


> Think of setState() as a request to update the component. Reading state right after calling setState() a potential pitfall.
> 



# Reactjs 2 approaches for adding collapsabile in a list of items

## 1) create a customized item (where open state is localized to each component)
https://material-ui.com/components/tables/#collapsible-table

https://stackoverflow.com/a/65362002

## 2) save the current 'open' state for each of the menus separately
https://stackoverflow.com/a/55673454


## 1) create a customized item (where open state is localized to each component)
https://material-ui.com/components/tables/#collapsible-table

https://stackoverflow.com/a/65362002

```javascript
import React, { useState } from 'react'

const CustomizedListItem = ({ doc }) => {
    const [ open, setOpen ] = useState(false)
    const handleClick = () => {
        setOpen(!open)
    }
    
    return (
        <div>
            <ListItem button key={doc.Id} onClick={handleClick}>
                <ListItemText primary={doc.Name} />
                {open ? <ExpandLess /> : <ExpandMore />}
            </ListItem>
            <Collapse
                key={doc.Sheets.Id}
                in={open}
                timeout='auto'
                unmountOnExit
            >
                <List component='li' disablePadding key={doc.Id}>
                    {doc.Sheets.map(sheet => {
                        return (
                            <ListItem button key={sheet.Id}>
                                <ListItemIcon>
                                    {/* <InsertDriveFileTwoToneIcon /> */}
                                </ListItemIcon>
                                <ListItemText key={sheet.Id} primary={sheet.Title} />
                            </ListItem>
                        )
                    })}
                </List>
            </Collapse>
            <Divider />
        </div>
    )
}


export default function CategoriesResults() {
    const docs = data.documents  //this coming from a json file
    return (
        <div>
            <List component='nav' aria-labelledby='nested-list-subheader'>
                {docs.map(doc => {
                    return (
                        <CustomizedListItem key={doc.id} doc={doc} />
                    )
                })}
            </List>
        </div>
    )
}
```



## 2) save the current 'open' state for each of the menus separately
https://stackoverflow.com/a/55673454


You already have a unique id for your different menus, you can use them in order to achieve your goal. One way would be to extend your state with the related settings for your menus:

```
state = { settings: [{ id: "1", open: false }, { id: "2", open: false }] };
```

This allows you to have the information about the collapsed status of each of your menus.

According to that you need to extend your handleClick function a bit in order to only change the state of the menu item you clicked:

```
handleClick = id => {
  this.setState(state => ({
    ...state,
    settings: state.settings.map(item =>
      item.id === id ? { ...item, open: !item.open } : item
    )
  }));
};
```

And in your render function you need to make sure that you pass the right id of the menu item you clicked to your handleClick function and that you select the right open state.

```
<React.Fragment key={each.id}>
  <ListItem button onClick={() => this.handleClick(each.id)}>
    <ListItemText inset primary={each.nameHeader} />
    settings.find(item => item.id === each.id).open
    ? "expanded"
    : "collapsed"}
  </ListItem>
  <Divider />
  <Collapse
    in={settings.find(item => item.id === each.id).open}
    timeout="auto"
    unmountOnExit
  >
  <List component="div" disablePadding>
    {each.subMenu.map(subData => (
      <ListItem key={subData.id} button>
        <ListItemText inset primary={subData.name} />
      </ListItem>
     ))}
   </List>
 </Collapse>
</React.Fragment>
```

# how to edit an item in a list in state

https://stackoverflow.com/a/49502115/2897115

Since there's a lot of misinformation in this thread, here's how you can do it without helper libs:

    handleChange: function (e) {
        // 1. Make a shallow copy of the items
        let items = [...this.state.items];
        // 2. Make a shallow copy of the item you want to mutate
        let item = {...items[1]};
        // 3. Replace the property you're intested in
        item.name = 'newName';
        // 4. Put it back into our array. N.B. we *are* mutating the array here, but that's why we made a copy first
        items[1] = item;
        // 5. Set the state to our new copy
        this.setState({items});
    },

You can combine steps 2 and 3 if you want:

    let item = {
        ...items[1],
        name: 'newName'
    }

Or you can do the whole thing in one line:

    this.setState(({items}) => ({
        items: [
            ...items.slice(0,1),
            {
                ...items[1],
                name: 'newName',
            },
            ...items.slice(2)
        ]
    }));

Note: I made `items` an array. OP used an object. However, the concepts are the same.


------

You can see what's going on in your terminal/console:

    ❯ node
    > items = [{name:'foo'},{name:'bar'},{name:'baz'}]
    [ { name: 'foo' }, { name: 'bar' }, { name: 'baz' } ]
    > clone = [...items]
    [ { name: 'foo' }, { name: 'bar' }, { name: 'baz' } ]
    > item1 = {...clone[1]}
    { name: 'bar' }
    > item1.name = 'bacon'
    'bacon'
    > clone[1] = item1
    { name: 'bacon' }
    > clone
    [ { name: 'foo' }, { name: 'bacon' }, { name: 'baz' } ]
    > items
    [ { name: 'foo' }, { name: 'bar' }, { name: 'baz' } ] // good! we didn't mutate `items`
    > items === clone
    false // these are different objects
    > items[0] === clone[0]
    true // we don't need to clone items 0 and 2 because we're not mutating them (efficiency gains!)
    > items[1] === clone[1]
    false // this guy we copied


# another way

Sometimes in React, mutating the cloned array can affect the original one, this method will never cause mutation:

        const myNewArray = Object.assign([...myArray], {
            [index]: myNewItem
        });
        setState({ myArray: myNewArray });
Or if you just want to update a property of an item:

        const myNewArray = Object.assign([...myArray], {
            [index]: {
                ...myArray[index],
                prop: myNewValue
            }
        });
        setState({ myArray: myNewArray });

# changing property in all objects in an array

```
  myArray = myArray.map(arrayElem => {
    arrayElem.property = newValue
    return arrayElem
  })
```
You **don't** need `lodash` for this.

<hr/>

The first object is missing your status property and it will be added.

<br>

<h2>SHOWING THREE WAYS HOW YOU CAN DO IT</h2>

<br>

**IMMUTABLE VERSION**  (We create a new array using `map`)

    const arrImmutableVersion = arr.map(e => ({...e, status: "active"}));

 

**MUTABLE VERSIONS**  (We change the original array)

    arr.forEach((el)=>{el.status = "active";}) 

 or

    arr.forEach(function(el){el.status = "active";}) 

 


