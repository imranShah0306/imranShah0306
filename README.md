- 👋 Hi, I’m @imranShah0306
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
imranShah0306/imranShah0306 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <title>Meri Website</title>
  <style>
    body { font-family: Arial; text-align: center; margin-top: 50px; }
    h1 { color: #2ecc71; }
  </style>
</head>
<body>
  <h1>नमस्ते! ये मेरी GitHub Pages वेबसाइट है 😊</h1>
  <p>by @ImranShah163398</p>
</body>
</html>ImranShah163398.github.io/
│
├── index.html
├── style.css
├── script.js
├── assets/
│   └── logo.png          (optional – add your logo)
└── data/
    └── books.json        (all books, quotes, poems…)<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>BookVerse – हर भाषा, हर थीम</title>
  <link rel="stylesheet" href="style.css" />
  <link rel="icon" href="assets/logo.png" type="image/png" />
</head>
<body>
  <!-- Header -->
  <header>
    <div class="container flex">
      <h1><a href="/">BookVerse</a></h1>
      <nav>
        <select id="langSelect">
          <option value="en">English</option>
          <option value="hi">हिन्दी</option>
          <option value="ur">اردو</option>
          <option value="ta">தமிழ்</option>
        </select>
        <button id="themeBtn">🌙</button>
      </nav>
    </div>
  </header>

  <!-- Search -->
  <section class="search container">
    <input type="text" id="searchBox" placeholder="Search books, quotes, poems…" />
  </section>

  <!-- Tabs -->
  <section class="tabs container">
    <button class="tab active" data-tab="novels">Novels</button>
    <button class="tab" data-tab="poems">Poems</button>
    <button class="tab" data-tab="quotes">Quotes</button>
    <button class="tab" data-tab="qa">Q&A</button>
    <button class="tab" data-tab="motiv">Motivational</button>
  </section>

  <!-- Content Grid -->
  <section id="content" class="container grid"></section>

  <footer class="container">
    <p>© 2025 <a href="https://github.com/ImranShah163398" target="_blank">@ImranShah163398</a> – Free for everyone</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
/* ==== Reset & Base ==== */
* { margin:0; padding:0; box-sizing:border-box; }
body { font-family: 'Segoe UI', sans-serif; line-height:1.6; background:#fafafa; color:#333; transition:background .3s, color .3s; }
a { color:inherit; text-decoration:none; }

/* ==== Theme Colors ==== */
body.dark { background:#121212; color:#e0e0e0; }
body.sepia { background:#f4ecd8; color:#5a3f2d; }

/* ==== Layout ==== */
.container { max-width:1200px; margin:auto; padding:1rem; }
.flex { display:flex; justify-content:space-between; align-items:center; }
.grid { display:grid; gap:1.5rem; grid-template-columns:repeat(auto-fill, minmax(260px,1fr)); }

/* ==== Header ==== */
header { background:#2c3e50; color:#fff; padding:1rem 0; }
header h1 a { font-size:1.8rem; }
nav select, nav button { margin-left:.5rem; padding:.4rem .8rem; }

/* ==== Search ==== */
.search input { width:100%; padding:.8rem; font-size:1rem; border:1px solid #ccc; border-radius:4px; }

/* ==== Tabs ==== */
.tabs { margin:1.5rem 0; display:flex; gap:.5rem; flex-wrap:wrap; }
.tab { padding:.6rem 1rem; background:#eee; border:none; border-radius:4px; cursor:pointer; }
.tab.active { background:#2c3e50; color:#fff; }

/* ==== Cards ==== */
.card {
  background:#fff; border-radius:8px; overflow:hidden; box-shadow:0 2px 6px rgba(0,0,0,.1);
  transition:transform .2s;
}
.card:hover { transform:translateY(-4px); }
.card img { width:100%; height:180px; object-fit:cover; }
.card-body { padding:1rem; }
.card-title { font-weight:600; margin-bottom:.4rem; }
.card-lang { font-size:.85rem; color:#777; }

/* Dark mode overrides */
body.dark .card { background:#1e1e1e; }
body.dark .tab { background:#333; color:#ddd; }
body.dark .tab.active { background:#bb86fc; }

/* Footer */
footer { text-align:center; padding:2rem 0; font-size:.9rem; color:#777; }
// ==== Data (books.json will be fetched) ====
const DATA_URL = "data/books.json";

// ==== DOM Elements ====
const langSelect = document.getElementById('langSelect');
const themeBtn   = document.getElementById('themeBtn');
const searchBox  = document.getElementById('searchBox');
const tabs       = document.querySelectorAll('.tab');
const content    = document.getElementById('content');

// ==== State ====
let allData = [];
let currentLang = 'en';
let currentTab = 'novels';
let currentTheme = 'light';

// ==== Load JSON ====
fetch(DATA_URL)
  .then(r => r.json())
  .then(data => {
    allData = data;
    render();
  });

// ==== Render ====
function render() {
  const filtered = allData
    .filter(item => item.type === currentTab)
    .filter(item => item.title.toLowerCase().includes(searchBox.value.toLowerCase()) ||
                    item.author.toLowerCase().includes(searchBox.value.toLowerCase()));

  content.innerHTML = filtered.map(book => `
    <article class="card">
      ${book.cover ? `<img src="${book.cover}" alt="${book.title}">` : ''}
      <div class="card-body">
        <div class="card-title">${book.title}</div>
        <div class="card-lang">${book.author} • ${book.lang.toUpperCase()}</div>
        <p>${book.desc.slice(0,80)}…</p>
        <a href="${book.link}" target="_blank" class="btn">Read →</a>
      </div>
    </article>
  `).join('');

  document.querySelectorAll('.tab').forEach(t => t.classList.toggle('active', t.dataset.tab === currentTab));
}

// ==== Language Switch ====
langSelect.addEventListener('change', e => {
  currentLang = e.target.value;
  render();
});

// ==== Theme Switch ====
themeBtn.addEventListener('click', () => {
  if (currentTheme === 'light') { currentTheme = 'dark'; themeBtn.textContent = '☀️'; }
  else if (currentTheme === 'dark') { currentTheme = 'sepia'; themeBtn.textContent = '🌙'; }
  else { currentTheme = 'light'; themeBtn.textContent = '🌙'; }

  document.body.className = currentTheme;
});

// ==== Tab Switch ====
tabs.forEach(t => t.addEventListener('click', () => {
  currentTab = t.dataset.tab;
  render();
}));

// ==== Search ====
searchBox.addEventListener('input', () => render());
[
  {
    "type": "novels",
    "title": "Pride and Prejudice",
    "author": "Jane Austen",
    "lang": "en",
    "desc": "A classic romance novel about Elizabeth Bennet and Mr. Darcy.",
    "cover": "https://covers.openlibrary.org/b/id/8257873-M.jpg",
    "link": "https://www.gutenberg.org/ebooks/1342"
  },
  {
    "type": "novels",
    "title": "गोदान",
    "author": "प्रेमचंद",
    "lang": "hi",
    "desc": "भारतीय ग्रामीण जीवन का महाकाव्य उपन्यास।",
    "cover": "https://example.com/godan.jpg",
    "link": "https://hindisahitya.org/godan"
  },
  {
    "type": "poems",
    "title": "मधुशाला",
    "author": "हरिवंश राय बच्चन",
    "lang": "hi",
    "desc": "जीवन, प्रेम और शराब की काव्यात्मक यात्रा।",
    "cover": "",
    "link": "https://rekhta.org/ebooks/madhusala-harivansh-rai-bachchan-ebooks"
  },
  {
    "type": "quotes",
    "title": "Success Quote",
    "author": "APJ Abdul Kalam",
    "lang": "en",
    "desc": "“Dream, Dream, Dream. Dreams transform into thoughts and thoughts result in action.”",
    "cover": "",
    "link": "#"
  },
  {
    "type": "qa",
    "title": "What is GitHub Pages?",
    "author": "GitHub Docs",
    "lang": "en",
    "desc": "GitHub Pages is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository.",
    "cover": "",
    "link": "https://docs.github.com/en/pages"
  },
  {
    "type": "motiv",
    "title": "Never Give Up",
    "author": "Winston Churchill",
    "lang": "en",
    "desc": "“If you're going through hell, keep going.”",
    "cover": "",
    "link": "#"
  }
]
# 1. Clone (or create locally)
git clone https://github.com/ImranShah163398/ImranShah163398.github.io.git
cd ImranShah163398.github.io

# 2. Copy all files (index.html, style.css, script.js, data/, assets/)

# 3. Commit & push
git add .
git commit -m "Initial BookVerse site"
git push origin main