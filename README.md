<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>検索ページ</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .search-container {
      text-align: center;
    }
    .search-box {
      width: 500px;
      padding: 12px;
      font-size: 16px;
      border: 1px solid #dcdcdc;
      border-radius: 24px;
      outline: none;
      box-sizing: border-box;
    }
    .search-button {
      margin-top: 20px;
      padding: 12px 24px;
      font-size: 16px;
      background-color: #f8f8f8;
      border: 1px solid #dcdcdc;
      border-radius: 24px;
      cursor: pointer;
      outline: none;
    }
    .search-button:hover {
      background-color: #f1f1f1;
    }
  </style>
</head>
<body>
  <div class="search-container">
    <h1>Google風検索ページ</h1>
    <input type="text" id="searchInput" class="search-box" placeholder="検索する内容を入力">
    <br>
    <button class="search-button" onclick="search()">検索</button>
  </div>

  <script>
    function search() {
      const query = document.getElementById("searchInput").value;
      if (query) {
        // Googleの検索URLにクエリを追加して検索
        window.location.href = `https://www.google.com/search?q=${encodeURIComponent(query)}`;
      }
    }
  </script>
</body>
</html>
