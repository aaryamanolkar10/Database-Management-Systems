# Aggregation and Indexing in MongoDB

## Aim
To perform aggregation and indexing operations using MongoDB.

---

# Problem Statement
Design and execute MongoDB queries using aggregation and indexing techniques with suitable examples.

---

# Software Required
- MongoDB
- Mongo Shell (mongosh)

---

# Step 1: Create and Use Database

```javascript
use product_detail
```

---

# Step 2: Display All Databases

```javascript
show dbs
```

---

# Step 3: Create Collection

```javascript
db.createCollection("product")
```

---

# Step 4: Display All Collections

```javascript
show collections
```

---

# Step 5: Insert Documents into product Collection

```javascript
db.product.insertMany([
{
    item: "pen",
    price: 10,
    quantity: 2
},
{
    item: "book",
    price: 50,
    quantity: 1
},
{
    item: "pen",
    price: 10,
    quantity: 5
},
{
    item: "pencil",
    price: 5,
    quantity: 10
}
])
```

---

# Step 6: Retrieve All Documents

```javascript
db.product.find()
```

---

# Step 7: Create Index on item Field in Ascending Order

```javascript
db.product.createIndex({ item: 1 })
```

---

# Step 8: Display Indexes Created on Collection

```javascript
db.product.getIndexes()
```

---

# Step 9: Create Compound Index

```javascript
db.product.createIndex({
    price: 1,
    quantity: -1
})
```

### Explanation
- `1` → Ascending Order
- `-1` → Descending Order

---

# Step 10: Drop Index Created on price

```javascript
db.product.dropIndex({
    price: 1,
    quantity: -1
})
```

---

# Step 11: Perform Aggregation Queries

## Calculate Total Sales for Each Item

### Formula
```text
sales = price × quantity
```

```javascript
db.product.aggregate([
{
    $group: {
        _id: "$item",
        totalSales: {
            $sum: {
                $multiply: ["$price", "$quantity"]
            }
        }
    }
},
{
    $sort: {
        totalSales: -1
    }
},
{
    $project: {
        _id: 0,
        item: "$_id",
        totalSales: 1
    }
}
])
```

---

# Output Example

```javascript
[
  { item: "pen", totalSales: 70 },
  { item: "book", totalSales: 50 },
  { item: "pencil", totalSales: 50 }
]
```

---

# Concepts Used
- MongoDB Database Operations
- Collection Creation
- insertMany()
- find()
- createIndex()
- getIndexes()
- dropIndex()
- Aggregation Framework
- $group
- $sum
- $multiply
- $sort
- $project

---

# Result
Successfully performed aggregation and indexing operations in MongoDB including index creation, compound indexing, aggregation pipeline queries, and summarized sales report generation.