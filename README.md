<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stock Trading Bot Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            position: relative;
            overflow: hidden;
        }

        /* Candlestick background container */
        .candlestick-container {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: -1;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        canvas {
            width: 100%;
            height: 100%;
            position: absolute;
        }

        .login-box {
            background: rgba(0, 0, 0, 0.85);
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            color: white;
            box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.3);
            position: relative;
            z-index: 1;
        }

        input {
            width: 80%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            background: #222;
            color: white;
            text-align: center;
        }

        button {
            padding: 10px 20px;
            border: none;
            background: green;
            color: white;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background: darkgreen;
        }
    </style>
</head>
<body>

    <div class="candlestick-container">
        <canvas id="candlestickChart"></canvas>
    </div>

    <div class="login-box">
        <h2>Stock Trading Bot Login</h2>
        <input type="password" placeholder="Enter Password">
        <br>
        <button>Continue</button>
    </div>

    <script>
        // Candlestick pattern generator
        const canvas = document.getElementById("candlestickChart");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        function drawCandle(x, open, close, high, low) {
            ctx.strokeStyle = "white";
            ctx.fillStyle = close > open ? "green" : "red";
            
            // Wick
            ctx.beginPath();
            ctx.moveTo(x + 10, high);
            ctx.lineTo(x + 10, low);
            ctx.stroke();

            // Body
            ctx.fillRect(x, Math.min(open, close), 20, Math.abs(open - close));
        }

        function generateCandlesticks() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            let x = 50;
            for (let i = 0; i < 30; i++) {
                let open = Math.random() * (canvas.height / 2) + 100;
                let close = Math.random() * (canvas.height / 2) + 100;
                let high = Math.max(open, close) + Math.random() * 50;
                let low = Math.min(open, close) - Math.random() * 50;
                drawCandle(x, open, close, high, low);
                x += 30;
            }
        }

        generateCandlesticks();
    </script>

</body>
</html>
