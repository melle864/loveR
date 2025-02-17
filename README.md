
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>Love Quotes, Poems & Labyrinth ❤️</title>
  <style>
    /* Global Reset & Base Styles */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      background: linear-gradient(to bottom right, red, pink);
      color: white;
      text-align: center;
      font-family: 'Arial', sans-serif;
      padding: 20px;
      overflow-x: hidden;
    }
    h1 {
      font-size: 28px;
      text-shadow: 2px 2px 4px black;
      margin-bottom: 10px;
    }
    /* Navigation Bar */
    nav {
      position: fixed;
      top: 0;
      width: 100%;
      background: rgba(0, 0, 0, 0.7);
      padding: 10px 0;
      z-index: 10;
    }
    nav a {
      color: gold;
      text-decoration: none;
      margin: 0 15px;
      font-size: 1.1rem;
      font-weight: bold;
    }
    /* Floating Hearts Animation */
    .heart {
      position: absolute;
      font-size: 30px;
      opacity: 0.8;
      animation: floatUp 5s infinite ease-in-out;
    }
    @keyframes floatUp {
      0% { transform: translateY(100vh); opacity: 1; }
      50% { opacity: 0.8; }
      100% { transform: translateY(-10vh); opacity: 0; }
    }
    /* Background Floating Quotes (for extra life) */
    .bg-quotes {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      pointer-events: none;
      z-index: -1;
      font-family: 'Arial', sans-serif;
      color: rgba(255,255,255,0.3);
      overflow: hidden;
    }
    .bg-quotes span {
      position: absolute;
      font-size: 3rem;
      text-shadow: 2px 2px 8px black;
      animation: float 25s linear infinite;
    }
    @keyframes float {
      0% { transform: translateY(100vh) rotate(0deg); opacity: 0.3; }
      50% { opacity: 0.5; }
      100% { transform: translateY(-150vh) rotate(360deg); opacity: 0.3; }
    }
    /* Quote & Poems Section */
    .quote-container {
      background: rgba(0, 0, 0, 0.6);
      padding: 20px;
      border-radius: 15px;
      margin-top: 80px;
      font-size: 20px;
      max-width: 90%;
      margin-left: auto;
      margin-right: auto;
    }
    .nav-buttons {
      margin-top: 20px;
      display: flex;
      justify-content: center;
      gap: 20px;
    }
    .btn {
      background: gold;
      color: black;
      padding: 10px 20px;
      font-size: 18px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: 0.3s;
    }
    .btn:hover {
      background: white;
    }
    /* Labyrinth (Maze) Section */
    .maze-section {
      background: rgba(255,255,255,0.98);
      color: #333;
      border-radius: 10px;
      padding: 15px;
      margin: 20px auto 140px;
      max-width: 400px;
    }
    .maze-section h1 {
      color: #333;
      font-size: 1.2rem;
      margin-bottom: 10px;
    }
    .maze-container {
      display: grid;
      grid-template-columns: repeat(8, 1fr);
      gap: 2px;
    }
    .maze-cell {
      width: 100%;
      padding-top: 100%;
      position: relative;
      border: 2px solid #333;
      background: #fff;
    }
    .maze-cell.open-top { border-top: none; }
    .maze-cell.open-right { border-right: none; }
    .maze-cell.open-bottom { border-bottom: none; }
    .maze-cell.open-left { border-left: none; }
    .maze-cell.player::after,
    .maze-cell.goal::after {
      position: absolute;
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.6rem;
    }
    .maze-cell.player::after { content: "☺"; color: #ff6f61; }
    .maze-cell.goal::after { content: "❤"; color: red; }
    /* On-screen Maze Controls */
    .controls {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      gap: 10px;
      width: 90%;
      max-width: 400px;
      z-index: 5;
    }
    .controls button {
      flex: 1;
      padding: 15px 0;
      background: #ff6f61;
      border: none;
      border-radius: 5px;
      color: #fff;
      font-size: 1.2rem;
      cursor: pointer;
    }
    @media (max-width: 400px) {
      .quote-container { font-size: 18px; }
      .btn { font-size: 16px; padding: 8px 16px; }
      .controls button { font-size: 1rem; padding: 12px 0; }
    }
  </style>
</head>
<body>
  <!-- Navigation Bar -->
  <nav>
    <a href="love.html">Forever Us</a>
    <a href="#quotes">Love Words</a>
  </nav>
  
  <!-- Background Floating Quotes -->
  <div class="bg-quotes">
    <span style="top: 5%; left: 10%; animation-delay: 0s;">"Eternity in a glance"</span>
    <span style="top: 15%; left: 70%; animation-delay: 3s;">"In your eyes, I see forever"</span>
    <span style="top: 35%; left: 30%; animation-delay: 5s;">"Hearts beat as one"</span>
    <span style="top: 55%; left: 80%; animation-delay: 2s;">"Whispers of passion"</span>
    <span style="top: 70%; left: 20%; animation-delay: 6s;">"Dreams woven in love"</span>
    <span style="top: 85%; left: 50%; animation-delay: 4s;">"Souls entwined in magic"</span>
  </div>
  
  <!-- Love Quotes & Poems Section -->
  <section id="quotes" class="quote-container">
    <h1>Love in Words ❤️</h1>
    <div id="quoteDisplay">"You are my today and all of my tomorrows. ❤️"</div>
    <div class="nav-buttons">
      <button class="btn" onclick="prevQuote()">⬅ Previous</button>
      <button class="btn" onclick="nextQuote()">Next ➡</button>
    </div>
    <br>
    <button class="btn" onclick="window.location.href='love.html'">Back to Love Page ❤️</button>
  </section>
  
  <!-- Labyrinth (Maze) Section -->
  <section class="maze-section">
    <h1>Labyrinth of Love</h1>
    <div id="maze" class="maze-container"></div>
  </section>
  
  <!-- On-screen Maze Controls -->
  <div class="controls">
    <button onclick="move('up')">&#8593;</button>
    <button onclick="move('left')">&#8592;</button>
    <button onclick="move('down')">&#8595;</button>
    <button onclick="move('right')">&#8594;</button>
  </div>
  
  <script>
    /* Love Quotes Logic */
    const quotes = [
      "You are my today and all of my tomorrows. ❤️",
      "I love you more than words can express, more than the stars in the sky. ✨",
      "In your eyes, I see my forever. 💕",
      "You are the melody my heart has always wanted to sing. 🎶",
      "Loving you is my favorite adventure. 🌍",
      "You and me—always and forever. 🔗",
      "Every moment with you is a beautiful memory in the making. 📖",
      "You are my greatest love story. 💌",
      "If love were a journey, I’d walk it forever with you. 🚶‍♂️❤️",
      "You are the missing piece I never knew I needed. 🧩",
      "Your love is the most beautiful thing I have ever known. 🌹",
      "Forever isn’t long enough to love you. ⏳",
      "I found my home in your heart. 🏡❤️",
      "Every heartbeat echoes our shared dreams. – Unknown",
      "Together, our souls write an endless poem. – Unknown",
      "In your smile, I see my destiny. – Unknown",
      "Our love is a timeless dance of passion. – Unknown",
      "With you, every day is a celebration of life. – Unknown",
      "Our hearts beat as one, forever entwined. – Unknown",
      "Love begins and ends with you. – Unknown"
    ];
    let currentQuoteIndex = 0;
    document.getElementById("quoteDisplay").innerText = quotes[currentQuoteIndex];
    function nextQuote() {
      currentQuoteIndex = (currentQuoteIndex + 1) % quotes.length;
      document.getElementById("quoteDisplay").innerText = quotes[currentQuoteIndex];
    }
    function prevQuote() {
      currentQuoteIndex = (currentQuoteIndex - 1 + quotes.length) % quotes.length;
      document.getElementById("quoteDisplay").innerText = quotes[currentQuoteIndex];
    }
    
    /* ------------------------------
         Maze Game: Recursive Backtracking
    ------------------------------ */
    const gridSize = 8; // 8x8 maze grid
    const mazeEl = document.getElementById("maze");
    let mazeGrid = [];
    let playerPos = { i: 0, j: 0 };
    const goalPos = { i: gridSize - 1, j: gridSize - 1 };
    
    function initMaze() {
      mazeGrid = [];
      for (let i = 0; i < gridSize; i++) {
        mazeGrid[i] = [];
        for (let j = 0; j < gridSize; j++) {
          mazeGrid[i][j] = { walls: { top: true, right: true, bottom: true, left: true }, visited: false };
        }
      }
      let stack = [];
      let current = { i: 0, j: 0 };
      mazeGrid[0][0].visited = true;
      while (true) {
        let neighbors = [];
        if (current.i > 0 && !mazeGrid[current.i - 1][current.j].visited)
          neighbors.push({ i: current.i - 1, j: current.j, direction: 'top' });
        if (current.j < gridSize - 1 && !mazeGrid[current.i][current.j + 1].visited)
          neighbors.push({ i: current.i, j: current.j + 1, direction: 'right' });
        if (current.i < gridSize - 1 && !mazeGrid[current.i + 1][current.j].visited)
          neighbors.push({ i: current.i + 1, j: current.j, direction: 'bottom' });
        if (current.j > 0 && !mazeGrid[current.i][current.j - 1].visited)
          neighbors.push({ i: current.i, j: current.j - 1, direction: 'left' });
        
        if (neighbors.length > 0) {
          const next = neighbors[Math.floor(Math.random() * neighbors.length)];
          if (next.direction === 'top') {
            mazeGrid[current.i][current.j].walls.top = false;
            mazeGrid[next.i][next.j].walls.bottom = false;
          } else if (next.direction === 'right') {
            mazeGrid[current.i][current.j].walls.right = false;
            mazeGrid[next.i][next.j].walls.left = false;
          } else if (next.direction === 'bottom') {
            mazeGrid[current.i][current.j].walls.bottom = false;
            mazeGrid[next.i][next.j].walls.top = false;
          } else if (next.direction === 'left') {
            mazeGrid[current.i][current.j].walls.left = false;
            mazeGrid[next.i][next.j].walls.right = false;
          }
          stack.push(current);
          current = { i: next.i, j: next.j };
          mazeGrid[current.i][current.j].visited = true;
        } else if (stack.length > 0) {
          current = stack.pop();
        } else {
          break;
        }
      }
    }
    
    /* Maze Rendering */
    function renderMaze() {
      mazeEl.innerHTML = "";
      for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
          const cell = document.createElement("div");
          cell.classList.add("maze-cell");
          const walls = mazeGrid[i][j].walls;
          if (!walls.top) cell.classList.add("open-top");
          if (!walls.right) cell.classList.add("open-right");
          if (!walls.bottom) cell.classList.add("open-bottom");
          if (!walls.left) cell.classList.add("open-left");
          if (i === playerPos.i && j === playerPos.j) cell.classList.add("player");
          if (i === goalPos.i && j === goalPos.j) cell.classList.add("goal");
          mazeEl.appendChild(cell);
        }
      }
    }
    
    /* Maze Movement & Win Check */
    function canMove(direction) {
      const cell = mazeGrid[playerPos.i][playerPos.j];
      if (direction === "up" && !cell.walls.top) return true;
      if (direction === "right" && !cell.walls.right) return true;
      if (direction === "down" && !cell.walls.bottom) return true;
      if (direction === "left" && !cell.walls.left) return true;
      return false;
    }
    function move(direction) {
      if (!canMove(direction)) return;
      if (direction === "up") playerPos.i--;
      else if (direction === "right") playerPos.j++;
      else if (direction === "down") playerPos.i++;
      else if (direction === "left") playerPos.j--;
      renderMaze();
      checkWin();
    }
    function checkWin() {
      if (playerPos.i === goalPos.i && playerPos.j === goalPos.j) {
        setTimeout(() => {
          alert("Congratulations, you have found my heart!");
          playerPos = { i: 0, j: 0 };
          initGame();
        }, 100);
      }
    }
    function initGame() {
      playerPos = { i: 0, j: 0 };
      initMaze();
      renderMaze();
    }
    initGame();
  </script>
</body>
</html>

