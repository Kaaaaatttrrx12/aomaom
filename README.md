<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aom Massage & Spa</title>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            --pink: #ffd1dc;
            --brown: #c4a484;
            --bg: #fff5f5;
            --text: #5c4033;
            --glass: rgba(255, 255, 255, 0.6);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Kanit', sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            padding-bottom: 100px;
            overflow-x: hidden;
            position: relative;
        }

        /* Floating Emojis */
        .emoji-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: -1;
        }
        .floating-emoji {
            position: absolute;
            font-size: 24px;
            animation: floatUp linear infinite;
            opacity: 0.6;
        }
        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0.8); opacity: 0; }
            10% { opacity: 0.8; }
            90% { opacity: 0.8; }
            100% { transform: translateY(-10vh) scale(1.2); opacity: 0; }
        }

        /* Header & Profile */
        .header {
            text-align: center;
            padding: 30px 20px 10px;
        }
        .profile-pic {
            width: 100px;
            height: 100px;
            background-color: var(--pink);
            border: 3px solid var(--brown);
            border-radius: 50%;
            margin: 0 auto 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text);
            font-size: 14px;
            overflow: hidden;
        }
        .profile-pic img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none; /* Show this when you add an image source */
        }
        
        .music-btn {
            background: var(--brown);
            color: white;
            border: none;
            padding: 5px 15px;
            border-radius: 20px;
            cursor: pointer;
            margin-bottom: 20px;
            font-size: 14px;
        }

        /* Pages */
        .page {
            display: none;
            padding: 0 20px;
            max-width: 600px;
            margin: 0 auto;
            animation: fadeIn 0.4s ease;
        }
        .page.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Top 2 Columns (Clock & Calendar) */
        .top-widgets {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }
        .widget-card {
            background: rgba(255, 255, 255, 0.8);
            padding: 15px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            border: 1px solid var(--pink);
            cursor: pointer;
            transition: transform 0.2s;
        }
        .widget-card:hover {
            transform: scale(1.02);
        }
        #clock {
            font-size: 20px;
            font-weight: 500;
            color: var(--brown);
        }

        /* Accordion Services */
        details {
            background: white;
            border-radius: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            overflow: hidden;
            border-left: 5px solid var(--pink);
        }
        summary {
            padding: 15px;
            font-weight: 500;
            cursor: pointer;
            list-style: none;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        summary::after {
            content: '▼';
            font-size: 12px;
            color: var(--brown);
        }
        details[open] summary::after {
            content: '▲';
        }
        .service-info {
            padding: 15px;
            border-top: 1px dashed var(--pink);
            font-size: 14px;
            line-height: 1.6;
        }
        .img-placeholder {
            width: 100%;
            height: 150px;
            background-color: #f0e6e6;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #999;
            margin-bottom: 15px;
        }

        /* Page 2 Cards */
        .info-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            border-top: 5px solid var(--brown);
        }
        .info-card h3 {
            color: var(--brown);
            margin-bottom: 15px;
        }
        .info-card ul {
            margin-left: 20px;
            margin-bottom: 10px;
            font-size: 14px;
        }
        .divider {
            height: 1px;
            background: var(--pink);
            margin: 15px 0;
        }

        /* Mac OS Dock */
        .dock {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--glass);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            padding: 10px 25px;
            border-radius: 30px;
            display: flex;
            gap: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            border: 1px solid rgba(255,255,255,0.4);
            z-index: 100;
        }
        .dock-btn {
            background: none;
            border: none;
            font-size: 28px;
            cursor: pointer;
            transition: transform 0.2s;
            position: relative;
        }
        .dock-btn:hover {
            transform: scale(1.2) translateY(-5px);
        }
        .dock-btn.active::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 50%;
            transform: translateX(-50%);
            width: 5px;
            height: 5px;
            background-color: var(--brown);
            border-radius: 50%;
        }
    </style>
