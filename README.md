<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="theme-color" content="#07000e">
<title>💕 Piano Tiles — Pour Ibtissem</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Lato:wght@300;400;700&display=swap');

/* ═══════════════════════════════════════════════════════
   RESET TOTAL — isole le jeu du CSS du site parent
   Tout est scopé sous #pt-root
   ═══════════════════════════════════════════════════════ */
#pt-root, #pt-root *, #pt-root *::before, #pt-root *::after {
  all: initial;
  box-sizing: border-box !important;
  -webkit-tap-highlight-color: transparent !important;
  -webkit-touch-callout: none !important;
}

#pt-root {
  display: block !important;
  position: fixed !important;
  top: 0 !important; left: 0 !important; right: 0 !important; bottom: 0 !important;
  width: 100% !important; height: 100% !important;
  background: #07000e !important;
  z-index: 999999 !important;
  overflow: hidden !important;
  touch-action: none !important;
  font-family: 'Lato', sans-serif !important;
}

/* BG canvas */
#pt-root #bg-canvas {
  display: block !important;
  position: fixed !important;
  top: 0 !important; left: 0 !important;
  width: 100% !important; height: 100% !important;
  z-index: 0 !important; pointer-events: none !important;
}

/* APP layout */
#pt-root #app {
  display: flex !important; flex-direction: column !important;
  position: relative !important; z-index: 1 !important;
  width: 100% !important; height: 100% !important;
  max-width: 560px !important; margin: 0 auto !important;
}

/* HEADER */
#pt-root #header {
  display: flex !important; align-items: center !important;
  justify-content: space-between !important;
  flex-shrink: 0 !important;
  background: linear-gradient(135deg, #8b0000, #c0006e) !important;
  padding: max(10px, env(safe-area-inset-top, 10px)) 18px 10px 18px !important;
  box-shadow: 0 2px 22px rgba(192,0,110,0.55) !important;
}
#pt-root #header h1 {
  display: block !important;
  color: #ffe0f0 !important;
  font-family: 'Playfair Display', serif !important;
  font-size: clamp(14px, 4vw, 18px) !important;
  font-weight: 700 !important; letter-spacing: 2px !important;
  text-shadow: 0 0 14px #ff69b4 !important;
  margin: 0 !important; padding: 0 !important;
  background: none !important; border: none !important;
  border-bottom: none !important; text-decoration: none !important;
  line-height: 1.2 !important;
}
#pt-root #score-val {
  display: block !important; color: #ffb3d9 !important;
  font-size: clamp(20px, 5vw, 26px) !important; font-weight: 700 !important;
  text-shadow: 0 0 10px #ff1493 !important; line-height: 1 !important;
  min-width: 55px !important; text-align: right !important;
}

/* SONG BAR */
#pt-root #song-bar {
  display: flex !important; align-items: center !important; flex-shrink: 0 !important;
  background: rgba(90,0,36,0.85) !important; padding: 5px 16px !important;
  gap: 8px !important; border-bottom: 1px solid rgba(192,0,110,0.35) !important;
}
#pt-root #song-name { display:block !important; color:#ff9ec8 !important; font-size:12px !important; font-style:italic !important; flex:1 !important; overflow:hidden !important; white-space:nowrap !important; text-overflow:ellipsis !important; }
#pt-root #combo-val { display:block !important; color:#ffb3e6 !important; font-size:12px !important; white-space:nowrap !important; }
#pt-root #speed-val { display:block !important; color:rgba(255,179,217,.55) !important; font-size:11px !important; white-space:nowrap !important; }

/* PROGRESS */
#pt-root #prog-wrap { display:block !important; flex-shrink:0 !important; height:4px !important; background:rgba(255,255,255,.07) !important; }
#pt-root #prog-bar  { display:block !important; height:100% !important; width:0% !important; background:linear-gradient(90deg,#ff1493,#ff69b4,#ffb3d9) !important; box-shadow:0 0 8px #ff1493 !important; transition:width .08s linear !important; }

/* GAME AREA */
#pt-root #game-area {
  display:block !important; flex:1 !important; position:relative !important;
  overflow:hidden !important; min-height:0 !important;
  background:linear-gradient(180deg,#060010 0%,#0a0008 100%) !important;
}
#pt-root #game-canvas { display:block !important; position:absolute !important; top:0 !important; left:0 !important; width:100% !important; height:100% !important; }

