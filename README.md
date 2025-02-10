# username.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be My Love?</title>
    <style>
        body {
            background-color: red;
            color: white;
            font-family: 'Arial', sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            position: relative;
            overflow: hidden;
            background-image: url('https://www.example.com/heart-background.png'); /* Replace with your heart background image */
            background-size: cover;
        }

        .moon {
            position: absolute;
            top: 20px;
            left: 20px;
            width: 60px;
            height: 60px;
            background-image: url('https://www.example.com/moon.png'); /* Replace with your moon image */
            background-size: cover;
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 40px;
            text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.7);
        }

        .button {
            font-size: 1.5em;
            padding: 15px 25px;
            margin: 20px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
        }

        .yes {
            background-color: #4CAF50;
        }

        .no {
            background-color: #f44336;
        }

        .yes:hover, .no:hover {
            transform: scale(1.1);
            opacity: 0.8;
        }

        .yes.growing {
            font-size: 4em;
            padding: 40px 80px;
        }

        .hidden {
            display: none;
        }

        .message {
            font-size: 1.8em;
            color: white;
            margin-top: 20px;
            text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.7);
        }
    </style>
</head>
<body>

    <!-- Moon -->
    <div class="moon"></div>

    <!-- Question -->
    <h1>Will you be the love of my life?</h1>

    <!-- Buttons -->
    <button class="button yes" id="yesBtn">Yes</button>
    <button class="button no" id="noBtn">No</button>

    <!-- Messages -->
    <div class="message" id="message"></div>

    <script>
        const yesButton = document.getElementById('yesBtn');
        const noButton = document.getElementById('noBtn');
        const message = document.getElementById('message');
        let noClickCount = 0;

        // When "No" button is clicked
        noButton.addEventListener('click', function() {
            noClickCount++;
            yesButton.classList.add('growing');
            if (noClickCount === 1) {
                message.textContent = 'Wrong button?';
            } else if (noClickCount === 2) {
                message.textContent = 'What are you doing? Press Yes!';
            } else if (noClickCount === 3) {
                message.textContent = 'Please?? 🙏';
            } else if (noClickCount === 4) {
                message.textContent = 'Press Yes and I\'ll get you chocolate!';
            } else if (noClickCount === 5) {
                message.textContent = 'B2olek eh ya bt enty dosy 3la el zorar el 25dar?';
            } else if (noClickCount === 6) {
                yesButton.style.fontSize = '10em';
                yesButton.style.padding = '150px 250px';
                message.textContent = 'Now... PRESS YES!';
            }
        });

        // When "Yes" button is clicked, navigate to the second page
        yesButton.addEventListener('click', function() {
            window.location.href = 'timer.html'; // Redirect to the second page
        });
    </script>

</body>
</html>
