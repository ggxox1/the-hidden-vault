<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Vault | Anonymous Network</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background-color: #030303;
            color: #f0f0f0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            padding: 20px;
        }
        .container {
            width: 100%;
            max-width: 500px;
        }
        .profile-bar {
            background: #0a0a0a;
            border: 1px solid #1f1f1f;
            padding: 12px 18px;
            border-radius: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            font-size: 0.85rem;
        }
        .profile-bar span { color: #888; }
        .profile-bar strong { color: #fff; cursor: pointer; }
        
        .post-card, .feed-card {
            background: #0a0a0a;
            border: 1px solid #1f1f1f;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        textarea {
            width: 100%;
            height: 100px;
            background: #121212;
            border: 1px solid #262626;
            border-radius: 8px;
            color: #fff;
            padding: 12px;
            font-size: 0.95rem;
            resize: none;
            outline: none;
            margin-bottom: 12px;
        }
        button.primary-btn {
            width: 100%;
            background: #f5f5f5;
            color: #0a0a0a;
            border: none;
            padding: 12px;
            font-size: 0.8rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 700;
            border-radius: 8px;
            cursor: pointer;
        }
        .feed-header {
            display: flex;
            justify-content: space-between;
            font-size: 0.8rem;
            color: #777;
            margin-bottom: 10px;
        }
        .feed-author { color: #ccc; font-weight: 600; }
        .feed-text {
            font-size: 0.95rem;
            line-height: 1.5;
            color: #e0e0e0;
            margin-bottom: 15px;
            word-break: break-word;
        }
        .feed-actions {
            display: flex;
            gap: 20px;
            font-size: 0.85rem;
            color: #888;
            border-top: 1px solid #161616;
            padding-top: 12px;
        }
        .action-btn {
            background: none;
            border: none;
            color: #888;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 0.85rem;
        }
        .action-btn:hover { color: #fff; }
        .comments-section {
            margin-top: 12px;
            border-top: 1px dashed #1a1a1a;
            padding-top: 10px;
            display: none;
        }
        .comment-item {
            font-size: 0.8rem;
            color: #aaa;
            background: #111;
            padding: 8px 10px;
            border-radius: 6px;
            margin-bottom: 6px;
        }
        .comment-input-box {
            display: flex;
            gap: 8px;
            margin-top: 8px;
        }
        .comment-input-box input {
            flex: 1;
            background: #111;
            border: 1px solid #222;
            border-radius: 6px;
            padding: 8px;
            color: #fff;
            font-size: 0.8rem;
            outline: none;
        }
        .comment-input-box button {
            background: #333;
            color: #fff;
            border: none;
            padding: 0 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.8rem;
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- شريط الملف الشخصي والاسم المستعار -->
        <div class="profile-bar">
            <span>Alias: <strong id="currentAlias" onclick="changeAlias()">Anonymous</strong></span>
            <span style="font-size: 0.75rem; color: #555;">Click alias to edit</span>
        </div>

        <!-- صندوق نشر السر -->
        <div class="post-card">
            <textarea id="secretInput" placeholder="Broadcast your secret to the network..."></textarea>
            <button class="primary-btn" onclick="publishSecret()">Publish Secret</button>
        </div>

        <!-- قائمة الأسرار المنشورة (Timeline) -->
        <div id="feedContainer"></div>
    </div>

    <script>
        let alias = localStorage.getItem('vault_alias') || 'Shadow_' + Math.floor(Math.random() * 9000 + 1000);
        document.getElementById('currentAlias').textContent = alias;

        let posts = JSON.parse(localStorage.getItem('vault_posts')) || [
            {
                id: 1,
                author: "Agent_07",
                text: "I was a lead engineer for a state-sponsored cyber unit. In 2023, we successfully embedded an untraceable kill-switch into the firmware of the global banking infrastructure.",
                likes: 14,
                comments: [{author: "System_X", text: "This explains a lot about the recent outages."}]
            },
            {
                id: 2,
                author: "Ghost_Writer",
                text: "Everyone thinks I am working hard to build a successful future, but the dark truth is I am doing this purely out of spite.",
                likes: 29,
                comments: []
            }
        ];

        function changeAlias() {
            let newAlias = prompt("Enter your new pseudonymous alias:", alias);
            if(newAlias && newAlias.trim().length > 0) {
                alias = newAlias.trim();
                localStorage.setItem('vault_alias', alias);
                document.getElementById('currentAlias').textContent = alias;
            }
        }

        function saveAndRender() {
            localStorage.setItem('vault_posts', JSON.stringify(posts));
            renderFeed();
        }

        function publishSecret() {
            const text = document.getElementById('secretInput').value.trim();
            if(text.length < 3) {
                alert('Secret is too short.');
                return;
            }
            const newPost = {
                id: Date.now(),
                author: alias,
                text: text,
                likes: 0,
                comments: []
            };
            posts.unshift(newPost);
            document.getElementById('secretInput').value = '';
            saveAndRender();
        }

        function likePost(id) {
            const post = posts.find(p => p.id === id);
            if(post) {
                post.likes++;
                saveAndRender();
            }
        }

        function toggleComments(id) {
            const box = document.getElementById('comments-' + id);
            box.style.display = box.style.display === 'block' ? 'none' : 'block';
        }

        function addComment(id) {
            const input = document.getElementById('comment-input-' + id);
            const text = input.value.trim();
            if(!text) return;
            const post = posts.find(p => p.id === id);
            if(post) {
                post.comments.push({ author: alias, text: text });
                input.value = '';
                saveAndRender();
                document.getElementById('comments-' + id).style.display = 'block';
            }
        }

        function renderFeed() {
            const container = document.getElementById('feedContainer');
            container.innerHTML = '';
            
            posts.forEach(post => {
                let commentsHtml = '';
                post.comments.forEach(c => {
                    commentsHtml += `<div class="comment-item"><strong>@${c.author}:</strong> ${c.text}</div>`;
                });

                const card = document.createElement('div');
                card.className = 'feed-card';
                card.innerHTML = `
                    <div class="feed-header">
                        <span class="feed-author">@${post.author}</span>
                        <span>Encrypted</span>
                    </div>
                    <div class="feed-text">"${post.text}"</div>
                    <div class="feed-actions">
                        <button class="action-btn" onclick="likePost(${post.id})">❤️ ${post.likes}</button>
                        <button class="action-btn" onclick="toggleComments(${post.id})">💬 ${post.comments.length} Comments</button>
                    </div>
                    <div id="comments-${post.id}" class="comments-section">
                        ${commentsHtml}
                        <div class="comment-input-box">
                            <input type="text" id="comment-input-${post.id}" placeholder="Reply anonymously...">
                            <button onclick="addComment(${post.id})">Send</button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        renderFeed();
    </script>
</body>
</html>
