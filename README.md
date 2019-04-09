# mongodb-with-python-tutorial
MongoDB with Pymongo Tutorial

### Installing

```
$ pip install pymongo
```

### Making a Connection

Making a connection without authentication:

```
>>> from pymongo import MongoClient
>>> uri = 'mongodb://mongodb.domain.com:27017/'
>>> client = MongoClient(uri)
>>> client.database_names()
[u'admin', u'local', u'mycargarage', u'random_api', u'shared_db', u'testdb']
```

Making a connection with authentication:

```
>>> from pymongo import MongoClient
>>> uri = 'mongodb://username:password@mongodb.domain.com:27017/random_api?authSource=admin&authMechanism=SCRAM-SHA-1'
>>> client = MongoClient(uri)
>>> client.database_names()
[u'admin', u'local', u'mycargarage', u'random_api', u'shared_db', u'testdb']
```
