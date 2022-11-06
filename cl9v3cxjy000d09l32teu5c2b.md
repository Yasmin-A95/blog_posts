# Using a Ruby on Rails API as your backend

Let's make a rails API and use it as our backend, so we can plug whatever shiny new best-practice buzzword frontend we'd like into it. Probably React, let's be honest. Onward. 

#### Assumed knowledge 

This tutorial assumes you know your way around a command line interface, ruby/ruby on rails, PostgreSQL, code editors, and what an API is. I've also written it as if you're using VS Code and iTerm. Due to the passage of time, even if you do have my set-up, results may vary, google is your friend. 

#### In the beginning 

The lord said  `rails new mixology_api --api --database=postgresql`, and so shall you. Unless you're making some different kind of API in which case insert your filename where appropriate ya silly, stop blindly copy-pasting! Otherwise, perhaps you don't have [PostgreSQL](https://www.postgresql.org/download/), in which case, go get it. 

If you've done this correctly, you'll be able to take it to your editor, check out the `database.yml` file and see `PostgreSQL` mentioned a whole lot. Another thing to have a squizz at is `application_controller.rb`.

```rb
class ApplicationController < ActionController::API
end
```
We're inheriting from `ActionController::API` instead of the usual `ActionController::Base`. Fun!

`rails db:create` to init that database. 

#### Models

`rails g scaffold mixologist name:text image:text`

If you want to win best practice awards, **do not this:** `scaffold`. Why? It makes a bunch of stuff you might not use and is therefore a bit of a messy app. However, for the purposes of a quick app to learn things at a top level, go for it and scaffold away. 

`rails g scaffold drink name:text ingredients:text mixologist_id:integer image:text`

Note `mixologist_id:integer`. This is our foreign key. When you want to create models that relate to one another, in this case, by way of one thing *having* another, you've got to use foreign keys and primary keys. The thing which `has_many` contains the primary key. The primary key you needn't concern yourself with when you're generating the model as Rails always includes an id column for free which we will use as our primary key. However, to use that id as the foreign_key of that which belongs_to, you've got to make a column in the table of that which is had, hence `mixologist_id:integer`.

If you've got a complex set of relationships going on feel free to refer to the [docs](https://guides.rubyonrails.org/v2.3.8/association_basics.html) or this [blog post](https://yasmina95.hashnode.dev/crud-on-rails-users-security-many-to-many-relationships-and-more) I prepared earlier. 

Now, if you navigate to `db/migrate` you'll see the tables we just created. 

```rb
class CreateDrinks < ActiveRecord::Migration[5.2]
  def change
    create_table :drinks do |t|
      t.text :name
      t.text :ingredients
      t.integer :mixologist_id
      t.text :image
      
      t.timestamps
    end
  end
end
```
```rb
class CreateMixologists < ActiveRecord::Migration[5.2]
  def change
    create_table :mixologists do |t|
      t.text :name
      t.text :image

      t.timestamps
    end
  end
end
```
#### Relationships 

In drink.rb include the following:
 
```rb
class Drink < ApplicationRecord
    belongs_to :mixologist, :optional => true
end
```

While in mixologist.rb we have the relatively simple:

```rb 
class Mixologist < ApplicationRecord
    has_many :drinks
end
```

Our drink class belongs_to one, and only one, mixologist. To make things easier on ourselves, we're including `:optional => true` here. 

Beautiful. `rails db:migrate` then let's have a look inside `rails db` and once you've dropped into the database `\d`. You should be looking at something like this:

```console
                     List of relations
 Schema |         Name         |   Type   |      Owner
--------+----------------------+----------+-----------------
 public | ar_internal_metadata | table    | your_name
 public | drinks               | table    | your_name
 public | drinks_id_seq        | sequence | your_name
 public | mixologists          | table    | your_name
 public | mixologists_id_seq   | sequence | your_name
 public | schema_migrations    | table    | your_name
(6 rows)
```
Then CTR-D out of there.

Another way we can quickly check our models have all ten fingers and toes is by dropping into `rails console` and testing out `Drink.new`.

```console
 => #<Drink id: nil, name: nil, ingredients: nil, mixologist_id: nil, image: nil, created_at: nil, updated_at: nil>
```
Nice. Now `Mixologist.new`.

```console
 => #<Mixologist id: nil, name: nil, image: nil, created_at: nil, updated_at: nil>
```
Perfect. If your adventure hasn't gone so well, note that you can always `db:rollback` to your heart's content.

#### Seed that data

Navigate to `seeds.rb` and let's throw in some seed data.

```rb
Drink.destroy_all 

    d1 = Drink.create name: 'sangria', ingredients: 'orange, lemon, seasonal fruit, maple syrup, red wine, brandy, ice'
    d2 = Drink.create name: 'moijto', ingredients: 'sugar syrip, lime juice, watermellon, mint leaves, spirit, soda water'
    d3 = Drink.create name: 'negroni', ingredients: 'gin, campari, sweet vermouth'
    d4 = Drink.create name: 'salty dog', ingredients: 'gin, sparking, grapefruit soda, lime juice'
    d5 = Drink.create name: 'Manhattan', ingredients: 'rye whiskey, sweet vermouth, bitters'

puts "#{Drink.count} drinks created"

Mixologist.destroy_all

    m1 = Mixologist.create name: 'yasmin'
    m2 = Mixologist.create name: 'dan'
    m3 = Mixologist.create name: 'bek'
    m4 = Mixologist.create name: 'micaela'

puts "#{Mixologist.count} mixologists created"
```
I've included `puts ("#{Mixologist.count} mixologists created")` and `puts "#{Drink.count} drinks created"` as a little human-readable something something to indicate things have gone well when we `rails db:seed`. I haven't included values for every column here as rails is an intelligent thing and will just fill what we don't specify in with `nil`.

#### Walking the database 

We're not quite done with that seed data yet, we haven't tested out our relationships! It's a good idea to try out all the relationships your app's living, breathing deployed data will have. 

If you've already ran the `db:seed` command fear not, you can run that command as many times as you like. We included the lines `Drink.destroy_all` and `Mixologist.destroy_all` so that if we reseed like the impatient creatures *some* of us are, we won't be duplicating that seed data over and over. 

Let's add some associations to our seed data by throwing the following to the bottom of `seeds.rb`.

```rb
#### Associations

puts "Mixologists and their drinks"

m1.drinks << d1 << d2 << d3 
m2.drinks << d4 << d5 
```
Now when we `rails db:seed` we see:
```console
5 drinks created
4 mixologists created
```
Now `rails db:seed` should give us what we're after. It's sensitive to syntax errors, so you might need to try this a few times between fixing up typos and such.

Let's do a quick sanity check. `rails console`. `m = Mixologist.first`.
```
 Mixologist Load (0.4ms)  SELECT  "mixologists".* FROM "mixologists" ORDER BY "mixologists"."id" ASC LIMIT $1  [["LIMIT", 1]]
=> #<Mixologist:0x00007fe01d112510
 id: 1,
 name: "yasmin",
 image: nil,
 created_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00,
 updated_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00>
```

Looking good. Now `m.drinks`.
```
Drink Load (0.9ms)  SELECT "drinks".* FROM "drinks" WHERE "drinks"."mixologist_id" = $1  [["mixologist_id", 13]]
=> [#<Drink:0x00007fe01a7528b0
  id: 1,
  name: "sangria",
  ingredients: "orange, lemon, seasonal fruit, maple syrup, red wine, brandy, ice",
  mixologist_id: 1,
  image: nil,
  created_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00,
  updated_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00>,
 #<Drink:0x00007fe01a7493a0
  id: 2,
  name: "moijto",
  ingredients: "sugar syrip, lime juice, watermellon, mint leaves, spirit, soda water",
  mixologist_id: 1,
  image: nil,
  created_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00,
  updated_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00>,
 #<Drink:0x00007fe01a749170
  id: 3,
  name: "negroni",
  ingredients: "gin, campari, sweet vermouth",
  mixologist_id: 1,
  image: nil,
  created_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00,
  updated_at: Sun, 30 Oct 2022 07:41:59 UTC +00:00>]
```
Do the same with commands `d = Drink.first` and `d.mixologist` to make sure everything's working fine in both directions. 

#### Get it running

`rails s`, then in your browser, navigate to localhost:3000. Throw /drinks onto the end of that URL and viola!

![drinks json](https://cdn.hashnode.com/res/hashnode/image/upload/v1667118074440/0Q8QPxwjA.png align="left")

Do the same with /mixologists.

![mixologist json](https://cdn.hashnode.com/res/hashnode/image/upload/v1667118216293/k9dhADOGr.png align="left")

Wowy wow, look at that. Go team.

#### Get It Serialized 

Throw the following Gem into your Gemfile, I've put it just before the development section.
```rb
gem 'active_model_serializers', '~> 0.10.13'
```
Run `bundle`, then `rails g serializer mixologist` and `rails g serializer drink`. You'll see a prompt to let you know the appropriate files were generated, thanks Rails.

Navigate to that file and you'll see that the id attribute has been pre-selected. 

```rb
class MixologistSerializer < ActiveModel::Serializer
  attributes :id
end
```
![mixologist JSON containing the ID as the only attribtue](https://cdn.hashnode.com/res/hashnode/image/upload/v1667179828718/zpz2fkM1c.png align="left")

Doesn't exactly make for very interesting JSON. Let's add the attributes we'd like to keep, leaving off those that aren't useful to us. 

In mixologist_serializer.rb include the following.

```rb
class MixologistSerializer < ActiveModel::Serializer
  attributes :id, :name
  has_many :drinks
end
```

Now it's a bit more interesting. 


![mixologist JSON containing id, name, and drinks which contain only the id for the drink](https://cdn.hashnode.com/res/hashnode/image/upload/v1667180001371/Bi6ClHqyj.png align="left")

In drinks_serializer.rb include

```rb
class DrinkSerializer < ActiveModel::Serializer
  attributes :id, :name, :ingredients
end
```
![mixologist JSON containing id, name, and drinks which contain id, name, and ingredients](https://cdn.hashnode.com/res/hashnode/image/upload/v1667180112561/x2ZRoguIP.png align="left")

#### Version It

Perhaps you'd like to version your API so that when you make changes to it, any site relying on your API won't beak under your new configuration. 

In `routes.rb` include the following namespace declarations. 

```rb
Rails.application.routes.draw do

  namespace :api do 
    namespace :v1 do
      resources :mixologists do 
        resources :drinks
      end
    end
  end

end
```

In `app/controllers` create an `api` folder, and within that folder, another folder named `v1`. 
Move your `drinks_controller.rb` and `mixologists_controller.rb` within that new space. Now in `drinks_controller.rb` update the first line to represent our new configuration.

```rb
class Api::V1:DrinksController < ApplicationController
```
Then as you probably guessed, in `mixologists_controller.rb`.

```rb
class Api::V1::MixologistsController < ApplicationController
```

#### CORS

In your `Gemfile` you'll already have this line of code included, it's just a matter of uncommenting it out and running `bundle`.

```rb
# Use Rack CORS for handling Cross-Origin Resource Sharing (CORS), making cross-origin AJAX possible
gem 'rack-cors'
```
Now head over to `cors.rb` in `config/initializers` and uncomment out the relevant file, replacing example.com with something more appropriate. 

```rb
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'localhost:3001'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
``` 

Note: `origins 'localhost:3001'` this line ought to be the URL of the client you'll be making the request from. Otherwise, if you'd like to set it so that anybody can use your API instead, replace `origins 'localhost:3001'` with `*` like so:

```rb
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```
#### Postman

I always like to use postman to play around with the crud operations so if you'd like to do the same download postman for desktop so that it plays nicely with localhost, create a workspace and start making requests.

![postman website displaying JSON for mixologists](https://cdn.hashnode.com/res/hashnode/image/upload/v1667181239403/JA-lxApaF.png align="left")

Next time probably: A react front end.