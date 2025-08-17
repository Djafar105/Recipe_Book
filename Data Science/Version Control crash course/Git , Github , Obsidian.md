## Git
### Intro
* In Git, the **main timeline** is called `main`. and can be reffered to 'on branch master' in bash 
* Creating a **branch** is like spinning off a parallel timeline where you can freely experiment (sandbox). after being done , you **commit** these changes or whatever 
* Each **commit** is a snapshot that insert changes onto whichever timeline you’re working in. 
* ***Pushing** is a term used if you want to add the commit online to github we say , push the commit  
* When you **merge**, Git tries to superpose two timelines back into one. This isn’t chaotic—Git looks at their common ancestor, compares the differences, and automatically combines them if no file lines conflict. If both timelines edited the same lines, Git marks this as a **merge conflict**, asking you to choose or combine the changes manually. Once resolved, the timelines are unified into a coherent history.

### Useful commands
* **pwd*** : prints my current directory
* ***cd /c/pathway*** : puts the tentacle in that exact position (pathway)
* ***mkdir newfolder*** : creating new folder via bash  then when cd you dont need to put the whole pathway , just the name of the folder and it will know , but if you do it manually then whole pathway 
* ***git init*** : basically activating the tentacle in that specefic location by creating a .git folder there that is invisible by default for protection 
* ***echo*** : This command works like Python’s `print()`, outputting text to the screen by default. Using `>` redirects this output into a file, creating the file if it doesn’t exist or **overwriting** it completely if it does. To avoid overwriting and instead add text at the end of an existing file, you use `>>`, which appends the output. So when you run `echo "aaslema !" > notes.txt`, you’re creating a new file called `notes.txt` in the current folder with the content “Hello Git!”, replacing any previous content if the file already existed.
* ***git status*** : it is kinda the dahsboard , it shows what are the tentacles ,are activly controlling and the commits needed to be made to that environment and any untracked files , meaning even if no commit done to the changes , git will understand and is aware of their presence but doesnt include them in the timeline until you commit 
* ***git add*** : this is like preparing a plate for the commit agent. you explicitly select which files you want to serve up for the next commit — placing them on the plate. You can add a single file, a list of files, or everything in the current directory with `git add .`. Nothing on the plate is permanent until you run `git commit`, in short it can be seen as a curating tool for allready at least once tracked files that are now modified , and a necessary tool to commit new untracked files
* ***git commit -m"messgae of the commit"*** : this is it , via this action you have inserted the shoping cart contents into the timeline ! , you can commit all the changes at once via `-am` if you didnt do the staging part and your files are allready have been tracked at least once and the -m is for the commit message that is obligatory
* ***git log*** : so basically this gives you an overview on the whole history from the root commit until the last one , and for more condensed overview you can add `--oneline`
* ***git diff*** : shows the changes made at the time

## Github
### Intro
* Github is basically an ocean of octapuses with unlimeted tentacles, in it you can be one and by being so you can either showcase whats in control in the scope of your set of tentacles , or hide them from the world and just see it as backup security plan in case the local setup is dead , or you can be a scuba diver with an access to everything public basically by other octapuses 
### Commands
* ***git remote add insert_name URL_of_the_repo*** :  this command is just an **initiation step** that introduces your local repository to the existence of a remote repository by giving it a shortcut name (`insert_name`) that is associated with the first root url that reflects the remote repo , basically we are storing the mirror to that remote cloud based repo(that is the url) in a simple configuration file located at `.git/config`, where it stores the remote’s name (`insert_name`) and the corresponding URL. 
* to check if there are any remote aded , do the command `git remote -v` if nothing show up , it means nothing was added 
* ***git branch -M main*** : simply **renames the current branch from `master` to `main`**, replacing the old name (used up to 2020) with the new one (2020-).
* ***git push -u insert_name main*** : this is basically the final thing , uploading  the local repo to a cloud based one in github platforme , for this to happen you need to make sure that you have the updated version of the online repo otherwise git will refuse , it is basically a safety thing , like you dont actually push the updates only but you need to first acquire the whole project (via a pull command) , then you can resend it back with the new commits , for it appears to me as a waste of resources but apperantly this is very important and secure , and in order the save the integrity of history documentation when you push you can only push everything , aka all the commits not sent 
* ***git pull insert_name main*** : this commands allows basically to update the local repo by activly downloading everything from the cloud repo , the thing here is that , when you pull you need to have the local unchanged or else youd have to merge them if you changed both the remote and the cloud since your last push , to merge you need the command : `git pull insert_name main --allow-unrelated-histories --no-edit`
* ***git clone URL*** : this allow you to copy an online repo into the the current active tentacle 

## Obsidian/Github :
### Intro 
* This is basically a documentation on how to make a local obsidian vault synced on a remote repo on github 
* The goal would be to be able to manually push changes done in an obsidian vault to a repo online , (no automtic sync for history integration)
* ***Token*** : or **Personal Access Token PAT** is a quite literally a token , (jeton in french) that serves as digital key that gives you access to repositories with customizable permissions. there are two types of tokens :
	* **Classic** : straight forward permisson scope 
	* **Fine grained** : specefic scope of permission 
	basically treat obsidian vault as a normal file thats it 
	
