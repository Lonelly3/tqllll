<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Сердце из слов</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(to right, #ffb6c1, #ff9a9e);
      height: 100vh;
      width: 100vw;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: sans-serif;
      overflow: hidden;
      animation: backgroundChange 10s infinite alternate;
    }

    @keyframes backgroundChange {
      0% { background: linear-gradient(to right, #ffb6c1, #ff9a9e); }
      100% { background: linear-gradient(to right, #ff9a9e, #ffb6c1); }
    }

    .heart-container {
      position: relative;
      width: 90vw;
      height: 90vh;
      max-width: 800px;
      max-height: 700px;
      animation: heartPulse 3s infinite ease-in-out;
    }

    @keyframes heartPulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }

    .word {
      position: absolute;
      font-size: 1.2rem;
      color: crimson;
      white-space: nowrap;
      text-shadow: 0 0 5px #fff5f5;
      animation: shimmer 4s ease-in-out infinite, fadeIn 1s ease-in-out forwards;
    }

    @keyframes shimmer {
      0%, 100% { opacity: 0.8; transform: translateY(0); }
      50% { opacity: 1; transform: translateY(-5px); }
    }

    @keyframes fadeIn {
      0% { opacity: 0; }
      100% { opacity: 1; }
    }

    .taiqli {
      position: absolute;
      font-size: 2.2rem;
      color: darkred;
      font-weight: bold;
      white-space: nowrap;
      text-shadow: 0 0 10px white, 0 0 20px crimson;
      animation: pulse 2s infinite ease-in-out;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.15); }
    }

    .heart-float {
      position: absolute;
      color: #ffb6c1;
      font-size: 1.5rem;
      animation: floatUp 6s linear infinite, floatSideways 8s ease-in-out infinite;
      opacity: 0.6;
    }

    @keyframes floatUp {
      0% {
        transform: translateY(100vh) scale(0.5) rotate(0deg);
        opacity: 0;
      }
      20% { opacity: 0.8; }
      100% {
        transform: translateY(-10vh) scale(1) rotate(360deg);
        opacity: 0;
      }
    }

    @keyframes floatSideways {
      0% { transform: translateX(0); }
      50% { transform: translateX(20px); }
      100% { transform: translateX(-20px); }
    }
  </style>
</head>
<body>
  <!-- Встраиваем видео с YouTube с музыкой -->
  <iframe width="0" height="0" src="https://www.youtube.com/embed/vY7qccCPWC0?autoplay=1&loop=1&playlist=vY7qccCPWC0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

  <div class="heart-container" id="heart"></div>

  <script>
    const words = [
      "Милая", "Любимая", "Нежная", "Солнышко", "Ангелочек", "Котёнок", "Радость", "Крошка",
      "Звёздочка", "Лапочка", "Душа", "Прелесть", "Бести", "Обожаю", "Крутышка", "Нежная",
      "Ласкавая", "Вдохновляет", "Волшебная", "Сказка", "Улыбочка", "Сердечко", "Чудо",
      "Самая Красивая", "Малышка", "Чудесная", "Лучшая", "Неповторимая", "Любимка", "Нежуля"
    ];

    function createHeart() {
      const heartContainer = document.getElementById("heart");
      heartContainer.innerHTML = ""; // Очищаем, если перерисовываем

      const centerX = heartContainer.offsetWidth / 2;
      const centerY = heartContainer.offsetHeight / 2;
      const scale = Math.min(heartContainer.offsetWidth, heartContainer.offsetHeight) / 35;

      for (let i = 0; i < words.length; i++) {
        const t = Math.PI * 2 * (i / words.length);
        const x = 16 * Math.pow(Math.sin(t), 3);
        const y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);

        const word = document.createElement("div");
        word.className = "word";
        word.textContent = words[i];
        word.style.left = `${centerX + x * scale - 25}px`;
        word.style.top = `${centerY - y * scale - 15}px`;
        heartContainer.appendChild(word);
      }

      const center = document.createElement("div");
      center.className = "taiqli";
      center.textContent = "taiqli";
      center.style.left = `${centerX - 35}px`;
      center.style.top = `${centerY}px`;
      heartContainer.appendChild(center);
    }

    function createFloatingHeart() {
      const heart = document.createElement("div");
      heart.className = "heart-float";
      heart.innerHTML = "❤️";
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.fontSize = (Math.random() * 1.5 + 1) + "rem";
      heart.style.opacity = Math.random() * 0.6 + 0.4;
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 6000);
    }

    window.addEventListener('load', () => {
      createHeart();
      setInterval(createFloatingHeart, 400);
    });

    window.addEventListener('resize', createHeart);
  </script>
</body>
</html>
