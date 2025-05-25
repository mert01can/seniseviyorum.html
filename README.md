<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kırmızı Kalp</title>
    <style>
        html, body {
            height: 100%;
            margin: 0;
            padding: 0;
        }
        body {
            min-height: 100vh;
            height: 100%;
            width: 100vw;
            background: #000;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        #container {
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100vw;
            height: 100vh;
            z-index: 1;
        }
        .heart {
            width: 64px;
            height: 64px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.2s;
        }
        .heart:active {
            transform: scale(1.1);
        }
        .heart svg {
            width: 64px;
            height: 64px;
            display: block;
        }
        #love-message {
            display: none;
            position: fixed;
            z-index: 10;
            top: 0; left: 0; right: 0; bottom: 0;
            width: 100vw;
            height: 100vh;
            background: #c70039;
            color: #fff;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            font-family: 'Arial', sans-serif;
            text-align: center;
        }
        #love-message.active {
            display: flex;
            animation: fadeIn 1s;
        }
        #love-message h1 {
            font-size: 3rem;
            margin-top: 0;
        }
        .hearts {
            position: absolute;
            left: 0; right: 0; bottom: 40px;
            width: 100vw;
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            pointer-events: none;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to   { opacity: 1; }
        }
        @keyframes flyHeart {
            to {
                transform: translateY(-80vh) scale(1.2) rotate(20deg);
                opacity: 0;
            }
        }
        .flying-heart {
            pointer-events: none;
            opacity: 0.85;
            animation-timing-function: cubic-bezier(.36,.07,.19,.97);
        }
    </style>
</head>
<body>
    <div id="container">
        <div id="heart" class="heart">
            <!-- TAM ORTADA KIRMIZI KALP -->
            <svg viewBox="0 0 32 32" fill="#c70039" xmlns="http://www.w3.org/2000/svg">
                <path d="M23.6 4.6c-2.3 0-4.4 1-5.6 2.6C16.8 5.6 14.7 4.6 12.4 4.6c-3.2 0-5.8 2.6-5.8 5.8 0 6.3 10.1 14.1 10.6 14.5.2.2.6.2.8 0 .5-.4 10.6-8.2 10.6-14.5 0-3.2-2.6-5.8-5.8-5.8z"/>
            </svg>
        </div>
    </div>
    <div id="love-message">
        <h1>Seni Seviyorum</h1>
        <div class="hearts"></div>
    </div>
    <script>
        const heart = document.getElementById('heart');
        const loveMessage = document.getElementById('love-message');
        const heartsContainer = document.querySelector('.hearts');
        const container = document.getElementById('container');

        heart.addEventListener('click', () => {
            loveMessage.classList.add('active');
            container.style.display = 'none'; // Kalbi gizle
            createHearts();
        });

        function createHearts() {
            heartsContainer.innerHTML = '';
            for(let i=0; i<30; i++) {
                const div = document.createElement('div');
                div.className = 'flying-heart';
                div.innerHTML = `
                    <svg width="32" height="32" viewBox="0 0 32 32" fill="red" xmlns="http://www.w3.org/2000/svg">
                        <path d="M23.6 4.6c-2.3 0-4.4 1-5.6 2.6C16.8 5.6 14.7 4.6 12.4 4.6c-3.2 0-5.8 2.6-5.8 5.8 0 6.3 10.1 14.1 10.6 14.5.2.2.6.2.8 0 .5-.4 10.6-8.2 10.6-14.5 0-3.2-2.6-5.8-5.8-5.8z"/>
                    </svg>
                `;
                const left = Math.random() * 90 + 5;
                const delay = Math.random() * 1.5;
                const duration = 2.5 + Math.random() * 2;
                div.style.position = 'absolute';
                div.style.left = `${left}%`;
                div.style.bottom = '0px';
                div.style.animation = `flyHeart ${duration}s ${delay}s forwards`;
                heartsContainer.appendChild(div);
            }
        }
    </script>
</body>
</html>
