# Lessons from Code Tests in New Languages

You're interviewing for a place, and they've sent you a take-home code test in a language you've never used before? It's a confusing codebase you're tasked with understanding, debugging, and extending? Wow crazy coincidence I just had one like that. This is what I learned from the experience, maybe it'll help you too. 

#### SLOW DOWN

I get it. This new language looks weird and frightening. You're full of adrenaline, and you've got bills to pay and cat dentists do not relate to your financial troubles, they just think you're a cheapskate. It's super stressful, girl I 100% get it. 

Still though. Code isn't something you can just skim-read and then start solving problems with. If you do that you're going to break stuff and waste time. 

#### Make So Many Comments

Use a quick tour of the language as a reference, something like [learn x in y minutes](https://learnxinyminutes.com/) or similar short-form references. Don't get lost in a blog post youtube binge you'll just be wasting time. 


Lots. Of. Comments. Unnecessary ones, even. Explain stuff you already understand. This function intakes this, then it does this with it. Then this. Then that. It outputs this. That output looks like this. On and on like that. The thing is you can hold all that in your head just fine until you're at line 40, your mind goes blank, and then you have to jump back 5 or 10 paces to resituate yourself. Treat yourself like an idiot. This is what it is to really get situated with a codebase. 

Again don't deep dive into the language on youtube or in unrelated blog posts unless you're majorly stuck. That happens sometimes, and if you're truly not making progress go watch the youtube video or what-have-you until you feel confident enough to get back to it, you might need a non-code-related break too. Go outside and eat something. Otherwise, you already have the code you're trying to understand, so take that code and just go through it slowly. I'm repeating myself a lot here because it's so tempting not to do the obvious thing.

Just do it though.

#### Ok, Now Delete Some

You're situated, let's not stay absolutely drowning in notes. What you keep will depend on your situation, but it's always nice to be able to visualise the output of things. I'm biased, though I was dealing with JSON, which is especially nice to be able to visualise.

#### Commit Often 

When you've made any amount of meaningful progress, commit your work. Make the commit messages meaningful, you want to show the kind of coworker you're going to be when you land the role. Write the commit messages in such a way that someone skimming over them doesn't need to ask you questions about your process because they've already *read* it. 

#### Now Pull It Apart 

It's scary to touch someone else's code, especially in an extensive code base. You're going to have to push past that tentativeness in order to get anything meaningful done. If you put everything back just how you found it when you don't get your expected results on the first try, you're probably not going to get very far. Only `git push` your changes when you have things in a working state, but feel free to `commit` when you're making progress. If you're in for a long-haul project, git branch is something you're going to want to get comfortable with. 

#### P.S If It's Live COMMUNICATE 

If you're pair programming or doing a code test live, communicate **everything**.  You should be walking them through your thought process. It's better to be wrong out loud than to push on in dead silence, they want you to succeed and might be allowed to give you hints in the right direction. 

#### Even If It Isn't Live COMMUNICATE

Comments help other people understand your code. Don't neglect explaining things to the people who will end up reading your code. If you run out of time, pseudo-code what you would do next to let the other person know that you had a game plan. If you can't get the code working how you want, pseudo code what you're trying to do. You could be on the right track, and you'll be able to show that if you've written it out. Worst case, you've shown that you're prioritising communication. 

#### You're Learning, Feel Good About It

If you land the job woo-hoo. If you don't, you're still skilling up. It's better to fail than to not try. Try and try again. Programming is hard. It's hard all the way up. Practising working through problems is good training, the more calm and focused you can be on the code in front of you, the better. Even with an absolute zen state, you're going to have to spend time sitting with the problem. Put in the hours and make them worth it by giving them your undivided attention, then take a break and do other things. 

Good luck and goodbye. 