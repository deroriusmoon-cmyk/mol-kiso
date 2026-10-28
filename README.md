<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>molをつかもう！｜高校化学基礎</title>
  <style>
    :root {
      --ink: #17324b;
      --blue: #1764ae;
      --blue-dark: #104b84;
      --pale: #eaf4ff;
      --line: #d3e1eb;
      --green: #16704b;
      --red: #ae3434;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      color: var(--ink);
      background: #f3f7fa;
      font-family: system-ui, -apple-system, "Noto Sans JP", sans-serif;
      line-height: 1.6;
    }

    header {
      background: #123e68;
      color: white;
      padding: 18px;
    }

    header > div,
    main {
      max-width: 1000px;
      margin: auto;
    }

    header h1 {
      margin: 0;
      font-size: clamp(1.5rem, 4vw, 2.1rem);
    }

    header p { margin: 0; }

    main { padding: 18px; }

    .screen[hidden],
    [hidden] {
      display: none !important;
    }

    .panel {
      background: white;
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: clamp(16px, 3vw, 28px);
      margin-bottom: 16px;
    }

    h2 { margin: 0 0 12px; }

    button,
    select,
    input {
      font: inherit;
    }

    button,
    select {
      min-height: 44px;
      border-radius: 9px;
    }

    button {
      cursor: pointer;
      padding: 9px 15px;
      border: 1px solid var(--blue);
      background: white;
      color: var(--blue);
      font-weight: 700;
    }

    button:hover:not(:disabled),
    button:focus-visible {
      background: var(--pale);
    }

    button:disabled {
      cursor: not-allowed;
      opacity: .65;
    }

    button.primary {
      background: var(--blue);
      color: white;
    }

    button.primary:hover:not(:disabled) {
      background: var(--blue-dark);
    }

    select {
      padding: 7px 10px;
      border: 1px solid #8eabba;
      background: white;
      color: var(--ink);
    }

    input[type="range"] {
      width: min(100%, 480px);
      accent-color: var(--blue);
    }

    .menu-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
      margin-top: 18px;
    }

    .menu-card {
      min-height: 110px;
      padding: 16px;
      text-align: left;
      font-size: 1.06rem;
    }

    .menu-card strong,
    .menu-card span {
      display: block;
    }

    .menu-card span {
      margin-top: 5px;
      font-size: .91rem;
      font-weight: 400;
    }

    .back { margin-bottom: 12px; }

    .muted {
      color: #52687b;
      font-size: .94rem;
    }

    .note {
      padding: 12px 15px;
      background: #fff5dd;
      border-radius: 9px;
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 10px;
      margin: 12px 0;
    }

    .stats {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 12px;
      margin: 18px 0;
    }

    .stat {
      padding: 14px;
      background: #eff6fc;
      border-radius: 12px;
      overflow-wrap: anywhere;
    }

    .stat strong {
      display: block;
      font-size: clamp(1.1rem, 2.5vw, 1.35rem);
    }

    /* 風船は外部画像を使わないCSSイラスト */
    .balloons {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      align-items: flex-start;
      gap: 12px 16px;
      min-height: 210px;
      padding: 18px;
      background: #f5faff;
      border: 1px dashed #8eabba;
      border-radius: 14px;
    }

    .balloon-unit {
      width: 116px;
      text-align: center;
    }

    .balloon {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 110px;
      height: 138px;
      margin: auto;
      padding: 12px;
      border: 2px solid #4185bb;
      border-radius: 52% 52% 48% 48%;
      background: linear-gradient(135deg, #c4eaff, #75b9ef);
      box-shadow: inset -10px -8px 0 #ffffff55;
      font-size: .9rem;
      font-weight: 800;
      line-height: 1.3;
    }

    .balloon::before {
      content: "";
      position: absolute;
      bottom: -9px;
      left: 46px;
      width: 16px;
      height: 14px;
      background: #75b9ef;
      border: 2px solid #4185bb;
      clip-path: polygon(50% 0, 100% 100%, 0 100%);
    }

    .balloon::after {
      content: "";
      position: absolute;
      top: 145px;
      left: 53px;
      width: 2px;
      height: 20px;
      background: #718896;
    }

    /* 0.5 molなら半分、0.25 molなら4分の1を黄色くする */
    .balloon.partial {
      background: linear-gradient(
        to top,
        #f5c563 0 var(--fill),
        white var(--fill) 100%
      );
      border-color: #b78627;
      box-shadow: none;
    }

    .balloon.partial::before {
      background: #f5c563;
      border-color: #b78627;
    }

    .balloon-unit p {
      margin: 27px 0 0;
      font-weight: 700;
    }

    .game-top {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 10px;
      padding: 11px 15px;
      background: var(--pale);
      border-radius: 10px;
      font-weight: 800;
    }

    .timer-low {
      color: var(--red);
    }

    .question {
      margin: 20px 0 15px;
      font-size: clamp(1.12rem, 3vw, 1.4rem);
      font-weight: 800;
    }

    .choices {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 12px;
      margin: 16px 0;
    }

    .choice {
      min-height: 92px;
      padding: 14px;
      text-align: center;
      font-size: clamp(1rem, 2.5vw, 1.23rem);
      overflow-wrap: anywhere;
    }

    .choice.correct-card {
      border: 3px solid var(--green);
      background: #e8f8ef;
      color: #105437;
    }

    .choice.wrong-card {
      border: 3px solid var(--red);
      background: #fff0f0;
      color: #8a2525;
    }

    .feedback {
      min-height: 52px;
      font-weight: 700;
      white-space: pre-line;
    }

    .feedback.correct { color: var(--green); }
    .feedback.incorrect { color: var(--red); }

    .game-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 14px;
    }

    @media (max-width: 650px) {
      .menu-grid,
      .stats,
      .choices {
        grid-template-columns: 1fr;
      }

      .choice { min-height: 65px; }
    }
  </style>
