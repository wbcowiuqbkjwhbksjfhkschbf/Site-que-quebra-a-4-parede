# Site-que-quebra-a-4-parede
NUM SEI
[relogio_4_parede_html (1).html](https://github.com/user-attachments/files/22116918/relogio_4_parede_html.1.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quebra da 4ª Parede — Relógio, Data, Bateria & Dispositivo</title>
<style>
@font-face { font-family: 'CustomFont'; src: url('https://files.catbox.moe/gloq11.ttf') format('truetype'); }
@font-face { font-family: 'Determination'; src: url('https://files.catbox.moe/u5o8ty.otf') format('opentype'); }
:root{--bg:#0b0f14;--panel:#121821;--ink:#e8f0ff;--muted:#93a1bb;--accent:#7c5cff;--good:#22c55e;--warn:#f59e0b;--bad:#ef4444;}
*{box-sizing:border-box}
html,body{height:100%}
body{margin:0;font-family:'CustomFont', ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Helvetica,Arial;background:#0b0f14;color:var(--ink);display:grid;place-items:center;overflow:hidden;}
.menu{display:flex;gap:20px;justify-content:center;align-items:center;padding:12px 0;background:var(--panel);border-bottom:1px solid rgba(255,255,255,.1);position:sticky;top:0;z-index:999;}
.menu a{color:var(--ink);text-decoration:none;font-weight:700;font-size:18px;position:relative;padding:6px 8px;}
.menu a::after{content:"";position:absolute;left:0;right:100%;bottom:-4px;height:3px;background:var(--accent);transition:right .28s ease;}
.menu a:hover::after{right:0;}
.app{width:min(960px,92vw);padding:28px;border-radius:20px;background:linear-gradient(180deg,rgba(255,255,255,.03),rgba(255,255,255,.01));box-shadow:0 30px 80px rgba(0,0,0,.45), inset 0 1px 0 rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.08);position:relative;margin-top:20px;}
.hdr{display:flex;gap:14px;align-items:center;justify-content:space-between;flex-wrap:wrap}
.title{font-size:clamp(22px,3.5vw,32px);font-weight:800;letter-spacing:.3px}
.aside{font-size:14px;color:var(--muted)}
.grid{display:grid;grid-template-columns:1fr;gap:16px;margin-top:16px}
@media (min-width:720px){.grid{grid-template-columns:1.2fr .8fr}}
.card{background:var(--panel);border:1px solid rgba(255,255,255,.06);border-radius:18px;padding:18px;position:relative;overflow:hidden}
.card h2{margin:0 0 8px;font-size:14px;letter-spacing:.4px;font-weight:700;color:var(--muted);text-transform:uppercase}
.time{font-variant-numeric:tabular-nums;letter-spacing:1px;font-size:clamp(40px,6vw,64px);font-weight:900}
.date{font-size:16px;color:var(--muted)}
.bubble{position:absolute;right:18px;top:18px;background:rgba(124,92,255,.18);border:1px solid rgba(124,92,255,.45);color:#eae6ff;padding:10px 12px;border-radius:12px;max-width:280px;font-size:14px;backdrop-filter:blur(6px)}
.blink{animation:blink 1.2s step-start infinite}
@keyframes blink{50%{opacity:.35}}
.stat{display:flex;align-items:center;gap:10px;margin:10px 0}
.meter{height:16px;width:160px;border-radius:8px;background:#0d121a;border:1px solid rgba(255,255,255,.08);position:relative;overflow:hidden}
.fill{position:absolute;left:0;top:0;bottom:0;width:0;background:linear-gradient(90deg,var(--good),#34d399);transition:width .3s}
.plug{font-size:12px;padding:2px 6px;border-radius:999px;border:1px solid rgba(255,255,255,.12)}
.list{display:grid;grid-template-columns:1fr;gap:10px}
.row{display:flex;justify-content:space-between;gap:12px;padding:10px;border:1px dashed rgba(255,255,255,.12);border-radius:12px}
.key{color:var(--muted)}
.val{font-weight:700}
.footer{margin-top:18px;color:var(--muted);font-size:12px;text-align:center}
.kbd{font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,monospace;background:#0e1420;border:1px solid rgba(255,255,255,.1);padding:2px 6px;border-radius:6px}
#secretWrapper{margin-top:20px;text-align:center}
#secretInput{padding:6px 10px;border-radius:6px;border:1px solid rgba(255,255,255,.3);background:var(--panel);color:var(--ink);width:220px;}
#secretBtn{margin-left:8px;padding:6px 12px;border-radius:6px;border:none;background:var(--accent);color:#fff;cursor:pointer;}
#secretMsg{margin-top:8px;color:var(--bad);font-weight:700;}
</style>
</head>
<body>
<nav class="menu">
<a href="#clock">Relógio</a>
<a href="#batteryFill">Bateria</a>
<a href="#deviceInfo">Dispositivo</a>
</nav>
<main class="app" role="main" aria-live="polite">
<div class="hdr">
<div class="title">👀 Oi, eu sou a sua página consciente (quebrando a <span class="blink">4ª parede</span>)</div>
<div class="aside" id="statusMsg">Carregando…</div>
</div>
<section class="grid">
<article class="card" aria-label="Relógio e Data em Tempo Real">
<div class="bubble" id="bubble">Eu tô te vendo aí, hein… <strong>não fecha</strong> essa aba! 😏</div>
<h2>Agora mesmo</h2>
<div class="time" id="clock">--:--:--</div>
<div class="date" id="date">—</div>
</article>
<article class="card" aria-label="Status da Bateria">
<h2>Bateria do seu dispositivo</h2>
<div class="stat">
<div class="meter" aria-hidden="true"><div class="fill" id="batteryFill"></div></div>
<div class="val" id="batteryPct">—%</div>
<span class="plug" id="batteryState">—</span>
</div>
<div class="date" id="batteryExtra">Tentando acessar a API da bateria…</div>
</article>
<article class="card" aria-label="Sobre seu dispositivo">
<h2>O que eu consigo deduzir sobre você</h2>
<div class="list" id="deviceInfo">
<div class="row"><span class="key">Hora local do navegador</span><span class="val" id="tz">—</span></div>
<div class="row"><span class="key">Navegador</span><span class="val" id="browser">—</span></div>
<div class="row"><span class="key">Sistema</span><span class="val" id="platform">—</span></div>
<div class="row"><span class="key">Provável dispositivo</span><span class="val" id="device">—</span></div>
<div class="row"><span class="key">Memória estimada</span><span class="val" id="memory">—</span></div>
</div>
<p class="date" style="margin-top:8px">⚠️ Por privacidade, o navegador <strong>não revela o nome exato do seu aparelho</strong>.</p>
</article>
</section>
<div id="secretWrapper">
<p>Coloque seu código secreto aqui abaixo 👇:</p>
<input type="text" id="secretInput" placeholder="Código secreto...">
<button id="secretBtn">Enviar</button>
<p id="secretMsg"></p>
</div>
<p class="footer">Dica: aperta <span class="kbd">Ctrl</span> + <span class="kbd">S</span> pra salvar como <span class="kbd">.html</span> e abrir offline. — Feito com ❤️.</p>
</main>
<script>
// Relógio e Data
const fmtTime = new Intl.DateTimeFormat('pt-BR',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
const fmtDateLong = new Intl.DateTimeFormat('pt-BR',{weekday:'long',day:'2-digit',month:'long',year:'numeric'});
function updateClock(){ const now = new Date(); document.getElementById('clock').textContent=fmtTime.format(now); document.getElementById('date').textContent=fmtDateLong.format(now); }
updateClock(); setInterval(updateClock,250);

// Bateria
const batteryFill = document.getElementById('batteryFill'); const batteryPct = document.getElementById('batteryPct'); const batteryState = document.getElementById('batteryState'); const batteryExtra = document.getElementById('batteryExtra');
function renderBattery(b){ const pct=Math.round(b.level*100); batteryPct.textContent=pct+'%'; batteryFill.style.width=pct+'%'; batteryFill.style.background=b.charging? 'linear-gradient(90deg,var(--good),#34d399)': pct<=20? 'linear-gradient(90deg,var(--bad),#f87171)': pct<=50? 'linear-gradient(90deg,var(--warn),#fbbf24)': 'linear-gradient(90deg,var(--good),#34d399)'; batteryState.textContent=b.charging?'Carregando':'Desconectado'; }
if('getBattery' in navigator){navigator.getBattery().then(b=>{renderBattery(b); ['levelchange','chargingchange','chargingtimechange','dischargingtimechange'].forEach(evt=>b.addEventListener(evt,()=>renderBattery(b)));});}else{batteryExtra.textContent='API de bateria não suportada'; batteryPct.textContent='—'; batteryState.textContent='—';}

// Device info
document.getElementById('tz').textContent=Intl.DateTimeFormat().resolvedOptions().timeZone||'—';
const ua=navigator.userAgent||''; const platform=(navigator.userAgentData&&navigator.userAgentData.platform)||navigator.platform||'—';
function detectBrowser(u){if(u.includes('Edg/')) return 'Microsoft Edge'; if(u.includes('OPR/')||u.includes('Opera')) return 'Opera'; if(u.includes('Chrome/')) return 'Chrome'; if(u.includes('Firefox/')) return 'Firefox'; if(u.includes('Safari/')&&!u.includes('Chrome/')) return 'Safari'; return 'Desconhecido';}
function guessDevice(u){if(/Android/i.test(u)) return 'Android'; if(/iPhone|iPad|iPod/i.test(u)) return 'iOS'; if(/CrOS/i.test(u)) return 'Chromebook'; if(/Win/i.test(u)) return 'Windows'; if(/Macintosh|Mac OS X/i.test(u)) return 'Mac'; if(/Linux/i.test(u)) return 'Linux'; return 'Desconhecido';}
document.getElementById('browser').textContent=detectBrowser(ua); document.getElementById('platform').textContent=platform; document.getElementById('device').textContent=guessDevice(ua);
document.getElementById('memory').textContent=navigator.deviceMemory?navigator.deviceMemory+' GB (estimado)':'—';

// Bubble & status
const bubble=document.getElementById('bubble'); const statusMsg=document.getElementById('statusMsg');
function setMsg(txt){statusMsg.textContent=txt;}
document.addEventListener('visibilitychange',()=>{document.hidden? (bubble.textContent='Ei! Não me abandona. 😶', setMsg('Aba em segundo plano')) : (bubble.innerHTML='Ah, voltou! Eu disse que estou te vendo ⏰ '+document.getElementById('clock').textContent,setMsg('Tudo sob controle'));});
window.addEventListener('focus',()=>setMsg('Olhando pra mim 👋')); window.addEventListener('blur',()=>setMsg('Você desviou o olhar…'));

// Easter eggs e códigos secretos
const secretInput=document.getElementById('secretInput'); const secretBtn=document.getElementById('secretBtn'); const secretMsg=document.getElementById('secretMsg');
secretBtn.addEventListener('click',()=>{
  const val=secretInput.value.trim();
  if(val==='Foxy'){
    const win=window.open('','Foxy','width=500,height=400');
    win.document.write('<img src="https://static.wikia.nocookie.net/pizzaria-freddy-fazbear/images/3/3a/FoxyJumpscare.gif" style="width:100%;height:100%">');
    new Audio('https://files.catbox.moe/t9z7wb.ogg').play();
    setTimeout(()=>win.close(),1500);
  } else if(val==='Undertale'){
    document.body.style.fontFamily='Determination, sans-serif';
  } else if(val==='Spamton'){
    const win=window.open('','Spamton','width=400,height=300');
    win.document.write('<img src="https://static.wikia.nocookie.net/deltarune/images/e/e3/Spamton_overworld_glitched_laugh.gif" style="width:100%;height:100%">');
    const aud=new Audio('https://files.catbox.moe/yq8e8v.mp3'); aud.play();
    setTimeout(()=>win.close(),aud.duration*1000 || 3000);
    setTimeout(()=>{ // tremer
      let x=window.screen.width/2-200, y=window.screen.height/2-150, pos=0;
      const interval=setInterval(()=>{win.moveTo(x+((pos%2)?10:-10),y); pos++;},50);
      aud.onended=()=>clearInterval(interval);
    },990);
  } else {
    secretMsg.textContent='ERRO: Código inválido';
    new Audio('https://files.catbox.moe/wy0nsf.mp3').play();
  }
});
</script>
</body>
</html>
