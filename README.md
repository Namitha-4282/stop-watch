<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch & Clock</title>
  <style>
    :root {
      --neon-blue: #0ff;
      --neon-pink: #ff00ff;
      --neon-green: #39ff14;
      --dark-bg: #0d0d0d;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: radial-gradient(circle at top, #1a1a1a 0%, #000 100%);
      color: var(--neon-blue);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }

    h1 {
      margin: 0.5rem;
      font-size: 2.5rem;
      color: var(--neon-pink);
      text-shadow: 0 0 10px var(--neon-pink);
    }

    .clock {
      font-size: 2rem;
      margin-bottom: 2rem;
      text-shadow: 0 0 10px var(--neon-blue);
    }

    .stopwatch {
      background-color: #111;
      border: 2px solid var(--neon-blue);
      padding: 2rem;
      border-radius: 1rem;
      box-shadow: 0 0 15px var(--neon-blue);
      text-align: center;
      max-width: 300px;
    }

    .time-display {
      font-size: 3rem;
      margin-bottom: 1.5rem;
      font-weight: bold;
      text-shadow: 0 0 12px var(--neon-green);
      color: var(--neon-green);
    }

    .buttons button {
      padding: 0.6rem 1.2rem;
      margin: 0.3rem;
      border: none;
      border-radius: 0.5rem;
      font-size: 1rem;
      font-weight: bold;
      cursor: pointer;
      color: #000;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .start {
      background-color: var(--neon-green);
      box-shadow: 0 0 10px var(--neon-green);
    }

    .stop {
      background-color: var(--neon-pink);
      box-shadow: 0 0 10px var(--neon-pink);
    }

    .reset {
      background-color: var(--neon-blue);
      box-shadow: 0 0 10px var(--neon-blue);
    }

    .buttons button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 20px white;
    }
  </style>
</head>
<body>

  <h1>Neon Stopwatch & Clock</h1>
  <div class="clock" id="clock">--:--:--</div>

  <div class="stopwatch">
    <div class="time-display" id="stopwatch">00:00:00</div>
    <div class="buttons">
      <button class="start" onclick="startStopwatch()">Start</button>
      <button class="stop" onclick="stopStopwatch()">Stop</button>
      <button class="reset" onclick="resetStopwatch()">Reset</button>
    </div>
  </div>

  <script>
    // Live Clock
    function updateClock() {
      const now = new Date();
      const time = now.toLocaleTimeString();
      document.getElementById('clock').textContent = time;
    }
    setInterval(updateClock, 1000);
    updateClock();

    // Stopwatch
    let startTime = 0;
    let elapsedTime = 0;
    let timerInterval;

    function updateStopwatch() {
      const time = Date.now() - startTime + elapsedTime;
      const seconds = Math.floor((time / 1000) % 60).toString().padStart(2, '0');
      const minutes = Math.floor((time / 60000) % 60).toString().padStart(2, '0');
      const hours = Math.floor(time / 3600000).toString().padStart(2, '0');
      document.getElementById('stopwatch').textContent = ${hours}:${minutes}:${seconds};
    }

    function startStopwatch() {
      if (!timerInterval) {
        startTime = Date.now();
        timerInterval = setInterval(updateStopwatch, 1000);
      }
    }

    function stopStopwatch() {
      if (timerInterval) {
        elapsedTime += Date.now() - startTime;
        clearInterval(timerInterval);
        timerInterval = null;
      }
    }

    function resetStopwatch() {
      clearInterval(timerInterval);
      timerInterval = null;
      startTime = 0;
      elapsedTime = 0;
      document.getElementById('stopwatch').textContent = '00:00:00';
    }
  </script>

</body>
</html>
