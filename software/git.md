Git
===

To set up a git friendly prompt on linux, see [bashrc](../linux/bashrc.md).

Reattach detached head
----------------------

```bash
git checkout -b temp
git branch -f master temp
git checkout master
git branch -d temp
```


Pull down submodules
--------------------

```bash
git submodule foreach git pull origin master
```


Clone with submodules
---------------------

```bash
git clone --recursive git://github.com/foo/bar.git
```

Pull submodules to a checked out repo
-------------------------------------

```bash
git submodule update --init --recursive
```
