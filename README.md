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
            font-size: 12px; /* Smaller font size */
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
        .progress-bar {
            width: 100%;
            background-color: #ddd;
            height: 30px;
            margin-top: 20px;
            border-radius: 5px;
            position: relative;
        }
        .progress-fill {
            height: 100%;
            background-color: #28a745;
            width: 0%;
            border-radius: 5px;
            position: absolute;
        }
        .invalid {
            color: red;
        }
        .valid {
            color: green;
        }
        .feedback-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #222;
            color: white;
            padding: 20px;
            border-radius: 5px;
        }
        .feedback-btn {
            padding: 10px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 3px;
            cursor: pointer;
        }
        .feedback-btn:hover {
            background-color: #218838;
        }

        /* Slot Game Styles */
        .slot-game {
            margin-top: 50px;
        }
        .slot-reels {
            display: flex;
            justify-content: center;
            margin: 10px;
        }
        .reel {
            background-color: #eee;
            width: 80px;
            height: 80px;
            margin: 5px;
            font-size: 30px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 5px;
        }
        .spin-btn {
            background-color: #28a745;
            color: white;
            padding: 15px 30px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 20px;
            margin-top: 20px;
        }
        .spin-btn:hover {
            background-color: #218838;
        }

        /* Simple Game Styles */
        .simple-game {
            margin-top: 50px;
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

    <!-- Verification Popup -->
    <div id="verification-popup" style="display: none;">
        <h2>Enter Admin Password</h2>
        <input type="password" id="admin-password" placeholder="Enter password">
        <button onclick="verifyAdmin()">Submit</button>
    </div>

    <h3>Tip me with Bitcoin (BTC):</h3>
    <p class="crypto-address" id="btc-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48 <button class="copy-btn" onclick="copyToClipboard('btc-address')">Copy</button></p>
    
    <h3>Tip me with Ethereum (ETH):</h3>
    <p class="crypto-address" id="eth-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('eth-address')">Copy</button></p>
    
    <!-- Feedback Section -->
    <button onclick="openFeedback()">Give Feedback</button>
    <div id="feedback-popup" class="feedback-popup">
        <h3>Feedback</h3>
        <textarea id="feedback-text" placeholder="Enter your feedback..."></textarea><br>
        <button class="feedback-btn" onclick="submitFeedback()">Submit</button>
    </div>

    <!-- Slot Game -->
    <div class="slot-game" id="slot-game">
        <h3>Slot Game</h3>
        <div class="slot-reels">
            <div class="reel" id="reel-1">🍒</div>
            <div class="reel" id="reel-2">🍒</div>
            <div class="reel" id="reel-3">🍒</div>
        </div>
        <button class="spin-btn" onclick="spinSlot()">Spin</button>
    </div>

    <!-- Flappy Bird Game -->
    <div class="simple-game" id="simple-game">
        <h3>Simple Game (Flappy Bird)</h3>
        <div id="game-board">
            <canvas id="gameCanvas" width="300" height="400"></canvas>
        </div>
        <h4>High Score: <span id="high-score">0</span></h4>
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

        // Verification process
        function verifyAdmin() {
            const password = document.getElementById('admin-password').value;
            const validPassword = "Ariengambleswhilebeingabillionaire";
            if (password === validPassword) {
                isAdmin = true;
                coinBalance = 999999999;  // Admin coins
                alert("Admin verified! Coin balance is now set to 999999999.");
            } else {
                alert("Invalid password. You are not an admin.");
            }
            document.getElementById('verification-popup').style.display = 'none';
        }

        // Open feedback form
        function openFeedback() {
            document.getElementById('feedback-popup').style.display = 'block';
        }

        // Submit fake feedback
        function submitFeedback() {
            const feedback = document.getElementById('feedback-text').value;
            alert("Feedback submitted: " + feedback);
            document.getElementById('feedback-popup').style.display = 'none';
        }

        // Slot Game Spin Function
        function spinSlot() {
            const fruits = ["🍒", "🍋", "🍉", "🍊", "🍇"];
            let reel1 = fruits[Math.floor(Math.random() * fruits.length)];
            let reel2 = fruits[Math.floor(Math.random() * fruits.length)];
            let reel3 = fruits[Math.floor(Math.random() * fruits.length)];

            document.getElementById('reel-1').innerText = reel1;
            document.getElementById('reel-2').innerText = reel2;
            document.getElementById('reel-3').innerText = reel3;
        }

        // Flappy Bird Game Logic
        let bird;
        let pipes = [];
        let gravity = 0.6;
        let lift = -15;
        let isFlapping = false;
        let gameCanvas;
        let ctx;

        function setupGame() {
            gameCanvas = document.getElementById('gameCanvas');
            ctx = gameCanvas.getContext('2d');

            bird = {
                x: 50,
                y: 150,
                width: 20,
                height: 20,
                velocity: 0,
            };

            window.addEventListener('keydown', function (e) {
                if (e.code === "Space") {
                    isFlapping = true;
                }
            });

            startGame();
        }

        function startGame() {
            bird.y = 150;
            bird.velocity = 0;
            pipes = [];
            highScore = Math.max(highScore, highScore);
            document.getElementById('high-score').innerText = highScore;
            gameLoop();
        }

        function gameLoop() {
            ctx.clearRect(0, 0, gameCanvas.width, gameCanvas.height);

            bird.velocity += gravity;
            bird.y += bird.velocity;

            if (bird.y > gameCanvas.height - bird.height) {
                bird.y = gameCanvas.height - bird.height;
                bird.velocity = 0;
            }

            if (isFlapping) {
                bird.velocity = lift;
                isFlapping = false;
            }

            ctx.fillStyle = "#ff0";
            ctx.fillRect(bird.x, bird.y, bird.width, bird.height);

            requestAnimationFrame(gameLoop);
        }

        setupGame();
    </script>
</body>
</html>
