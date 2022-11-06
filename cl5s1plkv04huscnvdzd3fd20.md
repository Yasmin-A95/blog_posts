# ROR Beginner's Guide: CRUD - Getting Started

From setting up to your first working page: CRUD with Rails.

Assumed Knowledge: This article was written with people who know what a CRUD app is, and who have made one before without using rails, perhaps with Sinatra. 

In the beginning the lord said "cd into the folder you made for your CRUD app in the terminal and type: ` rails new view-helpers `with or without skip git i.e `rails new view-helpers --skip-git` depending on whether you'd like it to make a new git repository for you or not". Folders! Miracles occur every day.
`cd view-helpers`. Looky there, you've got your view-helpers all sorted. `cd ..` to go back up a level in your directory for the next step.

Next `rails new some_app_name` - don't name it something you may be making a table for. If you're making a crud fan-site for me I'm very flattered. Also, it may be tempting to name it after me `rails new Yasmin`. However, this can cause problems later, so a safe bet is to throw app onto the end of the name `rails new Yasmin_app`. Now `cd Yasmin_app` and `rails db:create`. The terminal adage "no news is good news" doesn't apply here. You should see `Created database 'db/development.sqlite3'` and `Created database 'db/test.sqlite3'`. Assuming things haven't gone terribly wrong, congratulations, you've got a database! Just in case things have gone terribly wrong, let's do a sanity check. Enter `rails db` and you should see `sqlite>`. Throw in a `.schema` for practice and if nothing happens everything is going fine probably. 

CTR D to exit rails db (for mac terminals). `touch db/create_yasmins.sql`(more on the pluralisation later). Open it in your editor, and navigate to the db file. If you're using Visual Studio Code do yourself a favour and install the code command by opening VS code and hitting command shift p and typing in '>'. You should see 
"Shell Command: install 'code' command in path". Do so, go back to the terminal, and enter `code .`

Again I digress for my fellow VScoders, you can shortcut your way to the relevant files using command p, and in this case, typing in 'create', you should see the right file pop up without having to painfully traverse the many folders.

