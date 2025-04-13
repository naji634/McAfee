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
      padding: 50px 20px;
    }

    #message {
      font-size: 20px;
      line-height: 2;
      white-space: pre-wrap;
      margin: 30px 0;
    }

    #countdown {
      font-size: 28px;
      color: yellow;
      margin-top: 10px;
    }

    .chat-box {
      width: 90%;
      max-width: 600px;
      margin: 40px auto;
      background: #111;
      padding: 20px;
      border-radius: 10px;
      text-align: left;
      border: 2px solid red;
    }

    .chat-message {
      margin: 10px 0;
    }

    .user {
      color: #0ff;
    }

    .attacker {
      color: #f33;
    }

    button {
      padding: 10px 20px;
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
  <div id="countdown"></div>
  <div id="message"></div>
  <div class="chat-box" id="chat" style="display:none;"></div>

  <script>
    // 戻る防止
    history.pushState(null, null, location.href);
    window.onpopstate = () => history.go(1);

    // カウントダウンの設定（24時間 = 86400秒）
    let secondsLeft = 86400;

    function startCountdown() {
      setInterval(() => {
        if (secondsLeft <= 0) return;
        secondsLeft--;
        const h = String(Math.floor(secondsLeft / 3600)).padStart(2, '0');
        const m = String(Math.floor((secondsLeft % 3600) / 60)).padStart(2, '0');
        const s = String(secondsLeft % 60).padStart(2, '0');
        document.getElementById("countdown").innerText = `⏳ 残り時間: ${h}:${m}:${s}`;
      }, 1000);
    }

    function showWarning() {
      document.documentElement.requestFullscreen();
      document.querySelector("button").style.display = "none";
      document.querySelector("h1").style.display = "none";

      startCountdown();

      const msg = `
⚠️ 緊急警告：あなたのデバイスはランサムウェアに感染しました。

💀 全ファイルが暗号化されました。パスワード、写真、クレジット情報、SNS履歴も含まれます。

🪙 復号化には50,000円分のビットコインが必要です。
⏳ 支払い期限を過ぎると、データは完全に削除され復元不可能になります。

📥 振込先: https://ransom.fake-btc-wallet.com

🔒 注意：再起動・電源オフ・第三者への通報は、即時データ削除の対象となります。
      `;
      document.getElementById("message").innerText = msg;

      const chat = document.getElementById("chat");
      chat.style.display = "block";

      const messages = [
        { sender: "attacker", text: "こんにちは。すべてのファイルを預かっています。" },
        { sender: "user", text: "誰だ！？どういうことだ！？" },
        { sender: "attacker", text: "復元したければ金を払え。24時間以内だ。" },
        { sender: "user", text: "本当に返してくれるのか？" },
        { sender: "attacker", text: "払えば解除キーを送る。払わなければ全削除だ。" },
      ];

      messages.forEach((msg, index) => {
        setTimeout(() => {
          const div = document.createElement("div");
          div.className = `chat-message ${msg.sender}`;
          div.textContent = (msg.sender === "user" ? "あなた: " : "犯人: ") + msg.text;
          chat.appendChild(div);
          chat.scrollTop = chat.scrollHeight;
        }, 2000 * index);
      });
    }
  </script>
</body>
</html>
