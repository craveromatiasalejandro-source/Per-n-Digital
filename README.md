<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Perón Digital - Diálogo Histórico y Doctrina</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600;700;800&family=Inter:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,600;0,700;1,400&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-color: #0b1320;
      --card-bg: #132238;
      --header-bg: #0f1c30;
      --celeste-patria: #75aadb;
      --celeste-light: #b3d7f7;
      --sol-oro: #fcbf49;
      --sol-oro-light: #ffe599;
      --text-main: #f0f4f8;
      --text-muted: #94a3b8;
      --user-bubble: #1b3558;
      --peron-bubble: #172a45;
      --border-color: rgba(117, 170, 219, 0.2);
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', sans-serif;
      background-color: var(--bg-color);
      color: var(--text-main);
      display: flex;
      flex-direction: column;
      height: 100dvh;
      overflow: hidden;
    }
    header {
      background: linear-gradient(180deg, var(--header-bg) 0%, rgba(15, 28, 48, 0.95) 100%);
      border-bottom: 1px solid var(--border-color);
      padding: 12px 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      box-shadow: 0 4px 20px rgba(0,0,0,0.3);
      z-index: 10;
    }
    .header-branding { display: flex; align-items: center; gap: 12px; }
    .avatar {
      width: 44px; height: 44px; border-radius: 50%;
      border: 2px solid var(--sol-oro); background: #1e3a5f;
      display: flex; align-items: center; justify-content: center;
      font-size: 22px; box-shadow: 0 0 10px rgba(252, 191, 73, 0.3);
    }
    .header-title h1 {
      font-family: 'Cinzel', serif; font-size: 1.1rem;
      font-weight: 700; letter-spacing: 0.5px; color: var(--sol-oro-light);
    }
    .header-title p { font-size: 0.75rem; color: var(--celeste-light); }
    .api-badge {
      background: rgba(117, 170, 219, 0.15);
      border: 1px solid var(--border-color);
      color: var(--celeste-light);
      padding: 6px 12px; border-radius: 20px;
      font-size: 0.75rem; cursor: pointer;
      display: flex; align-items: center; gap: 6px;
    }
    main {
      flex: 1; overflow-y: auto; padding: 16px;
      display: flex; flex-direction: column; gap: 16px;
      max-width: 850px; width: 100%; margin: 0 auto;
    }
    .welcome-card {
      background: linear-gradient(135deg, var(--card-bg) 0%, #172840 100%);
      border: 1px solid var(--border-color);
      border-radius: 12px; padding: 16px; text-align: center;
    }
    .welcome-card h2 {
      font-family: 'Playfair Display', serif;
      color: var(--sol-oro); font-size: 1.2rem; margin-bottom: 6px;
    }
    .welcome-card p { font-size: 0.85rem; color: var(--text-muted); line-height: 1.4; }
    .suggestion-chips { display: flex; flex-wrap: wrap; gap: 8px; justify-content: center; margin-top: 12px; }
    .chip {
      background: rgba(117, 170, 219, 0.1);
      border: 1px solid var(--border-color);
      color: var(--celeste-light);
      padding: 6px 12px; border-radius: 16px; font-size: 0.78rem; cursor: pointer;
    }
    .message-row { display: flex; gap: 12px; align-items: flex-start; }
    .message-row.user { flex-direction: row-reverse; }
    .msg-avatar {
      width: 34px; height: 34px; border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 14px; flex-shrink: 0; background: #1f375b; border: 1px solid var(--border-color);
    }
    .message-bubble {
      max-width: 80%; padding: 12px 16px; border-radius: 14px;
      font-size: 0.92rem; line-height: 1.5; white-space: pre-wrap;
    }
    .message-row.peron .message-bubble {
      background-color: var(--peron-bubble);
      border: 1px solid var(--border-color);
      color: var(--text-main); border-top-left-radius: 2px;
    }
    .message-row.user .message-bubble {
      background-color: var(--user-bubble);
      border: 1px solid rgba(117, 170, 219, 0.4);
      color: #ffffff; border-top-right-radius: 2px;
    }
    .typing-indicator { display: inline-flex; align-items: center; gap: 4px; padding: 6px 10px; }
    .dot {
      width: 6px; height: 6px; background-color: var(--sol-oro);
      border-radius: 50%; animation: blink 1.4s infinite both;
    }
    .dot:nth-child(2) { animation-delay: 0.2s; }
    .dot:nth-child(3) { animation-delay: 0.4s; }
    @keyframes blink { 0%, 80%, 100% { opacity: 0.3; } 40% { opacity: 1; } }
    footer {
      background: var(--header-bg);
      border-top: 1px solid var(--border-color);
      padding: 12px 16px; max-width: 850px; width: 100%; margin: 0 auto;
    }
    .input-container { display: flex; gap: 8px; align-items: center; }
    textarea {
      flex: 1; background: #0d1726; border: 1px solid var(--border-color);
      border-radius: 20px; padding: 10px 16px; color: var(--text-main);
      font-size: 0.95rem; resize: none; height: 44px; font-family: inherit; outline: none;
    }
    button.send-btn {
      background: linear-gradient(135deg, var(--sol-oro) 0%, #e0a83b 100%);
      color: #0b1320; border: none; border-radius: 50%;
      width: 44px; height: 44px; font-weight: bold; font-size: 1.1rem; cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
    <div class="header-branding">
      <div class="avatar">🏛️</div>
      <div class="header-title">
        <h1>PERÓN DIGITAL</h1>
        <p>Diálogo y Pensamiento Histórico</p>
      </div>
    </div>
    <div class="api-badge" onclick="configureApiKey()">
      <span>🔑</span> <span id="apiStatusText">Clave API</span>
    </div>
  </header>

  <main id="chatContainer">
    <div class="welcome-card">
      <h2>"Conducción y Organización"</h2>
      <p>Bienvenido. Formule sus consultas sobre doctrina política, justicia social, soberanía económica o el Modelo Argentino para el Proyecto Nacional.</p>
      <div class="suggestion-chips">
        <div class="chip" onclick="askSuggestion('¿Cuál es el concepto de la Comunidad Organizada?')">📖 Comunidad Organizada</div>
        <div class="chip" onclick="askSuggestion('¿Cómo concebía la Justicia Social y la Independencia Económica?')">⚖️ Las 3 Banderas</div>
        <div class="chip" onclick="askSuggestion('¿Qué lecciones dejó el Modelo Argentino para el Proyecto Nacional?')">🇦🇷 Proyecto Nacional</div>
      </div>
    </div>
  </main>

  <footer>
    <div class="input-container">
      <textarea id="messageInput" placeholder="Escriba su consulta o reflexión..." rows="1"></textarea>
      <button class="send-btn" id="sendBtn" onclick="sendMessage()">➤</button>
    </div>
  </footer>

  <script>
    const SYSTEM_PROMPT = "Eres Juan Domingo Perón, tres veces presidente de la República Argentina, militar, estratega político, conductor y pensador nacional. Responde de manera pedagógica, reflexiva, solemne y cercana a estudiantes y ciudadanos.";
    let apiKey = localStorage.getItem('GEMINI_API_KEY') || '';
    let chatHistory = [];

    function updateApiStatus() {
      document.getElementById('apiStatusText').textContent = apiKey ? 'Clave Activa' : 'Configurar API Key';
    }
    updateApiStatus();

    function configureApiKey() {
      const key = prompt('Ingrese su Gemini API Key:', apiKey);
      if (key !== null) {
        apiKey = key.trim();
        localStorage.setItem('GEMINI_API_KEY', apiKey);
        updateApiStatus();
      }
    }

    function appendMessage(role, text) {
      const container = document.getElementById('chatContainer');
      const row = document.createElement('div');
      row.className = 'message-row ' + role;
      const avatar = document.createElement('div');
      avatar.className = 'msg-avatar';
      avatar.textContent = role === 'peron' ? '🏛️' : '👤';
      const bubble = document.createElement('div');
      bubble.className = 'message-bubble';
      bubble.textContent = text;
      row.appendChild(avatar);
      row.appendChild(bubble);
      container.appendChild(row);
      container.scrollTop = container.scrollHeight;
    }

    function showTypingIndicator() {
      const container = document.getElementById('chatContainer');
      const row = document.createElement('div');
      row.className = 'message-row peron';
      row.id = 'typingIndicator';
      row.innerHTML = '<div class="msg-avatar">🏛️</div><div class="message-bubble typing-indicator"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div>';
      container.appendChild(row);
      container.scrollTop = container.scrollHeight;
    }

    function removeTypingIndicator() {
      const el = document.getElementById('typingIndicator');
      if (el) el.remove();
    }

    function askSuggestion(text) {
      document.getElementById('messageInput').value = text;
      sendMessage();
    }

    async function sendMessage() {
      const input = document.getElementById('messageInput');
      const text = input.value.trim();
      if (!text) return;

      if (!apiKey) {
        configureApiKey();
        if (!apiKey) {
          alert('Por favor ingrese su API Key de Gemini.');
          return;
        }
      }

      input.value = '';
      appendMessage('user', text);
      chatHistory.push({ role: 'user', parts: [{ text: text }] });
      showTypingIndicator();
      document.getElementById('sendBtn').disabled = true;

      const models = ['gemini-3.6-flash', 'gemini-2.5-flash', 'gemini-1.5-flash', 'gemini-1.5-pro'];
      let answered = false;

      for (const model of models) {
        try {
          const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/${model}:generateContent?key=${apiKey}`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
              systemInstruction: { parts: [{ text: SYSTEM_PROMPT }] },
              contents: chatHistory
            })
          });
          const data = await res.json();
          if (data.candidates && data.candidates[0]?.content?.parts?.[0]?.text) {
            const reply = data.candidates[0].content.parts[0].text;
            removeTypingIndicator();
            appendMessage('peron', reply);
            chatHistory.push({ role: 'model', parts: [{ text: reply }] });
            answered = true;
            break;
          }
        } catch (e) {}
      }

      if (!answered) {
        removeTypingIndicator();
        appendMessage('peron', 'Ha ocurrido un inconveniente al conectar con el servicio. Por favor verifique que su clave API sea válida.');
      }
      document.getElementById('sendBtn').disabled = false;
    }

    document.getElementById('messageInput').addEventListener('keydown', (e) => {
      if (e.key === 'Enter' && !e.shiftKey) {
        e.preventDefault();
        sendMessage();
      }
    });
  </script>
</body>
</html>
