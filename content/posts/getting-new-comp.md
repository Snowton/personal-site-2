---
title: "Things to do when getting a new computer"
date: 2021-12-14T23:28:27-05:00
draft: false
---
Houskeeping list for myself.
<!-- ## Things to do when getting a new computer -->

- [ ] Download chrome, vscode, tinytex
- [ ] Make sure to not set chrome as default
- [ ] Change dock
- [ ] Change terminal appearance (i.e. paste the following in .zshrc)
```
function parse_git_branch() {
    git branch 2> /dev/null | sed -n -e 's/^\* \(.*\)/[\1]/p'
}

setopt PROMPT_SUBST
export PROMPT='%F{228}%n%f %F{197}%~%f %F{39}$(parse_git_branch)%f %F{normal}$%f '
```
- [ ] Store previous files in hard drive
- [ ] Install python3
- [ ] Install home-brew
- [ ] Install jdk
- [ ] Configure vscode (extensions, code command)
- [ ] Pin tabs, etc
- [ ] Get relevant folders back from hard drive: downloads, latex, program files (personal site)
- [ ] Get that thing (oh, Hugo https://gohugo.io/getting-started/)
- [ ] Make ssh key and put it in GitHub