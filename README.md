<html lang="en" dir="ltr" id="htmlRoot">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AuraSync // Neural Ambient & Mood Architecture</title>
    <style>
        :root {
            --bg: #020205;
            --card-bg: #08080f;
            --border: #181824;
            --border-hover: #35354d;
            --text-main: #f0f0f5;
            --text-muted: #707085;
            --accent-cyan: #00f0ff;
            --accent-purple: #9d4edd;
            --accent-pink: #ff007f;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; outline: none; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
        body {
            background-color: var(--bg);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            overflow-x: hidden;
            transition: background 1s ease;
        }
        .container {
            width: 100%;
            max-width: 650px;
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 28px;
            padding: 40px;
            box-shadow: 0 40px 90px rgba(0,0,0,0.95);
            position: relative;
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 18px;
        }
        .brand-logo {
            font-size: 1.1rem;
            letter-spacing: 4px;
            text-transform: uppercase;
            font-weight: 800;
            background: linear-gradient(45deg, var(--accent-cyan), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .lang-options { display: flex; gap: 6px; }
        .lang-btn {
            background: #11111a;
            border: 1px solid var(--border);
            color: var(--text-muted);
            padding: 5px 12px;
            border-radius: 8px;
            font-size: 0.7rem;
            cursor: pointer;
            transition: 0.3s;
        }
        .lang-btn.active, .lang-btn:hover { color: #fff; border-color: var(--accent-cyan); background: #1a1a2b; }

        .screen { display: none; }
        .screen.active { display: block; }

        h2 {
            font-size: 1.6rem;
            font-weight: 500;
            margin-bottom: 10px;
            letter-spacing: 1px;
        }
        p.desc {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-bottom: 25px;
            line-height: 1.6;
        }

        .social-login-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 20px;
        }
        .social-btn {
            width: 100%;
            background: #11111a;
            border: 1px solid var(--border);
            color: #fff;
            padding: 15px;
            border-radius: 14px;
            font-size: 0.85rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            transition: 0.3s;
        }
        .social-btn:hover { border-color: var(--border-hover); background: #161624; transform: translateY(-2px); }

        .mood-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 14px;
            margin-bottom: 25px;
        }
        .mood-card {
            background: #040408;
            border: 2px solid var(--border);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: 0.3s;
        }
        .mood-card:hover, .mood-card.selected { border-color: var(--accent-cyan); background: #0c0c17; box-shadow: 0 0 25px rgba(0,240,255,0.15); }
        .mood-icon { font-size: 2rem; margin-bottom: 8px; }
        .mood-title { font-size: 0.9rem; font-weight: 600; color: #fff; }

        .form-group {
            margin-bottom: 20px;
            text-align: left;
        }
        label {
            display: block;
            font-size: 0.75rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 8px;
        }
        textarea {
            width: 100%;
            background: #040408;
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 15px;
            color: #fff;
            font-size: 0.95rem;
            height: 110px;
            resize: none;
            transition: 0.3s;
        }
        textarea:focus { border-color: var(--accent-cyan); box-shadow: 0 0 20px rgba(0,240,255,0.15); }

        .btn-main {
            width: 100%;
            background: #fff;
            color: #020205;
            border: none;
            padding: 16px;
            border-radius: 14px;
            font-size: 0.85rem;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 2px;
            cursor: pointer;
            transition: 0.3s;
        }
        .btn-main:hover { background: #d0d0dc; transform: translateY(-2px); }

        .aura-container {
            text-align: center;
            padding: 10px 0;
        }
        .aura-orb {
            width: 140px;
            height: 140px;
            border-radius: 50%;
            margin: 30px auto;
            background: radial-gradient(circle, var(--accent-cyan) 0%, #002b3d 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3.5rem;
            box-shadow: 0 0 60px rgba(0, 240, 255, 0.4);
            animation: floatOrb 4s infinite alternate ease-in-out;
        }
        @keyframes floatOrb {
            0% { transform: translateY(0) scale(1); }
            100% { transform: translateY(-10px) scale(1.05); }
        }
        .insight-box {
            background: #040408;
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 20px;
            font-size: 0.95rem;
            color: #fff;
            margin-bottom: 25px;
            line-height: 1.7;
            text-align: center;
        }
        .btn-reset {
            background: #11111a;
            color: var(--text-muted);
            border: 1px solid var(--border);
            padding: 12px 25px;
            border-radius: 12px;
            font-size: 0.8rem;
            cursor: pointer;
            transition: 0.3s;
        }
        .btn-reset:hover { color: #fff; border-color: var(--accent-pink); }
    </style>
</head>
<body>

    <div class="container">
        
        <div class="top-bar">
            <div class="brand-logo">AuraSync</div>
            <div class="lang-options">
                <button class="lang-btn active" onclick="changeAppLang('en')">EN</button>
                <button class="lang-btn" onclick="changeAppLang('fr')">FR</button>
                <button class="lang-btn" onclick="changeAppLang('ar')">AR</button>
            </div>
        </div>

        <div class="screen active" id="screenLogin">
            <h2 id="t-login-title">Synchronize Your Inner Aura</h2>
            <p class="desc" id="t-login-desc">Connect securely to calibrate your digital environment with your emotional frequency.</p>
            
            <div class="social-login-grid">
                <button class="social-btn" onclick="goToMood()">
                    <svg width="18" height="18" viewBox="0 0 24 24"><path fill="#EA4335" d="M12 5c1.6 0 3 .6 4.1 1.6l3.1-3.1C17.3 1.8 14.8 1 12 1 7.5 1 3.7 3.6 1.8 7.3l3.7 2.9C6.4 7.2 9 5 12 5z"/><path fill="#4285F4" d="M23.5 12.3c0-.8-.1-1.6-.2-2.3H12v4.5h6.5c-.3 1.5-1.1 2.8-2.4 3.7l3.7 2.9c2.2-2 3.7-5 3.7-8.8z"/><path fill="#FBBC05" d="M5.5 14.8c-.2-.8-.4-1.8-.4-2.8s.2-2 .4-2.8L1.8 6.3C.7 8.5 0 11.2 0 14s.7 5.5 1.8 7.7l3.7-2.9c-.3-.9-.5-1.9-.5-4z"/><path fill="#34A853" d="M12 23c3.2 0 6-1.1 8-3l-3.7-2.9c-1.1.7-2.5 1.2-4.3 1.2-3 0-5.6-2.2-6.5-5.2L1.8 16c1.9 3.7 5.7 7 10.2 7z"/></svg>
                    <span id="t-google">Continue with Google</span>
                </button>
                <button class="social-btn" onclick="goToMood()">
                    <svg width="18" height="18" viewBox="0 0 24 24" fill="#fff"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M15.97 5.35c.61-.75 1.03-1.8.92-2.85-.89.04-1.97.6-2.6 1.35-.57.67-1.08 1.74-.95 2.78 1 .08 2.02-.48 2.63-1.28z"/></svg>
                    <span id="t-apple">Continue with Apple ID</span>
                </button>
            </div>
        </div>

        <div class="screen" id="screenMood">
            <h2 id="t-mood-title">Select Your Current Frequency</h2>
            <p class="desc" id="t-mood-desc">Choose how you feel right now to tailor your personal resonance field.</p>

            <div class="mood-grid">
                <div class="mood-card selected" id="cardDeep" onclick="selectMood('deep')">
                    <div class="mood-icon">🌌</div>
                    <div class="mood-title" id="m-deep">Deep Focus (تركيز عميق)</div>
                </div>
                <div class="mood-card" id="cardCalm" onclick="selectMood('calm')">
                    <div class="mood-icon">🍃</div>
                    <div class="mood-title" id="m-calm">Absolute Calm (هدوء تام)</div>
                </div>
                <div class="mood-card" id="cardEnergy" onclick="selectMood('energy')">
                    <div class="mood-icon">⚡</div>
                    <div class="mood-title" id="m-energy">High Energy (طاقة وإبداع)</div>
                </div>
                <div class="mood-card" id="cardReflect" onclick="selectMood('reflect')">
                    <div class="mood-icon">🔮</div>
                    <div class="mood-title" id="m-reflect">Reflection (تأمل وراحة)</div>
                </div>
            </div>

            <div class="form-group">
                <label id="t-label-thought">Your Current Intention or Thought</label>
                <textarea id="userThought" placeholder="Write what's on your mind... e.g. Building a great future step by step."></textarea>
            </div>

            <button class="btn-main" onclick="launchAura()" id="t-launch-btn">Calibrate Aura</button>
        </div>

        <div class="screen" id="screenAura">
            <div class="aura-container">
                <div class="aura-orb" id="orbIcon">🌌</div>
                
                <div class="insight-box" id="insightText">
                    Calibrating neural resonance field based on your current state...
                </div>

                <button class="btn-reset" onclick="resetAura()" id="t-reset-btn">Recalibrate Aura</button>
            </div>
        </div>

    </div>

    <script>
        const uiText = {
            en: {
                loginTitle: "Synchronize Your Inner Aura",
                loginDesc: "Connect securely to calibrate your digital environment with your emotional frequency.",
                google: "Continue with Google",
                apple: "Continue with Apple ID",
                moodTitle: "Select Your Current Frequency",
                moodDesc: "Choose how you feel right now to tailor your personal resonance field.",
                mDeep: "Deep Focus",
                mCalm: "Absolute Calm",
                mEnergy: "High Energy",
                mReflect: "Reflection",
                labelThought: "Your Current Intention or Thought",
                launchBtn: "Calibrate Aura",
                resetBtn: "Recalibrate Aura"
            },
            fr: {
                loginTitle: "Synchronisez Votre Aura Intérieure",
                loginDesc: "Connectez-vous pour calibrer votre environnement numérique.",
                google: "Continuer avec Google",
                apple: "Continuer avec Apple ID",
                moodTitle: "Sélectionnez Votre Fréquence",
                moodDesc: "Choisissez votre état actuel pour adapter votre espace.",
                mDeep: "Focus Profond",
                mCalm: "Calme Absolu",
                mEnergy: "Haute Énergie",
                mReflect: "Réflexion",
                labelThought: "Votre Pensée ou Intention",
                launchBtn: "Calibrer l'Aura",
                resetBtn: "Recalibrer"
            },
            ar: {
                loginTitle: "وازن مجالك الداخلي (AuraSync)",
                loginDesc: "سجل دخولك لربط بيئتك الرقمية بترددك النفسي والذهني الحالي.",
                google: "المتابعة باستخدام قوقل",
                apple: "المتابعة باستخدام أبل آي كلاود",
                moodTitle: "اختر حالتك وترددك الحالي",
                moodDesc: "حدد شعورك الآن ليقوم النظام بتكييف المساحة الرقمية خصيصاً لك.",
                mDeep: "تركيز عميق (Deep Focus)",
                mCalm: "هدوء وسكينة (Absolute Calm)",
                mEnergy: "طاقة وإبداع (High Energy)",
                mReflect: "تأمل ووعي (Reflection)",
                labelThought: "أكتب فكرتك أو نيتك اللحظية",
                launchBtn: "تفعيل المجال الذكي",
                resetBtn: "إعادة ضبط المجال"
            }
        };

        let currentAppLang = 'en';
        let selectedMood = 'deep';

        function changeAppLang(lang) {
            currentAppLang = lang;
            document.getElementById('htmlRoot').setAttribute('lang', lang);
            document.getElementById('htmlRoot').setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');
            
            document.querySelectorAll('.lang-btn').forEach(b => b.classList.remove('active'));
            event.target.classList.add('active');

            const t = uiText[lang];
            document.getElementById('t-login-title').textContent = t.loginTitle;
            document.getElementById('t-login-desc').textContent = t.loginDesc;
            document.getElementById('t-google').textContent = t.google;
            document.getElementById('t-apple').textContent = t.apple;
            document.getElementById('t-mood-title').textContent = t.moodTitle;
            document.getElementById('t-mood-desc').textContent = t.moodDesc;
            document.getElementById('m-deep').textContent = t.mDeep;
            document.getElementById('m-calm').textContent = t.mCalm;
            document.getElementById('m-energy').textContent = t.mEnergy;
            document.getElementById('m-reflect').textContent = t.mReflect;
            document.getElementById('t-label-thought').textContent = t.labelThought;
            document.getElementById('t-launch-btn').textContent = t.launchBtn;
            document.getElementById('t-reset-btn').textContent = t.resetBtn;
        }

        function goToMood() {
            document.getElementById('screenLogin').classList.remove('active');
            document.getElementById('screenMood').classList.add('active');
        }

        function selectMood(mood) {
            selectedMood = mood;
            document.querySelectorAll('.mood-card').forEach(c => c.classList.remove('selected'));
            document.getElementById('card' + mood.charAt(0).toUpperCase() + mood.slice(1)).classList.add('selected');
        }

        function launchAura() {
            const thought = document.getElementById('userThought').value.trim();
            document.getElementById('screenMood').classList.remove('active');
            document.getElementById('screenAura').classList.add('active');

            const orb = document.getElementById('orbIcon');
            const insight = document.getElementById('insightText');

            let icon = '🌌';
            let message = '';

            if (selectedMood === 'deep') {
                icon = '🌌';
                message = currentAppLang === 'ar' ? 
                    `✨ مجالك المهيأ: التركيز العميق.\n"الوضوح الذهني يبدأ بإقصاء المشتتات والتركيز على نقطة واحدة."\n${thought ? 'فكرتك المسجلة: "' + thought + '" تتوافق تماماً مع نسق الإنتاج العالي.' : ''}` :
                    `✨ Deep Focus Aura Active.\n"Clarity comes from removing the non-essential."\n${thought ? 'Your intention: "' + thought + '" aligns with high productivity.' : ''}`;
            } else if (selectedMood === 'calm') {
                icon = '🍃';
                message = currentAppLang === 'ar' ? 
                    `🍃 مجالك المهيأ: الهدوء التام.\n"تنفس بعمق، أنت في المكان والزمان المناسبين تماماً."\n${thought ? 'رؤيتك: "' + thought + '" تحمل طاقة سلام داخلي عالية.' : ''}` :
                    `🍃 Absolute Calm Aura Active.\n"Breathe in peace, exhale tension."\n${thought ? 'Your thought: "' + thought + '" resonates with serenity.' : ''}`;
            } else if (selectedMood === 'energy') {
                icon = '⚡';
                message = currentAppLang === 'ar' ? 
                    `⚡ مجالك المهيأ: الطاقة العالية والإبداع.\n"الشغف هو الوقود الذي يترجم الأفكار إلى واقع ملموس."\n${thought ? 'شحنتك الفكرية: "' + thought + '" جاهزة للإطلاق والتنفيذ.' : ''}` :
                    `⚡ High Energy Aura Active.\n"Passion is the fuel of monumental action."\n${thought ? 'Your drive: "' + thought + '" is fully charged.' : ''}`;
            } else {
                icon = '🔮';
                message = currentAppLang === 'ar' ? 
                    `🔮 مجالك المهيأ: التأمل والوعي العميق.\n"التأمل في التفاصيل يصنع الرؤى الاستثنائية."\n${thought ? 'تأملك: "' + thought + '" يعكس عمقاً فكرياً مميزاً.' : ''}` :
                    `🔮 Reflection Aura Active.\n"Contemplation births extraordinary insights."\n${thought ? 'Your reflection: "' + thought + '" shows profound depth.' : ''}`;
            }

            orb.textContent = icon;
            insight.innerText = message;
        }

        function resetAura() {
            document.getElementById('screenAura').classList.remove('active');
            document.getElementById('screenMood').classList.add('active');
        }
    </script>
</body>
</html>
