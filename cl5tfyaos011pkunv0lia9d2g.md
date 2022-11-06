# Beginners CRUD on Rails: Lazy Edition

The best thing about ROR is all the things it gives you for free, so long as you follow certain conventions. In my last post, I hardcoded a lot of things unnecessarily. If you followed along on that adventure, you'll really appreciate the beauty of what I'm about to show you.

As we did last time, in your terminal: `rails new your_chosen_name_app` + `'--skip-git` if you don't want it to make a new git repository. Throwing app on the end of the name for good measure so that we don't name our tables the same thing as our file name (this can cause problems, trust). 

Let's set up a better example than my last one. `rails new library --skip-git` then cd into your chosen folder name. In my case, `cd library` then we type in `rails db:create`

**Now time for a fancy new trick.**

 `rails generate migration create_authors`, here I didn't need to throw app onto my folder name since as I won't have any tables for 'librarys'. Now open it in your editor and navigate to the db folder, then migrate. You should see your new rubyish table set up and ready for your columns! Mine looks like this: 

```
class CreateAuthors < ActiveRecord::Migration[5.2]
  def change
    create_table :authors do |t|
    end
  end
end
```
The t there is your table helper! Now we can tell ruby how we want our table to look, this time without having to code in the less forgiving language of SQL. How we name our columns with our handy table helper is as follows. 

```
class CreateAuthors < ActiveRecord::Migration[5.2]
  def change
    create_table :authors do |t|
      t.text :name
      t.text :nationality
      t.date :dob
      t.text :image
      t.text :quote
      t.timestamps
    end
  end
end
```

Let's break that down. The format goes t.datatype followed by :column_name. No commas on the end this time, just a new line.

```
 t.text :name
```

Timestamps are something ruby will generate for you for free so that you have a record of when you've created an author or updated one. It's easy enough to pop it in just in case you need it since you only have to code this once and then never think about it again. You may find two years into your project all of a sudden this category is relevant, since you threw it in there from the beginning you already have all that tasty data. Yum yum. 

```
t.timestamps
```

Back in terminal run `rails db:migrate` 

If this was successful, you should see your table when you navigate to the .schema file in your editor. This is what mine looks like. 

```
ActiveRecord::Schema.define(version: 2022_07_20_070654) do

  create_table "authors", force: :cascade do |t|
    t.text "name"
    t.text "nationality"
    t.date "dob"
    t.text "image"
    t.text "quote"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

end
```

Don't alter this file, it's an auto-generated map of what you have rather than something you can alter. If you've noticed a mistake in your table have no fear, there's an easy fix. In your terminal run `rails db:rollback`. You can rollback as many times as you'd like, to see what the state you've gotten to check .schema in your editor again. Make any changes you'd like and then just run `rails db:migrate` again in your terminal. Heads up, this doesn't work so smoothly if you've already committed changes to github. 

Now let's make our author model. Navigate to app/models and right-click to make a new file named author.rb in my case. Its best practice to use the singular here rather than the plural of authors. Mine looks like this.

```
class Author < ActiveRecord::Base
end
```
Now that we have our Author class inheriting from ActiveRecord::Base, rails will be able to write our SQL for us. What a treat, thanks Rails! This is the point where I'm going to include pry in my gemfile, for the details on how to do that check out my last ROR [blogpost](https://yasmina95.hashnode.dev/ror-beginners-guide-crud-getting-started). 

I like to check my work regularly on the way so I can debug as quickly as possible, so with my pry gem installed I'll go to the terminal and run the `rails console` then enter `Author.new` to check that it's heard of an Author, and all the appropriate columns are there.

Here I added some seed data to my Author's, so if you're coding along with me do the same and run `rails db:seed` in the terminal.

**Fancy trick number two**

Navigate to your routes.rb and enter

```
Rails.application.routes.draw do
  resources :authors
end
```
The pluralisation here is best practice. No more hard coding the routes for us! To have a look at the magic under the hood enter `rails routes` into your terminal. This is mine.
```
  Prefix Verb   URI Pattern                 Controller#Action
    authors GET    /authors(.:format)          authors#index
            POST   /authors(.:format)          authors#create
 new_author GET    /authors/new(.:format)      authors#new
edit_author GET    /authors/:id/edit(.:format) authors#edit
     author GET    /authors/:id(.:format)      authors#show
            PATCH  /authors/:id(.:format)      authors#update
            PUT    /authors/:id(.:format)      authors#update
            DELETE /authors/:id(.:format)      authors#destroy
```
There's a hot debate on what the differences between patch and put are, as well as when they should be used. However not a lot of browsers support either yet, and so they're interpreted as a post regardless. 

