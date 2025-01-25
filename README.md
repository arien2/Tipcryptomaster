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
            font-size: 14px; /* Address font size adjustment */
            color: red; /* Changed to red */
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

    <div class="feedback-popup" id="feedback-popup">
        <h3>User Feedback</h3>
        <textarea id="feedback-text" rows="4" cols="50" placeholder="Enter your feedback"></textarea><br><br>
        <button class="feedback-btn" onclick="sendFeedback()">Send Feedback</button>
        <button class="feedback-btn" onclick="closeFeedback()">Decline</button>
    </div>

    <footer>
        <p>Thank you for your support!</p>
    </footer>

    <script>
        // Copy to Clipboard
        function copyToClipboard(id) {
            var copyText = document.getElementById(id);
            var textArea = document.createElement('textarea');
            textArea.value = copyText.innerText;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand('copy');
            document.body.removeChild(textArea);
            alert("Address copied to clipboard");
        }

        // Feedback Popup
        function sendFeedback() {
            alert("Successfully sent to the owner!");
            closeFeedback();
        }

        function closeFeedback() {
            document.getElementById('feedback-popup').style.display = 'none';
        }

        // Admin Verification
        let isAdmin = false;

        // Verification function on page load
        window.onload = function() {
            verifyAdmin();
            updateCoinBalance();
        }

        function verifyAdmin() {
            setTimeout(function() {
                let verificationCode = prompt("This verification is only to detect if you are an admin or not. If you're not an admin, please click the decline button.\nEnter verification code:");

                if (verificationCode === "Letsgogamblingwhilebeingabillionaire") {
                    alert("Successful!");
                    isAdmin = true;
                    updateCoinBalance();
                } else {
                    alert("INVALID!");
                }
            }, 1000);
        }

        // Coin Balance Function
        let coinBalance = 0;
        function updateCoinBalance()
