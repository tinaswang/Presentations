# PresentationTemplate

Presentation template in revealjs with ORNL logos

## To see it locally:

```
python -m SimpleHTTPServer 8000

```
## To have it visible to the world:

To make it available in github pages do:
```
# create new branch named gh-pages
git checkout --orphan gh-pages

# Add and commit stuff
git add .
git commit -m 'push master into gh-pages'

# push the new branch upstream
git push origin gh-pages
```

To make the current version viewable:
```
git checkout  gh-pages
# Assuming the last updated branch was master
git rebase master
#
git push
```

Go to:

http://ricleal.github.io/Presentations
