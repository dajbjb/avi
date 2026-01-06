<!DOCTYPE html>
<html lang="he" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>David & Avia - The Kingdom</title>

    <meta name="theme-color" content="#000000">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

    <!-- Fonts -->
    <link
        href="https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;700;900&family=Fredoka:wght@300;400;500;600;700&family=Amatic+SC:wght@700&display=swap"
        rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- MODERN LOVE SYSTEM --- */
        :root {
            --neon-blue: #00f2ea;
            --neon-pink: #ff0050;
            --bg-dark: #050505;
            --glass: rgba(20, 20, 25, 0.9);
            --border: 1px solid rgba(255, 255, 255, 0.08);
            --safe-bottom: env(safe-area-inset-bottom, 20px);
        }

        body {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            background-color: var(--bg-dark);
            color: #fff;
            font-family: 'Fredoka', sans-serif;
            overflow: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        /* --- GRADIENT TITLE & HEARTS --- */
        .main-title {
            font-family: 'Amatic SC', cursive;
            font-size: 3.5rem;
            margin: 0 0 20px 0;
            background: linear-gradient(to right, var(--neon-blue), var(--neon-pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 1px;
            text-align: center;
        }

        .heart-bg-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 0;
        }

        .floating-heart {
            position: absolute;
            bottom: -20px;
            color: rgba(255, 0, 80, 0.1);
            animation: floatUp linear forwards;
            font-size: 20px;
        }

        @keyframes floatUp {
            to {
                transform: translateY(-120vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* --- LAYOUT --- */
        #app-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 10;
            display: none;
            /* Toggled by JS */
        }

        .view-section {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            padding: 20px 20px 100px 20px;
            overflow-y: auto;
            display: none;
            -webkit-overflow-scrolling: touch;
        }

        .view-section.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* --- WIDGETS --- */
        .glass-card {
            background: var(--glass);
            border: var(--border);
            border-radius: 24px;
            padding: 24px;
            margin-bottom: 20px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
        }

        /* Clock Pro */
        .clock-container {
            text-align: center;
            margin: 20px 0 10px 0;
        }

        .clock-time {
            font-family: 'Rubik', sans-serif;
            font-weight: 700;
            font-size: 4.8rem;
            line-height: 1;
            letter-spacing: -3px;
            background: linear-gradient(180deg, #fff, #bbb);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            color: white;
            /* Fallback */
        }

        .clock-seconds {
            font-size: 2rem;
            opacity: 0.5;
            font-weight: 300;
        }

        .clock-date {
            font-size: 1.1rem;
            opacity: 0.6;
            margin-top: 5px;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        /* Days */
        .days-container {
            text-align: center;
            margin-bottom: 30px;
        }

        .days-val {
            font-family: 'Rubik', sans-serif;
            font-weight: 900;
            font-size: 2.5rem;
            color: var(--neon-pink);
        }

        .days-lbl {
            font-size: 0.8rem;
            opacity: 0.6;
            letter-spacing: 2px;
        }

        /* Countdown */
        .countdown-widget {
            display: none;
            background: linear-gradient(135deg, #111, #000);
            border: 1px solid var(--neon-blue);
        }

        .cd-grid {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
            text-align: center;
            font-family: 'Rubik';
        }

        .cd-num {
            font-size: 1.5rem;
            font-weight: 600;
        }

        .cd-lbl {
            font-size: 0.7rem;
            opacity: 0.5;
            text-transform: uppercase;
        }

        /* Photo */
        .photo-widget {
            height: 280px;
            width: 100%;
            position: relative;
            border-radius: 24px;
            overflow: hidden;
            border: var(--border);
            background: #000;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
        }

        .photo-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .photo-actions {
            position: absolute;
            bottom: 15px;
            right: 15px;
            display: flex;
            gap: 10px;
        }

        .action-btn {
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(5px);
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
            font-size: 1.2rem;
        }

        /* Nav */
        #bottom-nav {
            position: fixed;
            bottom: 25px;
            left: 0;
            width: 100%;
            display: none;
            justify-content: center;
            z-index: 5000;
            pointer-events: none;
        }

        .nav-pill {
            background: rgba(20, 20, 22, 0.95);
            border-radius: 35px;
            padding: 15px 30px;
            display: flex;
            gap: 40px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            pointer-events: auto;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
        }

        .nav-icon {
            font-size: 1.4rem;
            color: #555;
            transition: 0.3s;
        }

        .nav-icon.active {
            color: #fff;
            transform: translateY(-4px);
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
        }

        body.role-david .active {
            color: var(--neon-blue);
            text-shadow: 0 0 15px rgba(0, 242, 234, 0.4);
        }

        body.role-avia .active {
            color: var(--neon-pink);
            text-shadow: 0 0 15px rgba(255, 0, 80, 0.4);
        }

        /* Login Overlay */
        #login-overlay {
            position: fixed;
            inset: 0;
            background: #050505;
            z-index: 99999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .role-avatar {
            font-size: 4.5rem;
            margin: 0 15px;
            transition: 0.3s;
        }

        .role-avatar:active {
            transform: scale(0.9);
        }

        /* Mobile */
        @media (max-width: 480px) {
            .main-title {
                font-size: 3rem;
            }

            .clock-time {
                font-size: 3.8rem;
            }

            .nav-pill {
                padding: 12px 25px;
                gap: 25px;
            }

            #bottom-nav {
                bottom: calc(15px + var(--safe-bottom));
            }
        }

        /* Standard Components */
        .btn-primary {
            background: linear-gradient(135deg, var(--neon-pink), #ff4785);
            color: #fff;
            border: 0;
            padding: 15px;
            border-radius: 16px;
            width: 100%;
            font-weight: 600;
            font-family: 'Rubik';
            font-size: 1rem;
            margin-top: 10px;
        }

        input {
            width: 100%;
            padding: 15px;
            background: #222;
            border: 0;
            color: #fff;
            border-radius: 12px;
            margin-bottom: 10px;
        }
    </style>
</head>

<body>

    <!-- HEARTS EFFECT -->
    <div id="hearts-container" class="heart-bg-container"></div>

    <!-- LOGIN -->
    <div id="login-overlay">
        <div class="main-title">David & Avia</div>
        <div style="font-size: 0.9rem; opacity: 0.5; margin-top: -10px; margin-bottom: 40px; letter-spacing: 3px;">THE
            KINGDOM</div>

        <div style="display:flex;">
            <div class="role-avatar" onclick="preLogin('david')">👑</div>
            <div class="role-avatar" onclick="preLogin('avia')">💖</div>
        </div>
        <input type="number" id="pin" placeholder="ACCESS CODE"
            style="display:none; text-align:center; width:150px; margin-top:40px; letter-spacing:5px;">
    </div>

    <!-- APP -->
    <div id="app-container">

        <!-- HOME -->
        <section id="view-home" class="view-section active">
            <div class="clock-container">
                <div class="clock-time" id="clock">00:00<span class="clock-seconds">00</span></div>
                <div class="clock-date" id="date-str">Loading...</div>
            </div>

            <div class="days-container">
                <div class="days-val" id="days-count">0</div>
                <div class="days-lbl">DAYS TOGETHER</div>
            </div>

            <!-- Countdown (Hidden by default) -->
            <div id="countdown-widget" class="glass-card countdown-widget">
                <div style="display:flex; justify-content:space-between;">
                    <strong style="color:var(--neon-blue);">NEXT DATE</strong>
                    <span id="next-title" style="opacity:0.7;">Date Night</span>
                </div>
                <div class="cd-grid">
                    <div>
                        <div class="cd-num" id="cd-d">0</div>
                        <div class="cd-lbl">Days</div>
                    </div>
                    <div>
                        <div class="cd-num" id="cd-h">0</div>
                        <div class="cd-lbl">Hrs</div>
                    </div>
                    <div>
                        <div class="cd-num" id="cd-m">0</div>
                        <div class="cd-lbl">Min</div>
                    </div>
                    <div>
                        <div class="cd-num" id="cd-s">0</div>
                        <div class="cd-lbl">Sec</div>
                    </div>
                </div>
            </div>

            <div class="photo-widget">
                <img id="home-photo" class="photo-img" src="">
                <div class="photo-actions">
                    <div class="action-btn" onclick="document.getElementById('uploader').click()">
                        <i class="fa-solid fa-camera"></i>
                    </div>
                </div>
                <!-- Compress & Upload Input -->
                <input type="file" id="uploader" accept="image/*" style="display:none;" onchange="handleUpload(this)">
            </div>

            <div style="height: 100px;"></div>
        </section>

        <!-- DATES -->
        <section id="view-dates" class="view-section">
            <div class="main-title" style="font-size:2.5rem;">Our Plan</div>
            <div id="dates-list"></div>
            <button class="btn-primary" onclick="document.getElementById('modal-date').style.display='flex'">+ New
                Date</button>
        </section>

        <!-- MEMORIES -->
        <section id="view-memories" class="view-section">
            <div class="main-title" style="font-size:2.5rem;">Memories</div>
            <div id="memories-list" style="display:grid; gap:15px;"></div>
        </section>

        <!-- CHAT -->
        <section id="view-chat" class="view-section">
            <div class="main-title" style="font-size:2.5rem;">Secrets</div>
            <div id="chat-box" style="padding-bottom:80px;"></div>
            <div style="position:fixed; bottom:110px; left:20px; right:20px; display:flex; gap:10px;">
                <input type="text" id="chat-in" placeholder="Whisper..." style="margin:0; flex:1;">
                <button onclick="sendMsg()"
                    style="width:50px; background:var(--neon-blue); border:0; border-radius:12px; color:#000;"><i
                        class="fa-solid fa-paper-plane"></i></button>
            </div>
        </section>

        <!-- ADMIN -->
        <section id="view-admin" class="view-section">
            <div class="main-title" style="font-size:2.5rem;">Settings</div>
            <button class="btn-primary" onclick="downloadBackup()">Download Backup</button>
            <button class="btn-primary" style="background:#222; color:#f00;" onclick="logout()">Logout</button>
        </section>

    </div>

    <!-- NAV -->
    <nav id="bottom-nav">
        <div class="nav-pill">
            <i class="fa-solid fa-house nav-icon active" onclick="go('home')"></i>
            <i class="fa-solid fa-calendar nav-icon" onclick="go('dates')"></i>
            <i class="fa-solid fa-heart nav-icon" onclick="go('memories')"></i>
            <i class="fa-solid fa-comments nav-icon" onclick="go('chat')"></i>
            <i class="fa-solid fa-crown nav-icon" onclick="go('admin')"></i>
        </div>
    </nav>

    <!-- MODAL -->
    <div id="modal-date"
        style="position:fixed; inset:0; background:rgba(0,0,0,0.9); z-index:20000; display:none; align-items:center; justify-content:center;">
        <div class="glass-card" style="width:85%;">
            <h2>New Date</h2>
            <input type="text" id="nd-title" placeholder="Title">
            <input type="datetime-local" id="nd-time">
            <button class="btn-primary" onclick="addDate()">Save</button>
            <button class="btn-primary" style="background:transparent; border:1px solid #444;"
                onclick="document.getElementById('modal-date').style.display='none'">Cancel</button>
        </div>
    </div>

    <script>
        // --- LOGIC CORE ---
        const DB = {
            data: JSON.parse(localStorage.getItem('k_db_final')) || {
                msgs: [],
                photos: ["https://images.unsplash.com/photo-1518199266791-5375a83190b7"],
                dates: [],
                memories: []
            },
            save: () => localStorage.setItem('k_db_final', JSON.stringify(DB.data))
        };
        let myRole = '';

        // --- AUTH ---
        function preLogin(role) {
            const p = document.getElementById('pin');
            p.style.display = 'block'; p.focus();
            p.onkeyup = () => {
                if (p.value.length >= 3) {
                    if ((role == 'david' && p.value == '777') || (role == 'avia' && p.value == '111')) login(role);
                    else { alert('Wrong Code'); p.value = ''; }
                }
            };
        }
        function login(role) {
            myRole = role;
            localStorage.setItem('k_role', role);
            document.body.classList.add('role-' + role);
            document.getElementById('login-overlay').style.display = 'none';
            document.getElementById('app-container').style.display = 'block';
            document.getElementById('bottom-nav').style.display = 'flex';
            init();
        }
        function logout() { localStorage.removeItem('k_role'); location.reload(); }

        // --- INIT ---
        function init() {
            // Clock & Hearts
            updateClock(); setInterval(updateClock, 1000);
            createFloatingHearts(); setInterval(createFloatingHearts, 2000); // Heart generator

            // Data
            renderDays();
            renderPhoto(); setInterval(renderPhoto, 10000);
            renderDates();
            renderChat();
            renderMemories();
        }

        // --- CLOCK ---
        function updateClock() {
            const now = new Date();
            const h = String(now.getHours()).padStart(2, '0');
            const m = String(now.getMinutes()).padStart(2, '0');
            const s = String(now.getSeconds()).padStart(2, '0');
            document.getElementById('clock').innerHTML = `${h}:${m}<span class="clock-seconds">${s}</span>`;

            const opts = { weekday: 'short', month: 'long', day: 'numeric' };
            document.getElementById('date-str').innerText = now.toLocaleDateString('en-US', opts);

            updateCountdown();
        }

        // --- HEARTS ---
        function createFloatingHearts() {
            const heart = document.createElement('div');
            heart.classList.add('floating-heart');
            heart.innerText = Math.random() > 0.5 ? '❤️' : '✨';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 10 + 10) + 's';
            heart.style.fontSize = (Math.random() * 15 + 10) + 'px';
            document.getElementById('hearts-container').appendChild(heart);
            setTimeout(() => heart.remove(), 20000);
        }

        // --- DAYS ---
        function renderDays() {
            const start = new Date('2025-04-20');
            const diff = Math.floor((new Date() - start) / 86400000);
            document.getElementById('days-count').innerText = Math.max(0, diff);
        }

        // --- PHOTOS (COMPRESSION) ---
        function handleUpload(input) {
            if (input.files && input.files[0]) {
                const file = input.files[0];
                const reader = new FileReader();
                reader.onload = (e) => {
                    const img = new Image();
                    img.src = e.target.result;
                    img.onload = () => {
                        const canvas = document.createElement('canvas');
                        const ctx = canvas.getContext('2d');
                        // Resize to max 800px width
                        const scale = 800 / img.width;
                        canvas.width = 800;
                        canvas.height = img.height * scale;
                        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
                        // Compress to JPEG 0.7
                        const dataUrl = canvas.toDataURL('image/jpeg', 0.7);
                        DB.data.photos.push(dataUrl);
                        DB.save();
                        renderPhoto();
                        alert('Photo Added!');
                    }
                }
                reader.readAsDataURL(file);
            }
        }
        function renderPhoto() {
            const arr = DB.data.photos;
            if (arr.length) document.getElementById('home-photo').src = arr[Math.floor(Math.random() * arr.length)];
        }

        // --- DATES ---
        function addDate() {
            const t = document.getElementById('nd-title').value;
            const tm = document.getElementById('nd-time').value;
            if (t && tm) {
                DB.data.dates.push({ id: Date.now(), title: t, time: tm });
                DB.data.dates.sort((a, b) => new Date(a.time) - new Date(b.time));
                DB.save();
                document.getElementById('modal-date').style.display = 'none';
                renderDates();
            }
        }
        function renderDates() {
            const list = document.getElementById('dates-list');
            list.innerHTML = DB.data.dates.map(d => `
                <div class="glass-card" style="padding:15px; display:flex; justify-content:space-between;">
                    <div><b>${d.title}</b><br><small style="opacity:0.6">${new Date(d.time).toLocaleString()}</small></div>
                    <div onclick="delDate(${d.id})">🗑️</div>
                </div>
            `).join('');
            updateCountdown();
        }
        function delDate(id) {
            if (confirm('Delete?')) {
                DB.data.dates = DB.data.dates.filter(d => d.id !== id);
                DB.save();
                renderDates();
            }
        }
        function updateCountdown() {
            const now = new Date();
            const next = DB.data.dates.find(d => new Date(d.time) > now);
            const w = document.getElementById('countdown-widget');

            if (next) {
                w.style.display = 'block';
                document.getElementById('next-title').innerText = next.title;
                const diff = new Date(next.time) - now;
                document.getElementById('cd-d').innerText = Math.floor(diff / 86400000);
                document.getElementById('cd-h').innerText = Math.floor((diff % 86400000) / 3600000);
                document.getElementById('cd-m').innerText = Math.floor((diff % 3600000) / 60000);
                document.getElementById('cd-s').innerText = Math.floor((diff % 60000) / 1000);
            } else {
                w.style.display = 'none';
            }
        }

        // --- CHAT & NAV ---
        function sendMsg() {
            const tx = document.getElementById('chat-in').value;
            if (tx) {
                DB.data.msgs.push({ u: myRole, t: tx });
                DB.save();
                document.getElementById('chat-in').value = '';
                renderChat();
            }
        }
        function renderChat() {
            const b = document.getElementById('chat-box');
            b.innerHTML = DB.data.msgs.map(m => `
                <div style="text-align:${m.u === myRole ? 'right' : 'left'}; margin:10px 0;">
                    <span style="background:${m.u === myRole ? 'var(--neon-blue)' : '#222'}; color:${m.u === myRole ? '#000' : '#fff'}; padding:10px 15px; border-radius:15px; display:inline-block;">
                        ${m.t}
                    </span>
                </div>
            `).join('');
            b.scrollTop = b.scrollHeight;
        }

        function go(tab) {
            document.querySelectorAll('.view-section').forEach(e => e.style.display = 'none');
            document.getElementById('view-' + tab).style.display = 'block';
            document.querySelectorAll('.nav-icon').forEach(e => e.classList.remove('active'));
            const idx = ['home', 'dates', 'memories', 'chat', 'admin'].indexOf(tab);
            document.querySelectorAll('.nav-icon')[idx].classList.add('active');
        }

        // --- MEMORIES ---
        function renderMemories() {
            // Placeholder logic for memories tab
            const d = document.getElementById('memories-list');
            if (DB.data.memories.length === 0) d.innerHTML = '<div style="text-align:center; opacity:0.5; padding:50px;">No memories saved yet.</div>';
        }

        function downloadBackup() {
            const a = document.createElement('a');
            a.href = URL.createObjectURL(new Blob([JSON.stringify(DB.data)], { type: 'application/json' }));
            a.download = 'kingdom_backup.json';
            a.click();
        }

        // Auto Login
        const r = localStorage.getItem('k_role');
        if (r) login(r);

    </script>
</body>

</html>
