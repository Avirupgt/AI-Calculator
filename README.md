<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>  AI Calculator - Avirup</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
}


.calculator {
    backdrop-filter: blur(20px);
    background: rgba(255, 255, 255, 0.05);
    border-radius: 20px;
    padding: 20px;
    width: 320px;
    box-shadow: 0 0 40px rgba(0, 255, 255, 0.2);
}


.title {
    text-align: center;
    color: #00f7ff;
    font-size: 22px;
    margin-bottom: 15px;
    letter-spacing: 1px;
}


.display {
    background: rgba(0,0,0,0.6);
    color: #00ffcc;
    font-size: 36px;
    padding: 20px;
    border-radius: 12px;
    text-align: right;
    margin-bottom: 20px;
    min-height: 70px;
    box-shadow: inset 0 0 10px rgba(0,255,255,0.3);
}


.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
}

button {
    padding: 18px;
    font-size: 18px;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    color: white;
    background: rgba(255,255,255,0.1);
    transition: 0.2s;
}


button:hover {
    transform: scale(1.08);
    box-shadow: 0 0 10px #00f7ff;
}


.operator {
    background: rgba(0, 247, 255, 0.3);
}

.equals {
    background: #00ffcc;
    color: black;
    grid-column: span 2;
}

.clear {
    background: #ff4d4d;
    grid-column: span 2;
}


button:active {
    transform: scale(0.95);
}
</style>
</head>

<body>

<div class="calculator">
    <div class="title">⚡  AI Calculator - Avirup</div>
    <div id="display" class="display">0</div>

    <div class="buttons">
        <button class="clear" onclick="clearDisplay()">C</button>
        <button class="operator" onclick="append('/')">÷</button>
        <button class="operator" onclick="append('*')">×</button>

        <button onclick="append('7')">7</button>
        <button onclick="append('8')">8</button>
        <button onclick="append('9')">9</button>
        <button class="operator" onclick="append('-')">−</button>

        <button onclick="append('4')">4</button>
        <button onclick="append('5')">5</button>
        <button onclick="append('6')">6</button>
        <button class="operator" onclick="append('+')">+</button>

        <button onclick="append('1')">1</button>
        <button onclick="append('2')">2</button>
        <button onclick="append('3')">3</button>
        <button onclick="append('.')">.</button>

        <button onclick="append('0')">0</button>
        <button class="equals" onclick="calculate()">=</button>
    </div>
</div>

<script>
let display = document.getElementById("display");
let input = "0";

function append(value) {
    const last = input.slice(-1);

   
    if ("+-*/.".includes(last) && "+-*/.".includes(value)) return;

    if (input === "0" && value !== ".") {
        input = value;
    } else {
        input += value;
    }

    update();
}

function update() {
    display.innerText = input;
}

function clearDisplay() {
    input = "0";
    update();
}

function calculate() {
    try {
        input = Function('"use strict"; return (' + input + ')')().toString();
    } catch {
        input = "Error";
    }
    update();
}


document.addEventListener("keydown", e => {
    if (!isNaN(e.key)) append(e.key);
    else if ("+-*/".includes(e.key)) append(e.key);
    else if (e.key === ".") append(".");
    else if (e.key === "Enter") calculate();
    else if (e.key === "Backspace") {
        input = input.slice(0, -1) || "0";
        update();
    }
    else if (e.key.toLowerCase() === "c") clearDisplay();
});
</script>

</body>
</html>
