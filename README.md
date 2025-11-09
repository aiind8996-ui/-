++++++++++.     .....  
    <!doctype html>
<html lang="hi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>JACK.LIVE — I LOVE YOU</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#000;
  --neon:#39ff14;
  --muted:rgba(57,255,20,0.08);
}
*{box-sizing:border-box;margin:0;padding:0}
body{
  height:100vh;
  overflow:hidden;
  background:var(--bg);
  color:var(--neon);
  font-family:'Share Tech Mono',monospace;
}

/* top buttons */
.black-btn{
  position:fixed;top:10px;left:10px;
  background:black;color:var(--neon);
  border:1px solid var(--neon);
  border-radius:8px;
  padding:6px 12px;
  font-weight:bold;
  font-size:14px;
  display:flex;align-items:center;gap:6px;
  z-index:100;
}
header{position:fixed;top:10px;left:0;right:0;text-align:center;z-index:99;}
.brand{font-weight:bold;font-size:18px;letter-spacing:2px;color:var(--neon);}

/* Matrix */
canvas#matrix{position:fixed;inset:0;z-index:0;display:block}

/* content views */
.view{position:absolute;top:0;left:0;width:100%;height:100%;display:none;align-items:center;justify-content:center;flex-direction:column;padding:20px;text-align:center;z-index:10;}
.view.active{display:flex;animation:fadeIn .5s ease;}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}

.title{font-size:40px;letter-spacing:3px;text-shadow:0 0 10px var(--neon);margin-bottom:8px;}
.status{font-size:12px;margin-bottom:16px;}
.terminal{width:90%;max-width:500px;background:rgba(0,0,0,0.6);border:1px solid var(--muted);padding:10px;border-radius:8px;min-height:100px;text-align:left;white-space:pre-wrap;margin:auto;}
.hint{margin-top:10px;font-size:12px;color:rgba(57,255,20,0.7);}

/* enter button */
.enter-btn{
  position:fixed;bottom:20px;right:20px;
  background:rgba(0,0,0,0.8);
  border:1px solid var(--neon);
  border-radius:10px;
  padding:10px 16px;
  text-align:center;
  box-shadow:0 0 8px rgba(57,255,20,0.3);
  z-index:90;
}
.enter-label{font-size:18px;font-weight:bold;letter-spacing:2px;}

/* second page */
.love-wrap{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:10px;}
.typing{font-size:32px;font-weight:bold;letter-spacing:3px;}
.cursor{display:inline-block;width:8px;height:1em;background:var(--neon);animation:blink 1s steps(2) infinite;vertical-align:middle;}
@keyframes blink{0%,50%{opacity:1}51%,100%{opacity:0}}
.love-text{font-size:32px;font-weight:900;letter-spacing:3px;color:var(--neon);opacity:0;}
.love-text.glow{animation:glow 1.5s ease-in-out infinite alternate;opacity:1;}
@keyframes glow{from{text-shadow:0 0 8px var(--neon)}to{text-shadow:0 0 20px var(--neon)}}

.controls{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-top:10px;}
.ctrl-btn{
  background:rgba(0,0,0,0.7);
  border:1px solid var(--neon);
  border-radius:6px;
  padding:8px 16px;
  font-weight:bold;
  color:var(--neon);
  cursor:pointer;
  font-size:14px;
}
.ctrl-btn:active{transform:scale(0.97);}

/* responsive tweak */
@media(max-width:480px){
  .title{font-size:28px;}
  .typing,.love-text{font-size:24px;}
  .enter-label{font-size:16px;}
}
</style>
</head>
<body>

<canvas id="matrix"></canvas>

<button id="blackBtn" class="black-btn"><span>←</span><span>BLACK</span></button>
<header><div class="brand">JACK.LIVE</div></header>

<!-- 🟢 Home View -->
<section id="homeView" class="view active">
  <div class="title">JACK.LIVE</div>
  <div class="status">connection: secure · mode: stealth</div>
  <div id="terminal" class="terminal"></div>
  <div class="hint">Tap ENTAR to continue</div>
</section>

<!-- 🟢 Second View -->
<section id="secondView" class="view">
  <div style="font-size:24px;margin-bottom:6px;">++++++</div>
  <div class="love-wrap">
    <div id="loveTyping" class="typing"></div><div id="loveCursor" class="cursor"></div>
    <div id="loveGlow" class="love-text">I LOVE YOU</div>
  </div>
  <div class="controls">
    <button class="ctrl-btn" id="btnBack">←</button>
    <button class="ctrl-btn">.........</button>
    <button class="ctrl-btn">++++++</button>
    <button class="ctrl-btn" id="btnEntar">ENTAR</button>
  </div>
</section>

<!-- 🟢 Enter Button (First Page) -->
<div id="enterBtn" class="enter-btn"><div class="enter-label">ENTAR</div></div>

<script>
// 🟢 Matrix animation
const canvas=document.getElementById('matrix'),ctx=canvas.getContext('2d');
let w=canvas.width=innerWidth,h=canvas.height=innerHeight;
let cols=Math.floor(w/14),drops=Array(cols).fill(1);
function drawMatrix(){
  ctx.fillStyle='rgba(0,0,0,0.15)';
  ctx.fillRect(0,0,w,h);
  ctx.fillStyle='rgba(57,255,20,0.6)';
  ctx.font='14px monospace';
  for(let i=0;i<drops.length;i++){
    const ch=String.fromCharCode(33+Math.random()*94);
    ctx.fillText(ch,i*14,drops[i]*14);
    if(drops[i]*14>h&&Math.random()>0.975)drops[i]=0;
    drops[i]++;
  }
}
setInterval(drawMatrix,50);
addEventListener('resize',()=>{w=canvas.width=innerWidth;h=canvas.height=innerHeight;cols=Math.floor(w/14);drops=Array(cols).fill(1);});

// 🟢 View switching
const home=document.getElementById('homeView');
const second=document.getElementById('secondView');
const enter=document.getElementById('enterBtn');
const back=document.getElementById('blackBtn');
const btnBack=document.getElementById('btnBack');
const btnEntar=document.getElementById('btnEntar');

function showSecond(){
  home.classList.remove('active');
  second.classList.add('active');
}
function showHome(){
  second.classList.remove('active');
  home.classList.add('active');
}
enter.addEventListener('click',showSecond);
back.addEventListener('click',showHome);
btnBack.addEventListener('click',showHome);

// 🟢 Terminal typing effect
const terminal=document.getElementById('terminal');
const lines=["Initializing JACK.LIVE...","Authenticating...OK","Access granted."];
let li=0,ci=0;
function typeStep(){
  if(li>=lines.length)return;
  const line=lines[li];
  if(ci<=line.length){
    terminal.textContent=lines.slice(0,li).join('\n')+ (li?'\n':'')+ line.slice(0,ci)+'█';
    ci++;setTimeout(typeStep,50);
  }else{ci=0;li++;setTimeout(typeStep,400);}
}
typeStep();

// 🟢 "I LOVE YOU" typing (triggered by 2nd page Enter)
const text="I LOVE YOU";
const love=document.getElementById('loveTyping');
const cursor=document.getElementById('loveCursor');
const glow=document.getElementById('loveGlow');
let i=0;
function startLoveTyping(){
  i=0;love.textContent='';glow.style.opacity=0;cursor.style.display='inline-block';
  function t(){
    if(i<=text.length){love.textContent=text.slice(0,i);i++;setTimeout(t,120);}
    else{cursor.style.display='none';glow.classList.add('glow');glow.style.opacity=1;}
  }t();
}
btnEntar.addEventListener('click',startLoveTyping);
</script>
</body>
</html>
