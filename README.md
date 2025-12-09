# MoglieWebsite

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Special Day for a Special Person</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');

        /* Custom Colors for the 2025 Aesthetic */
        :root {
            --color-dark-bg: #0A0A1A;
            --color-accent: #facc15; /* Tailwind yellow-400 */
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--color-dark-bg);
            color: #E5E7EB; /* Light gray text */
            overflow: hidden; /* Prevent scrollbars due to particle effect */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        /* --- Custom Animations and Effects --- */

        /* Pulsing Button Glow */
        .btn-pulse {
            box-shadow: 0 0 10px var(--color-accent), 0 0 40px var(--color-accent) inset;
            transition: all 0.3s ease-in-out;
        }
        .btn-pulse:hover {
            box-shadow: 0 0 20px var(--color-accent), 0 0 60px var(--color-accent) inset;
            transform: scale(1.05);
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.05); opacity: 0.8; }
        }
        .animate-pulse-slow {
            animation: pulse 4s infinite ease-in-out;
        }

       /* Card Hover Effect */
        .memory-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .memory-card:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: 0 20px 40px rgba(250, 202, 21, 0.2);
            z-index: 10;
        }

        /* Background Particle System (CSS only) */
        .particle {
            position: absolute;
            width: 3px;
            height: 3px;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            pointer-events: none;
            opacity: 0;
            animation: move-particles linear infinite;
        }

        @keyframes move-particles {
            0% { transform: translate(0, 0); opacity: 0.1; }
            50% { opacity: 0.5; }
            100% { transform: translate(var(--x), var(--y)); opacity: 0; }
        }

        /* Confetti Effect Container */
        #confetti-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 50;
            opacity: 0;
            transition: opacity 1s ease;
        }
        .confetti {
            position: absolute;
            width: 8px;
            height: 8px;
            opacity: 0;
            animation: confetti-fall 3s linear forwards;
        }
        @keyframes confetti-fall {
            0% { transform: translateY(-10vh) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
        }

    </style>
</head>
<body>

    <div class="relative w-full h-full flex justify-center items-center p-4">

        <!-- Background Particle Layer -->
        <div id="particle-layer" class="absolute inset-0 z-0"></div>

        <!-- Confetti Layer -->
        <div id="confetti-container" class="z-50"></div>

        <!-- Main Content Container -->
        <div id="greeting-app" class="w-full max-w-4xl p-8 md:p-12 lg:p-16 bg-[#121223] border border-gray-800 rounded-3xl shadow-2xl relative z-10 min-h-[500px] flex flex-col justify-center transition-all duration-1000">

            <!-- STAGE 1: INTRO SCREEN -->
            <div id="stage-intro" class="text-center transition-opacity duration-500">
                <h1 class="text-3xl md:text-5xl font-extrabold mb-6 text-gray-200 tracking-tight">
                    Welcome to Your Special Day!
                </h1>
                <p class="text-xl text-gray-400 mb-10">
                    A small collection of wishes, just for you.
                </p>
                <button id="start-button" class="btn-pulse bg-yellow-600 text-gray-900 font-bold py-3 px-8 rounded-full text-lg shadow-lg hover:bg-yellow-500 transition-colors duration-300 animate-pulse-slow">
                    Click to Begin
                </button>
            </div>

            <!-- STAGE 2: MAIN GREETING -->
            <div id="stage-main" class="text-center transition-opacity duration-1000 hidden opacity-0">
                <p class="text-lg text-yellow-400 font-semibold mb-4">
                    — From the bottom of my heart —
                </p>
                <h2 class="text-5xl md:text-7xl font-black text-white leading-tight mb-8">
                    Happy Birthday, My Dearest Moglie!
                </h2>
                <p class="text-xl md:text-2xl text-gray-300 max-w-3xl mx-auto mb-12">
                    Today is a celebration of the wonderful person you are. May this special day bring you sweet memories and a year filled with happiness and joy. Wish you happy happy birthday!
                </p>
                <button id="next-button" class="bg-gray-700 text-white font-medium py-2 px-6 rounded-full hover:bg-gray-600 transition-colors duration-300">
                    Reveal Your Gifts
                </button>
            </div>

            <!-- STAGE 3: INTERACTIVE GIFTS/MEMORIES -->
            <div id="stage-gifts" class="transition-opacity duration-1000 hidden opacity-0">
                <h3 class="text-3xl font-bold text-center text-yellow-400 mb-8">
                    Three Special Moments
                </h3>
                <div class="grid md:grid-cols-3 gap-6">
                    <!-- Gift Card 1 -->
                    <div id="card-1" class="memory-card bg-gray-800 p-6 rounded-xl cursor-pointer text-center border-2 border-gray-700 hover:border-yellow-400/50">
                        <div class="text-4xl mb-4" id="icon-1">🌟</div>
                        <h4 class="text-xl font-semibold mb-2">Memory 1</h4>
                        <p class="text-gray-400 transition-all duration-300" id="text-1">Click to reveal a beautiful memory we shared.</p>
                    </div>

                    <!-- Gift Card 2 -->
                    <div id="card-2" class="memory-card bg-gray-800 p-6 rounded-xl cursor-pointer text-center border-2 border-gray-700 hover:border-yellow-400/50">
                        <div class="text-4xl mb-4" id="icon-2">💫</div>
                        <h4 class="text-xl font-semibold mb-2">Future Wish</h4>
                        <p class="text-gray-400 transition-all duration-300" id="text-2">Click to reveal a wish for our next year together.</p>
                    </div>

                    <!-- Gift Card 3 -->
                    <div id="card-3" class="memory-card bg-gray-800 p-6 rounded-xl cursor-pointer text-center border-2 border-gray-700 hover:border-yellow-400/50">
                        <div class="text-4xl mb-4" id="icon-3">💖</div>
                        <h4 class="text-xl font-semibold mb-2">My Favorite Thing</h4>
                        <p class="text-gray-400 transition-all duration-300" id="text-3">Click to see what I appreciate most about you.</p>
                    </div>
                </div>

                <div id="final-message" class="mt-12 text-center hidden opacity-0 transition-opacity duration-1000">
                    <p class="text-2xl font-light italic text-gray-300">
                        "Every moment spent with you is a gift itself. Thank you for being you."
                    </p>
                    <p class="mt-4 text-yellow-400 font-bold text-lg">- [Your Name/Initials]</p>
                </div>
            </div>

        </div>
    </div>

    <script>
        const app = document.getElementById('greeting-app');
        const intro = document.getElementById('stage-intro');
        const main = document.getElementById('stage-main');
        const gifts = document.getElementById('stage-gifts');
        const startButton = document.getElementById('start-button');
        const nextButton = document.getElementById('next-button');
        const finalMessage = document.getElementById('final-message');
        const particleLayer = document.getElementById('particle-layer');
        const confettiContainer = document.getElementById('confetti-container');

        const CARD_DATA = [
            { id: 'card-1', iconId: 'icon-1', textId: 'text-1', defaultText: 'Click to reveal a beautiful memory we shared.', revealedText: 'Remember that night under the stars? That\'s when I truly realized how amazing you are. A core memory forever. 2022 December month 14, i remember your face when cutting a cake and you surprised' },
            { id: 'card-2', iconId: 'icon-2', textId: 'text-2', defaultText: 'Click to reveal a wish for our next year together.', revealedText: 'My wish is simple: more laughter, more adventures, and watching all your big dreams come true.i marry you. I\'ll be cheering you on!' },
            { id: 'card-3', iconId: 'icon-3', icon: '❤️', textId: 'text-3', defaultText: 'Click to see what I appreciate most about you.', revealedText: 'The thing I love most is your kindness. It\'s a superpower. You make everyone around you feel seen and valued. i promised every year, every month, every week, every every hours, and every second living togather. i love you moglie,' }
        ];

        // --- State Management ---
        let currentStage = 1;
        let cardsRevealed = 0;
        const totalCards = CARD_DATA.length;

        // --- Utility Functions ---

        /**
         * Smoothly transitions between stages.
         * @param {HTMLElement} hideElement - The element to hide.
         * @param {HTMLElement} showElement - The element to show.
         */
        const transitionStage = (hideElement, showElement) => {
            hideElement.classList.add('opacity-0');
            hideElement.ontransitionend = () => {
                hideElement.classList.add('hidden');
                hideElement.classList.remove('opacity-0');

                showElement.classList.remove('hidden');
                // Force repaint to ensure transition runs
                void showElement.offsetWidth;
                setTimeout(() => {
                    showElement.classList.add('opacity-100');
                }, 10); // Small delay for smoother start
            };
        };

        // --- Particle & Confetti Logic ---

        const createParticles = () => {
            const count = 50;
            for (let i = 0; i < count; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                const x = Math.random() * window.innerWidth;
                const y = Math.random() * window.innerHeight;
                const delay = Math.random() * 5;
                const duration = 10 + Math.random() * 10;

                // Random movement vectors
                const dx = (Math.random() - 0.5) * 500;
                const dy = (Math.random() - 0.5) * 500;

                particle.style.left = `${x}px`;
                particle.style.top = `${y}px`;
                particle.style.animationDelay = `-${delay}s`;
                particle.style.animationDuration = `${duration}s`;
                particle.style.setProperty('--x', `${dx}px`);
                particle.style.setProperty('--y', `${dy}px`);
                particleLayer.appendChild(particle);
            }
        };

        const generateConfetti = () => {
            confettiContainer.style.opacity = '1';
            const colors = ['#facc15', '#f87171', '#a78bfa', '#34d399', '#ffffff'];
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement('div');
                confetti.classList.add('confetti');

                // Set random color
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];

                // Set random position
                const startX = Math.random() * window.innerWidth;
                confetti.style.left = `${startX}px`;

                // Set random size and shape (square/circle)
                const size = 5 + Math.random() * 5;
                confetti.style.width = `${size}px`;
                confetti.style.height = `${size}px`;
                if (Math.random() > 0.5) {
                    confetti.style.borderRadius = '50%';
                }

                // Randomize animation properties
                confetti.style.animationDelay = `${Math.random() * 0.5}s`;
                confetti.style.animationDuration = `${2 + Math.random() * 2}s`;
                confettiContainer.appendChild(confetti);
            }

            // Remove confetti after it falls
            setTimeout(() => {
                confettiContainer.innerHTML = '';
                confettiContainer.style.opacity = '0';
            }, 3500);
        };

        // --- Event Handlers ---

        const handleStart = () => {
            if (currentStage === 1) {
                currentStage = 2;
                transitionStage(intro, main);
                // Trigger confetti immediately after main screen loads
                setTimeout(generateConfetti, 500);
            }
        };

        const handleNext = () => {
            if (currentStage === 2) {
                currentStage = 3;
                main.classList.remove('opacity-100');
                transitionStage(main, gifts);
            }
        };

        const handleCardClick = (event) => {
            const cardElement = event.currentTarget;
            const data = CARD_DATA.find(d => d.id === cardElement.id);

            if (cardElement.dataset.revealed !== 'true') {
                const textElement = document.getElementById(data.textId);
                const iconElement = document.getElementById(data.iconId);

                // Update content
                textElement.textContent = data.revealedText;
                iconElement.textContent = '✅';
                textElement.classList.add('text-yellow-400');

                // Mark as revealed and increment counter
                cardElement.dataset.revealed = 'true';
                cardsRevealed++;

                // Final reveal logic
                if (cardsRevealed === totalCards) {
                    setTimeout(() => {
                        finalMessage.classList.remove('hidden');
                        void finalMessage.offsetWidth; // Trigger repaint
                        finalMessage.classList.add('opacity-100');
                        generateConfetti(); // Final burst!
                    }, 500);
                }
            }
        };

        // --- Initialization ---
        const init = () => {
            createParticles();
            startButton.addEventListener('click', handleStart);
            nextButton.addEventListener('click', handleNext);

            // Add click listeners to all memory cards
            CARD_DATA.forEach(data => {
                const card = document.getElementById(data.id);
                if (card) {
                    card.addEventListener('click', handleCardClick);
                }
            });

            // Initial visual state setup
            intro.classList.add('opacity-100');
            main.classList.remove('opacity-100');
            gifts.classList.remove('opacity-100');
        };

        window.onload = init;
    </script>
</body>
</html>
