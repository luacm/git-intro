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

# Let's 'Git' Started!
Time to do some actual work! We're going to be using git exclusively through the terminal (command prompt on Windows). There are GUI tools out there that will help you out, and while they're great for some things, they abstract away git too much to the point where it will be difficult to understand what's going on. They also don't have a lot of the advanced git commands that you will most likely find yourself using semi-regularly.

Don't worry, to be safe, this guide is written in a way that assumes little to no terminal experience. As long as you understand the idea of files and directories, you should be good.

## Installing git
If you're using Mac OS or a flavor of Linux, then git is likely already installed on your system. However if it's not, or if you're running Windows, go [here](http://git-scm.com/downloads). They give you pretty good instructions.

## Making a repository
Open up terminal, and navigate to a directory where you want to keep your projects. A good place may be ```~/dev``` on Mac/Linux or ```C:/dev``` on Windows. From here, run the command ```git init titans```. This will create an empty git repository called ‘titans’. Git puts this in a folder called ‘titans’ for you. Navigate into this directory by typing ```cd titans```. Congratulations, you are now in a git repository!

## Adding files
Here's your first git command: ```git status```. Type that, and git will tell you what the status of your repository is. Right now, it'll tell you that you have nothing to commit. That's because there's nothing in there yet! Let's fix that. We'll make a file called ‘armin.txt' that has the contents "On that day, mankind received a grim reminder." You can do that with your text editor of choice, or you can type the following: 

```echo "On that day, mankind received a grim reminder." > armin.txt```

Now that we have that file, type ```git status``` again. Now it will tell you that you have an **untracked** file called ‘armin.txt'. An untracked file is a file that is not currently being versioned by git. As far as git is concerned, this file doesn't really exist. We can tell git to start tracking it by typing ```git add armin.txt```. Type ```git status``` again, and you see that git recognizes that you have a new file ‘armin.txt', and it is ready to be **commited**. 

## Committing files
A git _commit_ is one of those snapshots we were talking about earlier. It's the current state of your project at a point in time. We can see our list of commits by typing ```git log```. If you do that now, you'll get an error - because we haven't made any commits yet! So let's make one. Type the following command: 

```git commit -m "Initial commit."```

We've just made a commit! We also gave the commit a **message** of "Initial commit." Giving a commit a message is mandatory.  The ```-m``` tells git that we're going to give git the message right now. If we didn't put ```-m``` following by the message, git would open up your default text editor and force you to give a message. There's a lot to say on the subject of how to write a good commit message, but for now just use this ```-m``` syntax and keep your messages to be one sentence or less. 

If you type the command ```git log``` you can see that it is now in our log history. Success!

## Changing files
Now that we have a file being tracked by git, we can make some changes. Let's change armin.txt to say: "We lived in fear of the Titans and were disgraced to live in these cages we called walls.” . You can do this in your editor of choice, or you can type:

```echo 'We lived in fear of the Titans and were disgraced to live in these cages we called walls.' > armin.txt``` 

