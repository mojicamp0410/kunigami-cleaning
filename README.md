[kunigami_cleaning.html](https://github.com/user-attachments/files/27039901/kunigami_cleaning.html)
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>国頭村森林公園 清掃管理</title>
<link href="https://fonts.googleapis.com/css2?family=Zen+Kaku+Gothic+New:wght@300;400;700;900&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --ink:     #0f1a14;
  --forest:  #1a3c28;
  --green:   #2d6a45;
  --sage:    #5a8a6e;
  --mist:    #e8f0eb;
  --pale:    #f4f7f5;
  --white:   #ffffff;
  --gold:    #c8952a;
  --amber:   #e8b84b;
  --red:     #c0392b;
  --red-lt:  #fdf0ee;
  --done:    #1a6b3c;
  --done-lt: #e6f4ec;
  --warn:    #8b4513;
  --border:  #d0ddd5;
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

body {
  font-family: 'Zen Kaku Gothic New', sans-serif;
  background: var(--pale);
  color: var(--ink);
  min-height: 100vh;
}

/* ── TOP BAR ── */
.topbar {
  background: var(--forest);
  padding: .9rem 1.2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 12px rgba(0,0,0,.25);
}
.topbar-logo {
  display: flex;
  align-items: center;
  gap: .6rem;
  color: var(--white);
}
.topbar-logo .icon { font-size: 1.3rem; }
.topbar-logo .title { font-size: .95rem; font-weight: 700; line-height: 1.2; }
.topbar-logo .sub { font-size: .65rem; opacity: .7; font-weight: 300; }
.topbar-right { display: flex; align-items: center; gap: .7rem; }
.clock {
  font-family: 'DM Mono', monospace;
  font-size: .82rem;
  color: rgba(255,255,255,.75);
  background: rgba(255,255,255,.1);
  padding: .3rem .7rem;
  border-radius: 4px;
}
.btn-reset-all {
  background: rgba(255,255,255,.12);
  border: 1px solid rgba(255,255,255,.25);
  color: white;
  padding: .3rem .8rem;
  border-radius: 4px;
  font-size: .72rem;
  font-family: 'Zen Kaku Gothic New';
  cursor: pointer;
  transition: background .15s;
}
.btn-reset-all:hover { background: rgba(255,255,255,.22); }

/* ── OVERVIEW STRIP ── */
.overview {
  background: var(--forest);
  padding: .5rem 1.2rem 1rem;
  display: flex;
  gap: .6rem;
  overflow-x: auto;
  scrollbar-width: none;
}
.overview::-webkit-scrollbar { display: none; }
.ov-chip {
  flex-shrink: 0;
  background: rgba(255,255,255,.1);
  border: 1px solid rgba(255,255,255,.15);
  border-radius: 6px;
  padding: .35rem .8rem;
  cursor: pointer;
  transition: all .15s;
  text-align: center;
  min-width: 72px;
}
.ov-chip:hover { background: rgba(255,255,255,.2); }
.ov-chip .ov-name { font-size: .68rem; color: rgba(255,255,255,.8); font-weight: 400; }
.ov-chip .ov-status { font-size: .75rem; font-weight: 700; margin-top: .1rem; }
.ov-chip.ready   { border-color: var(--amber); background: rgba(200,149,42,.15); }
.ov-chip.done    { border-color: #4caf50; background: rgba(76,175,80,.15); }
.ov-chip.dirty   { border-color: rgba(255,255,255,.15); }

/* ── CATEGORY FILTER ── */
.cat-bar {
  padding: .8rem 1rem .4rem;
  display: flex;
  gap: .5rem;
  overflow-x: auto;
  scrollbar-width: none;
}
.cat-bar::-webkit-scrollbar { display: none; }
.cat-btn {
  flex-shrink: 0;
  background: var(--white);
  border: 1.5px solid var(--border);
  border-radius: 2rem;
  padding: .35rem .9rem;
  font-size: .75rem;
  font-family: 'Zen Kaku Gothic New';
  font-weight: 700;
  color: var(--sage);
  cursor: pointer;
  transition: all .15s;
}
.cat-btn.active {
  background: var(--forest);
  border-color: var(--forest);
  color: var(--white);
}

/* ── GRID ── */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 1rem;
  padding: .8rem 1rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

/* ── FACILITY CARD ── */
.card {
  background: var(--white);
  border-radius: 14px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(15,26,20,.08);
  border: 2px solid var(--border);
  transition: border-color .2s, box-shadow .2s;
}
.card.status-done {
  border-color: #4caf50;
  box-shadow: 0 2px 16px rgba(76,175,80,.15);
}
.card.status-ready {
  border-color: var(--amber);
  box-shadow: 0 2px 16px rgba(232,184,75,.2);
}

.card-head {
  padding: .9rem 1rem .7rem;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: .5rem;
  border-bottom: 1px solid var(--mist);
}
.card-head-left { display: flex; align-items: center; gap: .6rem; flex: 1; min-width: 0; }
.facility-icon {
  width: 40px; height: 40px;
  border-radius: 10px;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.3rem;
  flex-shrink: 0;
}
.card-info { min-width: 0; }
.card-type { font-size: .62rem; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; color: var(--sage); margin-bottom: .1rem; }
.card-name { font-size: 1rem; font-weight: 900; color: var(--ink); line-height: 1.2; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.card-name-jp { font-size: .72rem; color: var(--sage); font-weight: 400; }

.status-badge {
  flex-shrink: 0;
  padding: .28rem .75rem;
  border-radius: 2rem;
  font-size: .7rem;
  font-weight: 700;
  letter-spacing: .03em;
  white-space: nowrap;
}
.badge-dirty   { background: #f0f0f0; color: #888; }
.badge-wip     { background: #fff3cd; color: #856404; }
.badge-ready   { background: #fff3cd; color: var(--warn); border: 1px solid var(--amber); }
.badge-done    { background: var(--done-lt); color: var(--done); }

/* ── PROGRESS BAR ── */
.progress-wrap { padding: .5rem 1rem .3rem; }
.progress-bar-bg {
  background: var(--mist);
  border-radius: 2px;
  height: 4px;
  overflow: hidden;
  margin-bottom: .3rem;
}
.progress-bar-fill {
  height: 100%;
  border-radius: 2px;
  background: var(--green);
  transition: width .4s cubic-bezier(.4,0,.2,1);
}
.progress-bar-fill.complete { background: #4caf50; }
.progress-text {
  font-size: .68rem;
  color: var(--sage);
  font-family: 'DM Mono', monospace;
  display: flex;
  justify-content: space-between;
}

/* ── STEPS ── */
.steps { padding: .4rem .8rem .8rem; }
.step {
  display: flex;
  align-items: center;
  gap: .65rem;
  padding: .55rem .5rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background .12s;
  user-select: none;
  -webkit-user-select: none;
  position: relative;
}
.step:hover { background: var(--pale); }
.step:active { background: var(--mist); }

.step-check {
  width: 22px; height: 22px;
  border-radius: 50%;
  border: 2px solid var(--border);
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all .2s cubic-bezier(.4,0,.2,1);
  background: var(--white);
}
.step.checked .step-check {
  background: var(--green);
  border-color: var(--green);
}
.step.checked .step-check::after {
  content: '';
  width: 5px; height: 9px;
  border: 2px solid white;
  border-top: none; border-left: none;
  transform: rotate(42deg) translate(-1px, -1px);
}

.step-label {
  font-size: .84rem;
  color: var(--ink);
  line-height: 1.35;
  flex: 1;
}
.step.checked .step-label {
  color: var(--sage);
  text-decoration: line-through;
  text-decoration-color: var(--sage);
}

.step-icon { font-size: .9rem; flex-shrink: 0; opacity: .6; }

/* option badge */
.step-opt {
  font-size: .6rem;
  background: #e3f2fd;
  color: #1565c0;
  padding: .1rem .4rem;
  border-radius: 3px;
  font-weight: 700;
  white-space: nowrap;
}

/* ── ACTION BUTTONS ── */
.card-footer {
  padding: .6rem 1rem .9rem;
  border-top: 1px solid var(--mist);
  display: flex;
  gap: .5rem;
}
.btn-action {
  flex: 1;
  padding: .55rem;
  border-radius: 8px;
  font-family: 'Zen Kaku Gothic New';
  font-size: .78rem;
  font-weight: 700;
  cursor: pointer;
  border: none;
  transition: all .15s;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: .3rem;
}
.btn-complete {
  background: var(--green);
  color: white;
}
.btn-complete:hover { background: var(--forest); }
.btn-complete:disabled { background: #4caf50; opacity: .7; cursor: default; }
.btn-reset {
  background: var(--mist);
  color: var(--sage);
  flex: 0 0 auto;
  padding: .55rem .9rem;
}
.btn-reset:hover { background: var(--border); }

/* ── READY STAMP ── */
.ready-stamp {
  display: none;
  align-items: center;
  justify-content: center;
  gap: .4rem;
  background: var(--done-lt);
  color: var(--done);
  font-weight: 900;
  font-size: .9rem;
  padding: .7rem;
  border-radius: 8px;
  width: 100%;
  letter-spacing: .05em;
}
.ready-stamp .stamp-icon { font-size: 1.2rem; }
.card.status-done .ready-stamp { display: flex; }
.card.status-done .btn-action.btn-complete { display: none; }

/* ── TIMESTAMP ── */
.timestamp {
  font-family: 'DM Mono', monospace;
  font-size: .62rem;
  color: var(--sage);
  text-align: right;
  padding: 0 1rem .6rem;
  display: none;
}
.card.status-done .timestamp { display: block; }

/* ── MODAL (detail view) ── */
.modal-overlay {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(10,20,14,.6);
  z-index: 200;
  align-items: flex-end;
  justify-content: center;
  backdrop-filter: blur(3px);
}
.modal-overlay.open { display: flex; }
.modal-sheet {
  background: var(--white);
  border-radius: 20px 20px 0 0;
  width: 100%;
  max-width: 540px;
  max-height: 80vh;
  overflow-y: auto;
  padding: 1.2rem 1.4rem 2rem;
  animation: slideUp .25s ease;
}
@keyframes slideUp {
  from { transform: translateY(100%); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}
.sheet-handle {
  width: 36px; height: 4px;
  background: var(--border);
  border-radius: 2px;
  margin: 0 auto .9rem;
}
.sheet-title { font-size: 1.1rem; font-weight: 900; color: var(--ink); margin-bottom: 1rem; }
.sheet-close {
  position: absolute;
  right: 1.2rem; top: 1.2rem;
  background: var(--mist);
  border: none;
  width: 30px; height: 30px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 1rem;
  display: flex; align-items: center; justify-content: center;
  color: var(--sage);
}

/* ── TOAST ── */
.toast {
  position: fixed;
  bottom: 5rem;
  left: 50%;
  transform: translateX(-50%) translateY(60px);
  opacity: 0;
  background: var(--ink);
  color: white;
  padding: .6rem 1.3rem;
  border-radius: 2rem;
  font-size: .82rem;
  font-weight: 700;
  z-index: 999;
  transition: all .25s cubic-bezier(.34,1.56,.64,1);
  white-space: nowrap;
}
.toast.show {
  transform: translateX(-50%) translateY(0);
  opacity: 1;
}

/* ── EMPTY STATE ── */
.empty { text-align: center; padding: 3rem 1rem; color: var(--sage); }
.empty .e-icon { font-size: 3rem; opacity: .4; margin-bottom: .8rem; }

@media (max-width: 480px) {
  .grid { grid-template-columns: 1fr; gap: .75rem; padding: .6rem .75rem 2rem; }
  .topbar { padding: .7rem .9rem; }
  .overview { padding: .4rem .9rem .8rem; }
}
</style>
</head>
<body>

<!-- TOP BAR -->
<header class="topbar">
  <div class="topbar-logo">
    <span class="icon">🏕️</span>
    <div>
      <div class="title">国頭村森林公園</div>
      <div class="sub">清掃・引き継ぎ管理システム</div>
    </div>
  </div>
  <div class="topbar-right">
    <div class="clock" id="clock">--:--</div>
    <button class="btn-reset-all" onclick="resetAll()">全リセット</button>
  </div>
</header>

<!-- OVERVIEW STRIP -->
<div class="overview" id="overviewStrip"></div>

<!-- CATEGORY FILTER -->
<div class="cat-bar" id="catBar">
  <button class="cat-btn active" onclick="filterCat('all',this)">すべて</button>
  <button class="cat-btn" onclick="filterCat('bungalow',this)">🏠 バンガロー</button>
  <button class="cat-btn" onclick="filterCat('cottage',this)">⭐ 星のコテージ</button>
  <button class="cat-btn" onclick="filterCat('treehouse',this)">🌳 樹上ハウス</button>
  <button class="cat-btn" onclick="filterCat('cabin',this)">🦅 森のキャビン</button>
</div>

<!-- GRID -->
<main class="grid" id="grid"></main>

<div class="toast" id="toast"></div>

<script>
// ── FACILITY DEFINITIONS ──────────────────────────────────────
const FACILITIES = [
  {
    id: "matsu", cat: "bungalow",
    type: "バンガロー", nameEn: "MATSU", nameJp: "松棟",
    icon: "🏠", iconBg: "#e8f0eb",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🛏️", label:"寝具の撤収（ひっぺがし）" },
      { id:"s3", icon:"🚿", label:"シャワー・トイレの清掃" },
      { id:"s4", icon:"🧹", label:"フロアの清掃" },
      { id:"s5", icon:"🛏️", label:"寝具のセッティング" },
      { id:"s6", icon:"✨", label:"当日の仕上げ確認" },
      { id:"s7", icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "itajii", cat: "bungalow",
    type: "バンガロー", nameEn: "ITAJII", nameJp: "イタジイ棟",
    icon: "🏠", iconBg: "#e8f0eb",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🛏️", label:"寝具の撤収（ひっぺがし）" },
      { id:"s3", icon:"🚿", label:"シャワー・トイレの清掃" },
      { id:"s4", icon:"🧹", label:"フロアの清掃" },
      { id:"s5", icon:"🛏️", label:"寝具のセッティング" },
      { id:"s6", icon:"✨", label:"当日の仕上げ確認" },
      { id:"s7", icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "muribushi", cat: "cottage",
    type: "星のコテージ", nameEn: "MURIBUSHI", nameJp: "むりぶし",
    icon: "⭐", iconBg: "#fffde7",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🛏️", label:"寝具の撤収（ひっぺがし）" },
      { id:"s3", icon:"🚿", label:"シャワー室の清掃" },
      { id:"s4", icon:"🚽", label:"トイレの清掃" },
      { id:"s5", icon:"🧹", label:"フロアの清掃" },
      { id:"s6", icon:"🍳", label:"キッチンの清掃" },
      { id:"s7", icon:"❄️", label:"冷蔵庫等備品の清掃" },
      { id:"s8", icon:"🚪", label:"玄関の清掃" },
      { id:"s9", icon:"🌿", label:"外デッキの清掃" },
      { id:"s10",icon:"🛏️", label:"寝具のセッティング" },
      { id:"s11",icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "ninufa", cat: "cottage",
    type: "星のコテージ", nameEn: "NINUFABUSHI", nameJp: "にぬふぁぶし",
    icon: "⭐", iconBg: "#fffde7",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🛏️", label:"寝具の撤収（ひっぺがし）" },
      { id:"s3", icon:"🚿", label:"シャワー室の清掃" },
      { id:"s4", icon:"🚽", label:"トイレの清掃" },
      { id:"s5", icon:"🧹", label:"フロアの清掃" },
      { id:"s6", icon:"🍳", label:"キッチンの清掃" },
      { id:"s7", icon:"❄️", label:"冷蔵庫等備品の清掃" },
      { id:"s8", icon:"🚪", label:"玄関の清掃" },
      { id:"s9", icon:"🌿", label:"外デッキの清掃" },
      { id:"s10",icon:"🛏️", label:"寝具のセッティング" },
      { id:"s11",icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "tree3", cat: "treehouse",
    type: "樹上ハウス", nameEn: "TREE HOUSE No.3", nameJp: "No.3",
    icon: "🌳", iconBg: "#e8f5e9",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🧹", label:"室内の清掃" },
      { id:"s3", icon:"💧", label:"クーラーの水捨て" },
      { id:"s4", icon:"🛏️", label:"寝袋の回収または準備", opt:"寝袋オプション時" },
      { id:"s5", icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "tree4", cat: "treehouse",
    type: "樹上ハウス", nameEn: "TREE HOUSE No.4", nameJp: "No.4",
    icon: "🌳", iconBg: "#e8f5e9",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🧹", label:"室内の清掃" },
      { id:"s3", icon:"💧", label:"クーラーの水捨て" },
      { id:"s4", icon:"🛏️", label:"寝袋の回収または準備", opt:"寝袋オプション時" },
      { id:"s5", icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "tree5", cat: "treehouse",
    type: "樹上ハウス", nameEn: "TREE HOUSE No.5", nameJp: "No.5",
    icon: "🌳", iconBg: "#e8f5e9",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🧹", label:"室内の清掃" },
      { id:"s3", icon:"💧", label:"クーラーの水捨て" },
      { id:"s4", icon:"🛏️", label:"寝袋の回収または準備", opt:"寝袋オプション時" },
      { id:"s5", icon:"🐜", label:"アリ対策" },
    ]
  },
  {
    id: "akahige", cat: "cabin",
    type: "森のキャビン", nameEn: "AKAHIGE", nameJp: "アカヒゲ",
    icon: "🦅", iconBg: "#fce4ec",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🧹", label:"室内清掃" },
      { id:"s3", icon:"❄️", label:"冷蔵庫のクリーニング" },
      { id:"s4", icon:"🛏️", label:"寝具の撤収（オプション有時）", opt:"寝具オプション時" },
      { id:"s5", icon:"🛏️", label:"寝具のセッティング（オプション有時）", opt:"寝具オプション時" },
    ]
  },
  {
    id: "noguchi", cat: "cabin",
    type: "森のキャビン", nameEn: "NOGUCHIGERA", nameJp: "ノグチゲラ",
    icon: "🦅", iconBg: "#fce4ec",
    steps: [
      { id:"s1", icon:"🔍", label:"忘れ物チェック" },
      { id:"s2", icon:"🧹", label:"室内清掃" },
      { id:"s3", icon:"❄️", label:"冷蔵庫のクリーニング" },
      { id:"s4", icon:"🛏️", label:"寝具の撤収（オプション有時）", opt:"寝具オプション時" },
      { id:"s5", icon:"🛏️", label:"寝具のセッティング（オプション有時）", opt:"寝具オプション時" },
    ]
  },
];

// ── STATE ─────────────────────────────────────────────────────
const KEY = "kfp_cleaning_v2";
let state = loadState();

function loadState() {
  try {
    const s = JSON.parse(localStorage.getItem(KEY) || "{}");
    const out = {};
    FACILITIES.forEach(f => {
      out[f.id] = s[f.id] || {
        checked: {},
        completedAt: null
      };
    });
    return out;
  } catch(e) { return {}; }
}

function saveState() {
  localStorage.setItem(KEY, JSON.stringify(state));
}

function getFacilityStatus(fid) {
  const f = FACILITIES.find(x => x.id === fid);
  const s = state[fid];
  if (!f || !s) return "dirty";
  const total = f.steps.length;
  const done = Object.values(s.checked).filter(Boolean).length;
  if (done === 0) return "dirty";
  if (done === total) return "done";
  return "wip";
}

function getProgress(fid) {
  const f = FACILITIES.find(x => x.id === fid);
  const s = state[fid];
  if (!f || !s) return { done: 0, total: 0 };
  const total = f.steps.length;
  const done = Object.values(s.checked).filter(Boolean).length;
  return { done, total };
}

// ── CLOCK ─────────────────────────────────────────────────────
function updateClock() {
  const now = new Date();
  const h = String(now.getHours()).padStart(2,'0');
  const m = String(now.getMinutes()).padStart(2,'0');
  document.getElementById('clock').textContent = `${h}:${m}`;
}
updateClock();
setInterval(updateClock, 10000);

// ── RENDER ────────────────────────────────────────────────────
let currentCat = 'all';

function render() {
  renderOverview();
  renderGrid();
}

function renderOverview() {
  const strip = document.getElementById('overviewStrip');
  strip.innerHTML = FACILITIES.map(f => {
    const status = getFacilityStatus(f.id);
    const { done, total } = getProgress(f.id);
    const statusText = status === 'done' ? '✅ 使用可' :
                       status === 'wip'  ? `${done}/${total}` : '清掃待ち';
    return `
      <div class="ov-chip ${status}" onclick="scrollToCard('${f.id}')">
        <div class="ov-name">${f.icon} ${f.nameJp}</div>
        <div class="ov-status" style="color:${status==='done'?'#4caf50':status==='wip'?'#e8b84b':'rgba(255,255,255,.6)'}">${statusText}</div>
      </div>`;
  }).join('');
}

function renderGrid() {
  const grid = document.getElementById('grid');
  const list = currentCat === 'all' ? FACILITIES : FACILITIES.filter(f => f.cat === currentCat);

  if (!list.length) {
    grid.innerHTML = `<div class="empty"><div class="e-icon">🌿</div><div>施設が見つかりません</div></div>`;
    return;
  }

  grid.innerHTML = list.map(f => {
    const status = getFacilityStatus(f.id);
    const { done, total } = getProgress(f.id);
    const pct = total ? Math.round(done / total * 100) : 0;
    const s = state[f.id];

    const badgeClass = status === 'done' ? 'badge-done' : status === 'wip' ? 'badge-wip' : 'badge-dirty';
    const badgeText  = status === 'done' ? '✅ 使用可' : status === 'wip' ? '⚙️ 清掃中' : '— 清掃待ち';

    const stepsHtml = f.steps.map(step => {
      const checked = s.checked[step.id] || false;
      return `
        <div class="step ${checked?'checked':''}" onclick="toggleStep('${f.id}','${step.id}')">
          <div class="step-check"></div>
          <span class="step-icon">${step.icon}</span>
          <span class="step-label">${step.label}</span>
          ${step.opt ? `<span class="step-opt">${step.opt}</span>` : ''}
        </div>`;
    }).join('');

    const ts = s.completedAt ? new Date(s.completedAt).toLocaleString('ja-JP',{
      month:'numeric',day:'numeric',hour:'2-digit',minute:'2-digit'}) : '';

    return `
      <div class="card status-${status}" id="card-${f.id}">
        <div class="card-head">
          <div class="card-head-left">
            <div class="facility-icon" style="background:${f.iconBg}">${f.icon}</div>
            <div class="card-info">
              <div class="card-type">${f.type}</div>
              <div class="card-name">${f.nameEn}</div>
              <div class="card-name-jp">${f.nameJp}</div>
            </div>
          </div>
          <span class="status-badge ${badgeClass}">${badgeText}</span>
        </div>
        <div class="progress-wrap">
          <div class="progress-bar-bg">
            <div class="progress-bar-fill ${pct===100?'complete':''}" style="width:${pct}%"></div>
          </div>
          <div class="progress-text">
            <span>${done} / ${total} 工程完了</span>
            <span>${pct}%</span>
          </div>
        </div>
        <div class="steps">${stepsHtml}</div>
        <div class="card-footer">
          <button class="btn-action btn-complete"
            onclick="completeAll('${f.id}')"
            ${status==='done'?'disabled':''}>
            ${status==='done'?'✅ 完了済み':'🎯 全工程完了にする'}
          </button>
          <div class="ready-stamp"><span class="stamp-icon">✅</span> 使用可能です</div>
          <button class="btn-action btn-reset" onclick="resetCard('${f.id}')">↺</button>
        </div>
        <div class="timestamp">完了: ${ts}</div>
      </div>`;
  }).join('');
}

// ── INTERACTIONS ──────────────────────────────────────────────
function toggleStep(fid, sid) {
  if (!state[fid]) state[fid] = { checked: {}, completedAt: null };
  state[fid].checked[sid] = !state[fid].checked[sid];

  const f = FACILITIES.find(x => x.id === fid);
  const { done, total } = getProgress(fid);
  if (done === total && total > 0) {
    state[fid].completedAt = new Date().toISOString();
    showToast(`✅ ${f.nameJp} 清掃完了！使用可能です`);
  } else {
    state[fid].completedAt = null;
  }
  saveState();
  render();
}

function completeAll(fid) {
  const f = FACILITIES.find(x => x.id === fid);
  if (!state[fid]) state[fid] = { checked: {}, completedAt: null };
  f.steps.forEach(s => state[fid].checked[s.id] = true);
  state[fid].completedAt = new Date().toISOString();
  saveState();
  render();
  showToast(`✅ ${f.nameJp} 使用可能になりました！`);
}

function resetCard(fid) {
  const f = FACILITIES.find(x => x.id === fid);
  if (!confirm(`${f.nameJp} の清掃状況をリセットしますか？`)) return;
  state[fid] = { checked: {}, completedAt: null };
  saveState();
  render();
  showToast(`↺ ${f.nameJp} をリセットしました`);
}

function resetAll() {
  if (!confirm('全施設の清掃状況をリセットしますか？\n（朝のリセットに使ってください）')) return;
  FACILITIES.forEach(f => { state[f.id] = { checked: {}, completedAt: null }; });
  saveState();
  render();
  showToast('↺ 全施設をリセットしました');
}

function filterCat(cat, btn) {
  currentCat = cat;
  document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderGrid();
}

function scrollToCard(fid) {
  const el = document.getElementById('card-' + fid);
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'center' });
    el.style.outline = '3px solid var(--amber)';
    setTimeout(() => el.style.outline = '', 1500);
  }
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2800);
}

// ── INIT ──────────────────────────────────────────────────────
render();
</script>
</body>
</html>
