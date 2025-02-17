# username.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Love & Labyrinth</title>
  <style>
    /* General Reset and Fonts */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 10px;
    }
    h1 {
      margin-bottom: 10px;
    }
    /* Dynamic Quotes Section */
    .quote-section {
      background: rgba(255, 255, 255, 0.8);
      border-radius: 8px;
      padding: 20px;
      width: 100%;
      max-width: 600px;
      text-align: center;
      margin-bottom: 20px;
    }
    .quote-section p {
      font-size: 1.3em;
      margin-bottom: 10px;
    }
    .quote-section button {
      padding: 8px 16px;
      font-size: 1em;
      border: none;
      border-radius: 4px;
      background: #ff6f61;
      color: white;
      cursor: pointer;
    }
    /* Maze Section */
    .maze-section {
      background: rgba(255, 255, 255, 0.9);
      border-radius: 8px;
      padding: 10px;
      width: 100%;
      max-width: 400px;
      margin-bottom: 20px;
    }
    .maze-container {
      display: grid;
      grid-template-columns: repeat(10, 1fr);
      gap: 1px;
      background: #333;
    }
    .maze-cell {
      background: white;
      width: 100%;
      padding-top: 100%; /* 1:1 Aspect Ratio */
      position: relative;
    }
    /* Wall cells will have a darker background */
    .maze-cell.wall {
      background: #333;
    }
    /* Player marker */
    .maze-cell.player::after {
      content: "☺";
      font-size: 1.5em;
      color: #ff6f61;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    /* Heart/Goal marker */
    .maze-cell.goal::after {
      content: "❤";
      font-size: 1.5em;
      color: red;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    /* Arrow Buttons */
    .controls {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      max-width: 400px;
    }
    .controls button {
      background: #ff6f61;
      color: white;
      border: none;
      padding: 10px 16px;
      font-size: 1.2em;
      border-radius: 4px;
      cursor: pointer;
      flex: 1 1 30%;
    }
    @media (max-width: 400px) {
      .quote-section p { font-size: 1.1em; }
      .controls button { font-size: 1em; padding: 8px 12px; }
    }
  </style>
</head>
<body>
  <!-- Dynamic Love Quotes Section -->
  <div class="quote-section">
    <h1>Daily Dose of Love</h1>
    <p id="quote">"Your love is my endless inspiration."</p>
    <button onclick="nextQuote()">Next Quote</button>
  </div>

  <!-- Maze Game Section -->
  <div class="maze-section">
    <h1>Find the Heart</h1>
    <div id="maze" class="maze-container"></div>
  </div>

  <!-- On-Screen Arrow Buttons for Maze Navigation -->
  <div class="controls">
    <button onclick="movePlayer('up')">&#8593;</button>
    <button onclick="movePlayer('left')">&#8592;</button>
    <button onclick="movePlayer('down')">&#8595;</button>
    <button onclick="movePlayer('right')">&#8594;</button>
  </div>

  <script>
    /* Dynamic Quotes Logic */
    const quotes = [
      "Your love is my endless inspiration.",
      "In your eyes, I find my home.",
      "Every heartbeat sings a song of us.",
      "You turn my every moment into magic.",
      "Our love is a journey with no end."
    ];
    let quoteIndex = 0;
    function nextQuote() {
      quoteIndex = (quoteIndex + 1) % quotes.length;
      document.getElementById("quote").textContent = '"' + quotes[quoteIndex] + '"';
    }
    // Auto-rotate quotes every 8 seconds
    setInterval(nextQuote, 8000);

    /* Maze Game Logic */
    const mazeContainer = document.getElementById("maze");
    const gridSize = 10; // 10x10 maze
    let maze = []; // 2D array for maze cells
    let playerPos = { r: 0, c: 0 };
    const goalPos = { r: gridSize - 1, c: gridSize - 1 };

    // Simple maze generation: 0 for path, 1 for wall.
    // For simplicity, we'll hardcode a simple maze pattern.
    // (You can later replace this with a proper randomized maze generator.)
    function generateMaze() {
      maze = [];
      for (let r = 0; r < gridSize; r++) {
        let row = [];
        for (let c = 0; c < gridSize; c++) {
          // Create outer walls
          if (r === 0 || c === 0 || r === gridSize - 1 || c === gridSize - 1) {
            row.push(1);
          } else {
            // Randomly place walls (with 30% chance) but ensure start and goal are open.
            row.push(Math.random() < 0.3 ? 1 : 0);
          }
        }
        maze.push(row);
      }
      // Ensure start and goal are clear
      maze[playerPos.r][playerPos.c] = 0;
      maze[goalPos.r][goalPos.c] = 0;
    }
    
    // Render maze on screen
    function renderMaze() {
      mazeContainer.innerHTML = "";
      for (let r = 0; r < gridSize; r++) {
        for (let c = 0; c < gridSize; c++) {
          const cell = document.createElement("div");
          cell.className = "maze-cell";
          if (maze[r][c] === 1) {
            cell.classList.add("wall");
          }
          if (r === playerPos.r && c === playerPos.c) {
            cell.classList.add("player");
          }
          if (r === goalPos.r && c === goalPos.c) {
            cell.classList.add("goal");
          }
          mazeContainer.appendChild(cell);
        }
      }
    }
    
    // Check if move is valid (not out of bounds and not a wall)
    function canMove(newR, newC) {
      return newR >= 0 && newR < gridSize &&
             newC >= 0 && newC < gridSize &&
             maze[newR][newC] === 0;
    }
    
    // Move player in given direction
    function movePlayer(direction) {
      let newR = playerPos.r;
      let newC = playerPos.c;
      if (direction === "up") newR--;
      else if (direction === "down") newR++;
      else if (direction === "left") newC--;
      else if (direction === "right") newC++;
      
      if (canMove(newR, newC)) {
        playerPos = { r: newR, c: newC };
        renderMaze();
        checkWin();
      }
    }
    
    function checkWin() {
      if (playerPos.r === goalPos.r && playerPos.c === goalPos.c) {
        setTimeout(() => {
          alert("Congratulations! You reached the heart!");
          // Reset maze
          playerPos = { r: 0, c: 0 };
          generateMaze();
          renderMaze();
        }, 100);
      }
    }
    
    // Initialize game
    generateMaze();
    renderMaze();
  </script>
</body>
</html>



