<!DOCTYPE html>
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
    <div class="address-box">
        <div class="address">Bitcoin: bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</div>
        <button class="copy-btn" onclick="copyToClipboard('Bitcoin')">Copy</button>
    </div>
    <div class="address-box">
        <div class="address">Ethereum: 0x65793418b7a6b0Dced78d59AbD44041b1567BE63</div>
        <button class="copy-btn" onclick="copyToClipboard('Ethereum')">Copy</button>
    </div>
    <div class="address-box">
        <div class="address">XRP: riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ</div>
        <button class="copy-btn" onclick="copyToClipboard('XRP')">Copy</button>
    </div>
    <!-- Add all other addresses here -->

    <h3>Current Coin Balance: <span id="coinBalance">0</span> coins</h3>

    <!-- Admin Verification -->
    <div id="verificationBox">
        <input type="text" id="adminCode" placeholder="Enter Admin Code">
        <button onclick="verifyAdmin()">Verify Admin</button>
    </div>

    <div id="message" class="notification"></div>

    <!-- Redeem Coins -->
    <div class="redeem-box">
        <h4>Redeem Coins:</h4>
        <input type="text" id="redeemCode" placeholder="Enter Code">
        <button onclick="redeemCoins()">Redeem</button>
    </div>

    <div id="redeemMessage" class="feedback-message"></div>

    <!-- Simple Slot Game -->
    <div class="game-container">
        <h3>Slot Game - 1000 Coins to Play!</h3>
        <div id="slotGame" class="slot-game">
            <button onclick="playSlotGame()">Spin</button>
        </div>
    </div>

    <!-- Feedback Form -->
    <div class="feedback-form">
        <button class="feedback-button" onclick="showFeedbackForm()">Give Feedback</button>
        <div class="feedback-box">
            <textarea id="feedbackInput" placeholder="Enter your feedback here"></textarea><br>
            <button onclick="submitFeedback()">Submit Feedback</button>
            <button onclick="closeFeedbackForm()">Decline</button>
        </div>
    </div>
</div>

<script>
    let coinBalance = 0;
    let isAdmin = false;

    const adminCode = "Ariengambleswhilebeingabillionaire";
    const redeemCodes = {
        'a3B9kD7t': 100,
        'r4F8mL2z': 500,
        'z9J3nU1h': 1000,
        'h5Y2vQ4p': 2000,
        'x8W2fL6o': 5000,
        'q7T1wM5v': 10000,
        'e3D7gR4y': 15000,
        'p9Z5iK1b': 20000
    };

    // Admin Verification
    function verifyAdmin() {
        const enteredCode = document.getElementById('adminCode').value;

        if (enteredCode === adminCode) {
            isAdmin = true;
            coinBalance = 999999999; // Admin gets infinite coins
            document.getElementById('message').innerHTML = "Admin Verified! You now have infinite coins.";
            document.getElementById('coinBalance').innerHTML = coinBalance;
        } else {
            document.getElementById('message').innerHTML = "Incorrect Admin Code!";
        }
    }

    // Copy Address Function
    function copyToClipboard(addressType) {
        let address;
        if (addressType === "Bitcoin") address = "bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48";
        if (addressType === "Ethereum") address = "0x65793418b7a6b0Dced78d59AbD44041b1567BE63";
        if (addressType === "XRP") address = "riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ";
        // Add other addresses

        const tempInput = document.createElement("input");
        tempInput.value = address;
        document.body.appendChild(tempInput);
        tempInput.select();
        document.execCommand("copy");
        document.body.removeChild(tempInput);
    }

    // Redeem Coins
    function redeemCoins() {
        const code = document.getElementById('redeemCode').value;
        const message = document.getElementById('redeemMessage');

        if (redeemCodes[code]) {
            coinBalance += redeemCodes[code];
            message.className = 'correct';
            message.innerHTML = `Successfully redeemed ${redeemCodes[code]} coins! Your balance is now ${coinBalance} coins.`;
        } else {
            message.className = 'incorrect';
            message.innerHTML = "Incorrect Code!";
        }
    }

    // Slot Game
    function playSlotGame() {
        if (coinBalance >= 1000) {
            coinBalance -= 1000;
            document.getElementById('coinBalance').innerHTML = coinBalance;
            const fruits = ["🍎", "🍊", "🍒", "🍓", "🍉"];
            const result = [
                fruits[Math.floor(Math.random() * fruits.length)],
                fruits[Math.floor(Math.random() * fruits.length)],
                fruits[Math.floor(Math.random() * fruits.length)]
            ];
            alert(`You spun: ${result.join(' ')}`);
            if (result[0] === result[1] && result[1] === result[2]) {
                coinBalance += 1000;
                document.getElementById('coinBalance').innerHTML = coinBalance;
                alert("You won 1000 coins!");
            }
        } else {
            alert("You need 1000 coins to play!");
        }
    }

    // Feedback Form
    function showFeedbackForm() {
        document.querySelector('.feedback-box').style.display = 'block';
    }

    function submitFeedback() {
        const feedback = document.getElementById('feedbackInput').value;
        alert("Successfully sent to the owner!");
        document.querySelector('.feedback-box').style.display = 'none';
    }

    function closeFeedbackForm() {
        document.querySelector('.feedback-box').style.display = 'none';
    }
</script>

</body>
</html>
