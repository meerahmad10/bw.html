<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>🎁 Happy Birthday!</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background: linear-gradient(135deg, #ffecd2, #fcb69f);
      overflow: hidden;
      font-family: 'Poppins', sans-serif;
    }

    body {
      perspective: 1200px;
    }

    .scene {
      width: 100vw;
      height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .present {
      position: relative;
      width: 220px;
      height: 220px;
      transform-style: preserve-3d;
      transform: rotateX(-15deg) rotateY(15deg);
      animation: spin 12s infinite linear;
    }

    @keyframes spin {
      0%   { transform: rotateX(-15deg) rotateY(0deg); }
      100% { transform: rotateX(-15deg) rotateY(360deg); }
    }

    .box, .lid {
      position: absolute;
      width: 220px;
      height: 220px;
      background: linear-gradient(45deg, #ff4e50, #f9d423);
      box-shadow: 0 8px 20px rgba(0,0,0,0.3);
      border-radius: 12px;
    }

    .lid {
      background: linear-gradient(135deg, #ff416c, #ff4b2b);
      height: 40px;
      top: -40px;
      transform-origin: bottom center;
      animation: lidOpen 6s infinite ease-in-out;
      z-index: 10;
    }

    @keyframes lidOpen {
      0%, 100% { transform: rotateX(0deg); }
      50% { transform: rotateX(-90deg); }
    }

    .ribbon-h, .ribbon-v {
      position: absolute;
      background: #fff;
    }

    .ribbon-h {
      width: 100%;
      height: 20px;
      top: 100px;
      left: 0;
    }

    .ribbon-v {
      width: 20px;
      height: 100%;
      left: 100px;
      top: 0;
    }

    .text-inside {
      position: absolute;
      top: 80px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 90px;
      font-weight: bold;
      color: white;
      text-shadow: 0 0 10px #000;
      z-index: 2;
      animation: fadeIn 3s ease-out 3s forwards;
      opacity: 0;
    }

    @keyframes fadeIn {
      to { opacity: 1; }
    }

    .message {
      margin-top: 30px;
      font-size: 48px;
      color: #fff;
      text-shadow: 0 0 10px #fff, 0 0 20px #f0f;
      animation: fadeUp 2s forwards ease-in-out 4s;
      opacity: 0;
    }

    @keyframes fadeUp {
      to {
        transform: translateY(0);
        opacity: 1;
      }
    }

    .video-button {
      margin-top: 20px;
      padding: 12px 24px;
      background: linear-gradient(to right, #ff6a00, #ee0979);
      color: white;
      border: none;
      border-radius: 30px;
      font-size: 16px;
      cursor: pointer;
      box-shadow: 0 6px 15px rgba(0,0,0,0.3);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.1); }
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

    #slideshowModal {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      background: rgba(0,0,0,0.9);
      z-index: 999;
      align-items: center;
      justify-content: center;
      flex-direction: column;
    }

    #slideshowImage {
      max-width: 80vw;
      max-height: 80vh;
      border: 6px solid white;
      border-radius: 12px;
      box-shadow: 0 0 20px white;
    }

    #slideshowModal button {
      font-size: 18px;
      padding: 10px 20px;
      margin: 10px;
    }

    #slideshowModal span {
      position: absolute;
      top: 20px;
      right: 40px;
      color: white;
      font-size: 36px;
      cursor: pointer;
    }

    audio {
      display: none;
    }
  </style>
</head>
<body>
  <div class="scene">
    <div class="present">
      <div class="box">
        <div class="ribbon-h"></div>
        <div class="ribbon-v"></div>
        <div class="text-inside">U</div>
      </div>
      <div class="lid"></div>
    </div>

    <div class="message">🎉 Happy Birthday to You!</div>
    <button class="video-button" onclick="openVideo()">🎥 Watch Surprise</button>
    <button class="video-button" onclick="openMemoryLane()">🖼️ Click Me to Go on a Memory Lane</button>
  </div>

  <!-- Slideshow Modal -->
  <div id="slideshowModal">
    <span onclick="closeMemoryLane()">&times;</span>
    <img id="slideshowImage" src="https://via.placeholder.com/600x400?text=Memory+1">
    <div>
      <button onclick="prevImage()">⬅️ Back</button>
      <button onclick="nextImage()">Next ➡️</button>
    </div>
  </div>

  <audio id="birthdaySong" autoplay loop>
    <source src="birthday-song.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <script>
    // Confetti
    for (let i = 0; i < 100; i++) {
      const confetti = document.createElement('div');
      confetti.classList.add('confetti');
      confetti.style.left = Math.random() * window.innerWidth + 'px';
      confetti.style.animationDuration = (Math.random() * 3 + 2) + 's';
      confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 60%)`;
      document.body.appendChild(confetti);
    }

    // Balloons
    for (let i = 0; i < 6; i++) {
      const balloon = document.createElement('div');
      balloon.classList.add('balloon');
      balloon.style.left = `${10 + i * 15}%`;
      balloon.style.animationDelay = `${i * 1.5}s`;
      document.body.appendChild(balloon);
    }

    // Video Popup
    function openVideo() {
      const videoWindow = window.open('', '_blank', 'width=600,height=400');
      videoWindow.document.write(`
        <html><head><title>Surprise!</title></head><body style="margin:0; background:black; display:flex; align-items:center; justify-content:center;">
        <video controls autoplay style="width:100%; height:100%;">
          <source src="your-birthday-video.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video></body></html>`);
    }

    // Audio fallback
    window.addEventListener('click', () => {
      const audio = document.getElementById('birthdaySong');
      if (audio && audio.paused) {
        audio.play().catch(e => console.log('Autoplay blocked:', e));
      }
    });

    // Slideshow
    const images = [
      "img.png",
      "https://via.placeholder.com/600x400?text=Memory+2",
      "https://via.placeholder.com/600x400?text=Memory+3"
    ];
    let currentImageIndex = 0;

    function openMemoryLane() {
      document.getElementById("slideshowModal").style.display = "flex";
      showImage(currentImageIndex);
    }

    function closeMemoryLane() {
      document.getElementById("slideshowModal").style.display = "none";
    }

    function showImage(index) {
      document.getElementById("slideshowImage").src = images[index];
    }

    function nextImage() {
      currentImageIndex = (currentImageIndex + 1) % images.length;
      showImage(currentImageIndex);
    }

    function prevImage() {
      currentImageIndex = (currentImageIndex - 1 + images.length) % images.length;
      showImage(currentImageIndex);
    }
  </script>
</body>
</html>
