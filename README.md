# Introduction to Git
Git is one of today's most popular [version control systems](http://en.wikipedia.org/wiki/Version_control). It's picking up a lot of speed, and knowing git is basically a necessity at this point if you want to work as a developer.

## What is version control?
Before we can talk about git, we have to first go over the concept of what version control actually is. Have you ever been in any of the following situations?
* You just screwed up something on your project, and wished you could go back to a previous version.
* You have a working project, but discovered you have to make a big change to the code base in order to implement a new feature. Now you're worried that if you try to make the change you'll never be able to get back to your current working state if you screw it up.
* You're working with someone else on a project, and the 'put the code in Dropbox' method just isn't working out as well as you hoped.

If you're like me, you avoided some of these problems by periodically copying your entire project and putting these copies in another folder. Or maybe you just relied on Dropbox's built-in versioning to make backups of your work. But this just isn't an ideal solution, and it doesn't solve the problem of how to work collaboratively on a programming project.

That's where a version control system (VCS) comes in. It's a system that fixes all of the above problems and then some. The basic concept of version control is simple: it's a system to take snapshots of your work, and be able to move between snapshots at any point. You can then save these snapshots in a remote location to act as a backup, and share and merge these snapshots together with others as a way to work collaboratively.

We store these snapshots in something called a 'repository,' or 'repo' for short. And these snapshots are usually referred to as 'commits.' 

There are a bunch of version control systems (like Subversion, Mercurial, and Bazaar), but Git is pretty much the best.

## Why git?
Git is what's called a 'distributed' version control system. It means there is no one master copy of the repository. Instead, everyone who is working on the project has a complete copy of the repository. All the collaborators simply choose one to consistently push their changes to. This means that even if the server that you keep your repo on blows up, every person working on it will still have a functioning copy. This is not the case with other VCS, like Subversion. This also lets git also have very cheap branching - a concept we'll cover soon. Just know that branching will change how you code, and how you think about working on projects.

And really, it's what everyone is using right now. Subversion has a foothold in a lot of businesses, but a lot of companies are switching over to git as we speak. Not to mention, these days your Github page + LinkedIn profile is basically you're resume for Computer Science jobs. If you're not using Github (or at least working on a lot of side projects that you can give links to), you're going to have a hard time getting a job at a top tech company. They want to see passion, and using git and Github shows that you've got passion for what you do. 

# Let's Get Started!
Time to do some actual work! We're going to be using git exclusively through the terminal (command prompt on Windows). There are GUI tools out there that will help you out, and while they're great for some things, they abstract away git too much to the point where it will be difficult to understand what's going on. They also don't have a lot of the advanced git commands that you will most likely find yourself using semi-regularly.

Don't worry, to be safe, this guide is written in a way that assumes little to no terminal experience. As long as you understand the idea of files and directories, you should be good.

## Installing git
If you're using Mac OS or a flavor of Linux, then git is likely already installed on your system. However if it's not, or if you're running Windows, go [here](http://git-scm.com/downloads). They give you pretty good instructions.

## Making a repository
Open up terminal, and navigate to a directory where you want to keep your projects. A good place may be ```~/dev``` on Mac/Linux or ```C:/dev``` on Windows. From here, run the command ```git init spiderman```. This will create an empty git repository called 'spiderman'. Git puts this in a folder called 'spiderman' for you. Navigate into this directory by typing ```cd spiderman```. Congratulations, you are now in a git repository!

## Adding files
Here's your first git command: ```git status```. Type that, and git will tell you what the status of your repository is. Right now, it'll tell you that you have nothing to commit. That's because there's nothing in there yet! Let's fix that. We'll make a file called 'uncleben.txt' that has the contents 'With great power comes great responsibility.' You can do that with your text editor of choice, or you can type the following: 

```echo "With great power comes great responsibility." > uncleben.txt```

Now that we have that file, type ```git status``` again. Now it will tell you that you have an **untracked** file called 'uncleben.txt'. An untracked file is a file that is not currently being versioned by git. As far as git is concerned, this file doesn't really exist. We can tell git to start tracking it by typing ```git add uncleben.txt```. Type ```git status``` again, and you see that git recognizes that you have a new file 'uncleben.txt', and it is ready to be **commited**. 

## Committing files
A git _commit_ is one of those snapshots we were talking about earlier. It's the current state of your project at a point in time. We can see our list of commits by typing ```git log```. If you do that now, you'll get an error - because we haven't made any commits yet! So let's make one. Type the following command: 

```git commit -m "Initial commit."```

We've just made a commit! We also gave the commit a **message** of "Initial commit." Giving a commit a message is mandatory.  The ```-m``` tells git that we're going to give git the message right now. If we didn't put ```-m``` following by the message, git would open up your default text editor and force you to give a message. There's a lot to say on the subject of how to write a good commit message, but for now just use this ```-m``` syntax and keep your messages to be one sentence or less. 

If you type the command ```git log``` you can see that it is now in our log history. Success!

## Changing files
Now that we have a file being tracked by git, we can make some changes. Let's change uncleben.txt to say: "With great power there must also come -- great responsibility!" (which is how the quote originally appeared). You can do this in your editor of choice, or you can type:

```echo 'With great power there must also come -- great responsibility!' > uncleben.txt``` 

