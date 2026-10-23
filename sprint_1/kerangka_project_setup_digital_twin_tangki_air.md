# 3. Inisialisasi Kode Proyek (Project Setup)

## 1. Struktur Folder Proyek

Buat repository GitHub dengan nama `digital-twin-tangki-air`, kemudian
siapkan struktur berikut:

``` text
digital-twin-tangki-air/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── script.js
├── README.md
└── .gitignore
```

## 2. Kode Program Setiap File

### File 1 --- `index.html`

File utama untuk menampilkan tangki dan informasi ketinggian air.

``` html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Twin Tangki Air</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <h1>Monitoring Ketinggian Air Tangki</h1>
        <p>Simulasi Digital Twin Tangki Air</p>
    </header>

    <main class="container">
        <section class="tank-section">
            <h2>Visualisasi Tangki</h2>

            <div class="tank">
                <div id="water" class="water"></div>
            </div>

            <p>Ketinggian Air: <strong id="height">0 cm</strong></p>
            <p>Kapasitas Terisi: <strong id="percentage">0%</strong></p>
        </section>

        <section class="control-section">
            <h2>Kontrol Simulasi</h2>

            <label for="waterLevel">Atur Ketinggian Air (cm)</label>
            <input
                type="range"
                id="waterLevel"
                min="0"
                max="100"
                value="50"
            >

            <p>Status Air: <strong id="status">Normal</strong></p>
            <p id="warning">Kondisi air normal.</p>
        </section>
    </main>

    <footer>
        <p>Proyek Informatika - Digital Twin Tangki Air</p>
    </footer>

    <script src="js/script.js"></script>
</body>
</html>
```

### File 2 --- `css/style.css`

File untuk mengatur tampilan tangki dan visualisasi air.

``` css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    background-color: #f0f5f9;
    color: #243447;
}

header {
    background-color: #1565c0;
    color: white;
    text-align: center;
    padding: 25px 10px;
}

header h1 {
    margin-bottom: 8px;
}

.container {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-wrap: wrap;
    gap: 40px;
    padding: 30px 15px;
}

.tank-section,
.control-section {
    background-color: white;
    padding: 25px;
    border-radius: 12px;
    width: 280px;
    text-align: center;
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
}

.tank {
    width: 140px;
    height: 260px;
    border: 4px solid #455a64;
    border-radius: 12px 12px 25px 25px;
    margin: 20px auto;
    position: relative;
    overflow: hidden;
    background-color: #eaf4f8;
}

.water {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 50%;
    background-color: #29b6f6;
    transition: height 0.3s ease;
}

input[type="range"] {
    width: 100%;
    margin: 20px 0;
    cursor: pointer;
}

#status {
    color: #16803c;
}

#warning {
    font-size: 14px;
}

footer {
    text-align: center;
    padding: 15px;
    color: #526273;
}
```

### File 3 --- `js/script.js`

File untuk menghitung persentase air dan menentukan status ketinggian
air.

``` javascript
const waterLevel = document.getElementById("waterLevel");
const water = document.getElementById("water");
const heightText = document.getElementById("height");
const percentageText = document.getElementById("percentage");
const statusText = document.getElementById("status");
const warningText = document.getElementById("warning");

const MAX_HEIGHT = 100;

function updateWaterLevel() {
    const height = Number(waterLevel.value);
    const percentage = (height / MAX_HEIGHT) * 100;

    water.style.height = percentage + "%";
    heightText.textContent = height + " cm";
    percentageText.textContent = percentage + "%";

    if (height < 20) {
        statusText.textContent = "Rendah";
        statusText.style.color = "#d97706";
        warningText.textContent = "Peringatan: Ketinggian air rendah.";
    } else if (height >= 80) {
        statusText.textContent = "Tinggi";
        statusText.style.color = "#dc2626";
        warningText.textContent = "Peringatan: Air hampir penuh.";
    } else {
        statusText.textContent = "Normal";
        statusText.style.color = "#16803c";
        warningText.textContent = "Kondisi air normal.";
    }
}

waterLevel.addEventListener("input", updateWaterLevel);

updateWaterLevel();
```

### File 4 --- `README.md`

Dokumentasi proyek yang ditampilkan di halaman utama repository GitHub.

``` markdown
# Digital Twin Tangki Air

## Deskripsi Proyek
Proyek ini merupakan kerangka awal sistem monitoring
ketinggian air tangki menggunakan konsep Digital Twin.
Sistem menampilkan simulasi visual ketinggian air dan
memberikan informasi status air berdasarkan ketinggiannya.

## Tujuan
- Memantau ketinggian air tangki.
- Menampilkan visualisasi ketinggian air.
- Menghitung persentase kapasitas air.
- Memberikan peringatan ketika air rendah atau hampir penuh.

## Teknologi
- HTML
- CSS
- JavaScript

## Struktur Folder
- index.html: halaman utama.
- css/style.css: tampilan sistem.
- js/script.js: logika monitoring air.
- README.md: dokumentasi proyek.
- .gitignore: daftar file yang diabaikan Git.

## Cara Menjalankan
1. Unduh atau clone repository.
2. Buka file index.html melalui browser.
3. Geser pengatur ketinggian air.
4. Amati perubahan visual tangki, persentase, dan status air.

## Batasan Sistem
Data ketinggian air pada versi ini masih berupa simulasi.
Sistem belum terhubung dengan sensor atau perangkat IoT.

## Status
Project setup dan simulasi awal telah dibuat.
```

### File 5 --- `.gitignore`

``` gitignore
.vscode/
.idea/
*.log
*.tmp
.DS_Store
Thumbs.db
```

## 3. Cara Kerja Kerangka Proyek

1.  **Input ketinggian air:** Pengguna mengatur simulasi ketinggian air
    pada rentang 0--100 cm.
2.  **JavaScript:** Sistem menghitung ketinggian, persentase kapasitas,
    dan status air berdasarkan input.
3.  **Visualisasi Digital Twin:** Tampilan tangki berubah mengikuti
    input dan sistem menampilkan peringatan sesuai status air.

## 4. Hasil yang Diharapkan

Setelah seluruh file dimasukkan ke GitHub dan `index.html` dibuka di
browser, sistem akan menampilkan:

-   Visual tangki dengan air yang bisa naik dan turun.
-   Ketinggian air dalam satuan sentimeter.
-   Persentase kapasitas air.
-   Status rendah, normal, atau tinggi.
-   Peringatan saat ketinggian air rendah atau hampir penuh.

**Catatan untuk laporan:** Kerangka ini merupakan dasar simulasi awal,
tetapi belum menjadi sistem Digital Twin yang terhubung ke kondisi
tangki nyata. Jika proyek mengharuskan sensor ultrasonik,
mikrokontroler, atau database, komponen tersebut perlu ditambahkan pada
tahap pengembangan berikutnya.
