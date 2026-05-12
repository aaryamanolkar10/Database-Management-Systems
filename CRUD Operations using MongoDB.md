# CRUD Operations using MongoDB

## Aim
To perform CRUD (Create, Read, Update, Delete) operations using MongoDB.

---

# Problem Statement
Design and implement CRUD operations using MongoDB using:
- save()
- find()
- updateMany()
- deleteMany()
- renameCollection()
- Logical Operators
- Regular Expressions

---

# Software Required
- MongoDB
- Mongo Shell (mongosh)

---

# Step 1: Create and Use Database

```javascript
use Employee
```

---

# Step 2: Create Collection

```javascript
db.createCollection("emp1")
```

---

# Step 3: Insert Documents

```javascript
db.emp1.insertMany([
{
    eno: 101,
    ename: "Nikhil",
    address: "Pune",
    sal: 12000
},
{
    eno: 102,
    ename: "Amit",
    address: "Mumbai",
    sal: 4000
},
{
    eno: 103,
    ename: "Neha",
    address: "Nashik",
    sal: 18000
},
{
    eno: 104,
    ename: "Rohit",
    address: "Delhi",
    sal: 9000
},
{
    eno: 105,
    ename: "Nitin",
    address: "Chennai",
    sal: 22000
}
])
```

---

# Step 4: Display All Documents

```javascript
db.emp1.find()
```

---

# Step 5: Insert Document Using Custom ObjectId

```javascript
db.emp1.insertOne({
    _id: ObjectId("661111111111111111111111"),
    eno: 106,
    ename: "Nayana",
    address: "Bangalore",
    sal: 15000
})
```

---

# Step 6: Display Employees Having Salary Greater Than 5000

```javascript
db.emp1.find({
    sal: { $gt: 5000 }
})
```

---

# Step 7: Display Employees Having Salary Less Than 15000

```javascript
db.emp1.find({
    sal: { $lt: 15000 }
})
```

---

# Step 8: Display Employees Having Salary Greater Than 10000 and Less Than 20000

```javascript
db.emp1.find({
    $and: [
        { sal: { $gt: 10000 } },
        { sal: { $lt: 20000 } }
    ]
})
```

---

# Step 9: Update Salary of All Employees by 10%

```javascript
db.emp1.updateMany(
    {},
    {
        $mul: { sal: 1.1 }
    }
)
```

---

# Step 10: Delete Employees Having Salary Less Than 5000

```javascript
db.emp1.deleteMany({
    sal: { $lt: 5000 }
})
```

---

# Step 11: Rename Collection

```javascript
db.emp1.renameCollection("employee1")
```

---

# Step 12: Display Employees Whose Names Start With 'N'

```javascript
db.employee1.find({
    ename: /^N/
})
```

---

# Concepts Used
- MongoDB Database Creation
- createCollection()
- insertOne()
- insertMany()
- save()
- find()
- updateMany()
- deleteMany()
- renameCollection()
- Logical Operators:
  - $gt
  - $lt
  - $and
- Regular Expressions

---

# Result
Successfully performed CRUD operations in MongoDB including insertion, retrieval, updation, deletion, renaming collections, and pattern matching queries.