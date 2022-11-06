# Git Troubleshooting - Permission Denied (publickey)

#### Step 1 - Sulk about it a bit
Why me, this is so crap. It was working earlier. Why would it not *stay* working. I don't deserve this and have never done a wrong thing in my life. Why must terrible things happen to good people?

#### Step 2 - Chill out, we're going to fix it
Take a deep breath babes. It's all good.

#### Step 3 - Generate a new key
In terminal paste the following commands, but make sure you edit your Github email to sit nicely between those quotes. `ssh-keygen -t ed25519 -C "your-email-here@email.com"`. You should get back a heap of info that starts with `Generating public` and ends with `The key's randomart image is:` followed by said `random image`. Generative art as a form of security? Neat.

#### Step 4 - Copy the key

In the information returned from the previous command, you need to look for the line that looks like this `Your public key has been saved in /your/file/path/here`. Grab the file path and run the following command `pbcopy < /your/file/path/here`.

#### Step 5 - Give it to Github

Navigate to GitHub and find settings. 


![Screen Shot 2022-09-12 at 5.01.13 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662966084012/5cpIQ5Nan.png align="left")

Then navigate to SHH and GPG keys.

![Screen Shot 2022-09-12 at 5.02.05 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662966192832/rFCJmzjcB.png align="left")

Click the new SSH key button on the top right.

![Screen Shot 2022-09-12 at 5.05.15 pm.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662966327625/HAsgRSMfk.png align="left")

Add a title that's meaningful to you, I used 'Personal Laptop' and paste in the key you copied via the `pbcopy` command, add the key and you're set. 

If this didn't work out for you, damn. Good luck with that. Everyone else, you're welcome. 