</head>
<body>

    <audio id="bgMusic" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-15.mp3" type="audio/mpeg">
    </audio>
    <audio id="clickSound">
        <source src="https://www.soundjay.com/buttons/sounds/button-3.mp3" type="audio/mpeg">
    </audio>

    <div class="emoji-container" id="emojis"></div>

    <div class="header">
        <div class="profile-pic">
            <img src="" alt="Profile" id="profileImg">
            <span id="picText">ใส่รูปที่นี่</span>
        </div>
        <h2>ร้านนวด aom 🩷</h2>
        <p style="font-size: 14px; color: var(--brown); margin-bottom: 10px;">ผ่อนคลาย สไตล์คาเฟ่</p>
        <button class="music-btn" onclick="toggleMusic()">🎵 เล่นเพลงคลอเบาๆ</button>
    </div>

    <div id="page1" class="page active">
        <div class="top-widgets">
            <div class="widget-card">
                <div style="font-size: 24px; margin-bottom: 5px;">⏱️</div>
                <div id="clock">00:00:00</div>
            </div>
            <div class="widget-card" onclick="checkSpecialDay()">
                <div style="font-size: 24px; margin-bottom: 5px;">📅</div>
                <div style="font-size: 14px; font-weight: 500;">ปฏิทินวันนี้</div>
                <div style="font-size: 12px; color: #888;">(กดเพื่อดูวันสำคัญ)</div>
            </div>
        </div>

        <h3 style="margin-bottom: 15px; color: var(--brown);">💆‍♀️ รายการบริการ</h3>

        <details>
            <summary>1. นวดแผนไทย (Traditional Thai)</summary>
            <div class="service-info">
                <div class="img-placeholder">[ เว้นไว้ใส่รูปภาพนวดไทย ]</div>
                <p>⏱️ <b>เวลา:</b> 1 / 2 ชั่วโมง</p>
                <p>💰 <b>ราคา:</b></p>
                <ul>
                    <li>1 ชม. ≈ 180 – 300 บาท</li>
                    <li>2 ชม. ≈ 400 – 600 บาท</li>
                </ul>
                <p>📌 <b>จุดเด่น:</b> ยืดเส้น คลายปวดลึก เหมาะคนเมื่อยหนัก</p>
            </div>
        </details>

        <details>
            <summary>2. นวดน้ำมัน / อโรมา</summary>
            <div class="service-info">
                <div class="img-placeholder">[ เว้นไว้ใส่รูปภาพนวดอโรมา ]</div>
                <p>⏱️ <b>เวลา:</b> 1 / 1.5 / 2 ชั่วโมง</p>
                <p>💰 <b>ราคา:</b></p>
                <ul>
                    <li>1 ชม. ≈ 350 – 400 บาท</li>
                    <li>90 นาที ≈ 600 – 700 บาท</li>
                </ul>
                <p>📌 <b>จุดเด่น:</b> ผ่อนคลาย กลิ่นหอม เบากว่านวดไทย</p>
            </div>
        </details>

        <details>
            <summary>3. นวดคอ บ่า ไหล่ (Office Syndrome)</summary>
            <div class="service-info">
                <div class="img-placeholder">[ เว้นไว้ใส่รูปภาพนวดคอบ่าไหล่ ]</div>
                <p>⏱️ <b>เวลา:</b> 1 ชั่วโมง</p>
                <p>💰 <b>ราคา:</b> ≈ 250 – 300 บาท</p>
                <p>📌 <b>จุดเด่น:</b> เน้นจุดปวดเฉพาะคนทำงาน</p>
            </div>
        </details>

        <details>
            <summary>4. นวดเท้า (Foot Reflexology)</summary>
            <div class="service-info">
                <div class="img-placeholder">[ เว้นไว้ใส่รูปภาพนวดเท้า ]</div>
                <p>⏱️ <b>เวลา:</b> 1 ชั่วโมง</p>
                <p>💰 <b>ราคา:</b> ≈ 200 – 300 บาท</p>
                <p>📌 <b>จุดเด่น:</b> กระตุ้นการไหลเวียน เหมาะคนยืนนาน</p>
            </div>
        </details>

        <details>
            <summary>5. นวดประคบ / รีดเส้น (สายลึก)</summary>
            <div class="service-info">
                <div class="img-placeholder">[ เว้นไว้ใส่รูปภาพนวดประคบ ]</div>
                <p>⏱️ <b>เวลา:</b> 1 ชั่วโมง</p>
                <p>💰 <b>ราคา:</b> ≈ 350 – 450 บาท</p>
                <p>📌 <b>จุดเด่น:</b> ลดอักเสบ + กล้ามเนื้อคลายลึก</p>
            </div>
        </details>
    </div>

    <div id="page2" class="page">
        <div class="info-card">
            <div class="img-placeholder" style="height: 180px;">[ เว้นไว้ใส่รูปภาพนวดกษัย ]</div>
            <h3>💆‍♀️ นวดกษัยคืออะไร</h3>
            <p>เป็นการนวดเน้นบริเวณ:</p>
            <ul>
                <li>ท้องน้อย</li>
                <li>ขาหนีบ</li>
                <li>เส้นลมปราณ (เส้นประธานในร่างกาย)</li>
            </ul>
            <p>👉 ใช้กด คลึง ไล่ลม เพื่อกระตุ้นการไหลเวียน</p>
            
            <div class="divider"></div>
            
            <h4 style="margin-bottom: 10px;">🧠 ทำไมต้องนวดกษัย</h4>
            <p><b>1. ช่วยระบบไหลเวียนดีขึ้น</b></p>
            <ul><li>เลือด+ลมเดินสะดวก ลดอาการแน่นท้อง</li></ul>
            <p><b>2. แก้ปัญหาท้องผูก</b></p>
            <ul><li>กระตุ้นลำไส้ ขับของเสียง่ายขึ้น (คนที่นั่งนานจะได้ผลชัด)</li></ul>
            <p><b>3. ช่วยเรื่องฮอร์โมน</b></p>
            <ul><li>มดลูก/รังไข่ (หญิง), ระบบสืบพันธุ์ (ชาย) ปรับสมดุล</li></ul>
            <p><b>4. ลดอาการปวดเอว</b></p>
            <ul><li>ปวดประจำเดือน มีพุงตึงๆ แข็งๆ</li></ul>
            <p><b>5. ช่วยให้หน้าท้องนิ่มลง</b></p>
            <ul><li>คลายพังผืด ลดอาการท้องแข็งแน่น</li></ul>
            
            <div class="divider"></div>
            
            <div style="background: #fff0f0; padding: 10px; border-radius: 8px;">
                <p style="color: #d9534f; font-weight: 500;">⚠️ ข้อควรรู้ (สำคัญมาก)</p>
                <ul style="margin-bottom: 0;">
                    <li>❌ ไม่ควรนวดตอนอิ่มจัด</li>
                    <li>❌ คนท้อง / หลังผ่าตัด / มีโรคภายใน ต้องระวัง</li>
                    <li>❗ ต้องทำโดยคนที่มีความรู้จริง</li>
                </ul>
            </div>
        </div>

        <div class="info-card">
            <div class="img-placeholder" style="height: 180px;">[ เว้นไว้ใส่รูปภาพนวดอโรม่า ]</div>
            <h3>🌿 ทำไมถึงควรนวดอโรม่า</h3>
            <p><b>1. คลายเครียดได้เร็วมาก</b></p>
            <ul>
                <li>กลิ่นน้ำมันหอมระเหย ส่งผลกับสมองโดยตรง</li>
                <li>ช่วยให้ใจนิ่ง ลดความฟุ้ง</li>
                <li>💡 <i>เหมาะกับคนเครียด นอนไม่หลับ</i></li>
            </ul>
            <div class="divider"></div>
            <p><b>2. ผ่อนคลายกล้ามเนื้อแบบนุ่มลึก</b></p>
            <ul>
                <li>ไม่กดแรงเหมือนนวดไทย ใช้การ "ลูบ ไล้ กดเบา"</li>
                <li>👉 <i>เหมาะกับคนไม่ชอบเจ็บ หรือคนร่างกายล้า</i></li>
            </ul>
        </div>
    </div>

    <div class="dock">
        <button class="dock-btn active" onclick="switchPage('page1', this)">🏠</button>
        <button class="dock-btn" onclick="switchPage('page2', this)">🤍</button>
    </div>

    <script>
        // --- 1. Audio & Clicks ---
        const clickSound = document.getElementById('clickSound');
        const bgMusic = document.getElementById('bgMusic');
        let isMusicPlaying = false;

        function playClick() {
            clickSound.currentTime = 0;
            clickSound.play().catch(e => console.log("รอการโต้ตอบจากผู้ใช้"));
        }

        function toggleMusic() {
            if (isMusicPlaying) {
                bgMusic.pause();
                document.querySelector('.music-btn').innerText = "🎵 เล่นเพลงคลอเบาๆ";
            } else {
                bgMusic.volume = 0.2; // เสียงเบาๆ สไตล์คาเฟ่
                bgMusic.play();
                document.querySelector('.music-btn').innerText = "⏸️ หยุดเพลง";
            }
            isMusicPlaying = !isMusicPlaying;
            playClick();
        }

        // --- 2. Page Navigation ---
        function switchPage(pageId, btnElement) {
            playClick();
            // ซ่อนทุกหน้า
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            // เอาจุด active ออกจากปุ่ม
            document.querySelectorAll('.dock-btn').forEach(btn => btn.classList.remove('active'));
            
            // โชว์หน้าเว็บที่เลือกและเติมจุด active
            document.getElementById(pageId).classList.add('active');
            btnElement.classList.add('active');
            
            // เลื่อนขึ้นบนสุด
            window.scrollTo(0, 0);
        }

        // ทำให้ปุ่ม details (รายการนวด) มีเสียงคลิก
        document.querySelectorAll('details summary').forEach(item => {
            item.addEventListener('click', playClick);
        });

        // --- 3. Real-time Clock ---
        function updateClock() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('th-TH', { 
                hour: '2-digit', minute: '2-digit', second: '2-digit' 
            });
            document.getElementById('clock').innerText = timeString;
        }
        setInterval(updateClock, 1000);
        updateClock();

        // --- 4. Calendar Special Day Checker ---
        function checkSpecialDay() {
            playClick();
            const today = new Date();
            const date = today.getDate();
            const month = today.getMonth() + 1; // 1-12

            let message = "วันนี้เป็นวันธรรมดาที่เหมาะกับการนวดผ่อนคลายที่สุดเลยครับ 🤍";
            
            // จำลองปฏิทินวันสำคัญ (คุณสามารถแก้เลขวันที่และเดือนได้)
            if (date === 13 && month === 4) message = "💦 วันนี้วันสงกรานต์! แวะมาหลบร้อนนวดเย็นๆ ได้นะครับ";
            else if (date === 31 && month === 10) message = "🎃 วันฮาโลวีน! มานวดคลายความหลอนกันครับ";
            else if (date === 15 && month === 11) message = "🌕 วันลอยกระทง! นวดเสร็จไปเดินเล่นดูไฟได้เลย";
            else if (date === 14 && month === 2) message = "🌹 วันวาเลนไทน์! พาคนรักมานวดคู่กันได้นะครับ";
            
            // สุ่มวันพระจำลอง (เพื่อเป็นตัวอย่าง)
            const random = Math.random();
            if(random > 0.8 && message.includes("วันธรรมดา")) {
                message = "🪷 วันนี้ตรงกับวันพระครับ จิตใจสงบแล้ว ร่างกายก็ต้องผ่อนคลายด้วยนะครับ";
            }

            alert(message);
        }

        // --- 5. Floating Emojis Decoration ---
        const emojis = ['🪼', '🌻', '⭐️', '🌥️', '🫧'];
        function createEmoji() {
            const container = document.getElementById('emojis');
            const emojiEl = document.createElement('div');
            emojiEl.innerText = emojis[Math.floor(Math.random() * emojis.length)];
            emojiEl.className = 'floating-emoji';
            
            // สุ่มตำแหน่งซ้ายขวา และระยะเวลาลอย
            emojiEl.style.left = Math.random() * 100 + 'vw';
            emojiEl.style.animationDuration = (Math.random() * 5 + 5) + 's'; // 5-10 วินาที
            
            container.appendChild(emojiEl);
            
            // ลบอิโมจิเมื่อลอยพ้นจอเพื่อไม่ให้รกเครื่อง
            setTimeout(() => {
                emojiEl.remove();
            }, 10000);
        }
        setInterval(createEmoji, 1500); // สร้างใหม่ทุกๆ 1.5 วิ
    </script>
</body>
</html>
