
// mongod --fork --logpath /Users/prototypeadmin/Databases/mongo/mongodb.log --dbpath /Users/prototypeadmin/Databases/mongo

/// These are the steps

[Converts Excel to JSON](http://shancarter.github.io/mr-data-converter/)

NOTE: Import Statement doesn't like [ ] brackets at start/end of json file.
Zipcodes must be surrounded by quotes


mongoimport --host dotcomwiki.directv.com --db promiseDB --collection citadel521 --file citadel521.json
mongoimport --host dotcomwiki.directv.com --db promiseDB --collection citadel722 --file citadel722.json

mongo dotcomwiki.directv.com
use promiseDB


db.citadel722.find().forEach(function (data) { 
  db.disputes_locals.update( 
    { ZipCode: data.Zip , "Cty Name" : data.CtyName },
    { $set: { "Cty Name" : data.CtyName,
              "County" : data.CtyName,
              "State" : data.State }
    },
    { upsert: true } 
  )
});

68944

db.citadel722.find().forEach(function (data) { 
  db.disputes_locals.update( 
    { ZipCode: data.Zip , "Cty Name" : data.CtyName },
    { $addToSet: { "disputes" : "citadel722" } },

    { upsert: true } 
  )
});

02831

db.citadel521.find().forEach(function (data) { 
  db.disputes_locals.update( 
    { ZipCode: data.Zip , "Cty Name" : data.CtyName },
    { $set: { "ZipCode": data.Zip,
              "Cty Name" : data.CtyName,
              "County" : data.CtyName,
              "State" : data.State }
    },
    { upsert: true } 
  )
});


db.citadel521.find().forEach(function (data) { 
  db.disputes_locals.update( 
    { ZipCode: data.Zip , "Cty Name" : data.CtyName },
    { $addToSet: { "disputes" : "citadel521" } },

    { upsert: true } 
  )
});

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.with.citadel.Oct04.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131  -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals  --file disputes.locals.with.citadel.Oct04.json

//////////////////////////



http://directv-presscenter.nodejitsu.com/


mongo paulo.mongohq.com:10006/nodejitsudb9988487632
db.auth('nodejitsu', 'e60cfaeca9d1feaa622974af3320d494')


mongo paulo.mongohq.com:10006/nodejitsudb9988487632 -u nodejitsu -p e60cfaeca9d1feaa622974af3320d494
mongoimport --host paulo.mongohq.com:10006 --db nodejitsudb9988487632  -u nodejitsu -p e60cfaeca9d1feaa622974af3320d494 --collection users  --file presscenter.json

db.users.find({"_id": "cmbrugnoli@directv.com"})
db.users.find({"admin" :1 })
db.users.update({"_id": "cmbrugnoli@directv.com"}, {$set: {"admin":1}})

show collections
db.users.find()
db.users.update( { _id: "lszentmiklosy@directv.com" },
                 {
                   $set: { active: 1 }
                 } )




mongo dotcomwiki.directv.com
show dbs
use presscenter





db.disputes.find( { "disputes" : { $exists : true} } )
db.disputes.distinct(  "disputes" )

Promise:

mongo linus.mongohq.com:10015/nodejitsudb1061732131
db.auth('nodejitsu', 'a697799f4eb5aed374e913dcf787e54c')
OR
mongo linus.mongohq.com:10015/nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c


These are run from Command line, not while in Mongo:
mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131  -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals  --out disputes_locals.json

mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131  -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes  --out disputes_sports.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes --file disputes_sports.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection citadel --file citadelzips.json





show collections
// disputes = sports
// disputes_locals = locals

Upsert = Update, Insert New if doesn't exist


//WORKS 
db.citadel.find().forEach(function (data) { 
  db.disputes_locals.update( 
    { ZipCode: data.Zip},
    { $set: { "disputes" : "citadel"}},
    { upsert: true } 
  )
});


//HOORAY WORKS TOO
db.citadel.find().forEach(function (data) { 
  db.disputes_locals.update( 
    { ZipCode: data.Zip},
    { $set: { "disputes" : "citadel",
              "Cty Name" : data.CtyName,
              "County" : data.CtyName,
              "State" : data.State }
    },
    { upsert: true } 
  )
});





db.citadel.find().forEach(function (data) { 
  print (data."Cty Name");
});


db.disputes_locals.update( 
    { ZipCode: 52802 },
    { $set: { "disputes" : "citadel"}},
    { upsert: true } 
  )

db.disputes_locals.find( { "disputes" : "citadel" } )
db.disputes_local.find( { "disputes" : { $exists : true} } )


db.disputes_locals.find({ "disputes" : "yumaAZ"})


db.disputes_locals.remove ( { "disputes" : "citadel"} )


db.disputes_locals.remove ( { "disputes" : "citadel"} )

db.oldcollection.drop() //deletes collection

db.currentName.renameCollection("NewName")


db.yumaAZ.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip , "Cty Name" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State }
           },
           { upsert: true }
  )
});

