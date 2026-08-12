<!DOCTYPE html>
<html lang="en" dir="ltr" id="htmlRoot">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NeuraFrame // AI Visual Matrix</title>
    <style>
        :root {
            --bg: #030303;
            --card-bg: #080808;
            --border: #181818;
            --border-hover: #333333;
            --text-main: #f0f0f0;
            --text-muted: #666666;
            --accent-cyan: #00f0ff;
            --accent-gold: #ffb700;
            --accent-purple: #b000ff;
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
            max-width: 900px;
            text-align: center;
        }
        
        /* شريط تغيير اللغات */
        .lang-bar {
            display: flex;
            justify-content: flex-end;
            gap: 8px;
            margin-bottom: 20px;
        }
        .lang-btn {
            background: var(--card-bg);
            border: 1px solid var(--border);
            color: var(--text-muted);
            padding: 5px 12px;
            border-radius: 6px;
            font-size: 0.75rem;
            cursor: pointer;
            transition: all 0.3s;
        }
        .lang-btn:hover, .lang-btn.active {
            color: #fff;
            border-color: #555;
            background: #111;
        }

        /* الهيدر */
        .brand-header {
            margin-bottom: 35px;
        }
        .brand-header h1 {
            font-size: clamp(1.8rem, 4vw, 2.5rem);
            letter-spacing: 6px;
            text-transform: uppercase;
            font-weight: 300;
            color: #ffffff;
            margin-bottom: 8px;
        }
        .brand-header p {
            font-size: clamp(0.75rem, 2vw, 0.85rem);
            color: var(--text-muted);
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        /* شبكة الدوائر المتوهجة */
        .matrix-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            justify-content: center;
        }
        .matrix-node {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 30px 20px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .matrix-node:hover {
            transform: translateY(-5px);
            border-color: var(--border-hover);
            box-shadow: 0 25px 50px rgba(0,0,0,0.8);
        }
        
        .core-orb {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.3rem;
            transition: transform 0.4s ease;
        }
        .matrix-node:hover .core-orb { transform: scale(1.1); }

        .orb-cyan { background: radial-gradient(circle, var(--accent-cyan) 0%, #005f73 100%); box-shadow: 0 0 20px rgba(0, 240, 255, 0.25); }
        .orb-gold { background: radial-gradient(circle, var(--accent-gold) 0%, #ca6702 100%); box-shadow: 0 0 20px rgba(255, 183, 0, 0.25); }
        .orb-purple { background: radial-gradient(circle, var(--accent-purple) 0%, #3a0ca3 100%); box-shadow: 0 0 20px rgba(176, 0, 255, 0.25); }

        .node-title {
            font-size: 0.9rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 600;
            margin-bottom: 8px;
            color: #fff;
        }
        .node-desc {
            font-size: 0.78rem;
            color: var(--text-muted);
            line-height: 1.5;
        }

        /* مساحة العمل الديناميكية */
        .workspace {
            display: none;
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 30px;
            text-align: start;
            box-shadow: 0 30px 60px rgba(0,0,0,0.9);
        }
        .workspace-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 12px;
        }
        .workspace-name {
            font-size: 0.95rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: #fff;
        }
        .return-btn {
            background: none;
            border: 1px solid var(--border);
            color: var(--text-muted);
            padding: 6px 14px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.75rem;
            transition: all 0.3s;
        }
        .return-btn:hover { color: #fff; border-color: #555; }

        .dropzone {
            border: 2px dashed var(--border);
            border-radius: 14px;
            padding: 40px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 20px;
            background: #050505;
        }
        .dropzone:hover { border-color: #444; background: #070707; }
        .dropzone-text {
            font-size: 0.85rem;
            color: var(--text-muted);
            letter-spacing: 1px;
        }

        .action-submit-btn {
            width: 100%;
            background: #ffffff;
            color: #030303;
            border: none;
            padding: 14px;
            font-size: 0.8rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            font-weight: 700;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .action-submit-btn:hover { background: #e0e0e0; }
    </style>
</head>
<body>

    <div class="container">
        
        <!-- شريط تغيير اللغة -->
        <div class="lang-bar">
            <button class="lang-btn active" onclick="setLanguage('en')">EN</button>
            <button class="lang-btn" onclick="setLanguage('fr')">FR</button>
            <button class="lang-btn" onclick="setLanguage('ar')">AR</button>
        </div>

        <!-- الهيدر -->
        <div class="brand-header" id="brandHeader">
            <h1 id="t-brand">NeuraFrame</h1>
            <p id="t-subtitle">Advanced Neural Image Processing Matrix</p>
        </div>

        <!-- الشبكة الرئيسية -->
        <div class="matrix-grid" id="matrixGrid">
            <div class="matrix-node" onclick="launchWorkspace('bg')">
                <div class="core-orb orb-cyan">✂️</div>
                <div class="node-title" id="t-bg-title">BG Eraser</div>
                <div class="node-desc" id="t-bg-desc">Isolate complex subjects instantly with algorithmic neural edge masking.</div>
            </div>

            <div class="matrix-node" onclick="launchWorkspace('upscale')">
                <div class="core-orb orb-gold">⚡</div>
                <div class="node-title" id="t-up-title">AI Upscale</div>
                <div class="node-desc" id="t-up-desc">Reconstruct fine textures and maximize output resolution to 4K.</div>
            </div>

            <div class="matrix-node" onclick="launchWorkspace('gen')">
                <div class="core-orb orb-purple">🔮</div>
                <div class="node-title" id="t-gen-title">AI Genesis</div>
                <div class="node-desc" id="t-gen-desc">Transform visual composition with contextual text guidance.</div>
            </div>
        </div>

        <!-- مساحة العمل -->
        <div class="workspace" id="activeWorkspace">
            <div class="workspace-top">
                <span class="workspace-name" id="activeToolTitle">Workspace</span>
                <button class="return-btn" onclick="closeWorkspace()" id="t-return">← Matrix</button>
            </div>
            <p id="activeToolDesc" style="font-size: 0.8rem; color: var(--text-muted); margin-bottom: 25px;"></p>
            
            <div class="dropzone" onclick="alert(currentLang === 'ar' ? 'اختر صورة من جهازك.' : currentLang === 'fr' ? 'Sélectionnez une image.' : 'Select image asset.')">
                <div class="dropzone-text" id="t-drop">Drop visual asset here or Click to Browse</div>
            </div>

            <button class="action-submit-btn" onclick="alert(currentLang === 'ar' ? 'جارِ تنفيذ المعالجة...' : currentLang === 'fr' ? 'Exécution en cours...' : 'Executing neural pipeline...')" id="t-exec">Execute Process</button>
        </div>

    </div>

    <script>
        const translations = {
            en: {
                subtitle: "Advanced Neural Image Processing Matrix",
                bgTitle: "BG Eraser",
                bgDesc: "Isolate complex subjects instantly with algorithmic neural edge masking.",
                upTitle: "AI Upscale",
                upDesc: "Reconstruct fine textures and maximize output resolution to 4K.",
                genTitle: "AI Genesis",
                genDesc: "Transform visual composition with contextual text guidance.",
                return: "← Matrix",
                drop: "Drop visual asset here or Click to Browse",
                exec: "Execute Process"
            },
            fr: {
                subtitle: "Matrice de Traitement d'Images Neurale Avancée",
                bgTitle: "Gomme Arrière-plan",
                bgDesc: "Isolez des sujets complexes instantanément avec un masquage neuronal.",
                upTitle: "Mise à l'échelle IA",
                upDesc: "Reconstruisez les textures fines et maximisez la résolution en 4K.",
                genTitle: "Genèse IA",
                genDesc: "Transformez la composition visuelle avec des instructions textuelles.",
                return: "← Matrice",
                drop: "Déposez l'élément ici ou cliquez pour parcourir",
                exec: "Exécuter le Processus"
            },
            ar: {
                subtitle: "مصفوفة معالجة الصور بالذكاء الاصطناعي المتقدم",
                bgTitle: "ممحاة الخلفية",
                bgDesc: "عزل العناصر المعقدة فوراً باستخدام قناع حواف عصبي متطور.",
                upTitle: "رفع الجودة بالذكاء الاصطناعي",
                upDesc: "إعادة بناء التفاصيل الدقيقة ورفع الدقة حتى مستوى 4K.",
                genTitle: "التوليد الذكي",
                genDesc: "تحويل التكوين البصري باستخدام توجيهات النصوص والسياق.",
                return: "← القائمة",
                drop: "اسحب الصورة هنا أو اضغط للاستعراض من جهازك",
                exec: "بدء المعالجة"
            }
        };

        let currentLang = 'en';
        let activeToolKey = '';

        function setLanguage(lang) {
            currentLang = lang;
            const html = document.getElementById('htmlRoot');
            html.setAttribute('lang', lang);
            html.setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');

            // تحديث الأزرار النشطة
            document.querySelectorAll('.lang-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            // تطبيق النصوص
            const t = translations[lang];
            document.getElementById('t-subtitle').textContent = t.subtitle;
            document.getElementById('t-bg-title').textContent = t.bgTitle;
            document.getElementById('t-bg-desc').textContent = t.bgDesc;
            document.getElementById('t-up-title').textContent = t.upTitle;
            document.getElementById('t-up-desc').textContent = t.upDesc;
            document.getElementById('t-gen-title').textContent = t.genTitle;
            document.getElementById('t-gen-desc').textContent = t.genDesc;
            document.getElementById('t-return').textContent = t.return;
            document.getElementById('t-drop').textContent = t.drop;
            document.getElementById('t-exec').textContent = t.exec;

            if (activeToolKey) {
                updateWorkspaceTexts(activeToolKey);
            }
        }

        function launchWorkspace(toolKey) {
            activeToolKey = toolKey;
            document.getElementById('matrixGrid').style.display = 'none';
            document.getElementById('brandHeader').style.display = 'none';
            document.getElementById('activeWorkspace').style.display = 'block';
            updateWorkspaceTexts(toolKey);
        }

        function updateWorkspaceTexts(key) {
            const t = translations[currentLang];
            if (key === 'bg') {
                document.getElementById('activeToolTitle').textContent = t.bgTitle;
                document.getElementById('activeToolDesc').textContent = t.bgDesc;
            } else if (key === 'upscale') {
                document.getElementById('activeToolTitle').textContent = t.upTitle;
                document.getElementById('activeToolDesc').textContent = t.upDesc;
            } else if (key === 'gen') {
                document.getElementById('activeToolTitle').textContent = t.genTitle;
                document.getElementById('activeToolDesc').textContent = t.genDesc;
            }
        }

        function closeWorkspace() {
            activeToolKey = '';
            document.getElementById('activeWorkspace').style.display = 'none';
            document.getElementById('matrixGrid').style.display = 'grid';
            document.getElementById('brandHeader').style.display = 'block';
        }
    </script>
</body>
</html>
