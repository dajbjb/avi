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
            --deep-rose: #c9184a;
            --rose-gold: #ffb3c1;
            --wine: #590d22;
            --glass: rgba(255, 255, 255, 0.15);
            --glass-border: rgba(255, 255, 255, 0.3);
            --shadow: 0 20px 50px rgba(0, 0, 0, 0.15);
        }

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body,
        html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            font-family: 'Assistant', sans-serif;
            background: #0a0a0a;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

        /* רקע דינמי יוקרתי */
        .bg-gradient {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: radial-gradient(circle at 20% 30%, #590d22 0%, #0a0a0a 100%);
            overflow: hidden;
        }

        .bg-glow {
            position: absolute;
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(255, 77, 109, 0.15) 0%, transparent 70%);
            border-radius: 50%;
            filter: blur(80px);
            animation: moveGlow 20s infinite alternate;
        }

        @keyframes moveGlow {
            0% {
                transform: translate(-10%, -10%);
            }

            100% {
                transform: translate(50%, 50%);
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

        /* סימניות מודרניות - Floating Pills */
        .bookmarks {
            position: fixed;
            bottom: 40px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 15px;
            z-index: 100;
            background: rgba(255, 255, 255, 0.05);
            padding: 10px 20px;
            border-radius: 50px;
            backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
        }

        .bookmark {
            width: 12px;
            height: 12px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            transition: 0.4s all cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
        }

        .bookmark.active {
            width: 40px;
            background: var(--primary);
            box-shadow: 0 0 15px var(--primary);
        }

        /* קונטיינר שלבים */
        .viewport {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            perspective: 2000px;
        }

        .stage {
            position: absolute;
            width: 90%;
            max-width: 500px;
            background: var(--glass);
            backdrop-filter: blur(30px);
            -webkit-backdrop-filter: blur(30px);
            border-radius: 40px;
            border: 1px solid var(--glass-border);
            padding: 50px 30px;
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transform: scale(0.8) translateY(50px) rotateX(-20deg);
            transition: 1s cubic-bezier(0.2, 0.8, 0.2, 1);
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
            font-size: 4.5rem;
            margin: 0;
            background: linear-gradient(to bottom, #fff, var(--rose-gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 5px 15px rgba(0, 0, 0, 0.2));
            line-height: 1;
        }

        .subtitle {
            font-size: 1.1rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--rose-gold);
            font-weight: 300;
            margin-bottom: 20px;
            opacity: 0.8;
        }

        p {
            font-size: 1.3rem;
            line-height: 1.6;
            font-weight: 200;
            color: rgba(255, 255, 255, 0.9);
            margin-top: 15px;
        }

        /* רכיבים ויזואליים משוכללים */
        .heart-orb {
            position: relative;
            width: 180px;
            height: 180px;
            background: radial-gradient(circle at 30% 30%, rgba(255, 77, 109, 0.8), transparent);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 60px rgba(255, 77, 109, 0.3), inset 0 0 30px rgba(255, 255, 255, 0.2);
            animation: pulseOrb 4s infinite ease-in-out;
            margin: 30px 0;
        }

        @keyframes pulseOrb {

            0%,
            100% {
                transform: scale(1) rotate(0deg);
                box-shadow: 0 0 40px rgba(255, 77, 109, 0.2);
            }

            50% {
                transform: scale(1.05) rotate(5deg);
                box-shadow: 0 0 80px rgba(255, 77, 109, 0.5);
            }
        }

        .heart-icon {
            font-size: 80px;
            filter: drop-shadow(0 0 20px white);
        }

        /* כרטיסיות פיצ'רים */
        .feature-box {
            width: 100%;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 20px;
            text-align: right;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: 0.3s;
        }

        .feature-box:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(-10px);
        }

        .feature-icon {
            font-size: 2rem;
            min-width: 50px;
            text-align: center;
        }

        /* מתנה יוקרתית */
        .luxury-gift {
            font-size: 100px;
            cursor: pointer;
            position: relative;
            transition: 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .luxury-gift:hover {
            transform: scale(1.1) rotate(10deg);
            filter: brightness(1.2);
        }

        .luxury-gift::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 150%;
            height: 150%;
            background: radial-gradient(circle, var(--primary) 0%, transparent 70%);
            z-index: -1;
            opacity: 0.3;
            animation: glowPulse 2s infinite;
        }

        @keyframes glowPulse {

            0%,
            100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 0.2;
            }

            50% {
                transform: translate(-50%, -50%) scale(1.3);
                opacity: 0.4;
            }
        }

        /* לוגיקת נשיקה */
        .the-kiss {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            display: none;
            align-items: center;
            justify-content: center;
        }

        .kiss-big {
            font-size: 300px;
            animation: kissImpact 1.5s forwards cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes kissImpact {
            0% {
                transform: scale(0) rotate(-45deg);
                opacity: 0;
                filter: blur(20px);
            }

            40% {
                transform: scale(1.2) rotate(0);
                opacity: 1;
                filter: blur(0);
            }

            70% {
                transform: scale(1);
                opacity: 1;
            }

            100% {
                transform: scale(5);
                opacity: 0;
            }
        }

        /* פס טעינה דק ויוקרתי */
        .timer-track {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: rgba(255, 255, 255, 0.05);
        }

        .timer-fill {
            height: 100%;
            width: 0%;
            background: var(--primary);
            box-shadow: 0 0 10px var(--primary);
        }
    </style>
</head>

<body>

    <div class="bg-gradient">
        <div class="bg-glow"></div>
    </div>
    <div id="particles-container"></div>

    <!-- ניווט סימניות מודרני -->
    <div class="bookmarks">
        <div class="bookmark" id="b-1" onclick="jumpTo(1)"></div>
        <div class="bookmark" id="b-2" onclick="jumpTo(2)"></div>
        <div class="bookmark" id="b-3" onclick="jumpTo(3)"></div>
        <div class="bookmark" id="b-4" onclick="jumpTo(4)"></div>
    </div>

    <div class="viewport">

        <!-- שלב 1: שמות -->
        <div class="stage" id="s-1">
            <div class="timer-track">
                <div class="timer-fill" id="f-1"></div>
            </div>
            <div class="subtitle">Our Love Story</div>
            <h1>דוד & אביה</h1>
            <div class="heart-orb">
                <div class="heart-icon">❤️</div>
            </div>
            <p>שני עולמות שנפגשו והפכו לאחד.</p>
        </div>

        <!-- שלב 2: השקה -->
        <div class="stage" id="s-2">
            <div class="timer-track">
                <div class="timer-fill" id="f-2"></div>
            </div>
            <div class="subtitle">Coming Soon</div>
            <h1 style="font-size: 3.5rem;">ממלכת האהבה</h1>
            <p>אפליקציה שנועדה רק בשבילנו דוד ואביה.<br>השקה ושימוש בקרוב מאוד... 🥹</p>
            <div
                style="margin-top: 30px; width: 100%; height: 2px; background: rgba(255,255,255,0.1); position: relative;">
                <div
                    style="position: absolute; left: 0; top: 0; height: 100%; width: 60%; background: var(--primary); box-shadow: 0 0 15px var(--primary); animation: loadPulse 2s infinite;">
                </div>
            </div>
        </div>

        <!-- שלב 3: פיצ'רים -->
        <div class="stage" id="s-3">
            <div class="timer-track">
                <div class="timer-fill" id="f-3"></div>
            </div>
            <div class="subtitle">Inside the App</div>
            <h1 style="font-size: 3rem; margin-bottom: 20px;">מה מחכה בפנים?</h1>

            <div class="feature-box">
                <div class="feature-icon">💬</div>
                <div>
                    <div style="font-weight: 700; font-size: 1.1rem;">רגעים בשידור חי</div>
                    <div style="opacity: 0.6; font-size: 0.9rem;">צ'אט פרטי שסופר כל רגע ביחד.</div>
                </div>
            </div>

            <div class="feature-box">
                <div class="feature-icon">💎</div>
                <div>
                    <div style="font-weight: 700; font-size: 1.1rem;">עיצוב אישי</div>
                    <div style="opacity: 0.6; font-size: 0.9rem;">חוויה יוקרתית שמותאמת רק לכם.</div>
                </div>
            </div>

            <div class="feature-box">
                <div class="feature-icon">⏳</div>
                <div>
                    <div style="font-weight: 700; font-size: 1.1rem;">ציר זמן נצחי</div>
                    <div style="opacity: 0.6; font-size: 0.9rem;">כל הזיכרונות במקום אחד.</div>
                </div>
            </div>
        </div>

        <!-- שלב 4: מתנה -->
        <div class="stage" id="s-4">
            <div class="timer-track">
                <div class="timer-fill" id="f-4"></div>
            </div>
            <div class="subtitle">For You</div>
            <h1>משהו קטן...</h1>
            <p>לחצי כדי לגלות מה מחכה לך בתיבה</p>
            <div class="luxury-gift" onclick="blastKiss()">🎁</div>
        </div>

    </div>

    <!-- אפקט נשיקה -->
    <div class="the-kiss" id="kissBox">
        <div class="kiss-big">💋</div>
    </div>

    <script>
        let current = 1;
        const total = 4;
        const duration = 7000;
        let timerInt, mainInt;

        function init() {
            render(1);
            startAuto();
            createParticles();
        }

        function render(n) {
            document.querySelectorAll('.stage').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.bookmark').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.timer-fill').forEach(f => f.style.width = '0%');

            const s = document.getElementById(`s-${n}`);
            const b = document.getElementById(`b-${n}`);
            s.classList.add('active');
            b.classList.add('active');

            current = n;
            animateTimer(n);
        }

        function animateTimer(n) {
            const fill = document.getElementById(`f-${n}`);
            let start = Date.now();
            if (timerInt) clearInterval(timerInt);

            timerInt = setInterval(() => {
                let p = ((Date.now() - start) / duration) * 100;
                if (p <= 100) fill.style.width = p + '%';
                else clearInterval(timerInt);
            }, 50);
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

            for (let i = 0; i < 40; i++) {
                setTimeout(createExplodingHeart, i * 20);
            }

            setTimeout(() => {
                box.style.display = 'none';
            }, 1500);
        }

        function createExplodingHeart() {
            const h = document.createElement('div');
            h.innerHTML = Math.random() > 0.5 ? '❤️' : '💋';
            h.style.position = 'fixed';
            h.style.left = '50%'; h.style.top = '50%';
            h.style.fontSize = Math.random() * 40 + 20 + 'px';
            h.style.zIndex = '1100';

            const deg = Math.random() * 360;
            const dist = Math.random() * 400 + 100;
            const x = Math.cos(deg * Math.PI / 180) * dist;
            const y = Math.sin(deg * Math.PI / 180) * dist;

            document.body.appendChild(h);

            h.animate([
                { transform: 'translate(-50%, -50%) scale(0) rotate(0deg)', opacity: 1 },
                { transform: `translate(calc(-50% + ${x}px), calc(-50% + ${y}px)) scale(1.5) rotate(${Math.random() * 360}deg)`, opacity: 0 }
            ], {
                duration: 1200, easing: 'ease-out'
            }).onfinish = () => h.remove();
        }

        function createParticles() {
            const container = document.getElementById('particles-container');
            setInterval(() => {
                const p = document.createElement('div');
                p.style.position = 'absolute';
                p.style.bottom = '-20px';
                p.style.left = Math.random() * 100 + 'vw';
                p.style.fontSize = Math.random() * 20 + 10 + 'px';
                p.style.opacity = Math.random() * 0.5;
                p.innerHTML = Math.random() > 0.8 ? '✨' : '💖';
                container.appendChild(p);

                p.animate([
                    { transform: 'translateY(0) rotate(0deg)', opacity: p.style.opacity },
                    { transform: `translateY(-110vh) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                ], {
                    duration: Math.random() * 5000 + 10000,
                    easing: 'linear'
                }).onfinish = () => p.remove();
            }, 800);
        }

        init();
    </script>
</body>

</html>
