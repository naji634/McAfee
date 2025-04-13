<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>セキュリティ警告</title>
  <style>
    body {
      background: black;
      color: red;
      font-family: 'Courier New', monospace;
      text-align: center;
      overflow: hidden;
      animation: bgFlash 1s infinite alternate;
    }

    @keyframes bgFlash {
      0% { background: black; }
      100% { background: darkred; }
    }

    h1, p {
      margin: 20px;
      font-size: 2em;
    }

    .glitch {
      animation: glitch 0.3s infinite;
    }

    @keyframes glitch {
      0% { transform: translate(1px, -1px); }
      25% { transform: translate(-1px, 1px); }
      50% { transform: translate(1px, 1px); }
      75% { transform: translate(-1px, -1px); }
      100% { transform: translate(0, 0); }
    }

    #countdown {
      font-size: 3em;
      font-weight: bold;
    }

    button {
      padding: 10px 20px;
      font-size: 1.2em;
      background: red;
      color: white;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1 id="message">スキャン中...</h1>
  <button onclick="startRansom()">スキャンを続行</button>

  <script>
    // 無限戻り防止
    history.pushState(null, null, location.href);
    window.onpopstate = () => history.go(1);

    const ransomMessage = [
      "⚠️ システムが重大なウイルスに感染しました。",
      "💀 全ファイルは暗号化されました。",
      "🧨 復旧するには身代金が必要です。",
      "⏳ 制限時間以内に支払わないと全データは消去されます。",
      "🪙 0.01 BTC を以下のウォレットに送ってください。",
      "→ bc1qxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "⌛ タイマー："
    ];

    let i = 0;
    let message = document.getElementById("message");

    function typeMessage() {
      if (i < ransomMessage.length) {
        message.innerHTML = ransomMessage[i];
        i++;
        setTimeout(typeMessage, 2000);
      } else {
        startCountdown();
      }
    }

    function startRansom() {
      document.documentElement.requestFullscreen();
      document.querySelector("button").style.display = "none";
      message.classList.add("glitch");
      setTimeout(typeMessage, 1000);
    }

    function startCountdown() {
      const countdown = document.createElement("div");
      countdown.id = "countdown";
      document.body.appendChild(countdown);

      let time = 60; // 60秒カウントダウン
      const timer = setInterval(() => {
        countdown.textContent = time + " 秒";
        time--;
        if (time < 0) {
          clearInterval(timer);
          countdown.textContent = "💣 ファイルは削除されました。";
        }
      }, 1000);
    }
  </script>
</body>
</html>