</head>

<body>
<header>
  <div>
    <h1>molをつかもう！</h1>
    <p>高校化学基礎｜物質量・粒子の個数・質量・気体の体積</p>
  </div>
</header>

<main>
  <section id="menu" class="screen" aria-labelledby="menu-title">
    <div class="panel">
      <h2 id="menu-title">メニュー</h2>
      <p>学習したい内容を選んでください。</p>

      <div class="menu-grid">
        <button class="menu-card" type="button" data-screen="lab">
          <strong>mol実験室</strong>
          <span>風船を増減して、粒子の個数と質量を比べる</span>
        </button>

        <button class="menu-card" type="button" data-category="particles">
          <strong>① mol ⇔ 個数</strong>
          <span>粒子の個数と物質量の単位換算</span>
        </button>

        <button class="menu-card" type="button" data-category="mass">
          <strong>② mol ⇔ 重さ</strong>
          <span>質量〔g〕と物質量の単位換算</span>
        </button>

        <button class="menu-card" type="button" data-category="volume">
          <strong>③ mol ⇔ 体積</strong>
          <span>標準状態の気体の体積〔L〕を換算</span>
        </button>

        <button class="menu-card" type="button" data-category="mixed">
          <strong>④ 総合・単位換算</strong>
          <span>個数・重さ・体積を混ぜた問題</span>
        </button>
      </div>

      <p class="note">
        <strong>チャレンジのルール：</strong>
        ４枚のカードから答えを選びます。
        各コース<strong>10問・制限時間60秒</strong>。
        解説を見ている間も時間は進みます。
      </p>
    </div>
  </section>

  <!-- mol実験室 -->
  <section id="lab" class="screen" hidden aria-labelledby="lab-title">
    <button class="back" type="button" data-screen="menu">← メニューへ</button>

    <div class="panel">
      <h2 id="lab-title">mol実験室</h2>
      <p>物質を選び、目盛りを動かして風船を増減させよう。</p>

      <div class="controls">
        <label for="substance">物質：</label>
        <select id="substance">
          <option value="C">炭素 C</option>
          <option value="H2O">水 H₂O</option>
          <option value="O2">酸素 O₂</option>
          <option value="Al">アルミニウム Al</option>
          <option value="CO2">二酸化炭素 CO₂</option>
          <option value="NaCl">塩化ナトリウム NaCl</option>
        </select>
      </div>

      <div>
        <label for="amount">
          物質量：<strong id="amount-label">1 mol</strong>
        </label><br>
        <input id="amount" type="range" min="0" max="8" value="2">
      </div>

      <div class="stats" aria-live="polite">
        <div class="stat">
          数えている粒子
          <strong id="particle-kind"></strong>
        </div>
        <div class="stat">
          粒子の合計
          <strong id="particle-count"></strong>
        </div>
        <div class="stat">
          質量
          <strong id="mass"></strong>
        </div>
      </div>

      <p id="lab-calculation"></p>

      <div id="balloons" class="balloons"
           role="img" aria-label="物質量を風船で表した模式図"></div>

      <p class="muted">
        青い風船１個＝1 mol＝6.0×10²³個。
        0.25 molと0.5 molは、黄色い部分の割合で表します。
        <strong>風船は数えるための模式図</strong>であり、
        物質の状態・実際の体積・質量の大小は表しません。
      </p>

      <p id="lab-note" class="note"></p>
    </div>
  </section>

  <!-- 10問タイムアタック -->
  <section id="game" class="screen" hidden aria-labelledby="game-title">
    <button class="back" type="button" data-screen="menu">← メニューへ</button>

    <div class="panel">
      <h2 id="game-title">チャレンジ</h2>

      <div id="game-top" class="game-top" aria-live="polite">
        <span id="progress">1 / 10問</span>
        <span id="score">正解 0問</span>
        <span id="timer">残り60秒</span>
      </div>

      <div id="play-area">
        <p id="question" class="question"></p>
        <div id="choices" class="choices" role="group"
             aria-label="４つの選択肢"></div>
        <p id="feedback" class="feedback" role="status" aria-live="polite"></p>

        <div class="game-actions">
          <button id="next-button" class="primary" type="button" hidden>
            次の問題 →
          </button>
        </div>
      </div>

      <div id="result-area" hidden>
        <h3 id="result-title"></h3>
        <p id="result-detail"></p>
        <div class="game-actions">
          <button id="retry-button" class="primary" type="button">
            同じコースに再挑戦
          </button>
          <button type="button" data-screen="menu">
            メニューへ
          </button>
        </div>
      </div>
    </div>
  </section>
