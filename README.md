// Stop the spinning after a brief animation
            setTimeout(() => {
                item.classList.remove('spinning');
            }, 1000);
        });

        // Check if all fruits are the same (win condition)
        if (result[0] === result[1] && result[1] === result[2]) {
            win = true;
            showLuxuryNotification("You win 10,000 coins!");
            // Increase coin balance by 10,000
            updateCoinBalance(10000);
        } else {
            showLuxuryNotification("No win, try again!");
        }
    }

    // Luxury notification display
    function showLuxuryNotification(message) {
        const notification = document.getElementById('message');
        notification.textContent = message;
        notification.classList.add('show');
        setTimeout(() => {
            notification.classList.remove('show');
        }, 3000);
    }

    // Admin code verification logic
    function verifyAdmin() {
        const adminCode = document.getElementById('adminCode').value.trim();
        const validCode = "admin123";  // Set the valid admin code here (you can change it)

        if (adminCode === validCode) {
            showLuxuryNotification("Admin verified!");
            // Code to add admin privileges
        } else {
            showLuxuryNotification("Incorrect Admin Code!");
        }
    }

    // Redeem coins functionality
    const redeemCodes = {
        "redeem100": 100,
        "redeem500": 500,
        "redeem1000": 1000,
        "redeem2000": 2000,
        "redeem5000": 5000,
        "redeem10000": 10000,
        "redeem15000": 15000,
        "redeem20000": 20000
    };

    function redeemCoins() {
        const code = document.getElementById('redeemCode').value.trim().toLowerCase();
        const redeemMessage = document.getElementById('redeemMessage');

        if (redeemCodes[code]) {
            showLuxuryNotification(`Redeemed ${redeemCodes[code]} coins!`);
            updateCoinBalance(redeemCodes[code]);
            redeemMessage.textContent = `Successfully redeemed ${redeemCodes[code]} coins!`;
            redeemMessage.classList.add('correct');
        } else {
            redeemMessage.textContent = "Invalid code!";
            redeemMessage.classList.add('incorrect');
            setTimeout(() => {
                redeemMessage.classList.remove('incorrect');
            }, 3000);
        }
    }

    // Function to update the coin balance
    let coinBalance = 0;
    function updateCoinBalance(amount) {
        coinBalance += amount;
        document.getElementById('coinBalance').textContent = coinBalance;
    }

    // Feedback form functionality
    function showFeedbackForm() {
        const feedbackBox = document.querySelector('.feedback-box');
        feedbackBox.style.display = 'block';
    }

    function cancelFeedbackForm() {
        const feedbackBox = document.querySelector('.feedback-box');
        feedbackBox.style.display = 'none';
    }

    function submitFeedback() {
        const feedback = document.getElementById('feedback').value.trim();
        if (feedback) {
            showLuxuryNotification("Successfully sent to the owner!");
            cancelFeedbackForm();
        } else {
            showLuxuryNotification("Please provide feedback!");
        }
    }

    // Initialize site
    document.addEventListener("DOMContentLoaded", function () {
        displayCryptoAddresses();  // Display all the crypto addresses
    });

</script>

</body>
</html>
