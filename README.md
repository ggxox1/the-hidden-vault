<html lang="en" dir="ltr" id="htmlRoot">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Polyglot AI // Neural Language Academy</title>
    <style>
        :root {
            --bg: #030305;
            --card-bg: #0a0a0f;
            --border: #1a1a24;
            --border-hover: #3a3a50;
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
        }
        .container {
            width: 100%;
            max-width: 650px;
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 24px;
            padding: 35px;
            box-shadow: 0 40px 80px rgba(0,0,0,0.9);
            position: relative;
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 15px;
        }
        .brand-logo {
            font-size: 1.1rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            font-weight: 700;
            color: #fff;
            background: linear-gradient(45deg, var(--accent-cyan), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .lang-options { display: flex; gap: 6px; }
        .lang-btn {
            background: #111118;
            border: 1px solid var(--border);
            color: var(--text-muted);
            padding: 4px 10px;
            border-radius: 6px;
            font-size: 0.7rem;
            cursor: pointer;
            transition: 0.3s;
        }
        .lang-btn.active, .lang-btn:hover { color: #fff; border-color: var(--accent-cyan); background: #1a1a26; }

        .screen { display: none; }
        .screen.active { display: block; }

        h2 {
            font-size: 1.5rem;
            font-weight: 400;
            margin-bottom: 10px;
            letter-spacing: 1px;
        }
        p.desc {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-bottom: 25px;
            line-height: 1.5;
        }

        .social-login-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 25px;
        }
        .social-btn {
            width: 100%;
            background: #111118;
            border: 1px solid var(--border);
            color: #fff;
            padding: 14px;
            border-radius: 12px;
            font-size: 0.85rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            transition: 0.3s;
        }
        .social-btn:hover { border-color: var(--border-hover); background: #161622; transform: translateY(-2px); }

        .form-group {
            margin-bottom: 18px;
            text-align: left;
        }
        label {
            display: block;
            font-size: 0.75rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 6px;
        }
        input, select {
            width: 100%;
            background: #050508;
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 12px 15px;
            color: #fff;
            font-size: 0.9rem;
            transition: 0.3s;
        }
        input:focus, select:focus { border-color: var(--accent-cyan); box-shadow: 0 0 15px rgba(0, 240, 255, 0.15); }

        .tutors-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 25px;
        }
        .tutor-card {
            background: #050508;
            border: 2px solid var(--border);
            border-radius: 14px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: 0.3s;
        }
        .tutor-card.selected { border-color: var(--accent-cyan); background: #0b0b14; box-shadow: 0 0 20px rgba(0,240,255,0.2); }
        .tutor-avatar { font-size: 2rem; margin-bottom: 8px; }
        .tutor-name { font-size: 0.9rem; font-weight: 600; color: #fff; margin-bottom: 4px; }
        .tutor-role { font-size: 0.7rem; color: var(--text-muted); }

        .btn-main {
            width: 100%;
            background: #fff;
            color: #030305;
            border: none;
            padding: 15px;
            border-radius: 12px;
            font-size: 0.85rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 2px;
            cursor: pointer;
            transition: 0.3s;
        }
        .btn-main:hover { background: #d0d0d8; transform: translateY(-2px); }

        .call-container {
            text-align: center;
            padding: 10px 0;
        }
        .orb-wave {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            margin: 30px auto;
            background: radial-gradient(circle, var(--accent-cyan) 0%, #004d61 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            box-shadow: 0 0 40px rgba(0, 240, 255, 0.4);
            position: relative;
            transition: 0.3s;
        }
        .orb-wave.speaking {
            animation: pulseWave 1.5s infinite alternate;
        }
        @keyframes pulseWave {
            0% { transform: scale(1); box-shadow: 0 0 20px rgba(0,240,255,0.3); }
            100% { transform: scale(1.08); box-shadow: 0 0 50px rgba(0,240,255,0.7); }
        }
        .call-status {
            font-size: 0.85rem;
            color: var(--accent-cyan);
            letter-spacing: 2px;
            text-transform: uppercase;
            margin-bottom: 20px;
        }
        .chat-transcript {
            background: #050508;
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 15px;
            height: 120px;
            overflow-y: auto;
            text-align: left;
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-bottom: 25px;
            line-height: 1.6;
        }
        .controls-flex {
            display: flex;
            gap: 10px;
        }
        .btn-mic {
            flex: 2;
            background: var(--accent-cyan);
            color: #000;
            border: none;
            padding: 14px;
            border-radius: 12px;
            font-weight: 700;
            font-size: 0.8rem;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: 0.3s;
        }
        .btn-mic.listening {
            background: var(--accent-pink);
            color: #fff;
            animation: pulseMic 1s infinite;
        }
        @keyframes pulseMic { 0% { opacity: 0.8; } 50% { opacity: 1; } 100% { opacity: 0.8; } }
        .btn-end {
            flex: 1;
            background: #ff3344;
            color: #fff;
            border: none;
            padding: 14px;
            border-radius: 12px;
            font-weight: 700;
            font-size: 0.8rem;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <div class="container">
        
        <div class="top-bar">
            <div class="brand-logo">Polyglot AI</div>
            <div class="lang-options">
                <button class="lang-btn active" onclick="changeAppLang('en')">EN</button>
                <button class="lang-btn" onclick="changeAppLang('fr')">FR</button>
                <button class="lang-btn" onclick="changeAppLang('ar')">AR</button>
            </div>
        </div>

        <div class="screen active" id="screenLogin">
            <h2 id="t-login-title">Welcome to Neural Academy</h2>
            <p class="desc" id="t-login-desc">Sign in instantly to start your voice-immersed language journey.</p>
            
            <div class="social-login-grid">
                <button class="social-btn" onclick="skipToProfile('Google')">
                    <svg width="18" height="18" viewBox="0 0 24 24"><path fill="#EA4335" d="M12 5c1.6 0 3 .6 4.1 1.6l3.1-3.1C17.3 1.8 14.8 1 12 1 7.5 1 3.7 3.6 1.8 7.3l3.7 2.9C6.4 7.2 9 5 12 5z"/><path fill="#4285F4" d="M23.5 12.3c0-.8-.1-1.6-.2-2.3H12v4.5h6.5c-.3 1.5-1.1 2.8-2.4 3.7l3.7 2.9c2.2-2 3.7-5 3.7-8.8z"/><path fill="#FBBC05" d="M5.5 14.8c-.2-.8-.4-1.8-.4-2.8s.2-2 .4-2.8L1.8 6.3C.7 8.5 0 11.2 0 14s.7 5.5 1.8 7.7l3.7-2.9c-.3-.9-.5-1.9-.5-4z"/><path fill="#34A853" d="M12 23c3.2 0 6-1.1 8-3l-3.7-2.9c-1.1.7-2.5 1.2-4.3 1.2-3 0-5.6-2.2-6.5-5.2L1.8 16c1.9 3.7 5.7 7 10.2 7z"/></svg>
                    <span id="t-google">Continue with Google</span>
                </button>
                <button class="social-btn" onclick="skipToProfile('Apple')">
                    <svg width="18" height="18" viewBox="0 0 24 24" fill="#fff"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M15.97 5.35c.61-.75 1.03-1.8.92-2.85-.89.04-1.97.6-2.6 1.35-.57.67-1.08 1.74-.95 2.78 1 .08 2.02-.48 2.63-1.28z"/></svg>
                    <span id="t-apple">Continue with Apple ID</span>
                </button>
            </div>
        </div>

        <div class="screen" id="screenProfile">
            <h2 id="t-prof-title">Personalize Your Teacher</h2>
            <p class="desc" id="t-prof-desc">Tell us your goals so your personal AI professor can customize the conversation.</p>

            <div class="form-group">
                <label id="t-label-name">Your Full Name</label>
                <input type="text" id="userName" placeholder="e.g. Wassim">
            </div>

            <div class="form-group">
                <label id="t-label-age">Your Age</label>
                <input type="number" id="userAge" placeholder="e.g. 22">
            </div>

            <div class="form-group">
                <label id="t-label-lang">Language You Want to Learn</label>
                <select id="targetLang">
                    <option value="en">English (الإنجليزية)</option>
                    <option value="fr">French (الفرنسية)</option>
                    <option value="es">Spanish (الإسبانية)</option>
                    <option value="de">German (الألمانية)</option>
                </select>
            </div>

            <div class="form-group">
                <label id="t-label-level">Your Current Level</label>
                <select id="userLevel">
                    <option value="beginner" id="lvl-beg">Beginner (مبتدئ تماماً)</option>
                    <option value="intermediate" id="lvl-int">Intermediate (متوسط)</option>
                    <option value="advanced" id="lvl-adv">Advanced (متقدم)</option>
                </select>
            </div>

            <label id="t-label-tutor" style="margin-top: 15px; margin-bottom: 8px;">Choose Your AI Professor</label>
            <div class="tutors-grid">
                <div class="tutor-card selected" id="cardAlex" onclick="selectTutor('Alex')">
                    <div class="tutor-avatar">👨‍🏫</div>
                    <div class="tutor-name">Alex</div>
                    <div class="tutor-role" id="t-alex-role">Male Voice (Deep & Clear)</div>
                </div>
                <div class="tutor-card" id="cardAlexa" onclick="selectTutor('Alexa')">
                    <div class="tutor-avatar">👩‍🏫</div>
                    <div class="tutor-name">Alexa</div>
                    <div class="tutor-role" id="t-alexa-role">Female Voice (Soft & Natural)</div>
                </div>
            </div>

            <button class="btn-main" onclick="startCallSession()" id="t-start-btn">Start Voice Session</button>
        </div>

        <div class="screen" id="screenCall">
            <div class="call-container">
                <div class="call-status" id="callStatusIndicator">Connected // Live AI Tutor</div>
                
                <div class="orb-wave" id="aiOrb">🎙️</div>
                
                <div class="chat-transcript" id="chatTranscript">
                    <span id="initTranscriptMessage">Establishing secure neural audio bridge...</span>
                </div>

                <div class="controls-flex">
                    <button class="btn-mic" id="micBtn" onclick="toggleSpeechRecognition()">
                        <span id="t-mic-text">Hold to Speak</span>
                    </button>
                    <button class="btn-end" onclick="endCall()" id="t-end-btn">End</button>
                </div>
            </div>
        </div>

    </div>

    <script>
        const uiText = {
            en: {
                loginTitle: "Welcome to Neural Academy",
                loginDesc: "Sign in instantly to start your voice-immersed language journey.",
                google: "Continue with Google",
                apple: "Continue with Apple ID",
                profTitle: "Personalize Your Teacher",
                profDesc: "Tell us your goals so your personal AI professor can customize the conversation.",
                labelName: "Your Full Name",
                labelAge: "Your Age",
                labelLang: "Language You Want to Learn",
                labelLevel: "Your Current Level",
                lvlBeg: "Beginner (Absolute Zero)",
                lvlInt: "Intermediate",
                lvlAdv: "Advanced",
                labelTutor: "Choose Your AI Professor",
                alexRole: "Male Voice (Deep & Clear)",
                alexaRole: "Female Voice (Soft & Natural)",
                startBtn: "Start Voice Session",
                micText: "Tap to Speak",
                endBtn: "End"
            },
            fr: {
                loginTitle: "Bienvenue à l'Académie Neurale",
                loginDesc: "Connectez-vous instantanément pour commencer votre parcours.",
                google: "Continuer avec Google",
                apple: "Continuer avec Apple ID",
                profTitle: "Personnalisez Votre Professeur",
                profDesc: "Dites-nous vos objectifs pour adapter la conversation.",
                labelName: "Votre Nom Complet",
                labelAge: "Votre Âge",
                labelLang: "Langue à Apprendre",
                labelLevel: "Votre Niveau Actuel",
                lvlBeg: "Débutant",
                lvlInt: "Intermédiaire",
                lvlAdv: "Avancé",
                labelTutor: "Choisissez Votre Professeur IA",
                alexRole: "Voix Masculine",
                alexaRole: "Voix Féminine",
                startBtn: "Démarrer la Session Vocale",
                micText: "Appuyez pour Parler",
                endBtn: "Fin"
            },
            ar: {
                loginTitle: "أهلاً بك في الأكاديمية الذكية",
                loginDesc: "سجل دخولك فوراً وابدأ رحلة تعلم اللغة بالمحادثة الصوتية الواقعية.",
                google: "المتابعة باستخدام قوقل",
                apple: "المتابعة باستخدام أبل آي كلاود",
                profTitle: "تخصيص أستاذك الذكي",
                profDesc: "أدخل بياناتك لكي يتحدث معك الأستاذ بالطريقة التي تناسب مستواك تماماً.",
                labelName: "اسمك الكريم",
                labelAge: "عمرك",
                labelLang: "اللغة التي تريد تعلمها",
                labelLevel: "مستواك الحالي فيها",
                lvlBeg: "مبتدئ تماماً",
                lvlInt: "متوسط",
                lvlAdv: "متقدم",
                labelTutor: "اختر أستاذك الذكي (الصوت)",
                alexRole: "صوت رجل (Alex)",
                alexaRole: "صوت امرأة (Alexa)",
                startBtn: "بدء المكالمة الصوتية الآن",
                micText: "اضغط وتكلم الآن",
                endBtn: "إنهاء"
            }
        };

        let currentAppLang = 'en';
        let selectedTutor = 'Alex';
        let userData = { name: '', age: '', lang: 'en', level: 'beginner' };
        let recognition = null;
        let isListening = false;
        let systemVoices = [];

        // تحميل الأصوات المتاحة في المتصفح تلقائياً فور توفرها
        function loadVoices() {
            if ('speechSynthesis' in window) {
                systemVoices = window.speechSynthesis.getVoices();
            }
        }
        loadVoices();
        if ('speechSynthesis' in window) {
            window.speechSynthesis.onvoiceschanged = loadVoices;
        }

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
            document.getElementById('t-prof-title').textContent = t.profTitle;
            document.getElementById('t-prof-desc').textContent = t.profDesc;
            document.getElementById('t-label-name').textContent = t.labelName;
            document.getElementById('t-label-age').textContent = t.labelAge;
            document.getElementById('t-label-lang').textContent = t.labelLang;
            document.getElementById('t-label-level').textContent = t.labelLevel;
            document.getElementById('lvl-beg').textContent = t.lvlBeg;
            document.getElementById('lvl-int').textContent = t.lvlInt;
            document.getElementById('lvl-adv').textContent = t.lvlAdv;
            document.getElementById('t-label-tutor').textContent = t.labelTutor;
            document.getElementById('t-alex-role').textContent = t.alexRole;
            document.getElementById('t-alexa-role').textContent = t.alexaRole;
            document.getElementById('t-start-btn').textContent = t.startBtn;
            document.getElementById('t-mic-text').textContent = t.micText;
            document.getElementById('t-end-btn').textContent = t.endBtn;
        }

        function skipToProfile(provider) {
            document.getElementById('screenLogin').classList.remove('active');
            document.getElementById('screenProfile').classList.add('active');
        }

        function selectTutor(tutorName) {
            selectedTutor = tutorName;
            if(tutorName === 'Alex') {
                document.getElementById('cardAlex').classList.add('selected');
                document.getElementById('cardAlexa').classList.remove('selected');
            } else {
                document.getElementById('cardAlexa').classList.add('selected');
                document.getElementById('cardAlex').classList.remove('selected');
            }
        }

        function startCallSession() {
            userData.name = document.getElementById('userName').value.trim() || (currentAppLang === 'ar' ? 'صديقي' : 'Friend');
            userData.age = document.getElementById('userAge').value.trim() || '20';
            userData.lang = document.getElementById('targetLang').value;
            userData.level = document.getElementById('userLevel').value;

            document.getElementById('screenProfile').classList.remove('active');
            document.getElementById('screenCall').classList.add('active');

            let welcomeText = "";
            if(userData.lang === 'en') {
                welcomeText = `Hello ${userData.name}! I am ${selectedTutor}, your personal AI language tutor. Let's start practicing English right now! Tell me, how was your day?`;
            } else if(userData.lang === 'fr') {
                welcomeText = `Bonjour ${userData.name}! Je suis ${selectedTutor}, votre professeur. Commençons à parler français. Comment s'est passée votre journée?`;
            } else {
                welcomeText = `¡Hola ${userData.name}! Soy ${selectedTutor}, tu profesor. ¡Empecemos a conversar!`;
            }

            appendTranscript(selectedTutor, welcomeText);
            speakText(welcomeText, userData.lang);
        }

        function speakText(text, langCode) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                let utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = langCode === 'en' ? 'en-US' : langCode === 'fr' ? 'fr-FR' : 'es-ES';
                utterance.rate = 0.95; // سرعة هادئة وطبيعية للتعلم
                utterance.pitch = selectedTutor === 'Alexa' ? 1.2 : 0.8; // نبرة أعلى للإناث وأعمق للذكور

                if (systemVoices.length === 0) {
                    loadVoices();
                }

                let filtered = systemVoices.filter(v => v.lang.startsWith(langCode) || v.lang.replace('_','-').startsWith(langCode));
                
                if (filtered.length > 0) {
                    if (selectedTutor === 'Alexa') {
                        // البحث عن صوت نسائي بأسماء شائعة في المتصفحات
                        let femaleVoice = filtered.find(v => 
                            v.name.toLowerCase().includes('female') || 
                            v.name.toLowerCase().includes('zira') || 
                            v.name.toLowerCase().includes('samantha') || 
                            v.name.toLowerCase().includes('victoria') || 
                            v.name.toLowerCase().includes('karen') || 
                            v.name.toLowerCase().includes('amelie') ||
                            v.name.toLowerCase().includes('google uk english female')
                        );
                        if (femaleVoice) utterance.voice = femaleVoice;
                        else if (filtered[1]) utterance.voice = filtered[1]; // غالباً الصوت الثاني يكون نسائياً في النظام
                    } else {
                        // البحث عن صوت رجالي
                        let maleVoice = filtered.find(v => 
                            v.name.toLowerCase().includes('male') || 
                            v.name.toLowerCase().includes('david') || 
                            v.name.toLowerCase().includes('alex') || 
                            v.name.toLowerCase().includes('daniel') || 
                            v.name.toLowerCase().includes('thomas')
                        );
                        if (maleVoice) utterance.voice = maleVoice;
                        else if (filtered[0]) utterance.voice = filtered[0];
                    }
                }

                const orb = document.getElementById('aiOrb');
                orb.classList.add('speaking');
                utterance.onend = () => { orb.classList.remove('speaking'); };

                window.speechSynthesis.speak(utterance);
            }
        }

        function toggleSpeechRecognition() {
            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            if (!SpeechRecognition) {
                alert("Speech recognition is not supported on this browser.");
                return;
            }

            if (isListening) {
                if(recognition) recognition.stop();
                return;
            }

            recognition = new SpeechRecognition();
            recognition.lang = userData.lang === 'en' ? 'en-US' : userData.lang === 'fr' ? 'fr-FR' : 'es-ES';
            recognition.interimResults = false;
            recognition.maxAlternatives = 1;

            const micBtn = document.getElementById('micBtn');

            recognition.onstart = () => {
                isListening = true;
                micBtn.classList.add('listening');
                micBtn.textContent = currentAppLang === 'ar' ? 'جارِ الاستماع...' : 'Listening...';
            };

            recognition.onresult = (event) => {
                let speechResult = event.results[0][0].transcript;
                appendTranscript(userData.name, speechResult);
                processAIResponse(speechResult);
            };

            recognition.onerror = () => { stopMicUI(); };
            recognition.onend = () => { stopMicUI(); };

            recognition.start();
        }

        function stopMicUI() {
            isListening = false;
            const micBtn = document.getElementById('micBtn');
            micBtn.classList.remove('listening');
            micBtn.textContent = uiText[currentAppLang].micText;
        }

        function processAIResponse(userInput) {
            let reply = "";
            let lower = userInput.toLowerCase();

            if(userData.lang === 'en') {
                if(lower.includes('good') || lower.includes('fine') || lower.includes('great')) {
                    reply = `That's wonderful, ${userData.name}! Your pronunciation is getting better. Can you tell me what your favorite hobby is?`;
                } else {
                    reply = `I heard you say "${userInput}". Excellent effort! What else would you like to discuss today?`;
                }
            } else if(userData.lang === 'fr') {
                reply = `C'est très bien dit, ${userData.name}! Parlons de vos projets pour demain?`;
            } else {
                reply = `¡Excelente, ${userData.name}! Cuéntame más sobre lo que te gusta hacer.`;
            }

            appendTranscript(selectedTutor, reply);
            speakText(reply, userData.lang);
        }

        function appendTranscript(sender, text) {
            const transcript = document.getElementById('chatTranscript');
            if(transcript.innerHTML.includes('Establishing')) {
                transcript.innerHTML = '';
            }
            transcript.innerHTML += `<div style="margin-bottom: 8px;"><strong>${sender}:</strong> ${text}</div>`;
            transcript.scrollTop = transcript.scrollHeight;
        }

        function endCall() {
            if('speechSynthesis' in window) window.speechSynthesis.cancel();
            if(recognition) recognition.stop();
            document.getElementById('screenCall').classList.remove('active');
            document.getElementById('screenProfile').classList.add('active');
        }
    </script>
</body>
</html>
