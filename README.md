<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Simulateur Transfert Gabon → Maroc</title>
</head>
<body style="font-family: Arial, sans-serif; padding: 20px; max-width: 600px; margin: auto;">
  <h2>📤 Simulateur de transfert (XAF → MAD)</h2>

  <label for="xaf">💰 Montant envoyé (FCFA) :</label>
  <input type="number" id="xaf" value="100000" style="width: 100%; padding: 8px;"><br><br>
  <button onclick="calcul()" style="padding: 10px;">Simuler</button>

  <div id="result" style="margin-top: 20px;">
    <p>💸 <strong>Frais Airtel (3%) :</strong> <span id="frais">—</span> FCFA</p>
    <p>📉 <strong>Montant net converti :</strong> <span id="netXaf">—</span> FCFA</p>
    <p>🇲🇦 <strong>Montant remis au client :</strong> <span id="madClient">—</span> MAD</p>
  </div>

  <hr>
  <h3>🔒 Espace Admin (bénéfice caché)</h3>
  <label>Mot de passe :
    <input type="password" id="password" style="padding: 6px;">
  </label>
  <button onclick="afficherAdmin()" style="margin-left: 10px; padding: 6px;">Afficher</button>

  <div id="admin" style="margin-top: 20px; display: none;">
    <p>📈 <strong>Montant réel (taux officiel) :</strong> <span id="madReel">—</span> MAD</p>
    <p>🧾 <strong>Ton bénéfice :</strong> <span id="benefMad">—</span> MAD (<span id="benefXaf">—</span> FCFA)</p>
  </div>

  <script>
    const tauxReel = 62.26;
    const tauxClient = 0.01485;
    const motDePasse = "BENEF2025";

    function calcul() {
      let xaf = parseFloat(document.getElementById("xaf").value);
      let fraisAirtel = xaf * 0.03;
      let netXaf = xaf - fraisAirtel;
      let madClient = netXaf * tauxClient;
      let madReel = netXaf / tauxReel;
      let benefMad = madReel - madClient;
      let benefXaf = benefMad * tauxReel;

      document.getElementById("frais").textContent = fraisAirtel.toFixed(0);
      document.getElementById("netXaf").textContent = netXaf.toFixed(0);
      document.getElementById("madClient").textContent = madClient.toFixed(2);
      document.getElementById("madReel").textContent = madReel.toFixed(2);
      document.getElementById("benefMad").textContent = benefMad.toFixed(2);
      document.getElementById("benefXaf").textContent = Math.round(benefXaf);
    }

    function afficherAdmin() {
      let pass = document.getElementById("password").value;
      if (pass === motDePasse) {
        document.getElementById("admin").style.display = "block";
      } else {
        alert("Mot de passe incorrect !");
      }
    }
  </script>
</body>
</html>
