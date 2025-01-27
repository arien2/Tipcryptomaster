<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to the Tipping Site</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-color: #f4f4f4;
        }

        .button {
            padding: 10px 20px;
            margin: 10px;
            border: none;
            cursor: pointer;
            background-color: #007BFF;
            color: white;
            border-radius: 5px;
        }

        .button.green {
            background-color: #28a745;
        }

        .hidden {
            display: none;
        }

        .crypto-box {
            border: 1px solid #ccc;
            padding: 15px;
            margin: 10px auto;
            max-width: 600px;
            text-align: left;
            background-color: #fff;
            border-radius: 5px;
        }

        .crypto-box h3 {
            margin-top: 0;
        }

        #slotMachine {
            margin-top: 20px;
            display: flex;
            justify-content: center;
            gap: 5px;
        }

        .reel {
            width: 60px;
            height: 60px;
            border: 1px solid #000;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #fff;
            font-size: 24px;
        }

        #lever {
            margin-top: 20px;
            height: 80px;
            width: 20px;
            background-color: #ccc;
            position: relative;
            display: inline-block;
        }

        #lever.down {
            background-color: #888;
        }

        #redeemCoinsForm button {
            background-color: #28a745 !important; /* Redeem button is green */
        }

        .notification {
            display: none;
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            padding: 10px;
            border-radius: 5px;
            color: white;
            font-size: 16px;
        }

        .notification.red {
            background-color: #dc3545;
        }

        .notification.green {
            background-color: #28a745;
        }

        .notification.yellow {
            background-color: #ffc107;
        }
    </style>
</head>
<body>
    <h1>Welcome to the Tipping Site</h1>
    <p>Tip your favorite creators using cryptocurrency!</p>

    <div>
        <button class="button" id="showAddressesBtn" onclick="toggleAddresses()">Show Crypto Addresses</button>
        <button class="button" id="giveFeedbackBtn" onclick="toggleFeedback()">Give Feedback</button>
        <button class="button" id="redeemCoinsBtn" onclick="toggleRedeemCoins()">Redeem Coins</button>
        <button class="button" id="adminVerificationBtn" onclick="toggleAdminVerification()">Verify You're Admin</button>
    </div>

    <div id="cryptoAddresses" class="crypto-box hidden">
        <h3>Crypto Addresses</h3>
        <p>Bitcoin (BTC): bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48 <button onclick="copyToClipboard('bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48')">Copy</button></p>
        <p>XRP: riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ <button onclick="copyToClipboard('riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ')">Copy</button></p>
        <p>Solana (SOL): CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c <button onclick="copyToClipboard('CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c')">Copy</button></p>
        <!-- Add other addresses similarly -->
    </div>

    <div id="feedbackForm" class="crypto-box hidden">
        <h3>Give Feedback</h3>
        <textarea id="feedback" rows="5" placeholder="Enter your feedback"></textarea><br>
        <button class="button" onclick="submitFeedback()">Submit</button>
        <button class="button" onclick="cancelFeedback()">Cancel</button>
    </div>

    <div id="redeemCoinsForm" class="crypto-box hidden">
        <h3>Redeem Coins</h3>
        <input type="text" id="redeemCode" placeholder="Enter redeem code"><br>
        <button class="button">Redeem</button>
    </div>

    <div id="adminVerificationForm" class="crypto-box hidden">
        <h3>Admin Verification</h3>
        <input type="password" id="adminCode" placeholder="Enter admin code"><br>
        <button class="button" onclick="verifyAdmin()">Confirm</button>
    </div>

    <div>
        <h3>Coin Balance: <span id="coinBalance">0</span></h3>
        <div id="slotMachine">
            <div class="reel">🍒</div>
            <div class="reel">🍒</div>
            <div class="reel">🍒</div>
        </div>
        <div id="lever" onclick="spinSlotMachine()"></div>
    </div>

    <script>
        // Add the script logic for toggles, notifications, and slot functionality.
    </script>