</main>

<script>
"use strict";

const $ = id => document.getElementById(id);

const AVOGADRO = 6e23;
const MOLAR_VOLUME = 22.4; // 標準状態〔L/mol〕
const LIMIT_SECONDS = 60;
const QUESTION_COUNT = 10;

const amounts = [0.25, 0.5, 1, 2, 3, 4, 5, 7, 10];

const substances = {
  C: {
    name: "炭素 C",
    particle: "炭素原子",
    molarMass: 12,
    gas: false,
    note: "炭素1 molは炭素原子が6.0×10²³個。質量は12 gです。"
  },
  H2O: {
    name: "水 H₂O",
    particle: "水分子",
    molarMass: 18,
    gas: false,
    note: "水分子1個には水素原子が2個。水分子1 molには水素原子が2 mol含まれます。"
  },
  O2: {
    name: "酸素 O₂",
    particle: "酸素分子",
    molarMass: 32,
    gas: true,
    note: "酸素分子1個には酸素原子が2個。酸素分子1 molには酸素原子が2 mol含まれます。"
  },
  Al: {
    name: "アルミニウム Al",
    particle: "アルミニウム原子",
    molarMass: 27,
    gas: false,
    note: "アルミニウム1 molはアルミニウム原子が6.0×10²³個。質量は27 gです。"
  },
  CO2: {
    name: "二酸化炭素 CO₂",
    particle: "二酸化炭素分子",
    molarMass: 44,
    gas: true,
    note: "二酸化炭素分子1 molには酸素原子が2 mol含まれます。"
  },
  NaCl: {
    name: "塩化ナトリウム NaCl",
    particle: "NaClの組成式の単位",
    molarMass: 58.5,
    gas: false,
    note: "NaClは分子ではありません。NaCl 1 molにはNa⁺が1 mol、Cl⁻が1 mol含まれます。"
  },
  H2: {
    name: "水素 H₂",
    particle: "水素分子",
    molarMass: 2,
    gas: true,
    note: "水素分子1 molの質量は2.0 gです。"
  },
  N2: {
    name: "窒素 N₂",
    particle: "窒素分子",
    molarMass: 28,
    gas: true,
    note: "窒素分子1 molの質量は28 gです。"
  }
};

/*
  メニュー②の問題文に表示する原子量。
  物質に含まれる元素だけを表示する。
*/
const atomicMassText = {
  C: "C＝12",
  H2O: "H＝1、O＝16",
  O2: "O＝16",
  Al: "Al＝27",
  CO2: "C＝12、O＝16",
  NaCl: "Na＝23、Cl＝35.5",
  H2: "H＝1",
  N2: "N＝14"
};

