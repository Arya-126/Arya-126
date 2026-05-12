<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitHub README Generator — Arya-126</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:ital,wght@0,300;0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --surface2: #21262d;
    --border: #30363d;
    --accent: #39d353;
    --accent2: #58a6ff;
    --accent3: #f78166;
    --text: #e6edf3;
    --text-muted: #8b949e;
    --text-dim: #484f58;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  /* Header */
  header {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    padding: 16px 32px;
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .header-dots { display: flex; gap: 8px; }
  .dot {
    width: 12px; height: 12px;
    border-radius: 50%;
  }
  .dot-red { background: #ff5f57; }
  .dot-yellow { background: #febc2e; }
  .dot-green { background: #28c840; }

  .header-title {
    font-family: 'Syne', sans-serif;
    font-size: 14px;
    font-weight: 700;
    color: var(--text-muted);
    margin-left: 8px;
  }

  .header-title span { color: var(--accent); }

  /* Layout */
  .app {
    display: grid;
    grid-template-columns: 420px 1fr;
    flex: 1;
    height: calc(100vh - 53px);
  }

  /* Left Panel — Steps */
  .panel-left {
    background: var(--surface);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .steps-nav {
    display: flex;
    border-bottom: 1px solid var(--border);
    overflow-x: auto;
  }

  .step-btn {
    padding: 12px 16px;
    background: transparent;
    border: none;
    border-bottom: 2px solid transparent;
    color: var(--text-muted);
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    cursor: pointer;
    white-space: nowrap;
    transition: all 0.2s;
    letter-spacing: 1px;
  }

  .step-btn.active {
    color: var(--accent);
    border-bottom-color: var(--accent);
    background: rgba(57,211,83,0.05);
  }

  .step-btn:hover:not(.active) { color: var(--text); }

  .panel-content {
    flex: 1;
    overflow-y: auto;
    padding: 24px;
  }

  .panel-content::-webkit-scrollbar { width: 4px; }
  .panel-content::-webkit-scrollbar-track { background: transparent; }
  .panel-content::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }

  /* Step panels */
  .step-panel { display: none; }
  .step-panel.active { display: block; }

  .step-title {
    font-family: 'Syne', sans-serif;
    font-size: 18px;
    font-weight: 700;
    margin-bottom: 4px;
    color: var(--text);
  }

  .step-subtitle {
    font-size: 11px;
    color: var(--text-muted);
    margin-bottom: 24px;
    letter-spacing: 1px;
  }

  /* Form elements */
  .field {
    margin-bottom: 16px;
  }

  label {
    display: block;
    font-size: 11px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 6px;
  }

  input[type="text"], textarea, select {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    padding: 10px 14px;
    outline: none;
    transition: border-color 0.2s;
    resize: vertical;
  }

  input[type="text"]:focus,
  textarea:focus,
  select:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(57,211,83,0.1);
  }

  textarea { min-height: 80px; }

  /* Tag input */
  .tag-input-container {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 8px;
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    min-height: 48px;
    cursor: text;
    transition: border-color 0.2s;
  }

  .tag-input-container:focus-within {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(57,211,83,0.1);
  }

  .tag {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: rgba(57,211,83,0.12);
    border: 1px solid rgba(57,211,83,0.3);
    color: var(--accent);
    font-size: 11px;
    padding: 3px 8px;
    border-radius: 4px;
  }

  .tag-remove {
    cursor: pointer;
    opacity: 0.6;
    font-size: 13px;
    line-height: 1;
  }
  .tag-remove:hover { opacity: 1; }

  .tag-input {
    border: none;
    background: transparent;
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    outline: none;
    flex: 1;
    min-width: 120px;
    padding: 2px 4px;
  }

  /* Quick add chips */
  .quick-chips {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-top: 8px;
  }

  .chip {
    font-size: 10px;
    padding: 3px 8px;
    border: 1px solid var(--border);
    color: var(--text-muted);
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.2s;
    background: transparent;
    font-family: 'JetBrains Mono', monospace;
  }

  .chip:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(57,211,83,0.08);
  }

  /* Toggle */
  .toggle-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid var(--border);
  }

  .toggle-label {
    font-size: 12px;
    color: var(--text);
  }

  .toggle {
    width: 40px; height: 22px;
    background: var(--border);
    border-radius: 11px;
    position: relative;
    cursor: pointer;
    transition: background 0.2s;
  }

  .toggle.on { background: var(--accent); }

  .toggle::after {
    content: '';
    position: absolute;
    width: 16px; height: 16px;
    background: white;
    border-radius: 50%;
    top: 3px; left: 3px;
    transition: transform 0.2s;
  }

  .toggle.on::after { transform: translateX(18px); }

  /* Divider */
  .divider {
    height: 1px;
    background: var(--border);
    margin: 20px 0;
  }

  /* Section heading in form */
  .form-section {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 12px;
    margin-top: 20px;
  }

  /* Nav buttons */
  .panel-footer {
    padding: 16px 24px;
    border-top: 1px solid var(--border);
    display: flex;
    gap: 10px;
    justify-content: flex-end;
  }

  .btn {
    padding: 9px 20px;
    border-radius: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    letter-spacing: 1px;
    cursor: pointer;
    border: none;
    transition: all 0.2s;
  }

  .btn-primary {
    background: var(--accent);
    color: #0d1117;
    font-weight: 600;
  }

  .btn-primary:hover { background: #4ae868; transform: translateY(-1px); }

  .btn-secondary {
    background: var(--surface2);
    color: var(--text-muted);
    border: 1px solid var(--border);
  }

  .btn-secondary:hover { color: var(--text); border-color: var(--text-muted); }

  /* Right Panel — Preview */
  .panel-right {
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .preview-header {
    padding: 12px 20px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: var(--surface);
  }

  .preview-tabs {
    display: flex;
    gap: 4px;
  }

  .preview-tab {
    padding: 6px 14px;
    border-radius: 4px;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.2s;
    border: 1px solid transparent;
    font-family: 'JetBrains Mono', monospace;
    color: var(--text-muted);
    background: transparent;
  }

  .preview-tab.active {
    background: var(--surface2);
    border-color: var(--border);
    color: var(--text);
  }

  .copy-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 7px 14px;
    background: var(--accent);
    color: #0d1117;
    border: none;
    border-radius: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    font-weight: 600;
    cursor: pointer;
    letter-spacing: 1px;
    transition: all 0.2s;
  }

  .copy-btn:hover { background: #4ae868; transform: translateY(-1px); }

  .preview-body {
    flex: 1;
    overflow-y: auto;
  }

  .preview-body::-webkit-scrollbar { width: 4px; }
  .preview-body::-webkit-scrollbar-track { background: transparent; }
  .preview-body::-webkit-scrollbar-thumb { background: var(--border); }

  /* Rendered preview */
  #rendered-view {
    padding: 32px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    font-size: 14px;
    line-height: 1.6;
    color: #e6edf3;
  }

  #rendered-view h1 { font-size: 28px; margin-bottom: 8px; }
  #rendered-view h2 { font-size: 20px; margin: 20px 0 10px; border-bottom: 1px solid var(--border); padding-bottom: 8px; }
  #rendered-view h3 { font-size: 16px; margin: 16px 0 8px; }
  #rendered-view p { margin-bottom: 12px; color: var(--text-muted); }
  #rendered-view img { max-width: 100%; }
  #rendered-view a { color: var(--accent2); text-decoration: none; }
  #rendered-view code { background: var(--surface2); padding: 2px 6px; border-radius: 4px; font-size: 12px; font-family: 'JetBrains Mono', monospace; }
  #rendered-view hr { border: none; border-top: 1px solid var(--border); margin: 20px 0; }

  .badge-row {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin: 12px 0;
  }

  .badge-row img { height: 24px; }

  /* Raw markdown view */
  #raw-view {
    display: none;
    padding: 24px;
    background: var(--bg);
    height: 100%;
  }

  #raw-view pre {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    line-height: 1.8;
    color: var(--text-muted);
    white-space: pre-wrap;
    word-break: break-word;
  }

  .md-keyword { color: #79c0ff; }
  .md-link { color: var(--accent); }
  .md-comment { color: var(--text-dim); font-style: italic; }

  /* Progress bar */
  .progress-bar {
    height: 2px;
    background: var(--border);
    position: relative;
  }

  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transition: width 0.4s ease;
  }

  /* Typing animation */
  @keyframes typing {
    from { width: 0; }
    to { width: 100%; }
  }

  @keyframes blink {
    50% { opacity: 0; }
  }

  .typing-text {
    overflow: hidden;
    white-space: nowrap;
    border-right: 2px solid var(--accent);
    animation: typing 1.5s steps(30) forwards, blink 0.7s step-end infinite;
    display: inline-block;
    max-width: 100%;
  }

  /* Stats cards in preview */
  .stats-grid {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin: 12px 0;
  }

  .stats-grid img {
    border-radius: 4px;
    height: auto;
    max-width: 48%;
  }

  /* Emoji row */
  .about-list {
    list-style: none;
    margin: 12px 0;
  }

  .about-list li {
    padding: 6px 0;
    color: var(--text-muted);
    font-size: 14px;
    display: flex;
    align-items: flex-start;
    gap: 10px;
  }

  /* Toast */
  .toast {
    position: fixed;
    bottom: 24px;
    right: 24px;
    background: var(--accent);
    color: #0d1117;
    padding: 12px 20px;
    border-radius: 8px;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 1px;
    transform: translateY(80px);
    opacity: 0;
    transition: all 0.3s ease;
    z-index: 999;
    font-family: 'JetBrains Mono', monospace;
  }

  .toast.show {
    transform: translateY(0);
    opacity: 1;
  }

  /* Color picker row */
  .color-options {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-top: 8px;
  }

  .color-opt {
    width: 28px; height: 28px;
    border-radius: 50%;
    cursor: pointer;
    border: 2px solid transparent;
    transition: all 0.2s;
  }

  .color-opt.selected,
  .color-opt:hover {
    border-color: white;
    transform: scale(1.15);
  }

  /* Select styled */
  select {
    appearance: none;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%238b949e' stroke-width='1.5' fill='none'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 36px;
  }

  @media (max-width: 900px) {
    .app { grid-template-columns: 1fr; grid-template-rows: auto 1fr; }
    .panel-left { max-height: 55vh; }
  }
