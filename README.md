<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mohammed Azarin V P — AzarCodex</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Bebas+Neue&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #030712;
    --surface: #0d1117;
    --border: #1e2d3d;
    --accent: #00d4ff;
    --accent2: #ff3cac;
    --accent3: #7b2fff;
    --text: #e6edf3;
    --muted: #7d8590;
    --glow: 0 0 40px rgba(0,212,255,0.3);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.1s;
    mix-blend-mode: difference;
  }
  .cursor-trail {
    width: 36px; height: 36px;
    border: 1px solid var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: all 0.15s ease;
    opacity: 0.5;
  }

  /* CANVAS BG */
  #canvas-bg {
    position: fixed; inset: 0;
    z-index: 0; opacity: 0.6;
  }

  /* MAIN */
  main {
    position: relative; z-index: 1;
    max-width: 900px;
    margin: 0 auto;
    padding: 80px 24px;
  }

  /* HERO */
  .hero {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 40px;
    align-items: center;
    margin-bottom: 80px;
    opacity: 0;
    transform: translateY(30px);
    animation: fadeUp 0.8s 0.2s forwards;
  }

  .status-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    border: 1px solid var(--border);
    padding: 6px 14px;
    border-radius: 100px;
    margin-bottom: 20px;
    background: rgba(0,212,255,0.05);
  }
  .status-dot {
    width: 6px; height: 6px;
    background: #22c55e;
    border-radius: 50%;
    animation: pulse 2s infinite;
  }

  h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(52px, 8vw, 96px);
    line-height: 0.95;
    letter-spacing: 2px;
    margin-bottom: 8px;
  }

  h1 .name-gradient {
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent3) 50%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: gradShift 4s ease infinite alternate;
    background-size: 200%;
  }

  .role-line {
    font-family: 'Space Mono', monospace;
    font-size: 13px;
    color: var(--muted);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 24px;
  }
  .role-line span {
    color: var(--accent2);
  }

  .hero-quote {
    font-size: 15px;
    color: var(--muted);
    line-height: 1.7;
    border-left: 2px solid var(--accent3);
    padding-left: 16px;
    font-style: italic;
    max-width: 480px;
  }

  /* AVATAR */
  .avatar-wrapper {
    position: relative;
    width: 140px; height: 140px;
    flex-shrink: 0;
    opacity: 0;
    animation: fadeIn 0.8s 0.5s forwards;
  }
  .avatar-ring {
    position: absolute; inset: -12px;
    border-radius: 50%;
    background: conic-gradient(var(--accent), var(--accent3), var(--accent2), var(--accent));
    animation: spin 4s linear infinite;
    opacity: 0.7;
  }
  .avatar-ring-inner {
    position: absolute; inset: -6px;
    border-radius: 50%;
    background: var(--bg);
  }
  .avatar-inner {
    position: relative;
    width: 100%; height: 100%;
    background: linear-gradient(135deg, #0d1117, #1e2d3d);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 48px;
    background: linear-gradient(135deg, var(--accent), var(--accent3));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .avatar-inner-bg {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #0d1117, #131b2e);
    border-radius: 50%;
  }
  .avatar-letter {
    position: relative;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 56px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  /* SECTION */
  section {
    margin-bottom: 64px;
    opacity: 0;
    transform: translateY(24px);
    animation: fadeUp 0.7s forwards;
  }
  section:nth-child(2) { animation-delay: 0.4s; }
  section:nth-child(3) { animation-delay: 0.55s; }
  section:nth-child(4) { animation-delay: 0.7s; }
  section:nth-child(5) { animation-delay: 0.85s; }
  section:nth-child(6) { animation-delay: 1s; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  /* SPECIALIZATION PILLS */
  .tags {
    display: flex; flex-wrap: wrap; gap: 10px;
  }
  .tag {
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    padding: 8px 18px;
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    background: rgba(255,255,255,0.03);
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .tag::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, var(--accent), var(--accent3));
    opacity: 0;
    transition: opacity 0.3s;
  }
  .tag:hover::before { opacity: 0.12; }
  .tag:hover {
    border-color: var(--accent);
    box-shadow: 0 0 20px rgba(0,212,255,0.15);
    transform: translateY(-2px);
  }
  .tag span { position: relative; }

  /* TERMINAL CARD */
  .terminal {
    background: #0a0f16;
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    font-family: 'Space Mono', monospace;
    font-size: 13px;
  }
  .terminal-header {
    background: #111820;
    padding: 12px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid var(--border);
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.r { background: #ff5f57; }
  .dot.y { background: #febc2e; }
  .dot.g { background: #28c840; }
  .terminal-title {
    margin-left: auto;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 1px;
  }
  .terminal-body {
    padding: 24px;
    line-height: 2;
  }
  .t-comment { color: #3d5166; }
  .t-key { color: var(--accent2); }
  .t-val { color: #a5d6ff; }
  .t-str { color: #7ee787; }
  .t-num { color: #f2cc60; }
  .t-bracket { color: var(--muted); }
  .t-cursor {
    display: inline-block;
    width: 8px; height: 14px;
    background: var(--accent);
    animation: blink 1s infinite;
    vertical-align: middle;
    margin-left: 2px;
  }

  /* MISSION CARD */
  .mission-card {
    background: linear-gradient(135deg, rgba(0,212,255,0.05), rgba(123,47,255,0.05));
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 28px;
    position: relative;
    overflow: hidden;
  }
  .mission-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    animation: scanline 3s ease infinite;
  }
  .mission-text {
    font-size: 15px;
    line-height: 1.8;
    color: #c9d1d9;
  }
  .mission-highlight {
    color: var(--accent);
    font-family: 'Space Mono', monospace;
  }

  /* SOCIAL LINKS */
  .socials {
    display: flex; gap: 14px; flex-wrap: wrap;
  }
  .social-link {
    display: flex; align-items: center; gap: 10px;
    padding: 12px 22px;
    border: 1px solid var(--border);
    border-radius: 8px;
    text-decoration: none;
    color: var(--text);
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    transition: all 0.3s;
    background: rgba(255,255,255,0.02);
    position: relative;
    overflow: hidden;
  }
  .social-link::after {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, var(--accent), var(--accent3));
    opacity: 0;
    transition: opacity 0.3s;
  }
  .social-link:hover {
    border-color: var(--accent);
    transform: translateY(-3px);
    box-shadow: 0 8px 30px rgba(0,212,255,0.2);
  }
  .social-link:hover::after { opacity: 0.08; }
  .social-link svg, .social-link .sicon { position: relative; }
  .social-link span { position: relative; }

  /* STATS BAR */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
  .stat-box {
    background: rgba(255,255,255,0.02);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px;
    text-align: center;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .stat-box:hover {
    border-color: var(--accent3);
    box-shadow: 0 0 30px rgba(123,47,255,0.15);
    transform: translateY(-4px);
  }
  .stat-box::before {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent3), var(--accent));
    transform: scaleX(0);
    transition: transform 0.3s;
  }
  .stat-box:hover::before { transform: scaleX(1); }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 36px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
    margin-bottom: 6px;
  }
  .stat-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  /* LOCATION */
  .location-pill {
    display: inline-flex; align-items: center; gap: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    color: var(--muted);
    padding: 8px 16px;
    border: 1px solid var(--border);
    border-radius: 100px;
    background: rgba(255,255,255,0.02);
  }
  .location-dot {
    width: 8px; height: 8px;
    background: var(--accent2);
    border-radius: 50%;
    animation: pulse 2s infinite;
  }

  /* FOOTER */
  footer {
    text-align: center;
    padding: 40px 0 20px;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: #3d5166;
    opacity: 0;
    animation: fadeIn 1s 1.2s forwards;
  }
  footer span { color: var(--accent2); }

  /* FLOATING PARTICLES */
  .particles { position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden; }
  .particle {
    position: absolute;
    width: 2px; height: 2px;
    background: var(--accent);
    border-radius: 50%;
    animation: floatUp linear infinite;
    opacity: 0;
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    to { opacity: 1; }
  }
  @keyframes gradShift {
    0% { background-position: 0% 50%; }
    100% { background-position: 100% 50%; }
  }
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.6; transform: scale(1.3); }
  }
  @keyframes scanline {
    0% { transform: scaleX(0); transform-origin: left; }
    50% { transform: scaleX(1); transform-origin: left; }
    50.01% { transform-origin: right; }
    100% { transform: scaleX(0); transform-origin: right; }
  }
  @keyframes floatUp {
    0% { transform: translateY(100vh) translateX(0); opacity: 0; }
    10% { opacity: 0.6; }
    90% { opacity: 0.3; }
    100% { transform: translateY(-100px) translateX(100px); opacity: 0; }
  }

  @media (max-width: 600px) {
    .hero { grid-template-columns: 1fr; }
    .avatar-wrapper { display: none; }
    .stats-grid { grid-template-columns: 1fr 1fr; }
    h1 { font-size: 56px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-trail" id="cursorTrail"></div>

<canvas id="canvas-bg"></canvas>
<div class="particles" id="particles"></div>

<main>
  <!-- HERO -->
  <div class="hero">
    <div>
      <div class="status-badge">
        <span class="status-dot"></span>
        AVAILABLE FOR OPPORTUNITIES
      </div>
      <h1>
        <span class="name-gradient">AZARIN</span><br>
        <span style="color: var(--text); font-size: 0.55em; letter-spacing: 6px; font-family: 'DM Sans', sans-serif; font-weight: 300;">MOHAMMED AZARIN V P</span>
      </h1>
      <p class="role-line">Software Engineer <span>·</span> AzarCodex <span>·</span> India</p>
      <p class="hero-quote">"Code is poetry, debugging is the art of understanding the poet's mind."</p>
    </div>
    <div class="avatar-wrapper">
      <div class="avatar-ring"></div>
      <div class="avatar-ring-inner"></div>
      <div class="avatar-inner">
        <div class="avatar-inner-bg"></div>
        <span class="avatar-letter">AZ</span>
      </div>
    </div>
  </div>

  <!-- API TERMINAL -->
  <section>
    <p class="section-label">// system info</p>
    <div class="terminal">
      <div class="terminal-header">
        <div class="dot r"></div>
        <div class="dot y"></div>
        <div class="dot g"></div>
        <span class="terminal-title">GET /api/v1/users/azarcodex</span>
      </div>
      <div class="terminal-body">
        <div><span class="t-comment">// 200 OK — user found</span></div>
        <div><span class="t-bracket">{</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"name"</span>: <span class="t-str">"Mohammed Azarin V P"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"role"</span>: <span class="t-str">"Software Engineer"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"stack"</span>: <span class="t-bracket">[</span><span class="t-str">"Backend Architecture"</span>, <span class="t-str">"Scalable Systems"</span>, <span class="t-str">"Full Stack"</span><span class="t-bracket">]</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"location"</span>: <span class="t-str">"India 🇮🇳"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"status"</span>: <span class="t-str">"solving_complex_problems"</span></div>
        <div><span class="t-bracket">}</span><span class="t-cursor"></span></div>
      </div>
    </div>
  </section>

  <!-- MISSION -->
  <section>
    <p class="section-label">// current mission</p>
    <div class="mission-card">
      <p class="mission-text">
        Building <span class="mission-highlight">scalable backend systems</span> that can handle real-world complexity. 
        I architect solutions that are not just functional — they're resilient, performant, and 
        <span class="mission-highlight">built to last</span>. From microservices to full-stack applications, 
        every line of code is written with purpose.
      </p>
    </div>
  </section>

  <!-- SPECIALIZATIONS -->
  <section>
    <p class="section-label">// specializations</p>
    <div class="tags">
      <div class="tag"><span>⚡ Backend Architecture</span></div>
      <div class="tag"><span>🏗️ Scalable Systems</span></div>
      <div class="tag"><span>🌐 Full Stack</span></div>
      <div class="tag"><span>🔧 System Design</span></div>
      <div class="tag"><span>🚀 API Development</span></div>
      <div class="tag"><span>📦 Distributed Systems</span></div>
    </div>
  </section>

  <!-- STATS -->


  <!-- LOCATION -->
  <section>
    <p class="section-label">// location</p>
    <div class="location-pill">
      <span class="location-dot"></span>
      India — Available Remotely Worldwide
    </div>
  </section>

  <!-- SOCIALS -->
  <section>
    <p class="section-label">// connect</p>
    <div class="socials">
      <a class="social-link" href="https://www.linkedin.com/in/mohammed-azarin-v-p-0571bb239/" target="_blank">
        <span class="sicon">💼</span>
        <span>linkedin / mohammed-azarin-v-p</span>
      </a>
      <a class="social-link" href="https://x.com/AzarCodex" target="_blank">
        <span class="sicon">𝕏</span>
        <span>@AzarCodex</span>
      </a>
    </div>
  </section>

  <footer>
    crafted by <span>AzarCodex</span> · built with 🔥 and precision · © 2024
  </footer>
</main>

<script>
// CURSOR
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursorTrail');
let mx = -100, my = -100, tx = -100, ty = -100;

document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });

function animCursor() {
  cursor.style.transform = `translate(${mx - 6}px, ${my - 6}px)`;
  tx += (mx - tx) * 0.12;
  ty += (my - ty) * 0.12;
  trail.style.transform = `translate(${tx - 18}px, ${ty - 18}px)`;
  requestAnimationFrame(animCursor);
}
animCursor();

document.querySelectorAll('a, .tag, .stat-box, .social-link').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform += ' scale(2)';
    trail.style.transform += ' scale(1.5)';
  });
  el.addEventListener('mouseleave', () => {});
});

// CANVAS BACKGROUND
const canvas = document.getElementById('canvas-bg');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const nodes = [];
for (let i = 0; i < 80; i++) {
  nodes.push({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    vx: (Math.random() - 0.5) * 0.4,
    vy: (Math.random() - 0.5) * 0.4,
    r: Math.random() * 2 + 0.5
  });
}

function drawCanvas() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  nodes.forEach(n => {
    n.x += n.vx; n.y += n.vy;
    if (n.x < 0 || n.x > canvas.width) n.vx *= -1;
    if (n.y < 0 || n.y > canvas.height) n.vy *= -1;
    ctx.beginPath();
    ctx.arc(n.x, n.y, n.r, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(0,212,255,0.5)';
    ctx.fill();
  });
  for (let i = 0; i < nodes.length; i++) {
    for (let j = i + 1; j < nodes.length; j++) {
      const dx = nodes[i].x - nodes[j].x;
      const dy = nodes[i].y - nodes[j].y;
      const d = Math.sqrt(dx*dx + dy*dy);
      if (d < 120) {
        ctx.beginPath();
        ctx.moveTo(nodes[i].x, nodes[i].y);
        ctx.lineTo(nodes[j].x, nodes[j].y);
        ctx.strokeStyle = `rgba(0,212,255,${(1 - d/120) * 0.15})`;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
  requestAnimationFrame(drawCanvas);
}
drawCanvas();

window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});

// PARTICLES
const pContainer = document.getElementById('particles');
for (let i = 0; i < 25; i++) {
  const p = document.createElement('div');
  p.className = 'particle';
  p.style.left = Math.random() * 100 + 'vw';
  p.style.animationDuration = (Math.random() * 15 + 10) + 's';
  p.style.animationDelay = (Math.random() * 15) + 's';
  p.style.width = p.style.height = (Math.random() * 3 + 1) + 'px';
  if (Math.random() > 0.5) p.style.background = 'var(--accent2)';
  if (Math.random() > 0.7) p.style.background = 'var(--accent3)';
  pContainer.appendChild(p);
}
</script>
</body>
</html>