/* KEYS */
#pt-root #keys {
  display:flex !important; flex-shrink:0 !important;
  height: clamp(80px, 16vw, 110px) !important;
  padding-bottom: env(safe-area-inset-bottom, 0px) !important;
  background:linear-gradient(180deg,#0f0015,#180022) !important;
  border-top:2px solid #c0006e !important;
}
#pt-root .key {
  display:flex !important; flex:1 !important;
  align-items:flex-end !important; justify-content:center !important;
  padding-bottom:12px !important;
  border-right:1px solid rgba(192,0,110,0.18) !important;
  cursor:pointer !important; position:relative !important;
  transition: background .04s !important;
  -webkit-user-select:none !important; user-select:none !important;
}
#pt-root .key:last-child { border-right:none !important; }
#pt-root .key.pressed {
  background:linear-gradient(180deg,rgba(192,0,110,0.92),rgba(139,0,0,0.7)) !important;
  box-shadow:inset 0 0 30px rgba(255,20,147,0.5),0 0 28px rgba(255,20,147,0.35) !important;
}
#pt-root .key-lbl { display:block !important; color:rgba(255,180,220,0.35) !important; font-size:clamp(9px,2.5vw,12px) !important; letter-spacing:1px !important; }

/* FLASH / PERFECT */
#pt-root #miss-flash {
  display:block !important; position:fixed !important; top:0 !important; left:0 !important; right:0 !important; bottom:0 !important;
  background:rgba(192,0,110,0.18) !important; z-index:1000050 !important;
  pointer-events:none !important; opacity:0 !important;
}
#pt-root #perfect-txt {
  display:block !important; position:fixed !important; top:42% !important; left:50% !important;
  transform:translate(-50%,-50%) !important;
  color:#ff9ec8 !important; font-family:'Playfair Display',serif !important;
  font-size:clamp(22px,6vw,30px) !important; font-style:italic !important;
  z-index:1000060 !important; pointer-events:none !important;
  opacity:0 !important; white-space:nowrap !important;
  text-shadow:0 0 22px #ff1493 !important;
}

/* OVERLAY */
#pt-root #overlay {
  display:flex !important; position:fixed !important; top:0 !important; left:0 !important; right:0 !important; bottom:0 !important;
  background:rgba(6,0,12,0.96) !important; z-index:1000200 !important;
  align-items:center !important; justify-content:center !important;
  padding:max(16px,env(safe-area-inset-top,16px)) 16px max(16px,env(safe-area-inset-bottom,16px)) 16px !important;
}
#pt-root #overlay.hidden { display:none !important; }
#pt-root #panel {
  display:block !important;
  background:linear-gradient(140deg,rgba(139,0,0,0.92),rgba(70,0,55,0.92)) !important;
  border:1px solid #c0006e !important; border-radius:20px !important;
  padding:clamp(20px,5vw,32px) clamp(18px,6vw,36px) !important;
  max-width:420px !important; width:100% !important;
  box-shadow:0 0 60px rgba(192,0,110,0.3) !important;
  text-align:center !important; max-height:86vh !important;
  overflow-y:auto !important; -webkit-overflow-scrolling:touch !important;
}
#pt-root .panel-title {
  display:block !important; color:#ff9ec8 !important;
  font-family:'Playfair Display',serif !important; font-size:clamp(20px,6vw,26px) !important;
  font-weight:700 !important; text-shadow:0 0 16px #ff1493 !important; margin-bottom:6px !important;
}
#pt-root .panel-sub {
  display:block !important; color:#ffb3e6 !important;
  font-size:13px !important; line-height:1.7 !important;
  font-style:italic !important; margin-bottom:20px !important;
}

/* SONG ITEMS */
#pt-root .song-item {
  display:flex !important; align-items:center !important;
  background:linear-gradient(135deg,rgba(107,0,37,0.85),rgba(50,0,50,0.85)) !important;
  border:1px solid rgba(192,0,110,0.35) !important; border-radius:12px !important;
  padding:clamp(10px,3vw,14px) !important; margin-bottom:10px !important;
  cursor:pointer !important; gap:12px !important; text-align:left !important;
  transition:all .2s !important;
}
#pt-root .song-item:active {
  border-color:#ff69b4 !important;
  background:linear-gradient(135deg,rgba(160,0,58,0.92),rgba(80,0,80,0.92)) !important;
  box-shadow:0 0 16px rgba(192,0,110,0.4) !important;
}
#pt-root .song-icon   { display:block !important; font-size:clamp(22px,6vw,28px) !important; flex-shrink:0 !important; }
#pt-root .song-info   { display:block !important; flex:1 !important; overflow:hidden !important; }
#pt-root .song-title  { display:block !important; color:#ffe0f0 !important; font-family:'Playfair Display',serif !important; font-size:clamp(13px,3.5vw,15px) !important; overflow:hidden !important; white-space:nowrap !important; text-overflow:ellipsis !important; }
#pt-root .song-artist { display:block !important; color:#ff9ec8 !important; font-size:clamp(10px,2.5vw,12px) !important; margin-top:2px !important; }
#pt-root .song-bpm    { display:block !important; color:rgba(255,179,217,.5) !important; font-size:11px !important; margin-top:1px !important; }