db.yumaAZ.find().forEach(function (data) {
  db.disputes_locals.update(
    { ZipCode: data.Zip , "Cty Name" : data.CtyName },
    { $addToSet: { "disputes" : "yumaAZ" } },
    { upsert: true }
  )
});


mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.withNPG.Oct7.json


mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.withNPG.Oct7.json


db.disputes_locals.find( { "_id" : "ObjectId('524ee5d6bbd9e4f96a8885e0')" }

db.disputes_locals.find( { _id : ObjectId('524ee5d6bbd9e4f96a8885e4') } )


bendOR
citadel521
citadel722
columbiaMO
disputes
disputes_10072013
disputes_locals
disputes_locals_10072013
elpasoTX
idahofalls
palmspringsCA
santabarbraCA
springsCO
stjosephMO
system.indexes
yumaAZ


//Remove A dispute
db.disputes_11_4_2013.find({ "disputes" : "longhorn-network"});
db.disputes_11_4_2013.update({ "disputes" : "longhorn-network"}, { $pull: { "disputes" : "longhorn-network"} }, {multi: true});

db.disputes_locals_11_4_2013.find({"disputes" : "bendOR"});
db.disputes_locals_11_4_2013.update({ "disputes" : "bendOR"}, { $pull: { "disputes" : "bendOR"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "columbiaMO"}, { $pull: { "disputes" : "columbiaMO"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "elpasoTX"}, { $pull: { "disputes" : "elpasoTX"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "idahofalls"}, { $pull: { "disputes" : "idahofalls"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "palmspringsCA"}, { $pull: { "disputes" : "palmspringsCA"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "santabarbraCA"}, { $pull: { "disputes" : "santabarbraCA"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "springsCO"}, { $pull: { "disputes" : "springsCO"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "stjosephMO"}, { $pull: { "disputes" : "stjosephMO"} }, {multi: true});
db.disputes_locals_11_4_2013.update({ "disputes" : "yumaAZ"}, { $pull: { "disputes" : "yumaAZ"} }, {multi: true});

//How to remove if Disputes is empty?
db.disputes_11_4_2013.find({"disputes" : {$size : 0}})
db.disputes_11_4_2013.count({"disputes" : {$size : 0}})
db.disputes_11_4_2013.remove({"disputes" : {$size : 0}})


db.disputes_locals_11_4_2013.find({"disputes" : {$size : 0}})
db.disputes_locals_11_4_2013.count({"disputes" : {$size : 0}})
db.disputes_locals_11_4_2013.remove({"disputes" : {$size : 0}})


mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals_11_4_2013 --out locals_removed_NPG.json

//Add --drop to replace current
mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --file locals_removed_NPG.json --drop


mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_11_4_2013 --out sports_removed_longhorn.json
mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes --file sports_removed_longhorn.json --drop


mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c  --collection disputes_locals --file locals_removed_NPG.json --drop

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c  --collection disputes --file sports_removed_longhorn.json --drop


//db.weatherdata.find({"Wind Direction" : { $gt: 180 }})
db.weatherdata.find({"Wind Direction" : { $gt: 180, $lt :360 } })
db.weatherdata.find( { "Wind Direction" : { $gt: 180, $lt :360 }}).sort({"Temperature" : 1} )
[ "Vermont", "California", "Florida", "New Mexico" ]





//Vermont
db.weatherdata.find({"State" : "Vermont"}).sort({ "Temperature" : -1}).pretty()
db.weatherdata.findOne({ "_id" : ObjectId("52780440bf635f7869bfec5c") })
db.weatherdata.update({ "_id" : ObjectId("52780440bf635f7869bfec5c") }, { $set : {"month_high" : true }})

//California
db.weatherdata.find({"State" : "California"}).sort({ "Temperature" : -1}).limit(2).pretty()
ObjectId("52780440bf635f7869bfee1f")
db.weatherdata.update({ "_id" : ObjectId("52780440bf635f7869bfee1f") }, { $set : {"month_high" : true }})


//Florida
db.weatherdata.find({"State" : "Florida"}).sort({ "Temperature" : -1}).limit(2).pretty()
ObjectId("52780440bf635f7869bff0bc")
db.weatherdata.update({ "_id" : ObjectId("52780440bf635f7869bff0bc") }, { $set : {"month_high" : true }})


ObjectId("52780440bf635f7869bff3e5"
db.weatherdata.update({ "_id" : ObjectId("52780440bf635f7869bff3e5") }, { $set : {"month_high" : true }})



//When to Denormalize
1 to 1 - Embed the data 
1 to Few - Embed 
1 to Many  - Link 
Many to Many - Link 

//Indexes

db.collection.ensureIndex({ fieldName: 1});
db.collection.ensureIndex({ fieldName: 1}, { unique : true });
db.collection.ensureIndex({ fieldName: 1}, { sparse : 1 });

db.collection.dropIndex({ fieldName: 1});

db.collection.find({a : 1}).explain() // shows details about the search. cursor, multikey, index, time

multikey means arrays?


compound indexes

d, c, b, a
d yes
dc yes
db yes, only d
cb x

find, findeOne, Update, Remove all use Index

db.students.stats()
db.students.totalIndexSize()


//2d xy lookups
db.collection.find({ location: $near [x,y]});

3d geospatial distances in Radians
distiance in meters / radius of earth = radians.

ensureIndex{ Location: '2d'} (evne for 3d geospatial, 2d)
longitutde, latitude

// Need to use collection in geoNear because collection is not set.
// collection needs to have a 2d index
db.runCommand({ geoNear: 'collection', near: [long,lat], spherical: true, maxDistance: 1})


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals  --out disputes_locals_11_9_13.json

mongoimport --host dotcomwiki.directv.com --db promiseDB  --collection disputes_locals --file disputes_locals_11_9_13.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection gormally --file Gormally.json

db.gormally.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip , "Cty Name" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State }
           },
           { upsert: true }
  )
});



mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes_locals_gormally_11_19_13.json


mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c  --collection disputes_locals --file disputes_locals_gormally_11_19_13.json --drop


mongoimport --host dotcomwiki.directv.com --db presscenter --collection users --file presscenter.json


//Remove a Dispute. SHOULD HAVE USED PULL NOT REMOVE.
mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131  -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes  --out disputes_sports_with_pac12_Jan72014.json
mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_sports_with_pac12_Jan72014 --file disputes_sports_with_pac12_Jan72014.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection takeDownPac12 --file takeDownPac12.json
db.takeDownPac12.find().forEach(function (data) {
  db.disputes.remove({ ZipCode: data.Zip , "Cty Name" : data.CtyName })
});
mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes --out disputes_without_Pac12_Jan72014.json
mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes --file disputes_without_Pac12_Jan72014.json --drop

 

//Louisiana
mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131  -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals  --out disputes_locals_without_LA_Jan21.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection batonrougev1 --file batonrougev1.json


db.batonrougev1.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip , "CityName" : data.CityName },
   { $set: { "County" : data.CityName,
             "State" : data.State }
           },
           { upsert: true }
  )
});


