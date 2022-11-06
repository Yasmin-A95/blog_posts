# API Basics - CRUD with a DIY API

#### API's are Weird

Today as a means of teaching myself, I'm going to break API's down a bit by making a practice one and doing some CRUD stuff. API's are weird, getting them to behave is hard, but maybe in making one and practising making requests, I'll be able to visualise them better when I'm problem-solving trying to get one to work. 

#### CRUDCRUD API 

[crudcrud](https://crudcrud.com/) is a service that handles your backend code for you! You can get a REST API working on your front end without working out the backend first. 

![Screen Shot 2022-08-25 at 8.23.00 am.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661379793509/5blaDjcgn.png align="left")

Navigate to the link above, and you should land here. Copy paste the unique link in the centre and take a look. At first, you shouldn't see much of anything, just an empty array. The magic happens when you click the button and then navigate to the link just above it. Look at you go! You've got some JSON. 


![Screen Shot 2022-08-25 at 8.26.15 am.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661379988528/I-zlR3O4k.png align="left")

#### Postman

Now we're going to use [Postman](https://www.postman.com/) to make our requests. Postman has a heap of tools that allow you access to human-friendly visualisations of the interactions you're having with the API of your choice.

Navigate there with the link above and sign up, then create a new workspace. 


![Screen Shot 2022-08-25 at 8.29.07 am.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661380289782/BloPqCbxS.png align="left")

I called mine makingAPI. Name yours whatever. 

![Screen Shot 2022-08-25 at 8.32.15 am.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661380358857/QK2foWUZL.png align="left")

Once you're in your new workspace you're ready to make a new request. See that little plus button in the top left corner? Click it. 


![Screen Shot 2022-08-26 at 8.26.57 am.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661466454777/IMbMqbyt_.png align="left")

Paste your URL in, hit send, wait, and then you should get the treat of seeing the unicorn you created. You can make your own categories too. Let's throw /humans onto the end of our unique URL rather than Unicorns and make some POST requests. 
We could head back to postman to make our POST request, but let's bring some HTML and JavaScript into the mix for funsies. 

![Screen Shot 2022-08-26 at 8.38.49 am.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661467139068/Lu4nb6upk.png align="left")

#### Integrating API Requests into your Site
HTML:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Api Practice</title>
    <script src="js/scrips.js"></script>
</head>
<body>
    <h1>Coming Soon</h1>
    <form>
        <label>
            Human Name:
        </label>
        <input id="humanName" type="text" />
        <label>
            Flavour:
        </label>
        <input id="flavour" type="text" />
        <button id="submit-btn"> Submit your Delicious Data </button>
    </form>
</body>
</html>
```
SCRIPT:
```
function humanFactory(humanNameVal, flavourVal) {
    fetch('https://crudcrud.com/api/c72ead78fe12498baab7955f30007ddc/humans', {
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
        },
        method: "POST",
        body: JSON.stringify({
            "humanName": humanNameVal,
            "flavour": flavourVal
        })
    }).then(function (res) {
        console.log(res);
    }).catch(function (res) {
        console.log(res);
    });
}

function btnHandler(e) {
    e.preventDefault();
    const humanName = document.querySelector("#humanName").value
    const flavour = document.querySelector("#flavour").value
    humanFactory(humanName, flavour);
}

document.addEventListener("DOMContentLoaded", () => {

    fetch('https://crudcrud.com/api/c72ead78fe12498baab7955f30007ddc/humans').then((r) => {
        return r.json()
    }).then((data => console.log(data)));

    const button = document.querySelector("#submit-btn");
    button.addEventListener('click', btnHandler)
  });
```

Now you can make post requests from home. Go forth, play around with it and test out other crud stuff like update and destroy. 


