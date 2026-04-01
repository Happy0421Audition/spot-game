<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>勁舞團 9 週年找碴大賽</title>
    <style>
        body { font-family: sans-serif; text-align: center; padding: 40px 10px; background: #f4f4f9; margin: 0; }
        .container { max-width: 500px; margin: auto; background: white; padding: 25px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        input, select { width: 90%; padding: 12px; margin: 10px 0; border: 1px solid #ddd; border-radius: 8px; font-size: 16px; outline: none; }
        input:focus, select:focus { border-color: #ff4757; }
        button { background: #ff4757; color: white; border: none; padding: 15px 40px; border-radius: 30px; cursor: pointer; margin-top: 20px; font-size: 18px; font-weight: bold; transition: 0.3s; }
        button:hover { background: #e84118; transform: scale(1.05); }
        p { color: #666; font-size: 14px; line-height: 1.6; }
        h2 { color: #333; margin-bottom: 5px; }
    </style>
</head>
<body>

<div class="container">
    <h2>🎯 找看看有幾隻哈特？</h2>
    <p>請先填寫基本資料開始遊戲</p>
    
    <input type="text" id="username" placeholder="您的勁舞團(快樂玩)帳號" required>
    <input type="text" id="nickname" placeholder="您的勁舞團暱稱" required>

    <div style="margin-top: 15px;">
        <img src="game.jpg" style="width: 100%; border-radius: 10px; border: 2px solid #333;">
        
        <p style="margin-top: 15px; font-weight: bold; color: #333;">🔍 請問圖中總共有幾隻哈特貓？</p>
        
        <select id="catCount">
            <option value="">-- 請選擇數量 --</option>
            <option value="10">10 隻</option>
            <option value="12">12 隻</option>
            <option value="16">16 隻</option>
            <option value="18">18 隻</option>
            <option value="20">20 隻</option>
        </select>
    </div>

    <button onclick="submitGame()">提交結果</button>
</div>

<script>
    function submitGame() {
        const name = document.getElementById('username').value;
        const nickname = document.getElementById('nickname').value;
        const answer = document.getElementById('catCount').value;
        
        // 檢查欄位是否填寫
        if(!name || !nickname || !answer) { 
            alert("請完整填寫資料並選擇答案唷！"); 
            return; 
        }
        
        // 你的 GAS 網址
        const scriptURL = 'https://script.google.com/macros/s/AKfycbwUFAeQJo8i8eBr8Jgq1d-UypxOZhqX9NWcXKL1iuQZINWpGB-6Tb1KJLRCuvZEUKd3/exec';

        const data = {
            name: name,
            phone: nickname, // 雖然變數名是 phone，但我們拿來存暱稱
            answer: answer   // 傳送選擇的答案
        };

        // 發送資料到 GAS
        fetch(scriptURL, {
            method: 'POST',
            mode: 'no-cors',
            cache: 'no-cache',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(data)
        })
        .then(() => {
            alert("提交成功！\n感謝 " + nickname + " 參與活動，答案已記錄。");
            // 提交後清空選項防止重複點擊
            document.getElementById('catCount').value = "";
        })
        .catch(error => {
            console.error('Error!', error.message);
            alert("提交失敗，請檢查網路連線。");
        });
    }
</script>

</body>
</html>