**Another hot new trick **

Enter `rails generate controller Artists index new edit show`. `rails generate controller Artists` will give us all this and more. However, this creates a bunch of things we won't want for our crud app. Let's specify now rather than going through and deleting junk later.

Rails has in fact made some junk for us to delete, though less so than it would have if we hadn't been specific about our terminal command just now. In routes.rb we have a few things that are redundant. 
``` 
Rails.application.routes.draw do
  get 'authors/index'
  get 'authors/new'
  get 'authors/edit'
  get 'authors/show'
  resources :authors
end
```
Let's delete everything our resources :authors was already doing.
```
Rails.application.routes.draw do
  resources :authors
end
```
Now when we run `rails server` in the terminal and then navigate to http://localhost:3000/authors on our browser, we've got the bones of our page already!

Let's give our page the seed data we've added. Navigate to authors_controller and add a class instance variable in. That's the little guy with a fun hat on down there.

```
class AuthorsController < ApplicationController
  def index
    @authors = Author.all
  end

  def new
  end

  def edit
  end

  def show
  end
end
```
```
def index
    @authors = Author.all
```
You can think of an instance variable as somewhere between global or local. [Ruby-doc.org](https://ruby-doc.org/docs/ruby-doc-bundle/UsersGuide/rg/instancevars.html) describes it like this: "its scope is confined to whatever object self refers to". You'll get the hang of it best by practising using it in different places though, as with all things code spending time tinkering around is the best way to learn. Speaking of, let's make our index page a bit more interesting. 

***More fun tricks***
Here's an example of our instance variable being used in a loop. For each author I'd like their image displayed, but only if there is an image.

```
<h1>All Authors</h1>
<% @authors.each do |author| %>

    <%= image_tag author.image if author.image.present? %>
        <ul>
            <li> Name: <%= author.name %> </li>
            <li> Quote: <%= author.quote%> </li>

        </ul>
<% end %>

```
These guys are the embedded ruby tags (ERB). These two are non-echoing ERB tags for things we don't want to be displayed on our page.
```
<% "this won't be displayed" %>
```
```
<%= "Whereas these echoing ERB tags WILL be displayed" %>
```
Another new we've got up our sleeves is the image_tag method. No need to write HTML when we're in ruby-mode. Well. Less at least. Here's a [link](https://api.rubyonrails.org/v7.0.3/classes/ActionView/Helpers/AssetTagHelper.html) to some more of these handy methods 

Last but not least, by including the following I'm ensuring that my page won't break if a user happens to create a new author without including an image. 
```
if author.image.present?
```

Now our index page has so much more info on it!

You can even add classes to your images in that same block of code. If we code the following and add some styles to our feature class in CSS, we can alter the size of our images to make them appear more uniform on our index page.

```
<h1>All Authors</h1>
<% @authors.each do |author| %>

    <%= image_tag author.image, :class => 'feature' if author.image.present? %>
        <ul>
            <li> Name: <%= author.name %> </li>
            <li> Quote: <%= author.quote%> </li>

        </ul>
<%end%>
```
Adding another method into the mix, we can make the author name a clickable link.

```
<h1>All Authors</h1>
<% @authors.each do |author| %>

    <%= image_tag author.image, :class => 'thumb' if author.image.present? %>
        <ul>
            <li> Name: <%= link_to author.name, author %> </li>
            <li> Quote: <%= author.quote%> </li>

        </ul>
<%end%>
```
Now if we click on an author's name we go to a page with their ID in the URL. Tails autogenerated the ID for us without us ever even having to ask it to. It's not a particularly interesting page though. Let's add some flavour.

```
<%= image_tag @author.image, :class => 'feature' if @author.image.present? %>

<ul>
    <li> Name: <%= @author.name %> </li>
    <li> Nationality: <%= @author.nationality %> </li>
    <li> Date of Birth: <%= @author.dob.strftime '%B %d, %Y'> </li>
    <li> Quote: <%= @author.quote %> </li>
</ul>
```
For this to work we head over to our authors_controller.rb file and add this.
```
 def show
    @author = Author.find params[:id]
  end
```

Now that's sorted, lets go back and discuss what the heck this thing is.

```
 <li> Date of Birth: <%= @author.dob.strftime '%B %d, %Y' %> </li>
```
strftime! What a fun thing. It changes a date into a human readable string, you can even get it to calculate the day somebody was born, even if they happened to be born a hundred years ago. It's supported in a great many programming languages, and you can mess around with it until you've got it displaying how you like it in this here [sandbox](https://www.strfti.me/). Fun!

That's it for the tips and tricks today, I hope you're as relieved as I am to be hardcoding less of this finicky business. 
