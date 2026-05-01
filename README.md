<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Happy Birthday Ruana</title>
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background: linear-gradient(135deg, #fff0f5, #ffe4f0);
      font-family: 'Comic Sans MS', cursive, sans-serif;
      flex-direction: column;
      overflow: hidden;
    }

    .container {
      text-align: center;
      z-index: 10;
    }

    h1 {
      font-size: 3rem;
      color: #ff4081;
      margin: 20px 0;
      text-shadow: 2px 2px 4px rgba(255, 64, 129, 0.3);
      animation: bounce 1s infinite;
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-20px); }
    }

    a {
      font-size: 2rem;
      cursor: pointer;
      text-decoration: none;
      padding: 20px 40px;
      background: #ff4081;
      color: white;
      border-radius: 50px;
      display: inline-block;
      transition: transform 0.3s, box-shadow 0.3s;
      box-shadow: 0 4px 15px rgba(255, 64, 129, 0.4);
    }

    a:hover {
      transform: scale(1.1);
      box-shadow: 0 6px 20px rgba(255, 64, 129, 0.6);
    }

    .character {
      position: fixed;
      font-size: 8rem;
      animation: popIn 0.6s ease-out forwards;
      z-index: 5;
    }

    .birthday-sign {
      position: absolute;
      top: -40px;
      font-size: 1.5rem;
      font-weight: bold;
      white-space: nowrap;
      animation: float 3s ease-in-out infinite;
    }

    @keyframes popIn {
      0% {
        transform: scale(0) rotate(-180deg);
        opacity: 0;
      }
      100% {
        transform: scale(1) rotate(0deg);
        opacity: 1;
      }
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-20px); }
    }

    .chiikawa-sign { color: #8B7355; }
    .mymelody-sign { color: #FFB6D9; }

    #message {
      display: none;
      font-size: 2.5rem;
      color: #ff1493;
      margin-top: 30px;
      text-shadow: 3px 3px 6px rgba(255, 20, 147, 0.3);
      animation: slideIn 0.8s ease-out;
    }

    @keyframes slideIn {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
  </style>
</head>
<body>

<div class="container">
  <a onclick="startCelebration(event)">🎉 Click here 🎉</a>
  <h1 id="message" style="display:none;">ルアナ、お誕生日おめでとう！🎂</h1>
</div>

<script>
function startCelebration(e) {
  e.preventDefault();

  document.getElementById("message").style.display = "block";

  // Show characters
  createCharacter('🐭', -200, 100, 'chiikawa-sign', 'Birthday!');
  createCharacter('🎀', window.innerWidth + 200, 150, 'mymelody-sign', 'Happy Birthday!');
// Changed from:
createCharacter('🐭', -200, 100, 'chiikawa-sign', 'Birthday!');
createCharacter('🎀', window.innerWidth + 200, 150, 'mymelody-sign', 'Happy Birthday!');

// Changed to:
createCharacter('🐭', 50, 150, 'chiikawa-sign', 'Birthday!');
createCharacter('🎀', window.innerWidth - 150, 150, 'mymelody-sign', 'Happy Birthday!');
  const duration = 3 * 1000;
  const end = Date.now() + duration;

  (function frame() {
    confetti({
      particleCount: 5,
      angle: 60,
      spread: 55,
      origin: { x: 0 }
    });
    confetti({
      particleCount: 5,
      angle: 120,
      spread: 55,
      origin: { x: 1 }
    });
    confetti({
      particleCount: 3,
      angle: 90,
      spread: 100,
      origin: { x: 0.5, y: 0 }
    });

    if (Date.now() < end) {
      requestAnimationFrame(frame);
    }
  })();
}

function createCharacter(emoji, x, y, signClass, signText) {
  const char = document.createElement('div');
  char.className = 'character';
  char.style.left = x + 'px';
  char.style.top = y + 'px';
  
  const sign = document.createElement('div');
  sign.className = 'birthday-sign ' + signClass;
  sign.textContent = signText;
  
  char.textContent = emoji;
  char.appendChild(sign);
  document.body.appendChild(char);

  // Remove after animation
  setTimeout(() => {
    char.remove();
  }, 6000);
}
</script>

</body>
</html>
