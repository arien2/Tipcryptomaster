<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tipping Site</title>
    <style>
        /* General styles for the page */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
        }
        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 20px;
        }
        .button {
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
            margin-top: 10px;
        }
        .button:hover {
            background-color: #218838;
        }
        .hidden {
            display: none;
        }
        .notification {
            margin-top: 10px;
            padding: 10px;
            background-color: #28a745;
            color: white;
            border-radius: 5px;
        }
        .notification.error {
            background-color: #dc3545;
        }
        .notification.success {
            background-color: #28a745;
        }
        .coin-balance {
            margin-top: 20px;
        }
        .coin-balance span {
            font-weight: bold;
        }
        .slot-machine {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 30px;
            position: relative;
        }
        .slot {
            width: 100px;
            height: 100px;
            background-color: grey;
            margin: 10px;
            border-radius: 10px;
        }
        .lever {
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            position: absolute;
            left: -120px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
        }
        .lever:hover {
            background-color: #0056b3;
        }
        .lever:active {
            transform: translateY(-50%) translateX(5px);
        }
        .slot span {
            display: block;
            text-align: center;
            font-size: 20px;
            line-height: 100px;
            color: white;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>Welcome to the Tipping Site</h1>
    <div class="coin-balance">
        <h3>Coin Balance: <span id="coinBalance">0</span> Coins</h3>
    </div>
    <!-- Admin Verification -->
    <button class="button" id="adminVerificationBtn">Verify Admin</button>
    <div id="adminVerification" class="hidden">
        <input type="text" id="adminCode" placeholder="Enter Admin Code">
        <button class="button" id="adminVerifyBtn">Verify</button>
        <div id="adminVerificationMessage" class="notification hidden"></div>
    </div>

    <!-- Redeem Coins -->
    <button class="button" id="redeemCoinsBtn">Redeem Coins</button>
    <div id="redeemCoinsBox" class="hidden">
        <input type="text" id="redeemCode" placeholder="Enter Redeem Code">
        <button class="button" id="redeemVerifyBtn">Redeem</button>
        <div id="redeemMessage" class="notification hidden"></div>
    </div>
    <!-- Crypto Addresses -->
    <button class="button" id="showAddressesBtn">Show Crypto Addresses</button>
    <div id="cryptoAddresses" class="hidden">
        <div id="bitcoinAddress">
            Bitcoin (BTC): <span id="btcAddress">bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</span>
            <button class="button" id="copyBtcBtn">Copy</button>
        </div>
        <div id="xrpAddress">
            XRP: <span id="xrpAddressSpan">riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ</span>
            <button class="button" id="copyXrpBtn">Copy</button>
        </div>
        <div id="solanaAddress">
            Solana: <span id="solanaAddressSpan">CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</span>
            <button class="button" id="copySolanaBtn">Copy</button>
        </div>
    </div>
    <!-- Slot Machine -->
    <div class="slot-machine">
        <div class="slot" id="slot1"><span id="fruit1">🍒</span></div>
        <div class="slot" id="slot2"><span id="fruit2">🍇</span></div>
        <div class="slot" id="slot3"><span id="fruit3">🍊</span></div>
        <button class="lever" id="leverBtn">Pull Lever</button>
    </div>

    <script>
        // Coin balance initialization
        let coinBalance = 0;
        const coinBalanceElement = document.getElementById('coinBalance');

        // Admin verification
        const adminVerificationBtn = document.getElementById('adminVerificationBtn');
        const adminVerificationBox = document.getElementById('adminVerification');
        const adminCodeInput = document.getElementById('adminCode');
        const adminVerifyBtn = document.getElementById('adminVerifyBtn');
        const adminVerificationMessage = document.getElementById('adminVerificationMessage');
        
        adminVerificationBtn.addEventListener('click', () => {
            adminVerificationBox.classList.toggle('hidden');
        });

        adminVerifyBtn.addEventListener('click', () => {
            const code = adminCodeInput.value;
            if (code === 'admin123') {
                adminVerificationMessage.textContent = 'Successfully confirmed!';
                adminVerificationMessage.classList.remove('hidden');
                adminVerificationMessage.classList.add('success');
            } else {
                adminVerificationMessage.textContent = 'Invalid code!';
                adminVerificationMessage.classList.remove('hidden');
                adminVerificationMessage.classList.add('error');
            }
        });

        // Redeem coins functionality
        const redeemCoinsBtn = document.getElementById('redeemCoinsBtn');
        const redeemCoinsBox = document.getElementById('redeemCoinsBox');
        const redeemCodeInput = document.getElementById('redeemCode');
        const redeemVerifyBtn = document.getElementById('redeemVerifyBtn');
        const redeemMessage = document.getElementById('redeemMessage');

        redeemCoinsBtn.addEventListener('click', () => {
            redeemCoinsBox.classList.toggle('hidden');
        });

        redeemVerifyBtn.addEventListener('click', () => {
            const code = redeemCodeInput.value;
            const redeemMessages = {
                'a3B9kD7t': 100,
                'r4F8mL2z': 500,
                'z9J3nU1h': 1000,
                'h5Y2vQ4p': 2000,
                'x8W2fL6o': 5000,
                'q7T1wM5v': 10000,
                'e3D7gR4y': 15000,
                'p9Z5iK1b': 20000,
            };
            if (redeemMessages[code]) {
                coinBalance += redeemMessages[code];
                coinBalanceElement.textContent = coinBalance;
                redeemMessage.textContent = `Successfully redeemed ${redeemMessages[code]} coins!`;
                redeemMessage.classList.remove('hidden');
                redeemMessage.classList.add('success');
            } else {
                redeemMessage.textContent = 'Invalid code. Please try again!';
                redeemMessage.classList.remove('hidden');
                redeemMessage.classList.add('error');
            }
        });
        // Crypto addresses display
        const showAddressesBtn = document.getElementById('showAddressesBtn');
        const cryptoAddresses = document.getElementById('cryptoAddresses');
        showAddressesBtn.addEventListener('click', () => {
            cryptoAddresses.classList.toggle('hidden');
            showAddressesBtn.classList.toggle('green');
        });

        // Copy buttons functionality
        document.getElementById('copyBtcBtn').addEventListener('click', () => {
            navigator.clipboard.writeText(document.getElementById('btcAddress').textContent);
        });
        document.getElementById('copyXrpBtn').addEventListener('click', () => {
            navigator.clipboard.writeText(document.getElementById('xrpAddressSpan').textContent);
        });
        document.getElementById('copySolanaBtn').addEventListener('click', () => {
            navigator.clipboard.writeText(document.getElementById('solanaAddressSpan').textContent);
        });

        // Slot machine functionality
        let isSpinning = false;
        const leverBtn = document.getElementById('leverBtn');
        let fruits = ['🍒', '🍇', '🍊', '🍉', '🍓', '🍍'];

        leverBtn.addEventListener('click', () => {
            if (isSpinning) return;
            isSpinning = true;
            leverBtn.disabled = true;

            // Slot animation
            let slot1 = document.getElementById('fruit1');
            let slot2 = document.getElementById('fruit2');
            let slot3 = document.getElementById('fruit3');

            const spinSlot = (slot) => fruits[Math.floor(Math.random() * fruits.length)];

            slot1.textContent = spinSlot();
            slot2.textContent = spinSlot();
            slot3.textContent = spinSlot();

            setTimeout(() => {
                isSpinning = false;
                leverBtn.disabled = false;
            }, 1000); // Duration of spin
        });
    </script>
</body>
</html>