(Note that we had to use single quotes, othewise the terminal wouldn't allow us to use an exclamation point.) Now that we've made a change, type ```git status```. Git tells us that we've modified armin.txt, and that this is 'not staged for commit', or **unstaged**. If a change is **unstaged** then it will not be captured in our snapshot when we type ```git commit```. In order to have it captured in our snapshot, we must first **stage** it by using the ```git add``` command. Type the following:

```git add armin.txt```

Now type ```git status``` again. Git will now say that this is a 'change to be committed' or **staged**. Now we can type the following: 

```git commit -m “Changed the quote to the Grim Reminder.”```

Type ```git log``` and see that we now have two commits in our history!

### Emphasis on terminology
Let's take a brief detour and put some emphasis on the terms we just learned. Specifically: **tracked**, **untracked**, **staged**, and **unstaged**. 

**tracked** and **untracked** refer to whether or not the file is actually in the repository. Just because the file is in the folder doesn't mean git is watching it. In fact, there are some instances where we don't want git to track certain files (we'll look at that in another lesson). To track a file, we have to use ```git add``` to start tracking it.

**staged** and **unstaged** refer to changes to files that are already being tracked by git. If a change isn't staged, it won't be added to the next commit. Conversely, if it is staged, then it will be added to the next commit. 

It's important to keep this stuff in mind, because it's not uncommon to be confused with git early on. Knowing and understanding these terms is really important, and will really help if you run into issues.

## Building up a history
Before we do any other work, let's give ourselves some more files and commits to play around with. First, let's make a file called 'eren.txt' and give it the content of:
```
++===~I~~+~~+++=+:+++++++++++++++++++===:==========:+.:....:
+++,,.~~??~??????????????????I?++++++++++++++==+++=:++~,::::
???,=?~~I+?IIIIIIIIIIIII7???I~I??+???+?++++++++++++=:=~.,,,~
+??~,~+II=IIIIIIIIIIII77IIII=.II??I?????????????++++~?=~,,=~
,++,7$=777777777IIII7$$7II7=,,:III??I???????????????~I=~~,~:
,=~=~$77777777777Z777$Z777=,,,,=7II$IIIIIIIII??I????~=~,,,,~
,I~?+Z777777777$Z77ZZZZ7$=,,,,,,+7I$$IIIIIIIIIIIIII?~=~++++:
+I=+?I7=$$$$$$ZOZ7$ZZ+7$I,,,,,,,,I$7Z$I77$777IIIIIII==~++++=
:++?I=+7Z$$$$$OOO$$Z?,7$,,,,,,,,,,+$Z+$$77$77777777I=++?~~++
:~?+?++$OZZZOOOO?$ZZ,,7.,,,,,,,,,,,,$Z?$Z7ZZ$$777777=7+=====
:7++++?ZOOZZO8O+,$Z:,,$,,,,,,,,,,,,,,7,++Z7ZZZ$$$Z$7I7=+====
$$???Z7788OZ88O,:$Z::,+::,,,::,,,,::,,$:,?OOOO$$$ZZ$$II+?+=+
$$?$?+O+888O88I:,Z=:,,:::::::::::::::::,?$$:ZO$$ZOO$$:??77++
ZZ?II=Z$?:~888:::,?O?ZZ?:::::::::::~ZOI?=~::?OZZZ:Z$Z$??I7??
ZZI=I=?IOI:888:O++88DD8$ZO$:::::$Z8~88888++Z:OZO:?=$$???77??
ZZZI7II7Z::,88:+,,ZZ8OZ,??I=:::=II?+ZO8OZ,+~:8Z=,+=~???II7??
ZZ7IIIIOI,:Z$8::=,,~II~,,::?:::?::,,$,~I8,+::O8O7:+:$III7III
ZO7I7I7O7.:8:7+:::~,..7::?::::::::::=,,,7:::::Z$:~:=$I7I7III
OO77777Z7Z:?ODI:::::::::::::I::::::::::::::::OOO:7:II777$77=
8O7ZZZ$777I:~$,::::::~::::::8::::::::::::::::ZO~O=~I+777ZZ$7
?8DDD8=ZZ$$7:~O::~::::::::::::::::::::~~~~:~7~~8O:~+I$OZ$?77
$8888O=O888O+,8.:::~~~~~~~~~~~~:~:~:~~~~~~~~:~OOO?++$$$$ZO?$
$888888888OI++=8,:~~~~~~~~~~:~:~~~~~~~~~~~~O,:IOO==++O8O87$$
ZIDDN8888O::$++Z.:~~~~~~~~~~~II~~~~~~~~~~~:,,,,:::O???888?ZZ
ZZDDDDD88==8Z++8~.:~~~~~~~~~~~~~~~~~~~~~~~:++==~==8OIZ8Z8ZZZ
ZZ$8Z+?8++?+DDND=~.:~~~~~:7++~?+I=~~~~~~~7=+~:+=:~8DDD:~IZZZ
OZ8????8~+~=ODDD=~OD,~~~~~:I7I=::~~~~~~?8$=~?~I=:~DNND:~:$ZO
8I??$?$:=~:==D==7OOZ8,:~~~~~~~~~~~~~~~ZO8O77~+~~~~DND,:~:778
???????~====+~I778O:$DD,~~~~~~~~~~~~ZOO?O8O77I~~~~DND:~=?III
IIIIIIIZ====~777OOOD$D8888~~~~~~~~8O8Z$:O88877I~:~DD~:::=III
O7ZIIIIZ~~+=7777888D~$$N8O88~~~~OODO$7~~O88N777I=:DD,::~IIII
OIIIIIII=+~=777$88O8~~O$$DDOOO88O8O$$7~:O888O777I~8O===~ZIII
877IIIII+=I7777888O~~~$$$$$8888O8$$~7~~~8888877777~8=+~=ZI77
=$77777Z=777777O8O~~~~~Z$$$$$OOZ$7~7:~~$~8888$77777=7$$7$777
IZ7777777777777DD~~~~~~~7~~$$$$$?~~8~~~~~~DO8O777777~8$$7777
+87777ND8777777D~~~~~~~~$?~~~:~~~~=~~~~~~~~~OO7777777:~:7777
?~~~,IO8DN777778~~~~~~~~~7~~~~~~~~:~~~~~~~~~O87777$8N7:ZI$77
777777INNDZ$$$$D==========~=================O8$$$$8D878Z$Z7+
```
Nice, huh? We can make another one called 'swords.txt' with the content of:
```
::~~:~~::~:~~~~~~~~~~~~~~~~~~~~=~~~~~==~
~::~:~:~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~=
~~~~~~~~~$7~~~~~~~~~~~~~~~~~$=~~~~~~====
~~:~::~~~~Z$8~~~~~~~~~~~~~~$O~~~~=~=====
~~~~~~~~~~~=7$~~~~~~~~~~~~ZO=~~~~=======
~~~~~~~~~~~~~$78~~~~~~~~OZD~~~~~~~~===~=
:~:~~~~~~~~~~~?7$~~~~~~ZZ~~~~~==========
::~~~~~:~~~~~~~~7Z8~~:ZZ~~~~~~=~========
::~~~~~~~~~~~~~~~$$ZZ$8~~~~~~~~~~=~=====
~~~~~~~~~~~~~~~~~~~Z$8~~~~~~~~==~=======
:~::~~~~~~~~~~~~~+$7$$$I~~~~~==~========
~~~~~~~~~~~~~~~~7$O~~=$$O~~~=~==========
~~~~~~~~~~~~~~~$$8~~~~~$$ZO=====~~======
:::::::~~~~~~$$$8~~~~~~~+$O8~=~=~==~====
~:~~~~~~~~~~Z$D7~~~~~~~~~~$$DD8O=~~=====
~~::~~~788D8OD8O~~~~~~~=~~?DD8DDD8==~===
::::~~~DN8D88D88O?~~~~~~~=88D8+DD8======
:::~~~~~8DDO$:D8~~~~~~~~~~~8$D$D888=====
:~::~~88DND~=:8~~~~~=~~~~~~.~$8$8OD88===
::~::D8DDO8?8~~~~~~~~~~~~~~~~.~8=IOD88==
:~~:OOND~~~8~~~~~~~~~=~~~~~~~~:~O=IOD88=
:::8OND8~~?O~~~~~~~~~~~~~~~~~~=~=~. I8==
:::,+8~~~~~~~~~~~~~~~~~~~~~~~~=~~~~~====
~:::::~:~~~~~~~~~~~~~~~~~~~~=~~~========
~~::~::~~~~~~~~~~~~~~~~~~=~=~===========  
```
Perfect. Now you can add these to your repository using the command ```git add -A```. The ```-A``` adds tracks all untracked files and stages all unstaged changes. You could also add them individually by doing:

```
git add eren.txt
git add swords.txt
```

Your choice! Now let's commit these by typing ```git commit -m "Added some sweet ASCII art."```

## Going back in time
Let's say that we don't like this new Attack on Titan quote after all. It may be the more ominous, but the first quote just sounds cooler. There are a couple of ways to go about getting different versions of files in git, so we'll go through more than one. Let's start by using the ```git checkout``` command. 

Remember how when you type ```git log```, you see this really long string of letters and numbers next to the word 'commit'? That's called a SHA-1 tag (usually pronounced shaw-one). It's the unique identifier for the commit. If we want to get a version of a file at a specific commit, we need that identifier. So, copy the SHA-1 tag of the initial commit. Now type the following:

```git checkout ab2bacee5cad armin.txt``` (replace ```ab2bacee5cad``` with your SHA-1 tag)

You'll see that armin.txt now has the contents of 'On that day, mankind received a grim reminder.', just like it did in that version of the file. Cool, huh? Now if you do a ```git status``` you'll see that the change has already been staged for you. You could make a commit and put that file back at the state you wanted it.

But maybe this isn't what you wanted. Maybe you didn't want to get an old version of the file, but an old version of your entire project. You could reset your whole project back to an earlier state by using the ```git reset --hard``` command. If you wanted to go back to your initial commit, you could type: 

```git reset --hard ab2bacee5cad``` (replace ```ab2bacee5cad``` with your SHA-1 tag)

Go ahead and do that now. Then type ```ls``` to see that your new files are gone, and type ```git log``` to see that your commit history has been reset to be as if you were at your initial commit again. But what happens if we didn't want to do that? Where did your files go? What about your commit history? How can you get back to the state you were just at? Have you just lost all of your work?!

### The magic of reflog
Calm down, your history is still there! There's this magic little command that git has that most people actually don't know about. It's called ```git reflog```. Type that now.

You'll see a list of actions you have performed, and that list includes the normal things like commits, but also things like resets. And you can see here that git still has a history of your commits, even if they don't appear in the ```git log```. So fear not, you should see an entry for a commit with the message of 'Added some sweet ASCII art.' Grab the SHA-1 for that line and type:

```git reset --hard 31320af``` (replace ```31320af``` with your SHA-1 tag)

Now you're back to where you were before the reset! You'll find that with git, you can get yourself out of pretty much any jam as long as you commit at regular intervals.


## Recap
Let's do a quick run-down of the general workflow we've learned in this lesson. 

1. Create a repository by typing ```git init <repo-name>```.
2. Create some files.
3. Track those files using ```git add <filename>```.
4. Commit those files using ```git commit -m "<message>"```.
5. Make whatever changes you want, and when you're at a good checkpoint, use ```git add -A``` or ```git add <filename>``` to stage the changes.
6. Commit your staged changes using ```git commit -m "<message>"```.
7. Repeat steps 2-6 as necessary.

Then, if you ever need to get an old version of a file, use ```git checkout <SHA-1> <filename>```.
Or, if you want to reset your entire project back to an old commit, use ```git reset --hard <SHA-1>```.

# Key Commands
As an easy reference, here's a list of commands we learned in this lesson. 
*Note: terms in < > are places where you put your own text. Do not inclue the < > when actually writing the command.*

* ```git init <repo-name>```: Initializes an empty git repository with the name you give it.
* ```git status```: Tells you the status of the files in your repository, including things like stage/unstaged changes, tracked/untracked files, and more.
* ```git add <filename>```: Tracks an untracked file or stages an unstaged change.
* ```git add -A```: Tracks all untracked files and stages all unstaged changes.
* ```git commit -m "<message>"```: Makes a snapshot in time of all of your staged changes with the message you give it.
* ```git log```: Lists your commit history.
* ```git checkout <SHA-1> <filename>```: Swaps out the file specified with the version of the file that was active in the commit given by the SHA-1 tag.
* ```git reset --hard <SHA-1>```: Resets your whole project back to the commit specified by the SHA-1 tag. 
* ```git reflog```: Gives a list of all the snapshots of your project, even if those snapshots are things like resets and merges. It even includes commits that would otherwise not be listed after a ```git reset --hard``` by ```git log```. 
* ```git ```: Shows how to use the ```git ``` command and lists commonly used commands in git with a short description.
* ```git help <command> ```: Displays more information about a specific git command.

#Additional Resources
* [Git Succinctly](http://net.tutsplus.com/sessions/git-succinctly/): A fantastic guide on getting started with Git.
