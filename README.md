# ujian- <!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ujian Anti-Cheat PRO</title>
    <style>
        body { font-family: sans-serif; padding: 20px; user-select: none; -webkit-user-select: none; }
        .box { border: 2px solid #333; padding: 15px; border-radius: 8px; }
        
        /* Layar Kunci Total */
        #layar-kunci { 
            display: none; position: fixed; top: 0; left: 0; 
            width: 100%; height: 100%; background: #222; 
            color: #ff4444; text-align: center; padding-top: 50px; z-index: 9999;
        }
        input[type="password"] { padding: 10px; margin-top: 10px; border-radius: 5px; border: none; }
        button { padding: 10px 20px; background: #ff4444; color: white; border: none; border-radius: 5px; cursor: pointer; }
    </style>
</head>
<body>

    <div id="layar-kunci">
        <h1>🚫 UJIAN TERKUNCI</h1>
        <p>Sistem mendeteksi kamu membuka aplikasi lain.</p>
        <p>Berikan HP ini ke pengawas untuk membuka kunci.</p>
        <br>
        <input type="password" id="passInput" placeholder="Password Pengawas">
        <button onclick="bukaKunci()">Buka Kunci</button>
        <p id="pesan-salah" style="color: yellow; display: none;">Password Salah!</p>
    </div>

    <div id="konten-ujian">
        <h2>Ujian Fisika (Kinematika)</h2>
        <div class="box">
            <p>1. Jika $v(t) = 3t^2 + 2$, tentukan posisi $s(t)$ saat $t=2$ jika $s(0)=0$.</p>
            <input type="text" placeholder="Jawaban kamu...">
        </div>
        <p style="font-size: 12px; color: gray;">Status: <span style="color: green;">Aman (Sedang Diawasi)</span></p>
    </div>

    <script>
        const passwordBenar = "osn2026"; // <-- GANTI PASSWORDNYA DI SINI

        // Fungsi buat deteksi pindah tab/aplikasi
        document.addEventListener("visibilitychange", function() {
            if (document.hidden) {
                // Simpan status terkunci ke memori HP (biar direfresh tetep kunci)
                localStorage.setItem("statusUjian", "terkunci");
                tampilkanLayarKunci();
            }
        });

        function tampilkanLayarKunci() {
            document.getElementById('layar-kunci').style.display = 'block';
            document.getElementById('konten-ujian').style.display = 'none';
        }

        function bukaKunci() {
            const input = document.getElementById('passInput').value;
            if (input === passwordBenar) {
                localStorage.removeItem("statusUjian");
                location.reload();
            } else {
                document.getElementById('pesan-salah').style.display = 'block';
            }
        }

        // Cek pas halaman dibuka, apakah sebelumnya sudah kena lock?
        window.onload = function() {
            if (localStorage.getItem("statusUjian") === "terkunci") {
                tampilkanLayarKunci();
            }
        }
    </script>
</body>
</html>
