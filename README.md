# PRODIGY_WD_02
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #0f2027, #203a43, #2c5364);
      color: white;
      text-align: center;
      padding: 50px;
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 20px;
    }

    #display {
      font-size: 4rem;
      margin: 30px 0;
    }

    .buttons {
      margin: 20px;
    }

    button {
      font-size: 1.2rem;
      padding: 10px 20px;
      margin: 0 10px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background 0.3s;
    }

    button:hover {
      background-color: #555;
    }

    .start { background-color: #28a745; }
    .pause { background-color: #ffc107; }
    .reset { background-color: #dc3545; }
    .lap { background-color: #007bff; }

    #laps {
      margin-top: 30px;
      max-width: 400px;
      margin-left: auto;
      margin-right: auto;
      text-align: left;
    }

    #laps li {
      background: rgba(255, 255, 255, 0.1);
      padding: 8px;
      border-bottom: 1px solid #444;
      border-radius: 4px;
      margin: 5px 0;
    }
  </style>
</head>
<body>

  <h1>Stopwatch</h1>
  <div id="display">00:00:00.000</div>
  <div class="buttons">
    <button class="start" onclick="start()">Start</button>
    <button class="pause" onclick="pause()">Pause</button>
    <button class="reset" onclick="reset()">Reset</button>
    <button class="lap" onclick="recordLap()">Lap</button>
  </div>

  <ul id="laps"></ul>

  <script>
    let startTime = null;
    let elapsedTime = 0;
    let timerInterval = null;

    function updateDisplay(time) {
      const date = new Date(time);
      const minutes = String(date.getUTCMinutes()).padStart(2, '0');
      const seconds = String(date.getUTCSeconds()).padStart(2, '0');
      const milliseconds = String(date.getUTCMilliseconds()).padStart(3, '0');
      document.getElementById("display").textContent = `${minutes}:${seconds}.${milliseconds}`;
    }

    function start() {
      if (timerInterval) return; // already running

      startTime = Date.now() - elapsedTime;
      timerInterval = setInterval(() => {
        elapsedTime = Date.now() - startTime;
        updateDisplay(elapsedTime);
      }, 10);
    }

    function pause() {
      clearInterval(timerInterval);
      timerInterval = null;
    }

    function reset() {
      clearInterval(timerInterval);
      timerInterval = null;
      startTime = null;
      elapsedTime = 0;
      updateDisplay(0);
      document.getElementById("laps").innerHTML = '';
    }

    function recordLap() {
      if (!timerInterval) return;
      const lapTime = document.getElementById("display").textContent;
      const lapItem = document.createElement("li");
      lapItem.textContent = `Lap ${document.querySelectorAll("#laps li").length + 1}: ${lapTime}`;
      document.getElementById("laps").appendChild(lapItem);
    }
  </script>
</body>
</html>
