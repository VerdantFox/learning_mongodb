# Show databases
show dbs

# Move into database
use DATABASE
use video

# Show collections in a database
show collections

# Find on all documents in collection (while in database)
db.COLLECTION.find().pretty()
db.movieDetails.find().pretty()

# Get a count of documents returned
db.COLLECTION.find().count()
db.movieDetails.find().count()

# Find with a query
db.COLLECTION.find(QUERY).pretty()
db.movieDetails.find({"genres": "Family"}).pretty()

# Find with a query and limiting projection (ie limit fields shown)
db.COLLECTION.find(QUERY, PROJECTION).pretty()
db.movieDetails.find({"genres": "Family"}, {"title": 1}).pretty()

### Note: include fields with 1, exclude with 0. to exclude "_id" use:
db.movieDetails.find({"genres": "Family"}, {"title": 1, "_id": 0}).pretty()

## Insert document
db.COLLECTION.insertOne(DOCUMENT)
db.moviesScratch.insertOne({"title": "The Martian"})

## Insert many documents (Can use ordered false to keep going with error)
db.COLLECTION.insertMany([DOCUMENT, DOCUMENT, DOCUMENT...])
db.moviesScratch.insertMany(
    [
        {
	    "_id" : "tt0084726",
	    "title" : "Star Trek II: The Wrath of Khan",
	    "year" : 1982,
	    "type" : "movie"
        },
        {
	    "_id" : "tt0796366",
	    "title" : "Star Trek",
	    "year" : 2009,
	    "type" : "movie"
        },
    ],
    {
        "ordered": false 
    }
)

## Update one document
db.COLLECTION.updateOne({
    IDENTIFYING_FIELD
}, {
    UPDATE_OPT: {
        UPDATED_FIELD
    }
})
db.movieDetails.updateOne({
    title: "The Martian"
}, {
    $set: {
        poster: "http://ia.media-mbdb.com/images/M/MV5BMTc2MTQ3MDA1Nl5BMl5BanBnXkFtZTgw0DA30TI4NjE@._"
    }
})

## Update man documents (updates all documents that match the filter)
db.COLLECTION.updateMany({
    IDENTIFYING_FIELD
}, {
    UPDATE_OPT: {
        UPDATED_FIELD
    }
})
db.movieDetails.updateMany({
    rated: null
}, {
    $unset: {
        rated: ""
    }
})

#### upserts will update a document if it exists, else it will create the document
db.movieDetails.updateMany({
    "imdb.id: detail.imdb.id
}, {
    $set: detail
}, {
    upsert: true
})


#### Field update operators
$inc         - Increments the value of the field by the specified amount.
$mul         - Multiplies the value of the field by the specified amount.
$rename      - Renames a field.
$setOnInsert - Sets the value of a field if an update results in an insert of a document.
               Has no effect on update operations that modify existing documents.
$set         - Sets the value of a field in a document.
$unset       - Removes the specified field from a document.
$min         - Only updates the field if the specified value is greater than the existing field value.
$max         - Only updates the field if the specified value is less than the eisting field value.
$currentDate - Sets the value of a field to current date, either as a Date or a Timestamp.

... many more (I got lazy. see docs.mongodb.com/manual/reference/operator/update)

## replaceOne replaces an entire document with another document
javascript for doing this:
let filter = {title: "House, M.D., Season Four: New Beginnings"}
let doc = db.movieDetails.findOne(filter);
doc.poster;
doc.poster = "https://www.imdb.com/title/tt1329164/mediaviewer/rm2619416576";
doc.genres;
doc.genres.push("TV Series");
db.movieDetails.replaceOne(filter, doc);

## deleteOne deletes one matched document
db.COLLECTION.deleteOne(IDENTIFIER)
db.reviews.deleteOne({_id: ObjectId("a3fsdf979adshd9f87f9afu98s")})

## deleteMany deletes all matched documents
db.COLLECTION.deleteMany(IDENTIFIER)
db.reviews.deleteMany({reviewer_id: 7989897987})

