# Dev Logs

This is a collection of important notes gathered throughout working on various projects and contributing to Open-Source repositories.

## Github

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
    git commit --append
```
This opens up vim again, where you can update the commit message

Reference: [link](https://www.internalpointers.com/post/squash-commits-into-one-git)


## Vim

### Keys

* **i** : Press 'i' to start inserting text
* **ESC** : Escape text-inserting mode
* **:x** : Save and quit

