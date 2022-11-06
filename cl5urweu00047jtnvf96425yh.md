# CRUD On Rails - Users, Security, Many to Many Relationships, and More!

This ain't for kids anymore. Direct your children [this](https://yasmina95.hashnode.dev/ror-beginners-guide-crud-getting-started) way or [that](https://yasmina95.hashnode.dev/beginners-crud-on-rails-lazy-edition) way. Everybody else, let's go. 

First off, we're not using sqlite3 anymore, ew what are you, a baby? No. All the babies have left. You're an adult. Adults want to *deploy* their projects. What do we need to deploy our projects, I hear you ask? [Postgres](https://postgresapp.com/downloads.html) fool.

Say you want to make a site that allows users to make playlists, please. Oh good, that's what you wanted to make? Phew, I didn't want to come up with another example. 

So here's the thing, an Artist `has_many` songs, and a `song belongs_to` one Artist. In this universe, it's canon that collaborations never happen, ok? A song, however, also `beongs_to` one album. That album `has_many` songs. The Album  `belongs_to` an Artist, the Artist `has_many` albums. 

A user `has_many` mixtapes, and mixtapes `belong_to` that single user. No collabs here either, this is you and your laptop not Spotify. In that relationship for example, the mixtape would have the foreign key. The owner of the thing does not have the foreign key. The thing which `belongs_to`, does. However, in an annoying complication, the mixtape also `has_many` songs. That makes it a HABT relationship. Has and belongs to many. There's a polyamory joke in there somewhere but we don't have time for that. 

Back to our new elephant friend. Terminal command `rails new radio --skip-git -d postgresql`. Omit skip git if needed. `cd radio` `rails db:create`. `rails db` will now drop you into Postgres if that's what you've got running.  Also you might notice you can't see your database in the db folder anymore, but an elephant never forgets so it's fine. Don't worry about it. 

If you were a fan of the .schema command in sqlite3, grow up. We're using `\d` now.  CTR D outta there anyway, we don't even have any models yet. 

Now `rails generate model Song title:text album_id:integer artist_id:integer`. Woah look at you go, generating the model *and* the migration. Unless you stuffed it up, check your migrations folder. Mine looked like this.

```
class CreateSongs < ActiveRecord::Migration[5.2]
  def change
    create_table :songs do |t|
      t.text :title
      t.integer :album_id
      t.integer :artist_id

      t.timestamps
    end
  end
end
```
It's got a foreign key and everything! Aw yis. `rails db:migrate`. Let's do a sanity check and `rails db` then `\d`. You should see the songs table. `Rails console` and `Song.new` to be sure it's got all ten fingers and toes. A healthy baby song, nice. 

`rails generate model Artist name:text image:text`, check the migration folder, and onto `rails generate model Album title:text image:text`. `rails generate model Mixtape title:text user_id:integer` then `rails:db migrate`. Look at all those models, you busy thing, you. 

Ready for the big one? `rails generate model User email:text`. Because rails made our models for us, they're connected to ActiveRecord::Base via application_record in our models folder. That's fine though, since we're all inheriting from it, and it's inheriting from ActiveRecord::Base. It looks like this.
```
class ApplicationRecord < ActiveRecord::Base
  self.abstract_class = true
end
```

Let's go and make those connections. In song.rb. You'll notice it inheriting from ApplicationRecord.
```
class Song < ApplicationRecord
    belongs_to :artist, :optional => true
    belongs_to :album, :optional => true
    has_and_belongs_to_many :mixtapes
    has_and_belongs_to_many :genres
end
```
There's a lot going on there, huh? Artists are a bit like that. 
```
class Album < ApplicationRecord
    has_many :songs
end
```
```
class Artist < ApplicationRecord
    has_many :songs 
    has_many :genres, :through => :songs
end
```
```
class Genre < ApplicationRecord
    has_and_belongs_to_many :songs
end
```
```
class Mixtape < ApplicationRecord
    belongs_to :user, :optional => true
    has_and_belongs_to_many :songs
end
```

Now this one's extra fancy. Feast your eyes on User!
```
class User < ApplicationRecord
    has_secure_password
    validates :email, :uniqueness => true, :presence => true
    has_many :mixtapes 
end
```
In the user model I've tackled a few problems that could have been handled elsewhere. Where possible, it's best to fatten up your model and thin out your controller. Basically Thomas the tank engine rules in reverse. The model for example, should be in charge of what is and isn't a valid user. Why? [Because Rails](https://guides.rubyonrails.org/active_record_validations.html), that's why. Rails will take care of the validations for us with very little coding on our part. So let rails be rails, and change the user.rb. User `has_secure_password` and `validates :email, :uniqueness => true, :presence => true`, ok?! 

Want to see its controller? 

```
class UsersController < ApplicationController
  def new
    @user = User.new
  end
  def create
    @user = User.new user_params
    if @user.save
      session[:user_id] = @user.id
      redirect_to root_path
    else
      render :new
    end
  end
  private
  def user_params
    params.require(:user).permit(:email, :password, :password_confirmation)
  end
end
```

Busy busy. Let's break her down a bit. 

User.save is a predicate method, meaning it'll either be true or false. You can see that in action if you make an invalid user in pry (or irb). Using it and User.new rather than User.create means that we can make a decision based on whether or not a new user was created correctly. We do that by saving it in an instance variable and then using an if else statement to determine what to do next. 

```
 def create
    @user = User.new user_params
    if @user.save
      session[:user_id] = @user.id
      redirect_to root_path
    else
      render :new
    end
  end
```
In this case, we redirect_to root_path. By using render :new in our else case, we give the user the chance to correct their mistake while giving them a better idea of what went wrong by retaining the parts of the form they filled correctly. Rails, as always, has some great tricks up her sleeve in this department too. If you go and inspect element on your poorly filled out form. Oh fine I suppose I'll show you the form first. Behold, our users/new.html.erb. 

```
<h1>Sign up</h1>

<% if @user.errors.any? %>

    <ol>
        <% @user.errors.full_messages.each do |msg| %>
            <li> <%= msg %> </li>
        <% end %>
    </ol>
<% end %>

<%= form_for @user do |f| %>
    <%= f.label :email %>
    <%= f.email_field :email %>
    <%= f.label :password %>
    <%= f.password_field :password %>
    <%= f.label :password_confirmation %>
    <%= f.password_field :password_confirmation %>
    <%= f.submit "Sign Up!" %>
<% end %> 
```
Anyway, as I was saying, when you inspect element on our form, you'll see a div ruby made for us with the class of 'field_with_errors'. Feel free to add some css to make it more obvious to a user what's gone wrong here. 

Another neat trick that gets passed from programmer to programmer is the following.

```
class ApplicationController < ActionController::Base
    before_action :fetch_user

    def fetch_user
        @current_user = User.find_by :id => session[:user_id] if session[:user_id].present?
        session[:user_id] = nil unless @current_user.present? 
    end
end
```
This bad boy logs out non-existent users, which can end up being created in the development process if you reseed while a user is logged in, thus creating a horrible bug. Let's just copy-paste it into every project forever and ever, *as a community*. 

This has been baby's teaching babies to code. 

I mean, cool adults who know what they're doing. 

Goodnight. 