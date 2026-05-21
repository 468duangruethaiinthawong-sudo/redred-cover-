<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ประกาศผลการคัดเลือก Cover Dance ✨</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Prompt', 'Kanit', sans-serif;
            margin: 0;
            padding: 0;
        }

        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            padding: 30px;
            width: 100%;
            max-width: 450px;
            text-align: center;
        }

        h1 {
            color: #4a4a4a;
            margin-bottom: 15px;
            font-size: 24px;
        }

        .subtitle {
            color: #777;
            font-size: 14px;
            margin-bottom: 25px;
        }

        .input-group {
            margin-bottom: 25px;
        }

        /* สไตล์ของ Dropdown เลือกชื่อ */
        select {
            width: 100%;
            padding: 14px 20px;
            border: 2px solid #e0e0e0;
            border-radius: 25px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.3s;
            text-align-last: center; /* จัดตัวหนังสือให้อยู่ตรงกลาง */
            background-color: #fff;
            cursor: pointer;
            color: #333;
        }

        select:focus {
            border-color: #ff758c;
        }

        button {
            background: linear-gradient(135deg, #ff758c 0%, #ff7eb3 100%);
            color: white;
            border: none;
            padding: 14px 30px;
            font-size: 16px;
            border-radius: 25px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(255, 117, 140, 0.3);
            transition: transform 0.2s;
        }

        button:hover {
            transform: translateY(-2px);
        }

        .result-box {
            display: none;
            animation: fadeIn 0.5s ease-in-out;
        }

        .pass {
            color: #2ec4b6;
            font-size: 28px;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .fail {
            color: #e63946;
            font-size: 28px;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .message {
            font-size: 16px;
            line-height: 1.6;
            color: #555;
            margin-bottom: 20px;
            white-space: pre-line;
        }

        .qr-section {
            margin-top: 25px;
            padding: 20px;
            border: 2px dashed #ff758c;
            border-radius: 15px;
            background-color: #fff0f3;
        }

        .qr-code {
            width: 200px;
            height: 200px;
            margin: 15px auto;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .qr-code img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .btn-back {
            background: #6c757d;
            box-shadow: none;
            margin-top: 20px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&family=Prompt:wght@400;600&display=swap" rel="stylesheet">
</head>
<body>

<div class="container">
    <div id="login-screen">
        <h1>✨ ประกาศผลการคัดเลือก ✨</h1>
        <p class="subtitle">กรุณาเลือกชื่อของคุณเพื่อตรวจดูผลการคัดเลือก</p>
        
        <div class="input-group">
            <select id="name-select">
                <option value="" disabled selected>-- คลิกเพื่อเลือกชื่อของคุณ --</option>
                <option value="กอข้าว ม.4">กอข้าว ม.4</option>
                <option value="กอข้าว ม.1">กอข้าว ม.1</option>
                <option value="คิตตี้">คิตตี้</option>
                <option value="แพรวขวัญ">แพรวขวัญ</option>
                <option value="ปั้น">ปั้น</option>
                <option value="แก้มหอม">แก้มหอม</option>
                <option value="ออม">ออม</option>
                <option value="เป่าเป้ย">เป่าเป้ย</option>
            </select>
        </div>
        
        <button onclick="checkResult()">ดูผลประกาศ</button>
    </div>

    <div id="result-screen" class="result-box">
        <div id="result-status"></div>
        <div id="result-message" class="message"></div>
        
        <div id="qr-container" class="qr-section" style="display: none;">
            <p style="font-weight: bold; color: #ff758c;">🎉 ยินดีด้วยนะ! สแกน QR Code เข้ากลุ่ม IG เพื่อยืนยันสิทธิ์ได้เลยจ้า</p>
            <div class="qr-code">
                <img src="https://cdn.phototourl.com/free/2026-05-21-24ba9591-4be2-4988-9f69-5d0144085567.jpg" alt="IG Group QR Code">
            </div>
            <p style="font-size: 12px; color: #888;">*หากสแกนไม่ได้ ให้แคปหน้าจอไปเปิดในแอป Instagram นะคะ*</p>
        </div>

        <button class="btn-back" onclick="goBack()">กลับหน้าแรก</button>
    </div>
</div>

<script>
    // แยกรายชื่อกลุ่มคนผ่าน
    const passedList = ["กอข้าว ม.4", "แพรวขวัญ", "ปั้น", "เป่าเป้ย", "คิตตี้"];

    function checkResult() {
        const selectedName = document.getElementById('name-select').value;
        const loginScreen = document.getElementById('login-screen');
        const resultScreen = document.getElementById('result-screen');
        const resultStatus = document.getElementById('result-status');
        const resultMessage = document.getElementById('result-message');
        const qrContainer = document.getElementById('qr-container');

        // ถ้ายังไม่ได้เลือกชื่อแล้วกดปุ่ม
        if (selectedName === "") {
            alert("กรุณาเลือกชื่อตัวเองก่อนนะค้าบ! 😊");
            return;
        }

        // สลับหน้าจอ
        loginScreen.style.display = 'none';
        resultScreen.style.display = 'block';

        // เช็คผลลัพธ์จากชื่อที่เลือก
        if (passedList.includes(selectedName)) {
            // คนที่ผ่าน
            resultStatus.className = "pass";
            resultStatus.innerHTML = "🎉 คุณผ่านการคัดเลือก! 🎉";
            resultMessage.innerHTML = `ยินดีด้วยนะ <b>${selectedName}</b> ได้เข้ามาเป็นส่วนหนึ่งของทีมเราแล้ว!<br>ตั้งใจซ้อมไปด้วยกันนะค้าบ 💖`;
            qrContainer.style.display = 'block';
        } else {
            // คนที่ไม่ผ่าน (กอข้าว ม.1, แก้มหอม, ออม)
            resultStatus.className = "fail";
            resultStatus.innerHTML = "💖 สู้ๆ นะคะคนเก่ง 💖";
            resultMessage.innerHTML = `<b>${selectedName}</b> เก่งมากๆ เลยนะ ไม่ต้องเครียดนะ เราทำได้ดีมากมากแล้ว<br>พี่อยากรับทุกคนเลยจริงๆ ฮื่ออออ 🥺<br>ไว้โอกาสหน้ามาสนุกด้วยกันใหม่นะ อย่าเพิ่งท้อนะคนเก่ง!`;
            qrContainer.style.display = 'none';
        }
    }

    function goBack() {
        document.getElementById('login-screen').style.display = 'block';
        document.getElementById('result-screen').style.display = 'none';
        document.getElementById('name-select').selectedIndex = 0; // รีเซ็ตตัวเลือกกลับเป็นค่าเริ่มต้น
    }
</script>

</body>
</html>
