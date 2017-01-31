# mongodb-query

# Information

Membuat query-query di dalam database MongoDB

# Queries

#### 1. Membuat database academic

`use academic`
```
switched to db academic
```

#### 2. Menampilkan semua collection dan data dalam database

`show collections`

```
department
student
```

`db.department.find()`

`db.student.find()`

#### 3. Membuat atau mengaktifkan database

`use academic`
```
switched to db academic
```

#### 4. Membuat collection department

`db.createCollection("department")`
```
{ "ok" : 1 }
```
`db.department.insert({code:"IT",name:"Teknik",major:"Teknik Elektro"})`
```
WriteResult({ "nInserted" : 1 })
```

#### 5. Membuat collection student

`db.createCollection("student")`
```
{ "ok" : 1 }
```

`db.student.insert({
  studentId:"001",
  name:"Fadly Kayo",
  address:"Jakarta",
  department:{
    "$ref": "department",
    "$id" : ObjectId("5890109eaf7b648be41c650e"),
    "$db" : "academic"
    }
})`
```
WriteResult({ "nInserted" : 1 })
```

#### 6. Melihat struktur collection

Department

`var col_list= db.department.findOne();
for (var col in col_list) { print (col) ; }`
```
_id
code
name
major
```

Student

`var col_list= db.student.findOne();
for (var col in col_list) { print (col) ; }`
```
_id
studentId
name
address
department
```

#### 7. Menginputkan 5 data ke dalam collection department

`db.department.insert([
{
  code:"Sipil",
  name:"Teknik",
  major:"Teknik Sipil"
},
{
  code:"DKV",
  name:"Teknik",
  major:"Teknik Design Grafis"
},
{
  code:"Art",
  name:"Design",
  major:"Design Interior"
},
{
  code:"Art",
  name:"Design",
  major:"Mode Design"
},
{
  code:"Dokter",
  name:"Kedokteran",
  major:"Penyakit Dalam"
}
]);`
```
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 5,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
```

#### 8. Menginputkan 3 data ke dalam collection student beserta reference ke department

`db.student.insert([
  {
  studentId:"002",
  name:"Gana",
  address:"Bali",
  department:{
    "$ref": "department",
    "$id" : ObjectId("58901889af7b648be41c6511"),
    "$db" : "academic"
    }
  },
  {
  studentId:"003",
  name:"Iqbal",
  address:"Bandung",
  department:{
    "$ref": "department",
    "$id" : ObjectId("58901889af7b648be41c6511"),
    "$db" : "academic"
    }
  },
  {
  studentId:"004",
  name:"Radit",
  address:"Medan",
  department:{
    "$ref": "department",
    "$id" : ObjectId("58901889af7b648be41c6514"),
    "$db" : "academic"
    }
  }
]);`
```
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 3,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
```

#### 9. Melihat isi collection student

`db.student.find()`
```
{ "_id" : ObjectId("5890135eaf7b648be41c650f"), "studentId" : "001", "name" : "Fadly Kayo", "address" : "Jakarta", "department" : DBRef("department", ObjectId("5890109eaf7b648be41c650e"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6515"), "studentId" : "002", "name" : "Gana", "address" : "Bali", "department" : DBRef("department", ObjectId("58901889af7b648be41c6511"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6516"), "studentId" : "003", "name" : "Iqbal", "address" : "Bandung", "department" : DBRef("department", ObjectId("58901889af7b648be41c6511"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6517"), "studentId" : "004", "name" : "Radit", "address" : "Medan", "department" : DBRef("department", ObjectId("58901889af7b648be41c6514"), "academic") }
```

#### 10. Menampilkan key name dan address dalam collection student

`db.student.find({},{"name":1,"address":1,_id:0})`
```
{ "name" : "Fadly Kayo", "address" : "Jakarta" }
{ "name" : "Gana", "address" : "Bali" }
{ "name" : "Iqbal", "address" : "Bandung" }
{ "name" : "Radit", "address" : "Medan" }
```

#### 11. Menampilkan key studentId, name, dan address dari data student yang mempunyai studentId tertentu

`db.student.find({studentId:"001"},{"studentId":1,"name":1,"address":1,_id:0})
{ "studentId" : "001", "name" : "Fadly Kayo", "address" : "Jakarta" }`
```
{ "studentId" : "001", "name" : "Fadly Kayo", "address" : "Jakarta" }
```

#### 12. Menampilkan semua data student secara urut berdasarkan name dengan sort() ascending dan descending

Ascending

