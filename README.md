<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Jeu de mémorisation</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      padding: 30px;
      background: #f5f5f5;
    }
    textarea {
      width: 80%;
      height: 120px;
      font-size: 16px;
      padding: 10px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-top: 15px;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>

<h1>:brain: Mémorise et écris les mots</h1>
<p>Écris tous les mots dont tu te souviens :</p>

<textarea id="input" placeholder="Tape les mots séparés par des espaces ou des virgules..."></textarea>
<br>
<button onclick="corriger()">Valider</button>

<div class="result" id="resultat"></div>

<script>
  // :point_right: MODIFIE ICI TA LISTE DE MOTS
  const mots = [
    "chat", "chien", "maison", "école", "livre",
    "stylo", "table", "chaise", "ordinateur", "fenêtre"
  ];

  function nettoyer(texte) {
    return texte
      .toLowerCase()
      .normalize("NFD").replace(/[\u0300-\u036f]/g, "") // enlève accents
      .replace(/[^a-zA-Z0-9\s,]/g, "")
      .split(/[\s,]+/)
      .filter(m => m.length > 0);
  }

  function corriger() {
    const input = document.getElementById("input").value;
    const reponses = nettoyer(input);

    const uniques = [...new Set(reponses)];

    let bons = [];
    let faux = [];

    uniques.forEach(mot => {
      if (mots.includes(mot)) {
        bons.push(mot);
      } else {
        faux.push(mot);
      }
    });

    const manques = mots.filter(m => !bons.includes(m));

    document.getElementById("resultat").innerHTML = `
      <p><strong>Score : ${bons.length} / ${mots.length}</strong></p>
      <p>:white_check_mark: Mots trouvés : ${bons.join(", ") || "aucun"}</p>
      <p>:x: Mots manqués : ${manques.join(", ")}</p>
    `;
  }
</script>

</body>
</html>
