# username.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Love & Poetry</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Georgia', serif;
      background: linear-gradient(45deg, #ff9a9e, #fad0c4, #fad0c4);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
    }

    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .container {
      background: rgba(0, 0, 0, 0.5);
      padding: 30px 40px;
      border-radius: 10px;
      text-align: center;
      max-width: 90%;
    }

    h1 {
      margin-bottom: 20px;
      font-size: 2.5em;
    }

    .quote {
      font-size: 1.5em;
      line-height: 1.4;
      opacity: 0;
      transition: opacity 1s ease-in-out;
      margin: 0;
    }

    .quote.visible {
      opacity: 1;
    }

    .author {
      margin-top: 10px;
      font-size: 1.2em;
      font-style: italic;
      opacity: 0;
      transition: opacity 1s ease-in-out;
    }

    .author.visible {
      opacity: 1;
    }

    .next-btn {
      margin-top: 25px;
      padding: 10px 20px;
      font-size: 1em;
      background: #ff6f61;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      color: #fff;
      transition: background 0.3s ease;
    }

    .next-btn:hover {
      background: #ff3b2e;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Love & Poetry</h1>
    <p id="quote" class="quote"></p>
    <p id="author" class="author"></p>
    <button id="nextBtn" class="next-btn">Next</button>
  </div>

  <script>
    // Array of love quotes and poems
    const quotes = [
      { 
        quote: "Love is not just looking at each other, but looking in the same direction.", 
        author: "Antoine de Saint-Exupéry" 
      },
      { 
        quote: "I have waited for you as one waits for the moon to rise, patiently and with endless hope.", 
        author: "Unknown" 
      },
      { 
        quote: "Every moment without you is a journey through the stars, searching for the light of your smile.", 
        author: "Unknown" 
      },
      { 
        quote: "Your love is a poem written in the ink of passion and whispered in the silence of the night.", 
        author: "Unknown" 
      },
      { 
        quote: "In your eyes, I see the universe unfolding its infinite beauty, a love story beyond time.", 
        author: "Unknown" 
      }
    ];

    let currentQuote = 0;
    const quoteElement = document.getElementById("quote");
    const authorElement = document.getElementById("author");
    const nextBtn = document.getElementById("nextBtn");

    function showQuote(index) {
      // Remove visibility for fade-out effect
      quoteElement.classList.remove("visible");
      authorElement.classList.remove("visible");

      // Wait for the fade-out to complete, then update text
      setTimeout(() => {
        const { quote, author } = quotes[index];
        quoteElement.textContent = quote;
        authorElement.textContent = author ? `- ${author}` : "";
        // Fade-in the new quote
        quoteElement.classList.add("visible");
        authorElement.classList.add("visible");
      }, 500);
    }

    // Manual change on button click
    nextBtn.addEventListener("click", () => {
      currentQuote = (currentQuote + 1) % quotes.length;
      showQuote(currentQuote);
    });

    // Automatic cycle every 10 seconds
    setInterval(() => {
      currentQuote = (currentQuote + 1) % quotes.length;
      showQuote(currentQuote);
    }, 10000);

    // Show the first quote on page load
    showQuote(currentQuote);
  </script>
</body>
</html>

