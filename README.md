# MWAD-EX_03-To-Do-List-using-JavaScript
## Date: 9/09/2025

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Nithila's Todo App</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Poppins', sans-serif; }

    body {
      background: linear-gradient(135deg, #ffdde1, #ee9ca7, #a1c4fd, #c2e9fb);
      background-size: 400% 400%;
      animation: gradientBG 12s ease infinite;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    header {
      background: rgba(0,0,0,0.6);
      padding: 15px;
      text-align: center;
      color: #fff;
      font-size: 2rem;
      font-weight: bold;
      border-bottom: 3px solid #fff;
      letter-spacing: 1px;
    }

    .todo-container {
      flex: 1;
      max-width: 600px;
      margin: 30px auto;
      background: rgba(255,255,255,0.9);
      border-radius: 20px;
      padding: 25px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      animation: fadeIn 1s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .input-section {
      display: flex;
      gap: 10px;
      margin-bottom: 15px;
    }

    .input-section input {
      flex: 1;
      padding: 12px;
      border-radius: 10px;
      border: 2px solid #ccc;
      font-size: 1rem;
      transition: 0.3s;
    }

    .input-section input:focus {
      border-color: #6a11cb;
      outline: none;
      box-shadow: 0 0 10px rgba(106,17,203,0.3);
    }

    .input-section button {
      padding: 12px 18px;
      background: linear-gradient(135deg, #6a11cb, #2575fc);
      border: none;
      border-radius: 10px;
      color: white;
      cursor: pointer;
      font-weight: bold;
      transition: 0.3s;
    }

    .input-section button:hover {
      transform: scale(1.05);
      background: linear-gradient(135deg, #2575fc, #6a11cb);
    }

    ul {
      margin-top: 15px;
      list-style: none;
    }

    li {
      background: #fefefe;
      padding: 14px;
      margin-bottom: 12px;
      border-radius: 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      transition: 0.3s;
    }

    li:hover {
      transform: scale(1.02);
    }

    li.completed span {
      text-decoration: line-through;
      opacity: 0.6;
    }

    .actions button {
      margin-left: 6px;
      border: none;
      border-radius: 8px;
      padding: 6px 10px;
      cursor: pointer;
      font-size: 0.9rem;
      color: white;
      transition: 0.3s;
    }

    .edit { background: #f39c12; }
    .delete { background: #e74c3c; }
    .complete { background: #27ae60; }

    .actions button:hover {
      transform: scale(1.1);
    }

    .filter-section {
      margin-top: 15px;
      text-align: center;
    }

    .filter-section select {
      padding: 8px;
      border-radius: 8px;
      border: 2px solid #6a11cb;
      font-weight: bold;
    }

    footer {
      background: rgba(0,0,0,0.7);
      padding: 15px;
      text-align: center;
      color: white;
      font-size: 1rem;
      border-top: 3px solid #fff;
    }

    footer b {
      color: #ffd700;
    }
  </style>
</head>
<body>
  <header>🌸 Nithila's Todo Application 🌸</header>

  <div class="todo-container">
    <div class="input-section">
      <input type="text" id="todo-input" placeholder="✨ Write your task here...">
      <button id="add-btn">Add</button>
    </div>

    <div class="filter-section">
      <label><b>Filter:</b> </label>
      <select id="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="pending">Pending</option>
      </select>
    </div>

    <ul id="todo-list"></ul>
  </div>

  <footer>
    Developed by <b>Nithila S</b> | Reg.No: <b>212224040224</b>
  </footer>

  <script>
    const todoInput = document.getElementById("todo-input");
    const addBtn = document.getElementById("add-btn");
    const todoList = document.getElementById("todo-list");
    const filter = document.getElementById("filter");

    let todos = JSON.parse(localStorage.getItem("todos")) || [];

    function saveTodos() {
      localStorage.setItem("todos", JSON.stringify(todos));
    }

    function renderTodos() {
      todoList.innerHTML = "";
      const filterValue = filter.value;

      todos.forEach((todo, index) => {
        if (filterValue === "completed" && !todo.completed) return;
        if (filterValue === "pending" && todo.completed) return;

        const li = document.createElement("li");
        li.className = todo.completed ? "completed" : "";

        li.innerHTML = `
          <span>${todo.text}</span>
          <div class="actions">
            <button class="complete">✔</button>
            <button class="edit">✎</button>
            <button class="delete">🗑</button>
          </div>
        `;

        li.querySelector(".complete").addEventListener("click", () => {
          todos[index].completed = !todos[index].completed;
          saveTodos();
          renderTodos();
        });

        li.querySelector(".edit").addEventListener("click", () => {
          const newText = prompt("Edit task:", todo.text);
          if (newText) {
            todos[index].text = newText;
            saveTodos();
            renderTodos();
          }
        });

        li.querySelector(".delete").addEventListener("click", () => {
          todos.splice(index, 1);
          saveTodos();
          renderTodos();
        });

        todoList.appendChild(li);
      });
    }

    addBtn.addEventListener("click", () => {
      const text = todoInput.value.trim();
      if (text) {
        todos.push({ text, completed: false });
        todoInput.value = "";
        saveTodos();
        renderTodos();
      }
    });

    filter.addEventListener("change", renderTodos);

    renderTodos();
  </script>
</body>
</html>


## OUTPUT
<img width="1919" height="1033" alt="Screenshot 2025-09-09 132748" src="https://github.com/user-attachments/assets/e260abbb-6860-4c02-b46d-bcf1e6d3d6d7" />
<img width="1919" height="1017" alt="Screenshot 2025-09-09 132903" src="https://github.com/user-attachments/assets/ce87e21e-843e-4e90-84b9-c52f18b2f9ae" />



## RESULT
The program for creating To-do list using JavaScript is executed successfully.
