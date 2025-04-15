<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>ToolHubs-1</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f4f4f4;
    }
    header {
      background: #333;
      color: #fff;
      padding: 10px;
      text-align: center;
    }
    select {
      margin: 10px auto;
      display: block;
      padding: 8px;
      font-size: 16px;
    }
    section.tool {
      display: none;
      padding: 20px;
      background: white;
      margin: 20px auto;
      max-width: 800px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    section.active {
      display: block;
    }
  </style>
</head>
<body>
  <header>
    <h1>ToolHubs-1</h1>
  </header>

  <select id="toolSelector">
    <option value="password">Password Generator</option>
    <option value="textcase">Text Case Converter</option>
    <option value="wordcounter">Word Counter</option>
    <option value="colorpicker">Color Picker</option>
    <option value="imagecompressor">Image Compressor</option>
    <option value="calculator">Calculator</option>
    <option value="stopwatch">Stopwatch</option>
    <option value="qrcode">QR Generator</option>
    <option value="unitconverter">Unit Converter</option>
  </select>

  <section id="password" class="tool active">
    <!-- Password Generator Code Here -->
    <h2>Password Generator</h2>
    <p>[Working Password Generator code]</p>
  </section>

  <section id="textcase" class="tool">
    <!-- Text Case Converter Code Here -->
    <h2>Text Case Converter</h2>
    <p>[Working Text Case Converter code]</p>
  </section>

  <section id="wordcounter" class="tool">
    <!-- Word Counter Code Here -->
    <h2>Word Counter</h2>
    <p>[Working Word Counter code]</p>
  </section>

  <section id="colorpicker" class="tool">
    <!-- Color Picker Code Here -->
    <h2>Color Picker</h2>
    <p>[Working Color Picker code]</p>
  </section>

  <section id="imagecompressor" class="tool">
    <!-- Image Compressor Code Here -->
    <h2>Image Compressor</h2>
    <p>[Working Image Compressor code]</p>
  </section>

  <section id="calculator" class="tool">
    <h2>Calculator</h2>
    <input type="text" id="calcDisplay" readonly style="width:100%;font-size:20px;padding:5px;margin-bottom:10px;">
    <div>
      <button onclick="appendCalc('1')">1</button>
      <button onclick="appendCalc('2')">2</button>
      <button onclick="appendCalc('3')">3</button>
      <button onclick="appendCalc('+')">+</button><br>
      <button onclick="appendCalc('4')">4</button>
      <button onclick="appendCalc('5')">5</button>
      <button onclick="appendCalc('6')">6</button>
      <button onclick="appendCalc('-')">-</button><br>
      <button onclick="appendCalc('7')">7</button>
      <button onclick="appendCalc('8')">8</button>
      <button onclick="appendCalc('9')">9</button>
      <button onclick="appendCalc('*')">*</button><br>
      <button onclick="appendCalc('0')">0</button>
      <button onclick="appendCalc('.')">.</button>
      <button onclick="calculate()">=</button>
      <button onclick="appendCalc('/')">/</button>
      <button onclick="clearCalc()">C</button>
    </div>
  </section>

  <section id="stopwatch" class="tool">
    <h2>Stopwatch</h2>
    <p id="time">00:00:00</p>
    <button onclick="startStopwatch()">Start</button>
    <button onclick="stopStopwatch()">Stop</button>
    <button onclick="resetStopwatch()">Reset</button>
  </section>

  <section id="qrcode" class="tool">
    <h2>QR Code Generator</h2>
    <input type="text" id="qrText" placeholder="Enter text to generate QR">
    <button onclick="generateQR()">Generate</button>
    <div id="qrResult"></div>
  </section>

  <section id="unitconverter" class="tool">
    <h2>Unit Converter</h2>
    <input type="number" id="unitInput" placeholder="Enter value">
    <select id="unitType">
      <option value="km_miles">Km to Miles</option>
      <option value="miles_km">Miles to Km</option>
    </select>
    <button onclick="convertUnit()">Convert</button>
    <p id="unitResult"></p>
  </section>

  <script>
    const sections = document.querySelectorAll('.tool');
    document.getElementById('toolSelector').addEventListener('change', function () {
      sections.forEach(sec => sec.classList.remove('active'));
      document.getElementById(this.value).classList.add('active');
    });

    function appendCalc(value) {
      document.getElementById('calcDisplay').value += value;
    }
    function clearCalc() {
      document.getElementById('calcDisplay').value = '';
    }
    function calculate() {
      try {
        document.getElementById('calcDisplay').value = eval(document.getElementById('calcDisplay').value);
      } catch {
        alert('Invalid expression');
      }
    }

    let stopwatchInterval;
    let totalSeconds = 0;
    function startStopwatch() {
      if (!stopwatchInterval) {
        stopwatchInterval = setInterval(() => {
          totalSeconds++;
          const hrs = String(Math.floor(totalSeconds / 3600)).padStart(2, '0');
          const mins = String(Math.floor((totalSeconds % 3600) / 60)).padStart(2, '0');
          const secs = String(totalSeconds % 60).padStart(2, '0');
          document.getElementById('time').textContent = `${hrs}:${mins}:${secs}`;
        }, 1000);
      }
    }
    function stopStopwatch() {
      clearInterval(stopwatchInterval);
      stopwatchInterval = null;
    }
    function resetStopwatch() {
      stopStopwatch();
      totalSeconds = 0;
      document.getElementById('time').textContent = '00:00:00';
    }

    function generateQR() {
      const text = document.getElementById('qrText').value;
      document.getElementById('qrResult').innerHTML = `<img src='https://api.qrserver.com/v1/create-qr-code/?data=${encodeURIComponent(text)}&size=150x150'>`;
    }

    function convertUnit() {
      const val = parseFloat(document.getElementById('unitInput').value);
      const type = document.getElementById('unitType').value;
      let result = '';
      if (type === 'km_miles') {
        result = (val * 0.621371).toFixed(3) + ' Miles';
      } else if (type === 'miles_km') {
        result = (val / 0.621371).toFixed(3) + ' Km';
      }
      document.getElementById('unitResult').textContent = result;
    }
  </script>
</body>
</html>
