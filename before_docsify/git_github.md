# Show previews between two branches
https://github.com/foxbroadcasting/fbccontent/compare/branch1...branch2

# Is commit1 an ancestor of commit2?
```
git merge-base --is-ancestor <commit1> <commit2>
```
exits with status 0 if true, or with status 1 if not

Example:
```
ancestor=c3d5576f70de1bce12ff9315f4d4341124e1faf4
child=e19e45f58c94a23e0ea14a056d0116e9db1d03ab
git merge-base --is-ancestor $ancestor $child
echo $?
```

# Temporarily ignoring files
http://gitready.com/intermediate/2009/02/18/temporarily-ignoring-files.html

```
# ignore file
git update-index --assume-unchanged <file>
git ignore <file> # see the [alias] section of .gitconfig

# unignore file
git update-index --no-assume-unchanged <file>
git unignore <file> # see the [alias] section of .gitconfig

# list ignored files
git ls-files -v | grep ^[a-z]
git ignored # see the [alias] section of .gitconfig
```

# Adding images to github wiki
https://help.github.com/articles/adding-and-editing-wiki-pages-locally/
