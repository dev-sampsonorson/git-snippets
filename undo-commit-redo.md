# Undo a commit & redo it

<!-- language: shell -->

    $ git commit -m "Something terribly misguided" # (0: Your Accident)
    $ git reset HEAD~                              # (1)
    [ edit files as necessary ]                    # (2)
    $ git add .                                    # (3)
    $ git commit -c ORIG_HEAD                      # (4)

1. This command is responsible for the **undo**. It will undo your last commit while **leaving your working tree (the state of your files on disk) untouched.** You'll need to add them again before you can commit them again).

3. Make corrections to working tree files.
4. `git add` anything that you want to include in your new commit.
5. Commit the changes, reusing the old commit message. `reset` copied the old head to `.git/ORIG_HEAD`; `commit` with `-c ORIG_HEAD` will open an editor, which initially contains the log message from the old commit and allows you to edit it. If you do not need to edit the message, you could use the `-C` option.

**Alternatively, to edit the previous commit (or just its commit message)**, `commit --amend` will add changes within the current index to the previous commit.


  [1]: https://stackoverflow.com/q/179123/1146608
  [2]: https://git-scm.com/docs/git-reset


**To remove (not revert) a commit that has been pushed to the server**, rewriting history with `git push origin master --force` is necessary.


-----
## Further Reading
https://stackoverflow.com/questions/34519665/how-to-move-head-back-to-a-previous-location-detached-head/34519716#34519716

The above answer will show you `git reflog`, which you can use to determine the SHA-1 for the commit to which you wish to revert. Once you have this value, use the sequence of commands as explained above.

----
`HEAD~` is the same as `HEAD~1`. The article [What is the HEAD in git?](https://stackoverflow.com/a/46350644/5175709) is helpful if you want to uncommit multiple commits.