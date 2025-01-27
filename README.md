<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tipping Site</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
        }

        h1, h2 {
            text-align: center;
        }

        .button {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .button.green {
            background-color: #28a745;
        }

        .container {
            width: 80%;
            margin: 0 auto;
        }

        .hidden {
            display: none;
        }

        .notification {
            position: fixed;
            top: 10px;
            right: 10px;
            padding: 10px 20px;
            border-radius: 5px;
            color: white;
            font-size: 16px;
            opacity: 0;
            transform: translateY(-20px);
            transition: opacity 0.5s, transform 0.5s;
        }

        .notification.show {
            opacity: 1;
            transform: translateY(0);
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

        .crypto-box {
            margin-top: 20px;
            border: 1px solid #ddd;
            padding: 20px;
            border-radius: 10px;
            background: #fff;
        }

        .slot-machine {
            margin: 20px auto;
            padding: 20px;
            border: 2px solid #333;
            border-radius: 10px;
            text-align: center;
            background: #fff;
            width: 300px;
            height: 300px;
            position: relative;
        }

        .lever {
            position: absolute;
            top: 20px;
            right: -50px;
            width: 20px;
            height: 80px;
            background-color: gray;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s ease;
        }

        .lever.down {
            transform: rotate(30deg);
        }

        .reel {
            font-size: 36px;
            text-align: center;
            display: inline-block;
            width: 80px;
            height: 80px;
            line-height: 80px;
            border: 2px solid #333;
            margin: 5px;
            animation: spin 1s ease-in-out;
        }

        @keyframes spin {
            0% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-30px);
            }
            100% {
                transform: translateY(0);
            }
        }
    </style>
</head>
<body>
    <h1>Welcome to the Tipping Site</h1>
    <div class="container">
        <!-- Buttons -->
        <button class="button" id="showAddressesBtn" onclick="toggleAddresses()">Show Addresses</button>
        <button class="button" id="giveFeedbackBtn" onclick="toggleFeedback()">Give Feedback</button>
        <button class="button" id="redeemCoinsBtn" onclick="toggleRedeemCoins()">Redeem Coins</button>
        <button class="button" id="adminVerificationBtn" onclick="toggleAdminVerification()">Admin Verification</button>

        <!-- Crypto Addresses Section -->
        <div id="cryptoAddresses" class="hidden">
            <h2>Crypto Addresses</h2>
            <div class="crypto-box">
                <strong>Bitcoin:</strong> bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48
                <button onclick="copyToClipboard('bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48')">Copy</button>
            </div>
            <div class="crypto-box">
                <strong>XRP:</strong> riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ
                <button onclick="copyToClipboard('riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ')">Copy</button>
            </div>
            <!-- Repeat for other cryptocurrencies -->
        </div>

        <!-- Feedback Section -->
        <div id="feedbackForm" class="hidden">
            <textarea id="feedback" placeholder="Enter your feedback..."></textarea>
            <button class="button green" onclick="submitFeedback()">Submit</button>
            <button class="button" onclick="cancelFeedback()">Cancel</button>
        </div>

        <!-- Redeem Coins Section -->
        <div id="redeemCoinsForm" class="hidden">
            <input type="text" id="redeemCode" placeholder="Enter redeem code" />
            <button class="button" onclick="redeemCoins()">Redeem</button>
        </div>

        <!-- Admin Verification Section -->
        <div id="adminVerificationForm" class="hidden">
            <input type="text" id="adminCode" placeholder="Enter admin code" />
            <button class="button green" onclick="verifyAdmin()">Confirm</button>
        </div>

        <!-- Slot Machine -->
        <div class="slot-machine">
            <div class="reel">🍒</div>
            <div class="reel">🍊</div>
            <div class="reel">🍋</div>
            <div class="lever" id="lever" onclick="spinSlotMachine()"></div>
        </div>

        <!-- Coin Balance -->
        <p>Coin Balance: <span id="coinBalance">0</span></p>
    </div>