Great, you've successfully made the file, and you've successfully navigated to the file. If that's not true for you, damn. Anyway for everybody else, now let's make our table. 
```
CREATE TABLE yasmins (
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
image TEXT,
hottness FLOAT,
coolness FLOAT,
enemies INTEGER
);

```
Let's break that down a bit. Here we're creating the table, sql syntax requires these commands must be in uppercase while your custom table name should not. Convention says name your table with the plural. Here I'll admit that I regret my example choice now because "yasmins" makes no sense. Hindsight is 20/20 but time is of the essence so let's all just deal with it. 
```
CREATE TABLE yasmins (
```
Here we're making a column for an individual yasmin to have an id. As with 'yasmins' 'id' is in lowercase and the rest in uppercase because it won't work otherwise. SQL syntax is very unforgiving, so make sure you type carefully. We're setting the primary key to autoincrement so that it'll automatically number each new yasmin one after the other. Again, syntax is important, it must have a comma at the end. 
```
id INTEGER PRIMARY KEY AUTOINCREMENT,
``` 
Here we're giving the table a column of name in case one of the many yasmins spells her name yasmine or something, and we're assigning it text. We could use a string here as well, in some cases text is necessary because a string is limited to 250 characters.
```
name TEXT,
```
Ah, a case where text was needed! A url for an image may be longer than 250 characters (though please don't hotlink images in a site you're making that isn't just for practice purposes. If it will see the light of day, do not hotlink!). 
```
image TEXT,
```
We're using a floating point number here because my hottness may be a very big and complicated number with many decimals at the end.
```
hottness FLOAT,
```
Here we're using an integer because my enemies are few in numbers (this is a warning by the way). Note that this last column **does not** have a comma. The last column can't. Again SQL is really finicky. It also **must have** the closing parentheses with the semicolon. 
```
enemies INTEGER
);
```
Did you get the syntax right? Check again. Ok good. Now go back to the terminal and `cd db` then `sqlite3 development.sqlite3 < create_yasmins.sql`. Do yourself a favour and hit tab after every few letters rather than manually entering the whole thing in order to prevent typos. Forewarning, it is annoying to edit your table beyond this point, so try and get it right the first time where possible. 

Let's check things haven't gone horribly wrong as things are wont to do in your early coding experiences. `cd ..` back up a level and `rails db` then `.schema`. If things have gone right, you should see your table! If things have gone wrong, dang. 

Now CTR D and `code .` Now you're ready to set up your model file. CTR click on 'controllers' and make a new file called "yasmin.rb". The convention here is to name this in the singular, not the plural. In "yasmin.rb" the class Yasmin will inherit from ActiveRecord::Base
``` 
class Yasmin < ActiveRecord::Base
end
```
This is where we would need to configure things if we were making tables with associations e.g. has_many. But we're not, unless you are. If you are here's a resource ([click me](https://guides.rubyonrails.org/association_basics.html)). 

Back to the terminal. `rails console` will give you access to irb by default. Do a sanity check again to see that `Yasmin` exists. Then `Yasmin.new` to check that ActiveRecord has connected.  All the correct column names should appear though they'll be nil since we haven't actually entered any data yet.

If like me you prefer pry to irb you can use this instead by navigating to the Gemfile in VS code going down to the development group and throwing pry onto the bottom. This is what mine looked like:
```
group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
gem 'pry-rails'
end
```
Now's your chance to include any other gems you'd like to. Fun fact: To do so somewhere in the Gemfile other than the above would mean that they're included in the finished app rather than just while it's being developed. 

Now back in the terminal exit irb and enter `bundle`. You need to do this every time you want to update the Gemfile. Now if you `rails console` again you'll be in pry. Yay! Here you can even add data to your table like so 
```
y = Yasmin.new
y name = "Yasmin"
# ... etc
Yasmin.save
``` 
God that was a terrible choice for an example. Oh well. 

I prefer to do so in the seed file though. Navigate to seeds.rb in VS code and do something like the following 

```
Yasmin.create :name =>, 'Yasmin', :hottness =>  1000.132124, :enemies => 0
```
You don't have to fill out every column, that will just leave their value as nil. Do this for as many examples as you please. It's a good idea to have some data in your table early on so that you can see your database working in action. 

Now in the terminal enter `rails db:seed`. You may want to use command t to open a new terminal window so that you can use pry again without having to close it every time you need the terminal again. As you're making your CRUD app you might end up having three terminal windows open at all times, one as the server, one for pry and one for anything else you may need intermittently. 

Now in pry we'll do another check `Yasmin.count`, you should see a number to indicate the seed data is indeed there. Another way of doing this is to add a puts statement into your seeds.rb file. Navigate there and add
```
Yasmin.create :name =>, 'Yasmin', :hottness =>  1000.132124, :enemies => 0
# Seed Data
puts "#{ Yasmin.count } Yasmin's created"
```
Now in the vanilla terminal (as in, not irb or pry) run `rails db:seed` again. You may have ended up with even more seed data than you intended to, to prevent this it's best practice to go back and include
```
Yasmin.destroy_all
Yasmin.create :name =>, 'Yasmin', :hottness =>  1000.132124, :enemies => 0
# Seed Data
puts "#{ Yasmin.count } Yasmin's created"
```
at the top of your seeds.rb file. This stops you from continuing to accidentally create many identical copies of your seed data every time you run `rails db:seed` in your terminal. Huzzah, look at you go. What nice self-cleaning code.  

Navigate to routes.rb in VS code. Time to make our first page. Using the plural form is good practice again here, Rails is all about convention over configuration. 

``` 
Rails.application.routes.draw do
  get '/yasmins' => 'yasmins#index'
end
```
Enter `rails server` into the terminal, open your browser, and navigate to http://localhost:3000/ 
Here you should see "Yay! You’re on Rails!". Now navigate to http://localhost:3000/yasmins
Oh dear everything is broken. Want a clue as to why? Navigate to http://localhost:3000/rails/info/routes 
This will be helpful in debugging as you go! 

Let's get ourselves in order. Navigate to the controllers file in VS code and right click to create a new file named yasmins_controller.rb

```
class YasminsController < ApplicationController
    def index
    end
end
```
If you go back and check http://localhost:3000/yasmins still won't work. There's one last step in setting up our page. Navigate to the views folder, right-click on it and add a new folder named Yasmins (plural). To Yasmins add a file called index.html.erb , throw in some html like so
```
<h1> Stuff will go here </h1>
```

Then try again on http://localhost:3000/yasmins If this didn't work for you, ensure that you followed the previous steps correctly and put all the files in the right folders. If you accidentally put the folder Yasmins and index.html.erb in views/layouts rather than just views, your site won't work. This is why opting for convention over configuration is important. Customise all you like, just know you're in for a world of extra configuration.

And that's how to get your first page working! Follow the last few steps again in order to make more of them, you will want to do extra fancy things such as post rather than get and other such things later on.
```
Rails.application.routes.draw do
  post '/yasmins' => 'yasmins#create'
end
```
But that's a story for next time. Goodnight kids. 