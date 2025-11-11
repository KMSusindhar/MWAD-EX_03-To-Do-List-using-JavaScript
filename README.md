# MWAD-EX_03-To-Do-List-using-JavaScript
## Date:

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
```
<!DOCTYPE html>
<html lang="en" >
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Attractive Todo Application</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

    /* Reset and base */
    * {
      box-sizing: border-box;
    }
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      margin: 0;
      padding: 30px 15px;
      display: flex;
      justify-content: center;
      min-height: 100vh;
      color: #2e2e2e;
      user-select: none;
    }

    .todo-app {
      background: white;
      width: 100%;
      max-width: 480px;
      border-radius: 20px;
      box-shadow: 0 12px 40px rgba(0,0,0,0.15);
      padding: 35px 35px 50px;
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
      overflow: hidden;
    }

    /* Illustration */
    .todo-app::before {
      content: '';
      position: absolute;
      top: -80px;
      right: -80px;
      width: 180px;
      height: 180px;
      background: url('https://cdn-icons-png.flaticon.com/512/2913/2913465.png') no-repeat center center;
      background-size: contain;
      opacity: 0.15;
      pointer-events: none;
      user-select: none;
      filter: drop-shadow(0 0 4px rgba(0,0,0,0.05));
    }

    h1 {
      margin-bottom: 25px;
      font-weight: 600;
      font-size: 2.6rem;
      color: #764ba2;
      letter-spacing: 2px;
    }

    form {
      display: flex;
      width: 100%;
      gap: 15px;
      margin-bottom: 30px;
    }

    input[type="text"] {
      flex: 1;
      padding: 14px 18px;
      font-size: 1.1rem;
      border-radius: 50px;
      border: 2px solid #ccc;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
      outline-offset: 2px;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.05);
      font-weight: 500;
    }
    input[type="text"]:focus {
      border-color: #764ba2;
      box-shadow: 0 0 10px #764ba2;
    }

    button.add-btn {
      background-color: #764ba2;
      border: none;
      color: white;
      font-weight: 700;
      font-size: 1.3rem;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(118,75,162,0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      transition: background-color 0.3s ease, transform 0.3s ease;
      user-select: none;
    }
    button.add-btn:hover {
      background-color: #5c368d;
      transform: scale(1.1);
    }
    button.add-btn svg {
      width: 22px;
      height: 22px;
      fill: white;
    }

    ul.todo-list {
      list-style: none;
      padding-left: 0;
      width: 100%;
    }

    ul.todo-list li {
      background: #f6f6f6;
      border-radius: 15px;
      margin-bottom: 15px;
      padding: 15px 20px;
      display: flex;
      align-items: center;
      box-shadow: 0 3px 8px rgb(0 0 0 / 0.05);
      transition: background-color 0.3s ease;
    }
    ul.todo-list li.completed {
      background-color: #d6e9f8;
      color: #7a7a7a;
      text-decoration: line-through;
      box-shadow: 0 3px 8px rgb(118 75 162 / 0.3);
    }
    ul.todo-list li:hover:not(.completed) {
      background-color: #eaeaea;
    }

    /* Custom checkbox */
    ul.todo-list li input[type="checkbox"] {
      appearance: none;
      width: 28px;
      height: 28px;
      border: 3px solid #764ba2;
      border-radius: 50%;
      margin-right: 18px;
      position: relative;
      cursor: pointer;
      transition: all 0.3s ease;
      flex-shrink: 0;
    }
    ul.todo-list li input[type="checkbox"]:checked {
      background-color: #764ba2;
      border-color: #764ba2;
    }
    ul.todo-list li input[type="checkbox"]:checked::after {
      content: "";
      position: absolute;
      top: 5px;
      left: 9px;
      width: 6px;
      height: 12px;
      border: solid white;
      border-width: 0 3px 3px 0;
      transform: rotate(45deg);
    }
    ul.todo-list li input[type="checkbox"]:focus-visible {
      outline: 2px solid #764ba2;
      outline-offset: 3px;
    }

    .todo-text {
      flex: 1;
      font-size: 1.1rem;
      font-weight: 600;
      user-select: text;
      color: #333;
      cursor: text;
      padding: 2px 5px;
      border-radius: 5px;
      transition: background-color 0.2s ease;
    }
    .todo-text[contenteditable="true"] {
      background-color: #fff3fc;
      outline: none;
      box-shadow: 0 0 5px #764ba2;
    }
    .todo-text:hover:not([contenteditable="true"]) {
      background-color: #f0e6fb;
      border-radius: 8px;
    }

    button.delete-btn {
      background: transparent;
      border: none;
      color: #d9534f;
      cursor: pointer;
      font-weight: 700;
      font-size: 1.4rem;
      transition: color 0.3s ease;
      margin-left: 15px;
      flex-shrink: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0;
      width: 32px;
      height: 32px;
      border-radius: 50%;
      user-select: none;
    }
    button.delete-btn:hover {
      color: #b52b2b;
      background-color: #f8d7da;
    }
    button.delete-btn svg {
      width: 18px;
      height: 18px;
      pointer-events: none;
    }

    /* Filters */
    .filters {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin-top: 25px;
      flex-wrap: wrap;
    }

    .filters button {
      background: transparent;
      border: 2px solid #764ba2;
      color: #764ba2;
      padding: 8px 22px;
      font-weight: 600;
      border-radius: 30px;
      cursor: pointer;
      transition: all 0.3s ease;
      user-select: none;
    }

    .filters button.active,
    .filters button:hover {
      background-color: #764ba2;
      color: white;
      box-shadow: 0 6px 15px rgba(118, 75, 162, 0.5);
      transform: scale(1.1);
    }

    /* Clear completed */
    .clear-completed {
      margin-top: 30px;
      display: flex;
      justify-content: center;
    }

    button.clear-btn {
      background-color: #d9534f;
      border: none;
      color: white;
      padding: 12px 30px;
      border-radius: 50px;
      font-weight: 700;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.3s ease;
      user-select: none;
      box-shadow: 0 5px 15px rgba(217, 83, 79, 0.6);
    }
    button.clear-btn:hover {
      background-color: #b52b2b;
      transform: scale(1.05);
    }

    @media (max-width: 500px) {
      .todo-app {
        padding: 25px 25px 40px;
      }
      form {
        gap: 12px;
      }
      button.add-btn {
        width: 45px;
        height: 45px;
      }
      ul.todo-list li {
        padding: 12px 18px;
      }
      .filters button {
        padding: 7px 18px;
        font-size: 0.9rem;
      }
      button.clear-btn {
        padding: 10px 25px;
        font-size: 0.95rem;
      }
    }
  </style>
</head>
<body>
  <section class="todo-app" aria-label="Todo Application">
    <h1>Todo List</h1>
    <form id="todo-form" aria-label="Add todo form">
      <input
        type="text"
        id="todo-input"
        placeholder="Add a new todo..."
        aria-label="New todo"
        required
        autocomplete="off"
      />
      <button type="submit" class="add-btn" aria-label="Add todo">
        <!-- Plus icon SVG -->
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M12 5v14m-7-7h14" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>
    </form>

    <ul id="todo-list" class="todo-list" aria-live="polite"></ul>

    <div class="filters" role="group" aria-label="Filter todos">
      <button class="filter-btn active" data-filter="all" aria-pressed="true">All</button>
      <button class="filter-btn" data-filter="pending" aria-pressed="false">Pending</button>
      <button class="filter-btn" data-filter="completed" aria-pressed="false">Completed</button>
    </div>

    <div class="clear-completed">
      <button id="clear-completed" class="clear-btn" aria-label="Clear completed todos">
        Clear Completed
      </button>
    </div>
  </section>

  <script>
    (() => {
      const todoForm = document.getElementById('todo-form');
      const todoInput = document.getElementById('todo-input');
      const todoList = document.getElementById('todo-list');
      const filterButtons = document.querySelectorAll('.filter-btn');
      const clearCompletedBtn = document.getElementById('clear-completed');

      let todos = JSON.parse(localStorage.getItem('todos')) || [];
      let filter = 'all';

      // Save todos to localStorage
      function saveTodos() {
        localStorage.setItem('todos', JSON.stringify(todos));
      }

      // Render todos based on filter
      function renderTodos() {
        todoList.innerHTML = '';
        let filteredTodos = todos;

        if (filter === 'completed') {
          filteredTodos = todos.filter(todo => todo.completed);
        } else if (filter === 'pending') {
          filteredTodos = todos.filter(todo => !todo.completed);
        }

        if (filteredTodos.length === 0) {
          const emptyMsg = document.createElement('li');
          emptyMsg.textContent = 'No todos found.';
          emptyMsg.style.textAlign = 'center';
          emptyMsg.style.color = '#777';
          emptyMsg.style.padding = '20px 0';
          todoList.appendChild(emptyMsg);
          return;
        }

        filteredTodos.forEach(todo => {
          const li = document.createElement('li');
          li.className = todo.completed ? 'completed' : '';

          // Checkbox
          const checkbox = document.createElement('input');
          checkbox.type = 'checkbox';
          checkbox.checked = todo.completed;
          checkbox.setAttribute('aria-label', 'Mark todo completed');
          checkbox.addEventListener('change', () => toggleCompleted(todo.id));

          // Editable todo text
          const todoText = document.createElement('div');
          todoText.className = 'todo-text';
          todoText.contentEditable = true;
          todoText.spellcheck = false;
          todoText.textContent = todo.text;
          todoText.setAttribute('aria-label', 'Edit todo text');
          todoText.addEventListener('blur', () => updateTodoText(todo.id, todoText.textContent.trim()));
          todoText.addEventListener('keydown', e => {
            if (e.key === 'Enter') {
              e.preventDefault();
              todoText.blur();
            }
          });

          // Delete button with trash icon SVG
          const deleteBtn = document.createElement('button');
          deleteBtn.className = 'delete-btn';
          deleteBtn.setAttribute('aria-label', 'Delete todo');
          deleteBtn.innerHTML = `
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" 
              stroke-linecap="round" stroke-linejoin="round">
              <polyline points="3 6 5 6 21 6"></polyline>
              <path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6"></path>
              <path d="M10 11v6"></path>
              <path d="M14 11v6"></path>
              <path d="M9 6V4a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2"></path>
            </svg>
          `;
          deleteBtn.addEventListener('click', () => deleteTodo(todo.id));

          li.appendChild(checkbox);
          li.appendChild(todoText);
          li.appendChild(deleteBtn);

          todoList.appendChild(li);
        });
      }

      // Add new todo
      function addTodo(text) {
        todos.push({
          id: Date.now(),
          text,
          completed: false,
        });
        saveTodos();
        renderTodos();
      }

      // Toggle completed status
      function toggleCompleted(id) {
        todos = todos.map(todo =>
          todo.id === id ? { ...todo, completed: !todo.completed } : todo
        );
        saveTodos();
        renderTodos();
      }

      // Delete todo
      function deleteTodo(id) {
        todos = todos.filter(todo => todo.id !== id);
        saveTodos();
        renderTodos();
      }

      // Update todo text
      function updateTodoText(id, newText) {
        if (newText === '') {
          deleteTodo(id);
          return;
        }
        todos = todos.map(todo =>
          todo.id === id ? { ...todo, text: newText } : todo
        );
        saveTodos();
        renderTodos();
      }

      // Clear all completed todos
      function clearCompleted() {
        todos = todos.filter(todo => !todo.completed);
        saveTodos();
        renderTodos();
      }

      // Set active filter button styling & aria-pressed
      function setActiveFilter(newFilter) {
        filter = newFilter;
        filterButtons.forEach(btn => {
          const isActive = btn.dataset.filter === filter;
          btn.classList.toggle('active', isActive);
          btn.setAttribute('aria-pressed', isActive);
        });
        renderTodos();
      }

      // Event Listeners
      todoForm.addEventListener('submit', e => {
        e.preventDefault();
        const text = todoInput.value.trim();
        if (text !== '') {
          addTodo(text);
          todoInput.value = '';
          todoInput.focus();
        }
      });

      filterButtons.forEach(btn => {
        btn.addEventListener('click', () => {
          setActiveFilter(btn.dataset.filter);
        });
      });

      clearCompletedBtn.addEventListener('click', () => {
        clearCompleted();
      });

      // Initial render
      renderTodos();
    })();
  </script>
</body>
</html>
```

## OUTPUT
<img width="1907" height="1146" alt="image" src="https://github.com/user-attachments/assets/893ec2a8-c80c-444a-bd47-2bc6ea695944" />



## RESULT
The program for creating To-do list using JavaScript is executed successfully.
