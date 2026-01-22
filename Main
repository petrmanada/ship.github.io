<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Neon Orbit: Hangar & Upgrades</title>
  <style>
    :root { color-scheme: dark; }
    html, body { height: 100%; margin: 0; background:#06070a; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial; }
    canvas { display:block; width:100vw; height:100vh; }

    .hud {
      position: fixed; inset: 0;
      pointer-events: none;
      display: grid; grid-template-columns: 1fr auto; grid-template-rows: auto 1fr auto;
      padding: 14px;
      color: rgba(255,255,255,.92);
      text-shadow: 0 0 12px rgba(120,220,255,.25);
      font-weight: 700;
      z-index: 5;
      gap: 10px;
    }
    .topLeft { grid-column: 1; grid-row: 1; display:flex; flex-wrap:wrap; gap:10px; align-items: baseline; }
    .topRight { grid-column: 2; grid-row: 1; text-align:right; display:flex; flex-wrap:wrap; gap:10px; justify-content:flex-end; }
    .bottom { grid-column: 1 / -1; grid-row: 3; display:flex; justify-content:space-between; gap:10px; align-items:flex-end; color: rgba(255,255,255,.72); }

    .chip {
      padding: 6px 10px; border-radius: 999px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.10);
      backdrop-filter: blur(8px);
      white-space: nowrap;
    }

    .overlay {
      position: fixed; inset: 0;
      display: none;
      align-items: center; justify-content: center;
      pointer-events: auto;
      z-index: 10;
    }
    .panel {
      max-width: 860px; width: min(860px, calc(100vw - 28px));
      background: rgba(10,12,18,.74);
      border: 1px solid rgba(255,255,255,.12);
      border-radius: 18px;
      padding: 18px 18px;
      box-shadow: 0 0 0 1px rgba(70,200,255,.08), 0 18px 70px rgba(0,0,0,.55);
      backdrop-filter: blur(10px);
      pointer-events: auto;
      user-select: none;
    }
    .panel h1 { margin: 0 0 8px; font-size: 22px; letter-spacing: .3px; color: rgba(255,255,255,.96); }
    .panel p { margin: 8px 0; line-height: 1.45; color: rgba(255,255,255,.82); font-weight: 600;}

    .row { display:flex; gap:10px; align-items:center; flex-wrap:wrap; }
    .grid2 { display:grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    @media (max-width: 820px) { .grid2 { grid-template-columns: 1fr; } }

    .card {
      border-radius: 16px;
      background: rgba(255,255,255,.05);
      border: 1px solid rgba(255,255,255,.10);
      padding: 12px 12px;
    }
    .card h2 { margin: 0 0 6px; font-size: 15px; letter-spacing:.2px; }
    .muted { color: rgba(255,255,255,.72); font-weight: 600; }
    .small { font-size: 12px; opacity: .9; font-weight: 650; }

    .btn {
      border: 1px solid rgba(255,255,255,.14);
      background: rgba(90,240,255,.10);
      color: rgba(255,255,255,.92);
      border-radius: 14px;
      padding: 10px 12px;
      cursor: pointer;
      font-weight: 900;
      letter-spacing: .2px;
      box-shadow: 0 0 0 1px rgba(60,220,255,.10), 0 10px 30px rgba(0,0,0,.25);
      transition: transform .08s ease, background .2s ease, opacity .2s ease;
    }
    .btn:active { transform: translateY(1px) scale(.99); }
    .btn:hover { background: rgba(90,240,255,.15); }
    .btn.secondary { background: rgba(255,255,255,.06); }
    .btn.danger { background: rgba(255,80,110,.14); }
    .btn:disabled { opacity: .45; cursor: not-allowed; }

    .tabs { display:flex; flex-wrap:wrap; gap:10px; margin-top: 10px; }
    .pill { padding: 9px 12px; border-radius: 999px; background: rgba(255,255,255,.06); border: 1px solid rgba(255,255,255,.10); cursor:pointer; font-weight: 850; }
    .pill.active { background: rgba(90,240,255,.12); border-color: rgba(90,240,255,.25); }

    .list { display:grid; gap:10px; margin-top: 10px; }
    .item {
      display:flex; gap:12px; justify-content:space-between; align-items:center; flex-wrap:wrap;
      padding: 10px 12px; border-radius: 14px;
      background: rgba(255,255,255,.05);
      border: 1px solid rgba(255,255,255,.10);
    }
    .item .left { display:flex; flex-direction:column; gap:2px; }
    .item .title { font-weight: 950; }
    .item .desc { font-size: 12px; opacity:.85; font-weight: 650; }
    .item .right { display:flex; gap:10px; align-items:center; flex-wrap:wrap; justify-content:flex-end; }

    .kbd {
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
      padding: 3px 7px; border-radius: 10px;
      background: rgba(255,255,255,.08);
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: inset 0 -2px 0 rgba(0,0,0,.35);
      color: rgba(255,255,255,.92);
      white-space: nowrap;
      font-weight: 800;
    }
    .toast {
      position: fixed; left: 50%; bottom: 14px; transform: translateX(-50%);
      background: rgba(10,12,18,.78);
      border: 1px solid rgba(255,255,255,.12);
      border-radius: 14px;
      padding: 10px 12px;
      color: rgba(255,255,255,.9);
      font-weight: 800;
      box-shadow: 0 0 0 1px rgba(70,200,255,.08), 0 18px 60px rgba(0,0,0,.45);
      backdrop-filter: blur(10px);
      opacity: 0;
      pointer-events: none;
      transition: opacity .2s ease, transform .2s ease;
      z-index: 20;
    }
    .toast.show { opacity: 1; transform: translateX(-50%) translateY(-4px); }
  </style>
</head>
<body>
<canvas id="c"></canvas>

<div class="hud">
  <div class="topLeft">
    <div class="chip" id="scoreChip">Score: 0</div>
    <div class="chip" id="comboChip">Combo: x1</div>
    <div class="chip" id="dangerChip">Threat: 0%</div>
    <div class="chip" id="shipChip">Ship: -</div>
  </div>
  <div class="topRight">
    <div class="chip" id="hpChip">HP: 100</div>
    <div class="chip" id="energyChip">Energy: 100</div>
    <div class="chip" id="creditsChip">Credits: 0</div>
  </div>
  <div class="bottom">
    <div class="chip">Keys: <span class="kbd">WASD</span> move · <span class="kbd">LMB</span> shoot · <span class="kbd">Shift</span> dash · <span class="kbd">Space</span> pulse · <span class="kbd">P</span> pause</div>
    <div class="chip">Tip: Pulse clears space. Dash gives invulnerability.</div>
  </div>
</div>

<div class="overlay" id="overlay">
  <div class="panel">
    <h1 id="title">Neon Orbit</h1>
    <p id="subtitle" class="muted">Survive, earn credits, upgrade your ship, and unlock new hulls.</p>

    <div class="tabs">
      <div class="pill active" data-tab="menu">Main Menu</div>
      <div class="pill" data-tab="upgrades">Upgrades</div>
      <div class="pill" data-tab="hangar">Hangar</div>
      <div class="pill" data-tab="crates">Crates</div>
    </div>

    <div id="tab_menu" class="list">
      <div class="card">
        <h2>Play</h2>
        <p class="muted" style="margin:6px 0 10px;">Jump into a run. You keep your upgrades + unlocked ships.</p>
        <div class="row">
          <button class="btn" id="playBtn">Play</button>
          <button class="btn secondary" id="resumeBtn" style="display:none;">Resume</button>
          <button class="btn secondary" id="resetBtn" title="Resets saved progress">Reset Save</button>
          <span class="small muted" id="seedInfo"></span>
        </div>
        <p class="small muted" style="margin-top:10px;">
          Earn credits: roughly <span class="kbd">score/20</span> + <span class="kbd">seconds survived</span> (bonus for high score).
        </p>
      </div>

      <div class="grid2">
        <div class="card">
          <h2>Active Loadout</h2>
          <div class="muted small" id="activeInfo">-</div>
        </div>
        <div class="card">
          <h2>How to play</h2>
          <div class="muted small">
            Keep moving. Enemies lead your drift. Pulse when crowded. Dash through contact damage.
          </div>
        </div>
      </div>
    </div>

    <div id="tab_upgrades" class="list" style="display:none;">
      <div class="card">
        <h2>Upgrade Shop</h2>
        <p class="muted" style="margin:6px 0 0;">Upgrades are permanent. Costs scale up each level.</p>
        <div class="list" id="upgradeList" style="margin-top:10px;"></div>
      </div>
      <div class="card">
        <h2>Notes</h2>
        <div class="muted small">
          Max HP helps a lot. Damage helps combo. Regen helps constant firing. Dash Efficiency reduces dash cost.
        </div>
      </div>
    </div>

    <div id="tab_hangar" class="list" style="display:none;">
      <div class="card">
        <h2>Hangar</h2>
        <p class="muted" style="margin:6px 0 0;">Pick a ship you’ve unlocked. Each ship changes stats/feel.</p>
        <div class="list" id="shipList" style="margin-top:10px;"></div>
      </div>
    </div>

    <div id="tab_crates" class="list" style="display:none;">
      <div class="card">
        <h2>Ship Crates (Credits Only)</h2>
        <p class="muted" style="margin:6px 0 0;">
          Spend credits to roll for a new ship. If you roll one you already own, you get a credit refund bonus.
        </p>
        <div class="item" style="margin-top:10px;">
          <div class="left">
            <div class="title">Standard Ship Crate</div>
            <div class="desc">Odds: Rare 12% · Epic 3% · Legendary 0.8% (rest Common). Pity increases Legendary chance slightly each miss.</div>
          </div>
          <div class="right">
            <div class="chip">Cost: <span id="crateCostText">600</span> credits</div>
            <button class="btn" id="openCrateBtn">Open Crate</button>
          </div>
        </div>

        <div class="card" id="crateResult" style="display:none;">
          <h2>Crate Result</h2>
          <div class="muted" id="crateResultText"></div>
        </div>

        <div class="card">
          <h2>Why this is “gambling” but safe</h2>
          <div class="muted small">
            This uses only in-game credits earned by playing (no real money, no cashout). Odds are shown.
            If you want, I can also add a “direct purchase” option so players can buy ships outright with enough credits.
          </div>
        </div>
      </div>
    </div>

    <div class="row" style="justify-content:space-between; margin-top: 12px;">
      <div class="row">
        <button class="btn secondary" id="closeBtn">Close</button>
        <span class="small muted">Press <span class="kbd">P</span> to pause during play.</span>
      </div>
      <div class="row">
        <span class="chip">Credits: <span id="creditsInline">0</span></span>
      </div>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
(() => {
  // ===== Canvas =====
  const canvas = document.getElementById("c");
  const ctx = canvas.getContext("2d", { alpha: false });

  let W=0, H=0, DPR=1;
  function resize() {
    DPR = Math.max(1, Math.min(2, window.devicePixelRatio || 1));
    W = Math.floor(innerWidth);
    H = Math.floor(innerHeight);
    canvas.width = Math.floor(W*DPR);
    canvas.height = Math.floor(H*DPR);
    canvas.style.width = W+"px";
    canvas.style.height = H+"px";
    ctx.setTransform(DPR,0,0,DPR,0,0);
  }
  addEventListener("resize", resize);
  resize();

  // ===== Helpers =====
  const clamp = (v,a,b)=>Math.max(a,Math.min(b,v));
  const dist2=(ax,ay,bx,by)=>{const dx=ax-bx,dy=ay-by;return dx*dx+dy*dy;};
  const angleTo=(ax,ay,bx,by)=>Math.atan2(by-ay,bx-ax);

  // ===== UI =====
  const ui = {
    overlay: document.getElementById("overlay"),
    title: document.getElementById("title"),
    subtitle: document.getElementById("subtitle"),
    tabs: [...document.querySelectorAll(".pill")],
    tab_menu: document.getElementById("tab_menu"),
    tab_upgrades: document.getElementById("tab_upgrades"),
    tab_hangar: document.getElementById("tab_hangar"),
    tab_crates: document.getElementById("tab_crates"),

    playBtn: document.getElementById("playBtn"),
    resumeBtn: document.getElementById("resumeBtn"),
    resetBtn: document.getElementById("resetBtn"),
    closeBtn: document.getElementById("closeBtn"),

    upgradeList: document.getElementById("upgradeList"),
    shipList: document.getElementById("shipList"),

    openCrateBtn: document.getElementById("openCrateBtn"),
    crateCostText: document.getElementById("crateCostText"),
    crateResult: document.getElementById("crateResult"),
    crateResultText: document.getElementById("crateResultText"),

    seedInfo: document.getElementById("seedInfo"),
    creditsInline: document.getElementById("creditsInline"),
    activeInfo: document.getElementById("activeInfo"),

    scoreChip: document.getElementById("scoreChip"),
    comboChip: document.getElementById("comboChip"),
    dangerChip: document.getElementById("dangerChip"),
    hpChip: document.getElementById("hpChip"),
    energyChip: document.getElementById("energyChip"),
    creditsChip: document.getElementById("creditsChip"),
    shipChip: document.getElementById("shipChip"),

    toast: document.getElementById("toast"),
  };

  function toast(msg){
    ui.toast.textContent = msg;
    ui.toast.classList.add("show");
    clearTimeout(toast._t);
    toast._t = setTimeout(()=>ui.toast.classList.remove("show"), 1400);
  }

  // ===== RNG =====
  let seed = (Math.random()*1e9)|0;
  ui.seedInfo.textContent = "Seed: " + seed;
  function rng(){ // xorshift32
    seed ^= seed<<13; seed|=0;
    seed ^= seed>>>17; seed|=0;
    seed ^= seed<<5; seed|=0;
    return (seed>>>0)/4294967296;
  }
  function rand(a=0,b=1){ return a+(b-a)*rng(); }

  // ===== Persistence =====
  const SAVE_KEY = "neon_orbit_save_v2";

  const Ships = [
    // id, name, rarity, desc, stats multipliers
    { id:"starter", name:"Starter Dart", rarity:"Common",
      desc:"Balanced training ship. Reliable and forgiving.",
      stats:{ hp:1.00, regen:1.00, dmg:1.00, speed:1.00, dashCost:1.00, pulse:1.00 } },

    { id:"bulwark", name:"Bulwark", rarity:"Common",
      desc:"Chunky hull. More HP, slightly slower.",
      stats:{ hp:1.18, regen:0.98, dmg:0.95, speed:0.95, dashCost:1.05, pulse:1.02 } },

    { id:"spark", name:"Sparkwing", rarity:"Rare",
      desc:"Fast and slippery. Lower HP but higher speed + regen.",
      stats:{ hp:0.92, regen:1.15, dmg:0.98, speed:1.10, dashCost:0.92, pulse:1.00 } },

    { id:"laser", name:"Laser Mantis", rarity:"Rare",
      desc:"Damage focused. Shots hit harder, but energy is picky.",
      stats:{ hp:0.98, regen:0.95, dmg:1.18, speed:1.02, dashCost:1.00, pulse:0.98 } },

    { id:"nova", name:"Nova Coil", rarity:"Epic",
      desc:"Pulse specialist. Bigger, nastier pulse; solid overall.",
      stats:{ hp:1.06, regen:1.02, dmg:1.05, speed:1.00, dashCost:0.98, pulse:1.22 } },

    { id:"phantom", name:"Phantom Shift", rarity:"Epic",
      desc:"Dash king. Super cheap dashes and high speed; lower damage.",
      stats:{ hp:0.96, regen:1.02, dmg:0.92, speed:1.12, dashCost:0.75, pulse:1.00 } },

    { id:"singularity", name:"Singularity Crown", rarity:"Legendary",
      desc:"High-end experimental hull. Strong damage + regen, a bit pricey to dash.",
      stats:{ hp:1.10, regen:1.12, dmg:1.22, speed:1.05, dashCost:1.10, pulse:1.10 } },
  ];

  const UpgradeDefs = [
    {
      id:"maxHp",
      name:"Max HP",
      desc:"+10 max HP per level (survivability).",
      baseCost: 250,
      costMult: 1.35,
      maxLevel: 12,
    },
    {
      id:"regen",
      name:"Energy Regen",
      desc:"+1.2 energy/sec per level (more shooting).",
      baseCost: 220,
      costMult: 1.33,
      maxLevel: 12,
    },
    {
      id:"damage",
      name:"Bullet Damage",
      desc:"+6% damage per level (faster kills).",
      baseCost: 320,
      costMult: 1.38,
      maxLevel: 10,
    },
    {
      id:"pulse",
      name:"Pulse Power",
      desc:"+7% pulse damage/knockback per level.",
      baseCost: 300,
      costMult: 1.36,
      maxLevel: 10,
    },
    {
      id:"dashEff",
      name:"Dash Efficiency",
      desc:"-6% dash energy cost per level (min 55%).",
      baseCost: 280,
      costMult: 1.36,
      maxLevel: 10,
    },
  ];

  function defaultSave(){
    return {
      credits: 0,
      ownedShips: ["starter"],
      activeShip: "starter",
      upgrades: { maxHp:0, regen:0, damage:0, pulse:0, dashEff:0 },
      // crate pity: increases legendary chance slightly on misses
      pity: { legendary: 0 }, // 0..25
    };
  }

  let save = loadSave();

  function loadSave(){
    try {
      const raw = localStorage.getItem(SAVE_KEY);
      if (!raw) return defaultSave();
      const obj = JSON.parse(raw);
      // merge-safe
      const d = defaultSave();
      obj.credits = Number(obj.credits ?? d.credits) || 0;
      obj.ownedShips = Array.isArray(obj.ownedShips) ? obj.ownedShips : d.ownedShips;
      obj.activeShip = obj.activeShip || d.activeShip;
      obj.upgrades = { ...d.upgrades, ...(obj.upgrades||{}) };
      obj.pity = { ...d.pity, ...(obj.pity||{}) };
      // ensure starter
      if (!obj.ownedShips.includes("starter")) obj.ownedShips.push("starter");
      if (!Ships.find(s=>s.id===obj.activeShip)) obj.activeShip = "starter";
      return obj;
    } catch {
      return defaultSave();
    }
  }
  function saveNow(){ localStorage.setItem(SAVE_KEY, JSON.stringify(save)); syncUI(); }

  // ===== Balance + Stats =====
  function getShip(){ return Ships.find(s=>s.id===save.activeShip) || Ships[0]; }

  function upgradeLevel(id){ return clamp(save.upgrades[id]||0, 0, 99); }

  function calcPlayerBase() {
    const ship = getShip();
    const u = save.upgrades;

    const maxHp = (100 + u.maxHp * 10) * ship.stats.hp;
    const regen = (14 + u.regen * 1.2) * ship.stats.regen;          // energy/sec
    const dmgMult = (1 + (u.damage * 0.06)) * ship.stats.dmg;       // bullet dmg multiplier
    const pulseMult = (1 + (u.pulse * 0.07)) * ship.stats.pulse;    // pulse multiplier
    const speedMult = ship.stats.speed;

    const dashEff = clamp(1 - u.dashEff * 0.06, 0.55, 1.00) * ship.stats.dashCost;

    return { maxHp, regen, dmgMult, pulseMult, speedMult, dashEff };
  }

  // ===== Game State =====
  let running=false, paused=false, gameOver=false;

  const world = {
    t:0, dt:0,
    shake:0, flash:0,
    score:0,
    combo:1,
    comboTimer:0,
    threat:0,
    difficulty:1,
    spawnTimer:0,
    powerTimer:0,
    particles:[],
    bullets:[],
    enemies:[],
    powerups:[],
    stars:[],
  };

  function initStars(){
    world.stars.length=0;
    const n = Math.floor((W*H)/18000);
    for(let i=0;i<n;i++) world.stars.push({ x:rand(0,W), y:rand(0,H), z:rand(0.2,1.0), tw:rand(0,10) });
  }
  initStars();

  const player = {
    x: W/2, y: H/2,
    vx:0, vy:0,
    r:14,
    hp:100,
    maxHp:100,
    energy:100,
    invuln:0,
    dashCd:0,
    pulseCd:0,
    overdrive:0,
    // derived:
    regen:14,
    dmgMult:1,
    pulseMult:1,
    speedMult:1,
    dashEff:1,
  };

  // ===== Effects =====
  function spawnParticles(x,y,count,speed,life,hueBase){
    for(let i=0;i<count;i++){
      const ang=rand(0,Math.PI*2);
      const s=rand(0.2,1.0)*speed;
      world.particles.push({ x,y, vx:Math.cos(ang)*s, vy:Math.sin(ang)*s, r:rand(1.2,3.0), life:rand(life*0.6,life*1.2), maxLife:life, hue:hueBase+rand(-25,25) });
    }
  }
  function ringShock(x,y,radius,hue){
    world.particles.push({ x,y, vx:0, vy:0, r:radius, ring:true, life:0.55, maxLife:0.55, hue });
  }

  // ===== Enemies =====
  function spawnEnemy(){
    const edge = Math.floor(rand(0,4));
    let x,y;
    const pad=40;
    if(edge===0){ x=-pad; y=rand(0,H); }
    if(edge===1){ x=W+pad; y=rand(0,H); }
    if(edge===2){ x=rand(0,W); y=-pad; }
    if(edge===3){ x=rand(0,W); y=H+pad; }

    const typeRoll=rng();
    let type="chaser";
    if(typeRoll>0.84) type="sniper";
    else if(typeRoll>0.62) type="splitter";

    const base=10+world.difficulty*1.6;
    const e={
      type,x,y,vx:0,vy:0,t:0,
      r: type==="sniper"?14:12,
      hp: type==="splitter"? (22+base*0.35) : (16+base*0.25),
      maxHp:1,
      shoot: rand(0.95, 1.55),
      hue: type==="sniper"?310:(type==="splitter"?160:200),
      value: type==="sniper"?40:(type==="splitter"?30:20),
      splitLevel: type==="splitter"?2:0
    };
    e.maxHp=e.hp;
    world.enemies.push(e);
  }
  function splitEnemy(e){
    if(e.splitLevel<=0) return;
    for(let i=0;i<2;i++){
      const ang=rand(0,Math.PI*2);
      const child={
        type:"chaser",
        x:e.x+Math.cos(ang)*8,
        y:e.y+Math.sin(ang)*8,
        vx:Math.cos(ang)*rand(30,70),
        vy:Math.sin(ang)*rand(30,70),
        r:Math.max(9,e.r-2),
        hp:Math.max(9,e.maxHp*0.40),
        maxHp:1,
        t:0,
        shoot:rand(0.7,1.5),
        hue:210,
        value:10,
        splitLevel:e.splitLevel-1
      };
      child.maxHp=child.hp;
      world.enemies.push(child);
    }
  }

  // ===== Powerups =====
  function spawnPowerup(){
    const roll=rng();
    let kind="heal";
    if(roll>0.66) kind="energy";
    else if(roll>0.38) kind="overdrive";
    world.powerups.push({
      kind,
      x: rand(80,W-80),
      y: rand(80,H-80),
      r: 12,
      t: 0,
      life: 14
    });
  }

  // ===== Shooting / Abilities =====
  function shoot(){
    const cost = player.overdrive>0 ? 5 : 8;
    if(player.energy<cost) return;
    player.energy -= cost;

    const a=angleTo(player.x,player.y,mouseX,mouseY);
    const spread = player.overdrive>0 ? 0.10 : 0.055;
    const pellets = player.overdrive>0 ? 2 : 1;

    for(let i=0;i<pellets;i++){
      const aa=a+rand(-spread,spread);
      const speed = player.overdrive>0 ? 850 : 740;
      world.bullets.push({
        x: player.x+Math.cos(aa)*18,
        y: player.y+Math.sin(aa)*18,
        vx: Math.cos(aa)*speed,
        vy: Math.sin(aa)*speed,
        r: 3.2,
        life: 1.0,
        hue: player.overdrive>0 ? 55 : 190,
        enemy:false
      });
    }
    world.shake=Math.max(world.shake, 2);
    spawnParticles(player.x+Math.cos(a)*16, player.y+Math.sin(a)*16, 6, 120, 0.35, 190);
  }

  function dash(){
    if(player.dashCd>0) return;
    const baseCost = 26;
    const cost = baseCost * player.dashEff;
    if(player.energy < cost) return;

    player.energy -= cost;
    const a=angleTo(player.x,player.y,mouseX,mouseY);
    const dashSpeed=690 * player.speedMult;
    player.vx += Math.cos(a)*dashSpeed;
    player.vy += Math.sin(a)*dashSpeed;

    player.invuln = Math.max(player.invuln, 0.30);
    player.dashCd = 0.95;

    ringShock(player.x,player.y,18,190);
    spawnParticles(player.x,player.y,22,210,0.55,200);
    world.shake=Math.max(world.shake,7);
    world.flash=Math.max(world.flash,0.14);
  }

  function pulse(){
    if(player.pulseCd>0) return;
    player.pulseCd = 3.6;

    const R = 170;
    let hitCount=0;
    for(const e of world.enemies){
      const d=Math.sqrt(dist2(player.x,player.y,e.x,e.y));
      if(d<R){
        const t=1-d/R;
        const ang=angleTo(player.x,player.y,e.x,e.y);
        const mult = player.pulseMult;
        e.vx += Math.cos(ang) * (600 * t * mult);
        e.vy += Math.sin(ang) * (600 * t * mult);
        const dmg = (10 + 16*t) * mult;
        e.hp -= dmg;
        hitCount++;
        spawnParticles(e.x,e.y,10,150,0.45,e.hue);
      }
    }

    ringShock(player.x,player.y,22,80);
    ringShock(player.x,player.y,22,200);
    spawnParticles(player.x,player.y,55,240,0.65,80);
    world.shake=Math.max(world.shake,9);
    world.flash=Math.max(world.flash,0.18);

    if(hitCount>0){
      world.combo = clamp(world.combo + Math.floor(hitCount/2), 1, 12);
      world.comboTimer = 2.2;
      world.score += (hitCount*7)*world.combo;
    }
  }

  // ===== Input =====
  const keys=new Set();
  let mouseX=W/2, mouseY=H/2, mouseDown=false;

  addEventListener("pointermove",(e)=>{ mouseX=e.clientX; mouseY=e.clientY; });
  addEventListener("pointerdown",()=>{ mouseDown=true; });
  addEventListener("pointerup",()=>{ mouseDown=false; });

  addEventListener("keydown",(e)=>{
    if (["ArrowUp","ArrowDown","ArrowLeft","ArrowRight"," "].includes(e.key)) e.preventDefault();
    keys.add(e.key.toLowerCase());

    if(e.key.toLowerCase()==="p"){
      if(running && !gameOver){ togglePause(); }
      else { openOverlay(); }
    }
    if(!running && (e.key==="Enter" || e.key===" ")){ startRun(); }
  }, { passive:false });

  addEventListener("keyup",(e)=> keys.delete(e.key.toLowerCase()));

  // ===== UI / Tabs =====
  function setTab(name){
    for(const t of ui.tabs) t.classList.toggle("active", t.dataset.tab===name);
    ui.tab_menu.style.display = (name==="menu") ? "grid" : "none";
    ui.tab_upgrades.style.display = (name==="upgrades") ? "grid" : "none";
    ui.tab_hangar.style.display = (name==="hangar") ? "grid" : "none";
    ui.tab_crates.style.display = (name==="crates") ? "grid" : "none";
    if(name==="upgrades") renderUpgrades();
    if(name==="hangar") renderShips();
  }
  ui.tabs.forEach(p => p.addEventListener("click", ()=>setTab(p.dataset.tab)));

  function openOverlay(){
    ui.overlay.style.display="flex";
    ui.resumeBtn.style.display = (running && paused && !gameOver) ? "inline-block" : "none";
    syncUI();
  }
  function closeOverlay(){
    ui.overlay.style.display="none";
  }

  ui.closeBtn.addEventListener("click", closeOverlay);
  ui.playBtn.addEventListener("click", startRun);
  ui.resumeBtn.addEventListener("click", ()=>{ if(running && paused) togglePause(); });

  ui.resetBtn.addEventListener("click", ()=>{
    save = defaultSave();
    saveNow();
    toast("Save reset.");
    setTab("menu");
  });

  // ===== Upgrades UI =====
  function upgradeCost(def){
    const lvl = upgradeLevel(def.id);
    return Math.floor(def.baseCost * Math.pow(def.costMult, lvl));
  }
  function canBuy(cost){ return save.credits >= cost; }

  function renderUpgrades(){
    ui.upgradeList.innerHTML = "";
    for(const def of UpgradeDefs){
      const lvl = upgradeLevel(def.id);
      const cost = upgradeCost(def);
      const maxed = lvl >= def.maxLevel;

      const el = document.createElement("div");
      el.className = "item";
      el.innerHTML = `
        <div class="left">
          <div class="title">${def.name} <span class="muted">Lv ${lvl}/${def.maxLevel}</span></div>
          <div class="desc">${def.desc}</div>
        </div>
        <div class="right">
          <div class="chip">${maxed ? "MAXED" : `Cost: ${cost}`}</div>
          <button class="btn ${maxed ? "secondary" : ""}" ${maxed ? "disabled" : ""}>Buy</button>
        </div>
      `;
      const btn = el.querySelector("button");
      btn.addEventListener("click", ()=>{
        if(maxed) return;
        if(!canBuy(cost)) { toast("Not enough credits."); return; }
        save.credits -= cost;
        save.upgrades[def.id] = lvl + 1;
        saveNow();
        toast(`Upgraded ${def.name} to Lv ${lvl+1}`);
        renderUpgrades();
      });
      ui.upgradeList.appendChild(el);
    }
    syncUI();
  }

  // ===== Hangar UI =====
  function rarityColor(r){
    if(r==="Legendary") return "✨ Legendary";
    if(r==="Epic") return "💠 Epic";
    if(r==="Rare") return "🔷 Rare";
    return "⬜ Common";
  }

  function renderShips(){
    ui.shipList.innerHTML = "";
    for(const s of Ships){
      const owned = save.ownedShips.includes(s.id);
      const active = save.activeShip === s.id;

      const stats = s.stats;
      const statLine =
        `HP x${stats.hp.toFixed(2)} · Regen x${stats.regen.toFixed(2)} · Dmg x${stats.dmg.toFixed(2)} · Speed x${stats.speed.toFixed(2)} · DashCost x${stats.dashCost.toFixed(2)} · Pulse x${stats.pulse.toFixed(2)}`;

      const el = document.createElement("div");
      el.className = "item";
      el.innerHTML = `
        <div class="left">
          <div class="title">${s.name} <span class="muted">(${rarityColor(s.rarity)})</span></div>
          <div class="desc">${owned ? s.desc : "Locked — unlock from Crates."}</div>
          <div class="desc muted">${statLine}</div>
        </div>
        <div class="right">
          <div class="chip">${owned ? (active ? "Active" : "Owned") : "Locked"}</div>
          <button class="btn ${owned ? "" : "secondary"}" ${owned ? "" : "disabled"}>${active ? "Selected" : "Select"}</button>
        </div>
      `;
      const btn = el.querySelector("button");
      btn.addEventListener("click", ()=>{
        if(!owned) return;
        save.activeShip = s.id;
        saveNow();
        toast(`Selected ${s.name}`);
        renderShips();
      });
      ui.shipList.appendChild(el);
    }
    syncUI();
  }

  // ===== Crates =====
  const CRATE_COST = 600;
  ui.crateCostText.textContent = CRATE_COST;

  function rollShipCrate(){
    if(save.credits < CRATE_COST){ toast("Not enough credits."); return; }
    save.credits -= CRATE_COST;

    // Base odds
    const pity = clamp(save.pity.legendary || 0, 0, 25);
    const legendaryChance = 0.008 + pity * 0.002; // 0.8% + 0.2% per miss (caps at 5.8%)
    const epicChance = 0.03;
    const rareChance = 0.12;

    const r = rng();
    let poolRarity = "Common";
    if(r < legendaryChance) poolRarity = "Legendary";
    else if(r < legendaryChance + epicChance) poolRarity = "Epic";
    else if(r < legendaryChance + epicChance + rareChance) poolRarity = "Rare";

    // Update pity: if legendary hit -> reset; else increase
    if(poolRarity === "Legendary") save.pity.legendary = 0;
    else save.pity.legendary = clamp(pity + 1, 0, 25);

    const pool = Ships.filter(s=>s.rarity===poolRarity && s.id!=="starter");
    // If pool empty for some reason, fall back
    const pickFrom = pool.length ? pool : Ships.filter(s=>s.rarity!=="Legendary" && s.id!=="starter");

    const ship = pickFrom[Math.floor(rand(0, pickFrom.length))];

    let msg = `You rolled: ${ship.name} (${ship.rarity}). `;
    if(save.ownedShips.includes(ship.id)){
      // duplicate refund
      const refund = Math.floor(CRATE_COST * (ship.rarity==="Legendary" ? 0.75 : ship.rarity==="Epic" ? 0.45 : ship.rarity==="Rare" ? 0.25 : 0.15));
      save.credits += refund;
      msg += `Duplicate owned → refund bonus: +${refund} credits.`;
    } else {
      save.ownedShips.push(ship.id);
      msg += `New ship unlocked! Check Hangar to equip it.`;
    }

    saveNow();
    ui.crateResult.style.display = "block";
    ui.crateResultText.textContent = msg + ` (Legendary pity: ${save.pity.legendary}/25)`;
    toast("Crate opened!");
  }

  ui.openCrateBtn.addEventListener("click", rollShipCrate);

  // ===== Run lifecycle =====
  function resetRunState(){
    world.t=0; world.dt=0;
    world.shake=0; world.flash=0;
    world.score=0;
    world.combo=1; world.comboTimer=0;
    world.threat=0;
    world.difficulty=1;
    world.spawnTimer=0.8;
    world.powerTimer=2.0;
    world.particles.length=0;
    world.bullets.length=0;
    world.enemies.length=0;
    world.powerups.length=0;

    const base = calcPlayerBase();
    player.x=W/2; player.y=H/2;
    player.vx=0; player.vy=0;
    player.maxHp = base.maxHp;
    player.hp = player.maxHp;
    player.energy = 100;
    player.invuln=0;
    player.dashCd=0;
    player.pulseCd=0;
    player.overdrive=0;

    player.regen = base.regen;
    player.dmgMult = base.dmgMult;
    player.pulseMult = base.pulseMult;
    player.speedMult = base.speedMult;
    player.dashEff = base.dashEff;

    initStars();

    gameOver=false;
    paused=false;
  }

  function startRun(){
    resetRunState();
    running=true;
    paused=false;
    closeOverlay();
    last = performance.now();
    requestAnimationFrame(loop);
  }

  function endRunAndAwardCredits(){
    // credits based on score + time + bonus
    const time = world.t;
    const score = world.score;
    const base = Math.floor(score/20 + time);
    const bonus = Math.floor(Math.sqrt(score) * 0.6);
    const earned = Math.max(0, base + bonus);

    save.credits += earned;
    saveNow();
    toast(`Run rewards: +${earned} credits`);
  }

function togglePause() {
  // If game over, don't toggle back into gameplay
  if (gameOver) {
    paused = true;
    openOverlay();
    ui.title.textContent = "Game Over";
    ui.subtitle.textContent = `Final score: ${Math.floor(world.score)} • Survived: ${Math.floor(world.t)}s`;
    ui.resumeBtn.style.display = "none";
    setTab("menu");
    return;
  }

  paused = !paused;
  if (paused) {
    openOverlay();
    ui.title.textContent = "Paused";
    ui.subtitle.textContent = "Take a breather. You can upgrade, switch ships, or open crates.";
    ui.resumeBtn.style.display = "inline-block";
    setTab("menu");
  } else {
    closeOverlay();
  }
}

  // ===== Update / Render =====
  function updateUI(){
    ui.scoreChip.textContent = "Score: " + Math.floor(world.score);
    ui.comboChip.textContent = "Combo: x" + world.combo;
    ui.hpChip.textContent = "HP: " + Math.floor(player.hp) + "/" + Math.floor(player.maxHp);
    ui.energyChip.textContent = "Energy: " + Math.floor(player.energy);
    ui.dangerChip.textContent = "Threat: " + Math.floor(world.threat*100) + "%";

    ui.creditsChip.textContent = "Credits: " + Math.floor(save.credits);
    ui.creditsInline.textContent = Math.floor(save.credits);

    const ship = getShip();
    ui.shipChip.textContent = "Ship: " + ship.name;

    ui.activeInfo.textContent =
      `${ship.name} (${ship.rarity}) • Upgrades: HP Lv ${upgradeLevel("maxHp")}, Regen Lv ${upgradeLevel("regen")}, Dmg Lv ${upgradeLevel("damage")}, Pulse Lv ${upgradeLevel("pulse")}, Dash Lv ${upgradeLevel("dashEff")}`;
  }

  function syncUI(){ updateUI(); }

  function update(dt){
    world.t += dt;
    world.dt = dt;

    // difficulty: gently ramps
    world.difficulty = 1 + world.t * 0.045 + Math.sqrt(world.score)*0.0027;
    world.threat = clamp(world.enemies.length / (11 + world.difficulty*2.4), 0, 1);

    // combo
    world.comboTimer -= dt;
    if(world.comboTimer <= 0) world.combo = 1;

    // regen
    const regen = (player.overdrive>0 ? player.regen+6 : player.regen);
    player.energy = clamp(player.energy + regen*dt, 0, 100);
    if(!mouseDown) player.energy = clamp(player.energy + 9*dt, 0, 100);

    player.invuln = Math.max(0, player.invuln - dt);
    player.dashCd = Math.max(0, player.dashCd - dt);
    player.pulseCd = Math.max(0, player.pulseCd - dt);
    player.overdrive = Math.max(0, player.overdrive - dt);

    world.shake = Math.max(0, world.shake - 18*dt);
    world.flash = Math.max(0, world.flash - 2.6*dt);

    // spawn enemies
    world.spawnTimer -= dt;
    const spawnRate = 1.15 / (1 + world.difficulty*0.18);
    if(world.spawnTimer <= 0){
      world.spawnTimer = rand(spawnRate*0.75, spawnRate*1.15);
      const amount = world.threat > 0.88 ? 2 : 1;
      for(let i=0;i<amount;i++) spawnEnemy();
    }

    // powerups
    world.powerTimer -= dt;
    if(world.powerTimer <= 0){
      world.powerTimer = rand(5.0, 8.0);
      spawnPowerup();
    }

    // movement
    const ax = (keys.has("d")?1:0) - (keys.has("a")?1:0);
    const ay = (keys.has("s")?1:0) - (keys.has("w")?1:0);
    const accel = 820 * player.speedMult;
    const friction = (player.overdrive>0 ? 0.985 : 0.975);

    player.vx += ax*accel*dt;
    player.vy += ay*accel*dt;

    player.vx *= Math.pow(friction, dt*60);
    player.vy *= Math.pow(friction, dt*60);

    const maxV = (player.overdrive>0 ? 610 : 510) * player.speedMult;
    const sp = Math.hypot(player.vx, player.vy);
    if(sp > maxV){ player.vx *= maxV/sp; player.vy *= maxV/sp; }

    player.x += player.vx*dt;
    player.y += player.vy*dt;

    // bounds
    const margin=18;
    if(player.x<margin){ player.x=margin; player.vx*=-0.6; }
    if(player.x>W-margin){ player.x=W-margin; player.vx*=-0.6; }
    if(player.y<margin){ player.y=margin; player.vy*=-0.6; }
    if(player.y>H-margin){ player.y=H-margin; player.vy*=-0.6; }

    // actions
    if(mouseDown) shoot();
    if(keys.has("shift")) dash();
    if(keys.has(" ")) pulse();

    // bullets
    for(let i=world.bullets.length-1;i>=0;i--){
      const b=world.bullets[i];
      b.life -= dt;
      b.x += b.vx*dt;
      b.y += b.vy*dt;
      if(b.life<=0 || b.x<-80||b.x>W+80||b.y<-80||b.y>H+80) world.bullets.splice(i,1);
    }

    // enemies
    for(let i=world.enemies.length-1;i>=0;i--){
      const e=world.enemies[i];
      e.t += dt;

      const px=player.x, py=player.y;
      const d=Math.sqrt(dist2(e.x,e.y,px,py));
      const ang=angleTo(e.x,e.y,px,py);

      const lead=0.17 + world.difficulty*0.008;
      const tx = px + player.vx*lead;
      const ty = py + player.vy*lead;
      const angLead=angleTo(e.x,e.y,tx,ty);

      if(e.type==="chaser"){
        const chase=185+world.difficulty*26;
        e.vx += Math.cos(angLead)*chase*dt;
        e.vy += Math.sin(angLead)*chase*dt;
      } else if(e.type==="splitter"){
        const chase=165+world.difficulty*24;
        e.vx += Math.cos(angLead)*chase*dt;
        e.vy += Math.sin(angLead)*chase*dt;
      } else if(e.type==="sniper"){
        const desired=270;
        const push=(d<desired?-1:1);
        const steer=220+world.difficulty*22;
        e.vx += Math.cos(ang)*steer*dt*push;
        e.vy += Math.sin(ang)*steer*dt*push;

        e.shoot -= dt;
        if(e.shoot<=0){
          e.shoot = rand(0.95,1.45)/(1+world.difficulty*0.02);
          const sAng=angLead+rand(-0.06,0.06);
          const speed=500+world.difficulty*28;
          world.bullets.push({
            enemy:true,
            x:e.x+Math.cos(sAng)*18,
            y:e.y+Math.sin(sAng)*18,
            vx:Math.cos(sAng)*speed,
            vy:Math.sin(sAng)*speed,
            r:3.0,
            life:1.3,
            hue:320
          });
          spawnParticles(e.x,e.y,10,130,0.55,320);
        }
      }

      // damping
      e.vx *= Math.pow(0.985, dt*60);
      e.vy *= Math.pow(0.985, dt*60);
      const eMax=210+world.difficulty*10;
      const esp=Math.hypot(e.vx,e.vy);
      if(esp>eMax){ e.vx*=eMax/esp; e.vy*=eMax/esp; }

      e.x += e.vx*dt;
      e.y += e.vy*dt;

      // enemy-player collision
      const rr = e.r + player.r;
      if(dist2(e.x,e.y,player.x,player.y) < rr*rr){
        if(player.invuln<=0){
          const dmg = (e.type==="sniper")?14 : (e.type==="splitter"?11:9);
          player.hp -= dmg;
          player.invuln = 0.45;
          world.combo=1; world.comboTimer=0;
          world.shake=Math.max(world.shake,9);
          world.flash=Math.max(world.flash,0.14);
          spawnParticles(player.x,player.y,34,240,0.55,10);
        }
        const push=400;
        e.vx += Math.cos(ang+Math.PI)*push*dt;
        e.vy += Math.sin(ang+Math.PI)*push*dt;
      }

      // death
      if(e.hp<=0){
        world.comboTimer=2.2;
        world.combo=clamp(world.combo+1,1,12);
        world.score += e.value*world.combo;

        ringShock(e.x,e.y,16,e.hue);
        spawnParticles(e.x,e.y,34,250,0.75,e.hue);
        world.shake=Math.max(world.shake,6);

        if(e.type==="splitter") splitEnemy(e);
        world.enemies.splice(i,1);
      }
    }

    // bullet collisions
    for(let i=world.bullets.length-1;i>=0;i--){
      const b=world.bullets[i];

      if(b.enemy){
        const rr=b.r+player.r;
        if(dist2(b.x,b.y,player.x,player.y)<rr*rr){
          if(player.invuln<=0){
            player.hp -= 10;
            player.invuln=0.35;
            world.combo=1; world.comboTimer=0;
            world.shake=Math.max(world.shake,7);
            world.flash=Math.max(world.flash,0.10);
            spawnParticles(player.x,player.y,24,220,0.55,330);
          }
          world.bullets.splice(i,1);
        }
        continue;
      }

      for(let j=world.enemies.length-1;j>=0;j--){
        const e=world.enemies[j];
        const rr=b.r+e.r;
        if(dist2(b.x,b.y,e.x,e.y)<rr*rr){
          const baseDmg = (player.overdrive>0 ? 16 : 12);
          const dmg = baseDmg * player.dmgMult;
          e.hp -= dmg;

          world.comboTimer=2.2;
          world.score += 2*world.combo;

          spawnParticles(b.x,b.y,10,140,0.35,e.hue);
          world.bullets.splice(i,1);
          break;
        }
      }
    }

    // powerups
    for(let i=world.powerups.length-1;i>=0;i--){
      const p=world.powerups[i];
      p.t += dt;
      p.life -= dt;
      if(p.life<=0){ world.powerups.splice(i,1); continue; }

      const rr=p.r+player.r;
      if(dist2(p.x,p.y,player.x,player.y)<rr*rr){
        if(p.kind==="heal"){
          player.hp = clamp(player.hp + 38, 0, player.maxHp);
          spawnParticles(p.x,p.y,34,210,0.75,120);
          ringShock(p.x,p.y,14,120);
        } else if(p.kind==="energy"){
          player.energy = clamp(player.energy + 60, 0, 100);
          spawnParticles(p.x,p.y,34,210,0.75,60);
          ringShock(p.x,p.y,14,60);
        } else if(p.kind==="overdrive"){
          player.overdrive = 6.5;
          spawnParticles(p.x,p.y,50,240,0.85,55);
          ringShock(p.x,p.y,14,55);
          world.flash=Math.max(world.flash,0.14);
        }
        world.powerups.splice(i,1);
      }
    }

    // particles
    for(let i=world.particles.length-1;i>=0;i--){
      const p=world.particles[i];
      p.life -= dt;
      if(p.life<=0){ world.particles.splice(i,1); continue; }
      if(!p.ring){
        p.vx *= Math.pow(0.98, dt*60);
        p.vy *= Math.pow(0.98, dt*60);
        p.x += p.vx*dt;
        p.y += p.vy*dt;
      } else {
        p.r += 420*dt;
      }
    }

    // game over
// game over (fixed)
if (player.hp <= 0 && !gameOver) {
  gameOver = true;
  paused = true;

  // clamp so it doesn't go negative
  player.hp = 0;

  spawnParticles(player.x, player.y, 120, 320, 1.25, 10);
  ringShock(player.x, player.y, 20, 10);
  world.flash = 0.30;
  world.shake = 14;

  endRunAndAwardCredits();

  // DO NOT togglePause here (it would unpause).
  // Just open the menu overlay in a game-over state:
  openOverlay();
  ui.title.textContent = "Game Over";
  ui.subtitle.textContent = `Final score: ${Math.floor(world.score)} • Survived: ${Math.floor(world.t)}s`;
  ui.resumeBtn.style.display = "none";
  setTab("menu");
}


    updateUI();
  }

  function render(){
    const s=world.shake;
    const ox=(rng()-0.5)*s;
    const oy=(rng()-0.5)*s;

    ctx.save();
    ctx.translate(ox,oy);

    ctx.fillStyle="#05060a";
    ctx.fillRect(-ox,-oy,W,H);

    // stars
    for(const st of world.stars){
      st.tw += world.dt*(0.8+st.z);
      const tw = 0.5+0.5*Math.sin(st.tw);
      const px = (st.x + player.vx * -0.02 * st.z) % W;
      const py = (st.y + player.vy * -0.02 * st.z) % H;
      ctx.globalAlpha = 0.20 + 0.45*tw*st.z;
      ctx.fillStyle="white";
      ctx.fillRect(px,py,1.2*st.z,1.2*st.z);
    }
    ctx.globalAlpha=1;

    // powerups
    for(const p of world.powerups){
      const pulse = 0.5+0.5*Math.sin(p.t*5.5);
      let hue=120, icon="💚";
      if(p.kind==="energy"){ hue=60; icon="⚡"; }
      if(p.kind==="overdrive"){ hue=55; icon="✴"; }

      ctx.save();
      ctx.translate(p.x,p.y);
      const gg=ctx.createRadialGradient(0,0,2,0,0,34);
      gg.addColorStop(0,`hsla(${hue},100%,65%,${0.35+0.25*pulse})`);
      gg.addColorStop(1,"rgba(0,0,0,0)");
      ctx.fillStyle=gg;
      ctx.beginPath(); ctx.arc(0,0,34,0,Math.PI*2); ctx.fill();

      ctx.fillStyle=`hsla(${hue},100%,70%,0.85)`;
      ctx.beginPath(); ctx.arc(0,0,9+2*pulse,0,Math.PI*2); ctx.fill();

      ctx.font="18px ui-sans-serif, system-ui";
      ctx.textAlign="center"; ctx.textBaseline="middle";
      ctx.fillStyle="rgba(255,255,255,0.92)";
      ctx.fillText(icon,0,-18);
      ctx.restore();
    }

    // bullets
    for(const b of world.bullets){
      ctx.save();
      ctx.translate(b.x,b.y);
      const hue=b.hue ?? 190;
      const alpha=clamp(b.life/1.0,0,1);

      ctx.globalAlpha=0.25*alpha;
      ctx.strokeStyle=`hsla(${hue},100%,65%,0.7)`;
      ctx.lineWidth=3;
      ctx.beginPath();
      ctx.moveTo(0,0);
      ctx.lineTo(-b.vx*0.02,-b.vy*0.02);
      ctx.stroke();

      ctx.globalAlpha=0.9*alpha;
      ctx.fillStyle=`hsla(${hue},100%,70%,0.95)`;
      ctx.beginPath(); ctx.arc(0,0,b.r,0,Math.PI*2); ctx.fill();
      ctx.restore();
    }

    // enemies
    for(const e of world.enemies){
      const hpT=e.hp/e.maxHp;
      const hue=e.hue;
      ctx.save();
      ctx.translate(e.x,e.y);

      const gg=ctx.createRadialGradient(0,0,2,0,0,40);
      gg.addColorStop(0,`hsla(${hue},100%,60%,0.32)`);
      gg.addColorStop(1,"rgba(0,0,0,0)");
      ctx.fillStyle=gg;
      ctx.beginPath(); ctx.arc(0,0,40,0,Math.PI*2); ctx.fill();

      ctx.globalAlpha=0.95;
      ctx.fillStyle=`hsla(${hue},100%,60%,0.95)`;
      ctx.beginPath();
      if(e.type==="sniper"){
        ctx.moveTo(0,-e.r); ctx.lineTo(e.r,0); ctx.lineTo(0,e.r); ctx.lineTo(-e.r,0); ctx.closePath();
      } else if(e.type==="splitter"){
        const r=e.r;
        for(let i=0;i<6;i++){
          const a=i*Math.PI/3 + e.t*0.6;
          const px=Math.cos(a)*r, py=Math.sin(a)*r;
          if(i===0) ctx.moveTo(px,py); else ctx.lineTo(px,py);
        }
        ctx.closePath();
      } else {
        ctx.arc(0,0,e.r,0,Math.PI*2);
      }
      ctx.fill();

      ctx.globalAlpha=0.8;
      ctx.lineWidth=3;
      ctx.strokeStyle="rgba(255,255,255,0.22)";
      ctx.beginPath(); ctx.arc(0,0,e.r+8,-Math.PI/2,1.5*Math.PI); ctx.stroke();
      ctx.strokeStyle=`hsla(${hue},100%,70%,0.9)`;
      ctx.beginPath(); ctx.arc(0,0,e.r+8,-Math.PI/2,-Math.PI/2+Math.PI*2*hpT); ctx.stroke();

      ctx.restore();
    }

    // player
    const a=angleTo(player.x,player.y,mouseX,mouseY);
    ctx.save();
    ctx.translate(player.x,player.y);
    ctx.rotate(a);

    const phue = player.overdrive>0 ? 55 : 190;
    const pg=ctx.createRadialGradient(0,0,2,0,0,55);
    pg.addColorStop(0,`hsla(${phue},100%,65%,0.32)`);
    pg.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=pg;
    ctx.beginPath(); ctx.arc(0,0,55,0,Math.PI*2); ctx.fill();

    if(player.invuln>0){
      ctx.globalAlpha=0.25+0.25*Math.sin(world.t*18);
      ctx.strokeStyle="hsla(0,0%,100%,0.9)";
      ctx.lineWidth=2;
      ctx.beginPath(); ctx.arc(0,0,player.r+10,0,Math.PI*2); ctx.stroke();
    }

    ctx.globalAlpha=0.95;
    ctx.fillStyle=`hsla(${phue},100%,70%,0.95)`;
    ctx.beginPath();
    ctx.moveTo(18,0);
    ctx.lineTo(-12,-10);
    ctx.lineTo(-7,0);
    ctx.lineTo(-12,10);
    ctx.closePath();
    ctx.fill();

    ctx.restore();

    // particles
    for(const p of world.particles){
      const t=clamp(p.life/p.maxLife,0,1);
      if(p.ring){
        ctx.save();
        ctx.globalAlpha=0.65*t;
        ctx.strokeStyle=`hsla(${p.hue},100%,70%,0.85)`;
        ctx.lineWidth=3;
        ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2); ctx.stroke();
        ctx.restore();
      } else {
        ctx.save();
        ctx.globalAlpha=0.85*t;
        ctx.fillStyle=`hsla(${p.hue},100%,70%,0.95)`;
        ctx.beginPath(); ctx.arc(p.x,p.y,p.r*(0.6+0.7*t),0,Math.PI*2); ctx.fill();
        ctx.restore();
      }
    }

    // flash
    if(world.flash>0){
      ctx.save();
      ctx.globalAlpha=world.flash;
      ctx.fillStyle="white";
      ctx.fillRect(0,0,W,H);
      ctx.restore();
    }

    ctx.restore();
  }

  // ===== Loop =====
  let last = performance.now();
  function loop(now){
    if(!running) return;
    const dt = Math.min(0.033, (now-last)/1000);
    last = now;

    if(!paused) update(dt);
    render();

    requestAnimationFrame(loop);
  }

  // ===== Start in Menu =====
  function initMenu(){
    syncUI();
    ui.title.textContent = "Neon Orbit: Hangar & Upgrades";
    ui.subtitle.textContent = "Earn credits, upgrade your ship, and unlock new hulls via crates.";
    setTab("menu");
    openOverlay();
  }
  initMenu();

  // ===== Sync overlay state =====
  function syncOverlayState(){
    ui.resumeBtn.style.display = (running && paused && !gameOver) ? "inline-block" : "none";
  }

  // Keep overlay state clean when closing
  ui.overlay.addEventListener("click",(e)=>{
    // click outside panel closes only if paused (optional)
    if(e.target === ui.overlay && running && paused && !gameOver) togglePause();
  });

  // Also allow leaving to menu while paused
  function showMenuWhilePaused(){
    paused=true; openOverlay(); setTab("menu"); syncOverlayState();
  }

  // If user closes overlay during pause, keep paused
  ui.closeBtn.addEventListener("click", ()=>{
    if(running && paused && !gameOver) closeOverlay();
  });

  // Make sure UI always updates
  setInterval(syncUI, 400);

})();
</script>
</body>
</html>
