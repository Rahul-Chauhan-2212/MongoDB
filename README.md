# MongoDB

showdbs --- to show all databases

use databaseName --- to use a particular database it even works if database is not there but databse will be created only when we start entering data in database

db.flightData.insertOne({"name":"Rahul Chauhan", "salary":10000})
{
acknowledged: true,
insertedId: ObjectId("63975c4faf5a3885970c327b")
}

MongoDB CRUD
1)Create
insertOne(data, options)
insertMany(data, options)
2)Read
find()
find(filter, options)
findOne(filter, options)
3)Update
updateOne(filter, data, options)
updateMany(filter, data, options)
replaceOne(filter, data, options)
4)Delete
deleteOne(filter, options)
deleteMany(filter, options)

db.flightData.find().pretty()

InsertMany:

db.flightData.insertMany([
{
"departureAirport": "MUC",
"arrivalAirport": "SFO",
"aircraft": "Airbus A380",
"distance": 12000,
"intercontinental": true
},
{
"departureAirport": "LHR",
"arrivalAirport": "TXL",
"aircraft": "Airbus A320",
"distance": 950,
"intercontinental": false
}
])

{
acknowledged: true,
insertedIds: {
'0': ObjectId("63975e93af5a3885970c327c"),
'1': ObjectId("63975e93af5a3885970c327d")
}
}

Update One:
db.flightData.updateOne({distance: 12000}, {$set: {marker:"delete"}})
{
acknowledged: true,
insertedId: null,
matchedCount: 1,
modifiedCount: 1,
upsertedCount: 0
}

[
{
_id: ObjectId("63975e93af5a3885970c327c"),
departureAirport: 'MUC',
arrivalAirport: 'SFO',
aircraft: 'Airbus A380',
distance: 12000,
intercontinental: true,
marker: 'delete'
},
{
_id: ObjectId("63975e93af5a3885970c327d"),
departureAirport: 'LHR',
arrivalAirport: 'TXL',
aircraft: 'Airbus A320',
distance: 950,
intercontinental: false
}
]

Update Many:
db.flightData.updateMany({}, {$set: {marker:"toDelete"}})
{
acknowledged: true,
insertedId: null,
matchedCount: 2,
modifiedCount: 2,
upsertedCount: 0
}
[
{
_id: ObjectId("63975e93af5a3885970c327c"),
departureAirport: 'MUC',
arrivalAirport: 'SFO',
aircraft: 'Airbus A380',
distance: 12000,
intercontinental: true,
marker: 'toDelete'
},
{
_id: ObjectId("63975e93af5a3885970c327d"),
departureAirport: 'LHR',
arrivalAirport: 'TXL',
aircraft: 'Airbus A320',
distance: 950,
intercontinental: false,
marker: 'toDelete'
}
]

Insert one:
db.flightData.insertOne({\_id:373, departureAirport: 'NDLI', arrivalAirport: 'MUM', marker: 'toDelete'})
{ acknowledged: true, insertedId: 373 }

[
{
_id: ObjectId("63975e93af5a3885970c327c"),
departureAirport: 'MUC',
arrivalAirport: 'SFO',
aircraft: 'Airbus A380',
distance: 12000,
intercontinental: true,
marker: 'toDelete'
},
{
_id: ObjectId("63975e93af5a3885970c327d"),
departureAirport: 'LHR',
arrivalAirport: 'TXL',
aircraft: 'Airbus A320',
distance: 950,
intercontinental: false,
marker: 'toDelete'
},
{
_id: 373,
departureAirport: 'NDLI',
arrivalAirport: 'MUM',
marker: 'toDelete'
}
]

Delete One:
db.flightData.deleteOne({distance:950})
{ acknowledged: true, deletedCount: 1 }

[
{
_id: ObjectId("63975e93af5a3885970c327c"),
departureAirport: 'MUC',
arrivalAirport: 'SFO',
aircraft: 'Airbus A380',
distance: 12000,
intercontinental: true,
marker: 'toDelete'
},
{
_id: 373,
departureAirport: 'NDLI',
arrivalAirport: 'MUM',
marker: 'toDelete'
}
]

Delete Many:

db.flightData.deleteMany({marker:'toDelete'})
{ acknowledged: true, deletedCount: 2 }

Find:

db.flightData.find({distance: {$gt : 1000}})
[
{
_id: ObjectId("639762a8af5a3885970c327e"),
departureAirport: 'MUC',
arrivalAirport: 'SFO',
aircraft: 'Airbus A380',
distance: 12000,
intercontinental: true
}
]

$set, $gt are called atomic operators

update vs updateMany

db.flightData.updateOne({\_id: ObjectId("639762a8af5a3885970c327e")}, {$set:{delayed:true}})
{
acknowledged: true,
insertedId: null,
matchedCount: 1,
modifiedCount: 1,
upsertedCount: 0
}

db.flightData.update({ \_id: ObjectId("639762a8af5a3885970c327e") }, { $set: { delayed: true } })
DeprecationWarning: Collection.update() is deprecated. Use updateOne, updateMany, or bulkWrite.
{
acknowledged: true,
insertedId: null,
matchedCount: 1,
modifiedCount: 0,
upsertedCount: 0
}

db.flightData.update({ \_id: ObjectId("639762a8af5a3885970c327e") }, { $set: { delayed: false } })
{
acknowledged: true,
insertedId: null,
matchedCount: 1,
modifiedCount: 1,
upsertedCount: 0
}

db.flightData.find().pretty()
[
{
_id: ObjectId("639762a8af5a3885970c327e"),
departureAirport: 'MUC',
arrivalAirport: 'SFO',
aircraft: 'Airbus A380',
distance: 12000,
intercontinental: true,
delayed: false
},
{
_id: ObjectId("639762a8af5a3885970c327f"),
departureAirport: 'LHR',
arrivalAirport: 'TXL',
aircraft: 'Airbus A320',
distance: 950,
intercontinental: false
}
]

