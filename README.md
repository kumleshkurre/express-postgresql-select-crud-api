# Express PostgreSQL CRUD API 🚀

A simple and beginner-friendly **REST API** built using **Node.js (Express.js)** and **PostgreSQL**.  
This project demonstrates how to connect Express with PostgreSQL, perform CRUD operations, and build clean RESTful endpoints.

---

## 📌 Features

✅ PostgreSQL connection using `pg` Pool  
✅ Express.js REST API  
✅ CRUD Operations (Create, Read, Update, Delete)  
✅ Parameterized queries (SQL Injection safe)  
✅ CORS enabled  
✅ JSON request & response handling  

---

## 🛠️ Tech Stack

- **Backend:** Node.js, Express.js  
- **Database:** PostgreSQL  
- **Database Client:** pg (node-postgres)  
- **API Testing:** Postman  

---

## 📂 Project Structure
```
express-postgresql-crud-api
│
├── db.js # PostgreSQL connection pool
├── index.js # Express server & API routes
├── package.json
└── README.md
```
## ⚙️ Configure the PostgreSQL connection pool (`db.js`)
```
const { Pool } = require('pg');
const pool = new Pool({
   user: 'your_username',
   host: 'localhost',
   database: 'your_database_name',
   password: 'YOUR_PASSWORD',
   port: 5432,                     // Default PostgreSQL port

  });
  
  module.exports = pool;
```
## Create Your Express Server
Create a file: index.js
```
// index.js
const express = require('express');
const pool = require('./db');        
const bodyParser = require('body-parser');
const app = express();
const PORT = 1000;

app.use((req, res, next) => {
  res.setHeader('Access-Control-Allow-Origin', '*'); // Or specify your origin
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS, PUT, DELETE');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  res.setHeader('Access-Control-Allow-Credentials', true); // If needed
  next();
});

// Middleware to parse JSON
app.use(bodyParser.json());

// Test the connection
app.get('/',(req, res) => {
    res.send(`<h1>EXPRESS JS API</h1>`);
});
//------------------------------------all data select-------------------------------------
// Define a route to query the database
app.get('/employe', async (req, res) => {
    try {
      const result = await pool.query('SELECT * FROM employe'); // Adjust query to your table
      res.json({status:"200",data:result.rows});
    } catch (err) {
      console.error('Error executing query', err.stack);
      res.status(500).send('Internal Server Error');
    }
  });
  //----------------------------id selection params--------------------------------------
  app.get('/employe/:id', async (req, res) => {
    try {
      const { id } = req.params; // Get 'id' from route parameters
      const result = await pool.query('SELECT * FROM emp.jsloye WHERE id = $1', [id]); // Adjust query to your table
      res.json(result.rows);
    } catch (err) {
      console.error('Error executing query', err.stack);
      res.status(500).send('Internal Server Error');
    }
  });
  //------------------------------------body parser--------------------------------------------
  // Define a route to query the database
app.get('/employeBy', async (req, res) => {
  try {
    const { id } = req.body; // Get 'id' from route parameters
    const result = await pool.query('SELECT * FROM employe WHERE id = $1', [id]);     // Adjust query to your table
    res.json(result.rows);
    console.log(result.rows.length>0)
  } catch (err) {
    console.error('Error executing query', err.stack);
    res.status(500).send('Internal Server Error');
  }
});
    // Start the server
  app.listen(PORT,() => {
    console.log(`Server running on http://localhost:${PORT}`);
  });  
  ```
## 🚀 API Endpoints
🔹 Test API
```
http://localhost:1000
```
 Response:
 ```
<h1>EXPRESS JS API</h1>
```
🔹 Get All Employees
```
http://localhost:1000/employe
```
🔹 Get Employee By ID (URL Parameter)
```
http://localhost:1000/employe/1
```
🔹 Get Employee By ID (Request Body)
```
http://localhost:1000/employeBy
```
Body:
```
{
  "id": 1
}
```
## ▶️ How to Run the Project
### 1️⃣ Start Server
node index.js

### 2️⃣ Server Running On
http://localhost:1000

## 🎯 Learning Outcomes
- Express.js REST API development
- PostgreSQL database integration
- Using pg Pool for database connections
- Handling request params & request body
- Backend project structure best practices

## 👨‍💻 Author

- Kumlesh Kurre
- Backend Developer
- Skills: Express.js | Node.js | PostgreSQL | REST APIs
 
## ⭐ Support
If you like this project, please ⭐ star the repository to support my work!
  