(Note that we had to use single quotes, othewise the terminal wouldn't allow us to use an exclamation point.) Now that we've made a change, type ```git status```. Git tells us that we've modified uncleben.txt, and that this is 'not staged for commit', or **unstaged**. If a change is **unstaged** then it will not be captured in our snapshot when we type ```git commit```. In order to have it captured in our snapshot, we must first **stage** it by using the ```gti add``` command. Type the following:

```git add uncleben.txt```

Not type ```git status``` again. Git will now say that this is a 'change to be committed' or **staged**. Now we can type the following: 

```git commit -m "Fixed the quote to be the original occurance."```

Type ```git log``` and see that we now have two commits in our history!

### Emphasis on terminology
Let's take a brief detour and put some emphasis on the terms we just learned. Specifically: **tracked**, **untracked**, **staged**, and **unstaged**. 

**tracked** and **untracked** refer to whether or not the file is actually in the repository. Just because the file is in the folder doesn't mean git is watching it. In fact, there are some instances where we don't want git to track certain files (we'll look at that in another lesson). To track a file, we have to use ```git add``` to start tracking it.

**staged** and **unstaged** refer to changes to files that are already being tracked by git. If a change isn't staged, it won't be added to the next commit. Conversely, if it is staged, then it will be added to the next commit. 

It's important to keep this stuff in mind, because it's not uncommon to be confused with git early on. Knowing and understanding these terms is really important, and will really help if you run into issues.

## Building up a history
Before we do any other work, let's give ourselves some more files and commits to play around with. First, let's make a file called 'spidey.txt' and give it the content of:
```
                  ,,,, 
             ,;) .';;;;',
 ;;,,_,-.-.,;;'_,|I\;;;/),,_
  `';;/:|:);{ ;;;|| \;/ /;;;\__
      L;/-';/ \;;\',/;\/;;;.') \
      .:`''` - \;;'.__/;;;/  . _'-._ 
    .'/   \     \;;;;;;/.'_7:.  '). \_
  .''/     | '._ );}{;//.'    '-:  '.,L
.'. /       \  ( |;;;/_/         \._./;\   _,
 . /        |\ ( /;;/_/             ';;;\,;;_,
. /         )__(/;;/_/                (;;'''''
 /        _;:':;;;;:';-._             );
/        /   \  `'`   --.'-._         \/
       .'     '.  ,'         '-,
      /    /   r--,..__       '.\
    .'    '  .'        '--._     ]
    (     :.(;>        _ .' '- ;/
    |      /:;(    ,_.';(   __.'
     '- -'"|;:/    (;;;;-'--'
           |;/      ;;(
           ''      /;;|
                   \;;|
                    \/
```
Cute, huh? We can make another one called 'swing.txt' with the content of:
```
               :                
               ;                
              :                 
              ;                 
             /                  
           o/                   
         ._/\___,                
             \                  
             /                   
             `      
```

Perfect. Now you can add thses to your repository using the command ```git add -A```. The ```-A``` adds tracks all untracked files and stages all unstaged changes. You could also add them individually by doing:

```
git add spidey.txt
git add swing.txt
```

Your choice! Now let's commit these by typing ```git commit -m "Added some sweet ASCII art."```

## Going back in time
Let's say that we don't like this new Uncle Ben quote after it. It may be the original, but hey, the movie quote just sounds better. There are a couple of ways to go about getting different versions of files in git, so we'll go through a couple. Let's start by using the ```git checkout``` command. 

Remember how when you type ```git log```, you see this really long string of letters and numbers next to the word 'commit'? That's called a SHA1 tag (usually pronounced shah-won). It's the unique identifier for the commit. If we want to get a version of a file at a specific commit, we need that identifier. So, copy the SHA1 tag of the initial commit. Now type the following:

```git checkout ab2bacee5cad uncleben.txt``` (or whatever your SHA1 tag is)

You'll see that uncleben.txt now has the contents of 'With great power comes great responsibility.' Cool, huh? Now if you do a ```git status``` you'll see that the change has already been staged for you. You could make a commit and put that file back at the state you wanted it.

But maybe this isn't what you wanted. Maybe you didn't want to get an old version of the file, but an old version of your entire project. You could reset your whole project back to an earlier state by using the ```git reset --hard``` command. If you wanted to go back to your initial commit, you could type: 

```git reset --hard ab2bacee5cad``` (or whatever your SHA1 tag is)

Go ahead and do that now. Then type ```ls``` to see that your new files are gone, and type ```git log``` to see that your commit history has been reset to be as if you were at your initial commit again. But what happens if we didn't want to do that? Where did your files go? What about your commit history? How can you get back to the state you were just at? Have you just lost all of your work?!

### The magic of reflog
Calm down, your history is still there! There's this magic little command that git has that most people actually don't know about. It's called ```git reflog```. Type that now.

You'll see a list of actions you have performed, and that list includes the normal things like commits, but also things like resets. And you can see here that git still has a history of your commits, even if they don't appear in the ```git log```. So fear not, you should see an entry for a commit with the message of 'Added some sweet ASCII art.' Grab either the SHA1 for that line and type:

```git reset --hard 31320af``` (or whatever your SHA1 tag is)





