# antrean.html<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Antrean</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f7f6;
            margin: 0;
            padding: 50px 20px;
        }
        .container {
            max-width: 400px;
            margin: auto;
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            margin-bottom: 5px;
        }
        p {
            color: #666;
        }
        .nomor-sekarang {
            font-size: 60px;
            font-weight: bold;
            color: #0056b3;
            margin: 20px 0;
        }
        button {
            padding: 15px 30px;
            font-size: 18px;
            color: white;
            background-color: #28a745;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #218838;
        }
        .nomor-anda {
            margin-top: 25px;
            padding: 15px;
            background-color: #e9ecef;
            border-radius: 8px;
            display: none; /* Disembunyikan sebelum tombol ditekan */
        }
        .nomor-anda p {
            margin: 0 0 10px 0;
            color: #333;
        }
        .angka-anda {
            font-size: 40px;
            font-weight: bold;
            color: #d9534f;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Ambil Antrean</h1>
        <p>Silakan tekan tombol di bawah untuk mengambil nomor urut Anda.</p>
        
        <div class="nomor-sekarang" id="tampilNomor">0</div>
        
        <button onclick="ambilNomor()">AMBIL NOMOR</button>

        <div class="nomor-anda" id="kartuAntrean">
            <p>Nomor Antrean Anda:</p>
            <div class="angka-anda" id="angkaAnda">-</div>
            <p style="font-size: 12px; margin-top: 10px; color: #888;">Tunjukkan layar ini kepada petugas</p>
        </div>
    </div>

    <script>
        // Mengambil data nomor terakhir dari memori browser, jika kosong maka mulai dari 0
        let nomorTerakhir = localStorage.getItem('nomorAntrean') ? parseInt(localStorage.getItem('nomorAntrean')) : 0;
        
        // Menampilkan nomor terakhir di layar
        document.getElementById('tampilNomor').innerText = nomorTerakhir;

        function ambilNomor() {
            // Menambah nomor urut
            nomorTerakhir++;
            
            // Menyimpan nomor baru ke dalam memori browser
            localStorage.setItem('nomorAntrean', nomorTerakhir);
            
            // Memperbarui angka di layar
            document.getElementById('tampilNomor').innerText = nomorTerakhir;
            
            // Menampilkan nomor khusus untuk pengunjung tersebut
            document.getElementById('angkaAnda').innerText = nomorTerakhir;
            document.getElementById('kartuAntrean').style.display = 'block';
        }
    </script>

</body>
</html>
