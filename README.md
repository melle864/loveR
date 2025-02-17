# username.github.io

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
  <title>Love & Labyrinth</title>
  <style>
    /* Reset & Base Styles */
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
    h1 { margin-bottom: 10px; color: #333; }
    /* Quote Section */
    .quote-section {
      background: rgba(255, 255, 255, 0.95);
      border-radius: 10px;
      padding: 20px;
      margin-bottom: 20px;
      width: 100%;
      max-width: 600px;
      text-align: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }
    .quote-section p {
      font-size: 1.2rem;
      margin-bottom: 10px;
      color: #555;
    }
    .quote-section button {
      padding: 10px 20px;
      font-size: 1rem;
      background: #ff6f61;
      border: none;
      border-radius: 5px;
      color: #fff;
      cursor: pointer;
    }
    /* Maze Section */
    .maze-section {
      background: rgba(255, 255, 255, 0.98);
      border-radius: 10px;
      padding: 10px;
      margin-bottom: 20px;
      width: 100%;
      max-width: 400px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }
    .maze-container {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 2px;
    }
    .maze-cell {
      background: #fff;
      width: 100%;
      padding-top: 100%; /* square cells */
      position: relative;
    }
    .maze-cell.wall { background: #333; }
    .maze-cell.player::after {
      content: "☺";
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.5rem;
      color: #ff6f61;
    }
    .maze-cell.goal::after {
      content: "❤";
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.5rem;
      color: red;
    }
    /* Arrow Controls */
    .controls {
      display: flex;
      justify-content: space-around;
      gap: 10px;
      width: 100%;
      max-width: 400px;
    }
    .controls button {
      flex: 1;
      padding: 15px;
      font-size: 1.2rem;
      background: #ff6f61;
      border: none;
      border-radius: 5px;
      color: #fff;
      cursor: pointer;
    }
    @media (max-width: 400px) {
      .quote-section p { font-size: 1rem; }
      .controls button { padding: 12px; font-size: 1rem; }
    }
  </style>
</head>
<body>
  <!-- Dynamic Love Quotes Section -->
  <div class="quote-section">
    <h1>Words of Love</h1>
    <p id="quote">"Love is the light that guides me home."</p>
    <button onclick="nextQuote()">Next Quote</button>
  </div>

  <!-- Maze Game Section -->
  <div class="maze-section">
    <h1>Labyrinth of Love</h1>
    <div id="maze" class="maze-container"></div>
  </div>

  <!-- On-screen Arrow Controls -->
  <div class="controls">
    <button onclick="move('up')">&#8593;</button>
    <button onclick="move('left')">&#8592;</button>
    <button onclick="move('down')">&#8595;</button>
    <button onclick="move('right')">&#8594;</button>
  </div>

  <script>
    /* Dynamic Quotes */
    const quotes = [
      "Love is the light that guides me home.",
      "Your smile is the sunrise of my heart.",
      "In your eyes, I see endless possibility.",
      "Every heartbeat whispers your name.",
      "Our love is a journey of endless wonder."
    ];
    let quoteIndex = 0;
    function nextQuote() {
      quoteIndex = (quoteIndex + 1) % quotes.length;
      document.getElementById("quote").textContent = '"' + quotes[quoteIndex] + '"';
    }
    setInterval(nextQuote, 8000);

    /* Maze Game Logic */
    const gridSize = 5; // 5x5 maze for mobile
    const mazeElement = document.getElementById("maze");
    let maze = [
      [0, 1, 0, 0, 0],
      [0, 1, 0, 1, 0],
      [0, 0, 0, 1, 0],
      [1, 0, 1, 0, 0],
      [0, 0, 0, 1, 0]
    ];
    let playerPos = { r: 0, c: 0 };
    const goalPos = { r: gridSize - 1, c: gridSize - 1 };

    function renderMaze() {
      mazeElement.innerHTML = "";
      for (let r = 0; r < gridSize; r++) {
        for (let c = 0; c < gridSize; c++) {
          const cell = document.createElement("div");
          cell.classList.add("maze-cell");
          if (maze[r][c] === 1) cell.classList.add("wall");
          if (r === playerPos.r && c === playerPos.c) cell.classList.add("player");
          if (r === goalPos.r && c === goalPos.c) cell.classList.add("goal");
          mazeElement.appendChild(cell);
        }
      }
    }

    function move(direction) {
      let newR = playerPos.r, newC = playerPos.c;
      if (direction === "up") newR--;
      else if (direction === "down") newR++;
      else if (direction === "left") newC--;
      else if (direction === "right") newC++;
      if (newR >= 0 && newR < gridSize && newC >= 0 && newC < gridSize && maze[newR][newC] === 0) {
        playerPos = { r: newR, c: newC };
        renderMaze();
        checkWin();
      }
    }

    function checkWin() {
      if (playerPos.r === goalPos.r && playerPos.c === goalPos.c) {
        setTimeout(() => {
          alert("Congratulations! You found the heart!");
          // Reset the maze game
          playerPos = { r: 0, c: 0 };
          renderMaze();
        }, 100);
      }
    }

    // Initialize Maze
    renderMaze();
  </script>
</body>
</html>




