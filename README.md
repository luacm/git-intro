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

Now that we have that file, type ```git status``` again. Now it will tell you that you have an _untracked_ file called 'uncleben.txt'. An _untracked_ file is a file that is not currently being versioned by git. As far as git is concerned, this file doesn't really exist. We can tell git to start tracking it by typing ```git add uncleben.txt```. Type ```git status``` again, and you see that git recognizes that you have a new file 'uncleben.txt', and it is ready to be _commited_. 

## Committing files
A git _commit_ is one of those snapshots we were talking about earlier. It's the current state of your project at a point in time. We can see our list of commits by typing ```git log```. If you do that now, you'll get an error - because we haven't made any commits yet! So let's make one. Type the following command: 

```git commit -m "Initial commit."```

We've just made a commit! We also gave the commit a _message_ of "Initial commit." Giving a commit a message is mandatory.  The ```-m``` tells git that we're going to give git the message right now. If we didn't put ```-m``` following by the message, git would open up your default text editor and force you to give a message. There's a lot to say on the subject of how to write a good commit message, but for now just use this ```-m``` syntax and keep your messages to be one sentence or less. 