`db.student.find().sort({name:1})`
```
{ "_id" : ObjectId("58901ad5af7b648be41c6517"), "studentId" : "004", "name" : "Alicia", "address" : "Medan", "department" : DBRef("department", ObjectId("58901889af7b648be41c6514"), "academic") }
{ "_id" : ObjectId("5890135eaf7b648be41c650f"), "studentId" : "001", "name" : "Fadly Kayo", "address" : "Jakarta", "department" : DBRef("department", ObjectId("5890109eaf7b648be41c650e"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6515"), "studentId" : "002", "name" : "Gana", "address" : "Bali", "department" : DBRef("department", ObjectId("58901889af7b648be41c6511"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6516"), "studentId" : "003", "name" : "Iqbal", "address" : "Bandung", "department" : DBRef("department", ObjectId("58901889af7b648be41c6511"), "academic") }
```

Descending

`db.student.find().sort({name:-1})`
```
{ "_id" : ObjectId("58901ad5af7b648be41c6516"), "studentId" : "003", "name" : "Iqbal", "address" : "Bandung", "department" : DBRef("department", ObjectId("58901889af7b648be41c6511"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6515"), "studentId" : "002", "name" : "Gana", "address" : "Bali", "department" : DBRef("department", ObjectId("58901889af7b648be41c6511"), "academic") }
{ "_id" : ObjectId("5890135eaf7b648be41c650f"), "studentId" : "001", "name" : "Fadly Kayo", "address" : "Jakarta", "department" : DBRef("department", ObjectId("5890109eaf7b648be41c650e"), "academic") }
{ "_id" : ObjectId("58901ad5af7b648be41c6517"), "studentId" : "004", "name" : "Alicia", "address" : "Medan", "department" : DBRef("department", ObjectId("58901889af7b648be41c6514"), "academic") }
```

#### 13. Menampilkan semua data department secara urut berdasarkan name secara ascending dan descending

Ascending

`db.department.find().sort({name:1})`
```
{ "_id" : ObjectId("58901889af7b648be41c6512"), "code" : "Art", "name" : "Design", "major" : "Design Interior" }
{ "_id" : ObjectId("58901889af7b648be41c6513"), "code" : "Art", "name" : "Design", "major" : "Mode Design" }
{ "_id" : ObjectId("58901889af7b648be41c6514"), "code" : "Dokter", "name" : "Kedokteran", "major" : "Penyakit Dalam" }
{ "_id" : ObjectId("5890109eaf7b648be41c650e"), "code" : "IT", "name" : "Teknik", "major" : "Teknik Elektro" }
{ "_id" : ObjectId("58901889af7b648be41c6510"), "code" : "Sipil", "name" : "Teknik", "major" : "Teknik Sipil" }
{ "_id" : ObjectId("58901889af7b648be41c6511"), "code" : "DKV", "name" : "Teknik", "major" : "Teknik Design Grafis" }
```

Descending

`db.student.find().sort({name:-1})`
```
{ "_id" : ObjectId("5890109eaf7b648be41c650e"), "code" : "IT", "name" : "Teknik", "major" : "Teknik Elektro" }
{ "_id" : ObjectId("58901889af7b648be41c6510"), "code" : "Sipil", "name" : "Teknik", "major" : "Teknik Sipil" }
{ "_id" : ObjectId("58901889af7b648be41c6511"), "code" : "DKV", "name" : "Teknik", "major" : "Teknik Design Grafis" }
{ "_id" : ObjectId("58901889af7b648be41c6514"), "code" : "Dokter", "name" : "Kedokteran", "major" : "Penyakit Dalam" }
{ "_id" : ObjectId("58901889af7b648be41c6512"), "code" : "Art", "name" : "Design", "major" : "Design Interior" }
{ "_id" : ObjectId("58901889af7b648be41c6513"), "code" : "Art", "name" : "Design", "major" : "Mode Design" }
```

#### 14. Mencari data student dengan name

`db.student.find({name:"Fadly Kayo"})`
```
{ "_id" : ObjectId("5890135eaf7b648be41c650f"), "studentId" : "001", "name" : "Fadly Kayo", "address" : "Jakarta", "department" : DBRef("department", ObjectId("5890109eaf7b648be41c650e"), "academic") }
```

# Usage

```
brew install mongodb
brew cask install lunchy
cp /usr/local/Cellar/mongodb/*/homebrew.mxcl.mongodb.plist ~/Library/LaunchAgents/
lunchy start mongodb
mongo

```
