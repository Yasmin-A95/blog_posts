# Project 1 - Day 2 - MVP Launch

Spoiler: the big lesson here is that programming isn't a solo adventure! Get other people to interact with your project as early as possible. Talk to other programmers and seek the advice of people who have been doing this a lot longer than you.

Heroku, why won't you work? Please. None of the tutorials are up to date, your breakup with github could not have been worsely timed. Did you even consider how that might affect *me?* Don't answer that. I don't even want to hear it. Life is bad. 

Wait, maybe life is good. After relentlessly nagging the person who was formerly the only programmer I knew, I was informed I should use ngrok to use my laptop as the server. `brew install ngrok`, `ngrok http 3000` to the rescue. Nobody can see the page except for me, and I checked it in an incognito browser to attempt to simulate it from another person's perspective. Maybe that isn't how that works. Hmm. ngrok is just as toxic as heroku. Can't trust anybody these days. In sending the link to people, I'm realising that I'm explaining to them how to use the site and what the 'game' is all about. Even though the link didn't work, in the act of attempting to show it to other humans my empathy for a user is expanded. There are so many things I didn't consider when It was just me on my lonesome. Next on the to-do list is to add some more explanatory bits to my site. A user should know that they're not starting a new story but instead contributing to the big Frankenstein story, we're all making together. 

Oops. It turns out I can't send them the full link https included. Only f575-2001-8004-1d51-64c5-785b-8bd0-edff-a13c.au.ngrok.io/ on it's own will work. Strange, but ok. Now my friends can use my site! Happy days. 


![Screen Shot 2022-07-23 at 8.53.21 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658575184560/xZ-wms-fD.png align="left")

Feedback: my instincts were right, it's not immediately obvious what the point of the site is. I think my placeholder doesn't help in that department either. Also, when several people are using the site at once, they can't see a live update, and so the flow of the story becomes chaotic and mish-mashed as people talk over one another. I need to find a way to live update every time the database changes.

Luckily seeing my friends use the site, and reading all their cute messages has given me enough delicious serotonin to enjoy reading documentation. 

After another launch and a failed attempt at a solution, it's time for some more documentation deep diving. Reading [this](https://apidock.com/rails/ActiveRecord/Callbacks/after_update) I think I may have to restructure my data so that a user, rather than creating a new story, is adding a bit to the existing story. My site in its current form really is just displaying one big post. It's just that according to my current data structure, that one big post is made up of many stories. 

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

This has me wondering about the journey the user input has to go through in order to make it to the database. 
![Screen Shot 2022-07-23 at 9.35.30 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658576150109/axf6s00oU.png align="left")
According to my understanding of the model, the user input has to travel from my form (see below) in the views index.html.erb all the way back to the controller who talks to the model who talks to the database. It's got to walk all the way along the structure before it's stored. 
``` 
<section class="story-area" id="text-input">
        <%= form_for @story do |f| %>

          <%= f.label "Your turn" %>
          <%= f.text_area :bit, :placeholder => "Once upon a time, blah blah blah", class: 'text-field'   %> <%# , :maxlength => 250? %>
          <%= f.submit class: "submit-button" %>
      
        <% end %>
        
      </section>
```

After taking some notes to gather my thoughts, I'm resigning myself to asking for help. Thankfully, my friend earned her title of *formerly* the only other programmer I know by introducing me to a few more (sorry classmates, we don't count yet). I sought advice and had my understanding confirmed apparently frameworks like react phoenix reload automatically, and rails is the exception to the rule. The data really does have to jump through all those hoops in order to get to the database which is why it's considered slower than the alternatives. 

I'm sad about losing the cute messages people wrote while they were helping me test my site, but alas I'm going to start tomorrow by gutting my database. 