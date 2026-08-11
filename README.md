<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Vault</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background-color: #050505;
            color: #e5e5e5;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }
        .container {
            width: 100%;
            max-width: 420px;
            padding: 30px;
            text-align: center;
        }
        h1 {
            font-size: 1.2rem;
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-bottom: 30px;
            color: #ffffff;
            font-weight: 300;
        }
        textarea {
            width: 100%;
            height: 140px;
            background: #0f0f0f;
            border: 1px solid #222;
            border-radius: 4px;
            color: #fff;
            padding: 15px;
            font-size: 0.95rem;
            resize: none;
            outline: none;
            transition: border-color 0.3s;
        }
        textarea:focus {
            border-color: #555;
        }
        button {
            width: 100%;
            margin-top: 20px;
            background: #ffffff;
            color: #050505;
            border: none;
            padding: 12px;
            font-size: 0.9rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 600;
            border-radius: 4px;
            cursor: pointer;
            transition: opacity 0.3s;
        }
        button:hover {
            opacity: 0.85;
        }
        .vault-box {
            display: none;
            margin-top: 20px;
            text-align: left;
            max-height: 200px;
            overflow-y: auto;
            background: #0a0a0a;
            border: 1px solid #1a1a1a;
            padding: 15px;
            border-radius: 4px;
        }
        .secret-item {
            font-size: 0.85rem;
            color: #a0a0a0;
            border-bottom: 1px solid #141414;
            padding: 10px 0;
        }
        .secret-item:last-child {
            border-bottom: none;
        }
        .hint {
            margin-top: 15px;
            font-size: 0.75rem;
            color: #666;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>The Vault</h1>
        <div id="input-section">
            <textarea id="secretInput" placeholder="Write your secret to unlock the global vault..."></textarea>
            <button onclick="revealVault()">Commit Secret</button>
            <div class="hint">Absolute confidentiality. No names. No traces.</div>
        </div>

        <div id="vault-section" class="vault-box">
            <div class="secret-item">"I pretend to be confident, but every night I fear I will fail everyone who looks up to me."</div>
            <div class="secret-item">"We built a fortune from a broken device while everyone else was sleeping."</div>
            <div class="secret-item">"The biggest secret is that no one actually knows what they are doing; we just adapt faster."</div>
        </div>
    </div>

    <script>
        function revealVault() {
            const input = document.getElementById('secretInput').value;
            if(input.trim().length < 5) {
                alert('Please write a genuine secret to proceed.');
                return;
            }
            document.getElementById('input-section').style.display = 'none';
            document.getElementById('vault-section').style.display = 'block';
        }
    </script>

</body>
</html>
