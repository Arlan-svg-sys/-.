<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kaspi.kz</title>

  <!-- Web App как приложение -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="default">
  <meta name="apple-mobile-web-app-title" content="Kaspi.kz">
  <link rel="apple-touch-icon" href="https://kaspi.kz/favicon.ico">

  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Roboto', sans-serif;
      background-color: #f2f2f2;
    }

    .header {
      background-color: #e30613;
      color: white;
      padding: 16px;
      text-align: center;
      font-size: 20px;
      font-weight: bold;
    }

    .tabs {
      display: flex;
      justify-content: space-around;
      background-color: white;
      border-bottom: 1px solid #ccc;
    }

    .tab {
      flex: 1;
      text-align: center;
      padding: 12px;
      cursor: pointer;
      font-weight: 500;
      color: #666;
      border-bottom: 3px solid transparent;
    }

    .tab.active {
      border-bottom: 3px solid #e30613;
      color: #e30613;
    }

    .container {
      max-width: 420px;
      margin: 0 auto;
      padding: 20px;
      background-color: white;
    }

    label {
      display: block;
      margin-top: 15px;
      font-size: 14px;
      color: #333;
    }
from pathlib import Path

# Сохраняем HTML-файл с готовой разметкой
html_content = """
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kaspi.kz</title>
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="default">
  <meta name="apple-mobile-web-app-title" content="Kaspi.kz">
  <link rel="apple-touch-icon" href="https://kaspi.kz/favicon.ico">
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Roboto', sans-serif;
      background-color: #f5f5f5;
    }
    .header {
      background-color: #e30613;
      color: white;
      padding: 16px;
      text-align: center;
      font-size: 20px;
      font-weight: bold;
    }
    .tabs, .bottom-nav {
      display: flex;
      justify-content: space-around;
      background-color: white;
    }
    .tab, .nav-item {
      flex: 1;
      text-align: center;
      padding: 12px;
      cursor: pointer;
      font-weight: 500;
      color: #666;
      border-bottom: 3px solid transparent;
    }
    .tab.active, .nav-item.active {
      color: #e30613;
      border-bottom: 3px solid #e30613;
    }
    .container {
      max-width: 420px;
      margin: 0 auto;
      padding: 20px;
      background-color: white;
    }
    label {
      display: block;
      margin-top: 15px;
      font-size: 14px;
      color: #333;
    }
    input[type="text"],
    input[type="date"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 15px;
    }
    input[type="file"] {
      display: none;
    }
    .file-label {
      display: inline-block;
      background-color: #e30613;
      color: white;
      text-align: center;
      padding: 12px;
      border-radius: 6px;
      cursor: pointer;
      margin-bottom: 15px;
      width: 100%;
    }
    .preview-img {
      width: 100%;
      margin-top: 10px;
      border-radius: 8px;
      display: none;
    }
    button {
      width: 100%;
      background-color: #e30613;
      color: white;
      padding: 14px;
      border: none;
      border-radius: 6px;
      font-size: 16px;
      margin-top: 20px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="header">Kaspi.kz</div>

  <div class="tabs">
    <div class="tab active" onclick="switchTab('doc')">Документ</div>
    <div class="tab" onclick="switchTab('info')">Реквизиты</div>
    <div class="tab" onclick="switchTab('history')">История</div>
  </div>

  <div class="container" id="docTab">
    <label for="photo" class="file-label">Загрузить удостоверение</label>
    <input type="file" id="photo" accept="image/*" onchange="loadImage(event)" />
    <img id="preview" class="preview-img" />
  </div>

  <div class="container" id="infoTab" style="display:none;">
    <label>ФИО</label>
    <input type="text" placeholder="Иванов Иван Иванович" />
    <label>ИИН</label>
    <input type="text" placeholder="000000000000" />
    <label>Дата выдачи</label>
    <input type="date" />
    <label>Номер документа</label>
    <input type="text" placeholder="123456789" />
    <button onclick="alert('Данные отправлены')">Отправить</button>
  </div>

  <div class="container" id="historyTab" style="display:none;">
    <p>История пуста</p>
  </div>

  <div class="bottom-nav">
    <div class="nav-item active">Kaspi ID</div>
    <div class="nav-item">Платежи</div>
    <div class="nav-item">Магазин</div>
  </div>

  <script>
    function switchTab(tab) {
      document.getElementById('docTab').style.display = tab === 'doc' ? 'block' : 'none';
      document.getElementById('infoTab').style.display = tab === 'info' ? 'block' : 'none';
      document.getElementById('historyTab').style.display = tab === 'history' ? 'block' : 'none';
      const tabs = document.querySelectorAll('.tab');
      tabs.forEach(t => t.classList.remove('active'));
      if (tab === 'doc') tabs[0].classList.add('active');
      else if (tab === 'info') tabs[1].classList.add('active');
      else tabs[2].classList.add('active');
    }
    function loadImage(event) {
      const image = document.getElementById('preview');
      image.src = URL.createObjectURL(event.target.files[0]);
      image.style.display = 'block';
    }
  </script>
</body>
</html>
"""

file_path = Path("/mnt/data/index.html")
file_path.write_text(html_content.strip(), encoding="utf-8")
file_path
