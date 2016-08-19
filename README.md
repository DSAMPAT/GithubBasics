How to Upload / Publish to Github
---------------------------------

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
	
HEROKU BASICS
-------------

DEV Cloning

	$ heroku git:clone -a app-staging

Prod Cloning

	$ heroku git:clone -a app-production

To create a new App

	cd to the copy of an app folder or a new folder

Open Terminal

	cd test

	$ heroku create

Deploy / Update

Make changes via Text Editor / Notepad / Sublime Text

Commit the changes to save all modifications

	$ git commit –a –m “Change Desc”
	$ git push heroku master

Check that you are connected to the correct Heroku App Environment

	$ git remote -v
		$ heroku git:remote –a newappname
			$ heroku git:remote –a randomname-randomname-randomnumber
			$ heroku git:remote –a app-staging
	$ heroku run rake db:migrate --app app-staging

Commit all changes and upload to app

	$ git push heroku master				//Publish Master Branch
	$ git push heroku develop:master -f --progress	//Publish Develop Branch

Initilise site

	$ heroku rake db:seed 				//This will create the initial site parameters e.g. users

Add Tags to Commits

	$ git -c diff.mnemonicprefix=false -c core.quotepath=false tag -a -m "" v1.3.1
	$ git -c diff.mnemonicprefix=false -c core.quotepath=false push -v origin refs/tags/v1.3.1

Tag older commits

	$ git tag -a v1.2 9fceb02 -m "Message here"
	$ git push --tags origin master

BACKUPS
-------

Create a backup

The Manual process and it seems that we can also create a backup by just accessing the site once daily, after you log in.

Heroku Postgres :: Aqua

	https://postgres.heroku.com/databases/bloom-wood-9999-heroku-postgresql-aqua?addon_action=capture_backup

Heroku Postgres :: Olive

	$ https://postgres.heroku.com/databases/bloom-wood-9999-heroku-postgresql-olive?addon_action=capture_backup
	or
	$ heroku pg:backups capture
	or
	$ heroku pg:backups public-url

and then download the dump file by opening the public link that will expire after a few minutes

	$ heroku pg:backups public-url | cat
	$ curl -o latest.dump `heroku pg:backups public-url -a sushi`

Scheduling Backups

	$ Heroku pg:backups schedule --at ’02:00 Australia/Perth’ DATABASE_URL --app bloom-wood-9999

Downloading a Backup

	$ curl -o  latest.dump ‘heroku pg:backups public-url -a bloom-wood-9999’
	or
	Run	

		$ heroku pg:backups public-url and copy the resultant url
		$ curl -o latest.dump ‘<URL>’

Restore a Backup

To restore a backup from a dump file to the local rails server

	$ pg_restore --verbose --clean --no-acl --no-owner -h localhost -U postgres -d app_development app_b027.dump
then
	$ rake db:migrate

To restore a backup from a dump file located on an AWS S3 storage to a Heroku App

	$ heroku pg:backups restore ‘https://s3-ap-southeast-2.amazonaws.com/app/backups/gbi-staging_orange.dump’ DATABASE_URL

Steps

	Upload the backup file into the Backup folder on AWS S3

	Make the file public so that you can access it

		$ heroku pg:backups restore 'https://s3-2.aws.com/app/backups/20161406_bloom-wood-9999.dump' DATABASE_URL --confirm power-rings-7978

	then

		$ heroku rake db:migrate

	or

		$ heroku run rake

DATABASE MANAGEMENT
-------------------

On your local copy,

Load the backup DB

	$ pg_restore --verbose --clean --no-acl --no-owner -h localhost -U postgres -d App_development production_backup.dump

Reset the DB

	$ bundle exec rake db:migrate:reset
	$ bundle exec rake db:migrate

CONNECTION INFO
---------------

In order to view the repo remote URL

	$ git remote -v

remove staging url

	$ git remote rm heroku

add production url

	$ heroku git:remote -a bloom-wood-9999

show the config and info of the existing app

	$ heroku apps:info --app bloom-wood-9999

tail the logs

	$ heroku logs -t -n 1500 --app bloom-wood-9999

restart the production server

	$ heroku restart -a bloom-wood-9999

open the app from terminal to browser.
	$ heroku open --app bloom-wood-9999

use “git push heroku master -- force” if you have fast forward issues

	$ git push heroku master -- force
	$ git push heroku develop:master -f --progress

LOCAL SERVER
------------

After making sure your server side firewall is open to the incoming connection on high ports (this is normally true and the default port is 3000, so you probably don't have to do anything) you must also start the server like this:

	$ rails server -b 0.0.0.0

which binds it to the universal address. It binds to localhost by default.

Using this method you don't have to bind to port 80, but you can like this:

	$ rails server -b 0.0.0.0 -p 80

(If you're using rvm then you may need to use rvmsudo)

To make this change more permanent edit your config/boot.rb and add this:

	$ require 'rails/commands/server'
	$ module Rails
	$   class Server
	$     def default_options
	$       super.merge(Host:  '0.0.0.0', Port: 3000)
	$     end
	$   end
	$ end

Then you should only have to use rails s

Run local rails server to be access from network

	$ rails s -b 192.168.0.89 -p 3000
