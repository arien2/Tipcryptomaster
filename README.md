<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tip CryptoGuy</title>
    <style>
        body {
            background-color: #111;
            color: white;
            font-family: Arial, sans-serif;
        }

        .container {
            width: 80%;
            margin: 0 auto;
        }

        .address-box {
            background-color: #333;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
        }

        .address {
            color: yellow;
            font-size: 14px;
            word-wrap: break-word;
            max-width: 200px;
            text-overflow: ellipsis;
            overflow: hidden;
        }

        button {
            background-color: #28a745;
            border: none;
            padding: 10px 15px;
            color: white;
            cursor: pointer;
            border-radius: 5px;
        }

        button:hover {
            background-color: #218838;
        }

        #coinBalance {
            margin: 20px 0;
            font-size: 18px;
        }

        #verificationBox {
            margin: 20px 0;
            background-color: #444;
            padding: 15px;
            border-radius: 5px;
            display: flex;
            justify-content: center;
        }

        #verificationBox input {
            padding: 5px;
            font-size: 14px;
            margin-right: 10px;
        }

        #verificationBox button {
            background-color: #007bff;
        }

        .game-container {
            margin-top: 30px;
        }

        .slot-game {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-top: 30px;
        }

        .slot-machine {
            font-size: 40px;
            display: flex;
        }

        .slot-item {
            margin: 0 10px;
        }

        .notification {
            font-size: 16px;
            padding: 10px;
            margin: 10px 0;
        }

        .feedback-form {
            margin-top: 30px;
        }

        .feedback-box {
            display: none;
            padding: 10px;
            background-color: #333;
            margin-top: 10px;
            border-radius: 5px;
        }

        .feedback-button {
            padding: 10px;
            background-color: #ffc107;
            border: none;
            color: white;
            border-radius: 5px;
        }

        .redeem-box {
            margin-top: 30px;
            padding: 10px;
            background-color: #333;
            border-radius: 5px;
        }

        .redeem-box input {
            padding: 5px;
            margin-right: 10px;
        }

        .feedback-message {
            padding: 10px;
            color: white;
        }

        .correct {
            background-color: green;
        }

        .incorrect {
            background-color: red;
        }

    </style>
</head>
<body>

<div class="container">
    <h1>Welcome to Tip CryptoGuy</h1>

    <!-- Crypto Addresses Section -->
    <div id="cryptoAddresses"></div>

    <!-- Coin Balance Section -->
    <h3>Current Coin Balance: <span id="coinBalance">0</span> coins</h3>

    <!-- Admin Verification -->
    <div id="verificationBox">
        <input type="text" id="adminCode" placeholder="Enter Admin Code">
        <button onclick="verifyAdmin()">Verify Admin</button>
    </div>

    <div id="message" class="notification"></div>

    <!-- Redeem Coins Section -->
    <div class="redeem-box">
        <h4>Redeem Coins:</h4>
        <input type="text" id="redeemCode" placeholder="Enter Code">
        <button onclick="redeemCoins()">Redeem</button>
    </div>

    <div id="redeemMessage" class="feedback-message"></div>

    <!-- Slot Game Section -->
    <div class="game-container">
        <h3>Slot Game - 1000 Coins to Play!</h3>
        <div id="slotGame" class="slot-game">
            <button onclick="playSlotGame()">Spin</button>
            <div id="slotMachine" class="slot-machine">
                <div class="slot-item">🍒</div>
                <div class="slot-item">🍇</div>
                <div class="slot-item">🍉</div>
            </div>
        </div>
    </div>

    <!-- Feedback Form Section -->
    <div class="feedback-form">
        <button class="feedback-button" onclick="showFeedbackForm()">Give Feedback</button>
        <div class="feedback-box">
            <textarea id="feedback" placeholder="Your Feedback Here..."></textarea>
            <button onclick="submitFeedback()">Submit</button>
        </div>
    </div>
