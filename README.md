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
            --shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
        }

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html,
        body {
            margin: 0;
            padding: 0;
            width: 100% !important;
            height: 100% !important;
            /* פתרון לבעיות גובה בבוסרים של ניידים (iOS/Android) */
            height: -webkit-fill-available;
            font-family: 'Assistant', sans-serif;
            background: #050505;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            position: fixed;
            left: 0;
            top: 0;
            touch-action: none;
        }

        .bg-gradient {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: radial-gradient(circle at center, #2e0814 0%, #050505 100%);
        }

        .bg-glow {
            position: absolute;
            width: 150vw;
            height: 150vw;
            background: radial-gradient(circle, rgba(255, 77, 109, 0.12) 0%, transparent 70%);
            border-radius: 50%;
            filter: blur(80px);
            animation: moveGlow 25s infinite alternate ease-in-out;
        }

        @keyframes moveGlow {
            0% {
                transform: translate(-30%, -30%);
            }

            100% {
                transform: translate(10%, 10%);
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

        .bookmarks {
            position: fixed;
            bottom: calc(env(safe-area-inset-bottom) + 30px);
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 12px;
            z-index: 100;
            background: rgba(255, 255, 255, 0.08);
            padding: 12px 20px;
            border-radius: 50px;
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border: 1px solid var(--glass-border);
        }

        .bookmark {
            width: 10px;
            height: 10px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            transition: 0.5s all cubic-bezier(0.2, 0.8, 0.2, 1.2);
            cursor: pointer;
        }

        .bookmark.active {
            width: 35px;
            background: var(--primary);
            box-shadow: 0 0 15px var(--primary);
        }

        .viewport {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            perspective: 2000px;
            padding: env(safe-area-inset-top) 20px env(safe-area-inset-bottom) 20px;
        }

        .stage {
            position: absolute;
            /* הפכנו את הרוחב לגמיש יותר כדי למנוע את ה"מריחה" בגיטהב */
            width: 90%;
            max-width: 450px;
            background: var(--glass);
            backdrop-filter: blur(35px);
            -webkit-backdrop-filter: blur(35px);
            border-radius: 35px;
            border: 1px solid var(--glass-border);
            padding: 40px 25px;
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transform: scale(0.85) translateY(40px) rotateX(-15deg);
            transition: 0.9s cubic-bezier(0.2, 0.8, 0.2, 1);
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

        h1 {
            font-family: 'Amatic SC', cursive;
            font-size: 3.5rem;
            margin: 5px 0;
            background: linear-gradient(to bottom, #fff, var(--rose-gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            line-height: 1.1;
        }

        .subtitle {
            font-size: 0.85rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: var(--rose-gold);
            font-weight: 400;
            margin-bottom: 10px;
            opacity: 0.8;
        }

        p {
            font-size: 1.15rem;
            line-height: 1.5;
            font-weight: 300;
            color: rgba(255, 255, 255, 0.9);
            margin-top: 10px;
        }

        .heart-orb {
            position: relative;
            width: 140px;
            height: 140px;
            background: radial-gradient(circle at 30% 30%, rgba(255, 77, 109, 0.8), transparent);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 50px rgba(255, 77, 109, 0.25);
            animation: pulseOrb 4s infinite ease-in-out;
            margin: 20px 0;
        }

        @keyframes pulseOrb {

            0%,
            100% {
                transform: scale(1);
                box-shadow: 0 0 30px rgba(255, 77, 109, 0.2);
            }

            50% {
                transform: scale(1.05);
                box-shadow: 0 0 60px rgba(255, 77, 109, 0.4);
            }
        }

        .heart-icon {
            font-size: 65px;
            filter: drop-shadow(0 0 15px white);
        }

        .feature-box {
            width: 100%;
            background: rgba(255, 255, 255, 0.06);
            border-radius: 18px;
            padding: 15px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 15px;
            text-align: right;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .feature-icon {
            font-size: 1.6rem;
            min-width: 40px;
            text-align: center;
        }

        .feature-box div b {
            display: block;
            font-size: 0.95rem;
            margin-bottom: 2px;
        }

        .feature-box div span {
            font-size: 0.8rem;
            opacity: 0.6;
            display: block;
        }

        .luxury-gift {
            font-size: 90px;
            cursor: pointer;
            position: relative;
            margin-top: 15px;
            transition: 0.4s cubic-bezier(0.175, 0.885, 0.4, 1.4);
        }

        .luxury-gift:active {
            transform: scale(0.9) rotate(-5deg);
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
            font-size: 200px;
            animation: kissImpact 1.5s forwards ease-out;
        }

        @keyframes kissImpact {
            0% {
                transform: scale(0) rotate(-45deg);
                opacity: 0;
            }

            30% {
                transform: scale(1.3) rotate(0);
                opacity: 1;
            }

            100% {
                transform: scale(6);
                opacity: 0;
            }
        }

        .timer-track {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: rgba(255, 255, 255, 0.05);
            overflow: hidden;
            border-radius: 35px 35px 0 0;
        }

        .timer-fill {
            height: 100%;
            width: 0%;
            background: var(--primary);
            box-shadow: 0 0 10px var(--primary);
        }

        @media screen and (orientation: landscape) and (max-height: 500px) {
            .stage {
                transform: scale(0.7) !important;
                padding: 20px;
            }

            h1 {
                font-size: 2.5rem;
            }

            .heart-orb {
                width: 80px;
                height: 80px;
                margin: 10px 0;
            }

            .heart-icon {
                font-size: 40px;
            }
        }
    </style>
</head>

<body>

    <div class="bg-gradient">
        <div class="bg-glow"></div>
    </div>
    <div id="particles-container"></div>

    <div class="bookmarks">
        <div class="bookmark" id="b-1" onclick="jumpTo(1)"></div>
        <div class="bookmark" id="b-2" onclick="jumpTo(2)"></div>
        <div class="bookmark" id="b-3" onclick="jumpTo(3)"></div>
        <div class="bookmark" id="b-4" onclick="jumpTo(4)"></div>
    </div>

    <div class="viewport">
        <div class="stage" id="s-1">
            <div class="timer-track">
                <div class="timer-fill" id="f-1"></div>
            </div>
            <div class="subtitle">Our Love Story</div>
            <h1>דוד & אביה</h1>
            <div class="heart-orb">
                <div class="heart-icon">❤️</div>
            </div>
            <p>שני עולמות שנפגשו<br>והפכו לאחד מופלא.</p>
        </div>

        <div class="stage" id="s-2">
            <div class="timer-track">
                <div class="timer-fill" id="f-2"></div>
            </div>
            <div class="subtitle">Coming Soon</div>
            <h1>ממלכת האהבה</h1>
            <p>אפליקציה שנועדה רק בשבילנו.<br>השקה בקרוב מאוד... 🥹</p>
            <div
                style="margin-top: 25px; width: 100%; height: 2px; background: rgba(255,255,255,0.1); position: relative;">
                <div
                    style="position: absolute; left: 0; top: 0; height: 100%; width: 100%; background: linear-gradient(90deg, transparent, var(--primary), transparent); animation: loadPulse 2.5s infinite linear;">
                </div>
            </div>
            <style>
                @keyframes loadPulse {
                    0% {
                        transform: translateX(-100%);
                    }

                    100% {
                        transform: translateX(100%);
                    }
                }
            </style>
        </div>

        <div class="stage" id="s-3">
            <div class="timer-track">
                <div class="timer-fill" id="f-3"></div>
            </div>
            <div class="subtitle">Inside the App</div>
            <h1 style="font-size: 2.8rem; margin-bottom: 15px;">מה מחכה לנו?</h1>

            <div class="feature-box">
                <div class="feature-icon">💬</div>
                <div>
                    <b>רגעים בשידור חי</b>
                    <span>צ'אט פרטי ואישי רק לנו.</span>
                </div>
            </div>

            <div class="feature-box">
                <div class="feature-icon">⏳</div>
                <div>
                    <b>ציר זמן נצחי</b>
                    <span>כל הזיכרונות במקום אחד.</span>
                </div>
            </div>

            <div class="feature-box">
                <div class="feature-icon">🎁</div>
                <div>
                    <b>הפתעות יומיות</b>
                    <span>מסרים ופינוקים בכל יום.</span>
                </div>
            </div>
        </div>

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

    <div class="the-kiss" id="kissBox">
        <div class="kiss-big">💋</div>
    </div>

    <script>
        let current = 1;
        const total = 4;
        const duration = 6500;
        let timerInt, mainInt;

        function init() {
            render(1);
            startAuto();
            createParticles();

            // מניעת גלילה כפולה ובעיות מתיחה בגיטהב
            document.body.addEventListener('touchmove', function (e) {
                if (e.target.closest('.stage')) return; // אפשר גלילה פנימית אם יש תוכן רב
                e.preventDefault();
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
            for (let i = 0; i < 35; i++) { setTimeout(createExplodingHeart, i * 25); }
            setTimeout(() => { box.style.display = 'none'; }, 1500);
        }

        function createExplodingHeart() {
            const h = document.createElement('div');
            h.innerHTML = Math.random() > 0.5 ? '❤️' : '💋';
            h.style.position = 'fixed';
            h.style.left = '50%'; h.style.top = '50%';
            h.style.fontSize = Math.random() * 35 + 20 + 'px';
            h.style.zIndex = '1100';
            h.style.pointerEvents = 'none';
            const deg = Math.random() * 360;
            const dist = Math.random() * 350 + 100;
            const x = Math.cos(deg * Math.PI / 180) * dist;
            const y = Math.sin(deg * Math.PI / 180) * dist;
            document.body.appendChild(h);
            h.animate([
                { transform: 'translate(-50%, -50%) scale(0) rotate(0deg)', opacity: 1 },
                { transform: `translate(calc(-50% + ${x}px), calc(-50% + ${y}px)) scale(1.4) rotate(${Math.random() * 360}deg)`, opacity: 0 }
            ], { duration: 1000, easing: 'ease-out' }).onfinish = () => h.remove();
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
            }, 1000);
        }

        init();
    </script>
</body>

</html>
