# Intro to RSpec and Test Driven Development - What is it, Why is it?

Test-driven development (TDD) is the thing that'll save you from having to go through troves of code, some of which you most likely didn't write to find the bug. Sometimes you, or more likely your stupid coworker Bret, write some code that bleeps up code that was working perfectly fine before Bret got his stupid cheeto-dust-covered fingers all over it. 

#### Ok, but how?

There are lots of ways to go about this, and people tend to vary greatly in preferences, but the basic process is:

* Make a test that fails
* Write code until it passes 
* Refactor that code 
* Move on

My first introduction to a testing suite was using RSpec for ruby test-driven development, which is what I'm going to walk you through today. 

RSpec is a domain-specific language like ActiveRecord or Sinatra. A domain-specific language has a higher level of abstraction for whatever unique problems it's trying to make more human-brain friendly. Basically, it uses human words to describe things. Here's an example. 
```
describe User do
      describe '.new'
      user = User.new
      expect(user).to_not be nil 
    end

end
```
Notice the familiar words describe and expect. How nice, human talk. 

This part could have been written a number of ways, so feel free to change it depending on what made the most sense in your case. Maybe you'd prefer to have something that's more along the lines of expecting user to be an instance of the user class. 

The basics of RSpec are: 
- `describe` you write what it is
- `do` then what it's *supposed* to do.

Anyway, let's get into it to get some practice. Good test-driven development is something you have to spend your career keeping sharp at, so best get hour one of those 10 000 hours on with already.

#### Code along 

In terminal `gem install rspec` then in the directory you're working in `rspec --init`. The result of that is the birth of a new spec directory with a spec_helper.rb file to boot. Mine came with 98 lines of code and a heap of comments. 

I'm going to make an additional `rspec` file because I love files. `user_spec.rb`. At the top of this file, I require the following. 
```rb
require_relative '../user'
```
This is how you require your own files, the `../` is similar to the terminal command `cd ..`, in that they both bring you up a level.

Create a `user.rb` file at the root of your directory. Then as my first test. 

```rb
require_relative '../user'

describe User do
    describe '.new' do
        user = User.new
        expect(user).to_not be nil
    end
end
```
The way we run the test is by typing `rspec` command in terminal. RSpec has default formatting, but if you'd like you can configure it to suit your preferences. I like `rspec spec --format documentation`. If you find you do too, you can configure it on a more permanent basis by adding it to your `.bash_profile`.

Anyway, now you've written a test, back to the command line you little scamp. You've got to *run* the test. `rspec`. Easy as that. Look at all that red. The important bit here is.

```
NameError:
  uninitialized constant User
# ./spec/user_spec.rb:3:in `<top (required)>'
No examples found.
```
You've made a test and failed it, good job. That's the workflow, make a test, fail, fix it, test it, new test, new failure, lunch break. 

Because we're practising error-driven development (EDD) alongside TDD we've written a test that fails intentionally. This can be a way of creating a workflow for yourself that keeps things chugging along nicely. When you keep the tests simple, you're setting up your workflow in such a way that you can build things up by incremental chunks. The more experienced you are, the more steps you'll skip as they've become second nature at that point, but as a beginner dev, it might be nice to keep things simple. 

Before we pop off for lunch, let's fix our error with the following code in user.rb.

```rb
class User
end
```
Run the test again for funsies and see what happens.
```
Failure/Error: expect(user).to_not be nil
  `expect` is not available on an example group (e.g. a `describe` or `context` block). It is only available from within individual examples (e.g. `it` blocks) or from constructs that run in the scope of an example (e.g. `before`, `let`, etc).
# ./spec/user_spec.rb:6:in `block (2 levels) in <top (required)>'
# ./spec/user_spec.rb:4:in `block in <top (required)>'
# ./spec/user_spec.rb:3:in `<top (required)>'
No examples found.
```
A new error. Fun fun.

Let's go throw some more code in the mix of our user spec file.

In a somewhat creepier turn, we add the following:
```rb
describe User do
        describe '.new' do
            it 'creates a new user object' do
            user = User.new
            expect(user).to_not be nil
        end
    end
end
```
It creates a new user object, or else it gets the hose again. Run `rspec` in terminal and peep the following. 
```
1 example, 0 failures
```
Wowy wow look at us go. In the green.

Wait no, we hate green. Errors are good. I don't feel driven without errors. Let's fix that by breaking something. 

Let's write a test that assumes our user is Bret. It'll be more fun to delete this file when we're through with practising that way. 

```rb
require_relative '../user'

describe User do
        describe '.new' do
            it 'creates a new user object' do
            user = User.new
            expect(user).to_not be nil
        end
        it 'assigns the user a name' do
            user = User.new 'Bret'
            expect(user.name).to eq 'Bret'
        end
    end
end
```
Ah good. A failure.  
```
2 examples, 1 failure

Failed examples:

rspec ./spec/user_spec.rb:9 # User.new assigns the user a name
```
Now let's add the relevant code to our   `user.rb` file. 

```rb
class User
    def initialize(n)
        @name = n
    end
    
    def name 
        @name
    end
end
```
Run spec again, and... oh. 
```
2 examples, 1 failure

Failed examples:

rspec ./spec/user_spec.rb:5 # User.new creates a new user object
```
Another error. That's because we've changed our minds about how a user is defined and therefore broken our initial test. Let's go change that code to match our new expectations. 

```rb
describe User do
        describe '.new' do
            it 'creates a new user object' do
            user = User.new 'Bret'
            expect(user).to_not be nil
        end
        it 'assigns the user a name' do
            user = User.new 'Bret'
            expect(user.name).to eq 'Bret'
        end
    end
end
```

Now we get the following by running RSpec. 
```
2 examples, 0 failures
```
Noice. 

And that's intro to RSpec. Next time, Jest probably. 