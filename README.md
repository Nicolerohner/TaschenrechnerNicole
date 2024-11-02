<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interaktiver Taschenrechner für den Schulalltag</title>
    <style>
    /* https://www.tobiaskohn.ch/jython/students_calculator-de.html */
    
        /* Grundlegende Stildefinitionen für den Body */
        body {
            font-family: Arial, sans-serif;
            background-color: #d7eeff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        /* Stil für den Taschenrechner */
        .calculator {
            width: 260px;
            background-color: #c0c0c0;
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.1);
        }

        /* Stil für das Display */
        .display {
            background-color: #555555;
            color: #FEF3B0;
            font-size: 2em;
            text-align: right;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 10px;
            min-height: 50px;
            overflow: hidden;
            white-space: nowrap;
        }

        /* Stil für die Tasten */
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-gap: 10px;
        }

        /* Stil für die einzelnen Tasten */
        .btn {
            padding: 20px;
            font-size: 1.5em;
            background-color: #fff;
            color: #000;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .btn:hover {
            background-color: #FEF3B0;
        }

        .btn:active {
            background-color: #fada5e;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="btn" onclick="clearDisplay()">C</button>
            <button class="btn" onclick="inputOperator('/')">/</button>
            <button class="btn" onclick="inputOperator('*')">*</button>
            <button class="btn" onclick="inputOperator('-')">-</button>
            
            <button class="btn" onclick="input('7')">7</button>
            <button class="btn" onclick="input('8')">8</button>
            <button class="btn" onclick="input('9')">9</button>
            <button class="btn" onclick="inputOperator('+')">+</button>
            
            <button class="btn" onclick="input('4')">4</button>
            <button class="btn" onclick="input('5')">5</button>
            <button class="btn" onclick="input('6')">6</button>
            <button class="btn" onclick="calculateResult()">=</button>
            
            <button class="btn" onclick="input('1')">1</button>
            <button class="btn" onclick="input('2')">2</button>
            <button class="btn" onclick="input('3')">3</button>
            
            <button class="btn" onclick="input('0')">0</button>
            <button class="btn" onclick="input('(')">(</button>
            <button class="btn" onclick="input(')')">)</button>
            <button class="btn" onclick="input('.')">.</button>
            
            <button class="btn" onclick="input('√(')">√</button>
        </div>
    </div>

    <script>
        let displayValue = ""; 
        const display = document.getElementById("display"); 

        function updateDisplay() {
            display.innerText = displayValue.length > 10 ? displayValue.slice(-10) : displayValue || "0";
        }

        function input(value) {
            if (displayValue === "0") displayValue = ""; 
            if (value === '.' && displayValue.slice(-1) === '.') return;
            displayValue += value;
            updateDisplay();
        }

        function clearDisplay() {
            displayValue = "";
            updateDisplay();
        }

        function calculateResult() {
            try {
                let evaluation = displayValue.replace(/√\(/g, 'Math.sqrt(');
                displayValue = (Math.round(new Function('return ' + evaluation)() * 100) / 100).toString();
            } catch {
                displayValue = "Error";
            }
            updateDisplay();
        }

        function inputOperator(op) {
            if ("+-*/".includes(displayValue.slice(-1))) {
                displayValue = displayValue.slice(0, -1) + op;
            } else {
                displayValue += op;
            }
            updateDisplay();
        }
    </script>
</body>
</html>
