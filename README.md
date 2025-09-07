<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Catch Me Button Game</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      font-family: "Comic Sans MS", cursive, sans-serif;
      overflow: hidden;
      background: linear-gradient(to top, #ffecd2, #fcb69f);
      position: relative;
    }

    h1 {
      margin-bottom: 60px;
      font-size: 2rem;
      color: #ff3e3e;
      text-shadow: 2px 2px #fff;
      animation: bounceText 1.2s infinite alternate;
    }

    @keyframes bounceText {
      from { transform: translateY(0); }
      to { transform: translateY(-10px); }
    }

    button {
      padding: 12px 24px;
      background: #ff6f61;
      color: white;
      font-weight: bold;
      font-size: 1.1rem;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      position: absolute;
      transition: transform 0.2s;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    }

    button:active {
      transform: scale(1.2) rotate(-3deg);
    }

    /* Particle effect */
    .particle {
      position: absolute;
      width: 10px;
      height: 10px;
      background: gold;
      border-radius: 50%;
      opacity: 0.8;
      pointer-events: none;
      animation: explode 700ms ease-out forwards;
    }

    @keyframes explode {
      from { transform: scale(1) translate(0, 0); opacity: 1; }
      to { transform: scale(0.5) translate(var(--x), var(--y)); opacity: 0; }
    }

    /* Fun background circles */
    .circle {
      position: absolute;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.3);
      animation: float 8s infinite ease-in-out;
    }

    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-20px); }
    }
  </style>
</head>
<body>

  <h1>✨ Click the button to get a secret reward! ✨</h1>

  <button id="repel-btn">Catch Me 🎁</button>

  <audio id="click-sound" src="https://www.soundjay.com/buttons/sounds/button-16.mp3"></audio>

  <script>
    const btn = document.getElementById("repel-btn");
    const sound = document.getElementById("click-sound");

    // Create background circles
    for (let i = 0; i < 10; i++) {
      const circle = document.createElement("div");
      circle.classList.add("circle");
      const size = Math.random() * 80 + 30;
      circle.style.width = circle.style.height = size + "px";
      circle.style.left = Math.random() * window.innerWidth + "px";
      circle.style.top = Math.random() * window.innerHeight + "px";
      circle.style.animationDuration = (6 + Math.random() * 6) + "s";
      document.body.appendChild(circle);
    }

    // Move button on hover
    btn.onmouseover = function() {
      const maxX = window.innerWidth - this.offsetWidth;
      const maxY = window.innerHeight - this.offsetHeight;

      const newX = Math.random() * maxX;
      const newY = Math.random() * maxY;

      this.style.left = newX + "px";
      this.style.top = newY + "px";
    };

    // Click effect
    btn.onclick = function(e) {
      // Play sound
      sound.currentTime = 0;
      sound.play();

      // Create particles
      for (let i = 0; i < 10; i++) {
        const particle = document.createElement("div");
        particle.classList.add("particle");

        const angle = Math.random() * 2 * Math.PI;
        const distance = 60 + Math.random() * 40;
        particle.style.setProperty("--x", `${Math.cos(angle) * distance}px`);
        particle.style.setProperty("--y", `${Math.sin(angle) * distance}px`);

        particle.style.left = e.pageX + "px";
        particle.style.top = e.pageY + "px";

        document.body.appendChild(particle);

        particle.addEventListener("animationend", () => {
          particle.remove();
        });
      }
    };
  </script>
</body>
</html>
