<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tip CryptoGuy - Support Me</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
            background-color: #000;
            color: #fff;
        }
        h1 {
            font-size: 2.5em;
            color: #fff;
        }
        p {
            font-size: 1.2em;
            margin: 10px 0;
        }
        .crypto-address {
            font-weight: bold;
            background: #eaeaea;
            padding: 10px;
            border-radius: 5px;
            display: inline-block;
            margin-bottom: 20px;
            font-size: 12px;
            color: red;
            word-wrap: break-word;
            max-width: 400px;
        }
        .goal {
            margin: 20px auto;
            font-size: 1.5em;
            color: #28a745;
            font-weight: bold;
        }
        footer {
            margin-top: 30px;
            font-size: 0.9em;
            color: #666;
        }
        .copy-btn {
            padding: 5px 10px;
            background-color: #28a745;
            border: none;
            border-radius: 3px;
            cursor: pointer;
            color: white;
        }
        .copy-btn:hover {
            background-color: #218838;
        }
        /* Game Styles */
        .game-container {
            margin-top: 50px;
            padding: 20px;
        }
        .game-board {
            background-color: #eee;
            width: 300px;
            height: 400px;
            margin: 0 auto;
            border-radius: 5px;
        }
        #game-board {
            background-color: #eee;
            width: 300px;
            height: 400px;
            margin: 0 auto;
            border-radius: 5px;
        }
        #game-board canvas {
            display: block;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <h1>Welcome to Tip CryptoGuy</h1>
    <p>Your tips help me achieve my goals!</p>

    <!-- Admin Verification Section -->
    <h3>Admin Verification</h3>
    <input type="password" id="admin-password" placeholder="Enter Admin Password">
    <button onclick="verifyAdmin()">Submit</button>
    <div id="admin-status"></div>

    <h3>Tip me with Bitcoin (BTC):</h3>
    <p class="crypto-address" id="btc-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48 <button class="copy-btn" onclick="copyToClipboard('btc-address')">Copy</button></p>
    
    <h3>Tip me with Ethereum (ETH):</h3>
    <p class="crypto-address" id="eth-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('eth-address')">Copy</button></p>

    <h3>Tip me with Dogecoin (DOGE):</h3>
    <p class="crypto-address" id="doge-address">D9W4z33sejaWfrhTYL8DiD5GGUn7gUjT3fP <button class="copy-btn" onclick="copyToClipboard('doge-address')">Copy</button></p>
    
    <h3>Tip me with Litecoin (LTC):</h3>
    <p class="crypto-address" id="ltc-address">LcFf4y7wx8v9KjiMdx74y5JTK6Lgti3AHXw <button class="copy-btn" onclick="copyToClipboard('ltc-address')">Copy</button></p>
    
    <h3>Tip me with Bitcoin Cash (BCH):</h3>
    <p class="crypto-address" id="bch-address">qzv5u7f76nxjw2d8cqr9p0s0g54c9l85y3gn9wuh59 <button class="copy-btn" onclick="copyToClipboard('bch-address')">Copy</button></p>

    <!-- Feedback Section -->
    <button onclick="openFeedback()">Give Feedback</button>
    <div id="feedback-popup" class="game-container" style="display:none;">
        <h3>Feedback</h3>
        <textarea id="feedback-text" placeholder="Enter your feedback..."></textarea><br>
        <button class="copy-btn" onclick="submitFeedback()">Submit</button>
    </div>

    <!-- Game Section -->
    <div class="game-container" id="game-container">
        <h3>Simple Game: Click to Play</h3>
        <button onclick="startGame()">Start Simple Game</button>
        <div id="game-board"></div>
    </div>

    <footer>
        <p>Thank you for your support!</p>
    </footer>

    <script>
        let isAdmin = false;
        let coinBalance = 0; // Default balance for non-admin users
        let highScore = 0;

        // Function to copy text to clipboard
        function copyToClipboard(id) {
            const text = document.getElementById(id).innerText;
            navigator.clipboard.writeText(text);
        }

        // Admin verification process
        function verifyAdmin() {
            const password = document.getElementById('admin-password').value;
            const validPassword = "Ariengambleswhilebeingabillionaire";
            if (password === validPassword) {
                isAdmin = true;
                coinBalance = 999999999;  // Admin coins
                document.getElementById('admin-status').innerText = "Admin verified! Coin balance is now set to 999999999.";
                document.getElementById('admin-status').style.color = "green";
            } else {
                document.getElementById('admin-status').innerText = "Invalid password. You are not an admin.";
                document.getElementById('admin-status').style.color = "red";
            }
        }

        // Feedback Section
        function openFeedback() {
            document.getElementById('feedback-popup').style.display = 'block';
        }

        function submitFeedback() {
            const feedback = document.getElementById('feedback-text').value;
            alert("Feedback submitted: " + feedback);
            document.getElementById('feedback-popup').style.display = 'none';
        }

        // Simple Game
        function startGame() {
            let score = 0;
            let gameBoard = document.getElementById("game-board");
            gameBoard.innerHTML = `<h4>Score: <span id="score">${score}</span></h4>`;

            let interval = setInterval(() => {
                score++;
                document.getElementById("score").innerText = score;
            }, 1000);

            // Stop the game after 10 seconds
            setTimeout(() => {
                clearInterval(interval);
                alert("Game Over! Final score: " + score);
                if (score > highScore) {
                    highScore = score;
                    alert("New High Score: " + highScore);
                }
            }, 10000);
        }

    </script>
</body>
</html>
