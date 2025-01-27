<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Crypto Tipping Site</title>
  <style>
    /* Add your styles here */
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }

    .button {
      padding: 10px 20px;
      margin: 5px;
      cursor: pointer;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    .button.green {
      background-color: #28a745;
      color: #fff;
    }

    .button.red {
      background-color: #dc3545;
      color: #fff;
    }

    .notification {
      margin-top: 10px;
      padding: 10px;
      border-radius: 5px;
    }

    .notification.green {
      background-color: #d4edda;
      color: #155724;
    }

    .notification.red {
      background-color: #f8d7da;
      color: #721c24;
    }

    .notification.yellow {
      background-color: #fff3cd;
      color: #856404;
    }

    #slot-machine {
      display: flex;
      gap: 5px;
      align-items: center;
      position: relative;
    }

    .slot-column {
      width: 50px;
      height: 50px;
      border: 2px solid #000;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
    }

    #lever-handle {
      width: 20px;
      height: 100px;
      background-color: #555;
      position: absolute;
      top: 0;
      left: -80px;
      transform-origin: top center;
      transition: transform 0.3s ease-in-out;
    }

    .grey-connector {
      width: 10px;
      background-color: grey;
      position: absolute;
      left: 0;
      right: 0;
      height: 10px;
      top: 50%;
      transform: translateY(-50%);
    }
  </style>
</head>
<body>

  <h1>Welcome to the Tipping Site</h1>
  <p>Current Balance: <span id="balance">0</span> coins</p>

  <button id="show-crypto-btn" class="button">Show Crypto Addresses</button>
  <button id="show-redeem-btn" class="button">Redeem Coins</button>
  <button id="show-feedback-btn" class="button">Give Feedback</button>
  <button id="show-admin-btn" class="button">Verify Admin</button>

  <!-- Crypto Box -->
  <div id="crypto-box" style="display:none;">
    <h2>Crypto Addresses</h2>
    <div>
      <p>Bitcoin (BTC): bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48</p>
      <button class="button" onclick="copyToClipboard('bc1qx2rd440mz3dpc0mk4e3v766gt70glh32mfdq48')">Copy</button>
    </div>
    <div>
      <p>Ethereum (ETH): 0x65793418b7a6b0Dced78d59AbD44041b1567BE63</p>
      <button class="button" onclick="copyToClipboard('0x65793418b7a6b0Dced78d59AbD44041b1567BE63')">Copy</button>
    </div>
    <!-- Add other crypto addresses here -->
  </div>

  <!-- Redeem Coins Box -->
  <div id="redeem-box" style="display:none;">
    <h2>Redeem Coins</h2>
    <input type="text" id="redeem-code" placeholder="Enter redeem code">
    <button id="redeem-confirm-btn" class="button green">Redeem</button>
  </div>

  <!-- Feedback Box -->
  <div id="feedback-box" style="display:none;">
    <h2>Give Feedback</h2>
    <textarea id="feedback-input" placeholder="Your feedback here..."></textarea>
    <button id="feedback-submit-btn" class="button green">Submit</button>
    <button id="feedback-cancel-btn" class="button red">Cancel</button>
  </div>

  <!-- Admin Verification Box -->
  <div id="admin-box" style="display:none;">
    <h2>Verify Admin</h2>
    <input type="text" id="admin-code" placeholder="Enter admin code">
    <button id="admin-confirm-btn" class="button green">Confirm</button>
  </div>

  <!-- Slot Game -->
  <h2>Slot Machine</h2>
  <div id="slot-machine">
    <div id="lever-handle"></div>
    <div class="slot-column">🍎</div>
    <div class="slot-column">🍎</div>
    <div class="slot-column">🍎</div>
    <div class="grey-connector"></div>
  </div>
  <button id="spin-btn" class="button green">Spin</button>

  <div id="message" class="notification"></div>

  <script>
    // Copy crypto address to clipboard
    function copyToClipboard(text) {
      navigator.clipboard.writeText(text).then(() => {
        alert("Copied to clipboard!");
      });
    }

    // JavaScript functionality (balance system, redeem, etc.)
    let balance = 0;

    function updateBalance(amount) {
      balance += amount;
      document.getElementById("balance").textContent = balance;
    }

    // Add event listeners for buttons, slot game, redeem functionality here...
  </script>

