<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>💖 I Love You 💖</title>
<style>
  body {
    margin: 0;
    background: black;
    overflow: hidden;
    font-family: monospace;
    color: white;
  }

  canvas {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 0;
  }

  #controls {
    position: fixed;
    top: 10px;
    left: 10px;
    background: rgba(0, 0, 0, 0.7);
    padding: 10px;
    border-radius: 10px;
    z-index: 10;
    color: white;
    font-size: 14px;
  }

  label {
    display: block;
    margin-top: 6px;
  }

  h1 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: #00ff99;
    text-shadow: 0 0 20px #00ff99, 0 0 40px #00ff99;
    font-size: 3em;
  }
</style>
</head>
<body>

<div id="controls">
  <label>💨 Vitesse :
    <input type="range" id="speed" min="10" max="100" value="50">
  </label>
  <label>🎨 Couleur :
    <input type="color" id="color" value="#00ff00">
  </label>
  <label>🌍 Langue :
    <select id="lang">
      <option value="fr">Français (Je t'aime)</option>
      <option value="en">Anglais (I love you)</option>
      <option value="de">Allemand (Ich liebe dich)</option>
      <option value="pl">Polonais (Kocham cię)</option>
    </select>
  </label>
</div>

<h1 id="centerText">I Love You ❤️</h1>
<canvas id="matrix"></canvas>

<script>
  const canvas = document.getElementById('matrix');
  const ctx = canvas.getContext('2d');
  const speedControl = document.getElementById('speed');
  const colorPicker = document.getElementById('color');
  const langSelect = document.getElementById('lang');
  const centerText = document.getElementById('centerText');

  let color = colorPicker.value;
  let speed = 50;
  let words = ["I Love You"];

  const languages = {
    fr: ["Je t'aime", "Mon amour"],
    en: ["I Love You", "My Love"],
    de: ["Ich liebe dich", "Mein Schatz"],
    pl: ["Kocham cię", "Moja miłość"]
  };

  canvas.height = window.innerHeight;
  canvas.width = window.innerWidth;

  const fontSize = 16;
  const columns = canvas.width / fontSize;
  const drops = Array.from({ length: columns }).fill(1);

  function draw() {
    ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = color;
    ctx.font = fontSize + "px monospace";

    for (let i = 0; i < drops.length; i++) {
      const text = words[Math.floor(Math.random() * words.length)];
      ctx.fillText(text, i * fontSize, drops[i] * fontSize);

      if (drops[i] * fontSize > canvas.height && Math.random() > 0.975)
        drops[i] = 0;
      drops[i]++;
    }
  }

  let interval = setInterval(draw, speed);

  // 🎛️ Controls
  speedControl.oninput = () => {
    speed = 100 - speedControl.value;
    clearInterval(interval);
    interval = setInterval(draw, speed);
  };

  colorPicker.oninput = () => {
    color = colorPicker.value;
    centerText.style.color = color;
    centerText.style.textShadow = `0 0 20px ${color}, 0 0 40px ${color}`;
  };

  langSelect.onchange = () => {
    const selected = langSelect.value;
    words = languages[selected];
    centerText.textContent = words[0] + " ❤️";
  };

  // 🪄 Resize auto
  window.addEventListener("resize", () => {
    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;
  });
</script>

</body>
</html># Pour-toi
