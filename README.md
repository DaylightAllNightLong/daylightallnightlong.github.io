<!DOCTYPE html>
<html>
<head>
  <title>Album Reviews</title>
  <style>
    body {
      font-family: Arial;
      max-width: 700px;
      margin: auto;
      background: #111;
      color: white;
    }

    .album {
      border-bottom: 1px solid #444;
      padding: 20px 0;
      display: flex;
      gap: 20px;
    }

    img {
      width: 120px;
      height: 120px;
      object-fit: cover;
    }
  </style>
</head>

<body>

<h1>Album Reviews</h1>
<div id="albums"></div>

<script>
const sheetURL = https://docs.google.com/spreadsheets/d/e/2PACX-1vSQcqFaWF-hb5omsFhFoAQaWiRwFwx2JpZp9AnQOp-YZi3zU04osljRIiYivhRccyCvCpT4e3H5yqM3/pub?gid=0&single=true&output=csv;

fetch(sheetURL)
  .then(res => res.text())
  .then(data => {
    const rows = data.split("\n").slice(1);
    const container = document.getElementById("albums");

    rows.forEach(row => {
      const cols = row.split(",");
      const album = cols[0];
      const review = cols[1];
      const cover = cols[2];

      const div = document.createElement("div");
      div.className = "album";

      div.innerHTML = `
        <img src="${cover}">
        <div>
          <h2>${album}</h2>
          <p>${review}</p>
        </div>
      `;

      container.appendChild(div);
    });
  });
</script>

</body>
</html>