</body>
</html>
<script>
  // Toggle visibility of sections
  const cryptoBox = document.getElementById("crypto-box");
  const redeemBox = document.getElementById("redeem-box");
  const feedbackBox = document.getElementById("feedback-box");
  const adminBox = document.getElementById("admin-box");

  document.getElementById("show-crypto-btn").addEventListener("click", () => toggleVisibility(cryptoBox, "show-crypto-btn"));
  document.getElementById("show-redeem-btn").addEventListener("click", () => toggleVisibility(redeemBox, "show-redeem-btn"));
  document.getElementById("show-feedback-btn").addEventListener("click", () => toggleVisibility(feedbackBox, "show-feedback-btn"));
  document.getElementById("show-admin-btn").addEventListener("click", () => toggleVisibility(adminBox, "show-admin-btn"));

  function toggleVisibility(section, buttonId) {
    const button = document.getElementById(buttonId);
    if (section.style.display === "none") {
      section.style.display = "block";
      button.classList.add("green");
    } else {
      section.style.display = "none";
      button.classList.remove("green");
    }
  }

  // Feedback Box - Cancel and Submit Buttons
  document.getElementById("feedback-cancel-btn").addEventListener("click", () => {
    feedbackBox.style.display = "none";
    displayNotification("Successfully cancelled", "green");
  });

  document.getElementById("feedback-submit-btn").addEventListener("click", () => {
    const feedback = document.getElementById("feedback-input").value.trim();
    if (feedback) {
      displayNotification("Successfully sent to the owner!", "green");
      feedbackBox.style.display = "none";
      document.getElementById("feedback-input").value = "";
    } else {
      displayNotification("Please enter feedback!", "red");
    }
  });

  // Redeem Coins
  const redeemCodes = {
    "a3B9kD7t": 100,
    "r4F8mL2z": 500,
    "z9J3nU1h": 1000,
    "h5Y2vQ4p": 2000,
    "x8W2fL6o": 5000,
    "q7T1wM5v": 10000,
    "e3D7gR4y": 15000,
    "p9Z5iK1b": 20000
  };

  document.getElementById("redeem-confirm-btn").addEventListener("click", () => {
    const code = document.getElementById("redeem-code").value.trim();
    if (redeemCodes[code]) {
      updateBalance(redeemCodes[code]);
      displayNotification(`Redeemed ${redeemCodes[code]} coins!`, "green");
    } else {
      displayNotification("Invalid code. Please try again!", "red");
    }
    document.getElementById("redeem-code").value = "";
  });

  // Admin Verification
  const adminCode = "admin123";

  document.getElementById("admin-confirm-btn").addEventListener("click", () => {
    const code = document.getElementById("admin-code").value.trim();
    if (code === adminCode) {
      displayNotification("Successfully confirmed!", "green");
    } else {
      displayNotification("Invalid!", "red");
    }
    document.getElementById("admin-code").value = "";
  });

  // Slot Machine Game
  const slotColumns = document.querySelectorAll(".slot-column");
  const leverHandle = document.getElementById("lever-handle");
  const spinButton = document.getElementById("spin-btn");

  spinButton.addEventListener("click", () => {
    if (balance >= 1000) {
      updateBalance(-1000);
      spinSlotMachine();
    } else {
      displayNotification("Not enough coins to play!", "red");
    }
  });

  function spinSlotMachine() {
    leverHandle.style.transform = "rotate(30deg)"; // Lever animation
    setTimeout(() => leverHandle.style.transform = "rotate(0deg)", 300); // Reset lever

    const fruits = ["🍎", "🍌", "🍒", "🍇", "🍉", "🍍"];
    const results = [];

    slotColumns.forEach((column, index) => {
      const randomFruit = fruits[Math.floor(Math.random() * fruits.length)];
      results.push(randomFruit);
      setTimeout(() => column.textContent = randomFruit, index * 300); // Simulates spinning delay
    });

    setTimeout(() => {
      if (results.every((fruit, _, array) => fruit === array[0])) {
        updateBalance(10000);
        displayNotification("Jackpot! You won 10,000 coins!", "yellow");
      } else {
        displayNotification("Sorry, no match.", "red");
      }
    }, 1000);
  }

  // Display Notifications
  function displayNotification(message, color) {
    const messageBox = document.getElementById("message");
    messageBox.textContent = message;
    messageBox.className = `notification ${color}`;
    setTimeout(() => messageBox.textContent = "", 3000);
  }
</script>
