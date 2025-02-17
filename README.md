# username.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Love & Labyrinth</title>
  <style>
    /* Global and animated background */
    body {
      margin: 0;
      padding: 0;
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(45deg, #ff9a9e, #fad0c4, #fad0c4);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }
    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    .container {
      width: 90%;
      max-width: 600px;
      margin: 20px;
      text-align: center;
    }
    h1 {
      font-size: 2em;
      margin-bottom: 20px;
    }
    /* Quotes slider */
    .quote-container {
      margin-bottom: 30px;
    }
    .quote {
      font-size: 1.4em;
      margin: 10px 0;
      opacity: 0;
      transition: opacity 1s ease-in-out;
    }
    .quote.visible {
      opacity: 1;
    }
    /* Maze styles */
    .maze-container {
      display: grid;
      grid-template-columns: repeat(10, 1fr);
      grid-gap: 2px;
      margin: 0 auto;
      max-width: 90vw;
    }
    .maze-cell {
      width: 100%;
      padding-top: 100%; /* 1:1 Aspect Ratio */
      position: relative;
    }
    .maze-cell div {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
    }
    .wall {
      background-color: #333;
    }
    .path {
      background-color: #fff;
    }
    .player {
      background-color: #ff6f61;
      border-radius: 50%;
    }
    .heart {
      background-image: url('https://i.imgur.com/OJ8N6fM.png');
      background-size: cover;
    }
    /* Mobile adjustments */
    @media (max-width: 600px) {
      .quote { font-size: 1.2em; }
      h1 { font-size: 1.8em; }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Love & Labyrinth</h1>
    <!-- Dynamic Love Quotes -->
    <div class="quote-container">
      <p id="quote" class="quote"></p>
    </div>
    <!-- Maze -->
    <div id="maze" class="maze-container"></div>
  </div>

  <script>
    /* Dynamic Quotes Section */
    const quotes = [
      "Love is the labyrinth where every turn unveils a new wonder.",
      "In the maze of life, your love is my guiding star.",
      "Every step with you leads to a heart filled with hope."
    ];
    let currentQuote = 0;
    const quoteElement = document.getElementById("quote");
    function showQuote(index) {
      quoteElement.classList.remove("visible");
      setTimeout(() => {
        quoteElement.textContent = quotes[index];
        quoteElement.classList.add("visible");
      }, 500);
    }
    showQuote(currentQuote);
    setInterval(() => {
      currentQuote = (currentQuote + 1) % quotes.length;
      showQuote(currentQuote);
    }, 8000);

    /* Maze Section */
    // Maze represented as a 2D array (0 = path, 1 = wall)
    const mazeData = [
      [0,1,0,0,0,0,1,0,0,0],
      [0,1,0,1,1,0,1,1,1,0],
      [0,0,0,1,0,0,0,0,1,0],
      [1,1,0,1,0,1,1,0,1,0],
      [0,0,0,0,0,1,0,0,0,0],
      [0,1,1,1,0,1,0,1,1,0],
      [0,1,0,0,0,0,0,1,0,0],
      [0,1,0,1,1,1,0,1,0,1],
      [0,0,0,1,0,0,0,0,0,0],
      [1,1,0,0,0,1,1,1,0,0]
    ];
    const rows = mazeData.length;
    const cols = mazeData[0].length;
    const mazeContainer = document.getElementById("maze");
    let cells = []; // To store cell elements

    // Create maze grid
    for (let i = 0; i < rows; i++) {
      cells[i] = [];
      for (let j = 0; j < cols; j++) {
        const cellDiv = document.createElement("div");
        cellDiv.classList.add("maze-cell");
        const innerDiv = document.createElement("div");
        innerDiv.classList.add(mazeData[i][j] === 1 ? "wall" : "path");
        cellDiv.appendChild(innerDiv);
        mazeContainer.appendChild(cellDiv);
        cells[i][j] = innerDiv;
      }
    }

    // Define positions: player starts at top-left, heart is at bottom-right.
    let playerPos = { row: 0, col: 0 };
    const endPos = { row: rows - 1, col: cols - 1 };

    // Update maze with player and heart markers.
    function updateMaze() {
      for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
          cells[i][j].classList.remove("player", "heart");
        }
      }
      cells[playerPos.row][playerPos.col].classList.add("player");
      cells[endPos.row][endPos.col].classList.add("heart");
    }
    updateMaze();

    // Function to move player if allowed.
    function movePlayer(deltaRow, deltaCol) {
      const newRow = playerPos.row + deltaRow;
      const newCol = playerPos.col + deltaCol;
      if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols && mazeData[newRow][newCol] === 0) {
        playerPos = { row: newRow, col: newCol };
        updateMaze();
        checkWin();
      }
    }
    function checkWin() {
      if (playerPos.row === endPos.row && playerPos.col === endPos.col) {
        alert("Congratulations! You reached the heart!");
        playerPos = { row: 0, col: 0 };
        updateMaze();
      }
    }
    // Keyboard controls for desktop.
    document.addEventListener("keydown", (e) => {
      switch(e.key) {
        case "ArrowUp": movePlayer(-1, 0); break;
        case "ArrowDown": movePlayer(1, 0); break;
        case "ArrowLeft": movePlayer(0, -1); break;
        case "ArrowRight": movePlayer(0, 1); break;
      }
    });
    // Swipe detection for mobile.
    let touchStartX = 0, touchStartY = 0;
    document.addEventListener("touchstart", e => {
      touchStartX = e.changedTouches[0].screenX;
      touchStartY = e.changedTouches[0].screenY;
    });
    document.addEventListener("touchend", e => {
      let deltaX = e.changedTouches[0].screenX - touchStartX;
      let deltaY = e.changedTouches[0].screenY - touchStartY;
      if (Math.abs(deltaX) > Math.abs(deltaY)) {
        if (deltaX > 30) movePlayer(0, 1);
        else if (deltaX < -30) movePlayer(0, -1);
      } else {
        if (deltaY > 30) movePlayer(1, 0);
        else if (deltaY < -30) movePlayer(-1, 0);
      }
    });
  </script>
</body>
</html>


