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
