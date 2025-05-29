<!DOCTYPE html>
<html lang="id">

<head>
    <meta charset="UTF-8" />
    <title>Kalkulator Waktu</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }

        .container {
            border: 1px solid #ccc;
            padding: 20px;
            margin: 20px 0;
        }

        input[type="time"] {
            width: 100%;
            margin-bottom: 10px;
        }

        button {
            background: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            margin-right: 10px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        th,
        td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }

        th {
            background-color: #f2f2f2;
        }
    </style>
</head>

<body>
    <h1>Kalkulator Waktu</h1>

    <div class="container">
        <label for="start">Waktu Mulai:</label>
        <input type="time" id="start" required />

        <label for="end">Waktu Selesai:</label>
        <input type="time" id="end" required />

        <button onclick="hitungDurasi()">Hitung Durasi</button>
        <button onclick="resetForm()">Reset</button>
    </div>

    <div id="hasil"></div>

    <script>
        function hitungDurasi() {
            const start = document.getElementById("start").value;
            const end = document.getElementById("end").value;

            // Validasi input
            if (!start || !end) {
                alert("Silakan lengkapi waktu mulai dan selesai!");
                return;
            }

            // Konversi waktu ke menit
            function convertToMinutes(time) {
                const [hours, minutes] = time.split(":").map(Number);
                return hours * 60 + minutes;
            }

            const startMin = convertToMinutes(start);
            const endMin = convertToMinutes(end);

            if (endMin < startMin) {
                alert("Waktu selesai tidak boleh lebih awal dari waktu mulai!");
                return;
            }

            const diffMinutes = endMin - startMin;
            const jam = Math.floor(diffMinutes / 60);
            const menit = diffMinutes % 60;

            // Tampilkan hasil
            const hasilDiv = document.getElementById("hasil");
            hasilDiv.innerHTML = `
        <table>
          <tr><th>Waktu Mulai</th><td>${start}</td></tr>
          <tr><th>Waktu Selesai</th><td>${end}</td></tr>
          <tr><th>Durasi</th><td>${jam} jam ${menit} menit</td></tr>
        </table>
      `;
        }

        function resetForm() {
            document.getElementById("start").value = "";
            document.getElementById("end").value = "";
            document.getElementById("hasil").innerHTML = "";
        }
    </script>
</body>

</html>
