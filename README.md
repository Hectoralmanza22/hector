<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Flor para Alexandra 🌻</title>
  <style>
    body {
      background-color: #1a1a1a;
      color: white;
      font-family: Arial, sans-serif;
      text-align: center;
      overflow: hidden;
    }
    #poem {
      margin-top: 40px;
      line-height: 1.8;
    }
    #start-btn {
      margin-top: 40px;
      padding: 10px 30px;
      font-size: 18px;
      font-weight: bold;
      background-color: #ffcc00;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      color: black;
    }
    #canvas-container {
      display: none;
    }
    canvas {
      background-color: #1a1a1a;
      display: block;
      margin: 0 auto;
    }
    #dynamic-text {
      margin-top: 20px;
      font-size: 16px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div id="poem">
    <p>En el jardín donde nace el sol,<br>
    florece un nombre lleno de calor.<br>
    No hay pétalo más tierno ni mejor color,<br>
    que el de tu risa, dulce esplendor.</p>

    <p>Cada hoja lleva tu luz callada,<br>
    cada brisa susurra tu mirada.<br>
    Y así, sin decirlo, el día se adorna,<br>
    cuando tu esencia en el alma retorna.</p>

    <p>Una flor nació, y el mundo brilló...<br>
    pero entonces llegaste tú,<br>
    y hasta el sol se enamoró.</p>

    <p><strong>Una flor para otra flor: Alexandra 🌻</strong></p>

    <button id="start-btn">Alexandra</button>
  </div>

  <div id="canvas-container">
    <canvas id="flowerCanvas" width="600" height="600"></canvas>
    <div id="dynamic-text">Señor solo tú sabes cuánto quiero a esta niña, eres mi sol 🌻</div>
  </div>

  <script>
    const btn = document.getElementById("start-btn");
    const poemDiv = document.getElementById("poem");
    const canvasContainer = document.getElementById("canvas-container");
    const canvas = document.getElementById("flowerCanvas");
    const ctx = canvas.getContext("2d");
    const dynamicText = document.getElementById("dynamic-text");

    btn.addEventListener("click", () => {
      poemDiv.style.display = "none";
      canvasContainer.style.display = "block";
      drawFlower();
      animateText();
    });

    function drawPetal(cx, cy, radius, angle, color) {
      ctx.save();
      ctx.translate(cx, cy);
      ctx.rotate(angle);
      ctx.beginPath();
      ctx.moveTo(0, 0);
      ctx.bezierCurveTo(radius / 2, -radius / 2, radius / 2, radius / 2, 0, radius);
      ctx.bezierCurveTo(-radius / 2, radius / 2, -radius / 2, -radius / 2, 0, 0);
      ctx.fillStyle = color;
      ctx.fill();
      ctx.restore();
    }

    function hsvToRgb(h, s, v) {
      let f = (n, k = (n + h * 6) % 6) =>
        v - v * s * Math.max(Math.min(k, 4 - k, 1), 0);
      return `rgb(${f(5) * 255},${f(3) * 255},${f(1) * 255})`;
    }

    function drawFlower() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      let numPetals = 72;
      let radius = 100;
      for (let i = 0; i < numPetals; i++) {
        let angle = (i * 2 * Math.PI) / numPetals;
        let color = hsvToRgb(i / numPetals, 1, 1);
        drawPetal(canvas.width / 2, canvas.height / 2, radius, angle, color);
      }

      // Semillas en espiral
      const centerX = canvas.width / 2;
      const centerY = canvas.height / 2;
      const phi = 137.5 * Math.PI / 180;
      for (let i = 0; i < 200; i++) {
        let r = 4 * Math.sqrt(i);
        let theta = i * phi;
        let x = centerX + r * Math.cos(theta);
        let y = centerY + r * Math.sin(theta);
        ctx.beginPath();
        ctx.arc(x, y, 2.5, 0, 2 * Math.PI);
        ctx.fillStyle = "red";
        ctx.fill();
      }
    }

    function animateText() {
      let tick = 0;
      function update() {
        let offset = Math.sin(tick * 0.1) * 5;
        dynamicText.style.transform = `translateY(${offset}px)`;
        tick++;
        requestAnimationFrame(update);
      }
      update();
    }
  </script>
</body>
</html>
