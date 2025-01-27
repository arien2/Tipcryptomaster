<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crypto Gambling</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            color: white;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .header {
            padding: 20px;
            background-color: #333;
            width: 100%;
            text-align: center;
        }

        .crypto-box, .feedback-box {
            display: none;
            margin-top: 20px;
        }

        .luxury-notification {
            display: none;
            background-color: #4CAF50;
            color: white;
            padding: 15px;
            text-align: center;
            position: fixed;
            top: 20px;
            width: 100%;
            font-size: 18px;
            z-index: 1000;
        }

        .luxury-notification.show {
            display: block;
        }

        .copy-btn {
            background-color: #ffcc00;
            padding: 10px;
            border: none;
            cursor: pointer;
            font-size: 14px;
        }

        .crypto-address {
            font-size: 12px;
            word-wrap: break-word;
            max-width: 200px;
        }

        .slot-machine {
            margin-top: 30px;
        }

        .reel {
            width: 80px;
            height: 80px;
            margin: 10px;
            background-color: #888;
            display: inline-block;
            text-align: center;
            line-height: 80px;
            font-size: 24px;
            color: white;
            border-radius: 5px;
        }

        .spinning {
            animation: spin 1s infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .redeem-box {
            margin-top: 30px;
            padding: 20px;
            background-color: #333;
            border-radius: 10px;
            width: 300px;
            text-align: center;
        }

        .redeem-btn {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border: none;
            cursor: pointer;
            font-size: 14px;
            width: 100%;
            margin-top: 10px;
        }

    </style>
</head>
<body>

    <div class="header">
        <h1>Welcome to Crypto Gambling</h1>
        <p>Your Coin Balance: <span id="coinBalance">1000</span></p>
        <button onclick="showCryptoBox()">Show Crypto Addresses</button>
        <button onclick="showFeedbackForm()">Give Feedback</button>
        <button onclick="showRedeemBox()">Redeem Coins</button>
    </div>

    <div class="crypto-box">
        <h2>Crypto Addresses:</h2>
        <p>Bitcoin (BTC): <span class="crypto-address">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</span><button class="copy-btn" onclick="copyAddress('bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48')">Copy</button></p>
        <p>XRP: <span class="crypto-address">riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ</span><button class="copy-btn" onclick="copyAddress('riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ')">Copy</button></p>
        <p>Solana (SOL): <span class="crypto-address">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</span><button class="copy-btn" onclick="copyAddress('CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c')">Copy</button></p>
        <p>BNB: <span class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span><button class="copy-btn" onclick="copyAddress('0x65793418b7a6b0Dced78d59AbD44041b1567BE63')">Copy</button></p>
        <p>Polygon (MATIC): <span class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span><button class="copy-btn" onclick="copyAddress('0x65793418b7a6b0Dced78d59AbD44041b1567BE63')">Copy</button></p>
        <p>Litecoin (LTC): <span class="crypto-address">Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc</span><button class="copy-btn" onclick="copyAddress('Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc')">Copy</button></p>
        <p>USDT (Ethereum): <span class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span><button class="copy-btn" onclick="copyAddress('0x65793418b7a6b0Dced78d59AbD44041b1567BE63')">Copy</button></p>
        <p>USDC (Ethereum): <span class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span><button class="copy-btn" onclick="copyAddress('0x65793418b7a6b0Dced78d59AbD44041b1567BE63')">Copy</button></p>
        <p>COSMOS (ATOM): <span class="crypto-address">cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n</span><button class="copy-btn" onclick="copyAddress('cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n')">Copy</button></p>
        <p>Trump (Solana): <span class="crypto-address">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</span><button class="copy-btn" onclick="copyAddress('CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c')">Copy</button></p>
        <p>Shiba Inu (Ethereum): <span class="crypto-address">0x65793418b7a6b0Dced78d59AbD44041b1567BE63</span><button class="copy-btn" onclick="copyAddress('0x65793418b7a6b0Dced78d59AbD44041b1567BE63')">Copy</button></p>
    </div>

    <div class="feedback-box">
        <textarea id="feedback" placeholder="Enter your feedback..."></textarea>
        <button onclick="submitFeedback()">Submit</button>
        <button onclick="cancelFeedbackForm()">Cancel</button>
    </div>

    <div class="luxury-notification" id="message"></div>

    <div class="slot-machine">
        <div class="reel">🍒</div>
        <div class="reel">🍊</div>
        <div class="reel">🍉</div>
        <br>
        <button onclick="spinSlotMachine()">Spin</button>
    </div>

    <div class="redeem-box">
        <h2>Redeem Coins</h2>
        <input type="text" id="redeemCode" placeholder="Enter code">
        <button class="redeem-btn" onclick="redeemCoins()">Redeem</button>
    </div>

    <script>
        // Crypto address copying
        function copyAddress(address) {
            const tempInput = document.createElement("input");
            tempInput.value = address;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);
            showLuxuryNotification("Address copied!");
        }

        // Show the crypto addresses box
        function showCryptoBox() {
            document.querySelector('.crypto-box').style.display = 'block';
        }

        // Show feedback form
        function showFeedbackForm() {
            document.querySelector('.feedback-box').style.display = 'block';
        }

        // Cancel feedback form
        function cancelFeedbackForm() {
            document.querySelector('.feedback-box').style.display = 'none';
        }
        // Submit feedback form
        function submitFeedback() {
            const feedbackText = document.getElementById('feedback').value;
            if (feedbackText) {
                showLuxuryNotification("Successfully sent to the owner!");
                document.getElementById('feedback').value = ''; // Clear the feedback box
            } else {
                showLuxuryNotification("Please enter your feedback!");
            }
        }

        // Show luxury notification
        function showLuxuryNotification(message) {
            const notification = document.getElementById('message');
            notification.innerText = message;
            notification.classList.add('show');
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Redeem Coins Functionality
        function redeemCoins() {
            const redeemCode = document.getElementById('redeemCode').value;

            const validCodes = {
                "100 coins": "a3B9kD7t",
                "500 coins": "r4F8mL2z",
                "1000 coins": "z9J3nU1h",
                "2000 coins": "h5Y2vQ4p",
                "5000 coins": "x8W2fL6o",
                "10000 coins": "q7T1wM5v",
                "15000 coins": "e3D7gR4y",
                "20000 coins": "p9Z5iK1b"
            };

            if (Object.values(validCodes).includes(redeemCode)) {
                let amount = 0;
                for (let key in validCodes) {
                    if (validCodes[key] === redeemCode) {
                        amount = parseInt(key.split(" ")[0]);
                        break;
                    }
                }
                // Increase user's coin balance
                const currentBalance = parseInt(document.getElementById('coinBalance').innerText);
                const newBalance = currentBalance + amount;
                document.getElementById('coinBalance').innerText = newBalance;
                showLuxuryNotification(`Successfully redeemed ${amount} coins!`);
            } else {
                showLuxuryNotification("Invalid code. Please try again.");
            }
            document.getElementById('redeemCode').value = ''; // Clear input
        }

        // Slot machine spin function
        function spinSlotMachine() {
            const fruits = ["🍒", "🍊", "🍉", "🍓", "🍍", "🍎"];
            const reel1 = document.querySelectorAll('.reel')[0];
            const reel2 = document.querySelectorAll('.reel')[1];
            const reel3 = document.querySelectorAll('.reel')[2];

            // Add spinning animation
            reel1.classList.add('spinning');
            reel2.classList.add('spinning');
            reel3.classList.add('spinning');

            // Randomize the reels after a short delay
            setTimeout(() => {
                const randomFruit1 = fruits[Math.floor(Math.random() * fruits.length)];
                const randomFruit2 = fruits[Math.floor(Math.random() * fruits.length)];
                const randomFruit3 = fruits[Math.floor(Math.random() * fruits.length)];

                reel1.classList.remove('spinning');
                reel2.classList.remove('spinning');
                reel3.classList.remove('spinning');

                reel1.innerText = randomFruit1;
                reel2.innerText = randomFruit2;
                reel3.innerText = randomFruit3;

                // Check if all the fruits match
                if (randomFruit1 === randomFruit2 && randomFruit2 === randomFruit3) {
                    showLuxuryNotification("Congratulations! You won 10,000 coins!");
                    const currentBalance = parseInt(document.getElementById('coinBalance').innerText);
                    const newBalance = currentBalance + 10000;
                    document.getElementById('coinBalance').innerText = newBalance;
                } else {
                    showLuxuryNotification("Sorry, no match. Try again!");
                }
            }, 2000);
        }
    </script>
</body>
</html>
