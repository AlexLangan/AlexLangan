<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Alex Langan — Developer</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0f;
    --surface: #0f0f18;
    --border: #1e1e2e;
    --accent: #7df9c2;
    --accent2: #f97dbb;
    --accent3: #7db8f9;
    --text: #c9d1e0;
    --muted: #565b78;
    --warn: #f9c97d;
    --font-mono: 'JetBrains Mono', monospace;
    --font-display: 'Syne', sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-mono);
    font-size: 13px;
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
    pointer-events: none;
    z-index: 1000;
  }

  /* Noise texture */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 999;
    opacity: 0.4;
  }

  .layout {
    max-width: 1100px;
    margin: 0 auto;
    padding: 40px 24px;
    position: relative;
    z-index: 1;
  }

  /* ── TOP BAR ── */
  .topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid var(--border);
    padding-bottom: 16px;
    margin-bottom: 40px;
    animation: fadeDown 0.6s ease both;
  }

  .topbar-left {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .traffic-lights { display: flex; gap: 6px; }
  .tl {
    width: 12px; height: 12px;
    border-radius: 50%;
    cursor: pointer;
    transition: filter 0.2s;
  }
  .tl:hover { filter: brightness(1.3); }
  .tl.red { background: #ff5f57; }
  .tl.yellow { background: #febc2e; }
  .tl.green { background: #28c840; }

  .tab-title {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.08em;
  }

  .status-badge {
    font-size: 10px;
    padding: 3px 10px;
    border-radius: 20px;
    border: 1px solid var(--accent);
    color: var(--accent);
    letter-spacing: 0.1em;
    animation: pulse-glow 2s ease infinite;
  }

  @keyframes pulse-glow {
    0%, 100% { box-shadow: 0 0 0 0 rgba(125,249,194,0); }
    50% { box-shadow: 0 0 8px 2px rgba(125,249,194,0.2); }
  }

  /* ── HERO ── */
  .hero {
    margin-bottom: 60px;
    animation: fadeUp 0.7s 0.1s ease both;
  }

  .prompt-line {
    color: var(--muted);
    font-size: 12px;
    margin-bottom: 12px;
  }
  .prompt-line span { color: var(--accent3); }

  .hero-name {
    font-family: var(--font-display);
    font-size: clamp(48px, 9vw, 96px);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.03em;
    background: linear-gradient(135deg, #fff 0%, var(--accent) 50%, var(--accent3) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 4px;
  }

  .hero-sub {
    font-family: var(--font-display);
    font-size: clamp(14px, 2vw, 18px);
    font-weight: 400;
    color: var(--muted);
    margin-bottom: 24px;
  }

  .hero-meta {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 28px;
  }

  .meta-chip {
    font-size: 11px;
    padding: 4px 12px;
    border-radius: 4px;
    background: rgba(255,255,255,0.04);
    border: 1px solid var(--border);
    color: var(--muted);
  }
  .meta-chip .icon { margin-right: 5px; }

  .hero-links {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
  }

  .hero-link {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    font-size: 12px;
    color: var(--text);
    text-decoration: none;
    padding: 6px 16px;
    border: 1px solid var(--border);
    border-radius: 6px;
    background: rgba(255,255,255,0.02);
    transition: all 0.2s;
    letter-spacing: 0.04em;
  }
  .hero-link:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(125,249,194,0.05);
    transform: translateY(-1px);
  }

  /* ── SECTION HEADERS ── */
  .section { margin-bottom: 56px; }

  .section-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;
    animation: fadeUp 0.5s ease both;
  }

  .section-header::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .section-label {
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
  }

  .section-num {
    font-size: 10px;
    color: var(--accent);
    letter-spacing: 0.1em;
  }

  /* ── SKILLS GRID ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
  }

  .skill-cell {
    background: var(--surface);
    padding: 16px;
    transition: background 0.2s;
    cursor: default;
  }
  .skill-cell:hover { background: rgba(125,249,194,0.04); }

  .skill-category {
    font-size: 9px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 8px;
  }

  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
  }

  .tag {
    font-size: 11px;
    padding: 2px 8px;
    border-radius: 3px;
    background: rgba(255,255,255,0.05);
    color: var(--text);
    transition: all 0.2s;
  }
  .tag:hover { color: var(--accent); }
  .tag.lang { color: var(--accent3); background: rgba(125,184,249,0.08); }
  .tag.fw { color: var(--accent); background: rgba(125,249,194,0.08); }
  .tag.tool { color: var(--warn); background: rgba(249,201,125,0.08); }
  .tag.db { color: var(--accent2); background: rgba(249,125,187,0.08); }

  /* ── PROJECTS ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 12px;
  }

  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 20px;
    position: relative;
    overflow: hidden;
    transition: all 0.25s;
    animation: fadeUp 0.5s ease both;
  }
  .project-card:hover {
    border-color: rgba(125,249,194,0.3);
    transform: translateY(-2px);
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    border-radius: 8px 8px 0 0;
  }
  .card-green::before { background: linear-gradient(90deg, var(--accent), transparent); }
  .card-blue::before { background: linear-gradient(90deg, var(--accent3), transparent); }
  .card-pink::before { background: linear-gradient(90deg, var(--accent2), transparent); }
  .card-yellow::before { background: linear-gradient(90deg, var(--warn), transparent); }

  .project-status {
    font-size: 9px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    display: inline-block;
  }
  .dot-active { background: var(--accent); box-shadow: 0 0 6px var(--accent); animation: blink 1.4s ease infinite; }
  .dot-dev { background: var(--warn); }
  .dot-shipped { background: var(--muted); }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.3} }

  .project-name {
    font-family: var(--font-display);
    font-size: 17px;
    font-weight: 700;
    color: #fff;
    margin-bottom: 6px;
    letter-spacing: -0.02em;
  }

  .project-desc {
    font-size: 12px;
    color: var(--muted);
    margin-bottom: 14px;
    line-height: 1.5;
  }

  .project-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
  }

  /* ── CURRENT SPRINT ── */
  .sprint-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    border-radius: 8px;
    padding: 24px;
    font-size: 12px;
    animation: fadeUp 0.5s ease both;
  }

  .sprint-row {
    display: flex;
    gap: 12px;
    margin-bottom: 8px;
    align-items: flex-start;
  }
  .sprint-key {
    color: var(--accent);
    min-width: 160px;
    flex-shrink: 0;
  }
  .sprint-val { color: var(--text); }

  .sprint-cmd {
    margin-top: 16px;
    padding: 12px 16px;
    background: rgba(0,0,0,0.4);
    border-radius: 6px;
    color: var(--accent);
    font-size: 12px;
  }
  .sprint-cmd .ps1 { color: var(--muted); }

  /* ── FOOTER ── */
  .footer {
    border-top: 1px solid var(--border);
    padding-top: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 0.06em;
    animation: fadeUp 0.5s 0.3s ease both;
  }
  .footer-right { color: var(--accent); }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-10px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* stagger project cards */
  .project-card:nth-child(1) { animation-delay: 0.05s; }
  .project-card:nth-child(2) { animation-delay: 0.1s; }
  .project-card:nth-child(3) { animation-delay: 0.15s; }
  .project-card:nth-child(4) { animation-delay: 0.2s; }

  /* Cursor blink on prompt */
  .cursor {
    display: inline-block;
    width: 8px; height: 14px;
    background: var(--accent);
    vertical-align: middle;
    margin-left: 3px;
    animation: blink 1s step-end infinite;
  }

  @media (max-width: 600px) {
    .skills-grid { grid-template-columns: 1fr 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    .sprint-key { min-width: 120px; }
    .footer { flex-direction: column; gap: 8px; text-align: center; }
  }
</style>
</head>
<body>
<div class="layout">

  <!-- TOP BAR -->
  <div class="topbar">
    <div class="topbar-left">
      <div class="traffic-lights">
        <div class="tl red"></div>
        <div class="tl yellow"></div>
        <div class="tl green"></div>
      </div>
      <span class="tab-title">alex_langan — bash — 120×40</span>
    </div>
    <div class="status-badge">● OPEN TO PLACEMENT</div>
  </div>

  <!-- HERO -->
  <div class="hero">
    <div class="prompt-line"><span>alex@ulster-dev</span>:~/portfolio$ <span>whoami</span></div>
    <div class="hero-name">Alex Langan</div>
    <div class="hero-sub">Computer Science · Year 2 · Ulster University Derry</div>
    <div class="hero-meta">
      <span class="meta-chip"><span class="icon">📍</span>Northern Ireland</span>
      <span class="meta-chip"><span class="icon">🎓</span>BSc Computer Science</span>
      <span class="meta-chip"><span class="icon">⚡</span>ML · IoT · Cloud · Embedded</span>
      <span class="meta-chip"><span class="icon">🔄</span>Actively Seeking Placement</span>
    </div>
    <div class="hero-links">
      <a class="hero-link" href="mailto:alextrentlangan@gmail.com">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="4" width="20" height="16" rx="2"/><polyline points="2,4 12,13 22,4"/></svg>
        alextrentlangan@gmail.com
      </a>
      <a class="hero-link" href="https://linkedin.com/in/alex-langan1" target="_blank">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
        linkedin.com/in/alex-langan1
      </a>
      <a class="hero-link" href="https://github.com/AlexLangan" target="_blank">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        github.com/AlexLangan
      </a>
    </div>
  </div>

  <!-- SKILLS -->
  <div class="section">
    <div class="section-header">
      <span class="section-num">01</span>
      <span class="section-label">Tech Stack</span>
    </div>
    <div class="skills-grid">
      <div class="skill-cell">
        <div class="skill-category">Languages</div>
        <div class="skill-tags">
          <span class="tag lang">Python</span>
          <span class="tag lang">Java</span>
          <span class="tag lang">C++</span>
          <span class="tag lang">JavaScript</span>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Frameworks</div>
        <div class="skill-tags">
          <span class="tag fw">TensorFlow</span>
          <span class="tag fw">Flask</span>
          <span class="tag fw">React</span>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Tools & Infra</div>
        <div class="skill-tags">
          <span class="tag tool">Docker</span>
          <span class="tag tool">Git</span>
          <span class="tag tool">AWS</span>
          <span class="tag tool">Raspberry Pi</span>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Databases</div>
        <div class="skill-tags">
          <span class="tag db">MongoDB</span>
          <span class="tag db">PostgreSQL</span>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Specialisation</div>
        <div class="skill-tags">
          <span class="tag">ML</span>
          <span class="tag">Embedded</span>
          <span class="tag">Cloud</span>
          <span class="tag">IoT</span>
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Currently Learning</div>
        <div class="skill-tags">
          <span class="tag">Networking</span>
          <span class="tag">Automation</span>
          <span class="tag">Data Systems</span>
        </div>
      </div>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="section">
    <div class="section-header">
      <span class="section-num">02</span>
      <span class="section-label">Projects</span>
    </div>
    <div class="projects-grid">

      <div class="project-card card-green">
        <div class="project-status">
          <span class="dot dot-active"></span>
          <span style="color:var(--accent)">active</span>
        </div>
        <div class="project-name">OBD Dashboard</div>
        <div class="project-desc">Real-time car diagnostics over OBD-II with live data visualisation and performance monitoring.</div>
        <div class="project-stack">
          <span class="tag lang">Python</span>
          <span class="tag tool">Raspberry Pi</span>
          <span class="tag">OBD-II</span>
          <span class="tag">IoT</span>
        </div>
      </div>

      <div class="project-card card-blue">
        <div class="project-status">
          <span class="dot dot-active"></span>
          <span style="color:var(--accent)">active</span>
        </div>
        <div class="project-name">Docker Agent</div>
        <div class="project-desc">AI-powered Docker automation tool that generates intelligent configs and handles automated deployments.</div>
        <div class="project-stack">
          <span class="tag tool">Docker</span>
          <span class="tag">AI</span>
          <span class="tag lang">Python</span>
          <span class="tag">DevOps</span>
        </div>
      </div>

      <div class="project-card card-yellow">
        <div class="project-status">
          <span class="dot dot-dev"></span>
          <span style="color:var(--warn)">in development</span>
        </div>
        <div class="project-name">Lego Autonomous Car</div>
        <div class="project-desc">Raspberry Pi + LEGO Technic autonomous navigation using CV and ML. Currently adding RC control via mobile app.</div>
        <div class="project-stack">
          <span class="tag fw">TensorFlow</span>
          <span class="tag tool">Raspberry Pi</span>
          <span class="tag">CV</span>
          <span class="tag">Robotics</span>
        </div>
      </div>

      <div class="project-card card-pink">
        <div class="project-status">
          <span class="dot dot-shipped"></span>
          <span style="color:var(--muted)">shipped</span>
        </div>
        <div class="project-name">Alien Invasion</div>
        <div class="project-desc">Python game with a custom graphics engine, interactive gameplay, and progressive difficulty.</div>
        <div class="project-stack">
          <span class="tag lang">Python</span>
          <span class="tag">Pygame</span>
          <span class="tag">Game Dev</span>
        </div>
      </div>

    </div>
  </div>

  <!-- CURRENT SPRINT -->
  <div class="section">
    <div class="section-header">
      <span class="section-num">03</span>
      <span class="section-label">Current Sprint</span>
    </div>
    <div class="sprint-card">
      <div class="sprint-row">
        <span class="sprint-key">SPRINT_GOAL</span>
        <span class="sprint-val">Mobile app integration for LEGO car RC control</span>
      </div>
      <div class="sprint-row">
        <span class="sprint-key">LEARNING_TRACK_1</span>
        <span class="sprint-val">Networking fundamentals and protocols</span>
      </div>
      <div class="sprint-row">
        <span class="sprint-key">LEARNING_TRACK_2</span>
        <span class="sprint-val">Automation and scripting</span>
      </div>
      <div class="sprint-row">
        <span class="sprint-key">LEARNING_TRACK_3</span>
        <span class="sprint-val">Data-driven system architecture</span>
      </div>
      <div class="sprint-row">
        <span class="sprint-key">APPLYING_FROM</span>
        <span class="sprint-val">Mobile Apps Development class</span>
      </div>
      <div class="sprint-cmd">
        <span class="ps1">$ </span>echo "Building, learning, and shipping daily"<br>
        <span style="color:var(--text)">Building, learning, and shipping daily</span><span class="cursor"></span>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    <span>alex@ulster-dev:~/portfolio$ <span style="color:var(--text)">exit</span></span>
    <span class="footer-right">open for collaboration · placement ready</span>
  </div>

</div>
</body>
</html>
