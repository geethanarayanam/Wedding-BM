<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bhavani & Manoj Wedding</title>
    <style>
        :root {
            --gold: #D4AF37;
            --maroon: #800000;
            --cream: #FFFDD0;
            --vintage-red: #a52a2a;
        }

        body, html {
            margin: 0;
            padding: 0;
            font-family: 'Georgia', serif;
            background-color: var(--cream);
            color: var(--maroon);
            scroll-behavior: smooth;
            overflow-x: hidden;
        }

        section {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 20px;
        }

        /* --- Page 1: Addutera (Curtain) Effect --- */
        #curtain-page {
            background: #222;
            perspective: 1000px;
            overflow: hidden;
            position: relative;
        }

        .curtain-container {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            z-index: 2;
        }

        .curtain {
            width: 50%;
            height: 100%;
            background: var(--maroon);
            background-image: repeating-linear-gradient(to right, transparent, transparent 30px, rgba(0,0,0,0.1) 35px);
            transition: transform 2.5s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            box-shadow: inset 0 0 50px #000;
            border-bottom: 10px solid var(--gold);
        }

        .left-curtain { transform-origin: left; border-right: 3px solid var(--gold); }
        .right-curtain { transform-origin: right; border-left: 3px solid var(--gold); }

        .opened .left-curtain { transform: translateX(-100%); }
        .opened .right-curtain { transform: translateX(100%); }

        .names-reveal {
            z-index: 1;
            animation: fadeIn 3s;
        }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .btn {
            margin: 15px;
            padding: 12px 30px;
            background: var(--maroon);
            color: white;
            border: 2px solid var(--gold);
            cursor: pointer;
            font-size: 1.1rem;
            border-radius: 5px;
            transition: 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .btn:hover { background: var(--gold); color: var(--maroon); }

        /* --- Page 2: Date Buttons --- */
        .reveal-box {
            font-size: 2rem;
            color: var(--gold);
            height: 60px;
            margin-bottom: 20px;
            font-weight: bold;
        }

        /* --- Hidden State --- */
        .hidden { display: none; }
        
        .mandapam-icon {
            font-size: 100px;
            margin-bottom: 20px;
            filter: drop-shadow(2px 4px 6px black);
        }
    </style>
</head>
<body>

    <section id="curtain-page">
        <div class="curtain-container" id="curtainWrapper">
            <div class="curtain left-curtain"></div>
            <div class="curtain right-curtain"></div>
        </div>
        <div class="names-reveal">
            <h3 style="color: var(--gold); letter-spacing: 5px;">WEDDING OF</h3>
            <h1 style="font-size: 4rem; margin: 10px 0;">Bhavani <br>&<br> Manoj</h1>
            <button class="btn" onclick="openCurtains()">Reveal Names</button>
            <button id="nextToDate" class="btn hidden" onclick="showPage('date-page')">Press to know the Date</button>
        </div>
    </section>

    <section id="date-page" class="hidden">
        <h2>Click each button to reveal</h2>
        
        <div class="reveal-box" id="display-date">---</div>
        <button class="btn" onclick="revealInfo('display-date', 'October 25th')">Reveal Date</button>

        <div class="reveal-box" id="display-day">---</div>
        <button class="btn" onclick="revealInfo('display-day', 'Sunday')">Reveal Day</button>

        <div class="reveal-box" id="display-year">---</div>
        <button class="btn" onclick="revealInfo('display-year', '2026')">Reveal Year</button>

        <br><br>
        <button id="toInvite" class="btn hidden" onclick="showPage('invite-text')">View Invitation</button>
    </section>

    <section id="invite-text" class="hidden">
        <div style="max-width: 600px; border: 5px double var(--gold); padding: 40px; background: white; box-shadow: 0 0 20px rgba(0,0,0,0.1);">
            <h2 style="font-style: italic;">Wedding Invitation</h2>
            <p>Dear Colleagues,</p>
            <p>We cordially invite you to grace the occasion of our wedding. Your presence and good wishes are highly valued as we begin this new chapter together.</p>
            <p>Please join us for the celebrations!</p>
            <p>With Warm Regards,<br><strong>Bhavani & Manoj</strong></p>
        </div>
        <button class="btn" onclick="showPage('venue-page')">Check Venue Details</button>
    </section>

    <section id="venue-page" class="hidden">
        <div class="mandapam-icon">🏛️</div>
        <h2>Venue</h2>
        <p style="font-size: 1.5rem;"><strong>Swathi Function Hall</strong></p>
        <p>Ongole</p>
        <button class="btn" onclick="showPage('lunch-page')">Press for Lunch Details</button>
    </section>

    <section id="lunch-page" class="hidden">
        <h2 style="color: var(--gold);">Wedding Lunch</h2>
        <div style="font-size: 1.8rem; border-top: 2px solid var(--gold); border-bottom: 2px solid var(--gold); padding: 20px;">
            <p>Sunday | 12:30 PM</p>
            <p>At the Venue</p>
        </div>
        <button class="btn" onclick="showPage('final-page')">Final Message</button>
    </section>

    <section id="final-page" class="hidden">
        <h1 style="color: var(--gold); font-size: 3rem;">Thank You!</h1>
        <p style="font-size: 1.4rem; max-width: 500px;">Thanks to all the guests. Your presence is precious to us.</p>
    </section>

    <script>
        let revealCount = 0;

        function openCurtains() {
            document.getElementById('curtainWrapper').classList.add('opened');
            setTimeout(() => {
                document.getElementById('nextToDate').classList.remove('hidden');
            }, 1500);
        }

        function showPage(pageId) {
            const nextPage = document.getElementById(pageId);
            nextPage.classList.remove('hidden');
            nextPage.scrollIntoView({ behavior: 'smooth' });
        }

        function revealInfo(elementId, text) {
            const el = document.getElementById(elementId);
            if(el.innerText === "---") {
                el.innerText = text;
                revealCount++;
            }
            
            // Once all 3 buttons are pressed, show the "View Invitation" button
            if(revealCount >= 3) {
                document.getElementById('toInvite').classList.remove('hidden');
            }
        }
    </script>
</body>
</html>
