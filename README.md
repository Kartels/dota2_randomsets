<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dota Randomizer</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Inter, Arial, sans-serif;
    background:
        radial-gradient(circle at top, #182333 0, #0b0f16 45%, #07090d 100%);
    color: #f4f6f8;
    min-height: 100vh;
}

.container {
    max-width: 1150px;
    margin: auto;
    padding: 35px 20px 60px;
}

header {
    text-align: center;
    margin-bottom: 30px;
}

.logo {
    font-size: 42px;
    font-weight: 900;
    letter-spacing: -2px;
}

.logo span {
    color: #e64b3c;
}

.subtitle {
    color: #9ca7b5;
    margin-top: 8px;
}

.grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
}

.card {
    background: rgba(20, 26, 35, .88);
    border: 1px solid #293342;
    border-radius: 18px;
    padding: 24px;
    box-shadow: 0 15px 50px #0007;
}

.card h2 {
    margin: 0 0 18px;
    font-size: 22px;
}

.hero-box {
    min-height: 245px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    background: linear-gradient(145deg, #111923, #0c1118);
    border-radius: 14px;
    border: 1px solid #303b4a;
    padding: 20px;
}

.hero-icon {
    width: 105px;
    height: 105px;
    border-radius: 50%;
    overflow: hidden;
    display: grid;
    place-items: center;
    font-size: 42px;
    font-weight: 900;
    background: linear-gradient(135deg, #e64b3c, #77251f);
    box-shadow: 0 0 35px #e64b3c55;
    margin-bottom: 14px;
}

.hero-icon img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.hero-name {
    font-size: 29px;
    font-weight: 800;
}

.role {
    color: #aab5c2;
    margin-top: 5px;
}

button {
    width: 100%;
    border: 0;
    border-radius: 12px;
    padding: 14px 18px;
    margin-top: 18px;
    background: linear-gradient(90deg, #e64b3c, #ff715b);
    color: white;
    font-size: 16px;
    font-weight: 800;
    cursor: pointer;
    transition: .18s;
    box-shadow: 0 8px 25px #e64b3c33;
}

button:hover {
    transform: translateY(-2px);
    filter: brightness(1.08);
}

.secondary {
    background: #202936;
    box-shadow: none;
}

.items {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.item {
    background: #10161f;
    border: 1px solid #2b3542;
    border-radius: 11px;
    padding: 10px;
    min-height: 70px;
    display: flex;
    align-items: center;
    gap: 10px;
}

.item img {
    width: 52px;
    height: 52px;
    object-fit: cover;
    border-radius: 6px;
    flex: none;
}

.item b {
    display: block;
    font-size: 14px;
}

.item small {
    color: #7f8b99;
}

.options {
    display: flex;
    gap: 10px;
    margin-top: 14px;
}

.options select {
    flex: 1;
    background: #10161f;
    color: #fff;
    border: 1px solid #303b49;
    padding: 11px;
    border-radius: 10px;
}

.full {
    grid-column: 1 / -1;
}

.history {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
}

.tag {
    background: #171f2a;
    border: 1px solid #303a47;
    padding: 8px 10px;
    border-radius: 9px;
    color: #b9c3cf;
    font-size: 13px;
}

/* =========================
   РАСКАЧКА СКИЛЛОВ
========================= */

.skill-build {
    margin-top: 10px;
    background: #0f151e;
    border: 1px solid #2b3542;
    border-radius: 14px;
    padding: 16px;
}

.skill-head {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    margin-bottom: 14px;
}

.skill-head b {
    font-size: 17px;
}

.skill-note {
    color: #7f8b99;
    font-size: 12px;
}

.skill-levels {
    display: grid;
    grid-template-columns: repeat(10, 1fr);
    gap: 7px;
}

.skill-level {
    background: #151d28;
    border: 1px solid #303b49;
    border-radius: 9px;
    padding: 8px 4px;
    text-align: center;
    min-height: 66px;
    transition: .15s;
}

.skill-level:hover {
    transform: translateY(-2px);
    border-color: #e64b3c;
}

.skill-level .lvl {
    font-size: 10px;
    color: #7f8b99;
}

.skill-level .spell {
    font-weight: 900;
    font-size: 16px;
    margin-top: 3px;
}

.skill-level .name {
    font-size: 9px;
    color: #aeb8c4;
    margin-top: 3px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.skill-level.ult {
    border-color: #e64b3c;
    box-shadow: inset 0 0 12px #e64b3c18;
}

.skill-legend {
    display: flex;
    justify-content: center;
    gap: 15px;
    flex-wrap: wrap;
    margin-top: 14px;
    color: #aab5c2;
    font-size: 12px;
}

.legend-q {
    color: #ffb3a8;
}

.legend-w {
    color: #8dc8ff;
}

.legend-e {
    color: #a7e6a1;
}

.legend-r {
    color: #e6a7ff;
}

/* =========================
   АНИМАЦИИ
========================= */

@keyframes appear {
    from {
        opacity: 0;
        transform: scale(.85);
    }

    to {
        opacity: 1;
        transform: scale(1);
    }
}

.appear {
    animation: appear .35s ease;
}

/* =========================
   МОБИЛЬНАЯ ВЕРСИЯ
========================= */

@media(max-width: 900px) {
    .skill-levels {
        grid-template-columns: repeat(6, 1fr);
    }
}

@media(max-width: 750px) {
    .grid {
        grid-template-columns: 1fr;
    }

    .full {
        grid-column: auto;
    }

    .items {
        grid-template-columns: 1fr 1fr;
    }

    .logo {
        font-size: 34px;
    }

    .skill-levels {
        grid-template-columns: repeat(5, 1fr);
    }
}

@media(max-width: 450px) {
    .items {
        grid-template-columns: 1fr;
    }

    .skill-levels {
        grid-template-columns: repeat(3, 1fr);
    }
}
</style>
</head>

<body>

<div class="container">

<header>
    <div class="logo">
        DOTA <span>RANDOMIZER</span>
    </div>

    <div class="subtitle">
        Случайный герой + случайная сборка + поэтапная раскачка
    </div>
</header>


<div class="grid">

<!-- =========================
     ГЕРОЙ
========================= -->

<section class="card">

    <h2>🎲 Случайный герой</h2>

    <div class="hero-box">

        <div class="hero-icon" id="heroIcon">
            <span>?</span>
        </div>

        <div class="hero-name" id="heroName">
            Нажми кнопку
        </div>

        <div class="role" id="heroRole">
            Герой появится здесь
        </div>

    </div>

    <button onclick="randomHero()">
        🎲 Выбрать героя
    </button>

</section>


<!-- =========================
     ПРЕДМЕТЫ
========================= -->

<section class="card">

    <h2>🧰 Рандомная сборка</h2>

    <div class="items" id="items">

        <div class="item">
            <b>?</b>
            <small>Основной предмет</small>
        </div>

        <div class="item">
            <b>?</b>
            <small>Основной предмет</small>
        </div>

        <div class="item">
            <b>?</b>
            <small>Основной предмет</small>
        </div>

        <div class="item">
            <b>?</b>
            <small>Основной предмет</small>
        </div>

        <div class="item">
            <b>?</b>
            <small>Основной предмет</small>
        </div>

        <div class="item">
            <b>?</b>
            <small>Основной предмет</small>
        </div>

    </div>

    <div class="options">

        <select id="mode">

            <option value="normal">
                Обычная сборка
            </option>

            <option value="chaos">
                Полный хаос
            </option>

            <option value="core">
                Только основные предметы
            </option>

        </select>

    </div>

    <button onclick="randomBuild()">
        🧰 Сгенерировать сборку
    </button>

</section>


<!-- =========================
     РАСКАЧКА
========================= -->

<section class="card full">

    <h2>📈 Поэтапная раскачка скиллов</h2>

    <div class="skill-build">

        <div class="skill-head">

            <b id="skillTitle">
                Раскачка появится здесь
            </b>

            <span class="skill-note">
                Уровни 1–30
            </span>

        </div>


        <div class="skill-levels" id="skillLevels">

            <div class="tag">
                Сначала выбери героя
            </div>

        </div>


        <div class="skill-legend">

            <span class="legend-q">
                Q — первый навык
            </span>

            <span class="legend-w">
                W — второй навык
            </span>

            <span class="legend-e">
                E — третий навык
            </span>

            <span class="legend-r">
                R — ультимейт
            </span>

        </div>

    </div>

</section>


<!-- =========================
     ИСПЫТАНИЕ
========================= -->

<section class="card full">

    <h2>⚡ Испытание</h2>

    <div id="challenge" class="tag">
        Сначала выбери героя и сборку
    </div>

    <button class="secondary" onclick="randomAll()">
        🎯 Рандомизировать всё
    </button>

</section>


<!-- =========================
     ИСТОРИЯ
========================= -->

<section class="card full">

    <h2>🕘 История</h2>

    <div class="history" id="history">

        <span class="tag">
            Пока пусто
        </span>

    </div>

</section>

</div>

</div>


<script>

/* =====================================================
   КАРТИНКИ
===================================================== */

const heroImgBase =
"https://cdn.cloudflare.steamstatic.com/apps/dota2/images/dota_react/heroes/";

const itemImgBase =
"https://cdn.cloudflare.steamstatic.com/apps/dota2/images/dota_react/items/";


/* =====================================================
   СЛАГИ ГЕРОЕВ
===================================================== */

const heroSlugs = {

    "Anti-Mage": "antimage",
    "Axe": "axe",
    "Bane": "bane",
    "Crystal Maiden": "crystal_maiden",
    "Drow Ranger": "drow_ranger",
    "Earthshaker": "earthshaker",
    "Juggernaut": "juggernaut",
    "Lina": "lina",
    "Lion": "lion",
    "Mirana": "mirana",
    "Phantom Assassin": "phantom_assassin",
    "Pudge": "pudge",
    "Shadow Fiend": "nevermore",
    "Sniper": "sniper",
    "Sven": "sven",
    "Tidehunter": "tidehunter",
    "Tinker": "tinker",
    "Tiny": "tiny",
    "Vengeful Spirit": "vengefulspirit",
    "Witch Doctor": "witch_doctor",
    "Zeus": "zuus",
    "Invoker": "invoker",
    "Mars": "mars",
    "Pangolier": "pangolier",
    "Void Spirit": "void_spirit",
    "Windranger": "windrunner",
    "Lifestealer": "life_stealer",
    "Slark": "slark",
    "Earth Spirit": "earth_spirit",
    "Queen of Pain": "queenofpain",
    "Riki": "riki",
    "Viper": "viper"

};


/* =====================================================
   СЛАГИ ПРЕДМЕТОВ
===================================================== */

const itemSlugs = {

    "Power Treads": "power_treads",
    "Phase Boots": "phase_boots",
    "Arcane Boots": "arcane_boots",
    "Butterfly": "butterfly",
    "Black King Bar": "black_king_bar",
    "Blink Dagger": "blink",
    "Force Staff": "force_staff",
    "Glimmer Cape": "glimmer_cape",
    "Aghanim's Scepter": "ultimate_scepter",
    "Aghanim's Shard": "aghanims_shard",
    "Satanic": "satanic",
    "Daedalus": "greater_crit",
    "Desolator": "desolator",
    "Manta Style": "manta",
    "Linken's Sphere": "sphere",
    "Hurricane Pike": "hurricane_pike",
    "Bloodthorn": "bloodthorn",
    "Silver Edge": "silver_edge",
    "Shadow Blade": "invis_sword",
    "Assault Cuirass": "assault",
    "Heart of Tarrasque": "heart",
    "Skadi": "skadi",
    "Moon Shard": "moon_shard",
    "Nullifier": "nullifier",
    "Orchid Malevolence": "orchid",
    "Octarine Core": "octarine_core",
    "Refresher Orb": "refresher",
    "Shiva's Guard": "shivas_guard",
    "Kaya": "kaya",
    "Yasha": "yasha",
    "Crystalys": "lesser_crit",
    "Maelstrom": "maelstrom",
    "Mjollnir": "mjollnir",
    "Radiance": "radiance",
    "Battle Fury": "bfury",
    "Sange and Yasha": "sange_and_yasha",
    "Guardian Greaves": "guardian_greaves",
    "Pipe of Insight": "pipe",
    "Lotus Orb": "lotus_orb",
    "Heaven's Halberd": "heavens_halberd",
    "Eul's Scepter": "cyclone",
    "Rod of Atos": "rod_of_atos",
    "Dagon": "dagon",
    "Scythe of Vyse": "sheepstick",
    "Aeon Disk": "aeon_disk",
    "Mekansm": "mekansm",
    "Vladmir's Offering": "vladmir"

};


/* =====================================================
   ГЕРОИ
===================================================== */

const heroes = [

    ["Anti-Mage","Carry / Escape","AM"],
    ["Axe","Initiator / Durable","AX"],
    ["Bane","Support / Disabler","BA"],
    ["Crystal Maiden","Support / Nuker","CM"],
    ["Drow Ranger","Carry","DR"],
    ["Earthshaker","Initiator / Support","ES"],
    ["Juggernaut","Carry","JG"],
    ["Lina","Nuker / Support","LI"],
    ["Lion","Support / Disabler","LN"],
    ["Mirana","Support / Nuker","MI"],
    ["Phantom Assassin","Carry","PA"],
    ["Pudge","Initiator / Durable","PU"],
    ["Shadow Fiend","Carry / Nuker","SF"],
    ["Sniper","Carry","SN"],
    ["Sven","Carry / Durable","SV"],
    ["Tidehunter","Initiator / Durable","TH"],
    ["Tinker","Nuker / Pusher","TI"],
    ["Tiny","Carry / Initiator","TY"],
    ["Vengeful Spirit","Support / Disabler","VS"],
    ["Witch Doctor","Support / Nuker","WD"],
    ["Zeus","Nuker","ZE"],
    ["Invoker","Nuker / Carry","IN"],
    ["Mars","Initiator / Durable","MA"],
    ["Pangolier","Carry / Initiator","PG"],
    ["Void Spirit","Carry / Escape","VO"],
    ["Windranger","Carry / Support","WR"],
    ["Lifestealer","Carry / Durable","LS"],
    ["Slark","Carry / Escape","SL"],
    ["Earth Spirit","Support / Initiator","ER"],
    ["Queen of Pain","Nuker / Escape","QP"],
    ["Riki","Carry / Escape","RI"],
    ["Viper","Carry / Durable","VP"]

];


/* =====================================================
   ПРЕДМЕТЫ
===================================================== */

const items = [

    "Power Treads",
    "Phase Boots",
    "Arcane Boots",
    "Butterfly",
    "Black King Bar",
    "Blink Dagger",
    "Force Staff",
    "Glimmer Cape",
    "Aghanim's Scepter",
    "Aghanim's Shard",
    "Satanic",
    "Daedalus",
    "Desolator",
    "Manta Style",
    "Linken's Sphere",
    "Hurricane Pike",
    "Bloodthorn",
    "Silver Edge",
    "Shadow Blade",
    "Assault Cuirass",
    "Heart of Tarrasque",
    "Skadi",
    "Moon Shard",
    "Nullifier",
    "Orchid Malevolence",
    "Octarine Core",
    "Refresher Orb",
    "Shiva's Guard",
    "Kaya",
    "Yasha",
    "Crystalys",
    "Maelstrom",
    "Mjollnir",
    "Radiance",
    "Battle Fury",
    "Sange and Yasha",
    "Guardian Greaves",
    "Pipe of Insight",
    "Lotus Orb",
    "Heaven's Halberd",
    "Eul's Scepter",
    "Rod of Atos",
    "Dagon",
    "Scythe of Vyse",
    "Aeon Disk",
    "Mekansm",
    "Vladmir's Offering"

];


/* =====================================================
   СКИЛЛЫ ГЕРОЕВ
===================================================== */

const skillNames = {

    "Anti-Mage": [
        "Mana Break",
        "Blink",
        "Counterspell",
        "Mana Void"
    ],

    "Axe": [
        "Berserker's Call",
        "Battle Hunger",
        "Counter Helix",
        "Culling Blade"
    ],

    "Bane": [
        "Enfeeble",
        "Brain Sap",
        "Nightmare",
        "Fiend's Grip"
    ],

    "Crystal Maiden": [
        "Crystal Nova",
        "Frostbite",
        "Arcane Aura",
        "Freezing Field"
    ],

    "Drow Ranger": [
        "Frost Arrows",
        "Gust",
        "Multishot",
        "Marksmanship"
    ],

    "Earthshaker": [
        "Fissure",
        "Enchant Totem",
        "Aftershock",
        "Echo Slam"
    ],

    "Juggernaut": [
        "Blade Fury",
        "Healing Ward",
        "Blade Dance",
        "Omnislash"
    ],

    "Lina": [
        "Dragon Slave",
        "Light Strike Array",
        "Fiery Soul",
        "Laguna Blade"
    ],

    "Lion": [
        "Earth Spike",
        "Hex",
        "Mana Drain",
        "Finger of Death"
    ],

    "Mirana": [
        "Starstorm",
        "Sacred Arrow",
        "Leap",
        "Moonlight Shadow"
    ],

    "Phantom Assassin": [
        "Stifling Dagger",
        "Phantom Strike",
        "Blur",
        "Coup de Grace"
    ],

    "Pudge": [
        "Meat Hook",
        "Rot",
        "Flesh Heap",
        "Dismember"
    ],

    "Shadow Fiend": [
        "Shadowraze",
        "Necromastery",
        "Presence of the Dark Lord",
        "Requiem of Souls"
    ],

    "Sniper": [
        "Shrapnel",
        "Headshot",
        "Take Aim",
        "Assassinate"
    ],

    "Sven": [
        "Storm Hammer",
        "Great Cleave",
        "Warcry",
        "God's Strength"
    ],

    "Tidehunter": [
        "Gush",
        "Kraken Shell",
        "Anchor Smash",
        "Ravage"
    ],

    "Tinker": [
        "Laser",
        "March of the Machines",
        "Defense Matrix",
        "Keen-Conveyance"
    ],

    "Tiny": [
        "Avalanche",
        "Toss",
        "Tree Grab",
        "Grow"
    ],

    "Vengeful Spirit": [
        "Magic Missile",
        "Wave of Terror",
        "Vengeance Aura",
        "Nether Swap"
    ],

    "Witch Doctor": [
        "Paralyzing Cask",
        "Voodoo Restoration",
        "Maledict",
        "Death Ward"
    ],

    "Zeus": [
        "Arc Lightning",
        "Lightning Bolt",
        "Heavenly Jump",
        "Thundergod's Wrath"
    ],

    "Invoker": [
        "Cold Snap",
        "Tornado",
        "Sun Strike",
        "Invoke"
    ],

    "Mars": [
        "Spear of Mars",
        "God's Rebuke",
        "Bulwark",
        "Arena of Blood"
    ],

    "Pangolier": [
        "Swashbuckle",
        "Shield Crash",
        "Lucky Shot",
        "Rolling Thunder"
    ],

    "Void Spirit": [
        "Aether Remnant",
        "Dissimilate",
        "Resonant Pulse",
        "Astral Step"
    ],

    "Windranger": [
        "Shackleshot",
        "Powershot",
        "Windrun",
        "Focus Fire"
    ],

    "Lifestealer": [
        "Rage",
        "Feast",
        "Ghoul Frenzy",
        "Infest"
    ],

    "Slark": [
        "Dark Pact",
        "Pounce",
        "Essence Shift",
        "Shadow Dance"
    ],

    "Earth Spirit": [
        "Boulder Smash",
        "Rolling Boulder",
        "Geomagnetic Grip",
        "Magnetize"
    ],

    "Queen of Pain": [
        "Shadow Strike",
        "Blink",
        "Scream of Pain",
        "Sonic Wave"
    ],

    "Riki": [
        "Smoke Screen",
        "Blink Strike",
        "Tricks of the Trade",
        "Cloak and Dagger"
    ],

    "Viper": [
        "Poison Attack",
        "Nethertoxin",
        "Corrosive Skin",
        "Viper Strike"
    ]

};


/* =====================================================
   ИСПЫТАНИЯ
===================================================== */

const challenges = [

    "Не покупай предметы, кроме этой сборки.",

    "До 15-й минуты нельзя покупать Boots.",

    "Каждый раз после смерти покупай случайный недорогой предмет.",

    "Обязательно собери первый выбранный предмет первым слотом.",

    "Нельзя продавать предметы до 30-й минуты.",

    "Играй всю игру без телепорта.",

    "Первый большой предмет должен быть собран до 20-й минуты.",

    "Если получил роль саппорта — не фарми древних крипов."

];


/* =====================================================
   ПЕРЕМЕННЫЕ
===================================================== */

let currentHero = null;


/* =====================================================
   RANDOM
===================================================== */

function pick(array) {

    return array[
        Math.floor(
            Math.random() * array.length
        )
    ];

}


/* =====================================================
   ВЫБОР ГЕРОЯ
===================================================== */

function randomHero() {

    currentHero = pick(heroes);

    const heroName =
        document.getElementById("heroName");

    const heroRole =
        document.getElementById("heroRole");

    const heroIcon =
        document.getElementById("heroIcon");


    heroName.textContent =
        currentHero[0];

    heroRole.textContent =
        currentHero[1];


    const slug =
        heroSlugs[currentHero[0]];


    heroIcon.innerHTML = `
        <img
            src="${heroImgBase}${slug}.png"
            alt="${currentHero[0]}"
            onerror="
                this.style.display='none';
                this.parentElement.textContent='${currentHero[2]}'
            "
        >
    `;


    heroIcon.classList.remove("appear");

    void heroIcon.offsetWidth;

    heroIcon.classList.add("appear");


    generateSkillBuild();

    addHistory(
        "Герой: " + currentHero[0]
    );

}


/* =====================================================
   РАНДОМНАЯ СБОРКА
===================================================== */

function randomBuild() {

    let mode =
        document.getElementById("mode").value;


    let pool = [...items];


    if (mode === "core") {

        pool = pool.filter(
            x => ![
                "Glimmer Cape",
                "Force Staff",
                "Pipe of Insight",
                "Mekansm",
                "Guardian Greaves"
            ].includes(x)
        );

    }


    if (mode === "chaos") {

        pool.push(
            "Divine Rapier",
            "Divine Rapier",
            "Dagon"
        );

    }


    pool.sort(
        () => Math.random() - .5
    );


    const selected =
        pool.slice(0, 6);


    const itemsElement =
        document.getElementById("items");


    itemsElement.innerHTML =
        selected.map((x, i) => {

            const slug =
                itemSlugs[x] ||
                x
                    .toLowerCase()
                    .replace(
                        /[^a-z0-9]+/g,
                        "_"
                    );


            return `
                <div class="item appear">

                    <img
                        src="${itemImgBase}${slug}.png"
                        alt="${x}"
                        onerror="
                            this.style.display='none'
                        "
                    >

                    <div>

                        <b>
                            ${x}
                        </b>

                        <small>
                            Слот ${i + 1}
                        </small>

                    </div>

                </div>
            `;

        }).join("");


    addHistory(
        "Сборка: " +
        selected.join(", ")
    );

}


/* =====================================================
   РАНДОМИЗИРОВАТЬ ВСЁ
===================================================== */

function randomAll() {

    randomHero();

    randomBuild();

    generateSkillBuild();


    const challenge =
        pick(challenges);


    document.getElementById(
        "challenge"
    ).textContent = challenge;


    addHistory(
        "Испытание: " +
        challenge
    );

}


/* =====================================================
   ГЕНЕРАЦИЯ РАСКАЧКИ
===================================================== */

const skillPatterns = [

    /* Универсальная */
    [
        "Q","W","Q","E","Q","R",
        "Q","W","W","W","R","E",
        "E","E","E","R",
        "Q","W","E","Q",
        "W","E","Q","W",
        "E","Q","W","E","Q","R"
    ],

    /* Агрессивная */
    [
        "Q","E","Q","W","Q","R",
        "Q","E","E","E","R","W",
        "W","W","W","R",
        "Q","E","W","Q",
        "E","W","Q","E",
        "W","Q","E","W","Q","R"
    ],

    /* Безопасная */
    [
        "W","Q","E","Q","Q","R",
        "Q","W","W","R","W","E",
        "E","E","E","R",
        "Q","W","E","Q",
        "W","E","Q","W",
        "E","Q","W","E","Q","R"
    ]

];


function generateSkillBuild() {

    if (!currentHero) {
        return;
    }


    const names =
        skillNames[currentHero[0]];


    if (!names) {

        document.getElementById(
            "skillTitle"
        ).textContent =
            "Раскачка для " +
            currentHero[0];

        return;

    }


    const pattern =
        pick(skillPatterns);


    document.getElementById(
        "skillTitle"
    ).textContent =
        "Раскачка: " +
        currentHero[0];


    const levels =
        document.getElementById(
            "skillLevels"
        );


    levels.innerHTML =
        pattern.map((key, index) => {

            const skillIndex = {

                Q: 0,
                W: 1,
                E: 2,
                R: 3

            }[key];


            const skillName =
                names[skillIndex];


            const isUltimate =
                key === "R";


            return `
                <div
                    class="skill-level ${isUltimate ? "ult" : ""} appear"
                    title="${skillName}"
                >

                    <div class="lvl">
                        Ур. ${index + 1}
                    </div>

                    <div class="spell">
                        ${key}
                    </div>

                    <div class="name">
                        ${skillName}
                    </div>

                </div>
            `;

        }).join("");

}


/* =====================================================
   ИСТОРИЯ
===================================================== */

function addHistory(text) {

    const history =
        document.getElementById(
            "history"
        );


    if (
        history.children.length === 1 &&
        history.children[0].textContent === "Пока пусто"
    ) {

        history.innerHTML = "";

    }


    const tag =
        document.createElement("span");


    tag.className =
        "tag";


    tag.textContent =
        text;


    history.prepend(tag);


    if (
        history.children.length > 8
    ) {

        history.lastChild.remove();

    }

}

</script>

</body>
</html>
