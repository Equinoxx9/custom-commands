# custom-commands
Add these lines to .bashrc :

git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/[\1]/'
}

git_color() {
red=$(tput setaf 1)
green=$(tput setaf 2)
yellow=$(tput setaf 3)
branch=$(git_branch 2>/dev/null | grep "^*" | colrm 1 2)
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

export PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]\w'
PS1+="\[\$(git_color)\]\$(git_branch)\[\033[00m\]$ "

#Change Default Terminal Location
project_workspace=0
project_path=Desktop/Workspace/spi
practise_path=Desktop/Practise
if [ "$PWD" = "/home/user39" ]; then
	if [ $(wmctrl -d | grep '*' | cut -d ' ' -f1) = $project_workspace ]; then
		cd  $project_path
	else
		cd  $practise_path 
	fi
fi
clear