const categoryNames = {
  particles: "① mol ⇔ 個数",
  mass: "② mol ⇔ 重さ",
  volume: "③ mol ⇔ 体積",
  mixed: "④ 総合・単位換算"
};

/* ---------- 共通の表示 ---------- */

function fmt(value) {
  return Number(value.toFixed(4)).toString();
}

function superscript(integer) {
  const digits = {
    "0": "⁰", "1": "¹", "2": "²", "3": "³", "4": "⁴",
    "5": "⁵", "6": "⁶", "7": "⁷", "8": "⁸", "9": "⁹",
    "-": "⁻"
  };
  return String(integer).split("").map(character => digits[character]).join("");
}

function countText(count) {
  if (count === 0) return "0個";

  const exponent = Math.floor(Math.log10(count));
  const coefficient = count / (10 ** exponent);

  return `${fmt(coefficient)}×10${superscript(exponent)}個`;
}

function valueText(value, unit) {
  return unit === "個"
    ? countText(value)
    : `${fmt(value)} ${unit}`;
}

function shuffle(items) {
  const copy = [...items];

  for (let i = copy.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [copy[i], copy[j]] = [copy[j], copy[i]];
  }

  return copy;
}

function showScreen(screenId) {
  if (screenId !== "game") stopTimer();

  document.querySelectorAll(".screen").forEach(screen => {
    screen.hidden = screen.id !== screenId;
  });

  window.scrollTo(0, 0);
}

/* ---------- mol実験室 ---------- */

function addBalloon(container, amount) {
  const unit = document.createElement("div");
  unit.className = "balloon-unit";

  const balloon = document.createElement("div");
  balloon.className = "balloon" + (amount < 1 ? " partial" : "");

  // 0.5 molなら50%、0.25 molなら25%を黄色く表示
  if (amount < 1) {
    balloon.style.setProperty("--fill", `${amount * 100}%`);
  }

  balloon.textContent = countText(amount * AVOGADRO);

  const caption = document.createElement("p");
  caption.textContent = `${fmt(amount)} mol`;

  unit.append(balloon, caption);
  container.append(unit);
}

function updateLab() {
  const substance = substances[$("substance").value];
  const mol = amounts[Number($("amount").value)];

  $("amount-label").textContent = `${fmt(mol)} mol`;
  $("particle-kind").textContent = substance.particle;
  $("particle-count").textContent = countText(mol * AVOGADRO);
  $("mass").textContent = `${fmt(mol * substance.molarMass)} g`;

  $("lab-calculation").textContent =
    `質量：${fmt(mol)} mol × ${substance.molarMass} g/mol` +
    ` ＝ ${fmt(mol * substance.molarMass)} g`;

  $("lab-note").textContent = substance.note;

  const container = $("balloons");
  container.replaceChildren();

  if (mol < 1) {
    addBalloon(container, mol);
  } else {
    for (let i = 0; i < mol; i++) {
      addBalloon(container, 1);
    }
  }

  container.setAttribute(
    "aria-label",
    `${substance.particle}${fmt(mol)} molを表す模式図。` +
    `粒子の合計は${countText(mol * AVOGADRO)}。`
  );
}

$("substance").addEventListener("change", updateLab);
$("amount").addEventListener("input", updateLab);
updateLab();

/* ---------- 問題生成 ---------- */

