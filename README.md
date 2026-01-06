<!DOCTYPE html>
<html lang="he" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>ממלכת האהבה - ההשקה</title>
    <link
        href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&family=Amatic+SC:wght@700&family=Assistant:wght@200;400;700&display=swap"
        rel="stylesheet">
    <style>
        :root {
            --primary: #ff4d6d;
            --rose-gold: #ffb3c1;
            --glass: rgba(255, 255, 255, 0.12);
            --glass-border: rgba(255, 255, 255, 0.25);
            --shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
        }

        /* הגדרות בסיס למניעת עיוותים */
        html,
        body {
            margin: 0;
            padding: 0;
            width: 100vw;
            height: 100vh;
            height: calc(var(--vh, 1vh) * 100);
            /* תיקון לגובה בניידים */
            background: #050505;
            overflow: hidden;
            font-family: 'Assistant', sans-serif;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* רקע דינמי */
        .main-wrapper {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1;
        }

        .bg-gradient {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: radial-gradient(circle at center, #2e0814 0%, #050505 100%);
        }

        .bg-glow {
            position: absolute;
            width: 100vmax;
            height: 100vmax;
            background: radial-gradient(circle, rgba(255, 77, 109, 0.1) 0%, transparent 70%);
            border-radius: 50%;
            filter: blur(80px);
            animation: moveGlow 25s infinite alternate ease-in-out;
        }

        @keyframes moveGlow {
            0% {
                transform: translate(-20%, -20%);
            }

            100% {
                transform: translate(20%, 20%);
            }
        }

        #particles-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        /* ניווט סימניות - עבר לצד למראה מודרני יותר ב-Desktop ונגיש ב-Mobile */
        .bookmarks {
            position: fixed;
            bottom: 40px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 15px;
            z-index: 100;
            background: rgba(255, 255, 255, 0.08);
            padding: 12px 25px;
            border-radius: 50px;
            backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
        }

        .bookmark {
            width: 12px;
            height: 12px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            transition: 0.5s all cubic-bezier(0.2, 0.8, 0.2, 1.2);
            cursor: pointer;
        }

        .bookmark.active {
            width: 45px;
            background: var(--primary);
            box-shadow: 0 0 15px var(--primary);
        }

        /* קונטיינר שלבים - עכשיו הוא רספונסיבי באמת */
        .stage-viewport {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            perspective: 2000px;
            padding: 20px;
            z-index: 10;
        }

        .stage {
            position: absolute;
            width: 90%;
            max-width: 500px;
            /* מוגדר ל-500 כדי שלא יהיה צר מדי ב-PC */
            background: var(--glass);
            backdrop-filter: blur(40px);
            -webkit-backdrop-filter: blur(40px);
            border-radius: 40px;
            border: 1px solid var(--glass-border);
            padding: 50px 30px;
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transform: scale(0.9) translateY(40px) rotateX(-10deg);
            transition: 0.8s cubic-bezier(0.2, 0.8, 0.2, 1);
            box-shadow: var(--shadow);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .stage.active {
            opacity: 1;
            visibility: visible;
            transform: scale(1) translateY(0) rotateX(0);
        }

        /* כשיש מסך רחב (PC) ניתן לכרטיסייה מרחב גדול יותר */
        @media (min-width: 768px) {
            .stage {
                max-width: 650px;
                padding: 60px 50px;
            }

            h1 {
                font-size: 4.5rem !important;
            }

            p {
                font-size: 1.4rem !important;
            }

            .heart-orb {
                width: 180px !important;
                height: 180px !important;
            }

            .heart-icon {
                font-size: 85px !important;
            }
        }

        h1 {
            font-family: 'Amatic SC', cursive;
            font-size: 3.8rem;
            margin: 10px 0;
            background: linear-gradient(to bottom, #fff, var(--rose-gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            line-height: 1;
        }

        .subtitle {
            font-size: 0.9rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--rose-gold);
            font-weight: 400;
            margin-bottom: 20px;
            opacity: 0.8;
        }

        p {
            font-size: 1.2rem;
            line-height: 1.6;
            font-weight: 300;
            color: rgba(255, 255, 255, 0.9);
            margin: 15px 0;
        }

        .heart-orb {
            position: relative;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle at 30% 30%, rgba(255, 77, 109, 0.8), transparent);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 50px rgba(255, 77, 109, 0.3);
            animation: pulseOrb 4s infinite ease-in-out;
            margin: 25px 0;
        }

        @keyframes pulseOrb {

            0%,
            100% {
                transform: scale(1);
                box-shadow: 0 0 30px rgba(255, 77, 109, 0.2);
            }

            50% {
                transform: scale(1.08);
                box-shadow: 0 0 70px rgba(255, 77, 109, 0.5);
            }
        }

        .heart-icon {
            font-size: 75px;
            filter: drop-shadow(0 0 15px white);
        }

        .feature-box {
            width: 100%;
            background: rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 18px;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 20px;
            text-align: right;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: 0.3s transform;
        }

        .feature-box:hover {
            transform: translateX(-10px);
            background: rgba(255, 255, 255, 0.12);
        }

        .feature-icon {
            font-size: 1.8rem;
            min-width: 45px;
            text-align: center;
        }

        .luxury-gift {
            font-size: 100px;
            cursor: pointer;
            position: relative;
            margin-top: 20px;
            transition: 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        .luxury-gift:hover {
            transform: scale(1.1) rotate(10deg);
        }

        .the-kiss {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            z-index: 1000;
            display: none;
            align-items: center;
            justify-content: center;
            pointer-events: none;
        }

        .kiss-big {
            font-size: 250px;
            animation: kissImpact 1.5s forwards;
        }

        @keyframes kissImpact {
            0% {
                transform: scale(0);
                opacity: 0;
            }

            40% {
                transform: scale(1.2);
                opacity: 1;
            }

            100% {
                transform: scale(10);
                opacity: 0;
            }
        }

        .timer-track {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: rgba(255, 255, 255, 0.05);
            overflow: hidden;
            border-radius: 40px 40px 0 0;
        }

        .timer-fill {
            height: 100%;
            width: 0%;
            background: var(--primary);
            box-shadow: 0 0 15px var(--primary);
        }
    </style>
</head>

<body>

    <div class="main-wrapper">
        <div class="bg-gradient">
            <div class="bg-glow"></div>
        </div>
        <div id="particles-container"></div>

        <div class="stage-viewport">
            <!-- שלב 1 -->
            <div class="stage" id="s-1">
                <div class="timer-track">
                    <div class="timer-fill" id="f-1"></div>
                </div>
                <div class="subtitle">Our Love Story</div>
                <h1>דוד & אביה</h1>
                <div class="heart-orb">
                    <div class="heart-icon">❤️</div>
                </div>
                <p>שני עולמות שנפגשו והפכו לאחד מופלא.</p>
            </div>

            <!-- שלב 2 -->
            <div class="stage" id="s-2">
                <div class="timer-track">
                    <div class="timer-fill" id="f-2"></div>
                </div>
                <div class="subtitle">Coming Soon</div>
                <h1>ממלכת האהבה</h1>
                <p>אפליקציה שנועדה רק בשבילנו.<br>השקה בקרוב מאוד... 🥹</p>
                <div
                    style="margin-top: 30px; width: 100%; height: 2px; background: rgba(255,255,255,0.1); position: relative; overflow: hidden;">
                    <div
                        style="position: absolute; left: 0; top: 0; height: 100%; width: 50%; background: var(--primary); box-shadow: 0 0 15px var(--primary); animation: slideProgress 2s infinite linear;">
                    </div>
                </div>
                <style>
                    @keyframes slideProgress {
                        from {
                            left: -50%;
                        }

                        to {
                            left: 100%;
                        }
                    }
                </style>
            </div>

            <!-- שלב 3 -->
            <div class="stage" id="s-3">
                <div class="timer-track">
                    <div class="timer-fill" id="f-3"></div>
                </div>
                <div class="subtitle">Inside the App</div>
                <h1 style="font-size: 3.2rem; margin-bottom: 25px;">מה מחכה לנו?</h1>

                <div class="feature-box">
                    <div class="feature-icon">💬</div>
                    <div>
                        <b style="font-size: 1.1rem; display: block;">רגעים בשידור חי</b>
                        <span style="opacity: 0.6; font-size: 0.9rem;">צ'אט פרטי ואישי רק לנו.</span>
                    </div>
                </div>

                <div class="feature-box">
                    <div class="feature-icon">⏳</div>
                    <div>
                        <b style="font-size: 1.1rem; display: block;">ציר זמן נצחי</b>
                        <span style="opacity: 0.6; font-size: 0.9rem;">כל הזיכרונות במקום אחד.</span>
                    </div>
                </div>

                <div class="feature-box">
                    <div class="feature-icon">🎁</div>
                    <div>
                        <b style="font-size: 1.1rem; display: block;">הפתעות יומיות</b>
                        <span style="opacity: 0.6; font-size: 0.9rem;">מסרים ופינוקים בכל יום.</span>
                    </div>
                </div>
            </div>

            <!-- שלב 4 -->
            <div class="stage" id="s-4">
                <div class="timer-track">
                    <div class="timer-fill" id="f-4"></div>
                </div>
                <div class="subtitle">For You</div>
                <h1>משהו קטן...</h1>
                <p>לחצי כדי לגלות מה מחכה לך</p>
                <div class="luxury-gift" onclick="blastKiss()">🎁</div>
            </div>
        </div>

        <div class="bookmarks">
            <div class="bookmark" id="b-1" onclick="jumpTo(1)"></div>
            <div class="bookmark" id="b-2" onclick="jumpTo(2)"></div>
            <div class="bookmark" id="b-3" onclick="jumpTo(3)"></div>
            <div class="bookmark" id="b-4" onclick="jumpTo(4)"></div>
        </div>
    </div>

    <div class="the-kiss" id="kissBox">
        <div class="kiss-big">💋</div>
    </div>

    <script>
        let current = 1;
        const total = 4;
        const duration = 7000;
        let timerInt, mainInt;

        function updateVH() {
            let vh = window.innerHeight * 0.01;
            document.documentElement.style.setProperty('--vh', `${vh}px`);
        }

        window.addEventListener('resize', updateVH);
        updateVH();

        function init() {
            render(1);
            startAuto();
            createParticles();

            // מניעת גלילה בטלפון
            document.body.addEventListener('touchmove', function (e) {
                if (!e.target.closest('.stage')) e.preventDefault();
            }, { passive: false });
        }

        function render(n) {
            document.querySelectorAll('.stage').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.bookmark').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.timer-fill').forEach(f => f.style.width = '0%');

            const s = document.getElementById(`s-${n}`);
            const b = document.getElementById(`b-${n}`);
            if (s) s.classList.add('active');
            if (b) b.classList.add('active');

            current = n;
            animateTimer(n);
        }

        function animateTimer(n) {
            const fill = document.getElementById(`f-${n}`);
            let start = Date.now();
            if (timerInt) clearInterval(timerInt);

            timerInt = setInterval(() => {
                let p = ((Date.now() - start) / duration) * 100;
                if (p <= 100) { if (fill) fill.style.width = p + '%'; }
                else { clearInterval(timerInt); }
            }, 60);
        }

        function startAuto() {
            if (mainInt) clearInterval(mainInt);
            mainInt = setInterval(() => {
                let next = current + 1;
                if (next > total) next = 1;
                render(next);
            }, duration);
        }

        function jumpTo(n) {
            render(n);
            startAuto();
        }

        function blastKiss() {
            const box = document.getElementById('kissBox');
            box.style.display = 'flex';
            if (navigator.vibrate) navigator.vibrate([100, 50, 100]);
            for (let i = 0; i < 40; i++) { setTimeout(createExplodingHeart, i * 25); }
            setTimeout(() => { box.style.display = 'none'; }, 1500);
        }

        function createExplodingHeart() {
            const h = document.createElement('div');
            h.innerHTML = Math.random() > 0.5 ? '❤️' : '💋';
            h.style.position = 'fixed';
            h.style.left = '50%'; h.style.top = '50%';
            h.style.fontSize = Math.random() * 40 + 20 + 'px';
            h.style.zIndex = '1100';
            h.style.pointerEvents = 'none';
            const deg = Math.random() * 360;
            const dist = Math.random() * 400 + 100;
            const x = Math.cos(deg * Math.PI / 180) * dist;
            const y = Math.sin(deg * Math.PI / 180) * dist;
            document.body.appendChild(h);
            h.animate([
                { transform: 'translate(-50%, -50%) scale(0) rotate(0deg)', opacity: 1 },
                { transform: `translate(calc(-50% + ${x}px), calc(-50% + ${y}px)) scale(1.5) rotate(${Math.random() * 360}deg)`, opacity: 0 }
            ], { duration: 1200, easing: 'ease-out' }).onfinish = () => h.remove();
        }

        function createParticles() {
            const container = document.getElementById('particles-container');
            setInterval(() => {
                const p = document.createElement('div');
                p.style.position = 'absolute';
                p.style.bottom = '-30px';
                p.style.left = Math.random() * 100 + 'vw';
                p.style.fontSize = Math.random() * 18 + 8 + 'px';
                p.style.opacity = Math.random() * 0.4;
                p.innerHTML = Math.random() > 0.8 ? '✨' : '💖';
                p.style.pointerEvents = 'none';
                container.appendChild(p);
                p.animate([
                    { transform: 'translateY(0) rotate(0deg)', opacity: p.style.opacity },
                    { transform: `translateY(-110vh) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                ], { duration: Math.random() * 4000 + 8000, easing: 'linear' }).onfinish = () => p.remove();
            }, 800);
        }

        init();
    </script>
</body>

</html>
