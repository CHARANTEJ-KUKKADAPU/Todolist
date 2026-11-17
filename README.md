# Ex03 To-Do List using JavaScript
## Date:17.11.26

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

index.html
```c
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Todo Application</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <div class="container">

        <header>
            <h1>My Todo List</h1>
            <p>Organize your tasks and stay productive</p>
        </header>

        <div class="todo-box">

            <div class="input-section">
                <input type="text" id="taskInput" placeholder="Enter a new task...">
                <button id="addBtn">Add Task</button>
            </div>

            <div class="search-section">
                <input type="text" id="searchInput" placeholder="Search tasks...">
            </div>

            <div class="filter-section">
                <button class="filter-btn active" data-filter="all">All</button>
                <button class="filter-btn" data-filter="active">Active</button>
                <button class="filter-btn" data-filter="completed">Completed</button>
            </div>

            <div class="task-info">
                <span id="taskCount">0 tasks</span>
                <button id="clearCompleted">Clear Completed</button>
            </div>

            <ul id="taskList"></ul>

            <div id="emptyMessage" class="empty-message">
                No tasks found
            </div>

        </div>

        <footer>
            <p>Designed & Developed by <strong>Aathishwaran K</strong></p>
            <p>Register Number: <strong>212225040006</strong></p>
        </footer>

    </div>

    <script src="script.js"></script>

</body>
</html>
```

style.css
```c
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #667eea, #764ba2);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    padding: 40px 20px;
}

.container {
    width: 100%;
    max-width: 700px;
}

header {
    text-align: center;
    color: white;
    margin-bottom: 25px;
}

header h1 {
    font-size: 40px;
    margin-bottom: 8px;
}

header p {
    font-size: 16px;
}

.todo-box {
    background: white;
    padding: 25px;
    border-radius: 15px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.input-section {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

input {
    font-size: 16px;
    padding: 13px;
    border: 1px solid #ccc;
    border-radius: 8px;
    outline: none;
}

input:focus {
    border-color: #667eea;
}

#taskInput {
    flex: 1;
}

button {
    border: none;
    cursor: pointer;
    border-radius: 8px;
    padding: 12px 18px;
    font-size: 15px;
}

#addBtn {
    background: #667eea;
    color: white;
}

#addBtn:hover {
    background: #5568d8;
}

.search-section {
    margin-bottom: 15px;
}

#searchInput {
    width: 100%;
}

.filter-section {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.filter-btn {
    background: #eee;
    color: #333;
}

.filter-btn.active {
    background: #667eea;
    color: white;
}

.task-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
    color: #555;
}

#clearCompleted {
    background: #ff6b6b;
    color: white;
}

#clearCompleted:hover {
    background: #e85555;
}

#taskList {
    list-style: none;
}

.task-item {
    display: flex;
    align-items: center;
    gap: 10px;
    background: #f7f7f7;
    padding: 14px;
    margin-bottom: 10px;
    border-radius: 8px;
    border-left: 4px solid #667eea;
}

.task-item.completed {
    border-left-color: #28a745;
}

.task-item.completed .task-text {
    text-decoration: line-through;
    color: #888;
}

.task-text {
    flex: 1;
    font-size: 16px;
    word-break: break-word;
}

.complete-btn {
    background: #28a745;
    color: white;
}

.edit-btn {
    background: #ffc107;
    color: #222;
}

.delete-btn {
    background: #dc3545;
    color: white;
}

.complete-btn:hover {
    background: #218838;
}

.edit-btn:hover {
    background: #e0a800;
}

.delete-btn:hover {
    background: #c82333;
}

.empty-message {
    text-align: center;
    color: #888;
    padding: 25px;
    display: none;
}

footer {
    text-align: center;
    color: white;
    margin-top: 25px;
    line-height: 1.8;
}

footer strong {
    color: #fff;
}

@media (max-width: 600px) {

    body {
        padding: 20px 10px;
    }

    header h1 {
        font-size: 30px;
    }

    .todo-box {
        padding: 18px;
    }

    .input-section {
        flex-direction: column;
    }

    #addBtn {
        width: 100%;
    }

    .filter-section {
        flex-wrap: wrap;
    }

    .task-item {
        flex-wrap: wrap;
    }

    .task-text {
        width: 100%;
        flex-basis: 100%;
    }

    .task-info {
        flex-direction: column;
        gap: 10px;
        align-items: stretch;
    }

    #clearCompleted {
        width: 100%;
    }
}
```

