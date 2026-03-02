 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&display=swap" rel="stylesheet">
    <style>
        body, html { margin: 0; padding: 0; height: 100%; overflow: hidden; background: #1a0a0a; }
        
        /* Realistic background from the video */
        #bg-layer {
            position: fixed; width: 100%; height: 100%;
            background: url('https://images.unsplash.com/photo-1522383225653-ed111181a951?auto=format&fit=crop&w=1920&q=80') no-repeat center center;
            background-size: cover; transition: filter 1.5s ease; z-index: -1;
        }

        /* The Flipping Book */
        .book-wrapper { display: flex; justify-content: center; align-items: center; height: 100vh; perspective: 1500px; }
        .book { width: 300px; height: 400px; position: relative; transform-style: preserve-3d; transition: transform 1.2s cubic-bezier(0.645, 0.045, 0.355, 1); cursor: pointer; }
        .book.open { transform: rotateY(-160deg) translateX(50px); }

        .page { position: absolute; width: 100%; height: 100%; top: 0; left: 0; backface-visibility: hidden; border-radius: 15px; display: flex; flex-direction: column; justify-content: center; align-items: center; box-shadow: 0 20px 40px rgba(0,0,0,0.5); }
        
        .front { background: rgba(255, 183, 197, 0.9); border: 4px solid #fff; z-index: 2; }
        .inside { background: #fff0f5; transform: rotateY(180deg); z-index: 1; padding: 20px; text-align: center; color: #4a0e2e; }

        h1 { font-family: 'Dancing Script', cursive; font-size: 2.2rem; margin: 0; color: #d02090; }
        
        /* Falling Flower Petals */
        .petal { position: absolute; background-color: #ffb7c5; border-radius: 150% 0 150% 0; opacity: 0.8; pointer-events: none; animation: fall linear infinite; }
        @keyframes fall {
            0% { transform: translateY(-10vh) rotate(0deg) translateX(0); }
            100% { transform: translateY(110vh) rotate(360deg) translateX(60px); }
        }
    </style>
</head>
<body>

<div id="bg-layer"></div>

<div class="book-wrapper" onclick="openCard()">
    <div class="book" id="card">
        <div class="page front">
            <h1>Tap to Open 🌸</h1>
            <p>A beautiful surprise...</p>
        </div>
        <div class="page inside">
            <h1>Happy Birthday!</h1>
            <p>May your day bloom with joy.</p>
        </div>
    </div>
</div>

<script>
    function openCard() {
        const card = document.getElementById('card');
        const bg = document.getElementById('bg-layer');
        card.classList.toggle('open');
        
        // When opened, background changes and sharpens like the video
        if(card.classList.contains('open')) {
            bg.style.backgroundImage = "url('https://images.unsplash.com/photo-1493976040374-85c8e12f0c0e?auto=format&fit=crop&w=1920&q=80')";
            bg.style.filter = "brightness(1.1)";
        }
    }

    function createPetal() {
        const petal = document.createElement('div');
        petal.classList.add('petal');
        const size = Math.random() * 10 + 5 + 'px';
        petal.style.width = size;
        petal.style.height = size;
        petal.style.left = Math.random() * 100 + 'vw';
        petal.style.animationDuration = Math.random() * 2 + 3 + 's';
        document.body.appendChild(petal);
        setTimeout(() => petal.remove(), 5000);
    }
    setInterval(createPetal, 150); // This creates the constant flower fall
</script>
</body>
</html>