db.batonrougev1.find().forEach(function (data) {
  db.disputes_locals.update(
    { ZipCode: data.Zip , "CityName" : data.CityName },
    { $addToSet: { "disputes" : "batonrougev1" } },
    { upsert: true }
  )
});


mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Jan21.With.BatonRougev1.json


mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Jan21.With.BatonRougev1.json --drop

//v2
mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131  -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals  --out disputes_locals_with_only_v1.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection batonrougev2 --file batonrougev2.json


db.batonrougev2.find().forEach(function (data) {
  db.disputes_locals.update(
    { ZipCode: data.Zip , "CityName" : data.CityName },
    { $pull: { "disputes" : "batonrougev1" } }
  )
});


mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Jan21.With.BatonRougev2.json


mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Jan21.With.BatonRougev2.json --drop


db.disputes_locals.find({"disputes" : "batonrougev2"}).forEach(function (data) {
  db.disputes_locals.update(
    { ZipCode: data.Zip , "CityName" : data.CityName },
    { $addToSet: { "disputes" : "batonrougevtwo" } },
  )
});



mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c  --collection disputes_locals  --out disputes_locals_Feb102014.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes_locals_Feb102014.json --drop


mongoimport --host dotcomwiki.directv.com --db promiseDB --collection toledo --file toledo.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection erie --file erie.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection flint --file flint.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection elmira --file elmira.json

