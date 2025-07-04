# The-Grid
Study table for ICSE Board 2026
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Study Table</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Roboto', sans-serif;
    }
    body {
      background-color: #f0f4f8;
      color: #333;
      padding: 20px;
      transition: background-color 0.3s, color 0.3s;
    }
    .dark-mode {
      background-color: #121212;
      color: #eee;
    }
    header {
      text-align: center;
      margin-bottom: 20px;
    }
    .quote {
      font-style: italic;
      margin: 10px 0;
    }
    .section {
      margin: 20px 0;
    }
    textarea, input[type="text"] {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }
    .button {
      padding: 10px 20px;
      border: none;
      border-radius: 6px;
      background-color: #007bff;
      color: white;
      cursor: pointer;
      margin-right: 10px;
    }
    .button:hover {
      background-color: #0056b3;
    }
    .task-item {
      display: flex;
      justify-content: space-between;
      margin-bottom: 8px;
    }
    .task-item span {
      flex: 1;
    }
    .task-item button {
      margin-left: 10px;
    }
    .dark-toggle {
      position: fixed;
      top: 20px;
      right: 20px;
      background-color: #333;
      color: white;
      padding: 8px;
      border: none;
      border-radius: 50%;
      cursor: pointer;
    }
    .subject-list, .schedule {
      background-color: #fff;
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }
    .subject-list h3, .schedule h3 {
      margin-bottom: 10px;
    }
    .subject-list ul, .schedule ul {
      list-style: none;
      padding-left: 0;
    }
    .subject-list li, .schedule li {
      margin-bottom: 5px;
    }
  </style>
</head>
<body>
  <button class="dark-toggle" onclick="toggleDarkMode()">🌓</button>
  <header>
    <h1>My Study Table</h1>
    <p class="quote" id="quote">Loading quote...</p>
  </header>

  <div class="subject-list">
    <h3>Board: ICSE</h3>
    <h3>Subjects and Books:</h3>
    <ul>
      <li><strong>Physics:</strong> Concise Physics ICSE Class 10</li>
      <li><strong>Biology:</strong> Concise Biology ICSE Class 10</li>
      <li><strong>Chemistry:</strong> Simplified ICSE Chemistry by Viraf J. Dalal Class 10</li>
      <li><strong>Mathematics:</strong> APC Understanding Mathematics ICSE by M.L. Aggarwal</li>
      <li><strong>History & Civics:</strong> APC Modern Indian History and Civics ICSE Class 10 by B.B. Tayal</li>
      <li><strong>Geography:</strong> Frank Modern Certificate Geography Class 10 ICSE</li>
      <li><strong>English (Drama):</strong> Julius Caesar by Xavier Pinto - Beeta Publications</li>
      <li><strong>English (Prose & Poetry):</strong> Treasure Chest ICSE Short Stories and Poems Class 9 & 10</li>
      <li><strong>Bengali (Prose & Poetry):</strong> Sonkolita Class 9 & 10 Short Stories and Poems</li>
    </ul>
  </div>

  <div class="schedule">
    <h3>Weekly Schedule:</h3>
    <ul>
      <li><strong>Monday:</strong> School 8:00am–2:00pm | Computer 4:00–5:30pm | English 6:00–8:00pm</li>
      <li><strong>Tuesday:</strong> School 8:00am–2:00pm | No Tuitions</li>
      <li><strong>Wednesday:</strong> School 8:00am–2:00pm | Bengali 4:00–5:30pm | Science & Maths 7:00–8:30pm</li>
      <li><strong>Thursday:</strong> School 8:00am–2:00pm | Science & Maths 5:30–7:00pm</li>
      <li><strong>Friday:</strong> School 8:00am–2:00pm | English 4:30–6:30pm | Computer 8:30–10:00pm</li>
      <li><strong>Saturday:</strong> Science & Maths 4:00–5:30pm | Bengali 6:00–8:00pm</li>
      <li><strong>Sunday:</strong> No School / No Tuitions</li>
    </ul>
  </div>

  <section class="section">
    <h2>Notes</h2>
    <textarea id="notes" placeholder="Write your notes here..."></textarea>
  </section>

  <section class="section">
    <h2>To-Do List</h2>
    <input type="text" id="todoInput" placeholder="Add a task...">
    <button class="button" onclick="addTask()">Add</button>
    <div id="todoList"></div>
  </section>

  <section class="section">
    <h2>Useful Links</h2>
    <textarea id="links" placeholder="Paste links here...\nExample: https://www.khanacademy.org"></textarea>
  </section>

  <section class="section">
    <h2>Pomodoro Timer</h2>
    <div id="timer">25:00</div>
    <button class="button" onclick="startTimer()">Start</button>
    <button class="button" onclick="resetTimer()">Reset</button>
  </section>

  <script>
    function toggleDarkMode() {
      document.body.classList.toggle('dark-mode');
      localStorage.setItem('darkMode', document.body.classList.contains('dark-mode'));
    }
    if (localStorage.getItem('darkMode') === 'true') {
      document.body.classList.add('dark-mode');
    }
    const areas = ['notes', 'links'];
    areas.forEach(id => {
      const el = document.getElementById(id);
      el.value = localStorage.getItem(id) || '';
      el.addEventListener('input', () => localStorage.setItem(id, el.value));
    });
    function addTask() {
      const input = document.getElementById('todoInput');
      if (input.value.trim() === '') return;
      const taskList = document.getElementById('todoList');
      const div = document.createElement('div');
      div.className = 'task-item';
      div.innerHTML = `<span>${input.value}</span><button onclick="this.parentElement.remove(); saveTasks()">❌</button>`;
      taskList.appendChild(div);
      input.value = '';
      saveTasks();
    }
    function saveTasks() {
      const tasks = Array.from(document.querySelectorAll('.task-item span')).map(e => e.innerText);
      localStorage.setItem('tasks', JSON.stringify(tasks));
    }
    function loadTasks() {
      const tasks = JSON.parse(localStorage.getItem('tasks') || '[]');
      tasks.forEach(text => {
        const div = document.createElement('div');
        div.className = 'task-item';
        div.innerHTML = `<span>${text}</span><button onclick="this.parentElement.remove(); saveTasks()">❌</button>`;
        document.getElementById('todoList').appendChild(div);
      });
    }
    loadTasks();
    let timer;
    let timeLeft = 25 * 60;
    function updateTimerDisplay() {
      const min = Math.floor(timeLeft / 60);
      const sec = timeLeft % 60;
      document.getElementById('timer').textContent = `${min.toString().padStart(2, '0')}:${sec.toString().padStart(2, '0')}`;
    }
    function startTimer() {
      if (timer) return;
      timer = setInterval(() => {
        timeLeft--;
        updateTimerDisplay();
        if (timeLeft <= 0) {
          clearInterval(timer);
          timer = null;
          alert("Time's up! Take a break.");
        }
      }, 1000);
    }
    function resetTimer() {
      clearInterval(timer);
      timer = null;
      timeLeft = 25 * 60;
      updateTimerDisplay();
    }
    updateTimerDisplay();
    const quotes = [
      "Stay focused and never give up.",
      "Small progress is still progress.",
      "Your future depends on what you do today.",
      "Discipline is the bridge between goals and accomplishment.",
      "Push yourself, because no one else is going to do it for you."
    ];
    document.getElementById('quote').textContent = quotes[Math.floor(Math.random() * quotes.length)];
  </script>
</body>
</html>