/* ANALYZING */
#pt-root #analyzing {
  display:flex !important; position:fixed !important; top:0 !important; left:0 !important; right:0 !important; bottom:0 !important;
  background:rgba(6,0,12,0.93) !important; z-index:1000300 !important;
  flex-direction:column !important; align-items:center !important; justify-content:center !important; gap:16px !important;
}
#pt-root #analyzing.hidden { display:none !important; }
#pt-root .pulse-heart { display:block !important; font-size:56px !important; animation:pt-hb .65s ease-in-out infinite alternate !important; }
@keyframes pt-hb { from{transform:scale(1)} to{transform:scale(1.28)} }
#pt-root .an-title { display:block !important; color:#ff9ec8 !important; font-family:'Playfair Display',serif !important; font-size:20px !important; font-style:italic !important; text-shadow:0 0 14px #ff1493 !important; }
#pt-root .an-sub   { display:block !important; color:rgba(255,179,217,.55) !important; font-size:13px !important; }
#pt-root .load-wrap { display:block !important; width:220px !important; height:6px !important; background:rgba(255,255,255,.08) !important; border-radius:3px !important; overflow:hidden !important; }
#pt-root .load-bar  { display:block !important; height:100% !important; background:linear-gradient(90deg,#ff1493,#ff69b4) !important; border-radius:3px !important; transition:width .2s !important; }

/* FINAL */
#pt-root #final-score { display:block !important; color:#ffe0f0 !important; font-size:clamp(38px,10vw,50px) !important; font-family:'Playfair Display',serif !important; text-shadow:0 0 18px #ff1493 !important; margin:12px 0 !important; }
#pt-root #final-label { display:block !important; color:#ffb3e6 !important; font-size:13px !important; font-style:italic !important; }

/* BUTTONS */
#pt-root .btn {
  display:inline-block !important;
  background:linear-gradient(135deg,#c0006e,#8b0000) !important;
  color:#fff0f8 !important; border:none !important; border-radius:10px !important;
  padding:clamp(10px,3vw,13px) clamp(20px,5vw,28px) !important;
  font-size:clamp(13px,3.5vw,15px) !important; cursor:pointer !important;
  margin:5px !important; font-family:'Playfair Display',serif !important;
  letter-spacing:1px !important; box-shadow:0 4px 16px rgba(192,0,110,0.3) !important;
  transition:transform .15s,box-shadow .15s !important;
}
#pt-root .btn:active { transform:scale(1.06) !important; box-shadow:0 0 22px rgba(192,0,110,0.6) !important; }

/* UNLOCK SCREEN */
#pt-root #unlock-screen {
  display:flex !important; position:fixed !important; top:0 !important; left:0 !important; right:0 !important; bottom:0 !important;
  background:#07000e !important; z-index:1000400 !important;
  flex-direction:column !important; align-items:center !important; justify-content:center !important; gap:20px !important;
}
#pt-root #unlock-screen.hidden { display:none !important; }
#pt-root .unlock-emoji  { display:block !important; font-size:64px !important; animation:pt-hb .65s ease-in-out infinite alternate !important; }
#pt-root .unlock-title  { display:block !important; color:#ff9ec8 !important; font-family:'Playfair Display',serif !important; font-size:26px !important; font-style:italic !important; text-shadow:0 0 14px #ff1493 !important; text-align:center !important; }
#pt-root .unlock-sub    { display:block !important; color:rgba(255,179,217,.6) !important; font-size:13px !important; text-align:center !important; }
#pt-root .unlock-btn {
  display:block !important;
  background:linear-gradient(135deg,#c0006e,#8b0000) !important;
  color:#fff0f8 !important; border:none !important; border-radius:16px !important;
  padding:18px 48px !important; font-size:20px !important; cursor:pointer !important;
  font-family:'Playfair Display',serif !important; letter-spacing:2px !important;
  box-shadow:0 0 30px rgba(192,0,110,0.5) !important;
  animation:pt-pulse 1.2s ease-in-out infinite alternate !important;
}
@keyframes pt-pulse { from{box-shadow:0 0 20px rgba(192,0,110,0.4)} to{box-shadow:0 0 45px rgba(255,20,147,0.75)} }
</style>
</head>
<body>
<div id="pt-root">

  <canvas id="bg-canvas"></canvas>

  <div id="app">
    <div id="header">
      <h1>💕 Piano Tiles 💕</h1>
      <div id="score-val">0</div>
    </div>
    <div id="song-bar">
      <div id="song-name">Choisis une musique...</div>
      <div id="combo-val">Combo: 0x</div>
      <div id="speed-val">♩ ×1.0</div>
    </div>
    <div id="prog-wrap"><div id="prog-bar"></div></div>
    <div id="game-area">
      <canvas id="game-canvas"></canvas>
    </div>
    <div id="keys">
      <div class="key" data-col="0"><span class="key-lbl">A</span></div>
      <div class="key" data-col="1"><span class="key-lbl">S</span></div>
      <div class="key" data-col="2"><span class="key-lbl">D</span></div>
      <div class="key" data-col="3"><span class="key-lbl">F</span></div>
    </div>
  </div>

  <div id="miss-flash"></div>
  <div id="perfect-txt">💕 PERFECT!</div>

  <!-- Écran de démarrage — déblocage audio iOS obligatoire -->
  <div id="unlock-screen">
    <div class="unlock-emoji">💕</div>
    <div class="unlock-title">Piano Tiles</div>
    <div class="unlock-sub">TON JEU, Ibtissem ✨💗</div>
    <button class="unlock-btn" id="unlock-btn">▶ JOUER</button>
  </div>

  <!-- Chargement -->
  <div id="analyzing" class="hidden">
    <div class="pulse-heart">💗</div>
    <div class="an-title">Chargement...</div>
    <div class="an-sub" id="an-sub">Analyse du rythme</div>
    <div class="load-wrap"><div class="load-bar" id="an-bar" style="width:0%"></div></div>
  </div>

  <!-- Menu / Résultats -->
  <div id="overlay" class="hidden">
    <div id="panel">
      <div class="panel-title" id="p-title">💕 Piano Tiles 💕</div>
      <div class="panel-sub"  id="p-sub">uN jEu, our toi ✨<br>Choisis une musique !</div>
      <div id="p-body"></div>
    </div>
  </div>

