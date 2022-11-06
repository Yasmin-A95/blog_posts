# React frontend with a Rails API backend

We've set up our API backend, now let's deal with our client side. 

Instructions on setting up our rails API [here](https://yasmina95.hashnode.dev/using-a-ruby-on-rails-api-as-your-backend) for the uninitiated.

#### Setup 

Make sure your rails server is running. `cd` into the relevant file and `rails s`. Then in another file let's create our client side. `npx create-react-app mixology-client`, `cd mixology-client` and `npm i axios`. `npm start` and open the files in your editor. 

In `App.js` import axios and let's get that response.data in a console.log. Throw the following code above the App function. 

```js
import axios from 'axios';

axios.get('http://localhost:3000/api/v1/mixologists/').then((res) => {
  console.log(res.data)
})
```

![React app in browser with console open showing the JSON response](https://cdn.hashnode.com/res/hashnode/image/upload/v1667190310640/bK57mcEv2.png align="left")

Nice. Let's get a bit fancier with it though. 

#### Fancyer

What we really want is to generate HTML elements from our JSON, and we want to do it *dynamically*. If we hard-coded it, every time we or somebody else added new information to the API we would have to come back in and hardcode it some more. 

Let's make the HTML tag we wish existed. In `App.js` make the `<DisplayMixologists />` tag.
```js
import './App.css';

function App() {

  return (
    <div className="App">
      <DisplayMixologists />
    </div>
  );
}

export default App;
```

Now we've got an error saying this isn't defined. How helpful, now we know what to do next. It's almost like the error is driving our development. Cool.

![undefined error message](https://cdn.hashnode.com/res/hashnode/image/upload/v1667217799618/I5ebX8g1c.png align="left")

Make a folder in `src` called `components`, and create the `DisplayMixologists.js` file. Then throw in:

```js
const DisplayMixologists = () => {
    return (
        <h1> coming soon</h1>
    );
}

export default DisplayMixologists
```
Don't forget we've still got to import it in `App.js`
```js
import './App.css';
import DisplayMixologists from './components/DisplayMixologists';

function App() {

  return (
    <div className="App">
      <DisplayMixologists />
    </div>
  );
}

export default App;
```

Now, let's get our axios request dressed up a bit more reactish. 

```js
const DisplayMixologists = () => {
    const [mixologists, setMixologists] = useState([]);

   useEffect(() => {
        axios
            .get('http://localhost:3000/api/v1/mixologists/')
            .then((res) => {
                const mixologist = res.data
                setMixologists(mixologist)
            })
            .catch((err) => console.log(err));
    }, []);

    return (
        <h1> coming soon</h1>
    );
}
```
Here we're declaring a new state variable. This returns the current state value and a function that you can use to update it. By giving useState an empty array we're setting its initial value. 

```js
 const [mixologists, setMixologists] = useState([]);
```

Whereas wrapping our axios request in `useEffect` mimics the React lifecycle method `componentDidMount`, making sure our callback only fires on the first render. 

Warn: passing the empty array is super important in both the above bits of code!

Ok, now let's get that information into some HTML so we can display it. We're going to map over our mixologists array and return some `fragments`. 

```js
    return (
        <div>
            {
                mixologists.map((item) => {
                    let name = <React.Fragment key={item.id}>
                        <h1>{item.name}</h1>
                    </React.Fragmen
                    let drinksList = item.drinks.map(drink => {
                        let drinksInfo = <React.Fragment key={drink.id}>
                            <h3>{drink.name}</h3>
                            <p>{drink.ingredients}</p>
                        </React.Fragment>
                        return drinksInfo
                    })
                    return [name, drinksList]
                }
                )}
        </div>
    )
}
```

There's a lot going on there, huh? Let's break it down to get familiar with everything this is doing.

```js
mixologists.map((item) => {
    let name = <React.Fragment key={item.id}>
```
Here we're calling map on the array holding the current state value of mixologists, which is the information we've captured in our API request! Map iterates over our array and creates a copy of it populated with the results of the function we pass into map. In our case, that was an arrow function which we used to access the values within each mixologist in our JSON, and generate some HTML containing some of that mixologist's information, `{item.name}` for example. 

The variable name item could probably be a bit clearer, but the word mixologist has been used a lot already so item is what we got. 

```js
<React.Fragment>
    <ChildrenGoHere />
    <ChildrenGoHere />
</React.Fragment>
```
This guy is a new one for me. A React fragment is a component you can use to return multiple elements, which is exactly what we wanted in our map! In our naive implementation, we're giving it a key mostly so that we don't get an annoying error message in the console.

```js
<React.Fragment key={item.id}>
``` 
There's a fancy new shorthand for it now, but I thought it might be nice to learn it the extra semantic way before we graduate to... 

```js
<>
    <td> I'm a child of the fragment </td>
    <td> me too! </td>
</>
```
No keys are needed or possible for this brief creature. 

The result of our beefed up bit of code? Feast your eyes on this beauty.

![unstyled blocky text reading Yasmin, Sangria, then a list of ingredients followed by another drink and ingredients list followed shortly by another name and drink, then two names with no drinks underneath them](https://cdn.hashnode.com/res/hashnode/image/upload/v1667284007588/uslLSe0Ab.png align="left") 

There's no real use in displaying a name that has no drink's associated with it, so it's time for...

#### Conditional Rendering

Conditional rendering in React uses the same language as vanilla JavaScript, so I'm opting for an if statement for simplicity. 

```js
 if (drinksList[0]) {
                        return [name, drinksList]
                    }
```

If the `drinksList` array has a first element, then we will return it! Otherwise it's not useful to us. 

```js
return (
        <div>
            {
                mixologists.map((item) => {
                    let name = <React.Fragment key={item.id}>
                        <h1>{item.name}</h1>
                    </React.Fragment>
                    let drinksList = item.drinks.map(drink => {
                        let drinksInfo = <React.Fragment key={drink.id}>
                            <h3>{drink.name}</h3>
                            <p>{drink.ingredients}</p>
                        </React.Fragment>
                        return drinksInfo
                    })
                    if (drinksList[0]) {
                        return [name, drinksList]
                    }
                }
                )}
        </div>
    )
```



![the name Yasmin followed by sangria and a list of ingredients, and the name Dan followed by a list of ingredients](https://cdn.hashnode.com/res/hashnode/image/upload/v1667307786949/0NE_uchT8.png align="left")

#### Refactor and Style
(jk, bye)

Wow what a great website. The next steps here would be to refactor our code, make sure all our variable names are nice and meaningful, and to style things up a bit, so I'm going to stop writing this blog post and do that. 

Good luck and goodbye. 