</body>
</html>
<script>
    // Coin Balance
    let coinBalance = 0;
    const balanceDisplay = document.getElementById("coinBalance");

    // Toggles for various sections
    function toggleAddresses() {
        const addresses = document.getElementById("cryptoAddresses");
        const button = document.getElementById("showAddressesBtn");
        addresses.classList.toggle("hidden");
        button.classList.toggle("green");
    }

    function toggleFeedback() {
        const feedback = document.getElementById("feedbackForm");
        const button = document.getElementById("giveFeedbackBtn");
        feedback.classList.toggle("hidden");
        button.classList.toggle("green");
    }

    function toggleRedeemCoins() {
        const redeem = document.getElementById("redeemCoinsForm");
        const button = document.getElementById("redeemCoinsBtn");
        redeem.classList.toggle("hidden");
        button.classList.toggle("green");
    }

    function toggleAdminVerification() {
        const adminForm = document.getElementById("adminVerificationForm");
        const button = document.getElementById("adminVerificationBtn");
        adminForm.classList.toggle("hidden");
        button.classList.toggle("green");
    }

    // Feedback functionality
    function submitFeedback() {
        showNotification("Feedback successfully sent to the owner!", "green");
    }

    function cancelFeedback() {
        document.getElementById("feedback").value = "";
        showNotification("Successfully cancelled", "green");
    }

    // Redeem Coins functionality
    const redeemCodes = {
        "a3B9kD7t": 100,
        "r4F8mL2z": 500,
        "z9J3nU1h": 1000,
        "h5Y2vQ4p": 2000,
        "x8W2fL6o": 5000,
        "q7T1wM5v": 10000,
        "e3D7gR4y": 15000,
        "p9Z5iK1b": 20000,
    };

    function redeemCoins() {
        const code = document.getElementById("redeemCode").value.trim();
        if (redeemCodes[code]) {
            coinBalance += redeemCodes[code];
            balanceDisplay.textContent = coinBalance;
            showNotification("Successfully redeemed " + redeemCodes[code] + " coins!", "green");
        } else {
            showNotification("Invalid code. Please try again!", "red");
        }
    }

    // Slot Machine functionality
    const slotReels = document.querySelectorAll(".reel");
    const lever = document.getElementById("lever");
    let cooldown = false;

    function spinSlotMachine() {
        if (cooldown) {
            showNotification("Please wait until the countdown ends", "red");
            return;
        }

        if (coinBalance < 1000) {
            showNotification("Insufficient coins! You need 1,000 coins to play.", "red");
            return;
        }

        // Deduct coins and start the spin
        coinBalance -= 1000;
        balanceDisplay.textContent = coinBalance;
        lever.classList.add("down");
        setTimeout(() => lever.classList.remove("down"), 500);

        // Simulate spinning reels
        const fruits = ["🍒", "🍋", "🍇", "🍉", "🍊", "🍓"];
        const results = [];
        slotReels.forEach((reel, index) => {
            setTimeout(() => {
                const randomFruit = fruits[Math.floor(Math.random() * fruits.length)];
                results.push(randomFruit);
                reel.textContent = randomFruit;
            }, index * 300);
        });

        // Check results after the spin
        setTimeout(() => {
            const win = results.every(fruit => fruit === results[0]);
            if (win) {
                coinBalance += 10000;
                balanceDisplay.textContent = coinBalance;
                showNotification("Jackpot! You won 10,000 coins!", "yellow");
            } else {
                showNotification("Sorry, no match.", "red");
            }
        }, 1200);

        // Start cooldown
        cooldown = true;
        setTimeout(() => cooldown = false, 10000);
    }

    // Admin Verification functionality
    const adminCode = "secureAdmin123";
    function verifyAdmin() {
        const inputCode = document.getElementById("adminCode").value.trim();
        if (inputCode === adminCode) {
            showNotification("Successfully confirmed!", "green");
        } else {
            showNotification("Invalid!", "red");
        }
    }

    // Copy to Clipboard functionality
    function copyToClipboard(text) {
        navigator.clipboard.writeText(text).then(() => {
            showNotification("Copied to clipboard!", "green");
        }).catch(() => {
            showNotification("Failed to copy.", "red");
        });
    }

    // Notification functionality
    function showNotification(message, color) {
        const notification = document.createElement("div");
        notification.className = `notification ${color}`;
        notification.textContent = message;
        document.body.appendChild(notification);

        setTimeout(() => {
            notification.remove();
        }, 3000);
    }
</script>