</div>

<script>
'use strict';

// ══════════════════════════════════════════════════════
//  🎵 CONFIGURATION — ajoute tes chansons ici
// ══════════════════════════════════════════════════════
const SONGS_CONFIG = [
  {
    file:   './G-Eazy & Halsey - Him & I (Official Video).mp3',   // ← nom du fichier MP3
    title:  'Him & I',  // ← nom affiché
    artist: 'G-Eazy & Halsey',              // ← artiste affiché
    emoji:  '🌹',                   // ← emoji affiché
  },
  {
    file:   './Bessan Ismail - Al Harbein (Official Music Video)  بيسان اسماعيل - الحربين.mp3',
    title:  'Al Harbein',
    artist: 'Bessan Ismail',
    emoji:  '💕',
  },
  // Ajoute autant de chansons que tu veux :
  // { file: 'music/chanson3.mp3', title: '...', artist: '...', emoji: '✨' },
];
// ══════════════════════════════════════════════════════

// ══════════════════════════════════════════════════════
//  AUDIO — Double stratégie iPhone/Safari
//  • HTMLAudioElement pour la lecture (100% compatible iOS)
//  • WebAudioContext uniquement pour la beat detection
// ══════════════════════════════════════════════════════
let AC = null;
function getAC() {
  if (!AC) AC = new (window.AudioContext || window.webkitAudioContext)();
  return AC;
}

// Déblocage audio iOS : on crée un AudioContext + on joue un son
// OBLIGATOIREMENT dans le handler synchrone du touchend
const unlockBtn = document.getElementById('unlock-btn');
let audioUnlocked = false;

function doUnlock(e) {
  e.preventDefault();
  e.stopPropagation();

  // 1. Créer l'AudioContext dans le geste (synchrone)
  const ctx = getAC();

  // 2. Jouer un buffer silencieux — débloque Safari
  try {
    const buf = ctx.createBuffer(1, 1, 22050);
    const src = ctx.createBufferSource();
    src.buffer = buf;
    src.connect(ctx.destination);
    src.start(0);
  } catch(err) {}

  // 3. Resume (au cas où suspendu)
  const doStart = () => {
    audioUnlocked = true;
    document.getElementById('unlock-screen').classList.add('hidden');
    preloadAll();
  };

  if (ctx.state === 'suspended') {
    ctx.resume().then(doStart).catch(doStart);
  } else {
    doStart();
  }
}

// iOS : touchend déclenche le déblocage audio de façon synchrone
unlockBtn.addEventListener('touchend', doUnlock, { passive: false });
// PC : click normal
unlockBtn.addEventListener('click', doUnlock);

