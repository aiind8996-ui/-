++++++++++.     ..... 
...........
. <!doctype html>
<html lang="hi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>"**" — Shayri Mode</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
:root{
  --bg1:#000;
  --bg2:#020c0a;
  --bg3:#002b00;
  --neon:#39ff14;
  --muted:rgba(57,255,20,0.08);
}
*{box-sizing:border-box;margin:0;padding:0;user-select:none}
html,body{
  height:100%;
  font-family:'Share Tech Mono',monospace;
  color:var(--neon);
  overflow:hidden;
  background:linear-gradient(135deg,var(--bg1),var(--bg2),var(--bg3));
  background-size:300% 300%;
  animation:gradientMove 10s ease infinite;
}
@keyframes gradientMove{
  0%{background-position:0% 50%;}
  50%{background-position:100% 50%;}
  100%{background-position:0% 50%;}
}
.black-btn{
  position:fixed;top:10px;left:10px;
  background:#000;border:1px solid var(--neon);
  color:var(--neon);padding:6px 12px;border-radius:8px;
  z-index:200;cursor:pointer;
}
header{
  position:fixed;top:10px;left:0;right:0;
  text-align:center;z-index:190;font-weight:800;
  color:var(--neon);font-size:22px;letter-spacing:1px;
}
.settings-btn{
  position:fixed;top:10px;right:10px;background:#000;
  border:1px solid var(--neon);color:var(--neon);
  padding:6px 10px;border-radius:8px;z-index:210;cursor:pointer;
  box-shadow:0 0 8px var(--neon);
}
.settings-panel{
  position:fixed;top:55px;right:10px;background:rgba(0,0,0,0.85);
  border:1px solid var(--neon);border-radius:10px;padding:12px 16px;
  z-index:220;display:none;flex-direction:column;gap:8px;
  backdrop-filter:blur(4px);
}
.settings-panel.show{display:flex;animation:fadeIn .3s ease}
.settings-panel button{
  background:#000;border:1px solid var(--neon);
  color:var(--neon);padding:6px 10px;border-radius:6px;cursor:pointer;
}
.view{position:absolute;inset:0;display:none;align-items:center;justify-content:center;flex-direction:column;padding:18px;z-index:20}
.view.active{display:flex;animation:fadeIn .35s ease}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.panel{
  width:92%;max-width:960px;padding:18px;border-radius:10px;
  background:rgba(0,0,0,0.55);border:1px solid var(--muted);
  backdrop-filter:blur(4px);
}
.title{
  font-size:36px;text-align:center;margin-bottom:8px;
  text-shadow:0 0 8px rgba(57,255,20,0.5);
}
.terminal{
  width:100%;min-height:88px;background:rgba(0,0,0,0.65);
  border-radius:8px;padding:10px;border:1px solid var(--muted);
  white-space:pre-wrap;margin:10px 0;
}
.enter-btn{
  position:fixed;right:18px;bottom:18px;background:#000;
  border:1px solid var(--neon);color:var(--neon);
  padding:10px 16px;border-radius:10px;z-index:150;cursor:pointer;
}
.controls{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin-top:12px}
.ctrl-btn{
  background:rgba(0,0,0,0.6);border:1px solid var(--neon);
  color:var(--neon);padding:8px 14px;border-radius:8px;cursor:pointer;
  font-weight:700;
}
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
/* Prevent selection and right-click */
document.addEventListener('contextmenu', e => e.preventDefault());
document.addEventListener('selectstart', e => e.preventDefault());

/* VIEW SWITCHING */
const homeView=document.getElementById('homeView');
const secondView=document.getElementById('secondView');
enterBtn.onclick=()=>{homeView.classList.remove('active');secondView.classList.add('active');}
blackBtn.onclick=()=>{secondView.classList.remove('active');homeView.classList.add('active');}
btnBack.onclick=()=>{secondView.classList.remove('active');homeView.classList.add('active');}

/* TERMINAL TYPING */
const terminal=document.getElementById('terminal');
const lines=['Initializing vinay. love secure shell...','Authenticating ••• success','Loading poetic modules...','Mounting emotions [ok]','Access Granted — Welcome'];
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

/* LOVE ANIMATION */
const loveEl=document.getElementById('loveTyping');
const loveCur=document.getElementById('loveCursor');
const loveGlow=document.getElementById('loveGlow');
function startLove(){
  const text='I LOVE YOU';
  let k=0;loveEl.textContent='';loveGlow.textContent='';
  loveCur.style.display='inline-block';
  function t(){
    if(k<=text.length){
      loveEl.textContent=text.slice(0,k);k++;
      setTimeout(t,120);
    }else{
      loveCur.style.display='none';
      loveGlow.textContent=text;
      loveGlow.classList.add('show');
    }
  }t();
}
btnEntar.onclick=startLove;