/*
  route：
  mol-count / count-mol
  mol-mass  / mass-mol
  mol-volume / volume-mol
  count-mass / mass-count
  count-volume / volume-count
  mass-volume / volume-mass

  どの経路でもmolを経由して計算する。
  体積が関係する問題は気体の物質だけを使用する。
*/
function makeQuestion(route, key, mol, showAtomicMass = false) {
  const substance = substances[key];
  const count = mol * AVOGADRO;
  const mass = mol * substance.molarMass;
  const volume = mol * MOLAR_VOLUME;

  const source = {
    mol:    { value: mol, unit: "mol" },
    count:  { value: count, unit: "個" },
    mass:   { value: mass, unit: "g" },
    volume: { value: volume, unit: "L" }
  };

  const [from, to] = route.split("-");
  const given = source[from];
  const answer = source[to];

  const askVolume = from === "volume" || to === "volume";
  const context = askVolume ? "（標準状態）" : "";

  // メニュー②の場合だけ、問題文に必要な原子量を加える
  const atomicMassInfo = showAtomicMass
    ? `（原子量：${atomicMassText[key]}）`
    : "";

  const question =
    `${substance.name}${context}${atomicMassInfo}：` +
    `${from === "count" ? substance.particle + " " : ""}` +
    `${valueText(given.value, given.unit)} は` +
    `${to === "count" ? "何個" :
      to === "mass" ? "何 g" :
      to === "volume" ? "何 L" : "何 mol"}？`;

  let formula = "";

  if (route === "mol-count") {
    formula = `${fmt(mol)} mol × 6.0×10²³ 個/mol`;
  } else if (route === "count-mol") {
    formula = `${countText(count)} ÷ (6.0×10²³ 個/mol)`;
  } else if (route === "mol-mass") {
    formula = `${fmt(mol)} mol × ${substance.molarMass} g/mol`;
  } else if (route === "mass-mol") {
    formula = `${fmt(mass)} g ÷ ${substance.molarMass} g/mol`;
  } else if (route === "mol-volume") {
    formula = `${fmt(mol)} mol × 22.4 L/mol`;
  } else if (route === "volume-mol") {
    formula = `${fmt(volume)} L ÷ 22.4 L/mol`;
  } else if (route === "count-mass") {
    formula =
      `${countText(count)} ÷ (6.0×10²³ 個/mol)` +
      ` ＝ ${fmt(mol)} mol、${fmt(mol)} × ${substance.molarMass}`;
  } else if (route === "mass-count") {
    formula =
      `${fmt(mass)} ÷ ${substance.molarMass}` +
      ` ＝ ${fmt(mol)} mol、${fmt(mol)} × 6.0×10²³`;
  } else if (route === "count-volume") {
    formula =
      `${countText(count)} ÷ (6.0×10²³ 個/mol)` +
      ` ＝ ${fmt(mol)} mol、${fmt(mol)} × 22.4`;
  } else if (route === "volume-count") {
    formula =
      `${fmt(volume)} ÷ 22.4` +
      ` ＝ ${fmt(mol)} mol、${fmt(mol)} × 6.0×10²³`;
  } else if (route === "mass-volume") {
    formula =
      `${fmt(mass)} ÷ ${substance.molarMass}` +
      ` ＝ ${fmt(mol)} mol、${fmt(mol)} × 22.4`;
  } else if (route === "volume-mass") {
    formula =
      `${fmt(volume)} ÷ 22.4` +
      ` ＝ ${fmt(mol)} mol、${fmt(mol)} × ${substance.molarMass}`;
  }

  return {
    question,
    answer: answer.value,
    unit: answer.unit,
    explanation:
      `${formula} ＝ ${valueText(answer.value, answer.unit)}`
  };
}

function makePool(category) {
  const allKeys = ["C", "H2O", "O2", "Al", "CO2", "NaCl", "H2", "N2"];
  const gasKeys = ["O2", "CO2", "H2", "N2"];
  const molValues = [0.25, 0.5, 1, 2, 3, 4, 5, 10];

  const routes = category === "particles"
    ? ["mol-count", "count-mol"]
    : category === "mass"
      ? ["mol-mass", "mass-mol"]
      : category === "volume"
        ? ["mol-volume", "volume-mol"]
        : [
            "mol-count", "count-mol",
            "mol-mass", "mass-mol",
            "mol-volume", "volume-mol",
            "count-mass", "mass-count",
            "count-volume", "volume-count",
            "mass-volume", "volume-mass"
          ];

  const pool = [];

  for (const route of routes) {
    const keys = route.includes("volume") ? gasKeys : allKeys;

    for (const key of keys) {
      for (const mol of molValues) {
        pool.push(
          makeQuestion(route, key, mol, category === "mass")
        );
      }
    }
  }

  return pool;
}

/*
  誤答カードは正解の0.25倍・0.5倍・2倍・4倍・10倍など。
  同じ表示の選択肢が重ならないようにする。
*/
function makeOptions(question) {
  const multipliers = shuffle([0.1, 0.25, 0.5, 2, 4, 10]);
  const options = [question.answer];
  const seen = new Set([valueText(question.answer, question.unit)]);

  for (const factor of multipliers) {
    const candidate = question.answer * factor;
    const display = valueText(candidate, question.unit);

    if (!seen.has(display)) {
      options.push(candidate);
      seen.add(display);
    }

    if (options.length === 4) break;
  }

  return shuffle(options);
}

/* ---------- タイムアタック ---------- */