// ── Beat Detection ──
async function detectBeats(buffer) {
  const sr = buffer.sampleRate;
  const data = buffer.getChannelData(0);
  const winMs = 10, frameSz = Math.floor(sr * winMs / 1000);
  const numFr = Math.floor(data.length / frameSz);
  const energies = new Float32Array(numFr);
  for (let i = 0; i < numFr; i++) {
    let e = 0; const s = i*frameSz, end = s+frameSz;
    for (let j = s; j < end; j++) e += data[j]*data[j];
    energies[i] = e / frameSz;
  }
  const avgWin = Math.floor(1500/winMs), minGap = Math.floor(200/winMs);
  const beats = []; let lastBeat = -minGap;
  for (let i = avgWin; i < numFr-avgWin; i++) {
    let avg = 0;
    for (let j = i-avgWin; j < i+avgWin; j++) avg += energies[j];
    avg /= avgWin*2;
    if (energies[i] > 1.45*avg && i-lastBeat > minGap) {
      let peak = true;
      for (let k=i-3;k<=i+3;k++) { if(k!==i&&k>=0&&k<numFr&&energies[k]>=energies[i]){peak=false;break;} }
      if (peak) { beats.push(i*winMs/1000); lastBeat=i; }
    }
  }
  let bpm = 120;
  if (beats.length > 4) {
    const ibi = []; for(let i=1;i<beats.length;i++) ibi.push(beats[i]-beats[i-1]);
    ibi.sort((a,b)=>a-b);
    bpm = Math.round(60/ibi[ibi.length>>1]);
    while(bpm>180) bpm>>=1; while(bpm<55) bpm<<=1;
  }
  const patterns=[[0,2,1,3],[1,3,0,2],[2,0,3,1],[3,1,2,0],[0,1,3,2],[2,3,0,1],[1,0,2,3],[3,2,1,0]];
  let pi=0,pp=0;
  const beatData = beats.map(t => {
    const col=patterns[pi%patterns.length][pp%4]; pp++; if(pp%4===0) pi++;
    return {time:t,col};
  });
  return {beats:beatData, bpm, duration:buffer.duration};
}

const loadedSongs = [];

async function preloadAll() {
  showAnalyzing('Chargement...', 0);
  const total = SONGS_CONFIG.length; let done = 0;
  for (const cfg of SONGS_CONFIG) {
    try {
      updAn(`Chargement : ${cfg.title}`, done/total*60);

      // Fetch pour beat detection (WebAudio)
      const res = await fetch(cfg.file);
      if (!res.ok) throw new Error('Fichier introuvable : ' + cfg.file);
      const ab  = await res.arrayBuffer();

      updAn(`Analyse : ${cfg.title}`, done/total*60+30/total);

      // Décoder pour analyse beats uniquement
      const buf = await getAC().decodeAudioData(ab.slice(0)); // slice = copie
      const r   = await detectBeats(buf);

      // HTMLAudio pour la lecture — 100% compatible iOS/Safari
      const audioEl = new Audio(cfg.file);
      audioEl.preload = 'auto';
      audioEl.load();

      loadedSongs.push({ config: cfg, audioEl, beats: r.beats, bpm: r.bpm, duration: r.duration });
    } catch(err) {
      console.warn('Erreur chanson:', cfg.file, err.message);
    }
    done++; updAn(`${done}/${total} musique(s)`, done/total*100);
  }
  hideAnalyzing(); renderMenu();
}

// ── Game State ──
const G = { song:null, tiles:[], score:0, combo:0, speedMult:1, beatIdx:0, lastSpawn:-1, running:false, src:null, startT:0, raf:null };

// ── Canvas ──
const gc = document.getElementById('game-canvas');
const gx = gc.getContext('2d');
const COLS=4, TH=120, HR=0.80;
function resGC() { gc.width=gc.offsetWidth; gc.height=gc.offsetHeight; }
resGC(); window.addEventListener('resize', resGC);

const TC=[['#c0006e','#7a0045'],['#8b0000','#5a0000'],['#c0006e','#7a0045'],['#8b0000','#5a0000']];
const TG=['#ff69b4','#ff5555','#ff69b4','#ff5555'];

function drawTile(t) {
  const W=gc.width/COLS, x=t.col*W;
  gx.save();
  const g=gx.createLinearGradient(x,t.y,x,t.y+TH);
  g.addColorStop(0,TC[t.col][0]); g.addColorStop(1,TC[t.col][1]);
  gx.fillStyle=g; gx.shadowColor=TG[t.col]; gx.shadowBlur=16;
  gx.beginPath(); gx.roundRect(x+3,t.y+3,W-6,TH-6,8); gx.fill();
  gx.shadowBlur=0;
  gx.strokeStyle=t.col%2===0?'rgba(255,160,215,.5)':'rgba(255,130,130,.45)'; gx.lineWidth=1.5;
  gx.beginPath(); gx.roundRect(x+3,t.y+3,W-6,TH-6,8); gx.stroke();
  gx.fillStyle='rgba(255,255,255,.07)';
  gx.beginPath(); gx.roundRect(x+8,t.y+8,W-16,26,5); gx.fill();
  gx.restore();
}

