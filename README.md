<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Antrean</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: #f4f7f6; margin: 0; padding: 50px 20px; }
        .container { max-width: 400px; margin: auto; background: white; padding: 30px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        h1 { color: #333; margin-bottom: 5px; }
        p { color: #666; }
        .nomor-sekarang { font-size: 60px; font-weight: bold; color: #0056b3; margin: 20px 0; }
        
        button { padding: 15px 30px; font-size: 18px; color: white; background-color: #28a745; border: none; border-radius: 8px; cursor: pointer; width: 100%; transition: background-color 0.3s; }
        button:hover { background-color: #218838; }
        
        /* Gaya baru untuk tombol yang dinonaktifkan (mati) */
        button:disabled { background-color: #6c757d; cursor: not-allowed; } 
        
        .nomor-anda { margin-top: 25px; padding: 15px; background-color: #e9ecef; border-radius: 8px; display: none; }
        .nomor-anda p { margin: 0 0 10px 0; color: #333; }
        .angka-anda { font-size: 40px; font-weight: bold; color: #d9534f; }
    </style>
</head>
<body>

    <div class="container">
        <h1>Ambil Antrean</h1>
        <p>Satu perangkat hanya dapat mengambil satu nomor urut.</p>
        
        <div class="nomor-sekarang" id="tampilNomor">0</div>
        
        <button id="tombolAmbil" onclick="ambilNomor()">AMBIL NOMOR</button>

        <div class="nomor-anda" id="kartuAntrean">
            <p>Nomor Antrean Anda:</p>
            <div class="angka-anda" id="angkaAnda">-</div>
            <p style="font-size: 12px; margin-top: 10px; color: #888;">Tunjukkan layar ini kepada petugas</p>
        </div>
    </div>

    <script>
        let nomorTerakhir = localStorage.getItem('nomorAntrean') ? parseInt(localStorage.getItem('nomorAntrean')) : 0;
        let nomorSaya = localStorage.getItem('nomorPribadi'); // Cek memori apakah HP ini sudah ambil nomor
        
        document.getElementById('tampilNomor').innerText = nomorTerakhir;

        // Jika HP ini sudah punya nomor saat web dibuka, langsung kunci tombolnya
        if (nomorSaya) {
            kunciTombol(nomorSaya);
        }

        function ambilNomor() {
            // Cegah jika fungsi dipanggil paksa padahal sudah punya nomor
            if (localStorage.getItem('nomorPribadi')) return;

            nomorTerakhir++;
            
            // Simpan nomor terakhir dan tandai HP ini sudah mengambil nomor
            localStorage.setItem('nomorAntrean', nomorTerakhir);
            localStorage.setItem('nomorPribadi', nomorTerakhir); 
            
            document.getElementById('tampilNomor').innerText = nomorTerakhir;
            kunciTombol(nomorTerakhir);
        }

        // Fungsi untuk menampilkan nomor user dan mematikan tombol
        function kunciTombol(nomor) {
            document.getElementById('angkaAnda').innerText = nomor;
            document.getElementById('kartuAntrean').style.display = 'block';
            
            let tombol = document.getElementById('tombolAmbil');
            tombol.innerText = "NOMOR SUDAH DIAMBIL";
            tombol.disabled = true; // Tombol dimatikan dan berubah warna abu-abu
        }
    </script>

</body>
</html>
