# Project 1 - Day 0

Day 0 - Planning Begins. I've been handed the brief this afternoon, and gotten the ok for my second idea after the first one was deemed too complicated. Shelving that one for Project 3 or 4 down the track. 

The concept, a communal story that one person begins, and another continues. Basically it's just [exquisite corpse](https://en.wikipedia.org/wiki/Exquisite_corpse)

The MVP
 
![Screen Shot 2022-07-21 at 10.07.21 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658405253016/GqS1XKYKl.png align="left")


The most basic execution of this idea that I would be happy to add my name to involves at least a person submitting text and another person being able to add their text then. Thus, a story can exist. It's tempting to start thinking about what has_many and such, but I'm trying to avoid considering that until my idea is fleshed out a bit more. 


![Screen Shot 2022-07-21 at 10.15.30 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658405744216/3UWybcujs.png align="left")

A level more complex. Users! They exist and then continue to exist. Thus a login, username, password, and all that jazz are necessary. Maybe even more than one big story exists, with different genres or prompts. This could be as simple as the OP entering text into a field that gets tagged to the post. "Hey, guys this one is just rhymes" or "The last word every submission has to be banana". 


![Screen Shot 2022-07-21 at 10.19.32 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658406017272/87OxEcWhV.png align="left")

A far-reaching goal I might want to consider in my dreams is predictive text ai. Maybe a cute little button you can press with an icon of a robot that reads the story so far and spits something out based on our story. Maybe you can trash its suggestion and press it again for more! 

This would be especially nice for an impatient user that wants to continue the story but not all by themselves. 

![Screen Shot 2022-07-21 at 10.23.58 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658406247162/OiPvpqLnq.png align="left")

So how should I go about planning this crazy thing? I'm thinking it's best to focus on the experience I'd like a user to have. What does that look like? Then once I have a solid idea about what the goal is there, I should consider what data I need to create and maintain that experience. What are the relationships between the necessary kinds of data? 


![Screen Shot 2022-07-21 at 10.27.01 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658406436768/xawGeO1Xt.png align="left")

My next step then is to make some wireframes. What does the MVP look like? What does a step up look like? Then map out what goes under the hood. After that, think about how the 'insides' impact the 'outsides' again.


![Screen Shot 2022-07-21 at 10.30.51 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658406674385/fhXkW1_Ky.png align="left")

The bare bones version would only really need a way to display text, enter text, and add text. You type something in, it's sent into the story. I might want to put a limit on how many characters can be added, tweet size at most seems good. 

I'm also starting to consider what the different outcomes could be. What's the happy user experience vs the unhappy one. It would be terrible to type something in, feel good about it. Only to have your self-satisfied smile be wiped off your face when your pithy one-liner is disappeared instead of being displayed for everyone to agree on how great it is. What the heck! Now you have to type it all out again if you can even remember how it goes exactly, or be faced with a world devoid of your shining intellect.

No thanks. Happy path, please. I type in my funny thing, I press done. Off it goes, not into the void but into the story. The world is a tiny bit better now that the story has a hot vampire in it. 


![Screen Shot 2022-07-21 at 10.38.43 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658407140351/HpcR7pXbf.png align="left")

Alright, that's fun. What about our writers. Do I want them to have credit for their work? Maybe, maybe not. I don't want people to be competitive or self-conscious. It would be nice to get some indication of how many people are participating though. It would also be good to have a way to clear the text input quickly in case you've realised you don't like your idea, then another button to send it off. They would have to be very different looking so that a user wouldn't be confused and face the terrible problem I described in my unhappy path. 