function drawScene() {
  for(let i=1;i<COLS;i++){
    const x=gc.width/COLS*i;
    gx.save(); gx.strokeStyle='rgba(192,0,110,.09)'; gx.lineWidth=1;
    gx.beginPath(); gx.moveTo(x,0); gx.lineTo(x,gc.height); gx.stroke(); gx.restore();
  }
  const hy=gc.height*HR;
  gx.save(); gx.strokeStyle='rgba(192,0,110,.4)'; gx.lineWidth=1.5;
  gx.setLineDash([10,7]); gx.beginPath(); gx.moveTo(0,hy); gx.lineTo(gc.width,hy); gx.stroke();
  gx.setLineDash([]); gx.restore();
}

const parts=[];
function spawnParts(col){
  const W=gc.width/COLS, x=col*W+W/2, y=gc.height*HR;
  for(let i=0;i<12;i++){
    const a=Math.random()*Math.PI*2, s=2+Math.random()*5;
    parts.push({x,y,vx:Math.cos(a)*s,vy:Math.sin(a)*s-2.5,alpha:1,r:2+Math.random()*4,col});
  }
}
function drawParts(){
  for(let i=parts.length-1;i>=0;i--){
    const p=parts[i]; p.x+=p.vx; p.y+=p.vy; p.vy+=0.18; p.alpha-=0.04;
    if(p.alpha<=0){parts.splice(i,1);continue;}
    gx.save(); gx.globalAlpha=p.alpha; gx.fillStyle=TG[p.col]; gx.shadowColor=TG[p.col]; gx.shadowBlur=8;
    gx.beginPath(); gx.arc(p.x,p.y,p.r,0,Math.PI*2); gx.fill(); gx.restore();
  }
}

let lastTs=0;
function loop(ts){
  if(!G.running) return;
  const dt=Math.min(ts-lastTs,50); lastTs=ts;
  resGC(); gx.clearRect(0,0,gc.width,gc.height);

  // Utilise HTMLAudio.currentTime pour la sync — fonctionne sur iPhone
  const elapsed = G.src ? G.src.currentTime : 0;

  const pps=(3+G.speedMult*2.5)*60;
  const travel=(gc.height*HR)/pps;
  for(let i=G.beatIdx;i<G.song.beats.length;i++){
    const b=G.song.beats[i];
    if(elapsed>=b.time-travel){
      if(b.time>G.lastSpawn){ G.tiles.push({col:b.col,y:-TH,active:true}); G.lastSpawn=b.time; }
      G.beatIdx=i+1;
    } else break;
  }
  const spd=pps*dt/1000;
  for(const t of G.tiles) if(t.active) t.y+=spd;
  G.tiles=G.tiles.filter(t=>{
    if(!t.active) return false;
    if(t.y>gc.height+10){ doMiss(); return false; }
    return true;
  });
  if(!G.running) return;
  document.getElementById('prog-bar').style.width=Math.min(elapsed/G.song.duration*100,100)+'%';
  if(elapsed>=G.song.duration+travel+1&&G.tiles.length===0){endGame(true);return;}
  drawScene(); for(const t of G.tiles) drawTile(t); drawParts();
  G.raf=requestAnimationFrame(loop);
}

function doMiss(){
  if(!G.running) return;
  G.combo=0; document.getElementById('combo-val').textContent='Combo: 0x';
  flashMiss(); endGame(false);
}

function hitCol(col){
  if(!G.running) return;
  const hy=gc.height*HR; let best=null, bestD=9999;
  for(const t of G.tiles){
    if(t.col===col&&t.active){
      const d=Math.abs((t.y+TH/2)-hy);
      if(d<TH*0.85&&d<bestD){best=t;bestD=d;}
    }
  }
  if(best){
    best.active=false;
    G.score+=bestD<25?15:bestD<55?12:8;
    G.combo++;
    G.score+=Math.floor(G.combo/5)*3;
    document.getElementById('score-val').textContent=G.score;
    document.getElementById('combo-val').textContent='Combo: '+G.combo+'x';
    spawnParts(col); showPerfect(G.combo);
    if(G.combo%15===0){
      G.speedMult=Math.min(2.5,+(G.speedMult+0.1).toFixed(1));
      document.getElementById('speed-val').textContent='♩ ×'+G.speedMult.toFixed(1);
    }
  } else {
    G.combo=0; document.getElementById('combo-val').textContent='Combo: 0x';
    flashMiss(); endGame(false);
  }
}

