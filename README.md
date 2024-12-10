# Geodez
Підключено jQuery до проекту через <script src="./node_modules/jquery/dist/jquery.min.js"></script>, але це неправильно! 
Коректно буде підключити jQuery через npm, для цього потрібно правильно налаштувати збірку проекту. Оскільки npm завантажує бібліотеку в node_modules, підключати її напряму через HTML неправильно. Замість цього використаємо JavaScript-збірник, наприклад Webpack.

1. Структура проекту:
bash
Копировать код
/my-project
  /dist
    index.html
    bundle.js  (згенерований)
  /src
    index.js   (основний код)
  node_modules/
  package.json
  webpack.config.js

2. Налаштування проекту:
2.1 Ініціалізація проекту:
bash

npm init -y

2.2 Встановлення залежностей:
bash

npm install jquery
npm install --save-dev webpack webpack-cli

3. Створимо файл src/index.js:
javascript

// src/index.js
import $ from "jquery";

$(document).ready(function() {
  console.log("jQuery успішно завантажено через npm!");
  $("h1").css("color", "blue");
});


4. Створимо файл index.html:
html

<!DOCTYPE html>
<html lang="uk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Проект з jQuery</title>
</head>
<body>
  <h1>Привіт, світ!</h1>

  <!-- Підключення згенерованого файлу -->
  <script src="./dist/bundle.js"></script>
</body>
</html>

5. Налаштуємо webpack.config.js:
javascript

// webpack.config.js
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  mode: "development",
};

6. Додамо скрипти до package.json:
json

"scripts": {
  "build": "webpack",
  "start": "webpack --watch"
}

7. Запуск проекту:
bash

npm run build
Потім відкриємо index.html у браузері.

Чому так:
npm install jquery: Завантажує jQuery у node_modules.
Webpack: Створює bundle.js для підключення в HTML.