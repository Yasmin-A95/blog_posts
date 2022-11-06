# Intro to React

A guide to React from one beginner developer to another. We're starting out with an image search site to get some practice.

#### Intro

React is a popular framework that was made to solve several problems and has since expanded outward to solve many more. It's a way to hand over some of the management of complex apps. I think of it as a fun way of inventing HTML elements you wish existed. Take https://www.abc.net.au/news/ for example. Those distinct areas you see on the page are most likely *not* html divs, but React tags instead. They might have created a tag called Story. Within the Story you can define what a story is, what it contains, the css you'd like and whatnot. You could reuse the Story tag on multiple pages, creating a beautiful consistency throughout your site. That's one of the problems Facebook were trying to solve by creating React, they wanted each page to have a high level of consistency. 

React tags are like html elements, but richer. 

#### Fundamentals
The fundamentals to keep in mind are the following.

1. Components: If you've had experience with rails, you might find it useful to think of components as the React version of classes.
2. Props: are how you get data into a component. We can customise the way a component works by changing the props.
3. State: is data that changes over time. One source of state is user input. A user may click a button a certain number of times for example. The state of that button is localised to their computer, rather than being something that fundamentally changes the site. Another leading source of state comes from ajax. The data isn't there when the page initially loads, but comes about *afterwards*. 

#### Error-Driven Development 
The workflow will look like this:
- Create an element that doesn't exist
- Make it Exist By:
- Defining it
- Making it available
- Importing it

#### Getting to Know React

When I'm exploring something new, I like to dip my toes in and play around with things before jumping into a proper project. 

Let's take React on a little first date and get comfortable with eachother. Move into or create the folder you'd like to work from in the terminal and then `npx create-react-app flickr`. Open the file in your editor then head back into terminal and `cd flickr` and `npm run start` OR `npm rum start` for some reason. It works the same either way. If things haven't mysteriously gone wrong, you should have had it automatically open in your browser. It does preference chrome, but there are ways to command it to open in firefox or the like in the terminal for instance `BROWSER=firefox npm rum start`. I believe changing this permanently would mean to include that line in your `.bash_profile`.

In your editor move into App.js and make the following changes to the code. 

We want this:
```
 <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
```

To be this instead:
```
<p>
        Bless us Mark Zuckerberg. 
Bless our code since you redeemed us so dearly and delivered us from 
evil, as you gave us a share in this code so may you give us a share
 in eternal life.
        </p>
```
Oh wow, look at that! It updated our text without us needing to refresh. All that AND it opened our file in the browser without us asking it to? So convenient so productive wowowow. 

![Screen Shot 2022-08-07 at 5.28.32 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659857329676/db7VKlZm9.png align="left")


#### React (for Uncool Babies)

Alright, now let's get stuff going for reals. I'm suggesting that we create a new folder in `src` called `Components` because this is how I've been taught to do things, as with all things code there are many ways of going about this. Move `App.js` in there and create a new file called `Search.js`

Now head over to `index.js` and on line four change `import App from './App';` to `import App from './Components/App';`

At this point our site is still broken, but that's alright. We're doing error-driven development. Pro-tip, any time your code is bugging out call it error-driven development to console yourself. 

In App.js let's create a component that doesn't exist yet, then make it exist. That's the work flow babes. 

```
import Search from "./Search";

function App() {
  return (
    <div className="App">
      <Search />
    </div>
  );
}

export default App;
```

Take a look at the error, this is where we get the cue for our next job. Defining 'Search'. 


![Screen Shot 2022-08-07 at 7.06.46 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659863220498/S7ETJk3vV.png align="left")

There are a bunch of ways you *could* go about defining search, but there's a generally adopted practice that people will look at you sideways for defying. So let's do it with some object destructuring and avoid getting beaten up and having our lunch money stolen. 

```
import React, { Component } from "react";

class Search extends Component {
    render() {
        return <h1> Search Coming Soon </h1>
    }
}
export default Search;
```
Render is the only method that you absolutely must define in a class component. Without render, you have no component at all. 

![Screen Shot 2022-08-07 at 7.13.03 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659863594742/3N5wPUXIe.png align="left")

Oh my gosh what an interesting page we've got here.

Let's get the bones of a search form going.

In Search.js code out the following
```
import React, { Component } from "react";

class Search extends Component {
    render() {
        return (
        <form>
            <label>Search:
                <input type='text' placeholder="Search" autofocus />
            </label>
            <button>Submit</button>
        </form>
        );
    }
}
export default Search;
```


![Screen Shot 2022-08-07 at 7.24.07 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659864269075/juzH9QDAo.png align="left")

An even more interesting page! Look at us go. Alright, this thing is going to need to actually do something eventually. Let's get going on that front. 

```
import React, { Component } from "react";

class Search extends Component {
  constructor( props ) {
    super( props );
    this.state = { value: " " };
    this.handleChange = this.handleChange.bind( this );
    this.handle submit = this.handleSubmit.bind( this );
  }

  handleChange( event ) {
    this.setState({ value: event.target.value });
  }
  handleSubmit( event ) {
    alert("A search was made for " + this.state.value +
 " how nice for them");
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={ this.handleSubmit }>
        <label>
          Search:
          <input
            type="text"
            value={ this.state.value }
            onChange={ this.handleChange }
            placeholder="Search"
            autoFocus
          />
        </label>
        <button> Submit </button>
      </form>
    );
  }
}
export default Search;
```
If you're looking and that and thinking "that's a lot to take in". Fair. Let's break it down a bit. 

```
class Search extends Component {
  constructor( props ) {
    super( props );
    this.state = { value: " " };
    this.handleChange = this.handleChange.bind( this );
    this.handleSubmit = this.handleSubmit.bind( this );
  }
```

A constructor is necessary when we're initialising state and binding methods to our class. The number one thing a constructor cannot do without is `super(props)`. 

React constructors serve two main purposes. Initialising state i.e. `this.state = { value: " " };` . And binding event handlers to our methods i.e. `.bind(this);`.

All those references to state and value e.g. ` <input
            type="text"
            value={ this.state.value }
            onChange={ this.handleChange }
            placeholder="Search"
            autoFocus
          />` are examples of the way React handles state changes and rendering. React is the single source of truth about the state of components, it renders when the page loads and *reacts* to user input, handling changes and updating the DOM. `handleChange` runs on every keystroke updating the DOM as the user types. React touches the DOM and instructs us not to dare even look at it. Let mother Zuckerberg handle that for you, and don't worry your pretty little head about it. DOM. No touch. Got it? *Good*.

Let's take our very functional search form for a spin.

![Screen Shot 2022-08-07 at 9.10.22 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659870636962/Cm0efsH-9.png align="left")

Noice. 

In part two of this series we'll get image search working, use the syntax that the community  generally use, and plug in the flickr API. 