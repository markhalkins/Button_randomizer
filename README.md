<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Catch Me Button</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(to bottom, #f0f0f0, #ddd);
      overflow: hidden;
      font-family: Arial, sans-serif;
    }

    button {
      padding: 10px 20px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      position: absolute;
      transition: transform 0.2s;
    }

    button:active {
      transform: scale(1.2); /* click bounce effect */
    }

    /* Particle effect */
    .particle {
      position: absolute;
      width: 8px;
      height: 8px;
      background: gold;
      border-radius: 50%;
      opacity: 0.8;
      pointer-events: none;
      animation: explode 600ms ease-out forwards;
    }

    @keyframes explode {
      from { transform: scale(1) translate(0, 0); opacity: 1; }
      to { transform: scale(0.5) translate(var(--x), var(--y)); opacity: 0; }
    }
  </style>
</head>
<body>

  <button id="repel-btn">Catch Me</button>

  <audio id="click-sound" src="https://www.soundjay.com/buttons/sounds/button-16.mp3"></audio>

  <script>
    const btn = document.getElementById("repel-btn");
    const sound = document.getElementById("click-sound");

    btn.onmouseover = function() {
      // Get viewport size
      const maxX = window.innerWidth - this.offsetWidth;
      const maxY = window.innerHeight - this.offsetHeight;

      // Pick random position within bounds
      const newX = Math.random() * maxX;
      const newY = Math.random() * maxY;

      this.style.left = newX + "px";
      this.style.top = newY + "px";
    };

    btn.onclick = function(e) {
      // Play sound
      sound.currentTime = 0;
      sound.play();

      // Create particles
      for (let i = 0; i < 8; i++) {
        const particle = document.createElement("div");
        particle.classList.add("particle");

        // Random direction
        const angle = Math.random() * 2 * Math.PI;
        const distance = 50 + Math.random() * 50;
        particle.style.setProperty("--x", `${Math.cos(angle) * distance}px`);
        particle.style.setProperty("--y", `${Math.sin(angle) * distance}px`);

        // Position at click
        particle.style.left = e.pageX + "px";
        particle.style.top = e.pageY + "px";

        document.body.appendChild(particle);

        // Remove after animation
        particle.addEventListener("animationend", () => {
          particle.remove();
        });
      }
    };
  </script>
</body>
</html>
