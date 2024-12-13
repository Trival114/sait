<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Buttons with Modal</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(120deg, #74b9ff, #0984e3);
            font-family: Arial, sans-serif;
        }

        .button {
            background: #ffffff;
            border: none;
            padding: 15px 30px;
            margin: 10px;
            border-radius: 5px;
            font-size: 18px;
            color: #0984e3;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        .button:hover {
            transform: scale(1.1);
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.2);
        }

        .button:active {
            transform: scale(0.9);
        }

        .modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0);
            width: 300px;
            padding: 20px;
            background: white;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            text-align: center;
            z-index: 1000;
            opacity: 0;
            transition: transform 0.3s ease, opacity 0.3s ease;
        }

        .modal.active {
            transform: translate(-50%, -50%) scale(1);
            opacity: 1;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 999;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease;
        }

        .overlay.active {
            opacity: 1;
            visibility: visible;
        }

        .close-button {
            margin-top: 20px;
            padding: 10px 20px;
            background: #0984e3;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.2s ease;
        }

        .close-button:hover {
            background: #74b9ff;
        }
    </style>
</head>
<body>
    <!-- Buttons -->
    <div>
        <button class="button" data-info="Information about Button 1">Button 1</button>
        <button class="button" data-info="Information about Button 2">Button 2</button>
        <button class="button" data-info="Information about Button 3">Button 3</button>
    </div>

    <!-- Modal -->
    <div class="overlay" id="overlay"></div>
    <div class="modal" id="modal">
        <p id="modal-content"></p>
        <button class="close-button" id="close-button">Close</button>
    </div>

    <script>
        // Elements
        const buttons = document.querySelectorAll('.button');
        const modal = document.getElementById('modal');
        const overlay = document.getElementById('overlay');
        const modalContent = document.getElementById('modal-content');
        const closeButton = document.getElementById('close-button');

        // Show modal function
        function showModal(content) {
            modalContent.textContent = content;
            modal.classList.add('active');
            overlay.classList.add('active');
        }

        // Hide modal function
        function hideModal() {
            modal.classList.remove('active');
            overlay.classList.remove('active');
        }

        // Add event listeners to buttons
        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const info = button.getAttribute('data-info');
                showModal(info);
            });
        });

        // Add event listener to close button and overlay
        closeButton.addEventListener('click', hideModal);
        overlay.addEventListener('click', hideModal);
    </script>
</body>
</html>