</style>
</head>
<body>

<header>
  <div class="header-dots">
    <div class="dot dot-red"></div>
    <div class="dot dot-yellow"></div>
    <div class="dot dot-green"></div>
  </div>
  <div class="header-title">README.md Generator — <span>Arya-126</span></div>
</header>

<div class="app">
  <!-- Left Panel -->
  <div class="panel-left">
    <div class="progress-bar">
      <div class="progress-fill" id="progressFill" style="width: 20%"></div>
    </div>

    <div class="steps-nav">
      <button class="step-btn active" onclick="goToStep(0)">01 · Intro</button>
      <button class="step-btn" onclick="goToStep(1)">02 · About</button>
      <button class="step-btn" onclick="goToStep(2)">03 · Skills</button>
      <button class="step-btn" onclick="goToStep(3)">04 · Stats</button>
      <button class="step-btn" onclick="goToStep(4)">05 · Style</button>
    </div>

    <div class="panel-content">

      <!-- Step 1: Intro -->
      <div class="step-panel active" id="step-0">
        <div class="step-title">Hey there 👋</div>
        <div class="step-subtitle">// BASIC INFORMATION</div>

        <div class="field">
          <label>Display Name</label>
          <input type="text" id="displayName" value="Arya Y P" oninput="generate()">
        </div>

        <div class="field">
          <label>GitHub Username</label>
          <input type="text" id="username" value="Arya-126" oninput="generate()">
        </div>

        <div class="field">
          <label>Tagline / Role</label>
          <input type="text" id="tagline" value="Information Science Engineer @ BMSCE · Builder of real-time systems & AI pipelines" oninput="generate()">
        </div>

        <div class="field">
          <label>One-liner intro</label>
          <textarea id="intro" oninput="generate()">Passionate about building decentralized systems, real-time media pipelines and AI-powered products. Currently interning at Samsung Prism — crafting peer-to-peer conferencing without the cloud.</textarea>
        </div>

        <div class="field">
          <label>Location</label>
          <input type="text" id="location" value="Bengaluru, Karnataka 🇮🇳" oninput="generate()">
        </div>

        <div class="field">
          <label>Email</label>
          <input type="text" id="email" value="arya1262023@gmail.com" oninput="generate()">
        </div>

        <div class="field">
          <label>LinkedIn URL (username only)</label>
          <input type="text" id="linkedin" value="arya-y-p-508468297" oninput="generate()">
        </div>
      </div>

      <!-- Step 2: About -->
      <div class="step-panel" id="step-1">
        <div class="step-title">About Me</div>
        <div class="step-subtitle">// WHAT YOU'RE UP TO</div>

        <div class="field">
          <label>🔭 Currently working on</label>
          <input type="text" id="working" value="Project PRISM — Decentralized P2P AV conferencing @ Samsung Prism" oninput="generate()">
        </div>

        <div class="field">
          <label>🌱 Currently learning</label>
          <input type="text" id="learning" value="WebRTC internals, STUN/TURN/ICE NAT traversal, Distributed Systems" oninput="generate()">
        </div>

        <div class="field">
          <label>👯 Looking to collaborate on</label>
          <input type="text" id="collab" value="AI/ML projects, Full-stack applications, Open-source tools" oninput="generate()">
        </div>

        <div class="field">
          <label>💬 Ask me about</label>
          <input type="text" id="askme" value="Android P2P networking, H.264 encoding, YOLOv8, NLP pipelines, React" oninput="generate()">
        </div>

        <div class="field">
          <label>⚡ Fun fact</label>
          <input type="text" id="funfact" value="I debug code with the same focus I bring to a table tennis rally 🏓" oninput="generate()">
        </div>

        <div class="field">
          <label>🏆 Achievement highlight</label>
          <input type="text" id="achievement" value="Won HyperAPI Global Hackathon — detected 195/200 anomalies in 1000 pages of financial invoices" oninput="generate()">
        </div>

        <div class="field">
          <label>📚 Education</label>
          <input type="text" id="education" value="B.E. ISE @ BMSCE, Bengaluru | CGPA 9.73" oninput="generate()">
        </div>
      </div>

      <!-- Step 3: Skills -->
      <div class="step-panel" id="step-2">
        <div class="step-title">Tech Stack</div>
        <div class="step-subtitle">// YOUR SKILLS & TOOLS</div>

        <div class="form-section">Languages</div>
        <div class="field">
          <div class="tag-input-container" onclick="this.querySelector('input').focus()">
            <div id="lang-tags"></div>
            <input class="tag-input" id="lang-input" placeholder="Add language..." onkeydown="addTag(event,'lang')">
          </div>
          <div class="quick-chips">
            <button class="chip" onclick="quickAdd('lang','Python')">Python</button>
            <button class="chip" onclick="quickAdd('lang','JavaScript')">JavaScript</button>
            <button class="chip" onclick="quickAdd('lang','C++')">C++</button>
            <button class="chip" onclick="quickAdd('lang','C')">C</button>
            <button class="chip" onclick="quickAdd('lang','Kotlin')">Kotlin</button>
          </div>
        </div>

        <div class="form-section">Frameworks & Libraries</div>
        <div class="field">
          <div class="tag-input-container" onclick="this.querySelector('input').focus()">
            <div id="fw-tags"></div>
            <input class="tag-input" id="fw-input" placeholder="Add framework..." onkeydown="addTag(event,'fw')">
          </div>
          <div class="quick-chips">
            <button class="chip" onclick="quickAdd('fw','React')">React</button>
            <button class="chip" onclick="quickAdd('fw','Next.js')">Next.js</button>
            <button class="chip" onclick="quickAdd('fw','Node.js')">Node.js</button>
            <button class="chip" onclick="quickAdd('fw','TensorFlow')">TensorFlow</button>
            <button class="chip" onclick="quickAdd('fw','OpenCV')">OpenCV</button>
          </div>
        </div>

        <div class="form-section">AI / ML Tools</div>
        <div class="field">
          <div class="tag-input-container" onclick="this.querySelector('input').focus()">
            <div id="ai-tags"></div>
            <input class="tag-input" id="ai-input" placeholder="Add AI tool..." onkeydown="addTag(event,'ai')">
          </div>
          <div class="quick-chips">
            <button class="chip" onclick="quickAdd('ai','YOLOv8')">YOLOv8</button>
            <button class="chip" onclick="quickAdd('ai','HuggingFace')">HuggingFace</button>
            <button class="chip" onclick="quickAdd('ai','Scikit-learn')">Scikit-learn</button>
            <button class="chip" onclick="quickAdd('ai','MediaPipe')">MediaPipe</button>
          </div>
        </div>

        <div class="form-section">Databases</div>
        <div class="field">
          <div class="tag-input-container" onclick="this.querySelector('input').focus()">
            <div id="db-tags"></div>
            <input class="tag-input" id="db-input" placeholder="Add database..." onkeydown="addTag(event,'db')">
          </div>
          <div class="quick-chips">
            <button class="chip" onclick="quickAdd('db','PostgreSQL')">PostgreSQL</button>
            <button class="chip" onclick="quickAdd('db','MongoDB')">MongoDB</button>
            <button class="chip" onclick="quickAdd('db','MySQL')">MySQL</button>
            <button class="chip" onclick="quickAdd('db','Supabase')">Supabase</button>
          </div>
        </div>
      </div>

      <!-- Step 4: Stats -->
      <div class="step-panel" id="step-3">
        <div class="step-title">GitHub Stats</div>
        <div class="step-subtitle">// WIDGETS & BADGES</div>

        <div class="toggle-row">
          <span class="toggle-label">Show GitHub Stats Card</span>
          <div class="toggle on" id="toggle-stats" onclick="toggleFeature('stats')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show Top Languages</span>
          <div class="toggle on" id="toggle-langs" onclick="toggleFeature('langs')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show Streak Stats</span>
          <div class="toggle on" id="toggle-streak" onclick="toggleFeature('streak')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show Contribution Graph</span>
          <div class="toggle on" id="toggle-graph" onclick="toggleFeature('graph')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show Profile Views Counter</span>
          <div class="toggle on" id="toggle-views" onclick="toggleFeature('views')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show Trophies</span>
          <div class="toggle off" id="toggle-trophies" onclick="toggleFeature('trophies')"></div>
        </div>

        <div class="divider"></div>

        <div class="field">
          <label>Stats Card Theme</label>
          <select id="statsTheme" onchange="generate()">
            <option value="radical">Radical (Dark + Pink)</option>
            <option value="dark" selected>Dark</option>
            <option value="tokyonight">Tokyo Night</option>
            <option value="dracula">Dracula</option>
            <option value="nord">Nord</option>
            <option value="github_dark">GitHub Dark</option>
            <option value="onedark">One Dark</option>
          </select>
        </div>
      </div>

      <!-- Step 5: Style -->
      <div class="step-panel" id="step-4">
        <div class="step-title">Style & Extras</div>
        <div class="step-subtitle">// FINISHING TOUCHES</div>

        <div class="field">
          <label>Header Banner Style</label>
          <select id="bannerStyle" onchange="generate()">
            <option value="capsule">Capsule Header</option>
            <option value="wave" selected>Wave / Typing SVG</option>
            <option value="none">No Banner</option>
          </select>
        </div>

        <div class="field">
          <label>Typing Animation Text (comma-separated)</label>
          <input type="text" id="typingText" value="Information Science Engineer,Android Developer,AI/ML Enthusiast,Open Source Contributor" oninput="generate()">
        </div>

        <div class="field">
          <label>Footer Quote</label>
          <input type="text" id="footerQuote" value="\"Build things that matter. Debug with patience. Ship with confidence.\"" oninput="generate()">
        </div>

        <div class="toggle-row">
          <span class="toggle-label">Show Snake Animation</span>
          <div class="toggle on" id="toggle-snake" onclick="toggleFeature('snake')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show WakaTime Stats</span>
          <div class="toggle off" id="toggle-waka" onclick="toggleFeature('waka')"></div>
        </div>
        <div class="toggle-row">
          <span class="toggle-label">Show Recent Activity</span>
          <div class="toggle off" id="toggle-activity" onclick="toggleFeature('activity')"></div>
        </div>

        <div class="divider"></div>

        <div class="field">
          <label>Social Links to include</label>
          <div class="toggle-row">
            <span class="toggle-label">LinkedIn</span>
            <div class="toggle on" id="toggle-li" onclick="toggleFeature('li')"></div>
          </div>
          <div class="toggle-row">
            <span class="toggle-label">Email Badge</span>
            <div class="toggle on" id="toggle-email" onclick="toggleFeature('email')"></div>
          </div>
          <div class="toggle-row">
            <span class="toggle-label">GitHub Followers Badge</span>
            <div class="toggle on" id="toggle-followers" onclick="toggleFeature('followers')"></div>
          </div>
        </div>
      </div>

    </div><!-- end panel-content -->

    <div class="panel-footer">
      <button class="btn btn-secondary" id="prevBtn" onclick="prevStep()" style="display:none">← Prev</button>
      <button class="btn btn-primary" id="nextBtn" onclick="nextStep()">Next →</button>
    </div>
  </div>

  <!-- Right Panel — Preview -->
  <div class="panel-right">
    <div class="preview-header">
      <div class="preview-tabs">
        <button class="preview-tab active" onclick="switchView('rendered')">Preview</button>
        <button class="preview-tab" onclick="switchView('raw')">Raw Markdown</button>
      </div>
      <button class="copy-btn" onclick="copyMarkdown()">
        <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg>
        Copy README
      </button>
    </div>

    <div class="preview-body">
      <div id="rendered-view"></div>
      <div id="raw-view"><pre id="rawCode"></pre></div>
    </div>
  </div>
