<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Site d'Actualité</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background-color: #f5f5f5;
      color: #333;
    }
    header {
      background-color: #2c3e50;
      color: white;
      padding: 20px;
      text-align: center;
    }
    .journal-list, .articles, .article {
      max-width: 800px;
      margin: 20px auto;
      padding: 0 10px;
    }
    .journal-button {
      display: inline-block;
      margin: 5px;
      padding: 10px 20px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .journal-button:hover { background-color: #2980b9; }
    .article-card {
      background-color: white;
      margin: 10px 0;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      cursor: pointer;
    }
    .article-card img {
      max-width: 100%;
      border-radius: 5px;
    }
    .back-button {
      margin-top: 20px;
      display: inline-block;
      padding: 8px 15px;
      background-color: #e74c3c;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
    .back-button:hover { background-color: #c0392b; }
    a {
      color: #3498db;
      text-decoration: none;
    }
    a:hover { text-decoration: underline; }
  </style>
</head>
<body>

<header>
  <h1>Mon Site d'Actualité</h1>
</header>

<div class="journal-list">
  <h2>Choisissez un journal :</h2>
  <button class="journal-button" onclick="showArticles('BFM')">BFM</button>
  <button class="journal-button" onclick="showArticles('Le Figaro')">Le Figaro</button>
  <button class="journal-button" onclick="showArticles('Le Monde')">Le Monde</button>
</div>

<div class="articles" style="display:none;">
  <h2 id="journal-title"></h2>
  <div id="articles-container"></div>
  <div class="back-button" onclick="goHome()">← Retour</div>
</div>

<div class="article" style="display:none;">
  <h2 id="article-title"></h2>
  <img id="article-img" src="" alt="">
  <p id="article-text"></p>
  <p>Source : <a id="article-link" href="" target="_blank">Voir l'article original</a></p>
  <div class="back-button" onclick="showArticles(currentJournal)">← Retour aux articles</div>
</div>

<script>
  let currentJournal = '';

  const articlesData = {
    "BFM": [
      {title: "Macron annonce une nouvelle mesure", img:"https://via.placeholder.com/600x300", text:"Texte complet de l'article BFM du jour.", link:"https://www.bfmtv.com"},
      {title: "Economie française en hausse", img:"https://via.placeholder.com/600x300", text:"Texte complet de l'article BFM du jour.", link:"https://www.bfmtv.com"}
    ],
    "Le Figaro": [
      {title: "Politique internationale : situation tendue", img:"https://via.placeholder.com/600x300", text:"Texte complet de l'article Le Figaro du jour.", link:"https://www.lefigaro.fr"},
      {title: "Technologie : nouveautés 2026", img:"https://via.placeholder.com/600x300", text:"Texte complet de l'article Le Figaro du jour.", link:"https://www.lefigaro.fr"}
    ],
    "Le Monde": [
      {title: "Environnement : changement climatique", img:"https://via.placeholder.com/600x300", text:"Texte complet de l'article Le Monde du jour.", link:"https://www.lemonde.fr"},
      {title: "Culture : nouveaux films à voir", img:"https://via.placeholder.com/600x300", text:"Texte complet de l'article Le Monde du jour.", link:"https://www.lemonde.fr"}
    ]
  };

  function showArticles(journal) {
    currentJournal = journal;
    document.querySelector('.journal-list').style.display = 'none';
    document.querySelector('.articles').style.display = 'block';
    document.getElementById('journal-title').innerText = journal;
    const container = document.getElementById('articles-container');
    container.innerHTML = '';
    articlesData[journal].forEach((article, index) => {
      const card = document.createElement('div');
      card.className = 'article-card';
      card.innerHTML = `<h3>${article.title}</h3><img src="${article.img}" alt=""><p>${article.text.substring(0,100)}...</p>`;
      card.onclick = () => showArticle(journal, index);
      container.appendChild(card);
    });
  }

  function showArticle(journal, index) {
    const article = articlesData[journal][index];
    document.querySelector('.articles').style.display = 'none';
    document.querySelector('.article').style.display = 'block';
    document.getElementById('article-title').innerText = article.title;
    document.getElementById('article-img').src = article.img;
    document.getElementById('article-text').innerText = article.text;
    document.getElementById('article-link').href = article.link;
  }

  function goHome() {
    document.querySelector('.articles').style.display = 'none';
    document.querySelector('.journal-list').style.display = 'block';
  }
</script>

</body>
</html>

