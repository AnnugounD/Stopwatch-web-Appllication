<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #0e0e0e;
      margin: 0;
      padding: 40px;
      color: white;
    }

    h1 {
      margin-bottom: 20px;
    }

    .stopwatch {
      font-size: 48px;
      margin-bottom: 30px;
    }

    .glow-button {
      font-size: 18px;
      padding: 12px 25px;
      margin: 10px;
      background-color: #111;
      color: white;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      box-shadow:
        0 0 15px #8f00ff,
        0 0 30px #8f00ff,
        0 0 45px #8f00ff;
      transition: transform 0.2s ease, box-shadow 0.3s ease;
    }

    .glow-button:hover {
      transform: scale(1.05);
      box-shadow:
        0 0 20px #c800ff,
        0 0 40px #c800ff,
        0 0 60px #c800ff;
    }

    #laps {
      margin-top: 20px;
      list-style-type: none;
      padding: 0;
    }

    #laps li {
      background: #222;
      margin: 5px auto;
      padding: 8px;
      width: 200px;
      border-radius: 8px;
      color: #fff;
    }
  </style>
</head>
<body>

  <h1>⏱️ Stopwatch</h1>
  <div class="stopwatch" id="display">00:00:00</div>

  <button class="glow-button" onclick="start()">Start</button>
  <button class="glow-button" onclick="pause()">Pause</button>
  <button class="glow-button" onclick="reset()">Reset</button>
  <button class="glow-button" onclick="lap()">Lap</button>

  <ul id="laps"></ul>

  <script>
    let startTime = 0;
    let elapsedTime = 0;
    let timerInterval;
    let isRunning = false;

    function formatTime(ms) {
      let totalSeconds = Math.floor(ms / 1000);
      let hours = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
      let minutes = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
      let seconds = String(totalSeconds % 60).padStart(2, '0');
      return `${hours}:${minutes}:${seconds}`;
    }

    function updateDisplay() {
      document.getElementById('display').textContent = formatTime(elapsedTime);
    }

    function start() {
      if (!isRunning) {
        isRunning = true;
        startTime = Date.now() - elapsedTime;
        timerInterval = setInterval(() => {
          elapsedTime = Date.now() - startTime;
          updateDisplay();
        }, 100);
      }
    }

    function pause() {
      isRunning = false;
      clearInterval(timerInterval);
    }

    function reset() {
      isRunning = false;
      clearInterval(timerInterval);
      elapsedTime = 0;
      updateDisplay();
      document.getElementById('laps').innerHTML = '';
    }

    function lap() {
      if (isRunning) {
        const lapTime = formatTime(elapsedTime);
        const lapItem = document.createElement('li');
        lapItem.textContent = `Lap: ${lapTime}`;
        document.getElementById('laps').appendChild(lapItem);
      }
    }

    updateDisplay();
  </script>

</body>
</html>
