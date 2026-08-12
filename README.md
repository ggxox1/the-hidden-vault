<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OmniAI Pro - منصة تحويل المحتوى الذكية</title>
    <style>
        :root {
            --bg-main: #18181b;
            --bg-card: #27272a;
            --bg-input: #09090b;
            --accent: #d97706;
            --accent-hover: #b45309;
            --text-main: #f4f4f5;
            --text-muted: #a1a1aa;
            --border: #3f3f46;
            --success: #22c55e;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            border-bottom: 1px solid var(--border);
            padding: 1.2rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: rgba(24, 24, 27, 0.8);
            backdrop-filter: blur(8px);
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .logo {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--accent);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .badge {
            background-color: rgba(217, 119, 6, 0.15);
            color: var(--accent);
            border: 1px solid var(--accent);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
        }

        .container {
            max-width: 800px;
            margin: 2.5rem auto;
            padding: 0 1.2rem;
            width: 100%;
            flex: 1;
        }

        .hero {
            text-align: center;
            margin-bottom: 2.5rem;
        }

        .hero h1 {
            font-size: 2.2rem;
            margin-bottom: 0.8rem;
            font-weight: 800;
            letter-spacing: -0.5px;
        }

        .hero p {
            color: var(--text-muted);
            font-size: 1.05rem;
            line-height: 1.6;
        }

        .app-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 2rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5);
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        label {
            display: block;
            margin-bottom: 0.6rem;
            font-weight: 600;
            font-size: 0.95rem;
        }

        select, textarea {
            width: 100%;
            padding: 0.9rem;
            background-color: var(--bg-input);
            border: 1px solid var(--border);
            border-radius: 10px;
            color: var(--text-main);
            font-size: 1rem;
            outline: none;
            transition: border-color 0.2s;
        }

        select:focus, textarea:focus {
            border-color: var(--accent);
        }

        textarea {
            height: 140px;
            resize: vertical;
            line-height: 1.5;
        }

        .btn-generate {
            width: 100%;
            padding: 1rem;
            background-color: var(--accent);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }

        .btn-generate:hover {
            background-color: var(--accent-hover);
            transform: translateY(-1px);
        }

        .result-box {
            margin-top: 2rem;
            padding: 1.2rem;
            background-color: var(--bg-input);
            border: 1px solid var(--border);
            border-radius: 10px;
            display: none;
            animation: fadeIn 0.3s ease-in-out;
        }

        .result-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.8rem;
            padding-bottom: 0.5rem;
            border-bottom: 1px solid var(--border);
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        .btn-copy {
            background: transparent;
            border: 1px solid var(--border);
            color: var(--text-main);
            padding: 5px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.85rem;
            transition: all 0.2s;
        }

        .btn-copy:hover {
            border-color: var(--accent);
            color: var(--accent);
        }

        .result-content {
            white-space: pre-wrap;
            line-height: 1.7;
            font-size: 1rem;
        }

        footer {
            text-align: center;
            padding: 1.5rem;
            border-top: 1px solid var(--border);
            color: var(--text-muted);
            font-size: 0.85rem;
            margin-top: auto;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @media (max-width: 600px) {
            .hero h1 { font-size: 1.7rem; }
            .app-card { padding: 1.2rem; }
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">⚡ OmniAI Pro</div>
        <div class="badge" id="creditCount">المتبقي: 5 محاولات مجانية</div>
    </header>

    <div class="container">
        <div class="hero">
            <h1>فكرة واحدة.. محتوى شامل لكافة المنصات</h1>
            <p>أداة الذكاء الاصطناعي الأسرع لصناع المحتوى، المسوقين، وأصحاب الأعمال</p>
        </div>

        <div class="app-card">
            <div class="form-group">
                <label for="contentType">1. اختر نوع المحتوى المطلوب إنشاءه:</label>
                <select id="contentType">
                    <option value="linkedin">منشور احترافي لـ LinkedIn</option>
                    <option value="twitter">سلسلة تغريدات (Twitter/X Thread)</option>
                    <option value="email">بريد إلكتروني تسويقي للعملاء</option>
                    <option value="product">وصف منتج لـ متجر إلكتروني (SEO)</option>
                </select>
            </div>

            <div class="form-group">
                <label for="userInput">2. أدخل الفكرة أو النص الأساسي:</label>
                <textarea id="userInput" placeholder="مثال: أثر استخدام أجهزة الذكاء الاصطناعي في تحسين الإنتاجية والتسويق الرقمي..."></textarea>
            </div>

            <button class="btn-generate" onclick="generateContent()">
                <span>توليد المحتوى بذكاء</span> ✨
            </button>

            <div id="resultBox" class="result-box">
                <div class="result-header">
                    <span>النتيجة جاهزة للنشر:</span>
                    <button class="btn-copy" onclick="copyResult()" id="copyBtn">📋 نسخ النص</button>
                </div>
                <div class="result-content" id="resultText"></div>
            </div>
        </div>
    </div>

    <footer>
        جميع الحقوق محفوظة © 2026 OmniAI Engine • مصممة للعمل على كافة الأجهزة
    </footer>

    <script>
        let credits = 5;

        function generateContent() {
            const input = document.getElementById('userInput').value.trim();
            const type = document.getElementById('contentType').value;
            const resultBox = document.getElementById('resultBox');
            const resultText = document.getElementById('resultText');
            const creditBadge = document.getElementById('creditCount');

            if (!input) {
                alert('الرجاء كتابة الفكرة أو النص الأولية أولاً!');
                return;
            }

            if (credits <= 0) {
                alert('لقد استنفدت رصيد المحاولات المجانية لهذا اليوم!');
                return;
            }

            resultBox.style.display = 'block';
            resultText.innerText = 'جاري التفكير وصياغة المحتوى بأفضل أسلوب... ⏳';

            // محاكاة توليد الذكاء الاصطناعي (يمكن ربطها مستقبلاً بـ API حقيقي)
            setTimeout(() => {
                let generatedOutput = "";

                if (type === 'linkedin') {
                    generatedOutput = `💡 **رؤية في مجال الأعمال:**\n\n${input}\n\n📌 **أهم 3 نقاط رئيسية:**\n1. مواكبة التقنيات الحديثة يختصر 50% من الوقت.\n2. التركيز على جودة القيمة المتقدمة للعميل.\n3. التطوير المستمر هو أصل الاستدامة.\n\nهل تتفق مع هذه الرؤية؟ شاركنا رأيك في التعليقات! 👇\n\n#أعمال #ذكاء_اصطناعي #ريادة_الأعمال #تطوير`;
                } else if (type === 'twitter') {
                    generatedOutput = `🧵 [سلسلة تغريدات]\n\n1/4 حول موضوع: ${input}\nإليكم الخلاصة بأبسط صورة 👇\n\n2/4 البداية دائماً تبدأ من فهم المشكلة بشكل دقيق وتحديد الأدوات المناسبة للحل.\n\n3/4 التطبيق العملي يمنحك التغذية الراجعة السريعة للتطوير.\n\n4/4 إن أعجبك Thread لا تنسَ إعادت تغريده لتعم الفائدة 🔄`;
                } else if (type === 'email') {
                    generatedOutput = `الموضوع: فرصة مميزة للنمو والتطوير 🚀\n\nأهلاً بك،\n\nنود أن نشاركك اليوم فكرة قد تحدث فارقاً حقيقياً في عملك:\n\n"${input}"\n\nإذا كنت ترغب في معرفة كيف يمكنك تطبيق ذلك خطوة بخطوة، يسعدنا تواصلك معنا مباشرة.\n\nتحياتنا،\nفريق العمل`;
                } else if (type === 'product') {
                    generatedOutput = `🌟 **الخيار الأمثل لاحتياجاتك!**\n\nاحصل على أفضل تجربة مع المنتج المصمم خصيصاً ليمنحك التفوق.\n\n🔹 **المميزات:**\n- ${input}\n- جودة عالية وضمان متكامل.\n- سهولة في الاستخدام والتطبيق.\n\n🛒 **اطلبه الآن واستفد من العرض الخصم المتاح لفترة محدودة!**`;
                }

                resultText.innerText = generatedOutput;
                credits--;
                creditBadge.innerText = `المتبقي: ${credits} محاولات مجانية`;
            }, 1200);
        }

        function copyResult() {
            const text = document.getElementById('resultText').innerText;
            const copyBtn = document.getElementById('copyBtn');

            if (!text || text.includes('جاري التفكير')) return;

            navigator.clipboard.writeText(text).then(() => {
                copyBtn.innerText = '✅ تم النسخ!';
                copyBtn.style.color = 'var(--success)';
                setTimeout(() => {
                    copyBtn.innerText = '📋 نسخ النص';
                    copyBtn.style.color = 'var(--text-main)';
                }, 2000);
            });
        }
    </script>
</body>
</html>
