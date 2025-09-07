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
    }

    button {
      padding: 10px 20px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      position: absolute;
      transition: 0.2s;
    }
  </style>
</head>
<body>

  <button id="repel-btn">Catch Me</button>

  <script>
    const btn = document.getElementById("repel-btn");

    btn.onmouseover = function() {
      this.style.left = Math.random() * 90 + "vw";
      this.style.top = Math.random() * 90 + "vh";
    };
  </script>
</body>
</html>
