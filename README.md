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

        h1, h3, p {
            font-size: 1.8em;
        }

        .crypto-address {
            font-weight: bold;
            background: #eaeaea;
            padding: 10px;
            border-radius: 5px;
            display: inline-block;
            margin-bottom: 20px;
            color: yellow;
        }

        .goal {
            margin: 20px auto;
            font-size: 1.5em;
            color: #28a745;
            font-weight: bold;
            width: 80%;
            background-color: #333;
            border-radius: 10px;
            padding: 5px;
        }

        .progress-bar {
            height: 30px;
            border-radius: 10px;
            background: #eaeaea;
            width: 100%;
            margin: 5px 0;
        }

        .progress-bar-fill {
            height: 100%;
            width: 0;
            background: green;
            border-radius: 10px;
        }

        footer {
            margin-top: 30px;
            font-size: 0.9em;
            color: #ccc;
        }

        .notification {
            display: none;
            background-color: green;
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin-top: 20px;
        }

        .popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #fff;
            color: #000;
            padding: 20px;
            border-radius: 10px;
            z-index: 999;
        }

        .popup input {
            padding: 5px;
            font-size: 1.2em;
        }

        .popup button {
            padding: 10px 20px;
            margin-top: 10px;
        }

        .popup .decline {
            background-color: red;
            color: white;
        }

        .popup .confirm {
            background-color: green;
            color: white;
        }

        .coin-balance {
            font-size: 1.5em;
            margin-top: 20px;
        }

        .feedback {
            font-size: 1.2em;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>Welcome to Tip CryptoGuy</h1>
    <p>Your tips help me achieve my goals!</p>

    <h3>Tip me with Bitcoin (BTC):</h3>
    <p class="crypto-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</p>

    <h3>Tip me with Ethereum (ETH):</h3>
    <p class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>

    <h3>Tip me with XRP:</h3>
    <p class="crypto-address">riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ</p>

    <h3>Tip me with Solana (SOL):</h3>
    <p class="crypto-address">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</p>

    <h3>Tip me with Binance Coin (BNB):</h3>
    <p class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>

    <h3>Tip me with Polygon (MATIC):</h3>
    <p class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>

    <h3>Tip me with Litecoin (LTC):</h3>
    <p class="crypto-address">Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc</p>

    <h3>Tip me with USDT (Ethereum Network):</h3>
    <p class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>

    <h3>Tip me with USDC (Ethereum Network):</h3>
    <p class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>

    <h3>Tip me with Cosmos (ATOM):</h3>
    <p class="crypto-address">cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n</p>

    <h3>Tip me with Shiba Inu (Ethereum Network):</h3>
    <p class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>

    <div class="goal">
        <div>Current Donations: $0 / $10,000</div>
        <div class="progress-bar">
            <div class="progress-bar-fill" style="width: 0%"></div>
        </div>
    </div>

    <div class="coin-balance">
        Coin Balance: 0
    </div>

    <div class="feedback">
        <button onclick="showFeedback()">Give Feedback</button>
    </div>

    <div id="popup" class="popup">
        <div>This verification is only to detect if you are admin or not. If you're not an admin, please click the decline button.</div>
        <input type="text" id="verificationCode" placeholder="Enter secret verification code">
        <button class="decline" onclick="declineVerification()">Decline</button>
        <button class="confirm" onclick="confirmVerification()">Confirm</button>
    </div>

    <div id="notification" class="notification"></div>

    <footer>
        <p>Thank you for your support!</p>
    </footer>

    <script>
        let isAdmin = false;
        let coins = 0;

        function showFeedback() {
            let feedback = prompt("Please leave your feedback:");
            if (feedback) {
                alert("Successfully sent to the owner!");
            }
        }

        function declineVerification() {
            document.getElementById('popup').style.display = 'none';
        }

        function confirmVerification() {
            const verificationCode = document.getElementById('verificationCode').value;

            if (verificationCode === "Letsgogamblingwhilebeingabillionaire") {
                isAdmin = true;
                coins = Infinity;
                showNotification("Successfully Verified! Infinite coins granted.", "green");
            } else {
                showNotification("INVALID! Wrong code.", "red");
            }

            document.getElementById('popup').style.display = 'none';
        }

        function showNotification(message, color) {
            const notification = document.getElementById('notification');
            notification.innerText = message;
            notification.style.backgroundColor = color;
            notification.style.display = 'block';
            setTimeout(() => notification.style.display = 'none', 3000);
        }

        function updateDonationGoal(percentage) {
            const progressBar = document.querySelector('.progress-bar-fill');
            progressBar.style.width = percentage + '%';
        }

        // Simulate donation updates (for demo purposes)
        setInterval(() => {
            let randomDonation = Math.floor(Math.random() * 100);
            let goalPercentage = randomDonation;
            updateDonationGoal(goalPercentage);
        }, 5000); // Update every 5 seconds for demonstration

        // Show pop-up when page loads
        window.onload = () => {
            document.getElementById('popup').style.display = 'block';
        };
    </script>
</body>
</html>
