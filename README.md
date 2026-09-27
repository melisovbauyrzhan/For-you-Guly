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
      width: 100vw;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    #heart-wrapper {
      position: relative;
      width: 600px;
      height: 600px;
      max-width: 95vw;
      max-height: 95vw;
      display: flex;
      justify-content: center;
      align-items: center;
      animation: heartbeat 2s infinite ease-in-out;
    }

    @keyframes heartbeat {
      0%, 100% {
        transform: scale(1);
      }
      15% {
        transform: scale(1.08);
      }
      30% {
        transform: scale(0.98);
      }
      45% {
        transform: scale(1.05);
      }
    }

    .heart-char {
      position: absolute;
      font-weight: 900;
      font-size: 18px;
      color: #ff2a6d;
      user-select: none;
      transform-origin: center center;
      text-shadow: 0 0 8px #ff2a6d, 0 0 16px #ff2a6d, 0 0 24px #ff0055;
      opacity: 0;
      animation: fadeInChar 0.4s forwards;
    }

    @keyframes fadeInChar {
      to {
        opacity: 1;
      }
    }

    .center-letter {
      position: absolute;
      font-size: 110px;
      font-weight: 900;
      color: #ffffff;
      text-shadow: 0 0 10px #ff2a6d,
                   0 0 20px #ff2a6d,
                   0 0 40px #ff0055,
                   0 0 80px #ff0055;
      z-index: 10;
      user-select: none;
      top: 46%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-family: 'Georgia', 'Times New Roman', serif;
      animation: glowPulse 2s infinite ease-in-out;
    }

    @keyframes glowPulse {
      0%, 100% {
        text-shadow: 0 0 10px #ff2a6d, 0 0 20px #ff2a6d, 0 0 40px #ff0055, 0 0 80px #ff0055;
        transform: translate(-50%, -50%) scale(1);
      }
      50% {
        text-shadow: 0 0 15px #ff6699, 0 0 30px #ff2a6d, 0 0 60px #ff0055, 0 0 100px #ff0055;
        transform: translate(-50%, -50%) scale(1.05);
      }
    }

    .bg-heart {
      position: absolute;
      color: rgba(255, 42, 109, 0.25);
      pointer-events: none;
      user-select: none;
      animation: floatUp linear infinite;
    }

    @keyframes floatUp {
      0% {
        transform: translateY(105vh) rotate(0deg);
        opacity: 0;
      }
      20% {
        opacity: 0.5;
      }
      100% {
        transform: translateY(-10vh) rotate(360deg);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

  <div id="heart-wrapper">
    <div class="center-letter">G</div>
  </div>

  <script>
    const wrapper = document.getElementById('heart-wrapper');
    const textPattern = "I LOVE YOU "; // Последовательность букв
    const totalChars = 140; // Количество букв по контуру

    // Математическая формула для расчета точек контура сердца
    function getHeartPoint(t) {
      const x = 16 * Math.pow(Math.sin(t), 3);
      const y = -(13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t));
      return { x, y };
    }

    // Масштаб и центр контейнера
    const scale = 16;
    const centerX = 300;
    const centerY = 270;

    for (let i = 0; i < totalChars; i++) {
      const char = textPattern[i % textPattern.length];
      
      // Угол t расчитывается по всей окружности сердца
      const t = (i / totalChars) * Math.PI * 2;
      const point = getHeartPoint(t);

      const x = centerX + point.x * scale;
      const y = centerY + point.y * scale;

      const span = document.createElement('span');
      span.className = 'heart-char';
      span.innerText = char === ' ' ? '\u00A0' : char;

      span.style.left = `${x}px`;
      span.style.top = `${y}px`;
      
      // Плавная последовательная задержка появления букв
      span.style.animationDelay = `${i * 0.025}s`;

      wrapper.appendChild(span);
    }

    function createBgHeart() {
      const heart = document.createElement('div');
      heart.className = 'bg-heart';
      heart.innerHTML = '♥';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.fontSize = (Math.random() * 16 + 10) + 'px';
      heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
      
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 7000);
    }

    setInterval(createBgHeart, 250);
  </script>
</body>
</html>
