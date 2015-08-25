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
	

