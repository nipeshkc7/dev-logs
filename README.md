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

Or, better way, **rebase**:
```
git fetch
git pull --rebase origin master
```
or
```
git fetch
git rebase origin/master
```

However **DO NOT** hard reset when on a separate branch. If so, do a reflog to view the commit before the 'reset', and hard reset into that commit.

```
git reflog
```

Then find the commit hash and reset.

```
git reset --hard <commit-hash> 
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