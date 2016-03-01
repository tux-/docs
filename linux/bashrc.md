Bashrc
======

Set up a git friendly prompt
----------------------------
```
if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;36m\]\w\[\033[00m\]$(__git_ps1 " [\[\033[00;33m\]%s\[\033[00m\]] ")\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(__git_ps1 " [%s] ")\$ '
fi
unset color_prompt force_color_prompt
```
