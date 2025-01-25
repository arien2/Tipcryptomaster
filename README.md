<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tip CryptoGuy</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #222;
            color: white;
            text-align: center;
        }

        /* Feedback Modal styling */
        #feedback-modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.4);
            padding-top: 100px;
            opacity: 0;
            pointer-events: none;
            transition: opacity 1s ease;
        }

        #feedback-modal.show {
            display: block;
            opacity: 1;
            pointer-events: all;
        }

        #feedback-modal-content {
            background-color: #fff;
            margin: auto;
            padding: 20px;
            border-radius: 10px;
            width: 80%;
            max-width: 400px;
            text-align: center;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.2);
            animation: fadeIn 1s ease;
        }

        /* Notification styles */
        #notification {
            margin-top: 20px;
            padding: 10px;
            font-weight: bold;
            display: none;
        }

        #notification.success {
            background-color: #4CAF50;
            color: white;
        }

        #notification.error {
            background-color: #f44336;
            color: white;
        }

        /* Button styles */
        #feedback-button {
            padding: 10px 20px;
            margin-top: 20px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
        }

        #decline-button, #confirm-button {
            padding: 10px 20px;
            margin-top: 20px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            font-size: 16px;
        }

        #decline-button {
            background-color: #f44336;
            color: white;
        }

        #confirm-button {
            background-color: #28a745;
            color: white;
        }

        /* Animation for modal appearance */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Coin balance section */
        #coin-balance {
            margin-top: 20px;
            font-size: 18px;
        }

        /* Donation Goal progress bar */
        .goal-bar {
            width: 80%;
            margin: 20px auto;
            height: 30px;
            border: 1px solid #fff;
            background-color: #f44336;
            border-radius: 5px;
            position: relative;
        }

        .goal-bar-filled {
            background-color: green;
            height: 100%;
            width: 0;
            border-radius: 5px 0 0 5px;
        }

        /* Coin Game Section */
        #game-section {
            margin-top: 50px;
            padding: 20px;
            background-color: #444;
            border-radius: 10px;
        }

        #spin-button {
            margin-top: 10px;
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }

        #coin-count {
            font-size: 20px;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <!-- Coin balance display -->
    <div id="coin-balance">Coin Balance: 0</div>

    <!-- Donation Goal Section -->
    <div class="goal-bar">
        <div id="goal-bar-filled" class="goal-bar-filled"></div>
    </div>

    <!-- Feedback Button -->
    <button id="feedback-button" onclick="openFeedbackModal()">Give Feedback</button>

    <!-- Feedback Modal -->
    <div id="feedback-modal">
        <div id="feedback-modal-content">
            <h2>Enter your feedback below:</h2>
            <textarea id="feedback" placeholder="Enter your feedback here..."></textarea><br>
            <button id="confirm-button" onclick="submitFeedback()">Confirm</button>
            <button id="decline-button" onclick="closeFeedbackModal()">Decline</button>
            <div id="notification"></div>
        </div>
    </div>

    <!-- Admin Verification Modal -->
    <div id="admin-modal">
        <div id="admin-modal-content">
            <h2>This verification is only to detect if you are admin or not.</h2>
            <input type="text" id="admin-code" placeholder="Enter secret code" />
            <button id="confirm-admin-button" onclick="verifyAdmin()">Confirm</button>
            <button id="decline-admin-button" onclick="closeAdminModal()">Decline</button>
        </div>
    </div>

    <!-- Coin Game Section -->
    <div id="game-section">
        <h3>Spin the Slot Machine (Cost: 1000 coins)</h3>
        <button id="spin-button" onclick="spinSlot()">Spin</button>
        <div id="coin-count">Coins Available: 0</div>
    </div>

    <script>
        // Admin settings
        let isAdmin = false;
        let coinBalance = 0;
        const secretCode = "Letsgogamblingwhilebeingabillionaire";

        // Open feedback modal
        function openFeedbackModal() {
            document.getElementById("feedback-modal").classList.add("show");
        }

        // Close feedback modal
        function closeFeedbackModal() {
            document.getElementById("feedback-modal").classList.remove("show");
        }

        // Submit feedback
        function submitFeedback() {
            const feedbackText = document.getElementById("feedback").value;
            const notification = document.getElementById("notification");

            if (feedbackText.trim() !== "") {
                console.log("Feedback received: " + feedbackText);
                notification.innerText = "Successfully sent to the owner!";
                notification.classList.add("success");
                notification.classList.remove("error");
                notification.style.display = "block";

                setTimeout(() => {
                    document.getElementById("feedback").value = "";
                    closeFeedbackModal();
                    notification.style.display = "none";
                }, 2000);
            } else {
                notification.innerText = "Please enter feedback before submitting!";
                notification.classList.add("error");
                notification.classList.remove("success");
                notification.style.display = "block";
            }
        }

        // Open admin verification modal
        function openAdminModal() {
            document.getElementById("admin-modal").style.display = "block";
        }

        // Close admin verification modal
        function closeAdminModal() {
            document.getElementById("admin-modal").style.display = "none";
        }

        // Verify admin
        function verifyAdmin() {
            const inputCode = document.getElementById("admin-code").value;

            if (inputCode === secretCode) {
                isAdmin = true;
                coinBalance = Infinity;  // Admin gets infinite coins
                document.getElementById("notification").innerText = "Successfully verified as admin!";
                document.getElementById("notification").classList.add("success");
                document.getElementById("notification").classList.remove("error");
                document.getElementById("notification").style.display = "block";

                setTimeout(() => {
                    document.getElementById("notification").style.display = "none";
                }, 2000);
                closeAdminModal();
            } else {
                document.getElementById("notification").innerText = "INVALID CODE!";
                document.getElementById("notification").classList.add("error");
                document.getElementById("notification").classList.remove("success");
                document.getElementById("notification").style.display = "block";

                setTimeout(() => {
                    document.getElementById("notification").style.display = "none";
                }, 2000);
            }
        }

        // Spin the slot machine (game)
        function spinSlot() {
            if (coinBalance >= 1000) {
                coinBalance -= 1000;  // Cost of spinning
                updateCoinBalance();
                alert("You spun the slot! (This is just a placeholder for actual slot machine functionality)");
            } else {
                alert("You don't have enough coins to play!");
            }
        }

        // Update coin balance display
        function updateCoinBalance() {
            document.getElementById("coin-balance").innerText = `Coin Balance: ${coinBalance}`;
            document.getElementById("coin-count").innerText = `Coins Available: ${coinBalance}`;
        }

        // Simulate donation goal progress (for demo purposes)
        function updateDonationGoal() {
            let donationGoal = 10000;  // Example goal
            let currentDonation = 5000;  // Example donation

            let progress = (currentDonation / donationGoal) * 100;
            document.getElementById("goal-bar-filled").style.width = `${progress}%`;
        }

        // Initialize donation goal progress
        updateDonationGoal();

    </script>
</body>
</html>
