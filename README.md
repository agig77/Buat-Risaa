# Buat-Risaa


```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maukah Kamu Jadi Pasangan Agig? 🥺❤️</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Nunito:wght@400;600;800&display=swap" rel="stylesheet">
    
    <style>
        * {
            box-sizing: border-box;
            touch-action: manipulation;
        }

        body {
            font-family: 'Nunito', sans-serif;
            background: linear-gradient(135deg, #ffdde1 0%, #ee9ca7 50%, #ffdde1 100%);
            min-height: 100vh;
            overflow-x: hidden;
            user-select: none;
        }

        .title-font {
            font-family: 'Fredoka', cursive;
        }

        /* Floating background elements */
        .bg-heart {
            position: fixed;
            color: rgba(255, 255, 255, 0.45);
            animation: floatUp linear infinite;
            z-index: 0;
            pointer-events: none;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(105vh) rotate(0deg) scale(0.8);
                opacity: 0;
            }
            15% {
                opacity: 0.9;
            }
            100% {
                transform: translateY(-15vh) rotate(360deg) scale(1.3);
                opacity: 0;
            }
        }

        /* Card container animation */
        .card-pulse {
            animation: gentleFloat 4s ease-in-out infinite;
        }

        @keyframes gentleFloat {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        /* Dodge button smooth motion */
        #btnNo {
            transition: transform 0.15s ease-out, top 0.2s ease, left 0.2s ease;
        }

        /* Pulse glow effect for YES button */
        .yes-glow {
            animation: glowEffect 1.5s infinite;
        }

        @keyframes glowEffect {
            0% { box-shadow: 0 0 0 0 rgba(244, 63, 94, 0.6); }
            70% { box-shadow: 0 0 0 16px rgba(244, 63, 94, 0); }
            100% { box-shadow: 0 0 0 0 rgba(244, 63, 94, 0); }
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4 relative">

    <!-- Floating Background Hearts -->
    <div id="heartsContainer" class="fixed inset-0 pointer-events-none z-0"></div>

    <main id="mainCard" class="relative z-10 w-full max-w-md bg-white/85 backdrop-blur-md rounded-3xl p-6 md:p-8 shadow-2xl border-4 border-white/70 text-center card-pulse transition-all duration-300">
        
        <!-- Animated Cute Gif Header -->
        <div class="relative mb-5 flex justify-center">
            <div id="imageWrapper" class="w-40 h-40 md:w-48 md:h-48 rounded-full bg-pink-100 flex items-center justify-center p-2 shadow-inner border-4 border-pink-300 overflow-hidden">
                <img id="cuteGif" src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHIzOHhhZDVudnF4NjhvaXdyYmRwcmF0ZmptMnRnbXZ0eWVnNXBhYSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/cLS1dkpS5nZHsqfoBX/giphy.gif" 
                     alt="Cute Cat GIF" 
                     class="w-full h-full object-cover rounded-full"
                     onerror="this.onerror=null; this.src='https://placehold.co/200x200/ffb6c1/ffffff?text=🐱+Love+Cat'">
            </div>
        </div>

        <!-- Main Question -->
        <h1 class="title-font text-2xl md:text-3xl font-extrabold text-rose-600 mb-3 leading-snug">
            Maukah kamu jadi pasangan Agig? 🥺❤️
        </h1>

        <!-- Reaction Subtitle Text -->
        <p id="subText" class="text-rose-500 font-semibold text-sm md:text-base mb-6 min-h-[48px] flex items-center justify-center transition-all duration-300">
            Pikirin baik-baik yaa... Tapi tombol enggaknya rada bermasalah deh! 😜
        </p>

        <!-- Buttons Interactive Container -->
        <div id="buttonArea" class="flex flex-col sm:flex-row items-center justify-center gap-4 relative min-h-[140px] w-full">
            
            <!-- YES BUTTON -->
            <button id="btnYes" onclick="acceptProposal()" class="yes-glow bg-gradient-to-r from-rose-500 to-pink-500 hover:from-rose-600 hover:to-pink-600 text-white font-extrabold py-3.5 px-8 rounded-full shadow-lg transform active:scale-95 transition-all duration-200 text-lg flex items-center justify-center gap-2 z-20 cursor-pointer">
                <i class="fa-solid fa-heart text-xl"></i>
                <span id="yesBtnText">Iya Bangeet!</span>
            </button>

            <!-- NO BUTTON (DODGE BUTTON) -->
            <button id="btnNo" class="bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-3.5 px-8 rounded-full shadow transition-all duration-200 text-base z-10 cursor-pointer whitespace-nowrap">
                Tidak
            </button>
        </div>

        <!-- Dodge Counter Hint -->
        <p id="dodgeCountText" class="text-xs text-rose-400 mt-4 italic opacity-0 transition-opacity duration-300">
            Ditolak Agig <span id="dodgeCount" class="font-bold">0</span> kali! Coba terus kalo bisa Wkwk! 🤪
        </p>
    </main>

    <!-- Celebration Modal Card -->
    <div id="successCard" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-rose-950/50 backdrop-blur-md">
        <div id="innerSuccess" class="bg-white rounded-3xl p-6 md:p-8 max-w-md w-full text-center shadow-2xl border-4 border-pink-300 transform scale-90 opacity-0 transition-all duration-500">
            <div class="w-40 h-40 md:w-48 md:h-48 mx-auto mb-4 rounded-full overflow-hidden border-4 border-rose-400 shadow-md bg-pink-50">
                <img id="happyGif" src="https://media.giphy.com/media/26hpW3bE839CwoQpG/giphy.gif" 
                     alt="Happy Cat GIF" 
                     class="w-full h-full object-cover"
                     onerror="this.onerror=null; this.src='https://placehold.co/200x200/ff69b4/ffffff?text=🥳+YAY!'">
            </div>

            <h2 class="title-font text-2xl md:text-3xl font-extrabold text-rose-600 mb-3">
                YAY! RESMI JADI PASANGAN AGIG! 🥰❤️
            </h2>

            <p class="text-gray-700 text-sm md:text-base mb-6 leading-relaxed">
                Makasih yaaa udah mau jadi pasangan Agig! ✨<br>
                Pokoknya udah diklik IYA, ga boleh ditukar atau dikembalikan lagi ya Wkwkwk! 💑💖
            </p>

            <button onclick="sendToWhatsApp()" class="w-full bg-emerald-500 hover:bg-emerald-600 text-white font-extrabold py-3.5 px-6 rounded-full shadow-lg transition-transform hover:scale-105 active:scale-95 flex items-center justify-center gap-3 text-base">
                <i class="fa-brands fa-whatsapp text-2xl"></i>
                Kirim kabar ke WhatsApp Agig
            </button>
        </div>
    </div>

    <script>
        // State management
        let dodgeCount = 0;
        let yesScale = 1;

        // Reaction messages when dodging
        const reactions = [
            "Eits gak bisa! 😜",
            "Yakin mau nolak Agig? 🥺",
            "Coba lagi kalo bisa Wkwk! 🤪",
            "Duh makin susah kan ngejar tombolnya! 🤣",
            "Tombol IYA nya makin gede tuh, buruan klik! 🥰",
            "Masih berusaha nolak? Tidak akan bisa! 💖",
            "Udah iya aja napa sih 😆❤️"
        ];

        // Animated GIF list to change dynamically as dodge count increases
        const gifs = [
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHIzOHhhZDVudnF4NjhvaXdyYmRwcmF0ZmptMnRnbXZ0eWVnNXBhYSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/cLS1dkpS5nZHsqfoBX/giphy.gif",
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM3ZhcHVwb2x0bWVtbWFkYmhpeDRyZXZoOXB2cWZreGg0MXpxNnl4dyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/3o7TKoWXm3okO1mgHC/giphy.gif",
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExaG9jdzJvaG11bzhpNzBzc2Zpd3J5ODZpOWtyczN6ZW11NmsxcmhpYiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/MDJ9IbxxvDUQM/giphy.gif"
        ];

        // Create background floating hearts
        function createBackgroundHearts() {
            const container = document.getElementById('heartsContainer');
            const heartIcons = ['💖', '💗', '💕', '🌸', '✨', '❤️'];
            
            for (let i = 0; i < 18; i++) {
                const heart = document.createElement('div');
                heart.className = 'bg-heart';
                heart.innerText = heartIcons[Math.floor(Math.random() * heartIcons.length)];
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.fontSize = (Math.random() * 18 + 14) + 'px';
                heart.style.animationDuration = (Math.random() * 4 + 6) + 's';
                heart.style.animationDelay = (Math.random() * 5) + 's';
                container.appendChild(heart);
            }
        }

        const btnNo = document.getElementById('btnNo');
        const btnYes = document.getElementById('btnYes');
        const subText = document.getElementById('subText');
        const countDisplay = document.getElementById('dodgeCount');
        const countTextContainer = document.getElementById('dodgeCountText');
        const cuteGif = document.getElementById('cuteGif');

        // Function to move "No" button dynamically
        function handleDodge(event) {
            if (event) event.preventDefault();

            dodgeCount++;
            countDisplay.innerText = dodgeCount;
            countTextContainer.classList.remove('opacity-0');

            // Update subtext reaction
            const reactionIdx = Math.min(dodgeCount - 1, reactions.length - 1);
            subText.innerText = reactions[reactionIdx];
            subText.classList.add('text-rose-600', 'scale-105');
            setTimeout(() => subText.classList.remove('scale-105'), 200);

            // Expand YES button
            yesScale += 0.14;
            btnYes.style.transform = `scale(${yesScale})`;

            // Change cat GIF if dodge count reaches specific thresholds
            if (dodgeCount === 3) cuteGif.src = gifs[1];
            if (dodgeCount === 6) cuteGif.src = gifs[2];

            // If dodge count >= 7, convert the NO button to "Iya Deh!"
            if (dodgeCount >= 7) {
                btnNo.innerText = "Iya Deh! ❤️";
                btnNo.className = "bg-rose-500 hover:bg-rose-600 text-white font-extrabold py-3.5 px-8 rounded-full shadow-lg text-base z-20 cursor-pointer animate-bounce";
                btnNo.style.position = 'static';
                btnNo.style.transform = 'none';
                btnNo.onclick = acceptProposal;
                
                // Unbind move events
                btnNo.removeEventListener('mouseover', handleDodge);
                btnNo.removeEventListener('touchstart', handleDodge);
                return;
            }

            // Move NO button to random coordinates within screen
            const padding = 30;
            const btnWidth = btnNo.offsetWidth || 100;
            const btnHeight = btnNo.offsetHeight || 45;

            const maxX = window.innerWidth - btnWidth - padding;
            const maxY = window.innerHeight - btnHeight - padding;

            const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
            const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

            btnNo.style.position = 'fixed';
            btnNo.style.left = `${randomX}px`;
            btnNo.style.top = `${randomY}px`;
        }

        // Event listeners for dodge mechanism (PC mouse hover & Mobile touch)
        btnNo.addEventListener('mouseover', handleDodge);
        btnNo.addEventListener('touchstart', handleDodge, { passive: false });

        // Function triggered on accepting
        function acceptProposal() {
            // Trigger Confetti Explosion
            launchConfetti();

            // Display success modal
            const successCard = document.getElementById('successCard');
            const innerSuccess = document.getElementById('innerSuccess');

            successCard.classList.remove('hidden');
            setTimeout(() => {
                innerSuccess.classList.remove('scale-90', 'opacity-0');
                innerSuccess.classList.add('scale-100', 'opacity-100');
            }, 50);
        }

        // Confetti celebration launch
        function launchConfetti() {
            const duration = 3 * 1000;
            const animationEnd = Date.now() + duration;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 100 };

            function randomInRange(min, max) {
                return Math.random() * (max - min) + min;
            }

            const interval = setInterval(function() {
                const timeLeft = animationEnd - Date.now();

                if (timeLeft <= 0) {
                    return clearInterval(interval);
                }

                const particleCount = 50 * (timeLeft / duration);
                
                confetti(Object.assign({}, defaults, { 
                    particleCount, 
                    origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 },
                    colors: ['#ff4d6d', '#ff758f', '#ffb3c1', '#ffffff']
                }));
                confetti(Object.assign({}, defaults, { 
                    particleCount, 
                    origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 },
                    colors: ['#ff4d6d', '#ff758f', '#ffb3c1', '#ffffff']
                }));
            }, 250);
        }

        // Redirect to WhatsApp with pre-filled message
        function sendToWhatsApp() {
            const text = encodeURIComponent("Halo Agig! Aku udah terima tawaran kamu buat jadi pasangan kamu nih! 🥰❤️✨");
            // Directs to WhatsApp link
            window.open(`https://wa.me/?text=${text}`, '_blank');
        }

        // Run initialization after full window load
        window.onload = function() {
            createBackgroundHearts();
        };
    </script>
</body>
</html>
```