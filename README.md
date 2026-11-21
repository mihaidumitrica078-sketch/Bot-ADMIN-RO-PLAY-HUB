<!DOCTYPE html>
<html lang="ro">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Suport Joc</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #1e1f22;
      color: #ffffff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      background-color: #2b2d31;
      padding: 20px;
      border-radius: 10px;
      width: 90%;
      max-width: 400px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    }
    h2 {
      margin-top: 0;
      text-align: center;
    }
    input, textarea, button {
      width: 100%;
      margin-top: 10px;
      padding: 10px;
      border-radius: 5px;
      border: none;
      box-sizing: border-box;
      font-size: 16px;
    }
    input, textarea {
      background-color: #1e1f22;
      color: #ffffff;
    }
    button {
      background-color: #5865f2;
      color: white;
      font-weight: bold;
      cursor: pointer;
    }
    button:hover {
      background-color: #4752c4;
    }
    #status {
      margin-top: 10px;
      text-align: center;
      font-size: 14px;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>Suport Joc</h2>
    <input type="text" id="nume" placeholder="Numele tău din joc" required>
    <textarea id="mesaj" rows="4" placeholder="Descrie problema ta..." required></textarea>
    <button onclick="trimiteMesaj()">Trimite pe Discord</button>
    <div id="status"></div>
  </div>

  <script>
    const DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1573669767615611041/hgibeKkALGN9B3zc4RVeZvkfPZfqvIhBC9cDTyh2u11nYrscOxc95urmMhhEp-Z5GtUN";

    function trimiteMesaj() {
      const nume = document.getElementById("nume").value.trim();
      const mesaj = document.getElementById("mesaj").value.trim();
      const status = document.getElementById("status");

      if (!nume || !mesaj) {
        status.style.color = "#ff5555";
        status.innerText = "Te rog completează ambele câmpuri!";
        return;
      }

      status.style.color = "#ffffff";
      status.innerText = "Se trimite...";

      fetch(DISCORD_WEBHOOK_URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          content: `**Tichet nou de suport**\n**Jucător:** ${nume}\n**Mesaj:** ${mesaj}`
        })
      })
      .then(response => {
        if (response.ok) {
          status.style.color = "#55ff55";
          status.innerText = "Mesaj trimis cu succes!";
          document.getElementById("nume").value = "";
          document.getElementById("mesaj").value = "";
        } else {
          status.style.color = "#ff5555";
          status.innerText = "Eroare la trimitere. Verifică link-ul webhook.";
        }
      })
      .catch(error => {
        status.style.color = "#ff5555";
        status.innerText = "Eroare de conexiune.";
      });
    }
  </script>

</body>
</html>
