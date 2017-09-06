Config | Git
============

Core
----

Make sure you commit with lf
```
[core]
	autocrlf = false
	eol = lf
```


List config
-----------

Config values might be overwritten by equal keys. Bottom config value will be used.

```bash
git config -l
```


Edit global config
------------------

```bash
git config --global -e
```


Setup alias to uncommit
-----------------------

```bash
git config --global alias.uncommit '!git reset --soft HEAD^'
```
Undo the action of committing: ```git uncommit```.


Setup alias for multiple email users on one machine.
----------------------------------------------------

Some times you might want to use different emails for different projects.
```bash
git config --global alias.workprofile 'config user.email "user@work.lan"'
```
Then when you check out a rep, run: ```git workprofile```.


List ignored files
------------------

Lets say you did something like this to ignore a file:
```bash
git update-index --assume-unchanged filename.ext
```
If you want to list those files that are ignored, you can add this alias to the config.
```bash
git config --global alias.ignored '!git ls-files -v | grep "^[[:lower:]]"'
```
Show ignored files: ```git ignored```.


Find commits with a keyword in the commit message
-------------------------------------------------

```bash
git config --global alias.find '!f(){ git log --grep=$1; };f'
```
Show commits: ```git find keyword```.
