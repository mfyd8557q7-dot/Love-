<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Surprise for Riddhima</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Quicksand:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            font-family: 'Quicksand', sans-serif;
            overflow: hidden;
            background: #ffd1dc; /* Solid pastel pink */
        }

        /* Floating Hearts Decoration */
        .decor {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .card {
            background: rgba(255, 255, 255, 0.92);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.12);
            text-align: center;
            z-index: 10;
            max-width: 420px;
            width: 90%;
        }

        h2 { 
            color: #d63384; 
            line-height: 1.4; 
        }
        
        .final-question {
            font-family: 'Dancing Script', cursive;
            color: #ff0000;
            font-size: 2.8rem;
            margin: 25px 0;
        }

        .btn-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 25px;
        }

        button {
            padding: 14px 30px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 1.1rem;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .btn-yes { 
            background-color: #ff4d6d; 
            color: white; 
        }
        .btn-no { 
            background-color: #e9ecef; 
            color: #495057; 
        }

        button:hover { 
            transform: scale(1.08); 
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
        }

        .hidden { display: none; }
        
        .floating-item {
            position: absolute;
            animation: float 7s infinite ease-in-out;
            font-weight: bold;
            pointer-events: none;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-35px) rotate(10deg); }
        }
    </style>
</head>
<body>

<div class="decor" id="decorations"></div>

<div class="card">
    <div id="content">
        <h2 id="text-display">You know how much I love you, so here is a little surprise for you...</h2>
        <div class="btn-container">
            <button class="btn-yes" onclick="nextQuestion()">Next ❤️</button>
        </div>
    </div>
</div>

<script>
    let currentStep = 0;
    const questions = [
        "Are you ready for a few questions, Riddhima?",
        "Do you think we make the best team ever?",
        "Will you promise to always share your snacks with me?",
        "Do you know you're the prettiest girl in the world?",
        "Are you ready for the most important question?"
    ];

    const backupLines = [
        "Wait, really? Think again! 🥺",
        "Aisa karke mera dil mat todo... please? 💔",
        "You're breaking my heart! Try that 'Yes' button.",
        "I'll ask again... you know you want to say yes!",
        "Don't be mean! Click Yes! ❤️"
    ];

    function nextQuestion() {
        const content = document.getElementById('content');

        if (currentStep < questions.length) {
            content.innerHTML = `
                <h2>${questions[currentStep]}</h2>
                <div class="btn-container">
                    <button class="btn-yes" onclick="nextQuestion()">Yes!</button>
                    <button class="btn-no" onclick="wrongAnswer()">No</button>
                </div>
            `;
            currentStep++;
        } else {
            showFinalQuestion();
        }
    }

    function wrongAnswer() {
        const display = document.querySelector('#content h2');
        const randomLine = backupLines[Math.floor(Math.random() * backupLines.length)];
        display.innerText = randomLine;
    }

    function showFinalQuestion() {
        const content = document.getElementById('content');
        content.innerHTML = `
            <h2 class="final-question">Will You Be My Valentine?</h2>
            <div class="btn-container">
                <button class="btn-yes" onclick="celebrate()">Yes!</button>
                <button class="btn-no" onclick="heartbreak()">No</button>
            </div>
        `;
    }

    function heartbreak() {
        const content = document.getElementById('content');
        content.innerHTML = `
            <h2 style="color: #d63384;">Aisa karke mera dil mat todo...</h2>
            <h2 class="final-question">Will You Be My Valentine?</h2>
            <div class="btn-container">
                <button class="btn-yes" onclick="celebrate()">Yes!</button>
                <button class="btn-no" onclick="celebrate()">Yes (No is disabled now!)</button>
            </div>
        `;
    }

    function celebrate() {
        const content = document.getElementById('content');
        content.innerHTML = `
            <h2 style="font-size: 2.5rem; color: #ff4d6d;">YAY! ❤️</h2>
            <p style="font-size: 1.3rem;">I love you, Riddhima!</p>
        `;
        confetti({
            particleCount: 180,
            spread: 80,
            origin: { y: 0.6 }
        });
    }

    // Generate floating hearts only
    const decor = document.getElementById('decorations');
    const heartTypes = ['❤️', '💗', '🤍', '💕'];
    
    for (let i = 0; i < 24; i++) {
        const span = document.createElement('span');
        const heart = heartTypes[Math.floor(Math.random() * heartTypes.length)];
        span.innerText = heart;
        span.className = 'floating-item';
        span.style.left = Math.random() * 100 + 'vw';
        span.style.top = Math.random() * 100 + 'vh';
        span.style.fontSize = (Math.random() * 24 + 18) + 'px';
        span.style.color = heart === '🤍' ? '#ffffff' : '#ff4d6d';
        span.style.animationDuration = (Math.random() * 4 + 6) + 's';
        span.style.animationDelay = Math.random() * 5 + 's';
        decor.appendChild(span);
    }
</script>
</body>
</html>
