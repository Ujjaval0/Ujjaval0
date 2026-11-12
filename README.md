<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitHub README Visual Previewer</title>
<style>
  :root {
    --gh-bg: #0d1117;
    --gh-border: #30363d;
    --gh-text: #e6edf3;
    --gh-muted: #8b949e;
    --gh-blue: #58a6ff;
  }
  * { box-sizing: border-box; }
  body {
    margin: 0;
    padding: 16px;
    background-color: #010409;
    color: var(--gh-text);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Noto Sans", Helvetica, Arial, sans-serif;
  }
  /* Control Bar */
  .controls {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 16px;
    background: #161b22;
    padding: 12px;
    border-radius: 8px;
    border: 1px solid var(--gh-border);
    align-items: center;
    justify-content: space-between;
  }
  .tabs {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }
  .tab-btn {
    background: #21262d;
    color: var(--gh-text);
    border: 1px solid var(--gh-border);
    padding: 8px 14px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 13px;
    font-weight: 600;
    transition: all 0.2s;
  }
  .tab-btn:hover { background: #30363d; }
  .tab-btn.active {
    background: #1f6feb;
    border-color: #388bfd;
    color: #fff;
  }
  .toggle-group {
    display: flex;
    gap: 12px;
    font-size: 13px;
    color: var(--gh-muted);
    align-items: center;
  }
  .toggle-group label {
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 5px;
    color: var(--gh-text);
  }

  /* GitHub README Container Simulation */
  .gh-container {
    background-color: var(--gh-bg);
    border: 1px solid var(--gh-border);
    border-radius: 6px;
    padding: 24px 32px;
    max-width: 900px;
    margin: 0 auto;
    box-shadow: 0 8px 24px rgba(0,0,0,0.5);
  }
  .gh-file-header {
    font-family: monospace;
    font-size: 12px;
    color: var(--gh-muted);
    margin-bottom: 16px;
    padding-bottom: 12px;
    border-bottom: 1px solid #21262d;
    display: flex;
    justify-content: space-between;
  }

  /* Hero Banner Styles */
  .banner-wrapper {
    width: 100%;
    overflow: hidden;
    border-radius: 8px;
    position: relative;
    margin-bottom: 16px;
  }

  /* Option 1: Animated Wave */
  .hero-wave {
    background: linear-gradient(90deg, #0d1117 0%, #161b22 45%, #1f6feb 100%);
    height: 175px;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  .hero-wave h1 {
    margin: 0;
    font-size: 34px;
    color: #fff;
    z-index: 2;
    letter-spacing: -0.5px;
  }
  .hero-wave p {
    margin: 8px 0 24px 0;
    font-size: 14px;
    color: #a5d6ff;
    z-index: 2;
    font-weight: 500;
  }
  .wave-svg {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 200%;
    height: 55px;
    animation: waveMove 8s linear infinite;
  }
  @keyframes waveMove {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }

  /* Option 2: Cyber Grid / Dark Tech Texture */
  .hero-grid {
    background-color: #090d16;
    background-image: 
      linear-gradient(rgba(88, 166, 255, 0.08) 1px, transparent 1px),
      linear-gradient(90deg, rgba(88, 166, 255, 0.08) 1px, transparent 1px),
      radial-gradient(circle at 50% 50%, rgba(31, 111, 235, 0.25), transparent 70%);
    background-size: 24px 24px, 24px 24px, 100% 100%;
    border: 1px solid #1f6feb55;
    height: 165px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
  }
  .hero-grid h1 {
    margin: 0;
    font-size: 34px;
    background: linear-gradient(90deg, #ffffff, #58a6ff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .hero-grid p {
    margin: 8px 0 0 0;
    font-size: 14px;
    color: #8b949e;
    font-family: monospace;
  }

  /* Option 3: Soft Venom / Aurora Pulse */
  .hero-aurora {
    background: linear-gradient(-45deg, #0d1117, #1b1f3b, #0f3460, #16213e);
    background-size: 400% 400%;
    animation: auroraBG 6s ease infinite;
    height: 165px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    border: 1px solid #30363d;
  }
  @keyframes auroraBG {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  .hero-aurora h1 { margin: 0; font-size: 34px; color: #fff; }
  .hero-aurora p { margin: 8px 0 0 0; font-size: 14px; color: #79c0ff; }

  /* Option 4: Minimal Clean (No Banner) */
  .hero-minimal {
    text-align: center;
    padding: 10px 0 4px 0;
  }
  .hero-minimal h1 {
    margin: 0 0 10px 0;
    padding-bottom: 10px;
    border-bottom: 1px solid #21262d;
    font-size: 32px;
  }
  .hero-minimal p {
    margin: 6px 0;
    font-size: 15px;
  }

  /* Center Quote & Typing Simulation */
  .center-block {
    text-align: center;
    margin: 12px 0 20px 0;
  }
  .quote {
    font-style: italic;
    color: var(--gh-text);
    font-size: 15px;
    margin: 8px 0 14px 0;
  }
  .typing-container {
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 10px 0 18px 0;
  }
  .typing-text {
    color: #58A6FF;
    font-size: 18px;
    font-weight: 500;
    border-right: 2px solid #58A6FF;
    padding-right: 4px;
    animation: blinkCursor 0.75s step-end infinite;
  }
  @keyframes blinkCursor {
    from, to { border-color: transparent }
    50% { border-color: #58A6FF; }
  }

  /* Badges */
  .badge-row {
    display: flex;
    justify-content: center;
    gap: 6px;
    flex-wrap: wrap;
    margin-top: 8px;
  }
  .badge {
    display: inline-flex;
    align-items: center;
    padding: 5px 10px;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.8px;
    text-transform: uppercase;
    color: #fff;
    border-radius: 2px;
  }
  .b-vercel { background: #000; border: 1px solid #333; }
  .b-linkedin { background: #0A66C2; }
  .b-email { background: #EA4335; }
  .b-github { background: #181717; border: 1px solid #333; }

  /* Dividers */
  .divider-glow {
    height: 3px;
    width: 100%;
    margin: 22px 0;
    border-radius: 2px;
    background: linear-gradient(90deg, transparent, #1f6feb, #58a6ff, #a371f7, #58a6ff, #1f6feb, transparent);
    background-size: 200% 100%;
    animation: glowSlide 3s linear infinite;
  }
  @keyframes glowSlide {
    0% { background-position: 100% 0; }
    100% { background-position: -100% 0; }
  }
  .divider-standard {
    height: 1px;
    background: #21262d;
    margin: 22px 0;
  }

  /* Content Sections */
  h3 {
    font-size: 18px;
    margin: 16px 0 12px 0;
  }
  ul.about-list {
    padding-left: 20px;
    line-height: 1.6;
    font-size: 14px;
    color: #c9d1d9;
  }
  ul.about-list li { margin-bottom: 6px; }
  ul.about-list b { color: #fff; }

  /* 2x2 Table */
  .skills-table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
  }
  .skills-table td {
    width: 50%;
    vertical-align: top;
    border: 1px solid var(--gh-border);
    padding: 14px;
    background: #161b2255;
  }
  .skills-table h4 {
    margin: 0 0 10px 0;
    font-size: 14px;
  }
  .pill-group {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
  }
  .pill {
    font-size: 10px;
    font-weight: 700;
    padding: 4px 8px;
    border-radius: 2px;
    color: white;
    text-transform: uppercase;
  }

  /* Snake Animation Simulation */
  .snake-box {
    margin-top: 22px;
    padding: 14px;
    border: 1px dashed var(--gh-border);
    border-radius: 6px;
    text-align: center;
    background: #090d11;
  }
  .snake-title {
    font-size: 12px;
    color: var(--gh-muted);
    margin-bottom: 8px;
    font-family: monospace;
  }
  .contrib-grid {
    display: inline-grid;
    grid-template-columns: repeat(28, 10px);
    gap: 3px;
    position: relative;
  }
  .c-cell {
    width: 10px;
    height: 10px;
    border-radius: 2px;
    background: #161b22;
  }
  .c-1 { background: #0e4429; }
  .c-2 { background: #006d32; }
  .c-3 { background: #26a641; }
  .c-4 { background: #39d353; }
  .snake-dot {
    background: #58a6ff !important;
    box-shadow: 0 0 6px #58a6ff;
  }

  .caption-note {
    margin-top: 14px;
    padding: 10px 14px;
    background: #161b22;
    border-left: 3px solid #58a6ff;
    font-size: 13px;
    color: #c9d1d9;
    border-radius: 4px;
    max-width: 900px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
</head>
<body>

<div class="controls">
  <div class="tabs">
    <button class="tab-btn active" onclick="setStyle('wave', this)">1. Animated Wave Banner</button>
    <button class="tab-btn" onclick="setStyle('grid', this)">2. Cyber Tech Grid Texture</button>
    <button class="tab-btn" onclick="setStyle('aurora', this)">3. Aurora Gradient Pulse</button>
    <button class="tab-btn" onclick="setStyle('minimal', this)">4. Clean Centered (No Banner)</button>
  </div>
  <div class="toggle-group">
    <label><input type="checkbox" id="glowToggle" checked onchange="toggleDividers()"> Glowing Dividers</label>
    <label><input type="checkbox" id="snakeToggle" checked onchange="toggleSnake()"> Bottom Contribution Snake</label>
  </div>
</div>

<div class="gh-container">
  <div class="gh-file-header">
    <span>Ujjaval0 / README.md</span>
    <span id="styleBadge" style="color: #58a6ff;">Active: Style 1 (Animated Wave)</span>
  </div>

  <!-- Dynamic Header Area -->
  <div id="bannerArea">
    <div class="banner-wrapper hero-wave">
      <h1>Ujjaval Bhardwaj</h1>
      <p>AI Product & Strategy  |  LLM Evaluation & Data Analytics  ·  India 🇮🇳</p>
      <svg class="wave-svg" viewBox="0 0 1200 120" preserveAspectRatio="none">
        <path d="M0,40 C300,110 600,-20 900,50 C1050,85 1150,40 1200,40 L1200,120 L0,120 Z" fill="#0d1117" opacity="0.6"></path>
        <path d="M0,70 C400,0 800,120 1200,60 L1200,120 L0,120 Z" fill="#0d1117"></path>
      </svg>
    </div>
  </div>

  <!-- Centered Quote, Typing SVG & Connect Badges -->
  <div class="center-block">
    <div class="quote">"I started with data. Now I want to decide what gets built with it."</div>
    
    <!-- Centered Typing SVG Simulation -->
    <div class="typing-container">
      <span class="typing-text" id="typingElem">AI Product Management and Strategy</span>
    </div>

    <div class="badge-row">
      <span class="badge b-vercel">▲ Portfolio</span>
      <span class="badge b-linkedin">in LinkedIn</span>
      <span class="badge b-email">✉️ Email</span>
      <span class="badge b-github">🐙 GitHub</span>
    </div>
  </div>

  <div class="divider divider-glow"></div>

  <h3>⚡ About Me</h3>
  <ul class="about-list">
    <li><b>Background:</b> Technical Product Builder with a foundation in Data Analytics and hands-on LLM evaluation at <b>Soul AI</b>.</li>
    <li><b>Current Focus:</b> Evaluating <b>GPT-4, Claude, and Gemini</b> workflows, writing product specs, and dissecting <b>LangChain, LangGraph, and RAG</b> architectures under the hood.</li>
    <li><b>Core Advantage:</b> Bridging the gap between engineering and product—using <b>SQL & Python</b> to validate real user problems and <b>LLM Evals</b> to ensure AI features actually perform in production.</li>
  </ul>

  <div class="divider divider-glow"></div>

  <h3>🛠️ Skills & Stack</h3>
  <table class="skills-table">
    <tr>
      <td>
        <h4>🤖 AI & LLM Stack</h4>
        <div class="pill-group">
          <span class="pill" style="background:#412991">OpenAI</span>
          <span class="pill" style="background:#CC785C">Claude</span>
          <span class="pill" style="background:#4285F4">Gemini</span>
          <span class="pill" style="background:#1C3C3C">LangChain</span>
          <span class="pill" style="background:#00695C">LangGraph</span>
          <span class="pill" style="background:#E65100">LangSmith</span>
          <span class="pill" style="background:#000">RAG Systems</span>
        </div>
      </td>
      <td>
        <h4>🧭 Product & Strategy</h4>
        <div class="pill-group">
          <span class="pill" style="background:#F24E1E">Figma</span>
          <span class="pill" style="background:#000">Notion</span>
          <span class="pill" style="background:#050038">Miro</span>
          <span class="pill" style="background:#146EF5">Webflow</span>
          <span class="pill" style="background:#2B2D42">PRDs & Roadmapping</span>
          <span class="pill" style="background:#4A4E69">User Research</span>
        </div>
      </td>
    </tr>
    <tr>
      <td>
        <h4>📊 Product Analytics & Data</h4>
        <div class="pill-group">
          <span class="pill" style="background:#4479A1">SQL</span>
          <span class="pill" style="background:#3776AB">Python</span>
          <span class="pill" style="background:#F2C811; color:#000">Power BI</span>
          <span class="pill" style="background:#217346">Excel</span>
        </div>
      </td>
      <td>
        <h4>💻 Dev & Prototyping</h4>
        <div class="pill-group">
          <span class="pill" style="background:#000">Cursor</span>
          <span class="pill" style="background:#007ACC">VS Code</span>
          <span class="pill" style="background:#F05032">Git</span>
          <span class="pill" style="background:#FF6C37">REST APIs</span>
        </div>
      </td>
    </tr>
  </table>

  <!-- Optional Contribution Snake -->
  <div class="snake-box" id="snakeBox">
    <div class="snake-title">🐍 Animated Contribution Graph Snake (Optional Footer Widget)</div>
    <div class="contrib-grid" id="contribGrid"></div>
  </div>
</div>

<div class="caption-note" id="styleDesc">
  <b>Style 1 (Animated Wave Banner):</b> Uses <code>capsule-render</code> to create a dark-mode gradient banner with a smooth moving wave at the top. Gives the profile an immediate "designed portfolio" feel.
</div>

<script>
  // Typing SVG Animation Loop
  const lines = [
    "AI Product Management and Strategy",
    "LLM Evaluation | RAG Systems | Product Analytics",
    "Turning Model Capabilities into User Value"
  ];
  let lineIdx = 0;
  let charIdx = 0;
  let isDeleting = false;
  const typingElem = document.getElementById("typingElem");

  function typeLoop() {
    const currentLine = lines[lineIdx];
    if (isDeleting) {
      charIdx--;
    } else {
      charIdx++;
    }
    typingElem.textContent = currentLine.substring(0, charIdx);

    let speed = isDeleting ? 30 : 55;
    if (!isDeleting && charIdx === currentLine.length) {
      speed = 1600;
      isDeleting = true;
    } else if (isDeleting && charIdx === 0) {
      isDeleting = false;
      lineIdx = (lineIdx + 1) % lines.length;
      speed = 400;
    }
    setTimeout(typeLoop, speed);
  }
  setTimeout(typeLoop, 1000);

  // Banner Switcher
  function setStyle(type, btn) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    const area = document.getElementById('bannerArea');
    const badge = document.getElementById('styleBadge');
    const desc = document.getElementById('styleDesc');

    if (type === 'wave') {
      badge.textContent = "Active: Style 1 (Animated Wave)";
      desc.innerHTML = "<b>Style 1 (Animated Wave Banner):</b> Uses <code>capsule-render</code> to generate a dark-to-blue gradient header with a smooth moving wave. Great if you want high visual polish.";
      area.innerHTML = `
        <div class="banner-wrapper hero-wave">
          <h1>Ujjaval Bhardwaj</h1>
          <p>AI Product & Strategy  |  LLM Evaluation & Data Analytics  ·  India 🇮🇳</p>
          <svg class="wave-svg" viewBox="0 0 1200 120" preserveAspectRatio="none">
            <path d="M0,40 C300,110 600,-20 900,50 C1050,85 1150,40 1200,40 L1200,120 L0,120 Z" fill="#0d1117" opacity="0.6"></path>
            <path d="M0,70 C400,0 800,120 1200,60 L1200,120 L0,120 Z" fill="#0d1117"></path>
          </svg>
        </div>`;
    } else if (type === 'grid') {
      badge.textContent = "Active: Style 2 (Cyber Tech Grid)";
      desc.innerHTML = "<b>Style 2 (Cyber Tech Grid Texture):</b> Uses a custom SVG hero card with a subtle blueprint grid texture and glowing gradient title—very popular for AI & engineering product profiles.";
      area.innerHTML = `
        <div class="banner-wrapper hero-grid">
          <h1>Ujjaval Bhardwaj</h1>
          <p>AI Product & Strategy  |  LLM Evaluation & Data Analytics  ·  India 🇮🇳</p>
        </div>`;
    } else if (type === 'aurora') {
      badge.textContent = "Active: Style 3 (Aurora Soft Pulse)";
      desc.innerHTML = "<b>Style 3 (Aurora Soft Pulse):</b> Uses <code>capsule-render?type=soft</code> with a pulsing dark-indigo/blue background animation inside a rounded card.";
      area.innerHTML = `
        <div class="banner-wrapper hero-aurora">
          <h1>Ujjaval Bhardwaj</h1>
          <p>AI Product & Strategy  |  LLM Evaluation & Data Analytics  ·  India 🇮🇳</p>
        </div>`;
    } else if (type === 'minimal') {
      badge.textContent = "Active: Style 4 (Clean Centered)";
      desc.innerHTML = "<b>Style 4 (Clean Centered — Your Current Style Fixed):</b> Keeps your original minimalist layout with no heavy top banner, but fixes the Typing SVG centering and adds the glowing dividers.";
      area.innerHTML = `
        <div class="hero-minimal">
          <h1>Ujjaval Bhardwaj</h1>
          <p><b>AI Product & Strategy  |  LLM Evaluation & Data Analytics</b>  ·  India 🇮🇳</p>
        </div>`;
    }
  }

  // Toggle Dividers
  function toggleDividers() {
    const isGlow = document.getElementById('glowToggle').checked;
    document.querySelectorAll('.divider').forEach(d => {
      d.className = isGlow ? 'divider divider-glow' : 'divider divider-standard';
    });
  }

  // Toggle Snake
  function toggleSnake() {
    const show = document.getElementById('snakeToggle').checked;
    document.getElementById('snakeBox').style.display = show ? 'block' : 'none';
  }

  // Build Simulated Contribution Grid + Moving Snake
  const grid = document.getElementById('contribGrid');
  const classes = ['', 'c-1', 'c-2', 'c-3', 'c-4', '', 'c-1'];
  const cells = [];
  for (let i = 0; i < 84; i++) {
    const cell = document.createElement('div');
    cell.className = 'c-cell ' + classes[i % classes.length];
    grid.appendChild(cell);
    cells.push(cell);
  }
  let snakeHead = 0;
  setInterval(() => {
    cells.forEach(c => c.classList.remove('snake-dot'));
    for (let s = 0; s < 5; s++) {
      let idx = (snakeHead - s + cells.length) % cells.length;
      cells[idx].classList.add('snake-dot');
    }
    snakeHead = (snakeHead + 1) % cells.length;
  }, 120);
</script>

</body>
</html>
