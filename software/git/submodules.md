Submodules | Git
================

Pull down submodules only
-------------------------

```bash
git submodule update
```

Pull with down submodules
-------------------------

```bash
git pull && git submodule update
```


Clone with submodules
---------------------

```bash
git clone --recursive git://github.com/foo/bar.git
```

Clone submodules to a checked out repo
-------------------------------------

```bash
git submodule update --init --recursive
```