/* SHAYRI GENERATOR */
const base=["तुझसे प्यार तो हुआ था, पर तेरे खर्चे देखकर अब डर भी लगता है!",
  "तू बोली – 'मैं तुम्हें भूल जाऊँगी', मैंने कहा – 'थोड़ा नेट स्लो है, टाइम लगेगा!'",
  "प्यार में पागल हुआ था, अब इलाज में EMI भर रहा हूँ!",
  "तेरा चेहरा देख कर दिल ने कहा – 'लगता है WiFi मिल गया!'",
  "तू बोली – 'मैं रो रही हूँ', मैंने कहा – 'Data On कर, Video Call पर आ!'",
  "तेरा प्यार ऐसा है – जैसे Recharge खत्म होते ही Off!",
  "मोहब्बत में ऐसा डूबा हूँ – अब Password भी तेरा नाम रख दिया है!","तेरे बिना WiFi सा लगता है — कनेक्शन है पर स्पीड नहीं!",
  "वो बोली 'तुम बहुत स्वीट हो' — मैंने कहा 'शुगर फ्री हूँ बीटू!'",
  "मोहब्बत का सिग्नल तो मिला, पर नेटवर्क हमेशा बिज़ी निकला!",
  "दिल लगाया था प्यार में, अब बैटरी सेव मोड में चल रहे हैं यार में!",
  "तेरी यादें RAM की तरह हैं — क्लियर करो तो भी रहती हैं!",
  "वो बोली तुम्हें शर्म नहीं आती? — मैंने कहा 'नेट पर तो सब खुले आम हैं!'",
  "ज़िंदगी ने सिखाया है एक नया फार्मूला — टाइम नहीं है, पर ऑनलाइन ज़रूर हैं!",
  "तेरे प्यार में CPU गर्म हो गया — अब ठंडा करने के लिए चाय पीनी पड़ती है!",
  "जब भी कोई हँसी आती है, WiFi सिग्नल चला जाता है!",
  "मोहब्बत भी अब ऐप जैसी है — अपडेट करते रहो वरना हट जाएगी!",
  "तेरे इश्क़ में ऐसा डूबे — अब चार्जर भी गीला लगता है!",
  "मोहब्बत का नाम सुना — बैटरी 1% रह गई!",
  "उसने कहा 'भूल जाओ मुझे' — मैंने Google से भी डिलीट करा दिया!",
  "तुम्हारी यादें इतनी प्यारी हैं — जैसे EMI हर महीने आती है!",
  "दिल में तू और पेट में मैगी — दोनों हमेशा गरम रहते हैं!",
  "तेरी बातों में ऐसा जादू है — जैसे मोबाइल में फ़्री डेटा मिल गया हो!",
  "प्यार तो फ़्री है, पर टाइम बहुत महंगा है!",
  "वो बोली — 'तुमने दिल क्यों दिया?' — मैंने कहा 'रिटर्न पॉलिसी नहीं थी!'",
  "जब उसने कहा 'मैं सिर्फ फ्रेंड हूँ' — दिल ने बोला 'कंट्रोल यूज़र कंट्रोल!'",
  "तेरे बिना मेरा क्या हाल है — जैसे सस्ता फोन बिना कवर के चाल है!",
  "तेरे प्यार का नशा ऐसा — कि बैटरी भी 100% फुल लगे!",
  "वो हँस दी — और मैं चार्ज हो गया!",
  "प्यार में गिरा — अब Data भी गिर रहा है!",
  "तेरे आने से जैसे नेटवर्क फुल सिग्नल हो गया!",
  "तेरी हाँ में इतना करंट था — मेरा दिल राउटर बन गया!",
  "तू मुस्कुरा दे — तो मेरा पासवर्ड भूल जाऊँ!",
  "इश्क़ और इंटरनेट — दोनों कट जाएँ तो दर्द होता है!",
  "वो बोली — 'तुम बदल गए!' — मैंने कहा 'ऑटो अपडेट था!'",
  "तेरे प्यार का लिंक टूटा नहीं — बस सर्वर डाउन है!",
  "दिल लगा था तुझसे — अब Data खत्म हो गया!",
  "तेरी फोटो देख के लगा — सॉफ्टवेयर क्रैश हो गया!",
  "मोहब्बत भी अब WiFi जैसी है — पास रहो तो फ्री, दूर रहो तो लॉक!",
  "तू बोली — 'मेरी DP कैसी लगी?' — मैंने कहा 'Wallpaper बना लूँ क्या?'",
  "तेरे प्यार का लॉगिन किया — अब पासवर्ड भूल गया!",
  "उसने कहा 'बात करनी है' — मैंने कहा 'Error 404: Courage Not Found!'",
  "दिल चाहता है — तू भी मेरे इनबॉक्स में रिप्लाई दे!",
  "तू भी क्या चीज़ है — Screenshot लेने का मन करता है!",
  "तेरी मुस्कान इतनी Cute है — जैसे बिन Ads वाला YouTube है!",
  "तेरी यादें Pop-up की तरह आती हैं — Close करो तो फिर खुल जाती हैं!",
  "जब तू online आती है — मेरा दिल Refresh हो जाता है!",
  "प्यार तेरा ऐसा निकला — Battery Drain करने वाला App!",
  "वो बोली 'Main Busy Hoon' — और Insta पर Reel डाल दी!",
  "तेरा इश्क़ Virus बन गया — System Hang कर दिया!",
  "तू Offline भी Online लगती है — शायद Notification चालू है!",
  "तेरे प्यार का Effect ऐसा — अब Charger भी Romantic लगता है!",
  "तेरे बिना Net Slow लगता है — दिल भी Buffering में रहता है!",
  "तेरा नाम सुनते ही WiFi Connect हो जाता है!",
  "तेरी बातों में ऐसा Charm है — जैसे Cashback Offer Warm है!",
  "तेरा इश्क़ तो Bluetooth जैसा — जुड़ गया तो हटता नहीं!",
  "तू हँस दे तो मेरा Data Reset हो जाता
  "तू मुस्कुराई – तो लगा Cashback मिल गया!",
  "दिल ने कहा 'उससे बात कर', दिमाग बोला 'Recharge पहले कर!'",
  "तेरा प्यार Maggi जैसा है – दो मिनट में Ready और जल्दी खत्म!",
  "तू बोली – 'Main Busy Hoon', Insta खोला – वो Reels बना रही थी!",
  "तेरी आंखों में डूब गया, अब Search History में बस तू ही तू है!",
  "प्यार तो फ्री था, लेकिन टाइम और सिग्नल दोनों महंगे निकले!",
  "तेरी यादें WiFi जैसी हैं – कभी Connect, कभी Disconnect!",
  "तू कहती है 'तू मेरा Hero है', पर Hero तो Recharge करने गया है!",
  "तेरा नाम सुनते ही मेरा Data भी Refresh हो जाता है!",
  "तू रूठी – तो Mobile की Screen भी Fade हो गई!",
  "तेरा प्यार Virus जैसा – Install किया और Hang हो गया!",
  "वो बोली 'दिल दे दो', मैंने कहा 'Battery Low है यार!'",
  "तू बोली 'मुझसे बात क्यों नहीं करता?' – मैंने कहा 'Network Problem है दिल की!'",
  "तेरे प्यार में ऐसा फँसा हूँ – अब Google Map भी रास्ता नहीं दिखाता!",
  "तू बोली 'Love you', मैंने कहा 'Repeat कर, Recording चालू नहीं थी!'",
  "तेरी बातों में ऐसा Current है – Bluetooth अपने आप Connect हो जाता है!",
  "तू मेरी Battery Saver है – तेरे बिना सब Drain हो जाता है!",
  "तेरा गुस्सा Cute लगता है, पर Screenshot लेना जरूरी है!",
  "तेरी Smile का Notification आया – और मैं तुरंत Online हो गया!",
  "तू बोली 'तुम बदल गए', मैंने कहा 'Auto Update था!'",
  "तेरी यादें इतना हँसाती हैं – जैसे Free Meme Pack मिल गया हो!",
  "तू मेरी Favourite Mistake है – जिसे बार-बार दोहराने का मन करता है!",
  "तेरी DP देखकर तो Data खत्म करना भी सही लगता है!",
  "तू Offline हो तो लगता है – Server Down है!",
  "तेरे प्यार में Signal Full है, पर Call Drop हमेशा होता है!",
  "तेरे लिए तो मैं Password तक बदल दूँ!",
  "तू बोली 'Main Busy Hoon' – मैंने कहा 'मैं भी Recharge कर रहा हूँ!'",
  "तेरी मुस्कान वो Notification है – जिसे Ignore नहीं कर सकता!",
  "तेरी यादें Cache Memory जैसी – Clear करो फिर भी लौट आती हैं!",
  "तू बोली 'मुझसे झगड़ा मत कर' – मैंने कहा 'Update Pending है!'",
  "तेरे लिए Dil Unlimited Plan है – कभी खत्म नहीं होता!",
  "तू बोली 'तुम्हारा दिल कहाँ है?' – मैंने कहा 'Google Drive पर Backup में!'",
  "तेरे प्यार का असर ऐसा – अब Alarm भी तेरे नाम से बजता है!"," तेरी मुस्कान मेरी पहली ज़रूरत है।","हर ख़ुशी मेरी तेरे नाम कर दूँ।","दिल के खज़ाने में बस तुम्हारा पता है।","तेरे बिना ये चाँद भी फीका लगता है।","तेरी आँखों की चमक में खो जाना चाहता हूँ।","तेरी यादें दिल को हमेशा गुज़रने नहीं देतीं।"];
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
    if(p<=text.length){
      sh.textContent=text.slice(0,p)+(p%2?'█':'');
      p++;setTimeout(step,35);
    }else{
      sh.textContent=text;sh.classList.add('show');
    }
  }step();
}
btnPlus.onclick=showShayri;

/* DOTS GREETING */
const helloEl=document.getElementById('helloMsg');
btnDots.onclick=()=>{
  const msg="Hello sir, आप कैसे हैं ☺️";
  helloEl.textContent='';helloEl.classList.remove('show');
  let x=0;
  function type(){
    if(x<=msg.length){
      helloEl.textContent=msg.slice(0,x)+(x%2?'█':'');
      x++;setTimeout(type,80);
    }else{
      helloEl.textContent=msg;
      helloEl.classList.add('show');
    }
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
