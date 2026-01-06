<!DOCTYPE html>
<html lang="he" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>ממלכת האהבה - גרסת ה-Ultimate</title>
    <link
        href="https://fonts.googleapis.com/css2?family=Assistant:wght@300;400;600;700;800&family=Amatic+SC:wght@700&display=swap"
        rel="stylesheet">
    <style>
        /* --- דף משחקים וסגנונות --- */
        :root {
            --primary: #d4af37;
            --secondary: #f8c8dc;
            --accent: #fff;
            --text-main: #2c3e50;
            --glass-bg: rgba(255, 255, 255, 0.85);
            --glass-border: rgba(255, 255, 255, 0.5);
            --glass-blur: blur(25px);
            --shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
            --header-h: 75px;
            --nav-h: 95px;
        }

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Assistant', sans-serif;
            background: #fdfbfb;
            color: var(--text-main);
            height: 100vh;
            height: 100dvh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            direction: rtl;
        }

        /* רקע אנימטיבי */
        .page-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: linear-gradient(-45deg, #f8c8dc, #e5b39b, #fff5f7, #ffe4e9);
            background-size: 400% 400%;
            animation: moveGradient 15s ease infinite;
        }

        @keyframes moveGradient {
            0% {
                background-position: 0% 50%;
            }

            50% {
                background-position: 100% 50%;
            }

            100% {
                background-position: 0% 50%;
            }
        }

        #particles-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        .heart {
            position: absolute;
            bottom: -20px;
            font-size: 20px;
            animation: floatUp linear infinite;
            opacity: 0.6;
        }

        @keyframes floatUp {
            to {
                transform: translateY(-120vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* כותרת */
        header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: var(--header-h);
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--glass-bg);
            backdrop-filter: var(--glass-blur);
            -webkit-backdrop-filter: var(--glass-blur);
            border-bottom: 2px solid var(--glass-border);
            z-index: 100;
            box-shadow: var(--shadow);
            display: none;
            /* מוסתר עד לסיום ההגדרה */
        }

        .title-text {
            font-family: 'Amatic SC', cursive;
            font-size: 2.8rem;
            color: var(--primary);
            cursor: pointer;
            transition: 0.3s;
        }

        .title-text:active {
            transform: scale(0.95);
        }

        /* תוכן האפליקציה */
        #app-viewport {
            flex: 1;
            position: relative;
            overflow: hidden;
            margin-top: var(--header-h);
            display: none;
        }

        .screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            padding: 30px 20px 120px 20px;
            overflow-y: auto;
            overflow-x: hidden;
            opacity: 0;
            transform: translateY(30px);
            pointer-events: none;
            transition: 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
        }

        .screen.active {
            opacity: 1;
            transform: translateY(0);
            pointer-events: all;
            z-index: 10;
        }

        .card {
            background: rgba(255, 255, 255, 0.88);
            border-radius: 30px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.06);
            border: 1px solid var(--glass-border);
            backdrop-filter: blur(10px);
        }

        /* תפריט תחתון */
        nav {
            position: fixed;
            bottom: 25px;
            left: 50%;
            transform: translateX(-50%);
            width: 92%;
            max-width: 460px;
            height: 75px;
            background: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border-radius: 40px;
            display: flex;
            justify-content: space-around;
            align-items: center;
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.12);
            z-index: 100;
            display: none;
        }

        .nav-link {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #bbb;
            font-size: 0.7rem;
            width: 20%;
            cursor: pointer;
            transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .nav-link i {
            font-size: 1.6rem;
            margin-bottom: 4px;
        }

        .nav-link.active {
            color: var(--primary);
            transform: translateY(-8px);
        }

        .nav-link.active i {
            transform: scale(1.2);
        }

        /* מונה זמן */
        .timer-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            margin-top: 25px;
        }

        .timer-unit {
            text-align: center;
        }

        .timer-unit span {
            display: block;
            font-size: 2rem;
            font-weight: 800;
            color: var(--primary);
            text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.05);
        }

        .timer-unit label {
            font-size: 0.75rem;
            color: #999;
            text-transform: uppercase;
            font-weight: 600;
        }

        /* ציר זמן וקופונים */
        .tl-item {
            border-right: 4px solid var(--secondary);
            padding-right: 25px;
            margin-bottom: 30px;
            position: relative;
        }

        .tl-item::after {
            content: '❤';
            position: absolute;
            right: -12px;
            top: -5px;
            color: var(--primary);
            font-size: 18px;
            background: #fff;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .tl-title {
            font-weight: 800;
            color: var(--primary);
            font-size: 1.2rem;
        }

        .promo-card {
            background: #fff;
            border: 2px dashed var(--secondary);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 20px;
            transition: 0.3s;
        }

        .promo-card.used {
            opacity: 0.45;
            filter: grayscale(1);
            transform: scale(0.97);
        }

        .action-btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            font-weight: bold;
            margin-top: 15px;
            cursor: pointer;
            width: 100%;
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
        }

        /* מסך הגדרה ראשונית */
        .onboarding {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #fff;
            z-index: 1000;
            padding: 50px 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            text-align: center;
            overflow-y: auto;
        }

        .onboarding.fade-out {
            opacity: 0;
            pointer-events: none;
            transition: 0.6s;
        }

        .field {
            width: 100%;
            max-width: 420px;
            margin-bottom: 25px;
            text-align: right;
        }

        .field label {
            display: block;
            font-weight: 700;
            margin-bottom: 10px;
            color: #555;
        }

        .text-input {
            width: 100%;
            padding: 18px;
            border: 2px solid #f2f2f2;
            border-radius: 18px;
            font-size: 1.1rem;
            background: #fdfdfd;
            transition: 0.3s;
        }

        .text-input:focus {
            border-color: var(--primary);
            background: #fff;
        }

        .dot-box {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 10px;
        }

        .dot {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            border: 4px solid transparent;
            transition: 0.3s;
        }

        .dot.active {
            border-color: #333;
            transform: scale(1.15);
        }

        /* פאנל ניהול */
        #admin-view {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #fff;
            z-index: 500;
            padding: 40px 25px;
            display: none;
            flex-direction: column;
            overflow-y: auto;
            text-align: right;
        }

        .adm-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 35px;
            border-bottom: 2px solid #f8f8f8;
            padding-bottom: 15px;
        }

        .row-item {
            background: #f9f9f9;
            padding: 18px;
            border-radius: 18px;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #eee;
        }

        .btn-red {
            background: #ff3b30;
            color: white;
            border: none;
            border-radius: 12px;
            padding: 8px 15px;
            cursor: pointer;
            font-weight: 600;
        }

        /* טוסט והודעות */
        .toasty {
            position: fixed;
            bottom: 120px;
            left: 50%;
            transform: translateX(-50%);
            background: #333;
            color: white;
            padding: 15px 35px;
            border-radius: 100px;
            z-index: 2000;
            display: none;
            font-size: 0.95rem;
            font-weight: 600;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>

<body>

    <div class="page-bg"></div>
    <div id="particles-container"></div>

    <!-- מסך התחלה של אשפתון הגדרות -->
    <div id="setupWizard" class="onboarding">
        <h1 style="font-family:'Amatic SC'; font-size:4rem; color:#d4af37; margin-bottom:10px;">ממלכת האהבה ❤️</h1>
        <p style="margin-bottom:40px; opacity:0.7;">בואו נבנה לכם את האפליקציה המושלמת בכמה שניות.</p>

        <div class="field">
            <label>מה השמות שלכם?</label>
            <input type="text" id="inNames" class="text-input" placeholder="למשל: אביה ודוד / אבשלום ותמר">
        </div>

        <div class="field">
            <label>איזה יום הוא היום שלכם? (תאריך התחלה)</label>
            <input type="date" id="inDate" class="text-input">
        </div>

        <div class="field">
            <label>בחרו צבע שאתם אוהבים:</label>
            <div class="dot-box">
                <div class="dot" style="background:#d4af37" onclick="selectTheme('#d4af37', this)"></div>
                <div class="dot" style="background:#e73c7e" onclick="selectTheme('#e73c7e', this)"></div>
                <div class="dot" style="background:#ff3b30" onclick="selectTheme('#ff3b30', this)"></div>
                <div class="dot" style="background:#007aff" onclick="selectTheme('#007aff', this)"></div>
            </div>
        </div>

        <button class="action-btn" style="height:70px; font-size:1.4rem;" onclick="finishWizard()">צור לי את הממלכה!
            🏰✨</button>
    </div>

    <!-- כותרת ראשית (מופיעה אחרי הגדרה) -->
    <header id="appHeader">
        <div class="title-text" id="secretTrigger">Love App</div>
    </header>

    <!-- תוכן האפליקציה -->
    <div id="app-viewport">

        <!-- דף הבית -->
        <section id="sc-home" class="screen active">
            <div class="card" style="text-align:center;">
                <h1 id="outNames" style="font-family:'Amatic SC'; font-size:3.5rem; margin-bottom:10px;">אביה & דוד</h1>
                <p id="outWelcome" style="line-height:1.7; opacity:0.8; font-size:1.1rem;">ברוכים הבאים למקום הסודי שלכם
                    ❤️</p>
            </div>

            <div class="card" style="text-align:center;">
                <label style="text-transform:uppercase; font-size:0.75rem; letter-spacing:2px; opacity:0.6;">זמן של אושר
                    ביחד:</label>
                <div class="timer-grid">
                    <div class="timer-unit"><span id="dd">0</span><label>ימים</label></div>
                    <div class="timer-unit"><span id="hh">0</span><label>שעות</label></div>
                    <div class="timer-unit"><span id="mm">0</span><label>דקות</label></div>
                    <div class="timer-unit"><span id="ss">0</span><label>שניות</label></div>
                </div>
            </div>
        </section>

        <!-- דף ציר זמן -->
        <section id="sc-timeline" class="screen">
            <h2 style="margin-bottom:30px; font-weight:800;">הזיכרונות היפים שלנו 📸</h2>
            <div id="timelineCont"></div>
        </section>

        <!-- דף קופונים -->
        <section id="sc-coupons" class="screen">
            <h2 style="margin-bottom:30px; font-weight:800;">ארנק קופונים מפנקים 🎫</h2>
            <div id="couponsCont"></div>
        </section>

        <!-- דף סיבות -->
        <section id="sc-reasons" class="screen">
            <h2 style="margin-bottom:30px; font-weight:800;">למה את/ה הכי מיוחד בעולם ✨</h2>
            <div class="card"
                style="min-height:220px; display:flex; align-items:center; justify-content:center; text-align:center;">
                <h3 id="reasonText" style="font-weight:400; font-size:1.5rem; line-height:1.6;">לחצו על הכפתור למטה...
                </h3>
            </div>
            <button class="action-btn" style="height:65px;" onclick="getNewReason()">תפתיע אותי 🎲</button>
        </section>

        <!-- דף מתנה -->
        <section id="sc-surprise" class="screen" style="text-align:center;">
            <h2 style="margin-bottom:40px; font-weight:800;">הפתעה מתוקה להיום 🎁</h2>
            <div id="gift" style="font-size:110px; cursor:pointer; filter:drop-shadow(0 15px 25px rgba(0,0,0,0.1));"
                onclick="unwrapped()">🎁</div>
            <div id="giftMsg" class="card" style="display:none; margin-top:40px; animation: popUp 0.5s ease-out;"></div>
        </section>

    </div>

    <!-- תפריט ניווט -->
    <nav id="appNav">
        <div class="nav-link active" onclick="gotoTab('home', this)"><i>🏠</i>בית</div>
        <div class="nav-link" onclick="gotoTab('timeline', this)"><i>⏳</i>זמן</div>
        <div class="nav-link" onclick="gotoTab('coupons', this)"><i>🎫</i>קופון</div>
        <div class="nav-link" onclick="gotoTab('reasons', this)"><i>✨</i>למה?</div>
        <div class="nav-link" onclick="gotoTab('surprise', this)"><i>🎁</i>מתנה</div>
    </nav>

    <!-- פאנל ניהול סודי -->
    <div id="admin-view">
        <div class="adm-header">
            <h2 style="margin:0; color:var(--primary);">שליטה בממלכה 🛠️</h2>
            <button class="btn-red" style="background:#333;" onclick="closeAdmin()">סגור</button>
        </div>

        <div class="card">
            <label style="font-weight:bold; display:block; margin-bottom:8px;">ערוך שמות:</label>
            <input type="text" id="admNames" class="text-input" style="margin-bottom:15px;">
            <label style="font-weight:bold; display:block; margin-bottom:8px;">ערוך ברכה:</label>
            <textarea id="admWelcome" class="text-input" rows="3"></textarea>
            <button class="action-btn" style="padding:10px; font-size:0.95rem;" onclick="saveAdmGeneral()">עדכן
                נתונים</button>
        </div>

        <h3>ניהול ציר זמן</h3>
        <div id="admTimeline"></div>
        <div class="card">
            <input type="text" id="newTlDate" class="text-input" placeholder="תאריך / כותרת">
            <input type="text" id="newTlDesc" class="text-input" placeholder="תיאור הזיכרון" style="margin-top:10px;">
            <button class="action-btn" style="padding:10px;" onclick="doAddTl()">הוסף זיכרון +</button>
        </div>

        <h3>ניהול קופונים</h3>
        <div id="admCoupons"></div>
        <div class="card">
            <input type="text" id="newCoupon" class="text-input" placeholder="שם הקופון (למשל: קינוח מושחת)">
            <button class="action-btn" style="padding:10px;" onclick="doAddCoupon()">הוסף קופון +</button>
        </div>

        <button class="btn-red" style="width:100%; padding:25px; margin-top:60px; font-size:1.1rem; font-weight:800;"
            onclick="resetEverything()">⚠️ איפוס מוחלט והתחלה מחדש</button>
    </div>

    <div id="toast" class="toasty"></div>

    <script>
        // --- מסד נתונים פנימי ---
        let db = {
            names: "",
            startDate: "",
            primary: "#d4af37",
            welcome: "את היקרה לי מכל, הלב הפועם בתוכי. המקום הזה שייך רק לנו ❤️",
            timeline: [
                { title: "היום שבו הכל התחיל", desc: "הרגע שבו המבטים שלנו נפגשו לראשונה..." }
            ],
            coupons: [
                { name: "קינוח בבית קפה לבחירתך", used: false },
                { name: "פטור משטיפת כלים (חד פעמי!)", used: false },
                { name: "עיסוי מפנק ל-20 דקות", used: false }
            ],
            reasons: [
                "כי החיוך שלך מאיר את היום שלי", "כי את/ה הכי טוב/ה בעולם", "על הדרך שבה את/ה מבין/ה אותי", "כי הלב שלך פשוט ענק"
            ]
        };

        let activeColor = "#d4af37";
        let devClicks = 0;

        // --- טעינה ראשונית ---
        window.onload = () => {
            const saved = localStorage.getItem('ultimate_love_v2');
            if (saved) {
                db = JSON.parse(saved);
                document.getElementById('setupWizard').style.display = 'none';
                launchApp();
            }
            spawnHearts();
        };

        // --- אשף הגדרות ---
        function selectTheme(c, el) {
            activeColor = c;
            document.querySelectorAll('.dot').forEach(d => d.classList.remove('active'));
            el.classList.add('active');
        }

        function finishWizard() {
            const names = document.getElementById('inNames').value.trim();
            const date = document.getElementById('inDate').value;

            if (!names || !date) {
                alert("בבקשה תמלאו שמות ותאריך יפה!");
                return;
            }

            db.names = names;
            db.startDate = date;
            db.primary = activeColor;

            saveCache();
            document.getElementById('setupWizard').classList.add('fade-out');
            setTimeout(() => {
                document.getElementById('setupWizard').style.display = 'none';
                launchApp();
            }, 600);
        }

        // --- לוגיקת אפליקציה ---
        function launchApp() {
            document.documentElement.style.setProperty('--primary', db.primary);

            // תצוגה
            document.getElementById('appHeader').style.display = 'flex';
            document.getElementById('app-viewport').style.display = 'block';
            document.getElementById('appNav').style.display = 'flex';

            document.getElementById('outNames').innerText = db.names;
            document.getElementById('outWelcome').innerText = db.welcome;

            // מונה
            setInterval(runClock, 1000);
            runClock();

            refreshUI();

            // טריגר סודי למנהל
            document.getElementById('secretTrigger').onclick = () => {
                devClicks++;
                if (devClicks >= 7) {
                    openAdmin();
                    devClicks = 0;
                }
                setTimeout(() => devClicks = 0, 2500);
            };
        }

        function runClock() {
            if (!db.startDate) return;
            const diff = new Date() - new Date(db.startDate);
            if (diff < 0) return;

            document.getElementById('dd').innerText = Math.floor(diff / 86400000);
            document.getElementById('hh').innerText = Math.floor((diff / 3600000) % 24);
            document.getElementById('mm').innerText = Math.floor((diff / 60000) % 60);
            document.getElementById('ss').innerText = Math.floor((diff / 1000) % 60);
        }

        function refreshUI() {
            // ציר זמן
            const tl = document.getElementById('timelineCont');
            tl.innerHTML = db.timeline.map(t => `
                <div class="tl-item">
                    <div class="tl-title">${t.title}</div>
                    <div style="background:#fff; padding:12px; border-radius:12px; margin-top:6px; box-shadow:0 3px 10px rgba(0,0,0,0.03);">${t.desc}</div>
                </div>
            `).join('');

            // קופונים
            const cp = document.getElementById('couponsCont');
            cp.innerHTML = db.coupons.map((c, i) => `
                <div class="promo-card ${c.used ? 'used' : ''}">
                    <h3 style="margin:0; color:var(--primary);">${c.name}</h3>
                    <button class="action-btn" style="margin-top:10px; padding:8px;" onclick="useIt(${i})">${c.used ? 'נוצל ✅' : 'מימוש מיד'}</button>
                </div>
            `).join('');
        }

        function useIt(i) {
            db.coupons[i].used = true;
            saveCache();
            refreshUI();
            notify("הקופון נוצל בהצלחה! תהנו ❤️");
        }

        function getNewReason() {
            const r = db.reasons[Math.floor(Math.random() * db.reasons.length)];
            document.getElementById('reasonText').innerText = r;
            notify("סיבה חדשה צפה!");
        }

        function unwrapped() {
            const surp = ["נשיקה גדולה מאחורי האוזן!", "הזמנה לסרט שתבחר/י בסופ\"ש", "מחמאה: הריח שלך הוא האהוב עליי", "ערב בלי טלפונים - רק אנחנו"];
            const txt = surp[Math.floor(Math.random() * surp.length)];
            const el = document.getElementById('giftMsg');
            el.innerText = txt;
            el.style.display = 'block';
            document.getElementById('gift').style.transform = 'scale(1.1)';
            notify("היום זכית בשי!");
        }

        // --- ניווט ---
        function gotoTab(id, el) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById('sc-' + id).classList.add('active');
            document.querySelectorAll('.nav-link').forEach(n => n.classList.remove('active'));
            el.classList.add('active');
        }

        // --- מנהל ---
        function openAdmin() {
            document.getElementById('admin-view').style.display = 'flex';
            document.getElementById('admNames').value = db.names;
            document.getElementById('admWelcome').value = db.welcome;
            renderAdminTools();
        }

        function closeAdmin() {
            document.getElementById('admin-view').style.display = 'none';
            launchApp(); // רענון מהיר
        }

        function saveAdmGeneral() {
            db.names = document.getElementById('admNames').value;
            db.welcome = document.getElementById('admWelcome').value;
            saveCache();
            notify("נשמר בהצלחה!");
        }

        function renderAdminTools() {
            // זיכרונות
            document.getElementById('admTimeline').innerHTML = db.timeline.map((t, i) => `
                <div class="row-item">
                    <span>${t.title}</span>
                    <button class="btn-red" onclick="kill('timeline', ${i})">מחק</button>
                </div>
            `).join('');

            // קופונים
            document.getElementById('admCoupons').innerHTML = db.coupons.map((c, i) => `
                <div class="row-item">
                    <span>${c.name}</span>
                    <button class="btn-red" onclick="kill('coupons', ${i})">מחק</button>
                </div>
            `).join('');
        }

        function doAddCoupon() {
            const v = document.getElementById('newCoupon').value;
            if (v) {
                db.coupons.push({ name: v, used: false });
                saveCache();
                renderAdminTools();
                document.getElementById('newCoupon').value = "";
            }
        }

        function doAddTl() {
            const t = document.getElementById('newTlDate').value;
            const d = document.getElementById('newTlDesc').value;
            if (t) {
                db.timeline.push({ title: t, desc: d });
                saveCache();
                renderAdminTools();
                document.getElementById('newTlDate').value = "";
                document.getElementById('newTlDesc').value = "";
            }
        }

        function kill(type, i) {
            db[type].splice(i, 1);
            saveCache();
            renderAdminTools();
        }

        function resetEverything() {
            if (confirm("שימו לב: זה ימחק הכל ויחזיר את האפליקציה למצב חדש. בטוחים?")) {
                localStorage.removeItem('ultimate_love_v2');
                location.reload();
            }
        }

        // --- עזרים ---
        function saveCache() { localStorage.setItem('ultimate_love_v2', JSON.stringify(db)); }

        function notify(m) {
            const t = document.getElementById('toast');
            t.innerText = m;
            t.style.display = 'block';
            setTimeout(() => t.style.display = 'none', 3000);
        }

        function spawnHearts() {
            const c = document.getElementById('particles-container');
            setInterval(() => {
                const h = document.createElement('div');
                h.classList.add('heart');
                h.innerHTML = Math.random() > 0.5 ? '❤️' : '✨';
                h.style.left = Math.random() * 100 + 'vw';
                h.style.animationDuration = (Math.random() * 5 + 6) + 's';
                c.appendChild(h);
                setTimeout(() => h.remove(), 11000);
            }, 800);
        }
    </script>
</body>

</html>