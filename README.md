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
            background-color: #1c1c1c;
            color: #fff;
            margin: 0;
            padding: 0;
        }
        h1, h3 {
            color: #f1c40f;
        }
        .crypto-address {
            font-weight: bold;
            background: #eaeaea;
            padding: 10px;
            border-radius: 5px;
            display: inline-block;
            margin-bottom: 20px;
            font-size: 14px;
            color: #f39c12;
        }
        #coin-balance {
            font-size: 20px;
            color: #28a745;
            margin: 10px 0;
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
        .feedback-container {
            display: none;
            position: fixed;
            top: 20%;
            left: 50%;
            transform: translateX(-50%);
            padding: 20px;
            background-color: #fff;
            color: #000;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            z-index: 999;
        }
        .feedback-container input, .feedback-container textarea {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
        }
        .button {
            background-color: #3498db;
            color: #fff;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #2980b9;
        }
        #feedback-btn {
            margin-top: 30px;
        }
        .copy-btn {
            background-color: #f39c12;
            padding: 5px;
            border-radius: 5px;
            cursor: pointer;
        }
        .game-container {
            margin: 20px;
        }
        .game-btn {
            margin: 10px;
        }
        /* Styling for slot machine and blackjack game */
        .slot-container, .blackjack-container {
            margin-top: 20px;
        }
        .slot-item {
            width: 50px;
            height: 50px;
            margin: 5px;
            display: inline-block;
            background-color: #f1c40f;
            border-radius: 10px;
            color: #fff;
            font-size: 18px;
        }
        #blackjack-board {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Welcome to Tip CryptoGuy</h1>
    <p>Your tips help me achieve my goals!</p>
    
    <div id="coin-balance">Your Coin Balance: 0</div>

    <h3>Tip me with Bitcoin (BTC):</h3>
    <p class="crypto-address" id="btc-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</p>
    <button class="copy-btn" onclick="copyAddress('btc-address')">Copy</button>
    
    <h3>Tip me with Ethereum (ETH):</h3>
    <p class="crypto-address" id="eth-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>
    <button class="copy-btn" onclick="copyAddress('eth-address')">Copy</button>
    
    <!-- Add other crypto addresses as needed -->
    
    <div class="goal">
        Current Donations: $0 / $10,000
    </div>

    <button id="feedback-btn" class="button" onclick="showFeedbackForm()">Give Feedback</button>

    <!-- Admin verification input -->
    <div id="admin-verification">
        <input type="text" id="admin-code" placeholder="Enter Admin Code">
        <button class="button" onclick="verifyAdmin()">Verify</button>
    </div>

    <!-- Feedback Form -->
    <div class="feedback-container" id="feedback-container">
        <h3>Feedback</h3>
        <textarea id="feedback-text" placeholder="Write your feedback..."></textarea>
        <button class="button" onclick="sendFeedback()">Submit Feedback</button>
        <button class="button" onclick="closeFeedbackForm()">Cancel</button>
    </div>

    <!-- Slot Game -->
    <div class="slot-container" id="slot-container">
        <h3>Slot Game (1000 coins required)</h3>
        <button class="button game-btn" onclick="playSlotGame()">Spin</button>
        <div id="slot-result"></div>
    </div>

    <!-- Blackjack Game -->
    <div class="blackjack-container" id="blackjack-container">
        <h3>Blackjack Game</h3>
        <button class="button game-btn" onclick="hitCard()">Hit</button>
        <button class="button game-btn" onclick="stand()">Stand</button>
        <div id="blackjack-board"></div>
    </div>

    <footer>
        <p>Thank you for your support!</p>
    </footer>

    <script>
        let coins = 0;
        let adminCode = "Ariengambleswhilebeingabillionaire";
        let isAdmin = false;
        
        function copyAddress(addressId) {
            const addressText = document.getElementById(addressId).innerText;
            navigator.clipboard.writeText(addressText).then(() => {
                alert("Address copied!");
            });
        }

        function showFeedbackForm() {
            document.getElementById("feedback-container").style.display = "block";
        }

        function closeFeedbackForm() {
            document.getElementById("feedback-container").style.display = "none";
        }

        function sendFeedback() {
            const feedback = document.getElementById("feedback-text").value;
            if (feedback.trim() === "") {
                alert("Please write some feedback.");
                return;
            }
            alert("Successfully sent to the owner!");
            document.getElementById("feedback-container").style.display = "none";
        }

        function verifyAdmin() {
            const enteredCode = document.getElementById("admin-code").value;
            if (enteredCode === adminCode) {
                isAdmin = true;
                coins = 999999; // Admin gets infinite coins
                document.getElementById("coin-balance").innerText = `Your Coin Balance: ${coins}`;
                alert("Verification successful! Admin privileges granted.");
            } else {
                alert("INVALID! The admin code is incorrect.");
            }
        }

        function playSlotGame() {
            if (coins < 1000) {
                alert("You need at least 1000 coins to play the slot game.");
                return;
            }
            coins -= 1000; // Deduct coins for playing
            document.getElementById("coin-balance").innerText = `Your Coin Balance: ${coins}`;
            const result = ["🍒", "🍇", "🍉", "🍊", "🍓"];
            const randomResult = result[Math.floor(Math.random() * result.length)];
            document.getElementById("slot-result").innerText = `You got: ${randomResult}`;
        }

        function hitCard() {
            alert("You hit a card!");
            // Blackjack logic here
        }

        function stand() {
            alert("You stood!");
            // Blackjack logic here
        }
    </script>
</body>
</html>
