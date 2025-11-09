++++++++++.     .....  
........
.........
<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>JACK.LIVE — Single File (I LOVE YOU)</title>
  <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#000;
      --neon:#39ff14;
      --muted:rgba(57,255,20,0.08);
      --panel-bg: rgba(0,0,0,0.6);
      --glass: rgba(255,255,255,0.02);
      --trans: 240ms ease;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:var(--bg);color:var(--neon);font-family:'Share Tech Mono',monospace;-webkit-font-smoothing:antialiased}
    a{color:inherit;text-decoration:none}

    /* BLACK back button top-left */
    .black-btn{
      position:fixed;left:12px;top:10px;z-index:150;display:inline-flex;align-items:center;gap:8px;padding:8px 12px;border-radius:8px;
      background:#000;border:1px solid rgba(255,255,255,0.04);color:var(--neon);font-weight:800;cursor:pointer;backdrop-filter: blur(4px);
      box-shadow:0 8px 26px rgba(0,0,0,0.6);transition:transform var(--trans),box-shadow var(--trans);
    }
    .black-btn:active{transform:translateY(1px)}
    .black-btn .arrow{font-size:16px}
    .black-btn .label{font-size:13px;letter-spacing:1px}

    /* Top center brand */
    header{position:fixed;left:0;right:0;top:12px;z-index:140;display:flex;justify-content:center;pointer-events:none}
    .brand{pointer-events:auto;padding:2px 8px;font-weight:800;letter-spacing:2px;color:var(--neon);text-shadow:0 0 12px rgba(57,255,20,0.08)}

    /* Matrix canvas */
    canvas#matrix{position:fixed;inset:0;z-index:0;display:block}

    main.container{position:relative;z-index:30;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:48px}

    .panel{width:920px;max-width:96%;background:linear-gradient(180deg,var(--glass),transparent);border-radius:12px;padding:26px;border:1px solid var(--muted);box-shadow:0 24px 60px rgba(0,0,0,0.6);backdrop-filter:blur(6px)}
    .title{font-size:64px;text-align:center;margin:6px 0 10px;color:var(--neon);letter-spacing:2px}
    .status{font-size:13px;color:rgba(57,255,20,0.85);text-align:center;margin-bottom:12px}
    .terminal{background:rgba(0,0,0,0.65);border:1px solid var(--muted);padding:12px;border-radius:8px;min-height:120px;color:var(--neon);white-space:pre-wrap;overflow:auto}
    .hint{margin-top:10px;color:rgba(57,255,20,0.6);font-size:13px;text-align:center}

    /* Enter button */
    .enter-btn{position:fixed;right:18px;bottom:18px;z-index:90;display:flex;flex-direction:column;align-items:center;gap:6px;padding:10px;border-radius:10px;background:var(--panel-bg);border:1px solid var(--muted);cursor:pointer;transition:transform var(--trans),box-shadow var(--trans)}
    .enter-btn:hover{box-shadow:0 12px 46px rgba(57,255,20,0.08);transform:translateY(-2px)}
    .enter-top{font-size:18px;font-weight:800}
    .enter-dots{font-size:13px;letter-spacing:2px}
    .enter-plus{font-size:14px;letter-spacing:6px}
    .enter-label{margin-top:6px;padding:8px 18px;border-radius:8px;background:linear-gradient(90deg,rgba(57,255,20,0.06),rgba(0,0,0,0.06));font-weight:900}

    /* second view controls */
    .controls{display:flex;justify-content:center;gap:12px;flex-wrap:wrap;margin-top:18px}
    .ctrl-btn{background:var(--panel-bg);border:1px solid var(--muted);padding:10px 14px;border-radius:8px;font-weight:800;cursor:pointer;min-width:120px;text-align:center;color:var(--neon)}
    .ctrl-btn:hover{transform:translateY(-3px);box-shadow:0 10px 40px rgba(57,255,20,0.06)}

    /* options popup */
    .options{position:fixed;right:18px;bottom:94px;z-index:95;min-width:180px;background:rgba(0,0,0,0.86);border:1px solid var(--muted);padding:10px;border-radius:8px;display:none;flex-direction:column;gap:8px}
    .options.show{display:flex;animation:pop .14s ease-out}
    .options .opt{padding:8px;border-radius:6px;background:linear-gradient(180deg,rgba(57,255,20,0.02),transparent);font-weight:700;color:var(--neon)}
    @keyframes pop{0%{transform:translateY(6px);opacity:0}100%{transform:none;opacity:1}}

    /* settings modal */
    .settings{position:fixed;top:12px;right:14px;z-index:120;cursor:pointer;font-size:20px;padding:6px;border-radius:8px;background:var(--panel-bg);border:1px solid var(--muted)}
    .modal-back{position:fixed;inset:0;background:rgba(0,0,0,0.65);display:none;align-items:center;justify-content:center;z-index:130}
    .modal-back.show{display:flex}
    .modal{background:linear-gradient(180deg,#050507,#0b0b0d);border:1px solid var(--muted);padding:18px;border-radius:10px;min-width:300px;color:var(--neon)}
    .modal h3{margin:0 0 8px}

    /* view switching */
    .view{display:none;opacity:0;transform:translateY(6px);transition:opacity 300ms ease,transform 300ms ease;pointer-events:none}
    .view.active{display:block;opacity:1;transform:none;pointer-events:auto}

    /* I LOVE YOU box */
    .love-wrap{display:flex;align-items:center;justify-content:center;flex-direction:column;padding:32px 10px}
    .love-text{font-size:56px;font-weight:900;letter-spacing:4px;color:var(--neon);text-shadow:0 0 18px rgba(57,255,20,0.14),0 0 36px rgba(57,255,20,0.06);opacity:0}
    .love-text.glow{animation:glowPulse 1500ms ease-in-out infinite alternate;opacity:1}
    @keyframes glowPulse{from{text-shadow:0 0 12px rgba(57,255,20,0.12)} to{text-shadow:0 0 30px rgba(57,255,20,0.35)}}

    /* typing cursor for I LOVE YOU */
    .typing { font-size:56px; font-weight:900; letter-spacing:4px; white-space:pre; }
    .cursor { display:inline-block; width:12px; background:var(--neon); margin-left:6px; animation:blink 900ms steps(2) infinite; vertical-align:middle; height:1.1em; border-radius:2px;}
    @keyframes blink{0%,50%{opacity:1}51%,100%{opacity:0}}

    @media (max-width:820px){
      .title{font-size:36px}
      .panel{padding:18px}
      .enter-btn{right:12px;bottom:12px}
      .black-btn{left:10px;top:8px}
      .love-text,.typing{font-size:32px}
    }
  </style>
</head>
<body>

  <!-- BLACK back button -->
  <button id="blackBtn" class="black-btn" aria-label="Back / Black button">
    <span class="arrow">←</span>
    <span class="label">BLACK</span>
  </button>

  <!-- Brand -->
  <header><div class="brand">JACK.LIVE</div></header>

  <!-- Matrix -->
  <canvas id="matrix"></canvas>

  <main class="container" role="main">
    <!-- HOME VIEW -->
    <section id="homeView" class="view active" aria-label="Home">
      <div class="panel">
        <div class="title">JACK.LIVE</div>
        <div class="status">connection: secure · mode: stealth · port: 443</div>
        <div id="homeTerminal" class="terminal" aria-live="polite" tabindex="0"></div>
        <div class="hint">Press <kbd>Enter</kbd> or touch the button to open control panel · Esc to clear</div>
      </div>
    </section>

    <!-- SECOND VIEW -->
    <section id="secondView" class="view" aria-label="Control Panel">
      <div class="panel">
        <div style="text-align:center;font-size:30px;font-weight:900;margin-bottom:8px">++++++</div>

        <!-- I LOVE YOU animated area -->
        <div class="love-wrap" aria-hidden="false">
          <div id="loveTyping" class="typing" aria-live="polite"></div><div id="loveCursor" class="cursor" aria-hidden="true"></div>
          <div id="loveGlow" class="love-text" style="margin-top:18px">I LOVE YOU</div>
        </div>

        <div class="controls" id="secondControls">
          <button class="ctrl-btn" id="btnBack">←</button>
          <button class="ctrl-btn" id="btnDots">.........</button>
          <button class="ctrl-btn" id="btnPlus">++++++</button>
          <button class="ctrl-btn" id="btnEntar">ENTAR</button>
        </div>

        <div class="hint">Settings (⚙️) on top-right · Click BLACK ← to go home</div>
      </div>
    </section>
  </main>

  <!-- Enter button -->
  <div id="enterBtn" class="enter-btn" role="button" tabindex="0" aria-label="ENTAR button">
    <div class="enter-top" aria-hidden>←</div>
    <div class="enter-dots" aria-hidden>.........</div>
    <div class="enter-plus" aria-hidden>++++++</div>
    <div class="enter-label" aria-hidden>ENTAR</div>
  </div>

  <!-- options popup -->
  <div id="options" class="options" role="menu" aria-hidden="true">
    <div class="opt">← (Back Arrow)</div>
    <div class="opt">......... (Dots)</div>
    <div class="opt">++++++ (Pluses)</div>
    <div class="opt">ENTAR (Trigger)</div>
  </div>

  <!-- settings -->
  <div id="settingsBtn" class="settings" title="Settings">⚙️</div>
  <div id="modal" class="modal-back" role="dialog" aria-modal="true" aria-hidden="true">
    <div class="modal" role="document">
      <h3>Settings</h3>
      <p style="margin:6px 0 12px;color:#9fdca8">Theme & behavior</p>
      <div style="display:flex;gap:10px;flex-wrap:wrap">
        <button class="ctrl-btn" id="optMatrixToggle">Toggle Matrix</button>
        <button class="ctrl-btn" id="optSpeed">Speed x1</button>
        <button class="ctrl-btn" id="optTheme">Light / Dark</button>
        <button class="ctrl-btn" id="closeModal">Close</button>
      </div>
    </div>
  </div>

<script>
/* ---------------- Matrix rain ---------------- */
const canvas = document.getElementById('matrix'), ctx = canvas.getContext('2d');
let w = canvas.width = innerWidth, h = canvas.height = innerHeight;
let cols = Math.floor(w / 16), drops = Array(cols).fill(1);
let matrixInterval = null, matrixSpeed = 45, matrixOn = true;
function drawMatrix(){
  ctx.fillStyle = 'rgba(0,0,0,0.13)';
  ctx.fillRect(0,0,w,h);
  ctx.fillStyle = 'rgba(57,255,20,0.55)';
  ctx.font = '14px "Share Tech Mono"';
  for(let i=0;i<drops.length;i++){
    const text = String.fromCharCode(33 + Math.random()*94);
    ctx.fillText(text, i * 16, drops[i] * 16);
    if(drops[i] * 16 > h && Math.random() > 0.975) drops[i] = 0;
    drops[i]++;
  }
}
function startMatrix(){ if(matrixInterval) clearInterval(matrixInterval); matrixInterval = setInterval(drawMatrix, matrixSpeed); }
startMatrix();
addEventListener('resize', ()=>{ w = canvas.width = innerWidth; h = canvas.height = innerHeight; cols = Math.floor(w/16); drops = Array(cols).fill(1); });

/* ---------- Terminal typing ---------- */
const homeTerminal = document.getElementById('homeTerminal');
const lines = [
  'Initializing JACK.LIVE secure shell...',
  'Authenticating ••• success',
  'Mounting virtual overlay [ok]',
  'Syncing nodes: 12/12',
  'Decrypting payload... [complete]',
  '[ACCESS GRANTED] Welcome, operator.'
];
let li = 0, ci = 0, typing = false;
function resetTyping(){ li=0; ci=0; homeTerminal.textContent=''; typing=false; }
function typeStep(){
  typing = true;
  if(li >= lines.length){ typing=false; return; }
  const line = lines[li];
  if(ci <= line.length){
    homeTerminal.textContent = lines.slice(0,li).join('\n') + (li? '\n':'') + line.slice(0,ci) + '█';
    ci++; setTimeout(typeStep, 40 + Math.random()*60);
  } else {
    ci=0; li++; setTimeout(typeStep, 600);
  }
}

/* ------------- Views & interactions ------------- */
const homeView = document.getElementById('homeView'), secondView = document.getElementById('secondView');
const enterBtn = document.getElementById('enterBtn'), optionsEl = document.getElementById('options');
const settingsBtn = document.getElementById('settingsBtn'), modal = document.getElementById('modal');
const blackBtn = document.getElementById('blackBtn');

function showOptions(){ optionsEl.classList.add('show'); optionsEl.setAttribute('aria-hidden','false'); clearTimeout(window._optTimeout); window._optTimeout = setTimeout(()=>{ optionsEl.classList.remove('show'); optionsEl.setAttribute('aria-hidden','true'); }, 3500); }

/* open second both: same-page + new tab with #second */
function openSecondBoth(){
  homeView.classList.remove('active'); secondView.classList.add('active');
  document.title = '++++++ — Control Panel';
  showOptions();
  try{ const url = location.href.split('#')[0] + '#second'; window.open(url, '_blank'); }catch(e){}
}

/* show second only (if loaded with hash) */
function showSecondOnly(){ homeView.classList.remove('active'); secondView.classList.add('active'); document.title = '++++++ — Control Panel'; }

/* run sequence (terminal typing + options) */
function runSequence(){ if(typing) return; resetTyping(); typeStep(); showOptions(); }

/* keyboard handlers */
addEventListener('keydown', (e)=>{
  if(e.key === 'Enter'){ runSequence(); }
  else if(e.key === 'Escape'){ resetTyping(); optionsEl.classList.remove('show'); optionsEl.setAttribute('aria-hidden','true'); closeModal(); }
});

/* Enter click => typing + open second both after short delay */
enterBtn.addEventListener('click', ()=>{
  runSequence();
  setTimeout(()=>{ openSecondBoth(); startLoveTyping(); }, 600);
});
enterBtn.addEventListener('keydown', (e)=>{ if(e.key==='Enter' || e.key===' ') { e.preventDefault(); enterBtn.click(); } });

/* second view buttons */
document.getElementById('btnBack').addEventListener('click', ()=>{ secondView.classList.remove('active'); homeView.classList.add('active'); document.title = 'JACK.LIVE'; });
document.getElementById('btnDots').addEventListener('click', ()=> alert('Dots pressed'));
document.getElementById('btnPlus').addEventListener('click', ()=> alert('Pluses pressed'));
document.getElementById('btnEntar').addEventListener('click', ()=> { alert('ENTAR activated on second page'); });

/* Settings modal */
settingsBtn.addEventListener('click', ()=>{ modal.classList.add('show'); modal.setAttribute('aria-hidden','false'); });
document.getElementById('closeModal').addEventListener('click', closeModal);
function closeModal(){ modal.classList.remove('show'); modal.setAttribute('aria-hidden','true'); }

/* settings toggles */
let speedStage = 1;
document.getElementById('optMatrixToggle').addEventListener('click', ()=>{
  matrixOn = !matrixOn;
  if(!matrixOn){ clearInterval(matrixInterval); ctx.clearRect(0,0,w,h); } else startMatrix();
});
document.getElementById('optSpeed').addEventListener('click', (e)=>{
  speedStage = (speedStage % 3) + 1;
  matrixSpeed = Math.max(12, 45 / speedStage);
  e.target.textContent = 'Speed x' + speedStage;
  if(matrixOn) startMatrix();
});
document.getElementById('optTheme').addEventListener('click', ()=>{
  const root = document.documentElement;
  if(root.getAttribute('data-theme') === 'light'){ root.removeAttribute('data-theme'); localStorage.setItem('jt-theme','dark'); }
  else{ root.setAttribute('data-theme','light'); localStorage.setItem('jt-theme','light'); }
});

/* black button behavior: always go home on click (if second active) otherwise pulse */
blackBtn.addEventListener('click', ()=>{
  if(secondView.classList.contains('active')){
    secondView.classList.remove('active'); homeView.classList.add('active'); document.title = 'JACK.LIVE';
  } else {
    blackBtn.style.transform = 'scale(0.98)'; setTimeout(()=>{ blackBtn.style.transform='none'; },120);
  }
});

/* If opened with #second show second only */
if(location.hash === '#second'){ showSecondOnly(); }

/* initial glitch */
const glitch = document.querySelector('.title'); let gcount = 0;
const gint = setInterval(()=>{ if(glitch){ glitch.style.transform = `translate(${(Math.random()-0.5)*6}px, ${(Math.random()-0.5)*4}px)`; gcount++; if(gcount>6){ clearInterval(gint); if(glitch) glitch.style.transform = 'none'; } } },90);

/* Save theme */
if(localStorage.getItem('jt-theme') === 'light'){ document.documentElement.setAttribute('data-theme','light'); }

/* ---------- I LOVE YOU typing + glow ---------- */
const loveText = 'I LOVE YOU';
const loveEl = document.getElementById('loveTyping');
const loveCursor = document.getElementById('loveCursor');
const loveGlow = document.getElementById('loveGlow');
let lci = 0, loveTypingRunning = false;

function startLoveTyping(){
  // reset
  lci = 0; loveEl.textContent = ''; loveGlow.style.opacity = 0; loveCursor.style.display = 'inline-block'; loveTypingRunning = true;
  typeLove();
}
function typeLove(){
  if(lci <= loveText.length){
    loveEl.textContent = loveText.slice(0, lci);
    lci++;
    setTimeout(typeLove, 140);
  } else {
    // finished, show glowing static text and hide cursor
    loveCursor.style.display = 'none';
    loveGlow.classList.add('glow');
    // small pulse in case user returns
    setTimeout(()=>{ loveGlow.style.opacity = 1; }, 150);
    loveTypingRunning = false;
  }
}

/* Accessibility: allow pressing Enter on second view ENTAR to retrigger love animation */
document.getElementById('btnEntar').addEventListener('click', ()=>{ startLoveTyping(); });

/* focusable terminal */
homeTerminal.addEventListener('focus', ()=>{ /* no-op */ });

</script>
</body>
</html>