function startGame(idx){
  // Arrêter l'audio précédent
  if(G.src){
    try { G.src.pause(); G.src.currentTime=0; } catch(e){}
    G.src = null;
  }

  // Résume AudioContext si suspendu (iOS)
  const ctx = getAC();
  if(ctx.state === 'suspended') ctx.resume();

  const song = loadedSongs[idx];
  Object.assign(G, {song, tiles:[], score:0, combo:0, speedMult:1, beatIdx:0, lastSpawn:-1, running:true});
  parts.length = 0;

  document.getElementById('score-val').textContent  = '0';
  document.getElementById('combo-val').textContent  = 'Combo: 0x';
  document.getElementById('speed-val').textContent  = '♩ ×1.0';
  document.getElementById('song-name').textContent  = song.config.title + '  ·  ' + song.config.artist;
  document.getElementById('prog-bar').style.width   = '0%';
  hideOverlay();

  // Lecture via HTMLAudioElement — compatible iPhone Safari
  const audio = song.audioEl;
  audio.currentTime = 0;
  audio.volume = 1;

  // On note l'heure de début via AudioContext pour la sync beats
  const playPromise = audio.play();
  G.src    = audio;
  G.startT = ctx.currentTime; // référence temps AudioContext

  if(playPromise !== undefined){
    playPromise.catch(err => {
      console.warn('Audio play failed:', err);
      // Retry après interaction
    });
  }

  audio.onended = () => {
    if(G.running) setTimeout(()=>{ if(G.running) endGame(true); }, 2000);
  };

  if(G.raf) cancelAnimationFrame(G.raf);
  lastTs = performance.now();
  G.raf = requestAnimationFrame(loop);
}

function endGame(win){
  G.running=false; if(G.raf) cancelAnimationFrame(G.raf);
  if(G.src){ try{ G.src.pause(); G.src.currentTime=0; }catch(e){} G.src=null; }
  const name=G.song?G.song.config.title:'—';
  const idx=loadedSongs.indexOf(G.song);
  const body=win
    ?`<div id="final-score">${G.score}</div><div id="final-label">${name}</div><div class="panel-sub" style="margin-top:10px">Combo max : ${G.combo}x ✨</div>`
    :`<div id="final-score">${G.score}</div><div id="final-label">${name}</div><div class="panel-sub" style="margin-top:10px">Tu peux faire mieux ! 🌹</div>`;
  showPanel(
    win?'🎉 Bravo Ibtissem! 💕':'💔 Raté...',
    body,
    [{label:win?'Rejouer':'Réessayer',cb:()=>startGame(idx)},{label:'Menu',cb:renderMenu}]
  );
}

// ── UI ──
function flashMiss(){
  const el=document.getElementById('miss-flash');
  el.style.opacity='1';
  requestAnimationFrame(()=>{ el.style.transition='opacity .35s'; el.style.opacity='0'; setTimeout(()=>el.style.transition='',400); });
}
function showPerfect(c){
  const el=document.getElementById('perfect-txt');
  el.textContent=c>=25?'🔥 INCROYABLE!':c>=15?'✨ MAGNIFIQUE!':c>=8?'💕 PARFAIT!':'❤️ PERFECT!';
  el.style.transition='none'; el.style.opacity='1';
  el.style.fontSize=Math.min(30,Math.max(22,window.innerWidth*.07))+'px';
  setTimeout(()=>{ el.style.transition='opacity .45s,font-size .45s'; el.style.opacity='0'; el.style.fontSize='22px'; },350);
}
function showOverlay()  { document.getElementById('overlay').classList.remove('hidden'); }
function hideOverlay()  { document.getElementById('overlay').classList.add('hidden'); }
function showAnalyzing(t,p){ document.querySelector('#analyzing .an-title').textContent=t; document.getElementById('an-bar').style.width=p+'%'; document.getElementById('analyzing').classList.remove('hidden'); }
function updAn(s,p)    { document.getElementById('an-sub').textContent=s; document.getElementById('an-bar').style.width=p+'%'; }
function hideAnalyzing(){ document.getElementById('analyzing').classList.add('hidden'); }

function showPanel(title,bodyHTML,btns){
  document.getElementById('p-title').textContent=title;
  document.getElementById('p-sub').style.display='none';
  const pb=document.getElementById('p-body'); pb.innerHTML=bodyHTML;
  const row=document.createElement('div'); row.style.marginTop='16px';
  btns.forEach(b=>{ const btn=document.createElement('button'); btn.className='btn'; btn.textContent=b.label; btn.onclick=b.cb; row.appendChild(btn); });
  pb.appendChild(row); showOverlay();
}

