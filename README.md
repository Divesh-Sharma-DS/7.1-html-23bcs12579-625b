# 7.1-html-23bcs12579-625b
Connect React frontend to fetch data from Express API using Axios.

project/
│
├── backend/
│   ├── server.js
│
└── frontend/
    ├── src/
    │   ├── App.js
    │   ├── components/
    │   │   └── DataDisplay.js
    │   └── index.js



server.js
const express = require("express");
const cors = require("cors");

const app = express();
app.use(cors());

// Sample data
const users = [
  { id: 1, name: "Jaanu", role: "Software Engineer" },
  { id: 2, name: "Aarav", role: "Backend Developer" },
  { id: 3, name: "Riya", role: "Frontend Developer" }
];

// API endpoint
app.get("/api/users", (req, res) => {
  res.json(users);
});

const PORT = 5000;
app.listen(PORT, () => console.log(`✅ Server running on port ${PORT}`));


src/app.js
import React from "react";
import DataDisplay from "./components/DataDisplay";

function App() {
  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>👨‍💻 Fetch Data from Express API</h1>
      <DataDisplay />
    </div>
  );
}

export default App;


DataDisplay.js
import React, { useEffect, useState } from "react";
import axios from "axios";

function DataDisplay() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    axios
      .get("http://localhost:5000/api/users") // API URL
      .then((response) => {
        setUsers(response.data);
      })
      .catch((error) => {
        console.error("Error fetching data:", error);
      });
  }, []);

  return (
    <div>
      <h2>👥 Users List</h2>
      {users.length === 0 ? (
        <p>Loading...</p>
      ) : (
        <ul style={{ listStyleType: "none" }}>
          {users.map((user) => (
            <li key={user.id}>
              <strong>{user.name}</strong> - {user.role}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default DataDisplay;
