How to Upload / Publish to Github
…or create a new repository on the command line

echo # Blog >> README.md

  $ git init

  $ git add README.md

  $ git commit -m "first commit"

  $ git remote add origin https://github.com/DSAMPAT/Blog.git

  $ git push -u origin master

…or push an existing repository from the command line

  $ git remote add origin https://github.com/DSAMPAT/Blog.git

  $ git push -u origin master

To Check the status of an app and see what has been changed or modified or deleted since the last commit

  $ git status

To Check the Differences of an app and see what has been changed or modified or deleted since the last commit

  $ git diff

To commit all changes

	$ git add –A
	
or	

  $git add * -f

To delete all un-committed changes or new files/folders

	$ clean –d –f
	
Or to revert any file modifications or changes and restore back to your last commit

	$ git reset HEAD --hard
	
To commit all changes to the local repository

	$ git commit –m “change desc”
	
To Upload to github repository

	$ git push origin master
	
To upload to Heroku

	$ git push heroku master
	
To login to Heroku

	$ heroku login
	
To compile/generate a new app

	$ heroku create
	
To view the config file

	$ cat .git/config
	
Heroku 
DEV Cloning
	heroku git:clone -a app-staging
Prod Cloning
	heroku git:clone -a app-production

To create a new App
	cd to the copy of an app folder or a new folder

Open Terminal
	cd test
	heroku create

Deploy / Update

Make changes via Text Editor / Notepad / Sublime Text

Commit the changes to save all modifications
	git commit –a –m “Change Desc”
	git push heroku master

Check that you are connected to the correct Heroku App Environment
	git remote -v
		heroku git:remote –a newappname
			heroku git:remote –a randomname-randomname-randomnumber
			heroku git:remote –a app-staging
	heroku run rake db:migrate --app app-staging

Commit all changes and upload to app
	git push heroku master				//Publish Master Branch
	git push heroku develop:master -f --progress	//Publish Develop Branch

Initilise site
	heroku rake db:seed 				//This will create the initial site parameters e.g. users

Add Tags to Commits
	git -c diff.mnemonicprefix=false -c core.quotepath=false tag -a -m "" v1.3.1
	git -c diff.mnemonicprefix=false -c core.quotepath=false push -v origin refs/tags/v1.3.1

Tag older commits
	git tag -a v1.2 9fceb02 -m "Message here"
	git push --tags origin master

