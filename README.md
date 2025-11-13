................... ................. ................... .................
<!doctype html>
<html lang="hi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>"**" — Shayri Mode</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
:root{
  --bg1:#000;--bg2:#020c0a;--bg3:#002b00;
  --neon:#39ff14;--muted:rgba(57,255,20,0.08);
}
*{box-sizing:border-box;margin:0;padding:0;user-select:none}
html,body{
  height:100%;font-family:'Share Tech Mono',monospace;
  color:var(--neon);overflow:hidden;
  background:linear-gradient(135deg,var(--bg1),var(--bg2),var(--bg3));
  background-size:300% 300%;
  animation:gradientMove 10s ease infinite;
}
@keyframes gradientMove{0%{background-position:0% 50%}50%{background-position:100% 50%}100%{background-position:0% 50%}}
.black-btn,.settings-btn,.enter-btn,.ctrl-btn,.settings-panel button{
  background:#000;border:1px solid var(--neon);color:var(--neon);cursor:pointer;
}
.black-btn{position:fixed;top:10px;left:10px;padding:6px 12px;border-radius:8px;z-index:200}
header{position:fixed;top:10px;left:0;right:0;text-align:center;z-index:190;font-weight:800;font-size:22px}
.settings-btn{position:fixed;top:10px;right:10px;padding:6px 10px;border-radius:8px;z-index:210;box-shadow:0 0 8px var(--neon)}
.settings-panel{
  position:fixed;top:55px;right:10px;background:rgba(0,0,0,0.85);
  border:1px solid var(--neon);border-radius:10px;padding:12px 16px;
  z-index:220;display:none;flex-direction:column;gap:8px;backdrop-filter:blur(4px);
}
.settings-panel.show{display:flex;animation:fadeIn .3s ease}
.view{position:absolute;inset:0;display:none;align-items:center;justify-content:center;flex-direction:column;padding:18px;z-index:20}
.view.active{display:flex;animation:fadeIn .35s ease}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.panel{width:92%;max-width:960px;padding:18px;border-radius:10px;background:rgba(0,0,0,0.55);border:1px solid var(--muted);backdrop-filter:blur(4px);}
.title{text-align:center;font-size:36px;margin-bottom:8px;text-shadow:0 0 8px rgba(57,255,20,0.5);}
.terminal{width:100%;min-height:88px;background:rgba(0,0,0,0.65);border-radius:8px;padding:10px;border:1px solid var(--muted);white-space:pre-wrap;margin:10px 0;}
.enter-btn{position:fixed;right:18px;bottom:18px;padding:10px 16px;border-radius:10px;z-index:150}
.controls{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin-top:12px}
.ctrl-btn{padding:8px 14px;border-radius:8px;font-weight:700}
.love-wrap{display:flex;flex-direction:column;align-items:center;gap:10px}
.typing{font-size:30px;font-weight:800;letter-spacing:2px;min-height:40px}
.cursor{display:inline-block;width:8px;height:1em;background:var(--neon);vertical-align:middle;animation:blink 900ms steps(2) infinite}
@keyframes blink{0%,50%{opacity:1}51%,100%{opacity:0}}
.poem{margin-top:10px;font-size:20px;max-width:86%;text-align:center;line-height:1.4;opacity:0}
.poem.show{animation:poemIn .6s forwards}
@keyframes poemIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
.info{font-size:13px;color:rgba(57,255,20,0.7);text-align:center;margin-top:8px}
</style>
</head>
<body oncontextmenu="return false">

<button id="blackBtn" class="black-btn">← BLACK</button>
<header>DC PAGE</header>
<button id="settingsBtn" class="settings-btn">⚙️</button>

<div id="settingsPanel" class="settings-panel">
  <button id="fullScreenBtn">🖥 Full Screen</button>
  <button id="colorGreen">🟢 Neon Green</button>
  <button id="colorBlue">🔵 Neon Blue</button>
  <button id="colorRed">🔴 Neon Red</button>
  <button id="colorPink">💗 Neon Pink</button>
  <button id="closeSettings">❌ Close</button>
