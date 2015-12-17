Git
===

Reattach detached head
----------------------

```bash
git checkout -b temp
git branch -f master temp
git checkout master
git branch -d temp
```
