<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Crypto Tipping Site</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f5f5f5;
      margin: 0;
      padding: 0;
    }
    .container {
      padding: 20px;
    }
    h1 {
      margin-top: 20px;
    }
    .button {
      background-color: #007bff;
      color: white;
      border: none;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      margin: 10px;
    }
    .button.green {
      background-color: #28a745;
    }
    .button.red {
      background-color: #dc3545;
    }
    .crypto-box, .redeem-box, .feedback-box, .admin-box {
      display: none;
      margin-top: 20px;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 5px;
      padding: 20px;
    }
    .slot-machine {
      display: flex;
      justify-content: center;
      margin: 20px auto;
    }
    .slot-column {
      width: 80px;
      height: 80px;
      border: 2px solid #ccc;
      margin: 5px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      font-weight: bold;
      background-color: #fff;
    }
    .lever {
      margin: 20px auto;
      width: 40px;
      height: 150px;
      background-color: #ccc;
      border-radius: 20px;
      position: relative;
    }
    .lever-handle {
      width: 40px;
      height: 20px;
      background-color: gray;
      border-radius: 10px;
      position: absolute;
      bottom: -10px;
      left: 0;
      cursor: pointer;
    }
    .notification {
      margin-top: 20px;
      padding: 10px;
      font-weight: bold;
      border-radius: 5px;
    }
    .notification.green {
      background-color: #28a745;
      color: white;
    }
    .notification.red {
      background-color: #dc3545;
      color: white;
    }
    .notification.yellow {
      background-color: #ffc107;
      color: white;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Welcome to the Tipping Site</h1>
    <div>
      <button id="show-crypto-btn" class="button">Show Crypto Addresses</button>
      <button id="show-redeem-btn" class="button">Redeem Coins</button>
      <button id="show-feedback-btn" class="button">Give Feedback</button>
      <button id="show-admin-btn" class="button">Verify Admin</button>
    </div>

    <div id="crypto-box" class="crypto-box">
      <h2>Crypto Addresses</h2>
      <div><strong>Bitcoin:</strong> bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</div>
      <div><strong>Ethereum (USDT, USDC):</strong> 0x65793418b7a6b0Dced78d59AbD44041b1567BE63</div>
      <div><strong>XRP:</strong> riaJ77mQKU42oTv9b2p7KXZ25tYZWTVbQ</div>
      <div><strong>Solana (Trump Coin):</strong> CMmyoSQQrmAyrTdUg9XMfWosizxN7erCkHfMvd1NKx4c</div>
      <div><strong>BNB:</strong> 0x65793418b7a6b0Dced78d59AbD44041b1567BE63</div>
      <div><strong>Polygon:</strong> 0x65793418b7a6b0Dced78d59AbD44041b1567BE63</div>
      <div><strong>Litecoin:</strong> Lfadmh9uxk9pawfaH9muBZ5vkVQhkrN1kc</div>
      <div><strong>COSMOS (ATOM):</strong> cosmos1sm3tzv4jmv8ac9zul9fry0ped0d3y8kxxufk2n</div>
      <div><strong>Shiba Inu:</strong> 0x65793418b7a6b0Dced78d59AbD44041b1567BE63</div>
    </div>

    <div id="redeem-box" class="redeem-box">
      <h2>Redeem Coins</h2>
      <input type="text" id="redeem-code" placeholder="Enter redeem code">
      <button id="redeem-confirm-btn" class="button green">Redeem</button>
    </div>

    <div id="feedback-box" class="feedback-box">
      <h2>Feedback</h2>
      <textarea id="feedback-input" placeholder="Enter your feedback"></textarea>
      <button id="feedback-submit-btn" class="button green">Submit</button>
      <button id="feedback-cancel-btn" class="button red">Cancel</button>
    </div>

    <div id="admin-box" class="admin-box">
      <h2>Admin Verification</h2>
      <input type="text" id="admin-code" placeholder="Enter admin code">
      <button id="admin-confirm-btn" class="button green">Confirm</button>
    </div>

    <div id="slot-game">
      <h2>Slot Game</h2>
      <div id="slot-machine" class="slot-machine">
        <div class="slot-column">🍒</div>
        <div class="slot-column">🍋</div>
        <div class="slot-column">🍎</div>
      </div>
      <div class="lever">
        <div id="lever-handle" class="lever-handle"></div>
      </div>
      <button id="spin-btn" class="button green">Spin</button>
    </div>

    <div id="message" class="notification"></div>
  </div>
</body>
</html>
<script>
  document.addEventListener("DOMContentLoaded", () => {
    // Toggle visibility for Crypto, Redeem, Feedback, and Admin sections
    function toggleSection(button, section) {
      button.addEventListener("click", () => {
        const isVisible = section.style.display === "block";
        section.style.display = isVisible ? "none" : "block";
        button.classList.toggle("green", !isVisible);
      });
    }

    const cryptoBtn = document.getElementById("show-crypto-btn");
    const cryptoBox = document.getElementById("crypto-box");
    toggleSection(cryptoBtn, cryptoBox);

    const redeemBtn = document.getElementById("show-redeem-btn");
    const redeemBox = document.getElementById("redeem-box");
    toggleSection(redeemBtn, redeemBox);

    const feedbackBtn = document.getElementById("show-feedback-btn");
    const feedbackBox = document.getElementById("feedback-box");
    toggleSection(feedbackBtn, feedbackBox);

    const adminBtn = document.getElementById("show-admin-btn");
    const adminBox = document.getElementById("admin-box");
    toggleSection(adminBtn, adminBox);

    // Redeem coins functionality
    const redeemConfirmBtn = document.getElementById("redeem-confirm-btn");
    const redeemCodeInput = document.getElementById("redeem-code");
    const messageBox = document.getElementById("message");

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

    redeemConfirmBtn.addEventListener("click", () => {
      const code = redeemCodeInput.value.trim();
      if (redeemCodes[code]) {
        messageBox.textContent = `Successfully redeemed ${redeemCodes[code]} coins!`;
        messageBox.className = "notification green";
      } else {
        messageBox.textContent = "Invalid code. Please try again!";
        messageBox.className = "notification red";
      }
    });

    // Feedback form functionality
    const feedbackSubmitBtn = document.getElementById("feedback-submit-btn");
    const feedbackCancelBtn = document.getElementById("feedback-cancel-btn");

    feedbackSubmitBtn.addEventListener("click", () => {
      messageBox.textContent = "Feedback successfully sent to the owner!";
      messageBox.className = "notification green";
    });

    feedbackCancelBtn.addEventListener("click", () => {
      messageBox.textContent = "Successfully canceled.";
      messageBox.className = "notification green";
    });

    // Admin verification functionality
    const adminConfirmBtn = document.getElementById("admin-confirm-btn");
    const adminCodeInput = document.getElementById("admin-code");
    const validAdminCode = "admin123";

    adminConfirmBtn.addEventListener("click", () => {
      if (adminCodeInput.value === validAdminCode) {
        messageBox.textContent = "Successfully confirmed!";
        messageBox.className = "notification green";
      } else {
        messageBox.textContent = "Invalid!";
        messageBox.className = "notification red";
      }
    });

    // Slot game functionality
    const spinBtn = document.getElementById("spin-btn");
    const slotMachine = document.getElementById("slot-machine");
    const slotColumns = slotMachine.querySelectorAll(".slot-column");
    const leverHandle = document.getElementById("lever-handle");

    let spinning = false;

    spinBtn.addEventListener("click", () => {
      if (spinning) {
        messageBox.textContent = "Please wait until the countdown ends.";
        messageBox.className = "notification red";
        return;
      }

      spinning = true;
      spinBtn.disabled = true;
      leverHandle.style.transform = "rotate(45deg)";

      const fruits = ["🍒", "🍋", "🍎", "🍇", "🍉", "🍌"];
      slotColumns.forEach(column => {
        let count = 0;
        const spinInterval = setInterval(() => {
          column.textContent = fruits[Math.floor(Math.random() * fruits.length)];
          count++;
          if (count === 20) {
            clearInterval(spinInterval);
          }
        }, 100);
      });

      setTimeout(() => {
        leverHandle.style.transform = "rotate(0deg)";
        spinning = false;
        spinBtn.disabled = false;

        // Check if all columns match
        const results = Array.from(slotColumns).map(column => column.textContent);
        if (results.every(val => val === results[0])) {
          messageBox.textContent = "Congratulations! You won 10,000 coins!";
          messageBox.className = "notification yellow";
        } else {
          messageBox.textContent = "Sorry, no match.";
          messageBox.className = "notification red";
        }
      }, 2000);
    });
  });
</script>
