# Dev Logs

This is a collection of important notes gathered throughout working on various projects and contributing to Open-Source repositories.

## Git

### Squashing multiple commits into one.

When you have multiple commits in a branch, you can 'squash' them into a single one.

1. Use git rebase to generate a new commit, for example (if you have 2 previous commits)
```
    git rebase --interactive HEAD~2
```
This opens up the last 2 commits in your editor (probably vim)

2. In the editor, replace 'pick' with 'squash' for all except the first commits. (At this point you will have a commit with a long commit message)

3. Change commit message with the following command.

```
    git commit --amend
```
This opens up vim again, where you can update the commit message

Reference: [link](https://www.internalpointers.com/post/squash-commits-into-one-git)

### Making local master exactly same as origin

```
git fetch origin
git reset --hard origin/master
```

However **DO NOT** hard reset when on a separate branch. If so, do a reflog to view the commit before the 'reset', and hard reset into that commit.

```
git reflog
```

Then find the commit hash and reset.

```
git reset --hard <commit-hash> 
```

Or, better way to update local master, **rebase**:
```
git fetch
git pull --rebase origin master
```
or
```
git fetch
git rebase origin/master
```

### Git rebase vs Git merge

Git rebase, carries all the commits of a feature branch and puts it infront of master when you use the commands:

```
git checkout feature-branch
git rebase master
```
puts all the commits in the feature branch infront of master.

While when you merge a master branch like so:

```
git checkout feature-branch
git merge master
```
You are adding changes from the master branch to the feature branch, and you will need a new commit for the merged changes.

Keep in mind that, merge is a non-destructive command while rebase is a destructive command.

More info on this [link]([https](https://www.atlassian.com/git/tutorials/merging-vs-rebasing))


### What is origin/master?

origin/master is the local copy of branch 'master' on remote named 'origin'

Example: 

```
git fetch origin master
```
Or
```
git fetch
```

This command copies the 'master' branch from 'origin' and and the local copy will be named origin/master

So git fetch basically updates local copy (in this case origin/master).

## Vim

### Keys

* **i** : Press 'i' to start inserting text
* **ESC** : Escape text-inserting mode
* **:x** : Save and quit

### Plugins

These are some of the really useful plugins for vim:

* **NERDTree** : Shows a tree structure for the files and directories.
* **GitGutter** : Shows Git difference in the gutter.
* **Ctrl+P** : Easily navigate through recent files.

### vimrc ultimate configurations

[amix/vimrc](https://github.com/amix/vimrc) comes with the ultimate vim configuration, including all the above plugins and color and font stuff.

### vim navigation tips

* Use Ctrl + } to navigate to downwards, more logical.
* Use T + <any-letter> or F + <any-letter> to move directly to that word in the line.
* Navigation is done by the 'j', 'k', 'l', 'h' keys. Moving back and forth through words is done by the keys 'w', 'e', 'b'.

## Express

### Using middlewares

You can use middlewares to intercept the (req,res,next) objects before the controllers.

```javascript

app.get('/home',middleware1 , (req,res) =>{ ... })
// Or for multiple middlewares
app.get('/home',[middleware1 , middleware2] , (req,res) =>{ ... })

```

However avoid using middlewares if possible, as it intercepts any and every request and slows it down.

### Tip: use return res.end() or return next()

It is important to use the return keyword in some cases to complete the execution of the function, sometimes when there is no return keyword, the preceeding code will run and may end up with errors.

## Docker

### Tips

* When using alpine as the base image in a Dockerfile, remember you won't be able to use debian commands like 'sudo apt-install',
* 'docker-compose up' builds and runs the app, but might need to rebuild if you've made changes to the dockerfile.
* Remember 'Docker' runs in an isolated environment and has no additional apps installed unless specifiedi (like chromium for example).

## OAuth

[PassportJS](https://passportjs.org) is a great tool for authentication in NodeJS apps, However keep in mind, not all modules are OAuth2.

* For example, twitter is OAuth 1.0a whereas linked-in and google is OAuth2.0

## Npm on Ubuntu

Sometimes ubuntu won't let you install packages, with error 'EACESS no permissions'. Then,

```
sudo npm install --save-dev  --unsafe-perm=true --allow-root

```

## CSS Handy tips

* User gridboxes and flexboxes
* Minmax and clamp
* Use units like (fr) for gridboxes

[Link to glitch.me video](https://1linelayouts.glitch.me/)
