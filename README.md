<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crypto Gambling</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #222;
            color: white;
            margin: 0;
            padding: 0;
            text-align: center;
        }
        
        .header {
            background-color: #333;
            padding: 20px;
            text-align: center;
        }

        .header h1 {
            margin: 0;
        }

        .content {
            padding: 20px;
        }

        .coin-info, .crypto-addresses {
            display: inline-block;
            margin: 20px;
        }

        .crypto-addresses {
            max-width: 200px;
            text-align: left;
        }

        .crypto-addresses div {
            margin-bottom: 5px;
        }

        .slot-game {
            margin-top: 20px;
        }

        .slot-row {
            font-size: 40px;
            margin: 10px;
        }

        .feedback-box {
            display: none;
            background-color: #333;
            padding: 20px;
            width: 300px;
            margin: 20px auto;
        }

        .feedback-box textarea {
            width: 100%;
            height: 100px;
            margin-bottom: 10px;
        }

        .luxury-notification {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #444;
            padding: 10px 20px;
            color: white;
            border-radius: 5px;
            display: none;
            opacity: 0;
            transition: opacity 0.5s ease;
        }

        .luxury-notification.show {
            display: block;
            opacity: 1;
        }

        .button {
            background-color: #28a745;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
            margin: 10px;
            border-radius: 5px;
        }

        .button:hover {
            background-color: #218838;
        }

        .spinning {
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>

<div class="header">
    <h1>Welcome to Crypto Gambling!</h1>
    <p>Tip crypto master with your donation and enjoy the game!</p>
</div>

<div class="content">
    <!-- Coin Balance -->
    <div class="coin-info">
        <h2>Your Coin Balance: <span id="coinBalance">0</span></h2>
    </div>

    <!-- Admin Verification -->
    <div class="coin-info">
        <input type="text" id="adminCode" placeholder="Enter Admin Code">
        <button class="button" onclick="verifyAdmin()">Verify Admin</button>
    </div>

    <!-- Redeem Coins -->
    <div class="coin-info">
        <input type="text" id="redeemCode" placeholder="Enter Redeem Code">
        <button class="button" onclick="redeemCoins()">Redeem Coins</button>
    </div>

    <!-- Slot Game -->
    <div class="slot-game">
        <div class="slot-row" id="slot1">🍒</div>
        <div class="slot-row" id="slot2">🍉</div>
        <div class="slot-row" id="slot3">🍇</div>
        <button class="button" onclick="spinSlotGame()">Spin</button>
    </div>

    <!-- Feedback Form -->
    <button class="button" onclick="showFeedbackForm()">Give Feedback</button>
    <div class="feedback-box">
        <textarea id="feedback" placeholder="Enter your feedback..."></textarea><br>
        <button class="button" onclick="submitFeedback()">Submit</button>
        <button class="button" onclick="cancelFeedbackForm()">Cancel</button>
    </div>

    <!-- Crypto Addresses -->
    <div class="crypto-addresses">
        <h3>Crypto Addresses</h3>
        <div>Bitcoin (BTC): <span id="btc-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</span> <button class="button" onclick="copyToClipboard('btc-address')">Copy</button></div>
        <div>XRP: <span id="xrp-address">riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ</span> <button class="button" onclick="copyToClipboard('xrp-address')">Copy</button></div>
        <div>Solana (SOL): <span id="solana-address">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</span> <button class="button" onclick="copyToClipboard('solana-address')">Copy</button></div>
        <div>BNB: <span id="bnb-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span> <button class="button" onclick="copyToClipboard('bnb-address')">Copy</button></div>
        <div>Polygon (MATIC): <span id="polygon-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span> <button class="button" onclick="copyToClipboard('polygon-address')">Copy</button></div>
        <div>Litecoin (LTC): <span id="litecoin-address">Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc</span> <button class="button" onclick="copyToClipboard('litecoin-address')">Copy</button></div>
        <div>USDT (Ethereum Network): <span id="usdt-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span> <button class="button" onclick="copyToClipboard('usdt-address')">Copy</button></div>
        <div>USDC (Ethereum Network): <span id="usdc-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span> <button class="button" onclick="copyToClipboard('usdc-address')">Copy</button></div>
        <div>COSMOS (ATOM): <span id="cosmos-address">cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n</span> <button class="button" onclick="copyToClipboard('cosmos-address')">Copy</button></div>
        <div>Official Trump (Solana): <span id="trump-address">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</span> <button class="button" onclick="copyToClipboard('trump-address')">Copy</button></div>
        <div>Shiba Inu (Ethereum): <span id="shiba-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span> <button class="button" onclick="copyToClipboard('shiba-address')">Copy</button></div>
    </div>

    <!-- Notification -->
    <div id="message" class="luxury-notification"></div>
</div>

<script>
    // Slot Game Function
    function spinSlotGame() {
        const fruits = ["🍒", "🍉", "🍇", "🍊", "🍓", "🍋", "🍏"];
        let result = [];
        let win = false;

        // Generate a random result for the 3 rows
        for (let i = 0; i < 3; i++) {
            let randomFruit = fruits[Math.floor(Math.random() * fruits.length)];
            result.push(randomFruit);
        }

        // Display the result on the screen
        const slotRow = document.querySelectorAll('.slot-row');
        result.forEach((fruit, index) => {
            const item = slotRow[index];
            item.textContent = fruit;

            // Adding animation for spinning
            item.classList.add('spinning');
            setTimeout(() => {
                item.classList.remove('spinning');
            }, 800);
        });

        // Check if all 3 rows have the same fruit
        if (result[0] === result[1] && result[1] === result[2]) {
            win = true;
        }

        // Show the results after the spin
        setTimeout(() => {
            if (win) {
                showLuxuryNotification("You won 10,000 coins!");
                updateCoinBalance(10000
