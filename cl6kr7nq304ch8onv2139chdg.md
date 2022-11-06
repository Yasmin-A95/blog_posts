# Intro to React - Big Boy Time

#### Setup

Move into or create a file to store your project. `cd` into it in terminal and `npx create-react-app image-search`. Once that's done `cd image-search` and `mkdir src/components` then `mv src/App.js src/components/`. Take all that to your editor, for me that mean's `code .`. Then jump back into terminal and `npm rum start` because  run and rum both work but rum is more *fun*. If you aren't into chrome specify a browser like so `BROWSER=firefox npm run start`.

For all that hardwork you're greeted with this error
```
Compiled with problems:X

ERROR in ./src/index.js 7:0-24

Module not found: Error: Can't resolve './App' in 'your/path/here'
```

That's alright though, we're *error driven developers*. That means errors ARE ALWAYS GOOD. Yeah.* Error driven*. Let's fix it. In index.js change the line `import App from './App';` to `import App from './components/App';`.

New error, hell yeah. I love errors. 
```
Compiled with problems:X

ERROR in ./src/components/App.js 4:0-30

Module not found: Error: Can't resolve './logo.svg' in 
```
Let's go into App.js and delete all that stuff we don't need. Go from this:
```
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```
To this:
```
function App() {
  return (
    <div className="App">
    Hello World!
    </div>
  );
}

export default App;
```

A page that works?! Boo! I hate pages that work. Let's make an error so I'll be able to sleep at night. You know what that means, unless you don't. Go read the first blog [intro to react](https://yasmina95.hashnode.dev/intro-to-react).

#### Create The Tag You Wish Existed

Manifest it babes. 
```
function App() {
  return (
    <div className="App">
      <ImgSearch />
    </div>
  );
}

export default App;
```

A yummy error. Look.
```
Compiled with problems:X

ERROR

[eslint] 
src/components/App.js
  Line 4:8:  'ImgSearch' is not defined  react/jsx-no-undef

Search for the keywords to learn more about each error.
```
Now that life has meaning again, let's go fix it. 

#### Define It 

Create a file in src/components called `ImgSearch.js` and throw all this in there.
```
import React from "react";

const ImgSearch = () => {
    return(
    <div>
        <h1> this thing will exist soon I promise </h1>
    </div>
     );
}

export default ImgSearch
```
This line isn't really necessary, but it was once upon a time and so a lot of things look like this. It doesn't hurt to include it, and it might offend the eyes of your manager who's old and is used to react code looking a certain way. Include it and do dear old Harold a favour. 
```
import React from "react";
```
#### Make It Avaliable

Oh wait we already did that here. 

```
export default ImgSearch
```

We haven't fixed the error yet though. App.js hasn't heard of ImgSearch.js.

 #### Import It
```
import ImgSearch from "./ImgSearch";
function App() {
  return (
    <div className="App">
      <ImgSearch />
    </div>
  );
}

export default App;
```

Our error is gone. I'd be sad if it weren't for the fact that we still have a job to do, we made a *promise* after all. Before we jump into that, a little bit on why you may want to keep App.js even though it's not serving a purpose right now.

It's the parent element of ImgSearch, and that's all the functionality it's got. However if we were to be rid of it, and we made our ImgSearch the highest level parent.. or ancestor I guess I might call it. Sure, why not. 

If we made ImgSearch the ancestor of all following descendants and then find that we want to extend our site beyond simply an image search, we would need something a level higher than ImageSearch to make another family line from. To all the experienced devs out there reading this and tutting at all the weird extra terms I'm inventing, be quiet or I'll add you to my errors list.

Anyway that's why we're keeping it. Another thing to note are the enclosing divs. 
```
   <div>
        <h1> this thing will exist soon I promise </h1>
   </div>
```

The fancy choice here would've been to use jsx components, but I'm a simple gal so I'm using divs today. Alright, let's leave that promise on the back burner for a second because I'm starting to get jittery, I need some of that error page good good. 

Add the following to ImgSearch.js.
```
import React from "react";

const ImgSearch = () => {
    return(
    <div>
        <h1> this thing will exist soon I promise </h1>
        <SearchForm />
        <Gallery />
    </div>
    );
}

export default ImgSearch
```
Nice. Look at that error.
```
Compiled with problems:X

ERROR

[eslint] 
src/components/ImgSearch.js
  Line 7:10:  'SearchForm' is not defined  react/jsx-no-undef
  Line 8:10:  'Gallery' is not defined     react/jsx-no-undef

Search for the keywords to learn more about each error.
```
#### State

`<Searchform />` will definitely need state. State, which you would know all about if you read my part one like I told you to, is relevant to anything a user is going to interact with. Buttons and inputs being just two examples. `<Gallery />` on the other hand, is not an interactive feature. All we want that to do is do display the images returned from our search. 

Let's use a class for SearchForm to start out. Later on you'll start doing it the way the community generally do, but let's use class the way mother Zuckerberg intended before we move onto our rebellious teenage years. 

Make your `src/components/SearchForm.js` file and throw in the following.

```
import { Component } from "react";

class SearchForm extends Component {
    render() {
        return( 
        <form> Search form coming soon probably </form>
        )
    }
}
export default SearchForm
```
In `ImgSearch.js` we have to import our `SearchForm` or it might as well not exist. 
```
import React from "react";
import SearchForm from "./SearchForm";

const ImgSearch = () => {
    return(
    <div>
        <h1> this thing will exist soon I promise </h1>
        <SearchForm />
        <Gallery />
    </div>
    );
}

export default ImgSearch
```

