<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>I LOVE YOU - G</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background-color: #0b0208;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      font-family: 'Arial', sans-serif;
    }

    /* Красивый заголовок над сердцем */
    .site-title {
      color: #ffffff;
      font-size: 28px;
      font-weight: 700;
      margin-bottom: 20px;
      text-shadow: 0 0 10px #ff2a6d, 0 0 20px #ff2a6d;
      letter-spacing: 2px;
      z-index: 10;
    }

    #heart-wrapper {
      position: relative;
      width: 600px;
      height: 600px;
      animation: heartbeat 1.8s infinite ease-in-out;
    }

    .heart-char {
      position: absolute;
      font-weight: 800;
      font-size: 16px;
      color: #ff2a6d;
      white-space: nowrap;
      user-select: none;
      transform-origin: center center;
      text-shadow: 0 0 8px #ff2a6d, 0 0 16px #ff2a6d;
    }

    .center-letter {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 110px;
      font-weight: 900;
      color: #ffffff;
      text-shadow: 0 0 20px #ff2a6d, 0 0 40px #ff2a6d, 0 0 60px #ff2a6d;
      user-select: none;
      z-index: 10;
    }

    @keyframes heartbeat {
      0%, 100% { transform: scale(1); }
      15% { transform: scale(1.08); }
      30% { transform: scale(0.98); }
      45% { transform: scale(1.05); }
    }

    .floating-heart {
      position: absolute;
      color: rgba(255, 42, 109, 0.25);
      pointer-events: none;
      animation: floatUp linear infinite;
    }

    @keyframes floatUp {
      0% { transform: translateY(105vh) rotate(0deg); opacity: 0; }
      20% { opacity: 0.5; }
      100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
    }
  </style>
</head>
<body>

  <!-- Надпись над сердцем -->
  <div class="site-title">For you Guly</div>

  <div id="heart-wrapper">
    <div class="center-letter">G</div>
  </div>

  <script>
    const wrapper = document.getElementById('heart-wrapper');
    const textPattern = "I LOVE YOU ";
    const totalChars = 140;

    function getHeartPoint(t) {
      const x = 16 * Math.pow(Math.sin(t), 3);
      const y = -(13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t));
      return { x, y };
    }

    const scale = 16;
    const centerX = 300;
    const centerY = 270;

    for (let i = 0; i < totalChars; i++) {
      const char = textPattern[i % textPattern.length];
      const t = (i / totalChars) * Math.PI * 2;
      const point = getHeartPoint(t);

      const x = centerX + point.x * scale;
      const y = centerY + point.y * scale;

      const span = document.createElement('span');
      span.className = 'heart-char';
      span.innerText = char === ' ' ? '\u00A0' : char;

      span.style.left = `${x}px`;
      span.style.top = `${y}px`;

      wrapper.appendChild(span);
    }

    function spawnBackgroundHeart() {
      const heart = document.createElement('div');
      heart.className = 'floating-heart';
      heart.innerHTML = '♥';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.fontSize = (Math.random() * 18 + 12) + 'px';
      heart.style.animationDuration = (Math.random() * 4 + 4) + 's';
      
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 8000);
    }

    setInterval(spawnBackgroundHeart, 250);
  </script>
</body>
</html>
