<!DOCTYPE html>
<html lang="en" dir="ltr">
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
            padding: 25px;
            overflow-x: hidden;
        }
        .container {
            width: 100%;
            max-width: 850px;
            text-align: center;
        }
        
        /* الهيدر */
        .brand-header {
            margin-bottom: 45px;
            animation: fadeIn 0.8s ease;
        }
        .brand-header h1 {
            font-size: 2.2rem;
            letter-spacing: 8px;
            text-transform: uppercase;
            font-weight: 300;
            color: #ffffff;
            margin-bottom: 10px;
        }
        .brand-header p {
            font-size: 0.8rem;
            color: var(--text-muted);
            letter-spacing: 3px;
            text-transform: uppercase;
        }

        /* شبكة الدوائر المتوهجة */
        .matrix-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 20px;
            justify-content: center;
            animation: fadeIn 1s ease;
        }
        .matrix-node {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 35px 20px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            position: relative;
        }
        .matrix-node:hover {
            transform: translateY(-6px);
            border-color: var(--border-hover);
            box-shadow: 0 25px 50px rgba(0,0,0,0.8);
        }
        
        .core-orb {
            width: 65px;
            height: 65px;
            border-radius: 50%;
            margin: 0 auto 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4rem;
            transition: transform 0.4s ease;
        }
        .matrix-node:hover .core-orb {
            transform: scale(1.15);
        }

        .orb-cyan { background: radial-gradient(circle, var(--accent-cyan) 0%, #005f73 100%); box-shadow: 0 0 25px rgba(0, 240, 255, 0.25); }
        .orb-gold { background: radial-gradient(circle, var(--accent-gold) 0%, #ca6702 100%); box-shadow: 0 0 25px rgba(255, 183, 0, 0.25); }
        .orb-purple { background: radial-gradient(circle, var(--accent-purple) 0%, #3a0ca3 100%); box-shadow: 0 0 25px rgba(176, 0, 255, 0.25); }

        .node-title {
            font-size: 0.9rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 600;
            margin-bottom: 8px;
            color: #fff;
        }
        .node-desc {
            font-size: 0.75rem;
            color: var(--text-muted);
            line-height: 1.5;
        }

        /* مساحة العمل الديناميكية */
        .workspace {
            display: none;
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 40px;
            text-align: left;
            animation: slideUp 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards;
            box-shadow: 0 30px 60px rgba(0,0,0,0.9);
        }
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .workspace-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 15px;
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
            letter-spacing: 1px;
            transition: all 0.3s;
        }
        .return-btn:hover { color: #fff; border-color: #555; }

        .dropzone {
            border: 2px dashed var(--border);
            border-radius: 14px;
            padding: 45px 20px;
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
            padding: 15px;
            font-size: 0.8rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            font-weight: 700;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .action-submit-btn:hover { background: #e0e0e0; box-shadow: 0 0 20px rgba(255,255,255,0.15); }
    </style>
</head>
<body>

    <div class="container">
        
        <!-- الهيدر والتعريف بالمنصة -->
        <div class="brand-header" id="brandHeader">
            <h1>NeuraFrame</h1>
            <p>Advanced Neural Image Processing Matrix</p>
        </div>

        <!-- قائمة العقد (الدوائر المتوهجة) -->
        <div class="matrix-grid" id="matrixGrid">
            
            <div class="matrix-node" onclick="launchWorkspace('Background Extraction', 'Isolate complex subjects instantly with algorithmic neural edge masking.')">
                <div class="core-orb orb-cyan">✂️</div>
                <div class="node-title">BG Eraser</div>
                <div class="node-desc">Precise background removal driven by deep vision models.</div>
            </div>

            <div class="matrix-node" onclick="launchWorkspace('Neural Upscaling', 'Reconstruct fine textures and maximize output resolution to 4K.')">
                <div class="core-orb orb-gold">⚡</div>
                <div class="node-title">AI Upscale</div>
                <div class="node-desc">Enhance low-resolution assets with generative pixel interpolation.</div>
            </div>

            <div class="matrix-node" onclick="launchWorkspace('Generative Synthesis', 'Modify structural elements using natural language prompt architecture.')">
                <div class="core-orb orb-purple">🔮</div>
                <div class="node-title">AI Genesis</div>
                <div class="node-desc">Transform visual composition with contextual text guidance.</div>
            </div>

        </div>

        <!-- واجهة العمل الديناميكية المخفية -->
        <div class="workspace" id="activeWorkspace">
            <div class="workspace-top">
                <span class="workspace-name" id="activeToolTitle">Workspace</span>
                <button class="return-btn" onclick="closeWorkspace()">← Matrix</button>
            </div>
            <p id="activeToolDesc" style="font-size: 0.8rem; color: var(--text-muted); margin-bottom: 25px;"></p>
            
            <div class="dropzone" onclick="alert('Select your image asset from local storage.')">
                <div class="dropzone-text">Drop visual asset here or Click to Browse</div>
            </div>

            <button class="action-submit-btn" onclick="alert('Executing neural pipeline sequence...')">Execute Process</button>
        </div>

    </div>

    <script>
        function launchWorkspace(title, desc) {
            document.getElementById('matrixGrid').style.display = 'none';
            document.getElementById('brandHeader').style.display = 'none';
            
            document.getElementById('activeToolTitle').textContent = title;
            document.getElementById('activeToolDesc').textContent = desc;
            document.getElementById('activeWorkspace').style.display = 'block';
        }

        function closeWorkspace() {
            document.getElementById('activeWorkspace').style.display = 'none';
            document.getElementById('matrixGrid').style.display = 'grid';
            document.getElementById('brandHeader').style.display = 'block';
        }
    </script>

</body>
</html>
