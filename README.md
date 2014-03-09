CouchDB plugin for Dokku
------------------------

Project: https://github.com/progrium/dokku


Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/martin-hewitt/dokku-couchdb-plugin couchdb
dokku plugins-install
```


Commands
--------
```
$ dokku help
     couchdb:create <app>     Create a CouchDB container
     couchdb:delete <app>     Delete specified CouchDB container
     couchdb:info <app>       Display database informations
     couchdb:link <app> <db>  Link an app to a CouchDB database
     couchdb:logs <app>       Display last logs from CouchDB contain
```

Simple usage
------------

Create a new DB:
```
$ dokku couchdb:create foo            # Server side
$ ssh dokku@server couchdb:create foo # Client side

-----> CouchDB container created: couchdb/foo

       Host: 172.16.0.104
       User: 'root'
       Password: 'RDSBYlUrOYMtndKb'
       Database: 'db'
       Public port: 49187
```

Deploy your app with the same name (client side):
```
$ git remote add dokku git@server:foo
$ git push dokku master
Counting objects: 155, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (70/70), done.
Writing objects: 100% (155/155), 22.44 KiB | 0 bytes/s, done.
Total 155 (delta 92), reused 131 (delta 80)
remote: -----> Building foo ...
remote:        Ruby/Rack app detected
remote: -----> Using Ruby version: ruby-2.0.0

... blah blah blah ...

remote: -----> Deploying foo ...
remote: 
remote: -----> App foo linked to couchdb/foo database
remote:        DATABASE_URL=mysql://root:RDSBYlUrOYMtndKb@172.16.0.104/db
remote: 
remote: -----> Deploy complete!
remote: -----> Cleaning up ...
remote: -----> Cleanup complete!
remote: =====> Application deployed:
remote:        http://foo.server
```


Advanced usage
--------------

Inititalize the database with SQL statements:
```
cat init.sql | dokku couchdb:create foo
```

Deleting databases:
```
dokku couchdb:delete foo
```

Linking an app to a specific database:
```
dokku couchdb:link foo bar
```

CouchDB logs (per database):
```
dokku couchdb:logs foo
```

Database informations:
```
dokku couchdb:info foo
```
