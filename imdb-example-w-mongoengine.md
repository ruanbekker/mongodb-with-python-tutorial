```
docker run -itd ruanbekker/mongodb:python
docker exec -it f5b357cd3822 sh
```

```
wget https://raw.githubusercontent.com/steveren/docs-assets/charts-tutorial/movieDetails.json
mongoimport --db test --collection movieDetails --drop --file movieDetails.json
```

```
from pymongo import MongoClient
client = MongoClient()
db = client['test']
collection = db['movieDetails']
collection.find_one()
# {u'tomato': {u'rating': 9.0, u'userReviews':
```

```
import mongoengine
mongoengine.connect('test', host='mongodb://localhost:27017/test')

class Imdb(mongoengine.EmbeddedDocument):
    meta = {'collection': 'movieDetails'}
    id = mongoengine.StringField()
    rating = mongoengine.DecimalField()
    votes = mongoengine.IntField()

class Tomato(mongoengine.EmbeddedDocument):
    meta = {'collection': 'movieDetails'}
    meter = mongoengine.IntField()
    image = mongoengine.StringField()
    rating = mongoengine.IntField()
    reviews = mongoengine.IntField()
    fresh = mongoengine.IntField()
    consensus = mongoengine.StringField()
    userMeter = mongoengine.IntField()
    userRating = mongoengine.DecimalField()
    userReviews = mongoengine.IntField()

class Awards(mongoengine.EmbeddedDocument):
    meta = {'collection': 'movieDetails'}
    wins = mongoengine.IntField()
    nominations = mongoengine.IntField()
    text = mongoengine.StringField()
    
class Movie(mongoengine.Document):
    meta = {'collection': 'movieDetails'}
    title = mongoengine.StringField()
    year = mongoengine.IntField()
    rated = mongoengine.StringField()
    runtime = mongoengine.IntField()
    countries = mongoengine.ListField()
    genres = mongoengine.ListField()
    director = mongoengine.StringField()
    writers = mongoengine.ListField()
    actors = mongoengine.ListField()
    plot = mongoengine.StringField()
    poster = mongoengine.StringField()
    imdb = mongoengine.EmbeddedDocumentField(Imdb)
    tomato = mongoengine.EmbeddedDocumentField(Tomato)
    metacritic = mongoengine.IntField()
    awards = mongoengine.EmbeddedDocumentField(Awards)
    type = mongoengine.StringField()
```
```
Movie.objects.first()
# <Movie: Movie object>

movie = Movie.objects.first()
movie.actors
# [u'Claudia Cardinale', u'Henry Fonda', u'Jason Robards', u'Charles Bronson']

movie.to_json()
# '{"_id": {"$oid": "5b107bec1d2952d0da9046e0"}, "title": "Once Upon a Time

Movie.objects(year__lte=1988)
# [<Movie: Movie object>, <Movie:

Movie.objects(year__lte=1988)[0]
# <Movie: Movie object>

Movie.objects(year__lte=1988)[0].actors
# [u'Claudia Cardinale', u'Henry Fonda', u'Jason Robards', u'Charles Bronson']

Movie.objects(imdb__rating__gte=9)
# [<Movie: Movie object>, <Movie: Movie object>,

Movie.objects(imdb__rating__gte=9)[0]
# <Movie: Movie object>

Movie.objects(imdb__rating__gte=9)[0].title
# u'Gamechangers Ep. 3: A Legend in the Booth'

Movie.objects(title__contains='Love')
# [<Movie: Movie object>, <Movie: Movie object>,

[a.title for a in Movie.objects(title__contains='Love')]
# [u'Dr. Strangelove or: How I Learne

[a.actors for a in Movie.objects(title__contains='Love') if a.title == 'Shakespeare in Love']
# [[u'Geoffrey Rush', u'Tom Wilkinson',

Movie.objects.count()
Movie.objects(actors__size=2)
```

- https://docs.mongodb.com/charts/master/tutorial/movie-details/prereqs-and-import-data/
