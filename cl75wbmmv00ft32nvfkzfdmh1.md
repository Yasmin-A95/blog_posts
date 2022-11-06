# Vue Quickie

#### Vue, What?

Vue, it's like React. Kinda.

#### Vue, How?

Move into or create the relevant folder, `mkdir js`, then `cd js` + `curl https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js >> vue.js`. `touch scripts.js ` + `cd` to the root directory and then `touch index.html`.

In index html ensure you include the vue script source in the head. It doesn't work right if you throw it in the bottom of your body. However, your script src needs to be included in the body tag unless you create a document ready function. We're going to do that for neatness's sake though. 
```
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./js/vue.js"></script>
    <script src="js/scripts.js"></script>
    <title>Vue Wow</title>
</head>
```

In the document body include the following.
```
<div id="vm">
        {{ message }}
</div>
```

If you take that into the browser you're not in for much of a treat. Let's get Vue functional in our scripts.js.
```
document.addEventListener("DOMContentLoaded", () => {
    const vm = new Vue({
        el: '#vm',
        data: {
            message: 'Hello World'
        }
    });
});
```

So what the hell did we just do? We asked the Vue function to create a new instance vue, and we've assigned it to a variable. In this case the variable was vm but you can make it anything you like as it's just a variable name, same as always. I used vm here because the docs explain that this is the convention. Vue was inspired by the model-view-viewmodel pattern. Read more about that [here](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel) if you wish.

```
const vm = new Vue
```
After that, we add a data object. When a vue instance is created all the properties found in the data object are handed over to Vue. This allows us to hand the keys over to the DOM and let Vue deal with it. In the words of the Vue [docs](https://v2.vuejs.org/v2/guide/instance.html), we're adding these properties to their reactivity system. The more obvious name was taken already.