</div>

<script>
    // Your crypto addresses with networks
    const addresses = {
        Bitcoin: "bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48 (BTC)",
        Ethereum: "0x65793418b7a6b0Dced78d59AbD44041b1567BE63 (ETH)",
        XRP: "riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ (XRP)",
        Solana: "CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c (SOL)",
        BNB: "0x65793418b7a6b0Dced78d59AbD44041b1567BE63 (BNB)",
        Polygon: "0x65793418b7a6b0Dced78d59AbD44041b1567BE63 (MATIC)",
        Litecoin: "Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc (LTC)",
        USDT: "0x65793418b7a6b0Dced78d59AbD44041b1567BE63 (USDT)",
        USDC: "0x65793418b7a6b0Dced78d59AbD44041b1567BE63 (USDC)",
        COSMOS: "cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n (ATOM)",
        TrumpCoin: "CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c (TRUMP)",
        ShibaInu: "0x65793418b7a6b0Dced78d59AbD44041b1567BE63 (SHIBA)"
    };

    function displayCryptoAddresses() {
        const cryptoDiv = document.getElementById('cryptoAddresses');
        Object.keys(addresses).forEach(key => {
            const div = document.createElement('div');
            div.classList.add('address-box');
            div.innerHTML = `<div class="address">${key}: ${addresses[key]}</div><button class="copy-btn" onclick="copyToClipboard('${key}')">Copy</button>`;
            cryptoDiv.appendChild(div);
        });
    }

    function copyToClipboard(addressName) {
        const address = addresses[addressName];
        navigator.clipboard.writeText(address).then(() => {
            alert(addressName + " copied!");
        });
    }

    // Slot Game Logic
    function playSlotGame() {
        const fruits = ['🍒', '🍇', '🍉', '🍎', '🍊', '🍍', '🍓'];
        let result = [];
        let win = false;

        for (let i = 0; i < 3; i++) {
            result.push(fruits[Math.floor(Math.random() * fruits.length)]);
        }

        // Show slot results
        const slotMachine = document.getElementById('slotMachine');
        const slotItems = slotMachine.querySelectorAll('.slot-item');
        slotItems.forEach((item, index) => {
            item.textContent = result[index];
        });

        // Check if all fruits match
        if (result[0] === result[1] && result[1] === result[2]) {
            win = true;
            alert("You win 10,000 coins!");
            updateCoinBalance(10000);
        } else {
            alert("Try again!");
        }
    }

    // Update Coin Balance Function
    function updateCoinBalance(amount) {
        let currentBalance = parseInt(document.getElementById("coinBalance").innerText);
        currentBalance += amount;
        document.getElementById("coinBalance").innerText = currentBalance;
    }

    // Admin Verification Logic
    function verifyAdmin() {
        const adminCode = document.getElementById('adminCode').value;
        const correctCode = "Ariengambleswhilebeingabillionaire";
        if (adminCode === correctCode) {
            alert("Admin Verified!");
            updateCoinBalance(999999999);
        } else {
            alert("Invalid Admin Code");
        }
    }

    // Redeem Coins Logic
    function redeemCoins() {
        const redeemCode = document.getElementById('redeemCode').value;
        const correctCode = "SpecialRedeemCode123";
        if (redeemCode === correctCode) {
            alert("Coins Redeemed!");
            updateCoinBalance(5000);  // Adds 5000 coins
        } else {
            alert("Invalid Redeem Code");
        }
    }

    // Feedback Logic
    function showFeedbackForm() {
        const feedbackBox = document.querySelector('.feedback-box');
        feedbackBox.style.display = 'block';
    }

    function submitFeedback() {
        const feedback = document.getElementById('feedback').value;
        alert("Feedback submitted: " + feedback);
    }

    // Call this function when the page loads to display crypto addresses
    window.onload = function() {
        displayCryptoAddresses();
    };
</script>

</body>
</html>
