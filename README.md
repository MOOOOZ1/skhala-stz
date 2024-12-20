<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Калькулятор заработка</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #RGBA;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        .widget {
            max-width: 820px;
            margin: 0 auto;
            padding: 20px;
            background: #RGBA;
            border: 2px solid #fff;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .widget h3 {
            margin-bottom: 10px;
            font-size: 18px;
        }
        .slider-container {
            margin-bottom: 20px;
        }
        .slider-label {
            display: flex;
            justify-content: space-between;
            font-size: 14px;
        }
        .slider {
            width: 100%;
            margin: 10px 0;
        }
        .radio-group {
            margin: 10px 0;
        }
        .radio-group label {
            display: flex; 
            align-items: center;
            margin-bottom: 10px;
        }
        .radio-group input {
            margin-right: 10px;
        }
        .earnings {
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            color: #ffb800;
        }
    </style>
</head>
<body>
    <div class="widget">
        <h3>Рабочих дней</h3>
        <div class="slider-container">
            <input type="range" class="slider" min="8" max="30" value="24" step="1" id="days-slider">
          <div class="slider-label">
                <span>8</span><span>10</span><span>12</span><span>14</span><span>16</span><span>18</span><span>20</span><span>22</span><span>24</span><span>26</span><span>28</span><span>30</span>
            </div>
                    </div>

        <h3>Рабочих часов в день</h3>
        <div class="slider-container">
          <input type="range" class="slider" min="9" max="15" value="13" step="1" id="hours-slider">
            <div class="slider-label">
                <span>9</span><span>10</span><span>11</span><span>12</span><span>13</span><span>14</span><span>15</span>
            </div>
                  </div>

        <div class="radio-group">
            <label>
                <input type="radio" name="order-type" value="до 40 кг">
                буду работать один с заказами до 40кг
            </label>
            <label>
                <input type="radio" name="order-type" value="более 40 кг" checked>
                буду работать один с заказами более 40кг
            </label>
            <label>
                <input type="radio" name="order-type" value="с экспедитором">
                буду работать с экспедитором компании
            </label>
        </div>

        <div class="earnings">Мой заработок: <span id="earnings">403 200 руб.</span></div>
    </div>

    <script>
        const daysSlider = document.getElementById('days-slider');
        const hoursSlider = document.getElementById('hours-slider');
        const radioButtons = document.querySelectorAll('input[name="order-type"]');
        const earningsDisplay = document.getElementById('earnings');

        function getBaseRate() {
            let baseRate = 1000; // Default rate
            radioButtons.forEach((radio) => {
                if (radio.checked) {
                    if (radio.value === "более 40 кг") baseRate = 1200;
                    if (radio.value === "до 40 кг") baseRate = 1000;
                    if (radio.value === "с экспедитором") baseRate = 850;
                }
            });
            return baseRate;
        }

        function calculateEarnings() {
            const days = parseInt(daysSlider.value, 10);
            const hours = parseInt(hoursSlider.value, 10);
            const baseRate = getBaseRate();
            const earnings = days * (hours +1) * baseRate;
            earningsDisplay.textContent = `${earnings.toLocaleString('ru-RU')} руб.`;
        }

        daysSlider.addEventListener('input', calculateEarnings);
        hoursSlider.addEventListener('input', calculateEarnings);
        radioButtons.forEach((radio) =>
            radio.addEventListener('change', calculateEarnings)
        );
      </script>
</body>
