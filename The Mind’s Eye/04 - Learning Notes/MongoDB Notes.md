
## 🔧 **1. Basic MongoDB Commands**

|Command|Description|
|---|---|
|`mongo`|Start the MongoDB shell|
|`mongod`|Start the MongoDB server|
|`mongod --dbpath <path>`|Start MongoDB with a specific data directory|
|`exit`|Exit the MongoDB shell|

---

## 📂 **2. Database Operations**

|Command|Description|
|---|---|
|`show dbs`|List all databases|
|`use <dbName>`|Switch to or create a database|
|`db`|Show current database|
|`db.dropDatabase()`|Delete current database|

---

## 📁 **3. Collection Operations**

|Command|Description|
|---|---|
|`show collections`|List all collections in the current DB|
|`db.createCollection("<name>")`|Create a new collection|
|`db.<collection>.drop()`|Drop a collection|

---

## 📝 **4. Document Operations**

### ➕ **Insert Documents**

|Command|Description|
|---|---|
|`db.collection.insertOne({...})`|Insert a single document|
|`db.collection.insertMany([{...}, {...}])`|Insert multiple documents|

### 🔍 **Find/Retrieve Documents**

|Command|Description|
|---|---|
|`db.collection.find()`|Retrieve all documents|
|`db.collection.findOne()`|Retrieve one document|
|`db.collection.find({ field: value })`|Query with filter|
|`db.collection.find().pretty()`|Pretty-print the documents|

### ✏️ **Update Documents**

|Command|Description|
|---|---|
|`db.collection.updateOne({filter}, {$set: {field: value}})`|Update one document|
|`db.collection.updateMany({filter}, {$set: {field: value}})`|Update multiple documents|
|`db.collection.replaceOne({filter}, {newDoc})`|Replace one document completely|

### ❌ **Delete Documents**

|Command|Description|
|---|---|
|`db.collection.deleteOne({filter})`|Delete one document|
|`db.collection.deleteMany({filter})`|Delete multiple documents|

---

## 🧮 **5. Query Operators**

### 🔄 **Comparison Operators**

- `$eq`, `$ne`, `$gt`, `$lt`, `$gte`, `$lte`, `$in`, `$nin`
    

### ⚙️ **Logical Operators**

- `$and`, `$or`, `$not`, `$nor`
    

### 📏 **Element Operators**

- `$exists`, `$type`
    

### 🔁 **Evaluation Operators**

- `$regex`, `$expr`, `$mod`, `$text`, `$where`
    

---

## 🔢 **6. Aggregation**

|Command|Description|
|---|---|
|`db.collection.aggregate([{...}])`|Start an aggregation pipeline|

### Common Stages:

- `$match` – Filter
    
- `$group` – Group data
    
- `$sort` – Sort data
    
- `$project` – Reshape documents
    
- `$limit` / `$skip` – Pagination
    
- `$lookup` – Join collections
    
- `$unwind` – Deconstruct arrays
    

---

## 🔒 **7. Indexes**

|Command|Description|
|---|---|
|`db.collection.createIndex({field: 1})`|Create an index (1: ascending, -1: descending)|
|`db.collection.getIndexes()`|View existing indexes|
|`db.collection.dropIndex({field: 1})`|Drop specific index|

---

## 👤 **8. User Management**

|Command|Description|
|---|---|
|`use admin`|Switch to admin DB|
|`db.createUser({...})`|Create a new user|
|`db.updateUser("username", {...})`|Update user|
|`db.dropUser("username")`|Delete user|
|`db.getUsers()`|List users|

---

## 🧪 **9. Other Useful Commands**

|Command|Description|
|---|---|
|`db.stats()`|Database statistics|
|`db.collection.stats()`|Collection statistics|
|`db.collection.countDocuments({})`|Count documents|
|`db.collection.distinct("field")`|Get unique values for a field|
|`db.collection.find().sort({field: 1})`|Sort results|
|`db.collection.find().limit(n)`|Limit results|
|`db.collection.find().skip(n)`|Skip results|