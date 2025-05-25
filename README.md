<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Greeting</title>
    <link rel="shortcut icon" href="logo.jpg" type="image/x-icon">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom font for the entire page */
        body {
            font-family: 'Inter', sans-serif;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            
            background-color: #000000; /* Light blue-gray background */
            color: #005eff; /* Dark text */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 1rem;
        }

        /* Animation for greeting message */
        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: scale(0.8);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .fade-in-scale {
            animation: fadeInScale 0.5s ease-out forwards;
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center min-h-screen bg-bule-100 p-4">
    <div class="bg-white p-8 rounded-xl shadow-2xl w-full max-w-md text-center border border-black-200">
        <h1 class="text-3xl font-extrabold text-blue-700 mb-6"><span style="color: violet;">Personalized</span><br>Greeting</h1>

        <div class="mb-6">
            <label for="userName" class="block text-gray-700 text-lg font-semibold mb-2">Enter Your Name:</label>
            <input
                type="text"
                id="userName"
                placeholder="e.g., SAI"
                class="w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent text-lg"
            >
        </div>

        <button
            id="greetButton"
            class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-full shadow-lg transition duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-75"
        >
           <span style="color: rgb(248, 252, 255);">Greet</span> <span style="color: rgb(215, 215, 215);">ME</span>
        </button>

        <div id="messageDisplay" class="mt-8 p-4 bg-blue-100 text-blue-800 rounded-lg text-xl font-medium hidden">
            </div>

        <div id="errorDisplay" class="mt-4 p-3 bg-red-100 text-red-700 rounded-lg text-base font-medium hidden">
            </div>
    </div>

    <script>
        // Get references to HTML elements
        const userNameInput = document.getElementById('userName');
        const greetButton = document.getElementById('greetButton');
        const messageDisplay = document.getElementById('messageDisplay');
        const errorDisplay = document.getElementById('errorDisplay');

        // Function to display messages (greeting or error)
        function displayMessage(element, message, isError = false) {
            // Hide both message and error displays initially
            messageDisplay.classList.add('hidden');
            errorDisplay.classList.add('hidden');

            // Set the message content
            element.textContent = message;

            // Show the appropriate element
            element.classList.remove('hidden');

            // Add animation class if it's a greeting message
            if (!isError) {
                element.classList.add('fade-in-scale');
            } else {
                element.classList.remove('fade-in-scale'); // Ensure no animation for errors
            }
        }

        // Event listener for the "Greet Me" button
        greetButton.addEventListener('click', () => {
            const userName = userNameInput.value.trim(); // Get input value and remove leading/trailing whitespace

            if (userName === '') {
                // If input is empty, display an error message
                displayMessage(errorDisplay, 'Please enter your name!', true);
                userNameInput.classList.add('border-red-500', 'focus:ring-red-500'); // Highlight input field
                userNameInput.focus(); // Focus back on the input field
            } else {
                // If input is not empty, display a personalized greeting
                userNameInput.classList.remove('border-red-500', 'focus:ring-red-500'); // Remove error highlight
                const greetingMessage = `We are great to have you on board, MR.${userName}! Welcome to our Dynamic web-page.`;
                displayMessage(messageDisplay, greetingMessage);
                userNameInput.value = ''; // Clear the input field after greeting
            }
        });

        // Optional: Clear error message when user starts typing again
        userNameInput.addEventListener('input', () => {
            errorDisplay.classList.add('hidden');
            userNameInput.classList.remove('border-red-500', 'focus:ring-red-500');
        });
    </script>
</body>
</html>