script.jss
```c
let tasks = [];
let currentFilter = "all";

const taskInput = document.getElementById("taskInput");
const addBtn = document.getElementById("addBtn");
const taskList = document.getElementById("taskList");
const searchInput = document.getElementById("searchInput");
const taskCount = document.getElementById("taskCount");
const emptyMessage = document.getElementById("emptyMessage");
const clearCompleted = document.getElementById("clearCompleted");
const filterButtons = document.querySelectorAll(".filter-btn");

function addTask() {
    const taskText = taskInput.value.trim();

    if (taskText === "") {
        alert("Please enter a task.");
        return;
    }

    const task = {
        id: Date.now(),
        text: taskText,
        completed: false
    };

    tasks.push(task);
    taskInput.value = "";

    displayTasks();
}

function displayTasks() {
    taskList.innerHTML = "";

    const searchText = searchInput.value.toLowerCase();

    let filteredTasks = tasks.filter(function(task) {
        return task.text.toLowerCase().includes(searchText);
    });

    if (currentFilter === "active") {
        filteredTasks = filteredTasks.filter(function(task) {
            return !task.completed;
        });
    }

    if (currentFilter === "completed") {
        filteredTasks = filteredTasks.filter(function(task) {
            return task.completed;
        });
    }

    filteredTasks.forEach(function(task) {

        const li = document.createElement("li");
        li.className = "task-item";

        if (task.completed) {
            li.classList.add("completed");
        }

        const span = document.createElement("span");
        span.className = "task-text";
        span.textContent = task.text;

        const completeButton = document.createElement("button");
        completeButton.className = "complete-btn";
        completeButton.textContent = task.completed ? "Undo" : "Complete";

        completeButton.addEventListener("click", function() {
            toggleTask(task.id);
        });

        const editButton = document.createElement("button");
        editButton.className = "edit-btn";
        editButton.textContent = "Edit";

        editButton.addEventListener("click", function() {
            editTask(task.id);
        });

        const deleteButton = document.createElement("button");
        deleteButton.className = "delete-btn";
        deleteButton.textContent = "Delete";

        deleteButton.addEventListener("click", function() {
            deleteTask(task.id);
        });

        li.appendChild(span);
        li.appendChild(completeButton);
        li.appendChild(editButton);
        li.appendChild(deleteButton);

        taskList.appendChild(li);
    });

    updateTaskCount();

    if (filteredTasks.length === 0) {
        emptyMessage.style.display = "block";
    } else {
        emptyMessage.style.display = "none";
    }
}

function toggleTask(id) {
    tasks = tasks.map(function(task) {

        if (task.id === id) {
            task.completed = !task.completed;
        }

        return task;
    });

    displayTasks();
}

function editTask(id) {

    const task = tasks.find(function(task) {
        return task.id === id;
    });

    const newText = prompt("Edit your task:", task.text);

    if (newText !== null && newText.trim() !== "") {
        task.text = newText.trim();
        displayTasks();
    }
}

function deleteTask(id) {

    const confirmation = confirm("Are you sure you want to delete this task?");

    if (confirmation) {
        tasks = tasks.filter(function(task) {
            return task.id !== id;
        });

        displayTasks();
    }
}

function updateTaskCount() {

    const activeTasks = tasks.filter(function(task) {
        return !task.completed;
    });

    if (activeTasks.length === 1) {
        taskCount.textContent = "1 task remaining";
    } else {
        taskCount.textContent = activeTasks.length + " tasks remaining";
    }
}

addBtn.addEventListener("click", addTask);

taskInput.addEventListener("keydown", function(event) {
    if (event.key === "Enter") {
        addTask();
    }
});

searchInput.addEventListener("input", function() {
    displayTasks();
});

filterButtons.forEach(function(button) {

    button.addEventListener("click", function() {

        filterButtons.forEach(function(btn) {
            btn.classList.remove("active");
        });

        button.classList.add("active");

        currentFilter = button.dataset.filter;

        displayTasks();
    });
});

clearCompleted.addEventListener("click", function() {

    tasks = tasks.filter(function(task) {
        return !task.completed;
    });

    displayTasks();
});

displayTasks();
```


## OUTPUT
![alt text](<Screenshot 2026-11-17 183458.png>)

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