<script>
        // Global variables
        let coinBalance = 0;
        let slotCooldown = false;

        // Utility function for notifications
        function showMessage(message, colorClass) {
            const messageDiv = document.getElementById("message");
            messageDiv.textContent = message;
            messageDiv.className = `notification ${colorClass} show`;
            setTimeout(() => {
                messageDiv.className = "notification";
            }, 3000);
        }

        // Toggle crypto addresses
        function toggleAddresses() {
            const addresses = document.getElementById("cryptoAddresses");
            const button = document.getElementById("showAddressesBtn");
            if (addresses.classList.contains("hidden")) {
                addresses.classList.remove("hidden");
                button.classList.add("green");
            } else {
                addresses.classList.add("hidden");
                button.classList.remove("green");
            }
        }

        // Toggle feedback form
        function toggleFeedback() {
            const feedback = document.getElementById("feedbackForm");
            const button = document.getElementById("giveFeedbackBtn");
            if (feedback.classList.contains("hidden")) {
                feedback.classList.remove("hidden");
                button.classList.add("green");
            } else {
                feedback.classList.add("hidden");
                button.classList.remove("green");
            }
        }

        // Submit feedback
        function submitFeedback() {
            const feedback = document.getElementById("feedback").value;
            if (feedback.trim() !== "") {
                showMessage("Successfully sent to the owner!", "green");
                document.getElementById("feedback").value = "";
                toggleFeedback();
            } else {
                showMessage("Please enter valid feedback!", "red");
            }
        }

        // Cancel feedback
        function cancelFeedback() {
            showMessage("Successfully cancelled", "green");
            toggleFeedback();
        }

        // Toggle redeem coins
        function toggleRedeemCoins() {
            const redeemForm = document.getElementById("redeemCoinsForm");
            const button = document.getElementById("redeemCoinsBtn");
            if (redeemForm.classList.contains("hidden")) {
                redeemForm.classList.remove("hidden");
                button.classList.add("green");
            } else {
                redeemForm.classList.add("hidden");
                button.classList.remove("green");
            }
        }

        // Redeem coins
        function redeemCoins() {
            const redeemCode = document.getElementById("redeemCode").value;
            const codes = {
                "a3B9kD7t": 100,
                "r4F8mL2z": 500,
                "z9J3nU1h": 1000,
                "h5Y2vQ4p": 2000,
                "x8W2fL6o": 5000,
                "q7T1wM5v": 10000,
                "e3D7gR4y": 15000,
                "p9Z5iK1b": 20000,
            };

            if (codes[redeemCode]) {
                coinBalance += codes[redeemCode];
                document.getElementById("coinBalance").textContent = coinBalance;
                showMessage(`Successfully redeemed ${codes[redeemCode]} coins!`, "green");
                toggleRedeemCoins();
            } else {
                showMessage("Invalid code. Please try again!", "red");
            }
        }

        // Toggle admin verification
        function toggleAdminVerification() {
            const adminForm = document.getElementById("adminVerificationForm");
            const button = document.getElementById("adminVerificationBtn");
            if (adminForm.classList.contains("hidden")) {
                adminForm.classList.remove("hidden");
                button.classList.add("green");
            } else {
                adminForm.classList.add("hidden");
                button.classList.remove("green");
            }
        }

        // Admin verification
        function verifyAdmin() {
            const adminCode = document.getElementById("adminCode").value;
            const validAdminCode = "admin123"; // Example admin code

            if (adminCode === validAdminCode) {
                showMessage("Successfully confirmed!", "green");
                toggleAdminVerification();
            } else {
                showMessage("Invalid!", "red");
            }
        }

        // Slot Machine
        function spinSlotMachine() {
            if (coinBalance < 1000) {
                showMessage("Insufficient coins to play!", "red");
                return;
            }

            if (slotCooldown) {
                showMessage("Please wait until the countdown ends", "red");
                return;
            }

            coinBalance -= 1000;
            document.getElementById("coinBalance").textContent = coinBalance;

            slotCooldown = true;
            const lever = document.getElementById("lever");
            const reels = document.querySelectorAll(".reel");

            // Pull the lever animation
            lever.classList.add("down");
            setTimeout(() => {
                lever.classList.remove("down");
            }, 300);

            // Start spinning
            const fruits = ["🍒", "🍊", "🍋", "🍉", "🍇", "🍓"];
            let results = [];
            reels.forEach((reel, index) => {
                setTimeout(() => {
                    let randomFruit = fruits[Math.floor(Math.random() * fruits.length)];
                    results[index] = randomFruit;
                    reel.textContent = randomFruit;
                }, index * 200);
            });

            // Determine result
            setTimeout(() => {
                const allMatch = results.every((fruit) => fruit === results[0]);
                if (allMatch) {
                    coinBalance += 10000;
                    document.getElementById("coinBalance").textContent = coinBalance;
                    showMessage("Congratulations! You won 10,000 coins!", "yellow");
                } else {
                    showMessage("Sorry, no match.", "red");
                }

                // Cooldown ends
                setTimeout(() => {
                    slotCooldown = false;
                }, 10000); // 10-second cooldown
            }, 1000);
        }

        // Copy to clipboard
        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                showMessage("Copied to clipboard!", "green");
            });
        }
    </script>
</body>
</html>
    <div id="message" class="notification"></div>
