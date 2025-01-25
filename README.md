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

    <h3>Tip me with Bitcoin (BTC):</h3>
    <p class="crypto-address" id="btc-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48 <button class="copy-btn" onclick="copyToClipboard('btc-address')">Copy</button></p>
    
    <h3>Tip me with Ethereum (ETH):</h3>
    <p class="crypto-address" id="eth-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('eth-address')">Copy</button></p>
    
    <h3>Tip me with XRP:</h3>
    <p class="crypto-address" id="xrp-address">riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ <button class="copy-btn" onclick="copyToClipboard('xrp-address')">Copy</button></p>
    
    <h3>Tip me with Solana (SOL):</h3>
    <p class="crypto-address" id="sol-address">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c <button class="copy-btn" onclick="copyToClipboard('sol-address')">Copy</button></p>
    
    <h3>Tip me with Binance Coin (BNB):</h3>
    <p class="crypto-address" id="bnb-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('bnb-address')">Copy</button></p>

    <h3>Tip me with Polygon (MATIC):</h3>
    <p class="crypto-address" id="matic-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('matic-address')">Copy</button></p>

    <h3>Tip me with Litecoin (LTC):</h3>
    <p class="crypto-address" id="ltc-address">Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc <button class="copy-btn" onclick="copyToClipboard('ltc-address')">Copy</button></p>

    <h3>Tip me with USDT (Ethereum Network):</h3>
    <p class="crypto-address" id="usdt-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('usdt-address')">Copy</button></p>

    <h3>Tip me with USDC (Ethereum Network):</h3>
    <p class="crypto-address" id="usdc-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('usdc-address')">Copy</button></p>

    <h3>Tip me with Cosmos (ATOM):</h3>
    <p class="crypto-address" id="atom-address">cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n <button class="copy-btn" onclick="copyToClipboard('atom-address')">Copy</button></p>

    <h3>Tip me with Shiba Inu (Ethereum Network):</h3>
    <p class="crypto-address" id="shiba-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63 <button class="copy-btn" onclick="copyToClipboard('shiba-address')">Copy</button></p>

    <div class="goal">
        Current Donations: $0 / $10,000
    </div>

    <div class="progress-bar">
        <div class="progress-fill" id="donation-progress"></div>
    </div>

    <div class="slot-game" id="slot-game">
        <h3>Slot Game</h3>
        <div class="slot-reels">
            <div class="reel" id="reel-1">🍒</div>
            <div class="reel" id="reel-2">🍒</div>
            <div class="reel" id="reel-3">🍒</div>
        </div>
        <button class="spin-btn" onclick="spinSlot()">Spin</button>
    </div>

    <div class="simple-game" id="simple-game">
        <h3>Simple Game (No Coin Required)</h3>
        <div id="game-board">
            <canvas id="gameCanvas" width="300" height="400"></canvas>
        </div>
        <button class="feedback-btn" onclick="startGame()">Start Game</button>
        <h4>High Score: <span id="high-score">0</span></h4>
    </div>

    <footer>
        <p>Thank you for your support!</p>
    </footer>

    <script>
        let isAdmin = false;
        let coinBalance = 0;
        let highScore = 0;

        window.onload = function() {
            verifyAdmin();
            updateCoinBalance();
            loadFeedbackPopup();
        }

        function verifyAdmin() {
            setTimeout(function() {
                let verificationCode = prompt("This verification is only to detect if you are an admin or not. If you're not an admin, please click the decline button.\nEnter verification code:");

                if (verificationCode === "Ariengambleswhilebeingabillionaire") {
                    alert("Successful!");
                    isAdmin = true;
