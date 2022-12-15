# MongoDB

### What is NoSQL

<i>
NoSQL databases (aka "not only SQL") are non-tabular databases and store data differently than relational tables. NoSQL databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and graph. They provide flexible schemas and scale easily with large amounts of data and high user loads.
</i>

#### NoSQL database features

<i>Each NoSQL database has its own unique features. At a high level, many NoSQL databases have the following features:

<ul>
<li>Flexible schemas</li>
<li>Horizontal scaling</li>
<li>Fast queries due to the data model</li>
<li>Ease of use for developers</li>
</ul>
</i>

#### Types of NoSQL databases

<i>Over time, four major types of NoSQL databases emerged: document databases, key-value databases, wide-column stores, and graph databases.

<ul>
<li><b>Document databases</b> store data in documents similar to JSON (JavaScript Object Notation) objects. Each document contains pairs of fields and values. The values can typically be a variety of types including things like strings, numbers, booleans, arrays, or objects.
<li><b>Key-value databases</b> are a simpler type of database where each item contains keys and values.</li>
<li><b>Wide-column stores</b> store data in tables, rows, and dynamic columns.</li>
<li><b>Graph databases</b> store data in nodes and edges. Nodes typically store information about people, places, and things, while edges store information about the relationships between the nodes.</li>
</ul>
</i>

#### Difference between RDBMS and NoSQL databases

<i>
<ul>
<li>Data Modeling</li>
<li>Flexibility of the schema</li>
<li>Scaling technique</li>
<li>Support for transactions</li>
<li>Reliance on data to object mapping</li>
</ul>
</i>

#### Why NoSQL?

<i>NoSQL databases are used in nearly every industry. Use cases range from the highly critical (e.g., storing financial data and healthcare records) to the more fun and frivolous (e.g., storing IoT readings from a smart kitty litter box).

In the following sections, we'll explore when you should choose to use a NoSQL database and common misconceptions about NoSQL databases.
</i>

### When should NoSQL be used?

<i>When deciding which database to use, decision-makers typically find one or more of the following factors lead them to selecting a NoSQL database:

<ul>
<li>Fast-paced Agile development</li>
<li>Storage of structured and semi-structured data</li>
<li>Huge volumes of data</li>
<li>Requirements for scale-out architecture</li>
<li>Modern application paradigms like microservices and real-time streaming</li>
</ul>
</i>

<hr>

### MongoDB

<i>MongoDB is a cross-platform, document oriented database that provides, high performance, high availability, and easy scalability. MongoDB works on concept of collection and document.
</i>

#### Database

<i>Database is a physical container for collections. Each database gets its own set of files on the file system. A single MongoDB server typically has multiple databases.</i>

#### Collection

<i>Collection is a group of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database. Collections do not enforce a schema. Documents within a collection can have different fields. Typically, all documents in a collection are of similar or related purpose.
</i>

#### Document

<i> A document is a set of key-value pairs. Documents have dynamic schema. Dynamic schema means that documents in the same collection do not need to have the same set of fields or structure, and common fields in a collection's documents may hold different types of data.
</i>

The following table shows the relationship of RDBMS terminology with MongoDB.

<table>
<thead><tr><td>RDBMS</td><td>MongoDB</td></tr>
</thead>
<tbody>
<tr>
<td>Database</td><td>Database</td>
</tr>
<tr><td>Table</td><td>Collection</td></tr>
<tr><td>Tuple/Row</td><td>Document</td></tr>
<tr><td>column</td><td>Field</td></tr>
<tr><td>Table Join</td><td>Embedded Documents</td></tr>
<tr><td>Primary Key</td><td>Primary Key (Default key _id provided by MongoDB itself)</td</tr>
</tbody>
</table>

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
... {
... "name": "Max Schwarzmueller",
... "age": 29
... },
... {
... "name": "Manu Lorenz",
... "age": 30
... },
... {
... "name": "Chris Hayton",
... "age": 35
... },
... {
... "name": "Sandeep Kumar",
... "age": 28
... },
... {
... "name": "Maria Jones",
... "age": 30
... },
... {
... "name": "Alexandra Maier",
... "age": 27
... },
... {
... "name": "Dr. Phil Evans",
... "age": 47
... },
... {
... "name": "Sandra Brugge",
... "age": 33
... },
... {
... "name": "Elisabeth Mayr",
... "age": 29
... },
... {
... "name": "Frank Cube",
... "age": 41
... },
... {
... "name": "Karandeep Alun",
... "age": 48
... },
... {
... "name": "Michaela Drayer",
... "age": 39
... },
... {
... "name": "Bernd Hoftstadt",
... "age": 22
... },
... {
... "name": "Scott Tolib",
... "age": 44
... },
... {
... "name": "Freddy Melver",
... "age": 41
... },
... {
... "name": "Alexis Bohed",
... "age": 35
... },
... {
... "name": "Melanie Palace",
... "age": 27
... },
... {
... "name": "Armin Glutch",
... "age": 35
... },
... {
... "name": "Klaus Arber",
... "age": 53
... },
... {
... "name": "Albert Twostone",
... "age": 68
... },
... {
... "name": "Gordon Black",
... "age": 38
... }
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