</div>

<div class="toast" id="toast">✓ Copied to clipboard!</div>

<script>
  // State
  let currentStep = 0;
  const totalSteps = 5;

  const features = {
    stats: true, langs: true, streak: true, graph: true,
    views: true, trophies: false, snake: true, waka: false,
    activity: false, li: true, email: true, followers: true
  };

  const tags = { lang: [], fw: [], ai: [], db: [] };

  // Pre-populate default tags
  const defaults = {
    lang: ['Python', 'JavaScript', 'C++', 'C', 'Kotlin'],
    fw: ['React', 'Next.js', 'Node.js', 'TensorFlow', 'OpenCV'],
    ai: ['YOLOv8', 'HuggingFace', 'Scikit-learn', 'MediaPipe'],
    db: ['PostgreSQL', 'MongoDB', 'MySQL', 'Supabase']
  };

  Object.keys(defaults).forEach(cat => {
    defaults[cat].forEach(t => addTagDirect(cat, t));
  });

  function addTagDirect(cat, val) {
    if (!tags[cat].includes(val)) {
      tags[cat].push(val);
      renderTags(cat);
      generate();
    }
  }

  function addTag(e, cat) {
    if (e.key === 'Enter' || e.key === ',') {
      e.preventDefault();
      const input = document.getElementById(cat + '-input');
      const val = input.value.trim().replace(',', '');
      if (val && !tags[cat].includes(val)) {
        tags[cat].push(val);
        renderTags(cat);
        generate();
      }
      input.value = '';
    }
  }

  function quickAdd(cat, val) {
    addTagDirect(cat, val);
  }

  function removeTag(cat, val) {
    tags[cat] = tags[cat].filter(t => t !== val);
    renderTags(cat);
    generate();
  }

  function renderTags(cat) {
    const container = document.getElementById(cat + '-tags');
    container.innerHTML = tags[cat].map(t =>
      `<span class="tag">${t}<span class="tag-remove" onclick="removeTag('${cat}','${t}')">×</span></span>`
    ).join('');
  }

  function toggleFeature(key) {
    features[key] = !features[key];
    const el = document.getElementById('toggle-' + key);
    el.classList.toggle('on', features[key]);
    el.classList.toggle('off', !features[key]);
    generate();
  }

  function goToStep(n) {
    document.querySelectorAll('.step-panel').forEach((p, i) => {
      p.classList.toggle('active', i === n);
    });
    document.querySelectorAll('.step-btn').forEach((b, i) => {
      b.classList.toggle('active', i === n);
    });
    currentStep = n;
    document.getElementById('prevBtn').style.display = n === 0 ? 'none' : 'block';
    document.getElementById('nextBtn').textContent = n === totalSteps - 1 ? '✓ Done' : 'Next →';
    document.getElementById('progressFill').style.width = ((n + 1) / totalSteps * 100) + '%';
  }

  function nextStep() {
    if (currentStep < totalSteps - 1) goToStep(currentStep + 1);
  }

  function prevStep() {
    if (currentStep > 0) goToStep(currentStep - 1);
  }

  function g(id) { return document.getElementById(id)?.value || ''; }

  function getShieldsBadge(label, color, logo, url) {
    const badge = `https://img.shields.io/badge/${encodeURIComponent(label)}-${color}?style=for-the-badge&logo=${logo}&logoColor=white`;
    return url ? `[![${label}](${badge})](${url})` : `![${label}](${badge})`;
  }

  function getSkillBadge(name) {
    const map = {
      'Python': ['Python', '3776AB', 'python'],
      'JavaScript': ['JavaScript', 'F7DF1E', 'javascript', '000'],
      'C++': ['C++', '00599C', 'cplusplus'],
      'C': ['C', 'A8B9CC', 'c'],
      'Kotlin': ['Kotlin', '7F52FF', 'kotlin'],
      'React': ['React', '61DAFB', 'react', '000'],
      'Next.js': ['Next.js', '000000', 'nextdotjs'],
      'Node.js': ['Node.js', '339933', 'nodedotjs'],
      'TensorFlow': ['TensorFlow', 'FF6F00', 'tensorflow'],
      'OpenCV': ['OpenCV', '5C3EE8', 'opencv'],
      'YOLOv8': ['YOLOv8', '00FFFF', 'yolo', '000'],
      'HuggingFace': ['HuggingFace', 'FFD21E', 'huggingface', '000'],
      'Scikit-learn': ['Scikit--learn', 'F7931E', 'scikitlearn', '000'],
      'MediaPipe': ['MediaPipe', '0097A7', 'google'],
      'PostgreSQL': ['PostgreSQL', '4169E1', 'postgresql'],
      'MongoDB': ['MongoDB', '47A248', 'mongodb'],
      'MySQL': ['MySQL', '4479A1', 'mysql'],
      'Supabase': ['Supabase', '3ECF8E', 'supabase'],
    };
    const m = map[name];
    if (m) {
      const logoColor = m[3] || 'white';
      return `![${m[0]}](https://img.shields.io/badge/${encodeURIComponent(m[0])}-${m[1]}?style=flat-square&logo=${m[2]}&logoColor=${logoColor})`;
    }
    return `![${name}](https://img.shields.io/badge/${encodeURIComponent(name)}-555555?style=flat-square)`;
  }

  function generateMarkdown() {
    const username = g('username') || 'Arya-126';
    const name = g('displayName') || 'Arya Y P';
    const tagline = g('tagline');
    const intro = g('intro');
    const location = g('location');
    const email = g('email');
    const linkedin = g('linkedin');
    const working = g('working');
    const learning = g('learning');
    const collab = g('collab');
    const askme = g('askme');
    const funfact = g('funfact');
    const achievement = g('achievement');
    const education = g('education');
    const statsTheme = g('statsTheme') || 'dark';
    const typingTexts = g('typingText').split(',').map(s => encodeURIComponent(s.trim())).join(';');
    const footerQuote = g('footerQuote');
    const bannerStyle = g('bannerStyle');

    let md = '';

    // Banner / Header
    if (bannerStyle === 'wave') {
      md += `<div align="center">\n\n`;
      md += `[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=28&pause=1000&color=39D353&center=true&vCenter=true&width=700&lines=${typingTexts})](https://git.io/typing-svg)\n\n`;
    } else if (bannerStyle === 'capsule') {
      md += `<div align="center">\n\n`;
      md += `![header](https://capsule-render.vercel.app/api?type=waving&color=39D353&height=200&section=header&text=${encodeURIComponent(name)}&fontSize=40&fontColor=fff&animation=fadeIn)\n\n`;
    } else {
      md += `<div align="center">\n\n`;
    }

    // Title & views
    if (features.views) {
      md += `![Profile Views](https://komarev.com/ghpvc/?username=${username}&color=39d353&style=flat-square&label=Profile+Views)\n\n`;
    }

    if (features.followers) {
      md += `[![GitHub followers](https://img.shields.io/github/followers/${username}?label=Followers&style=social)](https://github.com/${username})\n\n`;
    }

    md += `# Hi there, I'm ${name} 👋\n\n`;
    md += `### ${tagline}\n\n`;
    md += `</div>\n\n`;

    md += `---\n\n`;

    // About
    md += `## 🙋‍♂️ About Me\n\n`;
    md += `${intro}\n\n`;
    md += `- 🔭 I'm currently working on **${working}**\n`;
    md += `- 🌱 I'm currently learning **${learning}**\n`;
    md += `- 👯 I'm looking to collaborate on **${collab}**\n`;
    md += `- 💬 Ask me about **${askme}**\n`;
    md += `- 📍 Based in **${location}**\n`;
    md += `- 🎓 **${education}**\n`;
    md += `- 🏆 ${achievement}\n`;
    md += `- ⚡ Fun fact: ${funfact}\n\n`;

    // Connect
    md += `## 🔗 Connect with Me\n\n`;
    md += `<div align="left">\n\n`;
    if (features.li) {
      md += `[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/${linkedin})\n`;
    }
    md += `[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/${username})\n`;
    if (features.email && email) {
      md += `[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:${email})\n`;
    }
    md += `\n</div>\n\n`;

    // Skills
    md += `## 🛠️ Tech Stack\n\n`;

    if (tags.lang.length > 0) {
      md += `**Languages:**\n\n`;
      md += tags.lang.map(t => getSkillBadge(t)).join(' ') + '\n\n';
    }
    if (tags.fw.length > 0) {
      md += `**Frameworks & Libraries:**\n\n`;
      md += tags.fw.map(t => getSkillBadge(t)).join(' ') + '\n\n';
    }
    if (tags.ai.length > 0) {
      md += `**AI / ML:**\n\n`;
      md += tags.ai.map(t => getSkillBadge(t)).join(' ') + '\n\n';
    }
    if (tags.db.length > 0) {
      md += `**Databases:**\n\n`;
      md += tags.db.map(t => getSkillBadge(t)).join(' ') + '\n\n';
    }

    // Stats
    md += `## 📊 GitHub Stats\n\n`;
    md += `<div align="center">\n\n`;

    if (features.stats) {
      md += `![${name}'s GitHub Stats](https://github-readme-stats.vercel.app/api?username=${username}&show_icons=true&theme=${statsTheme}&hide_border=true&count_private=true)\n\n`;
    }
    if (features.langs) {
      md += `![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=${username}&layout=compact&theme=${statsTheme}&hide_border=true)\n\n`;
    }
    if (features.streak) {
      md += `[![GitHub Streak](https://streak-stats.demolab.com?user=${username}&theme=${statsTheme}&hide_border=true)](https://git.io/streak-stats)\n\n`;
    }
    if (features.graph) {
      md += `![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=${username}&theme=github-compact&hide_border=true)\n\n`;
    }
    if (features.trophies) {
      md += `[![Trophies](https://github-profile-trophy.vercel.app/?username=${username}&theme=darkhub&no-frame=true&margin-w=4)](https://github.com/${username})\n\n`;
    }

    md += `</div>\n\n`;

    // Snake
    if (features.snake) {
      md += `## 🐍 Contribution Snake\n\n`;
      md += `<div align="center">\n\n`;
      md += `![Snake animation](https://github.com/${username}/${username}/blob/output/github-contribution-grid-snake-dark.svg)\n\n`;
      md += `</div>\n\n`;
      md += `> ⚙️ To enable the snake, add a GitHub Action in \`.github/workflows/snake.yml\`\n\n`;
    }

    // Footer
    md += `---\n\n`;
    md += `<div align="center">\n\n`;
    md += `*${footerQuote}*\n\n`;
    md += `![Wave](https://capsule-render.vercel.app/api?type=waving&color=39D353&height=100&section=footer)\n\n`;
    md += `</div>\n`;

    return md;
  }

  function renderPreview(md) {
    const username = g('username') || 'Arya-126';
    const name = g('displayName') || 'Arya Y P';
    const statsTheme = g('statsTheme') || 'dark';
    const typingTexts = g('typingText').split(',').map(s => encodeURIComponent(s.trim())).join(';');

    let html = '';

    // Header
    html += `<div style="text-align:center;margin-bottom:24px;">`;

    if (g('bannerStyle') === 'wave') {
      html += `<img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=22&pause=1000&color=39D353&center=true&vCenter=true&width=600&lines=${typingTexts}" alt="Typing SVG" style="max-width:100%;margin-bottom:16px;display:block;margin:0 auto 16px;"><br>`;
    } else if (g('bannerStyle') === 'capsule') {
      html += `<img src="https://capsule-render.vercel.app/api?type=waving&color=39D353&height=150&section=header&text=${encodeURIComponent(name)}&fontSize=32&fontColor=fff&animation=fadeIn" style="width:100%;border-radius:8px;margin-bottom:16px;"><br>`;
    }

    if (features.views) {
      html += `<img src="https://komarev.com/ghpvc/?username=${username}&color=39d353&style=flat-square&label=Profile+Views" style="margin:4px;"> `;
    }
    if (features.followers) {
      html += `<img src="https://img.shields.io/github/followers/${username}?label=Followers&style=social" style="margin:4px;">`;
    }

    html += `<h1 style="margin-top:16px;">Hi there, I'm ${g('displayName')} 👋</h1>`;
    html += `<p style="color:#8b949e;font-size:15px;">${g('tagline')}</p>`;
    html += `</div><hr>`;

    // About
    html += `<h2>🙋‍♂️ About Me</h2>`;
    html += `<p>${g('intro')}</p>`;
    html += `<ul class="about-list">`;
    const items = [
      ['🔭', 'Currently working on', 'working'],
      ['🌱', 'Currently learning', 'learning'],
      ['👯', 'Looking to collaborate on', 'collab'],
      ['💬', 'Ask me about', 'askme'],
      ['📍', 'Based in', 'location'],
      ['🎓', '', 'education'],
      ['🏆', '', 'achievement'],
      ['⚡', 'Fun fact', 'funfact'],
    ];
    items.forEach(([emoji, label, id]) => {
      const val = g(id);
      if (val) html += `<li><span>${emoji}</span><span>${label ? `<strong>${label}:</strong> ` : ''}${val}</span></li>`;
    });
    html += `</ul><hr>`;

    // Connect
    html += `<h2>🔗 Connect with Me</h2><div class="badge-row">`;
    if (features.li) html += `<a href="https://linkedin.com/in/${g('linkedin')}"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"></a>`;
    html += `<a href="https://github.com/${username}"><img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"></a>`;
    if (features.email && g('email')) html += `<a href="mailto:${g('email')}"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"></a>`;
    html += `</div><hr>`;

    // Skills
    html += `<h2>🛠️ Tech Stack</h2>`;
    if (tags.lang.length > 0) {
      html += `<p><strong>Languages:</strong></p><div class="badge-row">`;
      tags.lang.forEach(t => html += `<img src="https://img.shields.io/badge/${encodeURIComponent(t)}-555?style=flat-square&logo=${t.toLowerCase().replace('.','').replace('+','p').replace(' ','')}">` );
      html += `</div>`;
    }
    if (tags.fw.length > 0) {
      html += `<p><strong>Frameworks & Libraries:</strong></p><div class="badge-row">`;
      tags.fw.forEach(t => html += `<img src="https://img.shields.io/badge/${encodeURIComponent(t)}-333?style=flat-square">` );
      html += `</div>`;
    }
    if (tags.ai.length > 0) {
      html += `<p><strong>AI / ML:</strong></p><div class="badge-row">`;
      tags.ai.forEach(t => html += `<img src="https://img.shields.io/badge/${encodeURIComponent(t)}-0d1117?style=flat-square&color=39d353">` );
      html += `</div>`;
    }
    if (tags.db.length > 0) {
      html += `<p><strong>Databases:</strong></p><div class="badge-row">`;
      tags.db.forEach(t => html += `<img src="https://img.shields.io/badge/${encodeURIComponent(t)}-4479A1?style=flat-square">` );
      html += `</div>`;
    }
    html += `<hr>`;

    // Stats
    html += `<h2>📊 GitHub Stats</h2><div class="stats-grid">`;
    if (features.stats) html += `<img src="https://github-readme-stats.vercel.app/api?username=${username}&show_icons=true&theme=${statsTheme}&hide_border=true&count_private=true" style="max-width:48%;">`;
    if (features.langs) html += `<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=${username}&layout=compact&theme=${statsTheme}&hide_border=true" style="max-width:48%;">`;
    html += `</div>`;
    if (features.streak) html += `<div style="margin:8px 0;"><img src="https://streak-stats.demolab.com?user=${username}&theme=${statsTheme}&hide_border=true" style="max-width:100%;border-radius:4px;"></div>`;
    if (features.graph) html += `<div style="margin:8px 0;"><img src="https://github-readme-activity-graph.vercel.app/graph?username=${username}&theme=github-compact&hide_border=true" style="max-width:100%;border-radius:4px;"></div>`;
    html += `<hr>`;

    // Footer
    html += `<div style="text-align:center;color:#8b949e;font-style:italic;padding:16px 0;">${g('footerQuote')}</div>`;
    html += `<img src="https://capsule-render.vercel.app/api?type=waving&color=39D353&height=80&section=footer" style="width:100%;">`;

    document.getElementById('rendered-view').innerHTML = html;
  }

  function generate() {
    const md = generateMarkdown();
    renderPreview(md);
    // Syntax highlight raw
    const raw = document.getElementById('rawCode');
    raw.textContent = md;
  }

  function switchView(view) {
    document.querySelectorAll('.preview-tab').forEach((t, i) => {
      t.classList.toggle('active', (i === 0 && view === 'rendered') || (i === 1 && view === 'raw'));
    });
    document.getElementById('rendered-view').style.display = view === 'rendered' ? 'block' : 'none';
    document.getElementById('raw-view').style.display = view === 'raw' ? 'block' : 'none';
  }

  function copyMarkdown() {
    const md = generateMarkdown();
    navigator.clipboard.writeText(md).then(() => {
      const toast = document.getElementById('toast');
      toast.classList.add('show');
      setTimeout(() => toast.classList.remove('show'), 2500);
    });
  }

  // Init
  generate();
</script>
</body>
</html>
