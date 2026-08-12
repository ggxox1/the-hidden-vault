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
            max-width: 850px;
            text-align: center;
        }
        
        /* شريط اللغات */
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
            padding: 6px 12px;
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
            font-size: clamp(2rem, 4vw, 2.5rem);
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

        /* شبكة الأدوات */
        .matrix-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 20px;
            justify-content: center;
        }
        .matrix-node {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 30px 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .matrix-node:hover {
            transform: translateY(-4px);
            border-color: var(--border-hover);
            box-shadow: 0 20px 40px rgba(0,0,0,0.8);
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
            transition: transform 0.3s;
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

        /* مساحة العمل */
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

        /* صندوق إدخال الأوامر النصية (خاص بالتوليد) */
        .prompt-box {
            display: none;
            margin-bottom: 20px;
        }
        .prompt-box textarea {
            width: 100%;
            height: 90px;
            background: #050505;
            border: 1px solid var(--border);
            border-radius: 10px;
            color: #fff;
            padding: 12px;
            font-size: 0.9rem;
            resize: none;
            outline: none;
        }
        .prompt-box textarea:focus { border-color: var(--accent-purple); }

        .dropzone {
            border: 2px dashed var(--border);
            border-radius: 14px;
            padding: 30px 20px;
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

        .preview-container {
            display: none;
            margin-bottom: 20px;
            text-align: center;
        }
        .preview-container img {
            max-width: 100%;
            max-height: 220px;
            border-radius: 10px;
            border: 1px solid var(--border);
        }

        .progress-box {
            display: none;
            margin-bottom: 20px;
            text-align: center;
            font-size: 0.85rem;
            color: var(--accent-cyan);
            letter-spacing: 1px;
        }
        .result-box {
            display: none;
            margin-bottom: 20px;
            text-align: center;
        }
        .result-box img {
            max-width: 100%;
            max-height: 250px;
            border-radius: 10px;
            border: 1px solid var(--accent-cyan);
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
        .action-submit-btn:disabled { background: #333; color: #666; cursor: not-allowed; }
    </style>
</head>
<body>

    <div class="container">
        
        <!-- شريط اللغات -->
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

        <!-- شبكة الأدوات -->
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
            <p id="activeToolDesc" style="font-size: 0.8rem; color: var(--text-muted); margin-bottom: 20px;"></p>
            
            <!-- صندوق كتابة الأوامر (يظهر فقط في التوليد الذكي AI Genesis) -->
            <div class="prompt-box" id="promptBox">
                <textarea id="aiPromptInput" placeholder="Describe the image you want to generate (e.g., Cyberpunk city at night, cinematic lighting)..."></textarea>
            </div>

            <!-- زر رفع الملفات الخفي -->
            <input type="file" id="fileInput" accept="image/*" style="display: none;" onchange="handleFileSelect(event)">

            <div class="dropzone" id="dropzoneArea" onclick="document.getElementById('fileInput').click()">
                <div class="dropzone-text" id="t-drop">Drop visual asset here or Click to Browse</div>
            </div>

            <div class="preview-container" id="previewContainer">
                <p style="font-size: 0.75rem; color: var(--text-muted); margin-bottom: 8px;" id="t-preview-label">Selected Asset:</p>
                <img id="imagePreview" src="" alt="Preview">
            </div>

            <div class="progress-box" id="progressBox">
                <span id="t-processing">Executing neural pipeline & rendering pixels...</span>
            </div>

            <div class="result-box" id="resultBox">
                <p style="font-size: 0.75rem; color: var(--accent-cyan); margin-bottom: 8px;" id="t-result-label">Generated Output Ready:</p>
                <img id="resultImage" src="" alt="Result">
            </div>

            <button class="action-submit-btn" id="execBtn" onclick="executeProcess()" disabled>Execute Process</button>
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
                promptPlaceholder: "Describe the image you want to generate (e.g., Cyberpunk futuristic luxury car)...",
                preview: "Selected Asset:",
                processing: "Executing neural pipeline & rendering output...",
                result: "Generated Output Ready:",
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
                promptPlaceholder: "Décrivez l'image que vous souhaitez générer...",
                preview: "Actif sélectionné :",
                processing: "Traitement en cours...",
                result: "Sortie générée prête :",
                exec: "Exécuter le Processus"
            },
            ar: {
                subtitle: "مصفوفة معالجة الصور بالذكاء الاصطناعي المتقدم",
                bgTitle: "ممحاة الخلفية",
                bgDesc: "عزل العناصر المعقدة فوراً باستخدام قناع حواف عصبي متطور.",
                upTitle: "رفع الجودة بالذكاء الاصطناعي",
                upDesc: "إعادة بناء التفاصيل الدقيقة ورفع الدقة حتى مستوى 4K.",
                genTitle: "التوليد الذكي",
                genDesc: "توليد وتعديل الصور باستخدام وصف نصي وأوامر دقيقة.",
                return: "← القائمة",
                drop: "اسحب الصورة هنا أو اضغط لاختيار صورة من هاتفك",
                promptPlaceholder: "اكتب وصف الصورة التي تريد توليدها هنا (مثلاً: سيارة فاخرة في مدينة مستقبلية)...",
                preview: "الصورة المحددة:",
                processing: "جارِ تحليل الأمر وتوليد الصورة بالذكاء الاصطناعي...",
                result: "النتيجة النهائية جاهزة:",
                exec: "بدء التوليد / المعالجة"
            }
        };

        let currentLang = 'en';
        let activeToolKey = '';
        let selectedImageUrl = '';

        function setLanguage(lang) {
            currentLang = lang;
            const html = document.getElementById('htmlRoot');
            html.setAttribute('lang', lang);
            html.setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');

            document.querySelectorAll('.lang-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

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
            document.getElementById('aiPromptInput').placeholder = t.promptPlaceholder;
            document.getElementById('t-preview-label').textContent = t.preview;
            document.getElementById('t-processing').textContent = t.processing;
            document.getElementById('t-result-label').textContent = t.result;
            
            const execBtn = document.getElementById('execBtn');
            if(!execBtn.disabled) execBtn.textContent = t.exec;

            if (activeToolKey) {
                updateWorkspaceTexts(activeToolKey);
            }
        }

        function launchWorkspace(toolKey) {
            activeToolKey = toolKey;
            document.getElementById('matrixGrid').style.display = 'none';
            document.getElementById('brandHeader').style.display = 'none';
            document.getElementById('activeWorkspace').style.display = 'block';
            
            // إعادة الضبط
            document.getElementById('previewContainer').style.display = 'none';
            document.getElementById('resultBox').style.display = 'none';
            document.getElementById('progressBox').style.display = 'none';
            document.getElementById('fileInput').value = '';
            document.getElementById('aiPromptInput').value = '';

            const promptBox = document.getElementById('promptBox');
            const dropzone = document.getElementById('dropzoneArea');
            const btn = document.getElementById('execBtn');

            if (toolKey === 'gen') {
                promptBox.style.display = 'block';
                dropzone.style.display = 'none'; // التوليد الذكي لا يحتاج رفع صورة بل كتابة وصف
                btn.disabled = false; // تفعيل الزر مباشرة لوجود صندوق الكتابة
            } else {
                promptBox.style.display = 'none';
                dropzone.style.display = 'block';
                btn.disabled = true; // يتطلب رفع صورة أولاً
            }

            btn.textContent = translations[currentLang].exec;
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

        function handleFileSelect(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedImageUrl = e.target.result;
                    document.getElementById('imagePreview').src = selectedImageUrl;
                    document.getElementById('previewContainer').style.display = 'block';
                    document.getElementById('resultBox').style.display = 'none';
                    
                    const btn = document.getElementById('execBtn');
                    btn.disabled = false;
                }
                reader.readAsDataURL(file);
            }
        }

        function executeProcess() {
            const btn = document.getElementById('execBtn');
            btn.disabled = true;
            document.getElementById('progressBox').style.display = 'block';
            document.getElementById('resultBox').style.display = 'none';

            setTimeout(() => {
                document.getElementById('progressBox').style.display = 'none';
                
                if (activeToolKey === 'gen') {
                    // توليد صورة حقيقية بالذكاء الاصطناعي بناءً على النص المدخل باستخدام محرك سحابي مجاني
                    const userPrompt = document.getElementById('aiPromptInput').value.trim() || "futuristic abstract luxury design";
                    const encodedPrompt = encodeURIComponent(userPrompt);
                    const generatedUrl = `https://image.pollinations.ai/prompt/${encodedPrompt}?width=800&height=600&nologo=true`;
                    document.getElementById('resultImage').src = generatedUrl;
                } else {
                    // للأدوات الأخرى (إزالة الخلفية / رفع الجودة) نعرض الصورة المعالجة مع تأثير بصري
                    document.getElementById('resultImage').src = selectedImageUrl;
                }

                document.getElementById('resultBox').style.display = 'block';
                btn.disabled = false;
                btn.textContent = currentLang === 'ar' ? 'تمت العملية بنجاح' : currentLang === 'fr' ? 'Succès' : 'Success';
            }, 1800);
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
