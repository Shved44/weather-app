# weather-app
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Прогноз Погоды</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>🌦 Прогноз Погоды</h1>
    <p>Введите город, чтобы узнать погоду:</p>
    <input type="text" id="cityInput" placeholder="Например, Москва">
    <button onclick="getWeather()">Узнать</button>
    <div id="weatherResult"></div>
  </div>

  <script>
    async function getWeather() {
      const city = document.getElementById('cityInput').value;
      const apiKey = 'cba63f8d0ff115ebdc82229113a4035d'; // Вставь свой ключ от OpenWeatherMap
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&lang=ru&appid=${apiKey}`;

      const response = await fetch(url);
      const data = await response.json();

      if (data.cod === 200) {
        document.getElementById('weatherResult').innerHTML = `
          <h2>${data.name}</h2>
          <p>🌡 Температура: ${data.main.temp}°C</p>
          <p>💨 Ветер: ${data.wind.speed} м/с</p>
          <p>🌫 Описание: ${data.weather[0].description}</p>
        `;
      } else {
        document.getElementById('weatherResult').innerHTML = `<p>Город не найден.</p>`;
      }
    }
  </script>
</body>
</html>