function renderMenu(){
  document.getElementById('p-title').textContent='💕 Piano Tiles 💕';
  document.getElementById('p-sub').style.display='';
  document.getElementById('p-sub').innerHTML='Pour toi, Ibtissem ✨<br>Choisis une musique !';
  const pb=document.getElementById('p-body'); pb.innerHTML='';
  if(loadedSongs.length===0){
    pb.innerHTML='<div style="color:rgba(255,179,217,.45);font-style:italic;font-size:13px;padding:12px 0">Aucune chanson chargée.<br>Vérifie les noms des fichiers MP3.</div>';
  } else {
    loadedSongs.forEach((song,i)=>{
      const el=document.createElement('div'); el.className='song-item';
      el.innerHTML=`<div class="song-icon">${song.config.emoji}</div><div class="song-info"><div class="song-title">${song.config.title}</div><div class="song-artist">${song.config.artist}</div><div class="song-bpm">${song.bpm} BPM · ${fmt(song.duration)}</div></div>`;
      // Touch natif iPhone
      el.addEventListener('touchend', (e)=>{ e.preventDefault(); startGame(i); }, {passive:false});
      el.addEventListener('click', ()=>startGame(i));
      pb.appendChild(el);
    });
  }
  showOverlay();
}

function fmt(s){ return Math.floor(s/60)+':'+String(Math.floor(s%60)).padStart(2,'0'); }

// ── Touch iPhone — écoute sur toute la zone #keys ──
const keysEl = document.getElementById('keys');

keysEl.addEventListener('touchstart', function(e){
  e.preventDefault(); e.stopPropagation();
  const rect=keysEl.getBoundingClientRect();
  for(let i=0;i<e.changedTouches.length;i++){
    const t=e.changedTouches[i];
    const col=Math.floor((t.clientX-rect.left)/(rect.width/COLS));
    if(col>=0&&col<COLS){
      hitCol(col);
      const k=document.querySelector(`.key[data-col="${col}"]`);
      if(k){ k.classList.add('pressed'); setTimeout(()=>k.classList.remove('pressed'),130); }
    }
  }
}, {passive:false});

keysEl.addEventListener('touchmove',   e=>e.preventDefault(), {passive:false});
keysEl.addEventListener('touchend',    e=>e.preventDefault(), {passive:false});
keysEl.addEventListener('touchcancel', e=>e.preventDefault(), {passive:false});

// ── Mouse PC ──
document.querySelectorAll('.key').forEach(k=>{
  const col=+k.dataset.col;
  k.addEventListener('mousedown', e=>{ e.preventDefault(); k.classList.add('pressed'); hitCol(col); });
  k.addEventListener('mouseup',    ()=>k.classList.remove('pressed'));
  k.addEventListener('mouseleave', ()=>k.classList.remove('pressed'));
});

// ── Clavier PC ──
document.addEventListener('keydown', e=>{
  if(e.repeat) return;
  const m={a:0,s:1,d:2,f:3};
  if(m[e.key]!==undefined){
    hitCol(m[e.key]);
    const k=document.querySelector(`.key[data-col="${m[e.key]}"]`);
    if(k){ k.classList.add('pressed'); setTimeout(()=>k.classList.remove('pressed'),110); }
  }
  if(e.key==='Escape'&&G.running) endGame(false);
});

// Bloquer scroll/zoom sur tout le jeu
document.getElementById('pt-root').addEventListener('touchmove', e=>e.preventDefault(), {passive:false});

// ── Background hearts ──
const bgC=document.getElementById('bg-canvas'), bgX=bgC.getContext('2d');
const EM=['❤️','🌸','💕','💖','🌹','✨','💗','🥀','💝','🌷','💞','🦋','💓','🌺','💘'];
function rzBg(){ bgC.width=innerWidth; bgC.height=innerHeight; }
rzBg(); window.addEventListener('resize',rzBg);
const BH=Array.from({length:30},()=>({x:Math.random()*100,y:Math.random()*110,sz:14+Math.random()*22,sp:.009+Math.random()*.022,em:EM[Math.random()*EM.length|0],al:.06+Math.random()*.12,rot:Math.random()*Math.PI*2,rs:(Math.random()-.5)*.012}));
function bgLoop(){
  bgX.clearRect(0,0,bgC.width,bgC.height);
  for(const h of BH){
    h.y-=h.sp; h.rot+=h.rs;
    if(h.y<-5){h.y=105+Math.random()*10;h.x=Math.random()*100;h.em=EM[Math.random()*EM.length|0];}
    bgX.save(); bgX.globalAlpha=h.al;
    bgX.translate(h.x/100*bgC.width,h.y/100*bgC.height); bgX.rotate(h.rot);
    bgX.font=h.sz+'px serif'; bgX.textAlign='center'; bgX.textBaseline='middle';
    bgX.fillText(h.em,0,0); bgX.restore();
  }
  requestAnimationFrame(bgLoop);
}
bgLoop();
</script>
</body>
</html>