db.elmira.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip , "Cty Name" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "elmira" }
           },
           { upsert: true }
  )
});

db.elmira.find().forEach(function (data) {
  db.disputes_locals.update(
    { ZipCode: data.Zip , "Cty Name" : data.CtyName },
    { $addToSet: { "disputes" : "elmira" } },
    { upsert: true }
  )
});

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Feb102014.withUpdates.json


mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Feb102014.withUpdates.json --drop


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.feb142014.withBatonRouge.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.feb142014.withBatonRouge.json


db.disputes_locals.remove({ "disputes" : "batonrougev1"});
 {multi: true});

db.disputes_locals.remove({ "disputes" : "batonrougev2"});

, { $pull: { "disputes" : "batonrougev2"} }, {multi: true});


// Sports Net LA

mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_sports --out disputes.sports.feb142014.withOutSportsLA.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_sports  --file disputes.sports.feb142014.withOutSportsLA.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection sportsNetLA --file sportsnetla.json


db.sportsNetLA.find().forEach(function (data) {
  db.disputes_sports.update(
   { ZipCode: data.ZIP, "County" : data.COUNTY },
   { $set: { "County" : data.COUNTY,
             "State" : data.STATE },
    $addToSet: { "disputes" : "sportsnet-la" }
           },
           { upsert: true }
  )
});

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_sports --out disputes.sports.Feb252014.withSportsNetLA.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_sports --file disputes.sports.Feb252014.withSportsNetLA.json --drop

// KOMU

mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.Apr82014.withOutKomu.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.Apr82014.withOutKomu.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection komu --file komu.json

db.komu.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip, "County" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "komu" }
           },
           { upsert: true }
  )
});

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Apr82014.withKomu.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Apr82014.withKomu.json --drop

//Marquee

mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.Apr282014.withOutMarquee.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.Apr282014.withOutMarquee.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection marquee --file marquee.json


db.marquee.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip, "County" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "marquee" }
           },
           { upsert: true }
  )
});

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Apr282014.withMarquee.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Apr282014.withMarquee.json --drop








/////////// REMOVING DISPUTES
flint
48417


toledo
43402

////////////
mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.June18.WITH.Marquee.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.May2.withFlintToledo.json --drop

db.disputes_locals.update({ "disputes" : "flint"}, { $pull: { "disputes" : "flint"} }, {multi: true});

db.disputes_locals.update({ "disputes" : "toledo"}, { $pull: { "disputes" : "toledo"} }, {multi: true});

db.disputes_locals.find({"disputes" : {$size : 0}})
db.disputes_locals.remove({"disputes" : {$size : 0}})


mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.June18.Without.Marquee.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.June18.Without.Marquee.json --drop


db.disputes_locals.find({"disputes" : "marquee" })

db.disputes_locals.update({ "disputes" : "marquee"}, { $pull: { "disputes" : "marquee"} }, {multi: true});
db.disputes_locals.find({"disputes" : {$size : 0}})
db.disputes_locals.remove({"disputes" : {$size : 0}})

////////////

mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.June23.WITH.KOMU.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.June23.WITH.KOMU.json --drop

db.disputes_locals.find({"disputes" : "komu" })

db.disputes_locals.update({ "disputes" : "komu"}, { $pull: { "disputes" : "komu"} }, {multi: true});
db.disputes_locals.find({"disputes" : {$size : 0}})
db.disputes_locals.remove({"disputes" : {$size : 0}})

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.June23.Without.KOMU.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals  --file disputes.locals.June23.Without.KOMU.json --drop

mongo --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals 



// Import WBOC


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.July15.withOutWBOC.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.July15.withOutWBOC.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection wboc --file wboc.json --drop

mongo dotcomwiki.directv.com

use promiseDB


