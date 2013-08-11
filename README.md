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

## Why Git?
Git is what's called a 'distributed' version control system. It means there is no one master copy of the repository. Instead, everyone who is working on the project has a complete copy of the repository. All the collaborators simply choose one to consistently push their changes to. This means that even if the server that you keep your repo on blows up, every person working on it will still have a functioning copy. This is not the case with other VCS, like Subversion. This also lets git also have very cheap branching - a concept we'll cover soon. Just know that branching will change how you code, and how you think about working on projects. 

And really, it's what everyone is using right now. Subversion has a foothold in a lot of businesses, but a lot of companies are switching over to git as we speak. Not to mention, these days your Github page + LinkedIn profile is basically you're resume for Computer Science jobs. If you're not using Github (or at least working on a lot of side projects that you can give links to), you're going to have a hard time getting a job at a top tech company. They want to see passion, and using git and Github shows that you've got passion for what you do. 
