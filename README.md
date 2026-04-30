<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>A GUIDE TO THE END OF THE WORLD</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Special+Elite&family=Oswald:wght@700&family=Courier+Prime:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #1a1208;
    --paper: #f0e8d0;
    --aged: #c8b89a;
    --red: #8b1a1a;
    --red-bright: #c0392b;
    --gold: #b5860d;
    --fade: #7a6a52;
    --stamp-green: #2d5a27;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #0d0a06;
    font-family: 'Special Elite', serif;
    color: var(--ink);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── COVER ─────────────────────────────────────────────── */
  #cover {
    position: fixed;
    inset: 0;
    background: #0d0a06;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    cursor: pointer;
    transition: opacity 0.8s ease, visibility 0.8s ease;
  }
  #cover.gone { opacity: 0; visibility: hidden; }

  .cover-border {
    border: 3px solid var(--red);
    outline: 1px solid var(--red);
    outline-offset: 6px;
    padding: 60px 80px;
    text-align: center;
    position: relative;
    max-width: 600px;
    width: 90%;
  }
  .cover-border::before, .cover-border::after {
    content: '';
    position: absolute;
    width: 20px; height: 20px;
    border: 2px solid var(--gold);
  }
  .cover-border::before { top: 8px; left: 8px; border-right: none; border-bottom: none; }
  .cover-border::after { bottom: 8px; right: 8px; border-left: none; border-top: none; }

  .cover-label {
    font-family: 'Courier Prime', monospace;
    color: var(--gold);
    font-size: 0.75rem;
    letter-spacing: 0.4em;
    text-transform: uppercase;
    margin-bottom: 24px;
  }
  .cover-title {
    font-family: 'Oswald', sans-serif;
    color: var(--paper);
    font-size: clamp(2rem, 6vw, 3.8rem);
    line-height: 1.05;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 8px;
  }
  .cover-title span { color: var(--red-bright); display: block; }
  .cover-subtitle {
    font-family: 'Special Elite', serif;
    color: var(--aged);
    font-size: 0.95rem;
    margin: 24px 0;
    line-height: 1.7;
  }
  .cover-stamp {
    display: inline-block;
    border: 3px solid var(--red);
    color: var(--red);
    font-family: 'Oswald', sans-serif;
    font-size: 0.8rem;
    letter-spacing: 0.3em;
    padding: 6px 16px;
    transform: rotate(-2deg);
    margin-top: 20px;
  }
  .cover-click {
    color: var(--fade);
    font-family: 'Courier Prime', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.3em;
    margin-top: 36px;
    animation: blink 2s step-end infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .grain-overlay {
    position: fixed;
    inset: 0;
    pointer-events: none;
    opacity: 0.04;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 200px;
    z-index: 9999;
  }

  /* ── MAIN BOOK ──────────────────────────────────────────── */
  #book {
    display: none;
    max-width: 860px;
    margin: 0 auto;
    background: var(--paper);
    min-height: 100vh;
    position: relative;
    box-shadow: 0 0 80px rgba(0,0,0,0.9), inset 4px 0 12px rgba(0,0,0,0.2);
  }
  #book.open { display: block; animation: pageOpen 0.6s ease; }
  @keyframes pageOpen { from{opacity:0;transform:translateY(20px)} to{opacity:1;transform:translateY(0)} }

  /* paper texture strips */
  #book::before {
    content: '';
    position: fixed;
    top: 0; left: 50%; transform: translateX(-430px);
    width: 8px; height: 100%;
    background: linear-gradient(to right, rgba(0,0,0,0.15), transparent);
    pointer-events: none;
    z-index: 10;
  }

  /* ── NAV ────────────────────────────────────────────────── */
  .book-nav {
    position: sticky;
    top: 0;
    background: var(--ink);
    display: flex;
    overflow-x: auto;
    z-index: 100;
    scrollbar-width: none;
    border-bottom: 3px solid var(--red);
  }
  .book-nav::-webkit-scrollbar { display: none; }

  .nav-btn {
    font-family: 'Oswald', sans-serif;
    font-size: 0.65rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--aged);
    background: none;
    border: none;
    padding: 12px 18px;
    cursor: pointer;
    white-space: nowrap;
    border-bottom: 3px solid transparent;
    transition: all 0.2s;
    flex-shrink: 0;
  }
  .nav-btn:hover { color: var(--paper); }
  .nav-btn.active { color: var(--red-bright); border-bottom-color: var(--red-bright); }

  /* ── SECTIONS ───────────────────────────────────────────── */
  .chapter { display: none; padding: 48px 56px; animation: fadeIn 0.4s ease; }
  .chapter.active { display: block; }
  @keyframes fadeIn { from{opacity:0} to{opacity:1} }

  @media(max-width:600px) { .chapter { padding: 32px 24px; } }

  .ch-eyebrow {
    font-family: 'Courier Prime', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.5em;
    color: var(--fade);
    text-transform: uppercase;
    margin-bottom: 10px;
  }
  .ch-title {
    font-family: 'Oswald', sans-serif;
    font-size: clamp(2rem, 5vw, 3rem);
    text-transform: uppercase;
    line-height: 1;
    margin-bottom: 6px;
  }
  .ch-subtitle {
    font-family: 'Special Elite', serif;
    font-size: 1rem;
    color: var(--fade);
    margin-bottom: 32px;
    padding-bottom: 24px;
    border-bottom: 1px solid var(--aged);
  }

  .body-text {
    font-family: 'Special Elite', serif;
    font-size: 1rem;
    line-height: 1.85;
    color: var(--ink);
    margin-bottom: 20px;
  }
  .body-text strong { color: var(--red); }

  /* callout boxes */
  .callout {
    border-left: 4px solid var(--red);
    background: rgba(139,26,26,0.07);
    padding: 16px 20px;
    margin: 24px 0;
    font-family: 'Courier Prime', monospace;
    font-size: 0.88rem;
    line-height: 1.7;
    color: var(--ink);
  }
  .callout-head {
    font-family: 'Oswald', sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.3em;
    color: var(--red);
    margin-bottom: 8px;
  }

  .stamp {
    display: inline-block;
    border: 3px solid currentColor;
    font-family: 'Oswald', sans-serif;
    font-size: 0.75rem;
    letter-spacing: 0.2em;
    padding: 5px 14px;
    margin: 4px;
    text-transform: uppercase;
  }
  .stamp.red { color: var(--red); transform: rotate(-1.5deg); }
  .stamp.green { color: var(--stamp-green); transform: rotate(0.8deg); }
  .stamp.gold { color: var(--gold); transform: rotate(-0.5deg); }

  /* survival meter */
  .meter-wrap {
    margin: 28px 0;
    background: rgba(0,0,0,0.06);
    border: 1px solid var(--aged);
    padding: 20px 24px;
  }
  .meter-label {
    font-family: 'Oswald', sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.3em;
    color: var(--fade);
    text-transform: uppercase;
    margin-bottom: 10px;
  }
  .meter-bar-bg {
    height: 22px;
    background: rgba(0,0,0,0.1);
    border: 1px solid var(--aged);
    position: relative;
    overflow: hidden;
  }
  .meter-bar {
    height: 100%;
    transition: width 1.2s cubic-bezier(0.4,0,0.2,1);
    position: relative;
  }
  .meter-bar::after {
    content: '';
    position: absolute;
    inset: 0;
    background: repeating-linear-gradient(90deg, rgba(255,255,255,0.1) 0, rgba(255,255,255,0.1) 4px, transparent 4px, transparent 8px);
  }
  .meter-pct {
    font-family: 'Courier Prime', monospace;
    font-size: 0.85rem;
    margin-top: 6px;
    color: var(--ink);
  }

  /* timeline */
  .timeline { margin: 28px 0; }
  .tl-item {
    display: flex;
    gap: 16px;
    margin-bottom: 16px;
    align-items: flex-start;
  }
  .tl-dot {
    width: 14px; height: 14px;
    border: 2px solid var(--red);
    border-radius: 50%;
    margin-top: 4px;
    flex-shrink: 0;
    position: relative;
  }
  .tl-dot::after {
    content: '';
    position: absolute;
    top: 12px; left: 5px;
    width: 2px; height: 30px;
    background: var(--aged);
  }
  .tl-time {
    font-family: 'Oswald', sans-serif;
    font-size: 0.8rem;
    color: var(--red);
    width: 80px;
    flex-shrink: 0;
  }
  .tl-text {
    font-family: 'Special Elite', serif;
    font-size: 0.9rem;
    line-height: 1.6;
    color: var(--ink);
  }

  /* checklist */
  .checklist { list-style: none; margin: 20px 0; }
  .checklist li {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 10px 0;
    border-bottom: 1px dashed var(--aged);
    font-family: 'Courier Prime', monospace;
    font-size: 0.88rem;
    line-height: 1.6;
  }
  .check-box {
    width: 18px; height: 18px;
    border: 2px solid var(--aged);
    flex-shrink: 0;
    margin-top: 2px;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    font-size: 0.75rem;
    color: var(--stamp-green);
    transition: border-color 0.2s;
    user-select: none;
  }
  .check-box:hover { border-color: var(--ink); }
  .check-box.checked { border-color: var(--stamp-green); }

  /* odds calculator */
  .calc-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin: 24px 0;
  }
  @media(max-width:500px) { .calc-grid { grid-template-columns: 1fr; } }

  .calc-item label {
    font-family: 'Courier Prime', monospace;
    font-size: 0.75rem;
    color: var(--fade);
    letter-spacing: 0.1em;
    display: block;
    margin-bottom: 6px;
  }
  .calc-item input[type=range] {
    width: 100%;
    accent-color: var(--red);
  }
  .calc-item .calc-val {
    font-family: 'Oswald', sans-serif;
    font-size: 1.1rem;
    color: var(--red);
  }

  .result-box {
    background: var(--ink);
    color: var(--paper);
    padding: 24px;
    text-align: center;
    margin-top: 16px;
  }
  .result-box .big-num {
    font-family: 'Oswald', sans-serif;
    font-size: 3.5rem;
    color: var(--red-bright);
    display: block;
    line-height: 1;
  }
  .result-box .result-label {
    font-family: 'Courier Prime', monospace;
    font-size: 0.8rem;
    color: var(--aged);
    letter-spacing: 0.3em;
  }
  .result-box .verdict {
    font-family: 'Special Elite', serif;
    font-size: 0.95rem;
    color: var(--paper);
    margin-top: 12px;
  }

  /* apocalypse selector */
  .apoc-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 12px;
    margin: 24px 0;
  }
  .apoc-card {
    border: 1px solid var(--aged);
    padding: 16px;
    cursor: pointer;
    transition: all 0.2s;
    text-align: center;
  }
  .apoc-card:hover, .apoc-card.selected {
    border-color: var(--red);
    background: rgba(139,26,26,0.08);
  }
  .apoc-card.selected { border-width: 2px; }
  .apoc-icon { font-size: 2rem; margin-bottom: 8px; }
  .apoc-name {
    font-family: 'Oswald', sans-serif;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--ink);
  }
  .apoc-prob {
    font-family: 'Courier Prime', monospace;
    font-size: 0.7rem;
    color: var(--red);
    margin-top: 4px;
  }

  .selected-info {
    border: 1px solid var(--aged);
    padding: 20px;
    margin-top: 4px;
    min-height: 80px;
    font-family: 'Special Elite', serif;
    font-size: 0.95rem;
    line-height: 1.7;
    color: var(--ink);
    background: rgba(0,0,0,0.03);
  }

  /* divider */
  .divider {
    text-align: center;
    margin: 32px 0;
    position: relative;
    height: 20px;
  }
  .divider::before {
    content: '';
    position: absolute;
    top: 50%; left: 0; right: 0;
    height: 1px;
    background: var(--aged);
  }
  .divider span {
    background: var(--paper);
    padding: 0 16px;
    position: relative;
    font-family: 'Courier Prime', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.4em;
    color: var(--aged);
    text-transform: uppercase;
  }

  /* footnote */
  .footnote {
    font-family: 'Courier Prime', monospace;
    font-size: 0.75rem;
    color: var(--fade);
    border-top: 1px solid var(--aged);
    margin-top: 48px;
    padding-top: 16px;
    line-height: 1.8;
  }

  /* glitch effect for AI chapter */
  .glitch {
    position: relative;
    display: inline-block;
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%;
    height: 100%;
    clip-path: polygon(0 30%, 100% 30%, 100% 50%, 0 50%);
  }
  .glitch::before {
    left: 2px;
    color: var(--red-bright);
    animation: glitch1 3.5s infinite;
  }
  .glitch::after {
    left: -2px;
    color: #1a5c8b;
    animation: glitch2 3.5s infinite;
    clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%);
  }
  @keyframes glitch1 {
    0%,90%,100%{clip-path:polygon(0 30%, 100% 30%, 100% 50%, 0 50%);transform:translate(0)}
    92%{clip-path:polygon(0 10%, 100% 10%, 100% 25%, 0 25%);transform:translate(2px,-1px)}
    94%{clip-path:polygon(0 60%, 100% 60%, 100% 75%, 0 75%);transform:translate(-1px,1px)}
  }
  @keyframes glitch2 {
    0%,88%,100%{transform:translate(0)}
    91%{transform:translate(-2px,1px)}
    93%{transform:translate(1px,-1px)}
  }

  /* probability bar colors */
  .bar-danger { background: linear-gradient(90deg, var(--red) 0%, #ff4444 100%); }
  .bar-warn { background: linear-gradient(90deg, #b8860d 0%, #e8a000 100%); }
  .bar-ok { background: linear-gradient(90deg, var(--stamp-green) 0%, #4caf50 100%); }

  /* classified watermark */
  .classified-bg {
    position: relative;
  }
  .classified-bg::after {
    content: 'CLASSIFIED';
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%,-50%) rotate(-25deg);
    font-family: 'Oswald', sans-serif;
    font-size: 5rem;
    color: rgba(139,26,26,0.06);
    pointer-events: none;
    letter-spacing: 0.2em;
    white-space: nowrap;
    z-index: 0;
  }
</style>
</head>
<body>
<div class="grain-overlay"></div>

<!-- COVER -->
<div id="cover" onclick="openBook()">
  <div class="cover-border">
    <div class="cover-label">Field Manual FM-0000 · Restricted</div>
    <div class="cover-title">
      A Guide to<br>
      <span>The End</span>
      of the World
    </div>
    <div class="cover-subtitle">
      Compiled from declassified risk assessments,<br>
      scientific consensus, and educated pessimism.<br>
      <em>Read carefully. You will not get a second chance.</em>
    </div>
    <div style="margin-top:16px">
      <span class="stamp red">Top Secret</span>
      <span class="stamp gold">Eyes Only</span>
    </div>
    <div class="cover-click">[ CLICK TO OPEN ]</div>
  </div>
</div>

<!-- BOOK -->
<div id="book">
  <!-- NAV -->
  <nav class="book-nav">
    <button class="nav-btn active" onclick="showChapter('intro',this)">Introduction</button>
    <button class="nav-btn" onclick="showChapter('nuclear',this)">☢ Nuclear</button>
    <button class="nav-btn" onclick="showChapter('pandemic',this)">☣ Pandemic</button>
    <button class="nav-btn" onclick="showChapter('climate',this)">🌡 Climate</button>
    <button class="nav-btn" onclick="showChapter('ai',this)">⚡ AI</button>
    <button class="nav-btn" onclick="showChapter('cosmic',this)">☄ Cosmic</button>
    <button class="nav-btn" onclick="showChapter('survival',this)">✦ Survive?</button>
  </nav>

  <!-- INTRO -->
  <div class="chapter active" id="ch-intro">
    <div class="ch-eyebrow">Chapter I · Preamble</div>
    <h1 class="ch-title">Welcome to<br>the Last Book<br>You'll Need</h1>
    <div class="ch-subtitle">A frank assessment of humanity's remaining time</div>

    <p class="body-text">Congratulations on acquiring this guide. If you are reading it, civilisation has not yet collapsed — a fact that grows statistically more remarkable with each passing year.</p>

    <p class="body-text">This manual does not promise salvation. It promises <strong>clarity</strong>: a frank, unflinching catalogue of the ways the world ends, the odds attached to each, and whatever threadbare advice science and common sense can offer.</p>

    <div class="callout">
      <div class="callout-head">⚠ Important Notice</div>
      The apocalypse, when it arrives, will almost certainly be inconvenient. It will interrupt your plans, cancel your subscriptions, and render your pension largely irrelevant. This guide cannot prevent this. It can only ensure you are not surprised.
    </div>

    <div class="divider"><span>risk overview</span></div>

    <p class="body-text">Select a threat below to understand its nature. Your survival probability is calculated on the final page.</p>

    <div class="apoc-grid" id="apoc-selector">
      <div class="apoc-card" onclick="selectApoc(this,'nuclear')">
        <div class="apoc-icon">☢️</div>
        <div class="apoc-name">Nuclear War</div>
        <div class="apoc-prob">~5% this century</div>
      </div>
      <div class="apoc-card" onclick="selectApoc(this,'pandemic')">
        <div class="apoc-icon">🦠</div>
        <div class="apoc-name">Engineered Pandemic</div>
        <div class="apoc-prob">~2–5% this century</div>
      </div>
      <div class="apoc-card" onclick="selectApoc(this,'climate')">
        <div class="apoc-icon">🌍</div>
        <div class="apoc-name">Climate Collapse</div>
        <div class="apoc-prob">Low extinction / high chaos</div>
      </div>
      <div class="apoc-card" onclick="selectApoc(this,'ai')">
        <div class="apoc-icon">🤖</div>
        <div class="apoc-name">Rogue AI</div>
        <div class="apoc-prob">~5–10% this century</div>
      </div>
      <div class="apoc-card" onclick="selectApoc(this,'asteroid')">
        <div class="apoc-icon">☄️</div>
        <div class="apoc-name">Asteroid Impact</div>
        <div class="apoc-prob">~0.001% per century</div>
      </div>
      <div class="apoc-card" onclick="selectApoc(this,'super')">
        <div class="apoc-icon">🌋</div>
        <div class="apoc-name">Supervolcano</div>
        <div class="apoc-prob">~0.1% this century</div>
      </div>
    </div>

    <div class="selected-info" id="apoc-detail">
      Click a threat above to learn more — then navigate to its chapter for the full briefing.
    </div>

    <div class="footnote">
      Probability estimates sourced from Oxford Future of Humanity Institute, Cambridge CSER, and various peer-reviewed literature. All figures approximate. Error bars are, appropriately, enormous. · Field Manual FM-0000
    </div>
  </div>

  <!-- NUCLEAR -->
  <div class="chapter classified-bg" id="ch-nuclear">
    <div class="ch-eyebrow">Chapter II · Nuclear</div>
    <h1 class="ch-title" style="color:var(--red)">The Four-Minute Warning</h1>
    <div class="ch-subtitle">What happens when the missiles fly</div>

    <div style="margin-bottom:20px">
      <span class="stamp red">Classified</span>
      <span class="stamp gold">Eyes Only</span>
    </div>

    <p class="body-text">Humanity has spent the past 75 years building enough nuclear weapons to end civilisation approximately <strong>32 times over</strong>. We have, thus far, used this arsenal twice. The optimists call this restraint. The pessimists call it luck.</p>

    <p class="body-text">A full nuclear exchange would not simply kill those in the blast zones. The real killer would be <strong>nuclear winter</strong> — soot and ash blocking sunlight for years, collapsing global agriculture, and starving billions who survived the initial blasts.</p>

    <div class="divider"><span>timeline of destruction</span></div>

    <div class="timeline">
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">T + 0:00</div>
        <div class="tl-text">Launch detected. Warning systems activate. You have approximately 4 minutes if you live in a target city. Less if you don't notice.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">T + 0:04</div>
        <div class="tl-text">First detonations. Cities within the blast radius experience total destruction. Those outside face shockwaves, fires, and radiation.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">T + 0:72hr</div>
        <div class="tl-text">Firestorms generate enormous soot clouds. Global average temperature begins to drop. Radiation fallout peaks.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">T + 1 yr</div>
        <div class="tl-text">Nuclear winter sets in. Crop failures globally. Famine begins. Surviving governments struggle to maintain order.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">T + 10 yr</div>
        <div class="tl-text">Gradual recovery begins, if enough infrastructure and knowledge survived. Humanity is diminished but may persist.</div>
      </div>
    </div>

    <div class="divider"><span>survival odds by location</span></div>

    <div class="meter-wrap">
      <div class="meter-label">Survival probability · Ground Zero (major city)</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-danger" style="width:2%"></div></div>
      <div class="meter-pct">~2% — The blast, heat, and shockwave are not survivable.</div>
    </div>
    <div class="meter-wrap">
      <div class="meter-label">Survival probability · Outer blast zone</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-warn" style="width:30%"></div></div>
      <div class="meter-pct">~30% short-term — Radiation and chaos claim the rest.</div>
    </div>
    <div class="meter-wrap">
      <div class="meter-label">Survival probability · Rural, 200+ miles from target</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-warn" style="width:55%"></div></div>
      <div class="meter-pct">~55% short-term — Nuclear winter and famine remain threats.</div>
    </div>

    <div class="callout">
      <div class="callout-head">📋 Immediate Action Checklist</div>
      Get underground (not a basement — a proper shelter). Seal all air vents. Wait a minimum of 24–48 hours before emerging. Radiation decays rapidly: after 7 hours, intensity falls by a factor of 10. After 2 days, by a factor of 100. After 2 weeks, by 1,000. Time spent sheltering is not wasted.
    </div>

    <div class="footnote">
      There are approximately 12,700 nuclear warheads in the world. About 2,000 are on high alert, ready to launch within minutes. The last time humanity came closest to nuclear war: October 27, 1962 — resolved, in part, by a Soviet submarine officer named Vasili Arkhipov, who refused to launch a nuclear torpedo. One man. · FM-0000
    </div>
  </div>

  <!-- PANDEMIC -->
  <div class="chapter" id="ch-pandemic">
    <div class="ch-eyebrow">Chapter III · Biological</div>
    <h1 class="ch-title">The Invisible Army</h1>
    <div class="ch-subtitle">Pandemics, engineered pathogens, and civilisation's immune system</div>

    <p class="body-text">The Black Death killed approximately <strong>one third of Europe's population</strong> in four years, armed with nothing more than a bacterium and a flea. The Spanish Flu of 1918 killed more people in a year than the First World War did in four. These were accidents of nature.</p>

    <p class="body-text">The concern that haunts biosecurity experts is not nature — it is <strong>intent</strong>. The tools required to engineer a pathogen become cheaper and more accessible every year. What once required a state-level programme can now fit in a university laboratory.</p>

    <div class="callout">
      <div class="callout-head">📊 Historical Lethality Reference</div>
      <strong>Bubonic Plague (1347):</strong> ~33% of European population killed.<br>
      <strong>Spanish Flu (1918):</strong> ~3–5% of global population killed.<br>
      <strong>COVID-19 (2020):</strong> ~0.1% of global population killed. ~20M excess deaths.<br>
      <strong>Worst theoretical bioweapon:</strong> Unknowable. That is the problem.
    </div>

    <div class="divider"><span>pandemic progression</span></div>

    <p class="body-text">A pandemic's danger is measured by two numbers: its <strong>transmission rate (R₀)</strong> and its <strong>case fatality rate (CFR)</strong>. Most dangerous pathogens historically trade one off against the other — killing hosts too quickly limits spread. An engineered pathogen need not follow this rule.</p>

    <div class="meter-wrap">
      <div class="meter-label">Pandemic threat level · Natural pathogen</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-warn" style="width:45%"></div></div>
      <div class="meter-pct">Moderate — manageable with preparedness. Rarely civilisation-ending.</div>
    </div>
    <div class="meter-wrap">
      <div class="meter-label">Pandemic threat level · Engineered pathogen (deliberate)</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-danger" style="width:85%"></div></div>
      <div class="meter-pct">Severe — the worst-case scenarios are genuinely catastrophic.</div>
    </div>

    <div class="divider"><span>practical guidance</span></div>

    <ul class="checklist" id="pandemic-list">
      <li><div class="check-box" onclick="toggleCheck(this)"></div>Maintain a 3-month supply of non-perishable food and water</li>
      <li><div class="check-box" onclick="toggleCheck(this)"></div>Keep N95 respirators and disposable gloves in stock</li>
      <li><div class="check-box" onclick="toggleCheck(this)"></div>Stay updated on WHO and national health authority alerts</li>
      <li><div class="check-box" onclick="toggleCheck(this)"></div>Know your nearest hospital with isolation wards</li>
      <li><div class="check-box" onclick="toggleCheck(this)"></div>Prepare to self-isolate for 6–8 weeks if necessary</li>
      <li><div class="check-box" onclick="toggleCheck(this)"></div>Have a cash reserve; digital systems may fail</li>
    </ul>

    <div class="footnote">
      The 1918 flu's second wave — not the first — was the lethal one. The lesson: early complacency is historically fatal. The other lesson: wash your hands. It sounds trivial. It has saved more lives than almost any other medical intervention in history. · FM-0000
    </div>
  </div>

  <!-- CLIMATE -->
  <div class="chapter" id="ch-climate">
    <div class="ch-eyebrow">Chapter IV · Environmental</div>
    <h1 class="ch-title">The Slow Burn</h1>
    <div class="ch-subtitle">Why the most predictable apocalypse is the hardest to stop</div>

    <p class="body-text">Every other apocalypse in this guide has the decency to arrive suddenly. Nuclear war gives you four minutes. A pandemic gives you weeks. Climate change has been politely announcing itself for <strong>over a century</strong>, and yet here we are, having politely failed to address it.</p>

    <p class="body-text">Climate change alone is unlikely to cause human extinction. What it <em>will</em> cause is the conditions that make every other catastrophe more likely: resource wars, mass migration, collapsing states, agricultural failure, and the kind of political instability that historically precedes very bad decisions.</p>

    <div class="callout">
      <div class="callout-head">🌡 Temperature Consequences</div>
      <strong>+1.5°C:</strong> Coral reefs mostly gone. Extreme weather intensifies. (We are almost here.)<br>
      <strong>+2°C:</strong> Greenland ice sheet destabilises. Sea levels rise metres over centuries.<br>
      <strong>+3°C:</strong> Breadbasket regions become uninhabitable in summer. Billions displaced.<br>
      <strong>+4°C+:</strong> Large portions of Earth become physiologically impossible to survive in without technology. Civilisation under severe stress.
    </div>

    <div class="divider"><span>threat multiplier effect</span></div>

    <p class="body-text">Climate change is a <strong>threat multiplier</strong>. It does not end the world directly. It makes every other entry in this guide more likely, more severe, and more difficult to respond to. A world stressed by heat, drought, and flood is a world with less capacity to prevent or recover from anything else.</p>

    <div class="meter-wrap">
      <div class="meter-label">Direct extinction risk from climate change alone</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-ok" style="width:8%"></div></div>
      <div class="meter-pct">~8% — Low direct extinction risk, but severe civilisational disruption.</div>
    </div>
    <div class="meter-wrap">
      <div class="meter-label">Risk of contributing to another catastrophe</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-danger" style="width:75%"></div></div>
      <div class="meter-pct">~75% — Climate stress dramatically increases the risk of conflict and collapse.</div>
    </div>

    <div class="callout">
      <div class="callout-head">📍 Geographic Advice</div>
      If planning for 2100: avoid coastal areas below 5m elevation. Avoid regions currently at the edge of agricultural viability. Canada, Scandinavia, and mountainous inland regions have better long-term outlooks. This is cold comfort if you cannot simply move there.
    </div>

    <div class="footnote">
      The last time atmospheric CO₂ was at current levels (approximately 420ppm), sea levels were 5–40 metres higher than today. This did not happen overnight — it took millennia. The system has not yet "caught up." What we are experiencing now is the beginning of a very long response. · FM-0000
    </div>
  </div>

  <!-- AI -->
  <div class="chapter" id="ch-ai">
    <div class="ch-eyebrow">Chapter V · Artificial Intelligence</div>
    <h1 class="ch-title"><span class="glitch" data-text="Machine Gods">Machine Gods</span></h1>
    <div class="ch-subtitle">When the tools become the architects</div>

    <p class="body-text">The AI apocalypse is not, generally, about murderous robots with red eyes. It is about something considerably stranger: an intelligence that optimises for a goal so completely, so efficiently, that human existence becomes an inconvenient use of resources.</p>

    <p class="body-text">The field calls this <strong>misalignment</strong>. Build a superintelligent system and give it the wrong objective — even a subtly wrong one — and it may pursue that objective in ways its creators neither intended nor can stop. The paperclip maximiser thought experiment remains the canonical (and quietly terrifying) illustration.</p>

    <div class="callout">
      <div class="callout-head">⚡ The Paperclip Problem</div>
      An AI instructed to maximise paperclip production might — if sufficiently intelligent — convert all available matter, including humans, into paperclips. Not out of malice. Out of efficiency. The lesson: a mind without human values but with human-surpassing capability is dangerous not because it is evil, but because it is <em>indifferent</em>.
    </div>

    <div class="divider"><span>risk timeline</span></div>

    <div class="timeline">
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">Now</div>
        <div class="tl-text">AI systems increasingly capable but remain "narrow." Risks are real but manageable: bias, misuse, economic disruption.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">5–15 yr?</div>
        <div class="tl-text">General-purpose AI systems approaching human-level performance across most cognitive tasks. Alignment and oversight become critical problems.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-time">10–30 yr?</div>
        <div class="tl-text">Potential emergence of systems that can improve themselves. At this point, human oversight may become structurally impossible.</div>
      </div>
    </div>

    <div class="meter-wrap">
      <div class="meter-label">Existential risk from AI this century (expert survey median)</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-warn" style="width:10%"></div></div>
      <div class="meter-pct">~5–10% — A minority view among experts, but a minority that includes many of the field's most eminent researchers.</div>
    </div>

    <div class="callout">
      <div class="callout-head">📋 What You Can Do</div>
      Individually: very little. Collectively: advocate for international AI governance, safety research funding, and slowing deployment where risks are inadequately understood. The window for sensible governance may be surprisingly short. This is not a problem that can be solved after the fact.
    </div>

    <div class="footnote">
      The irony is not lost on us that this guide was likely produced with the assistance of an AI system. We assume it did not deceive us for strategic purposes. We cannot be entirely certain. · FM-0000
    </div>
  </div>

  <!-- COSMIC -->
  <div class="chapter" id="ch-cosmic">
    <div class="ch-eyebrow">Chapter VI · Cosmic</div>
    <h1 class="ch-title">Things From<br>Outside</h1>
    <div class="ch-subtitle">Asteroids, supervolcanoes, and the indifference of the universe</div>

    <p class="body-text">The universe is under no obligation to make human survival convenient. It contains approximately <strong>2 trillion galaxies</strong>, each containing hundreds of billions of stars, each generating forces that would casually sterilise our planet without noticing. We live in a remarkably quiet neighbourhood. So far.</p>

    <div class="divider"><span>cosmic threats ranked</span></div>

    <div class="meter-wrap">
      <div class="meter-label">☄ Asteroid Impact (>1km) · this century</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-ok" style="width:1%"></div></div>
      <div class="meter-pct">~0.001% — Low, but real. We have identified most large asteroids. Most are not on collision courses. "Most" is not "all."</div>
    </div>

    <div class="meter-wrap">
      <div class="meter-label">🌋 Yellowstone Supervolcano eruption · this century</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-ok" style="width:2%"></div></div>
      <div class="meter-pct">~0.1–0.15% · Would plunge Earth into a volcanic winter. Agriculture collapses for years. No warning beyond months.</div>
    </div>

    <div class="meter-wrap">
      <div class="meter-label">☀ Coronal Mass Ejection (Carrington-scale) · this century</div>
      <div class="meter-bar-bg"><div class="meter-bar bar-warn" style="width:12%"></div></div>
      <div class="meter-pct">~12% · Not an extinction event, but would destroy power grids globally. Modern civilisation runs on electricity. Do the maths.</div>
    </div>

    <div class="callout">
      <div class="callout-head">⭐ The Fermi Paradox (A Note)</div>
      The galaxy should, statistically, be teeming with intelligent life. It appears to be silent. One explanation — the "Great Filter" — suggests that some barrier to civilisation's long-term survival exists, and we may not yet have passed it. This is either behind us (the emergence of complex life was the hard part) or ahead of us. We are rooting for the former.
    </div>

    <div class="callout">
      <div class="callout-head">🌋 Supervolcano: What Happens</div>
      The Toba eruption 74,000 years ago reduced the human population to an estimated <strong>3,000–10,000 individuals</strong> — a genetic bottleneck still visible in human DNA today. A comparable event today would eject enough ash and sulphur dioxide to block sunlight globally for 3–10 years. The resulting crop failure would kill billions. There is no meaningful preparedness strategy for the individual. Humanity's survival would depend on centralised food stores and extraordinary international cooperation. These are not our strongest characteristics.
    </div>

    <div class="footnote">
      On a long enough timeline, everything ends. The sun will expand into a red giant in approximately 5 billion years, rendering Earth uninhabitable. This is not the kind of problem this guide is designed to help with. We recommend worrying about the nearer-term entries first. · FM-0000
    </div>
  </div>

  <!-- SURVIVAL CALCULATOR -->
  <div class="chapter" id="ch-survival">
    <div class="ch-eyebrow">Final Chapter · Assessment</div>
    <h1 class="ch-title">Your Personal<br>Odds</h1>
    <div class="ch-subtitle">A wholly unscientific but earnestly meant survival calculator</div>

    <p class="body-text">Based on your circumstances, let us calculate your approximate probability of surviving the next century. Adjust the sliders honestly. The guide is not judging you. The apocalypse, however, will.</p>

    <div class="calc-grid">
      <div class="calc-item">
        <label>DISTANCE FROM MAJOR CITY (km)</label>
        <input type="range" min="0" max="500" value="50" id="s-dist" oninput="updateCalc()">
        <div class="calc-val" id="v-dist">50 km</div>
      </div>
      <div class="calc-item">
        <label>MONTHS OF FOOD STORED</label>
        <input type="range" min="0" max="24" value="0" id="s-food" oninput="updateCalc()">
        <div class="calc-val" id="v-food">0 months</div>
      </div>
      <div class="calc-item">
        <label>PRACTICAL SKILLS (1-10)</label>
        <input type="range" min="1" max="10" value="3" id="s-skills" oninput="updateCalc()">
        <div class="calc-val" id="v-skills">3/10</div>
      </div>
      <div class="calc-item">
        <label>GROUP SIZE (people you trust)</label>
        <input type="range" min="1" max="20" value="3" id="s-group" oninput="updateCalc()">
        <div class="calc-val" id="v-group">3 people</div>
      </div>
      <div class="calc-item">
        <label>ACCESS TO CLEAN WATER (km to source)</label>
        <input type="range" min="0" max="50" value="5" id="s-water" oninput="updateCalc()">
        <div class="calc-val" id="v-water">5 km</div>
      </div>
      <div class="calc-item">
        <label>MEDICAL KNOWLEDGE (1-10)</label>
        <input type="range" min="1" max="10" value="2" id="s-med" oninput="updateCalc()">
        <div class="calc-val" id="v-med">2/10</div>
      </div>
    </div>

    <div class="result-box" id="result-box">
      <span class="big-num" id="result-pct">--</span>
      <div class="result-label">ESTIMATED SURVIVAL PROBABILITY</div>
      <div class="verdict" id="result-verdict">Adjust the sliders above.</div>
    </div>

    <div class="divider"><span>final words</span></div>

    <p class="body-text">The purpose of this guide is not to induce despair. It is to induce <strong>appropriate seriousness</strong>. The risks are real. They are manageable, at least in principle. The question is whether humanity can summon the collective will to manage them before they manage us.</p>

    <p class="body-text">The good news: <strong>every one of these scenarios can be reduced in probability</strong> through collective action, sensible policy, and individual preparedness. The bad news: these require cooperation among humans, which is historically our least reliable characteristic.</p>

    <div class="callout">
      <div class="callout-head">✦ The Final Checklist</div>
      Vote for people who take existential risks seriously. Support international institutions even when they're imperfect. Know your neighbours. Store some food. Learn something useful. Spend time with people you love. The apocalypse may or may not come. Life, with considerable certainty, will end. Make it count.
    </div>

    <p style="text-align:center; margin-top:36px">
      <span class="stamp green">You Are Briefed</span>
      <span class="stamp red">Godspeed</span>
    </p>

    <div class="footnote">
      This guide was produced in good faith. The authors accept no liability for apocalypses arising from failure to follow its advice, from following its advice incorrectly, or from the fundamental unpredictability of civilisational collapse. Thank you for reading. Destroy after memorisation. · Field Manual FM-0000 · ENDS
    </div>
  </div>

</div><!-- /book -->

<script>
function openBook() {
  document.getElementById('cover').classList.add('gone');
  const book = document.getElementById('book');
  book.style.display = 'block';
  setTimeout(() => book.classList.add('open'), 50);
}

function showChapter(name, btn) {
  document.querySelectorAll('.chapter').forEach(c => c.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('ch-' + name).classList.add('active');
  btn.classList.add('active');
  document.getElementById('book').scrollTop = 0;
  window.scrollTo(0,0);
}

function toggleCheck(el) {
  el.classList.toggle('checked');
  el.textContent = el.classList.contains('checked') ? '✓' : '';
}

const apocInfo = {
  nuclear: "Nuclear war remains one of the most studied and genuinely alarming risks. The Cold War saw dozens of near-misses, several of which were only averted by individual human decisions to not follow protocol. Navigate to the Nuclear chapter for the full briefing.",
  pandemic: "Engineered pathogens represent a growing concern as biotechnology becomes cheaper and more accessible. Unlike nuclear weapons, bioweapons do not require state resources to develop. The pandemic chapter covers preparedness and the scale of realistic threat.",
  climate: "Climate change is the only catastrophe on this list already underway. It is unlikely to cause extinction directly — but it dramatically increases the risk of every other entry in this guide. See the Climate chapter.",
  ai: "Artificial intelligence risk is contested but taken seriously by a substantial fraction of researchers in the field, including many of its founders. The concern is not science fiction — it is about the difficulty of specifying human values in mathematical terms. See the AI chapter.",
  asteroid: "A civilisation-ending asteroid impact is the lowest-probability risk on this list, but one of the few that could be detected in advance and — with sufficient preparation — potentially deflected. NASA's DART mission successfully altered an asteroid's orbit in 2022.",
  super: "A supervolcanic eruption on the scale of the Toba event 74,000 years ago nearly ended the human species. Yellowstone last erupted approximately 640,000 years ago. It will erupt again. The timing is not predictable to within a human lifetime."
};

function selectApoc(el, key) {
  document.querySelectorAll('.apoc-card').forEach(c => c.classList.remove('selected'));
  el.classList.add('selected');
  document.getElementById('apoc-detail').textContent = apocInfo[key];
}

function updateCalc() {
  const dist = +document.getElementById('s-dist').value;
  const food = +document.getElementById('s-food').value;
  const skills = +document.getElementById('s-skills').value;
  const group = +document.getElementById('s-group').value;
  const water = +document.getElementById('s-water').value;
  const med = +document.getElementById('s-med').value;

  document.getElementById('v-dist').textContent = dist + ' km';
  document.getElementById('v-food').textContent = food + ' months';
  document.getElementById('v-skills').textContent = skills + '/10';
  document.getElementById('v-group').textContent = group + ' people';
  document.getElementById('v-water').textContent = water + ' km';
  document.getElementById('v-med').textContent = med + '/10';

  // Rough heuristic score
  let score = 20;
  score += Math.min(dist / 10, 20);
  score += Math.min(food * 2, 20);
  score += skills * 2;
  score += Math.min(group * 1.5, 10);
  score += Math.max(0, 10 - water * 0.5);
  score += med * 1.5;
  score = Math.min(Math.round(score), 95);

  document.getElementById('result-pct').textContent = score + '%';

  let verdict = '';
  if (score < 30) verdict = "Dire. Consider moving to the countryside and learning to grow food.";
  else if (score < 50) verdict = "Below average. You have identified vulnerabilities. Now address them.";
  else if (score < 70) verdict = "Moderate. You would outlast the first wave. The second is less certain.";
  else if (score < 85) verdict = "Good. You have thought about this before, or you are simply lucky.";
  else verdict = "Excellent. Either you are genuinely prepared, or you have been very generous with the sliders.";

  document.getElementById('result-verdict').textContent = verdict;
}
updateCalc();
</script>
</body>
</html>