Now we've only got one error showing up.
```
Compiled with problems:X

ERROR

[eslint] 
src/components/ImgSearch.js
  Line 9:10:  'Gallery' is not defined  react/jsx-no-undef

Search for the keywords to learn more about each error.
```
Alright. Let's give functions a go. These are generally used rather than classes now that Mother upgraded them to have state. I'm pretending that's not true for right now though to learn OG react and develop a deeper understanding of how it was intended to be used. 

So because classes are the only things that have state in this fine year of 2017, and gallery need not have any state, I can use a function. 

Make `Gallery.js` and write the following. 

```
import React from "react"

const Gallery = (props) => {
    return <div>Gallery Coming Soon</div>
}

export default Gallery
```

Back in `ImgSearch.js` we import it.
```
import React from "react";
import SearchForm from "./SearchForm";
import Gallery from "./Gallery";

const ImgSearch = () => {
    return(
    <div>
        <h1> this thing will exist soon I promise </h1>
        <SearchForm />
        <Gallery />
    </div>
    );
}

export default ImgSearch
```

Oh yeah. That's going in the portfolio. 

![Screen Shot 2022-08-08 at 7.43.31 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659951822670/m8L9SJW4w.png align="left")

#### Under the Hood
Let's have a squizz under the hood. Note, that one of the side effects of a framework that need not have us refresh the page to see our newly coded beauties, is that all the old error messages stay in the console. Refresh if they stress you out. But they shouldn't because errors are great we love errors and we love fixing errors. 

Locate your fancy purple dev tools by clicking the `>>`. Fun stuff hey. 


![Screen Shot 2022-08-08 at 7.45.35 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659951949688/9UDzunlU8.png align="left")

 Alright, let's get closer to a functional search. In `SearchForm.js` code out the following.
```
import { Component } from "react";

class SearchForm extends Component {

    _handleSubmit(event){
        event.preventDefault()
    }

render() {
     return( 
      <form>
        <input typeof="search" required placeholder="nothing creepy please" />
        <input type="submit" value="Search" />
      </form>
      )
  }
}
export default SearchForm
```
#### Event Handlers
Event handlers start with an underscore as a standard practice, it's not required for functionality per se, but it's good to keep the practice as a means of communicating with other people who might see your code. 
```
 _handleSubmit(event){
        event.preventDefault()
    }
```
Anytime you want a single page app you'll need to disable the form so that It doesn't try to send the user to another page. That's where `preventDefault` comes in. 

I included `nothing creepy please` as my placeholder, as it's best practice to discourage furries from using your site. 

Let's attach our method like so.
```
render() {
        return( 
        <form onSubmit={this._handleSubmit} >
            <input typeof="search" required placeholder="nothing creepy please" />
            <input type="submit" value="Search" />
        </form>
        )
    }
``` 
#### Handling Data, Parents and Children
Time to discuss how we're going to handle our data. I don't want to entangle my search form in the data returned from the flickr api I intend to use. That would make this code specific to that functionality, and the good thing about React is getting to use the same code in more than one place for more than one thing. 

More than that, our SearchForm and Gallery are *siblings*. Siblings cannot communicate, this family is a broken one tethered together in only one direction, down from grandparent to parent to children. 

Let's explore the problem. 

Update SearchForm to include the following.

```
import { Component } from "react";

class SearchForm extends Component {

    _handleInput(event) {
        console.log(event.target.value)
    }

    _handleSubmit(event){
        event.preventDefault()
    }

    render() {
        return( 
        <form onSubmit={this._handleSubmit} >
            <input onChange={this._handleInput}  typeof="search" required placeholder="nothing creepy please" />
            <input type="submit" value="Search" />
        </form>
        )
    }
}
export default SearchForm
```

`event.target.value` is similar to jQuerys `val()`, but rather than having the dom talk to us, the event object is. If you'd like to take a look at event object, change the console.log to `console.log(event)`

It should look like this. 

![Screen Shot 2022-08-08 at 8.34.32 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659954886406/BsGhb_XCB.png align="left")

While `console.log(event.target.value)` outputs this. 


![Screen Shot 2022-08-08 at 8.35.45 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659954954428/n_msxh69e.png align="left")

Now we need to store the `state` somewhere. Let's update our `SearchForm` and `_hanldeInput` method. 

```
class SearchForm extends Component {
    constructor(){
        super();
        this.state={ query: "" };
        this._handleInput = this._handleInput.bind(this);
    }

    _handleInput(event) {
        this.setState({query: event.target.value})
    }
```
`this._handleInput = this._handleInput.bind(this);` is an important line, by binding it to the parent we're ensuring that when we use it as an event listener it maintains its inheritance from its parent element. Just trust me. You gotta include it or else this wont work:
```
  _handleInput(event) {
        this.setState({query: event.target.value})
    }
```
Keep in mind though, `this.setState({query: event.target.value})` is asynchronous, which can throw a spanner in the works depending on what you're getting up to with it.  

For a bit of fun why don't we play around with interpolation like this.

```
<input type="submit" value={ `Search for ${ this.state.query }` } />
```

![Screen Shot 2022-08-08 at 9.26.37 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659958007399/iHyZsTaY6.png align="left")

Now because it's the grand old year of 2017 we've made a mistake in how we defined ImageSearch. It's a function! Those can't have state! We're going to have to get onto fixing that. 

Fun.
#### Child to Parent Communication

How can a child communicate to a parent exactly? React doesn't like that. Children are to be seen and not heard. There is a method for going about it though, and that's to have a function passed down to a child. We define the function in the parent, pass it down, and then it can return information that only the child knows! It's in this way that we can skirt around the strict rules about passing information down rather than up. 

React has changed a lot over the years, and so it's more complicated than you'll find in this blog post, but again, this is 2017 so we've got our whole lives ahead of us to figure the rest out.

Part Three Coming Soon I Hope. AXIOS Speedrun / API Plug In Finally