Projections:
when you need only some of the data of document(like some columns of a table)
db.passengers.find({},{name:1}).toArray();
[
{
_id: ObjectId("6397660eaf5a3885970c3280"),
name: 'Max Schwarzmueller'
},
{ _id: ObjectId("6397660eaf5a3885970c3281"), name: 'Manu Lorenz' },
{ _id: ObjectId("6397660eaf5a3885970c3282"), name: 'Chris Hayton' },
{ _id: ObjectId("6397660eaf5a3885970c3283"), name: 'Sandeep Kumar' },
{ _id: ObjectId("6397660eaf5a3885970c3284"), name: 'Maria Jones' },
{
_id: ObjectId("6397660eaf5a3885970c3285"),
name: 'Alexandra Maier'
},
{ _id: ObjectId("6397660eaf5a3885970c3286"), name: 'Dr. Phil Evans' },
{ _id: ObjectId("6397660eaf5a3885970c3287"), name: 'Sandra Brugge' },
{ _id: ObjectId("6397660eaf5a3885970c3288"), name: 'Elisabeth Mayr' },
{ _id: ObjectId("6397660eaf5a3885970c3289"), name: 'Frank Cube' },
{ _id: ObjectId("6397660eaf5a3885970c328a"), name: 'Karandeep Alun' },
{
_id: ObjectId("6397660eaf5a3885970c328b"),
name: 'Michaela Drayer'
},
{
_id: ObjectId("6397660eaf5a3885970c328c"),
name: 'Bernd Hoftstadt'
},
{ _id: ObjectId("6397660eaf5a3885970c328d"), name: 'Scott Tolib' },
{ _id: ObjectId("6397660eaf5a3885970c328e"), name: 'Freddy Melver' },
{ _id: ObjectId("6397660eaf5a3885970c328f"), name: 'Alexis Bohed' },
{ _id: ObjectId("6397660eaf5a3885970c3290"), name: 'Melanie Palace' },
{ _id: ObjectId("6397660eaf5a3885970c3291"), name: 'Armin Glutch' },
{ _id: ObjectId("6397660eaf5a3885970c3292"), name: 'Klaus Arber' },
{
_id: ObjectId("6397660eaf5a3885970c3293"),
name: 'Albert Twostone'
},
{ _id: ObjectId("6397660eaf5a3885970c3294"), name: 'Gordon Black' }
]

\_id will be by default included in projection but we can exclude it
db.passengers.find({},{name:1, \_id:0}).toArray();
[
{ name: 'Max Schwarzmueller' },
{ name: 'Manu Lorenz' },
{ name: 'Chris Hayton' },
{ name: 'Sandeep Kumar' },
{ name: 'Maria Jones' },
{ name: 'Alexandra Maier' },
{ name: 'Dr. Phil Evans' },
{ name: 'Sandra Brugge' },
{ name: 'Elisabeth Mayr' },
{ name: 'Frank Cube' },
{ name: 'Karandeep Alun' },
{ name: 'Michaela Drayer' },
{ name: 'Bernd Hoftstadt' },
{ name: 'Scott Tolib' },
{ name: 'Freddy Melver' },
{ name: 'Alexis Bohed' },
{ name: 'Melanie Palace' },
{ name: 'Armin Glutch' },
{ name: 'Klaus Arber' },
{ name: 'Albert Twostone' },
{ name: 'Gordon Black' }
]

Embedded Documents:
Nested Documents: One document under another document
Array in Documents:
{
\_id:173,
name: "Rahul",
details: {
age:28,
sex: "Male"
dob: {
day: 22,
month: 12,
year: 1995
}
},
languages: ["English", "Hindi"]
}

Resetting Data:
To get rid of your data, you can simply load the database you want to get rid of (use databaseName) and then execute db.dropDatabase().

Similarly, you could get rid of a single collection in a database via db.myCollection.drop().

---

Schemas and Relations:
