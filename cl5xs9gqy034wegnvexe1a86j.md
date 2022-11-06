# Project 1 - Day 1 - MVP V1

I was debating about whether or not the MVP version of my project idea was good enough (see the map out [here](https://yasmina95.hashnode.dev/project-1-day-0). Self-doubt is rearing its ugly head and whispering sour somethings into my ear. "What if you aim so low and fail anyway? How much more embarrassing would that be rather than if you aim for something so difficult that nobody really expects that you'll be able to achieve it?". 

That aside, I persist. I set up my first model `rails generate model Story bit:string`. Here I decided that each bit of the story should be a string, as I wanted to use the 255-character limitation of that datatype. That's it, the only model I need for the MVP, with its whopping 1 column (timestamps doesn't count).

```
class CreateStories < ActiveRecord::Migration[5.2]
  def change
    create_table :stories do |t|
      t.string :bit

      t.timestamps
    end
  end
end
```
Now if I add 
```
class StoriesController < ApplicationController
  include ActionController::Live

  def index
    @stories = Story.all 
    @story = Story.new 
    render :index 
  end
end
```
Along with my index.html.erb:

```
<h1>Welcome To The Wonderful World of This Site Existing</h1>
```
I can confirm things are working as they should, with a `rails console` and `Story.new` for good measure. 

By the end of the day, it's fleshed out to a fully formed website ready to test.

```
<h1>Welcome To The Wonderful World of This Site Existing</h1>

<section class="story-area">
    <% @stories.each do |story| %>
    <p> <%= story.bit %> </p>
<%end %>
</section>

 <section class="story-area" id="text-input">
        <%= form_for @story do |f| %>

          <%= f.label "Your turn" %>
          <%= f.text_area :bit, :placeholder => "Once upon a time, blah blah blah", class: 'text-field'   %> <%# , :maxlength => 250? %>
          <%= f.submit class: "submit-button" %>
      
        <% end %>
        
      </section>
``` 
I opt for sections here because in learning about screen-reader accessibility and good use of semantic HTML. It seemed more fitting than a div given that it made up a significant section of the page rather than just being a box I'd use for styling. 

```
class StoriesController < ApplicationController
  include ActionController::Live

  def index
    @stories = Story.all 
    @story = Story.new 
    render :index 
  end

  def new
    @story = Story.new
  end
  def create 
    @story = Story.new story_params
    @story.save
    redirect_to stories_path
  end
  private 
  def story_params
    params.require(:story).permit(:bit)
  end
end
```
In my application.html.erb I threw in a div for styling. 
```
  <body>

    <div class="outer-container">

      <div class="container">
        
      
      <%= yield %>

     
      </div>

    </div>

  </body>
```
After an evening of some fiddling with the following css
```
@import url('https://fonts.googleapis.com/css2?family=Sigmar+One&display=swap'); /* Chonky text */

 @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap'); /* Bit text */
 
 
 h1 {
   font-family: 'Sigmar One', cursive;
   font-size: 2em;
   text-align: center;
   padding-bottom: 1.5rem;
 }

 body {
    font-family: 'VT323', monospace;
    font-size: 1.5em;
    background-image: linear-gradient(rgb(179, 0, 255), rgb(255, 255, 227));
    background-repeat: no-repeat;
    background-attachment: fixed;
}

.container {
    max-width: 960px;
    margin: 0 auto;
}
.story-area {
    display: block;
    list-style-type: disc;
    margin-block-start: 1em;
    margin-block-end: 1em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    padding-inline-start: 40px;
    padding-inline-end: 40px;
    padding-top: 1rem;
    padding-bottom: 1rem;
    background-color: aliceblue;
    /* box-shadow: rgba(6, 24, 44, 0.4) 0px 0px 0px 1px, rgba(6, 24, 44, 0.65) 0px 4px 6px -1px, rgba(255, 255, 255, 0.08) 0px 20px 30px -10px; */
    box-shadow: rgba(0, 0, 0, 0.4) 10px 10px;
}

#text-input {
    background-color: aliceblue;
    width: max-content;
    display:inline-block;
    width: 100%;
    margin: 8px 0;
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
}

.text-field {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
}

.submit-button {
    font-family: 'VT323', monospace;
    padding: 11px 19px;
    font-size: 22px;
    border-color: rgba(255, 255, 227, 0.1) rgba(255, 255, 227, 0.1) rgba(255, 255, 227, 0.25);
    background-color: rgba(251795, 0, 255, 0.5);
    text-shadow: 0 -1px 0 rgb(0 0 0 / 25%);    
    color: #ffffff;
    -webkit-border-radius: 6px;
    -moz-border-radius: 6px;
    border-radius: 6px;
}
``` 

Voilà, a MVP site was born. 

![Screen Shot 2022-07-23 at 8.54.06 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658573662514/xyObCX5ZC.png align="left")

This was the point where I attempted to deploy it and get 'pages' working via GitHub, only to find out that the readme file was as best as that was ever going to get displayed. Tomorrow, Heroku. 
