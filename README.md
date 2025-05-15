<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Happy Birthday!</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background: radial-gradient(circle at top left, #fceabb, #f8b500);
      overflow: hidden;
      font-family: 'Poppins', sans-serif;
    }

    .scene {
      position: relative;
      width: 100vw;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      perspective: 1500px;
    }

    .gift-box {
      position: relative;
      width: 200px;
      height: 200px;
      background: linear-gradient(45deg, #ff6f61, #d7263d);
      border-radius: 20px;
      transform-style: preserve-3d;
      animation: rotateBox 8s infinite linear;
    }

    .lid {
      position: absolute;
      width: 100%;
      height: 50px;
      background: #d7263d;
      top: -50px;
      border-radius: 20px 20px 0 0;
      transform-origin: bottom center;
      animation: openLid 5s infinite;
    }

    @keyframes openLid {
      0%, 100% { transform: rotateX(0deg); }
      50% { transform: rotateX(-90deg); }
    }

    @keyframes rotateBox {
      0% { transform: rotateY(0deg); }
      100% { transform: rotateY(360deg); }
    }

    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: red;
      animation: fall linear infinite;
    }

    @keyframes fall {
      0% { transform: translateY(-100vh) rotate(0deg); opacity: 1; }
      100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
    }

    .balloon {
      position: absolute;
      bottom: -150px;
      width: 60px;
      height: 80px;
      background: radial-gradient(circle, #ff5e78, #ff2a68);
      border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
      animation: floatBalloon 10s infinite ease-in-out;
    }

    .balloon::after {
      content: '';
      position: absolute;
      top: 80px;
      left: 50%;
      width: 2px;
      height: 60px;
      background: #333;
    }

    @keyframes floatBalloon {
      0% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-500px) rotate(5deg); }
      100% { transform: translateY(0) rotate(-5deg); }
    }

    .message {
      position: absolute;
      bottom: 50px;
      font-size: 36px;
      color: white;
      animation: fadeInUp 3s ease forwards;
      opacity: 0;
    }

    @keyframes fadeInUp {
      to {
        transform: translateY(-20px);
        opacity: 1;
      }
    }

    .video-button {
      position: absolute;
      top: 30px;
      right: 30px;
      padding: 10px 20px;
      background: #f03e3e;
      color: white;
      border: none;
      border-radius: 20px;
      font-size: 16px;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.1); }
      100% { transform: scale(1); }
    }
  </style>
</head>
<body>
  <div class="scene">
    <div class="gift-box">
      <div class="lid"></div>
    </div>
    <div class="message">🎉 Happy Birthday! 🎂</div>
    <button class="video-button" onclick="openVideo()">🎥 Watch Surprise</button>
  </div>

  <script>
    // Generate Confetti
    for (let i = 0; i < 100; i++) {
      const confetti = document.createElement('div');
      confetti.classList.add('confetti');
      confetti.style.left = Math.random() * window.innerWidth + 'px';
      confetti.style.animationDuration = (Math.random() * 3 + 2) + 's';
      confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
      document.body.appendChild(confetti);
    }

    // Generate Balloons
    for (let i = 0; i < 5; i++) {
      const balloon = document.createElement('div');
      balloon.classList.add('balloon');
      balloon.style.left = `${10 + i * 18}%`;
      balloon.style.animationDelay = `${i * 2}s`;
      document.body.appendChild(balloon);
    }

    // Video modal
    function openVideo() {
      const videoWindow = window.open('', '_blank', 'width=600,height=400');
      videoWindow.document.write(`
        <html><head><title>Surprise!</title></head><body style="margin:0; background:black; display:flex; align-items:center; justify-content:center;">
        <video controls autoplay style="width:100%; height:100%;">
          <source src="your-birthday-video.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video></body></html>`);
    }
  </script>
</body>
</html>