</div>

<section id="homeView" class="view active">
  <div class="panel">
    <div class="title">JACK</div>
    <div id="terminal" class="terminal"></div>
    <div class="info">Press <strong>ENTAR</strong> to open control panel</div>
  </div>
</section>

<section id="secondView" class="view">
  <div class="panel">
    <div style="text-align:center;font-weight:900;font-size:22px;margin-bottom:8px">++++++</div>
    <div class="love-wrap">
      <div id="loveTyping" class="typing"></div>
      <div id="loveCursor" class="cursor"></div>
      <div id="loveGlow" class="poem"></div>
      <div id="shayri" class="poem"></div>
      <div id="helloMsg" class="poem"></div>
    </div>
    <div class="controls">
      <button id="btnBack" class="ctrl-btn">←</button>
      <button id="btnDots" class="ctrl-btn">.........</button>
      <button id="btnPlus" class="ctrl-btn">++++++</button>
      <button id="btnEntar" class="ctrl-btn">ENTAR</button>
    </div>
    <div class="info">Tap <strong>++++++</strong> for new shayri</div>
  </div>
</section>

<button id="enterBtn" class="enter-btn">ENTAR</button>

<script>
document.addEventListener('contextmenu',e=>e.preventDefault());
document.addEventListener('selectstart',e=>e.preventDefault());

const homeView=document.getElementById('homeView');
const secondView=document.getElementById('secondView');
const enterBtn=document.getElementById('enterBtn');
const blackBtn=document.getElementById('blackBtn');
const btnBack=document.getElementById('btnBack');
const btnEntar=document.getElementById('btnEntar');
const btnPlus=document.getElementById('btnPlus');
const btnDots=document.getElementById('btnDots');

enterBtn.onclick=()=>{homeView.classList.remove('active');secondView.classList.add('active');}
blackBtn.onclick=()=>{secondView.classList.remove('active');homeView.classList.add('active');}
btnBack.onclick=()=>{secondView.classList.remove('active');homeView.classList.add('active');}

/* TERMINAL */
const terminal=document.getElementById('terminal');
const lines=['Initializing us secure shell...','Authenticating ••• success','Loading poetic modules...','Mounting emotions [ok]','Access Granted — Welcome'];
let i=0,j=0;
function typeTerm(){
  if(i>=lines.length)return;
  const l=lines[i];
  if(j<=l.length){
    terminal.textContent=lines.slice(0,i).join('\n')+(i?'\n':'')+l.slice(0,j)+'█';
    j++;setTimeout(typeTerm,50);
  }else{j=0;i++;setTimeout(typeTerm,600);}
}
typeTerm();

/* LOVE TEXT */
const loveEl=document.getElementById('loveTyping');
const loveCur=document.getElementById('loveCursor');
const loveGlow=document.getElementById('loveGlow');
function startLove(){
  const text='I LOVE YOU';
  let k=0;loveEl.textContent='';loveGlow.textContent='';loveCur.style.display='inline-block';
  function t(){
    if(k<=text.length){loveEl.textContent=text.slice(0,k);k++;setTimeout(t,120);}
    else{loveCur.style.display='none';loveGlow.textContent=text;loveGlow.classList.add('show');}
  }t();
}
btnEntar.onclick=startLove;

