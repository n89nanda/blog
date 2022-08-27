server: git_status
	hugo serve

compile:
	hugo

git_status:
	git status

commit: git_status
	git add .
	git commit -m $(msg)

deploy: compile commit
