# custom-commands
Add these lines to .bashrc :

```bash
git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/[\1]/'
}

git_color() {
red=$(tput setaf 1)
green=$(tput setaf 2)
yellow=$(tput setaf 3)
branch=$(git branch 2>/dev/null | grep "^*" | colrm 1 2)
boshka= git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/' > /dev/null 2>&1
if git rev-parse --git-dir > /dev/null 2>&1; then
    if ! git status | grep "nothing to commit" > /dev/null 2>&1; then
      echo "${red}"
      return 0
    elif $boshka; then
if [ "$branch" = "master" ]; then
  echo "${yellow}"
else 
	echo "${green}"
fi
    fi
fi
}

git_when_color(){
	color=$(tput setaf 0)
	echo "${color}"
}

git_when(){
	date +"%d/%b/%y" -d @$(stat -c %Y .git/FETCH_HEAD 2> /dev/null) 2> /dev/null | sed 's/\(.*\)/\(\1\)/'
}

export PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]'
PS1+='$(basename "$PWD")/'
# PS1+='\w'
PS1+="\[\033[00m\]" #Small Font
PS1+="\[\$(git_color)\]\$(git_branch)" #Git Branch
PS1+="\[\033[01;6m\]" #Big Font
PS1+="\[\$(git_when_color)\]\$(git_when)" #Git last pull
PS1+="\[\033[00m\]$ "

#Change Default Terminal Location
# project_workspace=0
project_path=Desktop/Workspace/spi
# practise_path=Desktop/Practise/ROR/livify
if [ "$PWD" = "/home/user39" ]; then
	#if [ $(wmctrl -d | grep '*' | cut -d ' ' -f1) = $project_workspace ]; then
	cd  $project_path
	#else
		#cd  $practise_path 
		#code .
	#fi
fi
clear
```
