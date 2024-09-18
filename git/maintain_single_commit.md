
# After creating the PR, for ongoing changes/PR address review comments, use:

```
 git commit --amend
 git push -u origin +<your branch name>
 ```

# Rebase from master:
 ```
 git checkout master
 git pull
 git checkout -  # Switch to your branch
 git rebase origin/master
 git push -u origin +test_pr
 ```

 # if conflicts, then resolve it and then do:
 ```
 git add  .
 git rebase --continue
 git push -u origin +test_pr
```