db.flightData.update({ \_id: ObjectId("639762a8af5a3885970c327e") }, { delayed: false })
This works in Older Mongo Version but in Mongo 6 you will get below error
MongoInvalidArgumentError: Update document requires atomic operators
update in lower mongo version don't require atomic operator and this will result in creation of new data.
In newer versions, replaceOne is the alternative of update


 db.passengers.insertMany([
...   {
...     "name": "Max Schwarzmueller",
...     "age": 29
...   },
...   {
...     "name": "Manu Lorenz",
...     "age": 30
...   },
...   {
...     "name": "Chris Hayton",
...     "age": 35
...   },
...   {
...     "name": "Sandeep Kumar",
...     "age": 28
...   },
...   {
...     "name": "Maria Jones",
...     "age": 30
...   },
...   {
...     "name": "Alexandra Maier",
...     "age": 27
...   },
...   {
...     "name": "Dr. Phil Evans",
...     "age": 47
...   },
...   {
...     "name": "Sandra Brugge",
...     "age": 33
...   },
...   {
...     "name": "Elisabeth Mayr",
...     "age": 29
...   },
...   {
...     "name": "Frank Cube",
...     "age": 41
...   },
...   {
...     "name": "Karandeep Alun",
...     "age": 48
...   },
...   {
...     "name": "Michaela Drayer",
...     "age": 39
...   },
...   {
...     "name": "Bernd Hoftstadt",
...     "age": 22
...   },
...   {
...     "name": "Scott Tolib",
...     "age": 44
...   },
...   {
...     "name": "Freddy Melver",
...     "age": 41
...   },
...   {
...     "name": "Alexis Bohed",
...     "age": 35
...   },
...   {
...     "name": "Melanie Palace",
...     "age": 27
...   },
...   {
...     "name": "Armin Glutch",
...     "age": 35
...   },
...   {
...     "name": "Klaus Arber",
...     "age": 53
...   },
...   {
...     "name": "Albert Twostone",
...     "age": 68
...   },
...   {
...     "name": "Gordon Black",
...     "age": 38
...   }
... ]
... )
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("6397660eaf5a3885970c3280"),
    '1': ObjectId("6397660eaf5a3885970c3281"),
    '2': ObjectId("6397660eaf5a3885970c3282"),
    '3': ObjectId("6397660eaf5a3885970c3283"),
    '4': ObjectId("6397660eaf5a3885970c3284"),
    '5': ObjectId("6397660eaf5a3885970c3285"),
    '6': ObjectId("6397660eaf5a3885970c3286"),
    '7': ObjectId("6397660eaf5a3885970c3287"),
    '8': ObjectId("6397660eaf5a3885970c3288"),
    '9': ObjectId("6397660eaf5a3885970c3289"),
    '10': ObjectId("6397660eaf5a3885970c328a"),
    '11': ObjectId("6397660eaf5a3885970c328b"),
    '12': ObjectId("6397660eaf5a3885970c328c"),
    '13': ObjectId("6397660eaf5a3885970c328d"),
    '14': ObjectId("6397660eaf5a3885970c328e"),
    '15': ObjectId("6397660eaf5a3885970c328f"),
    '16': ObjectId("6397660eaf5a3885970c3290"),
    '17': ObjectId("6397660eaf5a3885970c3291"),
    '18': ObjectId("6397660eaf5a3885970c3292"),
    '19': ObjectId("6397660eaf5a3885970c3293"),
    '20': ObjectId("6397660eaf5a3885970c3294")
  }
}

db.passengers.find()
[
  {
    _id: ObjectId("6397660eaf5a3885970c3280"),
    name: 'Max Schwarzmueller',
    age: 29
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3281"),
    name: 'Manu Lorenz',
    age: 30
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3282"),
    name: 'Chris Hayton',
    age: 35
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3283"),
    name: 'Sandeep Kumar',
    age: 28
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3284"),
    name: 'Maria Jones',
    age: 30
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3285"),
    name: 'Alexandra Maier',
    age: 27
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3286"),
    name: 'Dr. Phil Evans',
    age: 47
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3287"),
    name: 'Sandra Brugge',
    age: 33
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3288"),
    name: 'Elisabeth Mayr',
    age: 29
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3289"),
    name: 'Frank Cube',
    age: 41
  },
  {
    _id: ObjectId("6397660eaf5a3885970c328a"),
    name: 'Karandeep Alun',
    age: 48
  },
  {
    _id: ObjectId("6397660eaf5a3885970c328b"),
    name: 'Michaela Drayer',
    age: 39
  },
  {
    _id: ObjectId("6397660eaf5a3885970c328c"),
    name: 'Bernd Hoftstadt',
    age: 22
  },
  {
    _id: ObjectId("6397660eaf5a3885970c328d"),
    name: 'Scott Tolib',
    age: 44
  },
  {
    _id: ObjectId("6397660eaf5a3885970c328e"),
    name: 'Freddy Melver',
    age: 41
  },
  {
    _id: ObjectId("6397660eaf5a3885970c328f"),
    name: 'Alexis Bohed',
    age: 35
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3290"),
    name: 'Melanie Palace',
    age: 27
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3291"),
    name: 'Armin Glutch',
    age: 35
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3292"),
    name: 'Klaus Arber',
    age: 53
  },
  {
    _id: ObjectId("6397660eaf5a3885970c3293"),
    name: 'Albert Twostone',
    age: 68
  }
]
Type "it" for more

find gives a cursor object used to cycle through results
mongodb shell gives first 20 results

 db.passengers.find().forEach((passengerData) => {printjson(passengerData)})
