<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <title>Legends of Fortnite</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0d0d0d;
      color: #eee;
    }
    header {
      background: linear-gradient(90deg, #6a11cb, #2575fc);
      padding: 20px;
      text-align: center;
      font-size: 28px;
      font-weight: bold;
      color: white;
      letter-spacing: 2px;
      text-transform: uppercase;
    }
    section {
      padding: 20px;
      margin: 20px;
      border-radius: 12px;
      background: #1a1a1a;
      box-shadow: 0 0 10px rgba(0,0,0,0.7);
    }
    h2 {
      color: #00ffcc;
      margin-top: 0;
    }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin: 6px 0;
      border: none;
      border-radius: 6px;
      font-size: 14px;
    }
    input, textarea {
      background: #2a2a2a;
      color: #eee;
    }
    button {
      background: linear-gradient(90deg, #2575fc, #6a11cb);
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      opacity: 0.85;
    }
    .hidden { display: none; }
    .admin-panel {
      border: 1px solid #444;
      padding: 15px;
      margin-top: 15px;
      border-radius: 8px;
      background: #111;
    }
    .list-item {
      background: #222;
      padding: 10px;
      margin: 5px 0;
      border-radius: 6px;
    }
    a {
      color: #00ccff;
    }
  </style>
</head>
<body>
  <header>Legends of Fortnite</header>

  <section>
    <h2>O nás</h2>
    <div id="about-text">Zatím žádné informace.</div>
  </section>

  <section>
    <h2>Sociální sítě</h2>
    <ul id="social-links"></ul>
  </section>

  <section>
    <h2>Přihláška do klubu</h2>
    <form id="signup-form">
      <input type="text" id="name" placeholder="Celé jméno" required>
      <input type="number" id="age" placeholder="Věk (9–14)" min="9" max="14" required>
      <input type="email" id="email" placeholder="E-mail (nebo nechte prázdné)">
      <input type="tel" id="phone" placeholder="Telefon (nebo nechte prázdné)">
      <textarea id="comment" placeholder="Komentář (volitelný)"></textarea>
      <button type="submit">Odeslat přihlášku</button>
    </form>
  </section>

  <section>
    <h2>Členové</h2>
    <div id="members-list"></div>
  </section>

  <section>
    <h2>Aktuality</h2>
    <div id="news-list"></div>
  </section>

  <section>
    <h2>Správce</h2>
    <input type="password" id="admin-code" placeholder="Zadej kód správce">
    <button onclick="loginAdmin()">Přihlásit</button>
    <div id="admin-panel" class="hidden admin-panel">
      <h3>Správcovský panel</h3>

      <h4>O nás</h4>
      <textarea id="about-input" placeholder="Popis o týmu"></textarea>
      <button onclick="updateAbout()">Uložit</button>

      <h4>Sociální sítě</h4>
      <input type="text" id="social-input" placeholder="Odkaz na sociální síť">
      <button onclick="addSocial()">Přidat odkaz</button>

      <h4>Přidat člena</h4>
      <input type="text" id="new-member" placeholder="Jméno člena">
      <button onclick="addMember()">Přidat</button>

      <h4>Přidat aktualitu</h4>
      <input type="text" id="new-news" placeholder="Text aktuality">
      <button onclick="addNews()">Přidat</button>

      <h4>Přihlášky</h4>
      <button onclick="showApplications()">Zobrazit přihlášky</button>
      <div id="applications" class="hidden"></div>
    </div>
  </section>

  <script>
    // Uložená data
    let members = JSON.parse(localStorage.getItem("members") || "[]");
    let news = JSON.parse(localStorage.getItem("news") || "[]");
    let socials = JSON.parse(localStorage.getItem("socials") || "[]");
    let about = localStorage.getItem("about") || "Zatím žádné informace.";
    let applications = JSON.parse(localStorage.getItem("applications") || "[]");

    // Zobrazení uložených dat
    document.getElementById("about-text").innerText = about;
    renderList("members-list", members);
    renderList("news-list", news);
    renderLinks();

    // Přihláška
    document.getElementById("signup-form").addEventListener("submit", e => {
      e.preventDefault();
      let name = document.getElementById("name").value.trim();
      let age = parseInt(document.getElementById("age").value);
      let email = document.getElementById("email").value.trim();
      let phone = document.getElementById("phone").value.trim();
      let comment = document.getElementById("comment").value.trim();

      if (!email && !phone) {
        alert("Musíte zadat alespoň e-mail nebo telefon.");
        return;
      }

      let app = {name, age, email, phone, comment};
      applications.push(app);
      localStorage.setItem("applications", JSON.stringify(applications));

      alert("Přihláška odeslána!");
      e.target.reset();
    });

    // Správce login
    function loginAdmin() {
      let code = document.getElementById("admin-code").value;
      if (code === "1235") {
        document.getElementById("admin-panel").classList.remove("hidden");
        alert("Vítej správče!");
      } else {
        alert("Špatný kód!");
      }
    }

    // O nás
    function updateAbout() {
      about = document.getElementById("about-input").value;
      document.getElementById("about-text").innerText = about;
      localStorage.setItem("about", about);
    }

    // Sociální sítě
    function addSocial() {
      let link = document.getElementById("social-input").value;
      if (link) {
        socials.push(link);
        localStorage.setItem("socials", JSON.stringify(socials));
        renderLinks();
        document.getElementById("social-input").value = "";
      }
    }
    function renderLinks() {
      let list = document.getElementById("social-links");
      list.innerHTML = "";
      socials.forEach(s => {
        let li = document.createElement("li");
        li.innerHTML = `<a href="${s}" target="_blank">${s}</a>`;
        list.appendChild(li);
      });
    }

    // Členové
    function addMember() {
      let name = document.getElementById("new-member").value;
      if (name) {
        members.push(name);
        localStorage.setItem("members", JSON.stringify(members));
        renderList("members-list", members);
        document.getElementById("new-member").value = "";
      }
    }

    // Aktuality
    function addNews() {
      let text = document.getElementById("new-news").value;
      if (text) {
        news.push(text);
        localStorage.setItem("news", JSON.stringify(news));
        renderList("news-list", news);
        document.getElementById("new-news").value = "";
      }
    }

    // Přihlášky
    function showApplications() {
      let box = document.getElementById("applications");
      box.innerHTML = "";
      applications.forEach(a => {
        let div = document.createElement("div");
        div.classList.add("list-item");
        div.innerHTML = `<b>${a.name}</b> (věk: ${a.age})<br>
                         Kontakt: ${a.email || a.phone}<br>
                         Komentář: ${a.comment || "—"}`;
        box.appendChild(div);
      });
      box.classList.toggle("hidden");
    }

    // Helper
    function renderList(id, arr) {
      let box = document.getElementById(id);
      box.innerHTML = "";
      arr.forEach(x => {
        let div = document.createElement("div");
        div.classList.add("list-item");
        div.innerText = x;
        box.appendChild(div);
      });
    }
  </script>
</body>
</html>
