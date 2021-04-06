# Create ssh git remote 

read local ssh key
	
	cat ~/.ssh/id_rsa.pub

Check current remote connection type (type is based on ssh or https)	
	
	git remote get-url origin

remove the current remote connection

	git remote remove origin

Add your ssh key to the github repo

![[Pasted image 20210101141855.png]]

Add the github repo

	git remote add origin  git@github.zhaw.ch:voro/MA-Bioinformatics-Workflows.git

Check if it is added

	git remote -v

Set the push to upstream (https://stackoverflow.com/questions/37770467/why-do-i-have-to-git-push-set-upstream-origin-branch)

	git push --set-upstream origin master
	
# Notes
* The user.name can be set individually and does not have to match the user name of the github repo