/* SHAYRI GENERATOR */
const base=[
"उसने कहा – 'मुझसे दूर रहो।' मैंने कहा – 'ठीक है, अब screenshots से काम चलेगा।'",
"माँ बोली – 'कब तक phone देखेगा?' मैंने कहा – 'जब तक last seen दिखती रहेगी।'",
"Crush बोली – 'तुम cute हो!' मैंने कहा – 'हाँ, पर limited edition – out of stock।'",
"पप्पू बोला – 'तेरा exam कैसा गया?' मैंने कहा – 'जैसे love story – start funny, end tragic।'",
"Crush बोली – 'Tum busy थे?' मैंने कहा – 'नहीं, उम्मीदों को format कर रहा था।'",
"माँ बोली – 'शादी कर ले।' मैंने कहा – 'माँ, crush की शादी attend करके आया हूँ।'",
"डॉक्टर बोला – 'तू थका क्यों है?' मैंने कहा – 'emotions night shift में हैं।'",
"वो बोली – 'तुम hero हो।' मैंने कहा – 'हाँ, heartbreak movie का।'",
"Crush बोली – 'मैं किसी और को पसंद करती हूँ।' मैंने कहा – 'ठीक है, delete press करना सीख लिया हूँ।'",
"तुझसे प्यार तो हुआ था, पर तेरे खर्चे देखकर अब डर भी लगता है!",
"तू बोली – 'मैं तुम्हें भूल जाऊँगी', मैंने कहा – 'थोड़ा नेट स्लो है, टाइम लगेगा!'",
"प्यार में पागल हुआ था, अब इलाज में EMI भर रहा हूँ!",
"तेरा चेहरा देख कर दिल ने कहा – 'लगता है WiFi मिल गया!'",
"तू बोली – 'मैं रो रही हूँ', मैंने कहा – 'Data On कर, Video Call पर आ!'",
"तेरे बिना WiFi सा लगता है — कनेक्शन है पर स्पीड नहीं!"
];
function makeShayri(){
  const a=base[Math.floor(Math.random()*base.length)];
  const b=base[Math.floor(Math.random()*base.length)];
  const end=["💚","🌙","✨","❤️","🔥","🌹"];
  return `${a.split("।")[0]} और ${b.toLowerCase()} ${end[Math.floor(Math.random()*end.length)]}`;
}
const sh=document.getElementById('shayri');
let count=0;
function showShayri(){
  count++;
  const text=`${makeShayri()} (${count}/5000)`;
  sh.textContent='';sh.classList.remove('show');
  let p=0;
  function step(){
    if(p<=text.length){sh.textContent=text.slice(0,p)+(p%2?'█':'');p++;setTimeout(step,35);}
    else{sh.textContent=text;sh.classList.add('show');}
  }step();
}
btnPlus.onclick=showShayri;

/* DOTS MESSAGE */
const helloEl=document.getElementById('helloMsg');
btnDots.onclick=()=>{
  const msg="Hello sir, आप कैसे हैं ☺️";
  helloEl.textContent='';helloEl.classList.remove('show');
  let x=0;
  function type(){
    if(x<=msg.length){helloEl.textContent=msg.slice(0,x)+(x%2?'█':'');x++;setTimeout(type,80);}
    else{helloEl.textContent=msg;helloEl.classList.add('show');}
  }type();
};

/* SETTINGS PANEL */
const settingsBtn=document.getElementById('settingsBtn');
const panel=document.getElementById('settingsPanel');
settingsBtn.onclick=()=>panel.classList.toggle('show');
document.getElementById('closeSettings').onclick=()=>panel.classList.remove('show');
document.addEventListener('click',e=>{
  if(!panel.contains(e.target)&&e.target!==settingsBtn)panel.classList.remove('show');
});
document.getElementById('fullScreenBtn').onclick=()=>{
  if(!document.fullscreenElement){document.documentElement.requestFullscreen();}
  else{document.exitFullscreen();}
};
function changeColor(color){
  document.documentElement.style.setProperty('--neon',color);
  panel.classList.remove('show');
}
document.getElementById('colorGreen').onclick=()=>changeColor('#39ff14');
document.getElementById('colorBlue').onclick=()=>changeColor('#00ffff');
document.getElementById('colorRed').onclick=()=>changeColor('#ff4444');
document.getElementById('colorPink').onclick=()=>changeColor('#ff33cc');
</script>
</body>
</html>
