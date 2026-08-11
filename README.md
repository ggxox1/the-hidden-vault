<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Vault</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background-color: #030303;
            color: #f0f0f0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .vault-card {
            width: 100%;
            max-width: 440px;
            background: #0a0a0a;
            border: 1px solid #1f1f1f;
            border-radius: 12px;
            padding: 35px 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.8);
        }
        .header {
            text-align: center;
            margin-bottom: 30px;
        }
        h1 {
            font-size: 1.1rem;
            letter-spacing: 5px;
            text-transform: uppercase;
            color: #ffffff;
            font-weight: 400;
            margin-bottom: 8px;
        }
        .subtitle {
            font-size: 0.8rem;
            color: #777;
            letter-spacing: 1px;
        }
        textarea {
            width: 100%;
            height: 130px;
            background: #121212;
            border: 1px solid #262626;
            border-radius: 8px;
            color: #fff;
            padding: 15px;
            font-size: 0.95rem;
            resize: none;
            outline: none;
        }
        button {
            width: 100%;
            margin-top: 20px;
            background: #f5f5f5;
            color: #0a0a0a;
            border: none;
            padding: 14px;
            font-size: 0.85rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            font-weight: 700;
            border-radius: 8px;
            cursor: pointer;
        }
        .vault-box {
            display: none;
            margin-top: 20px;
            background: #0f0f0f;
            border: 1px solid #222;
            padding: 15px;
            border-radius: 8px;
            max-height: 250px;
            overflow-y: auto;
        }
        .secret-item {
            font-size: 0.85rem;
            color: #b0b0b0;
            border-bottom: 1px solid #1a1a1a;
            padding: 12px 0;
            line-height: 1.4;
        }
        .security-note {
            margin-top: 20px;
            text-align: center;
            font-size: 0.72rem;
            color: #555;
            letter-spacing: 1px;
            text-transform: uppercase;
        }
        .back-btn {
            display: block;
            text-align: center;
            margin-top: 15px;
            font-size: 0.75rem;
            color: #666;
            cursor: pointer;
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <div class="vault-card">
        <div class="header">
            <h1>The Vault</h1>
            <div class="subtitle">Encrypted Anonymous Transmission</div>
        </div>

        <div id="input-section">
            <textarea id="secretInput" placeholder="Deposit your secret into the network..."></textarea>
            <button id="commitBtn" type="button">Commit Secret</button>
            <div class="security-note">End-to-End Anonymity • Zero Traces</div>
        </div>

        <div id="vault-section" class="vault-box">
            <div id="secretsList"></div>
            <a class="back-btn" id="backBtn">← Deposit another secret</a>
        </div>
    </div>

    <script>
        let secrets = JSON.parse(localStorage.getItem('vault_secrets')) || [
            "I was a lead engineer for a state-sponsored cyber unit. In 2023, we successfully embedded an untraceable kill-switch into the firmware of the global banking infrastructure.",
            "Everyone thinks I am working hard to build a successful future, but the dark truth is I am doing this purely out of spite, just to prove every single person who abandoned me that they were worthless."
        ];

        function renderSecrets() {
            const listContainer = document.getElementById('secretsList');
            listContainer.innerHTML = '';
            secrets.forEach(function(secret) {
                const div = document.createElement('div');
                div.className = 'secret-item';
                div.textContent = '"' + secret + '"';
                listContainer.appendChild(div);
            });
        }

        document.getElementById('commitBtn').addEventListener('click', function() {
            const input = document.getElementById('secretInput');
            const val = input.value.trim();
            if(val.length < 3) {
                alert('Please enter a secret first.');
                return;
            }
            secrets.unshift(val);
            localStorage.setItem('vault_secrets', JSON.stringify(secrets));
            input.value = '';
            renderSecrets();
            document.getElementById('input-section').style.display = 'none';
            document.getElementById('vault-section').style.display = 'block';
        });

        document.getElementById('backBtn').addEventListener('click', function() {
            document.getElementById('vault-section').style.display = 'none';
            document.getElementById('input-section').style.display = 'block';
        });

        renderSecrets();
    </script>

</body>
</html>
