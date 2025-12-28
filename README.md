<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GET / SET & CRUD Interactive</title>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #fff;
    }

    header {
      text-align: center;
      padding: 40px;
    }

    header h1 {
      font-size: 40px;
    }

    .container {
      max-width: 1000px;
      margin: auto;
      padding: 20px;
    }

    .section {
      background: rgba(255,255,255,0.1);
      border-radius: 16px;
      padding: 25px;
      margin-bottom: 30px;
    }

    h2 {
      color: #00ffd5;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 20px;
    }

    .card {
      background: rgba(0,0,0,0.3);
      padding: 20px;
      border-radius: 14px;
    }

    .example {
      background: #020617;
      padding: 12px;
      border-radius: 8px;
      margin-top: 10px;
      font-family: monospace;
      color: #38bdf8;
    }

    input, button {
      padding: 10px;
      border-radius: 8px;
      border: none;
      margin: 5px 0;
      width: 100%;
    }

    button {
      background: #00ffd5;
      cursor: pointer;
      font-weight: bold;
    }

    button:hover {
      background: #00c2a8;
    }

    ul {
      list-style: none;
      padding: 0;
    }

    li {
      background: rgba(0,0,0,0.4);
      padding: 10px;
      border-radius: 8px;
      margin-bottom: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .actions button {
      width: auto;
      margin-left: 5px;
      background: #ffd369;
    }

    .actions button.delete {
      background: #ff4d4d;
      color: white;
    }

    footer {
      text-align: center;
      padding: 20px;
      opacity: 0.7;
    }
  </style>
</head>
<body>

<header>
  <h1>GET / SET & CRUD</h1>
  <p>Interactive explanation with real examples</p>
</header>

<div class="container">

  <!-- GET & SET -->
  <div class="section">
    <h2>GET & SET</h2>

    <div class="cards">
      <div class="card">
        <h3>GET</h3>
        <p>Retrieve data without changing it.</p>
        <div class="example">GET /users</div>
      </div>

      <div class="card">
        <h3>SET</h3>
        <p>Assign or update a value.</p>
        <div class="example">user.setName("John")</div>
      </div>
    </div>
  </div>

  <!-- CRUD Explanation -->
  <div class="section">
    <h2>CRUD Operations</h2>

    <div class="cards">
      <div class="card">
        <h3>Create</h3>
        <div class="example">POST /users</div>
      </div>

      <div class="card">
        <h3>Read</h3>
        <div class="example">GET /users</div>
      </div>

      <div class="card">
        <h3>Update</h3>
        <div class="example">PUT /users/1</div>
      </div>

      <div class="card">
        <h3>Delete</h3>
        <div class="example">DELETE /users/1</div>
      </div>
    </div>
  </div>

  <!-- CRUD DEMO -->
  <div class="section">
    <h2>🧪 CRUD Demo (JavaScript)</h2>

    <input type="text" id="userInput" placeholder="Enter user name">
    <button onclick="createUser()">Create User</button>

    <ul id="userList"></ul>
  </div>

</div>

<footer>
  💻 CRUD Demo using JavaScript
</footer>

<script>
  let users = [];
  let editIndex = null;

  function createUser() {
    const input = document.getElementById("userInput");
    const value = input.value.trim();

    if (!value) return;

    if (editIndex !== null) {
      // UPDATE
      users[editIndex] = value;
      editIndex = null;
    } else {
      // CREATE
      users.push(value);
    }

    input.value = "";
    renderUsers();
  }

  function renderUsers() {
    const list = document.getElementById("userList");
    list.innerHTML = "";

    // READ
    users.forEach((user, index) => {
      const li = document.createElement("li");
      li.innerHTML = `
        ${user}
        <div class="actions">
          <button onclick="editUser(${index})">Edit</button>
          <button class="delete" onclick="deleteUser(${index})">Delete</button>
        </div>
      `;
      list.appendChild(li);
    });
  }

  function editUser(index) {
    document.getElementById("userInput").value = users[index];
    editIndex = index;
  }

  function deleteUser(index) {
    // DELETE
    users.splice(index, 1);
    renderUsers();
  }
</script>

</body>
</html>