let currentCategory = null;
let questions = [];
let questionIndex = 0;
let correctCount = 0;
let answeredCount = 0;
let waitingForNext = false;
let gameFinished = true;
let timerId = null;
let deadline = 0;
let secondsLeft = LIMIT_SECONDS;

function stopTimer() {
  if (timerId !== null) {
    clearInterval(timerId);
    timerId = null;
  }
}

function updateGameTop() {
  $("progress").textContent =
    `${Math.min(questionIndex + 1, QUESTION_COUNT)} / ${QUESTION_COUNT}問`;
  $("score").textContent = `正解 ${correctCount}問`;
  $("timer").textContent = `残り${secondsLeft}秒`;
  $("timer").classList.toggle("timer-low", secondsLeft <= 10);
}

function tickTimer() {
  if (gameFinished) return;

  secondsLeft = Math.max(
    0,
    Math.ceil((deadline - Date.now()) / 1000)
  );

  updateGameTop();

  if (secondsLeft <= 0) {
    finishGame(true);
  }
}

function startGame(category) {
  stopTimer();

  currentCategory = category;
  questions = shuffle(makePool(category)).slice(0, QUESTION_COUNT);
  questionIndex = 0;
  correctCount = 0;
  answeredCount = 0;
  waitingForNext = false;
  gameFinished = false;
  secondsLeft = LIMIT_SECONDS;

  $("game-title").textContent = categoryNames[category];
  $("play-area").hidden = false;
  $("result-area").hidden = true;
  $("next-button").hidden = true;

  showScreen("game");
  renderQuestion();
  updateGameTop();

  deadline = Date.now() + LIMIT_SECONDS * 1000;
  timerId = setInterval(tickTimer, 200);
}

function renderQuestion() {
  const current = questions[questionIndex];
  waitingForNext = false;

  $("question").textContent = current.question;
  $("feedback").textContent = "";
  $("feedback").className = "feedback";
  $("next-button").hidden = true;

  const choices = $("choices");
  choices.replaceChildren();

  for (const value of makeOptions(current)) {
    const card = document.createElement("button");
    card.type = "button";
    card.className = "choice";
    card.textContent = valueText(value, current.unit);

    card.addEventListener("click", () => {
      chooseAnswer(value, card);
    });

    choices.append(card);
  }

  updateGameTop();
}

function chooseAnswer(value, selectedCard) {
  if (gameFinished || waitingForNext) return;

  const current = questions[questionIndex];
  const isCorrect =
    Math.abs(value - current.answer) <=
    Math.abs(current.answer) * 1e-10;

  answeredCount++;

  if (isCorrect) correctCount++;

  waitingForNext = true;

  for (const card of $("choices").querySelectorAll("button")) {
    card.disabled = true;

    if (card.textContent === valueText(current.answer, current.unit)) {
      card.classList.add("correct-card");
    }
  }

  if (!isCorrect) {
    selectedCard.classList.add("wrong-card");
  }

  $("feedback").className =
    `feedback ${isCorrect ? "correct" : "incorrect"}`;

  $("feedback").textContent =
    `${isCorrect ? "正解！" : "惜しい！"}\n${current.explanation}`;

  updateGameTop();

  if (answeredCount === QUESTION_COUNT) {
    finishGame(false);
  } else {
    $("next-button").hidden = false;
  }
}

function finishGame(timeUp) {
  if (gameFinished) return;

  gameFinished = true;
  stopTimer();

  $("play-area").hidden = true;
  $("result-area").hidden = false;

  $("result-title").textContent =
    timeUp ? "時間切れ！" : "10問終了！";

  $("result-detail").textContent =
    `正解 ${correctCount}問 ／ 解答 ${answeredCount}問 ／ 全10問。` +
    (timeUp
      ? " 時間内に解けなかった問題は未解答です。"
      : ` 残り時間：${secondsLeft}秒。`);
}

/* ---------- ボタン操作 ---------- */

document.querySelectorAll("[data-screen]").forEach(button => {
  button.addEventListener("click", () => {
    showScreen(button.dataset.screen);
  });
});

document.querySelectorAll("[data-category]").forEach(button => {
  button.addEventListener("click", () => {
    startGame(button.dataset.category);
  });
});

$("next-button").addEventListener("click", () => {
  if (gameFinished || !waitingForNext) return;

  questionIndex++;
  renderQuestion();
});

$("retry-button").addEventListener("click", () => {
  startGame(currentCategory);
});

showScreen("menu");
</script>
</body>
</html>