db.wboc.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip, "County" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "wboc" }
           },
           { upsert: true }
  )
});

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.July15.withWBOC.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.July15.withWBOC.json --drop


// Remove WBOC

19930


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.Aug1.WITH.WBOC.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.Aug1.WITH.WBOC.json --drop

mongo dotcomwiki.directv.com

use promiseDB

db.disputes_locals.update({ "disputes" : "wboc"}, { $pull: { "disputes" : "wboc"} }, {multi: true});

db.disputes_locals.count()
db.disputes_locals.find({"disputes" : {$size : 0}})
db.disputes_locals.remove({"disputes" : {$size : 0}})
db.disputes_locals.count()

exit Mongo

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Aug1.Without.WBOC.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Aug1.Without.WBOC.json --drop



// Import Raycom


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.aug14.withoutraycom.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.aug14.withoutraycom.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection raycom --file raycom.json --drop

mongo dotcomwiki.directv.com

use promiseDB


db.raycom.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip, "County" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "raycom-" + data.DTVDMANAME  }
           },
           { upsert: true }
  )
});

db.disputes_locals.distinct("disputes")

exit 

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.aug18.withraycom.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.aug18.withraycom.json --drop



// Import Dispatch


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.aug21.withoutdispatch.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.aug21.withoutdispatch.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection dispatch --file dispatch.json --drop

mongo dotcomwiki.directv.com

use promiseDB


db.dispatch.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip, "County" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "dispatch"  }
           },
           { upsert: true }
  )
});

db.disputes_locals.distinct("disputes")

exit 

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.aug21.withdispatch.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.aug21.withdispatch.json --drop


// Update Dispatch

mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.sep2.withoutUpdateddispatch.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.sep2.withoutUpdateddispatch.json --drop

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection dispatch --file newdispatch.json --drop

mongo dotcomwiki.directv.com

use promiseDB

db.disputes_locals.update({ "disputes" : "dispatch"}, { $pull: { "disputes" : "dispatch"} }, {multi: true});

db.disputes_locals.count()
db.disputes_locals.find({"disputes" : {$size : 0}})
db.disputes_locals.remove({"disputes" : {$size : 0}})
db.disputes_locals.count()


db.dispatch.find().forEach(function (data) {
  db.disputes_locals.update(
   { ZipCode: data.Zip, "County" : data.CtyName },
   { $set: { "County" : data.CtyName,
             "State" : data.State },
    $addToSet: { "disputes" : "dispatch-" + data.DTVDMANAME""  }
           },
           { upsert: true }
  )
});

db.disputes_locals.distinct("disputes")

exit 

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.sept2.updateddispatch.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.sept2.updateddispatch.json --drop


// Remove citadel722

69046


mongoexport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --out disputes.locals.Sept10.Cleanup.json

mongoimport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals  --file disputes.locals.Sept10.Cleanup.json --drop

mongo dotcomwiki.directv.com

use promiseDB

db.disputes_locals.update({ "disputes" : "citadel722"}, { $pull: { "disputes" : "citadel722"} }, {multi: true});

db.disputes_locals.update({ "disputes" : "citadel521"}, { $pull: { "disputes" : "citadel521"} }, {multi: true});

db.disputes_locals.update({ "disputes" : "gormally"}, { $pull: { "disputes" : "gormally"} }, {multi: true});

db.disputes_locals.update({ "disputes" : "erie"}, { $pull: { "disputes" : "erie"} }, {multi: true});

db.disputes_locals.update({ "disputes" : "elmira"}, { $pull: { "disputes" : "elmira"} }, {multi: true});



db.disputes_locals.count()
db.disputes_locals.find({"disputes" : {$size : 0}}).count()
db.disputes_locals.remove({"disputes" : {$size : 0}})
db.disputes_locals.count()

exit Mongo

mongoexport --host dotcomwiki.directv.com --db promiseDB --collection disputes_locals --out disputes.locals.Sept10.Cleaned.json

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c --collection disputes_locals --file disputes.locals.Sept10.Cleaned.json --drop

//Sports!

mongoimport --host dotcomwiki.directv.com --db promiseDB  --collection sportstest --file teams.json --drop

mongoimport --host linus.mongohq.com:10015 --db nodejitsudb1061732131 -u nodejitsu -p a697799f4eb5aed374e913dcf787e54c  --collection sportstest --file teams.json --drop



