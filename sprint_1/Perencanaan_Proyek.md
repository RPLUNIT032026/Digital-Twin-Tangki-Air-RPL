# Perencanaan Proyek

**Perancangan Digital Twin Tangki Air untuk Monitoring Ketinggian dan Kondisi Air Secara Real-Time**

## Daftar Isi

1. Project Charter
2. Product Backlog & Sprint 1 Backlog
3. Perhitungan Function Point – Sprint 1

---

## Bagian 1: Project Charter


### 1. Latar Belakang

Pemantauan tangki air (rumah tangga, gedung, kampus, maupun industri kecil) umumnya masih dilakukan secara manual, yaitu dengan mengecek langsung ke tangki. Cara ini menimbulkan beberapa masalah: air meluap atau habis tanpa disadari, pompa menyala terus atau terlambat menyala, kualitas air menurun (keruh, suhu tidak normal, TDS tinggi) tanpa terdeteksi, serta tidak ada riwayat data yang bisa dianalisis. Diperlukan sistem yang mampu merepresentasikan kondisi tangki fisik secara digital (**digital twin**) dan memantaunya secara real-time agar pengelolaan air lebih efisien, aman, dan terdokumentasi.

### 2. Tujuan

- Membangun representasi digital (digital twin) tangki air yang mencerminkan kondisi tangki fisik secara real-time
- Memantau **ketinggian air** (level dalam cm dan persentase kapasitas)
- Memantau **kondisi air**, dengan parameter yang dibatasi pada tiga hal:
  - Suhu air (°C)
  - Kekeruhan / turbidity (NTU)
  - Kualitas air berdasarkan TDS (ppm)
- Menampilkan data dalam dashboard interaktif (visual tangki, grafik tren, status)
- Memberikan notifikasi otomatis saat kondisi tidak normal (air hampir habis, hampir meluap, kualitas di luar ambang batas)
- Menyimpan riwayat data sensor untuk analisis dan laporan
- Pada tahap pengembangan awal, data sensor menggunakan **data dummy hasil simulasi**, dengan arsitektur yang siap dihubungkan ke sensor nyata

### 3. Keputusan Sprint 1

#### a. Agile Methodology
- Metodologi yang digunakan: **Scrum**
- Durasi sprint: ± 1 bulan per sprint (mengikuti timeline Sp1–Sp5)
- Role tim: 1 orang sebagai **Scrum Master** (Ketua Tim/koordinator), sisanya **Development Team**
- Tools tracking task: **GitHub Projects**
- Artefak Scrum: Product Backlog, Sprint Backlog, dan Increment di akhir tiap sprint

#### b. UX Design
- Antarmuka dirancang dengan wireframe sederhana (Figma/sketsa) sebelum masuk development
- Elemen utama halaman:
  - Dashboard utama: visual tangki (animasi level air), nilai level saat ini, suhu, kekeruhan, TDS, dan indikator status (Normal / Waspada / Bahaya)
  - Grafik tren: level dan kualitas air per jam / hari / minggu
  - Riwayat data: tabel data sensor dengan filter tanggal dan parameter
  - Pengaturan ambang batas: batas minimum/maksimum level dan kualitas air
  - Notifikasi/alert (contoh: banner "Level air 15%, segera isi tangki")
  - Halaman login untuk pengguna dan admin
- Alur pengguna: login → lihat dashboard real-time → cek grafik tren → atur ambang batas → terima notifikasi → tinjau riwayat data

#### c. Project Setup
- Struktur folder awal repository:
  ```
  digital-twin-tangki-air/
  ├── backend/        # API server (Flask/Node.js)
  ├── frontend/       # Dashboard web (HTML/JS/CSS)
  ├── simulator/      # Python sensor simulator (data dummy)
  ├── database/       # Skema, ERD & seed data
  ├── docs/           # Charter, wireframe, FP, dokumentasi API
  └── README.md
  ```
- Tech stack awal: Python Sensor Simulator (data dummy level, suhu, kekeruhan, TDS), Flask/Node.js (backend), HTML/JS + Bootstrap/Tailwind + Chart.js (frontend awal)

### 4. Arsitektur Sistem

#### a. Objek Fisik & Pengguna (Sumber Data)
- **Tangki air fisik:** objek yang direpresentasikan, dengan sensor level (ultrasonik), suhu, kekeruhan, dan TDS
- **Pengguna/Operator:** memantau dashboard, mengatur ambang batas, menerima notifikasi
- **Admin:** mengelola pengguna, sensor/tangki, dan meninjau log sistem

#### b. Sistem Digital Twin (Representasi Digital)
- **Frontend web:** dashboard real-time, visual tangki, grafik, riwayat, pengaturan
- **Backend REST API:** menerima data sensor, autentikasi, pengelolaan tangki, ambang batas, dan notifikasi
- **Database:** menyimpan data sensor, pengguna, konfigurasi tangki, dan log notifikasi
- **Opsi data awal (tanpa perangkat keras):** Python Sensor Simulator yang mengirim data dummy berkala ke API, meniru perilaku sensor nyata (pengisian, pemakaian, fluktuasi kualitas)
- **Rencana integrasi sensor nyata (opsional):** ESP32 + sensor ultrasonik (level), DS18B20 (suhu), sensor turbidity, dan sensor TDS, mengirim data via HTTP/MQTT

#### c. Fitur Tambahan
- Notifikasi otomatis (in-app/email/Telegram/WhatsApp) saat melewati ambang batas
- Prediksi sederhana: estimasi waktu tangki penuh/habis berdasarkan laju perubahan level
- Kontrol pompa (simulasi on/off otomatis berdasarkan level)
- Ekspor riwayat data (CSV/PDF)
- Dukungan lebih dari satu tangki (multi-tank)

#### d. Catatan Risiko
- **Keterbatasan perangkat keras:** sensor dapat tidak akurat atau butuh kalibrasi; pada tahap awal digunakan data dummy dan validasi terhadap sensor nyata dilakukan bila perangkat tersedia
- **Keterlambatan data (latency) & koneksi:** data real-time bergantung pada jaringan; perlu penanganan data hilang dan indikator status koneksi sensor
- **Keamanan data:** autentikasi pengguna, validasi input dari sensor, dan pembatasan akses API
- **Pengelolaan waktu:** tim beranggotakan 3 orang, sehingga ruang lingkup dijaga tetap fokus (tiga parameter kondisi air dan satu jenis tangki pada rilis awal)

### 5. Tech Stack (Rencana Awal)

| Komponen | Teknologi |
|----------|-----------|
| Sumber Data | Python Sensor Simulator / sensor nyata (ESP32) |
| Backend | (isi sesuai kesepakatan tim, contoh: Flask atau Node.js/Express) |
| Database | (contoh: MySQL/PostgreSQL/InfluxDB untuk data time-series) |
| Frontend | HTML + JS + Bootstrap/Tailwind + Chart.js (atau React) |
| Real-time | Polling / WebSocket / MQTT (contoh: Mosquitto) |
| Notifikasi | Email / Telegram Bot API / in-app alert |
| Manajemen Proyek | GitHub & GitHub Projects |
| Komunikasi | HTTP REST API |

### 6. Rencana Sprint

| Sprint | Bulan | Fokus |
|--------|-------|-------|
| Sp1 | September | Project Charter, perhitungan Function Point, backlog, arsitektur & tech stack, ERD, UX wireframe, setup repo & boilerplate |
| Sp2 | October | Backend (autentikasi, API data sensor) + simulator sensor + dashboard real-time dasar (level air) |
| Sp3 | November | Monitoring kondisi air (suhu, kekeruhan, TDS), grafik tren, ambang batas & notifikasi, refinement |
| Sp4 | December | Testing, riwayat & ekspor data, kontrol pompa/prediksi (opsional), upgrade tampilan |
| Sp5 | December | Final testing, bug fixing, dokumentasi, persiapan demo/presentasi akhir |

### 7. Anggota Tim

|              Nama                  |        NIM      |                Peran                       |
|------------------------------------|-----------------|--------------------------------------------|
| Dekna Mutiara Ramadhani            |     240504080   | Ketua Tim / Project Manager (Scrum Master) |
| Nur Aimi Nadia Binti Hanafiah      |     240504077   |       System Analyst & UX Designer         |
| Meisya Amelia Lubis                |     240504088   |        Developer & Database Engineer       |

---

## Bagian 2: Product Backlog & Sprint 1 Backlog


**Proyek:** Perancangan Digital Twin Tangki Air untuk Monitoring Ketinggian dan Kondisi Air Secara Real-Time


### 1. Product Backlog

Prioritas: **Tinggi** = fondasi/inti sistem, **Sedang** = fitur pendukung, **Rendah** = pengembangan lanjutan.
Bobot FP diambil dari perhitungan Function Point Sprint 1 (UFC).

| ID | Fitur | User Story | Jenis FP | Bobot FP | Prioritas | Sprint |
| --- | --- | --- | --- | --- | --- | --- |
| PBI-01 | Konfigurasi tangki | Sebagai operator, saya ingin memasukkan kapasitas, tinggi, dan diameter tangki agar model digital sesuai tangki asli. | EI | 3 | Tinggi | 1 |
| PBI-02 | Input data sensor | Sebagai sistem, saya ingin menerima data ketinggian, suhu, dan kualitas air agar kondisi tangki dapat dipantau. | EI | 4 | Tinggi | 1 |
| PBI-03 | Visualisasi tangki & level air | Sebagai operator, saya ingin melihat gambar tangki dengan level air yang bergerak sesuai data agar kondisi air mudah dipahami. | EO | 5 | Tinggi | 1 |
| PBI-04 | Dashboard status & kualitas air | Sebagai operator, saya ingin melihat ringkasan status dan indikator kualitas air dalam satu halaman. | EO | 5 | Tinggi | 1 |
| PBI-05 | Notifikasi batas kritis / anomali | Sebagai operator, saya ingin mendapat peringatan saat air terlalu rendah, terlalu tinggi, atau kualitas menurun agar dapat segera bertindak. | EO | 4 | Tinggi | 1 |
| PBI-06 | Riwayat data pengukuran | Sebagai operator, saya ingin melihat riwayat pengukuran untuk memantau perubahan dari waktu ke waktu. | EQ | 3 | Sedang | 1 |
| PBI-07 | Pencarian berdasarkan rentang waktu | Sebagai operator, saya ingin menyaring data berdasarkan tanggal/jam agar mudah menemukan data tertentu. | EQ | 4 | Sedang | 1 |
| PBI-08 | Penyimpanan konfigurasi & pengguna | Sebagai sistem, saya ingin menyimpan data konfigurasi tangki dan pengguna agar tidak hilang. | ILF | 7 | Tinggi | 1 |
| PBI-09 | Penyimpanan rekaman data sensor | Sebagai sistem, saya ingin menyimpan setiap rekaman sensor sebagai dasar riwayat dan analisis. | ILF | 10 | Tinggi | 1 |
| PBI-10 | Penyimpanan catatan notifikasi | Sebagai sistem, saya ingin menyimpan log notifikasi agar kejadian anomali dapat ditelusuri. | ILF | 7 | Sedang | 1 |
| PBI-11 | Pengambilan data dari API simulasi sensor | Sebagai sistem, saya ingin mengambil data dari API simulasi agar pengembangan bisa berjalan tanpa sensor fisik. | EIF | 5 | Tinggi | 1 |
| PBI-12 | Login & manajemen peran pengguna | Sebagai admin, saya ingin mengatur akun dan hak akses agar sistem aman. | – | TBD | Sedang | 2 |
| PBI-13 | Grafik tren ketinggian & kualitas air | Sebagai operator, saya ingin melihat grafik tren agar pola perubahan terlihat jelas. | – | TBD | Sedang | 2 |
| PBI-14 | Ekspor laporan (CSV/PDF) | Sebagai operator, saya ingin mengunduh data riwayat sebagai laporan. | – | TBD | Sedang | 2 |
| PBI-15 | Pengaturan ambang batas notifikasi | Sebagai admin, saya ingin mengubah batas kritis sendiri tanpa mengubah kode. | – | TBD | Sedang | 2 |
| PBI-16 | Integrasi sensor fisik (mis. ESP32/MQTT) | Sebagai sistem, saya ingin menerima data dari sensor sungguhan menggantikan simulasi. | – | TBD | Rendah | 3 |
| PBI-17 | Prediksi waktu tangki habis/penuh | Sebagai operator, saya ingin perkiraan kapan tangki kosong/penuh agar bisa merencanakan pengisian. | – | TBD | Rendah | 3 |
| PBI-18 | Visualisasi 3D tangki | Sebagai operator, saya ingin tampilan 3D yang lebih realistis sebagai digital twin. | – | TBD | Rendah | 3 |
| PBI-19 | Pengujian menyeluruh & dokumentasi akhir | Sebagai tim, kami ingin sistem teruji dan terdokumentasi untuk penyerahan proyek. | – | TBD | Tinggi | 3 |

> Sprint 2 dan 3 bersifat rencana awal dan dapat disesuaikan setelah Sprint Review.


### 2. Sprint 1 Backlog

#### Sprint Goal

Menghasilkan versi awal sistem yang dapat menerima data simulasi sensor, menyimpannya, menampilkannya pada visualisasi tangki dan dashboard, serta memberi notifikasi saat kondisi kritis.

#### Ringkasan

| Item | Keterangan |
| --- | --- |
| Jumlah PBI | 11 (PBI-01 s.d. PBI-11) |
| Ukuran fungsional | UFC 57 → **53,01 FP** (VAF 0,93) |
| Total estimasi tugas | 108 jam |
| Durasi sprint | 2 minggu *(asumsi, sesuaikan dengan jadwal tim)* |

#### Daftar Tugas

Urutan tugas mengikuti ketergantungan: database dan simulator dulu, lalu fitur yang memakainya.

| ID Tugas | PBI | Tugas | Estimasi (jam) | Status |
| --- | --- | --- | --- | --- |
| T-01 | PBI-08 | Merancang skema database (konfigurasi, pengguna, sensor, notifikasi) | 4 | To Do |
| T-02 | PBI-08 | Membuat tabel & model konfigurasi tangki dan pengguna | 4 | To Do |
| T-03 | PBI-09 | Membuat tabel rekaman sensor beserta indeks waktu | 4 | To Do |
| T-04 | PBI-10 | Membuat tabel catatan notifikasi | 3 | To Do |
| T-05 | PBI-11 | Membuat API simulasi sensor (ketinggian, suhu, kualitas air) | 8 | To Do |
| T-06 | PBI-11 | Membuat layanan pengambilan data berkala dari API simulasi | 6 | To Do |
| T-07 | PBI-01 | Membuat form konfigurasi tangki dengan validasi | 6 | To Do |
| T-08 | PBI-01 | Menyimpan dan mengubah konfigurasi tangki ke database | 3 | To Do |
| T-09 | PBI-02 | Membuat proses input data sensor dengan validasi | 6 | To Do |
| T-10 | PBI-02 | Menyimpan rekaman sensor ke database | 3 | To Do |
| T-11 | PBI-03 | Membuat model visualisasi tangki | 10 | To Do |
| T-12 | PBI-03 | Menghubungkan level air pada visualisasi dengan data real-time | 6 | To Do |
| T-13 | PBI-04 | Membuat tata letak halaman dashboard | 6 | To Do |
| T-14 | PBI-04 | Membuat indikator kualitas air (suhu dan parameter kualitas) | 6 | To Do |
| T-15 | PBI-05 | Membuat logika ambang batas dan deteksi anomali | 6 | To Do |
| T-16 | PBI-05 | Menampilkan notifikasi di antarmuka dan menyimpannya ke log | 5 | To Do |
| T-17 | PBI-06 | Membuat halaman tabel riwayat pengukuran | 5 | To Do |
| T-18 | PBI-07 | Menambahkan filter rentang waktu pada riwayat | 5 | To Do |
| T-19 | Umum | Pengujian fungsional seluruh fitur Sprint 1 | 8 | To Do |
| T-20 | Umum | Integrasi akhir dan persiapan demo Sprint Review | 4 | To Do |
| | | **TOTAL** | **108** | |

#### Definition of Done

- Fitur berjalan sesuai user story dan lolos pengujian fungsional.
- Data tersimpan dan dapat ditampilkan kembali dengan benar.
- Tidak ada kesalahan kritis (error) yang tersisa pada alur utama.
- Kode tersimpan di repositori bersama.
- Fitur dapat didemokan pada Sprint Review.

#### Catatan

- Kolom penanggung jawab (PIC) belum diisi karena anggota tim belum diketahui; bisa ditambahkan.
- Estimasi jam adalah perkiraan awal dan sebaiknya dikonfirmasi bersama tim pada Sprint Planning.
- Isi Sprint 2 dan 3 adalah usulan; bobot FP-nya baru bisa dihitung setelah fitur dirinci.

---

## Bagian 3: Perhitungan Function Point – Sprint 1


### Daftar Fitur & Perhitungan UFC

| No. | Nama Fungsi | Jenis | Tingkat Kerumitan | Bobot |
| --- | --- | --- | --- | --- |
| 1 | Input data konfigurasi tangki (kapasitas, tinggi, diameter) | EI | Sederhana | 3 |
| 2 | Input data sensor (ketinggian, suhu, kualitas, data simulasi) | EI | Sedang | 4 |
| 3 | Tampilan visualisasi tangki & level air | EO | Sedang | 5 |
| 4 | Dashboard status & indikator kualitas air | EO | Sedang | 5 |
| 5 | Tampilan notifikasi batas kritis / anomali | EO | Sederhana | 4 |
| 6 | Lihat riwayat data pengukuran | EQ | Sederhana | 3 |
| 7 | Cari data berdasarkan rentang waktu | EQ | Sedang | 4 |
| 8 | Simpan data konfigurasi & pengguna | ILF | Sederhana | 7 |
| 9 | Simpan rekaman data sensor | ILF | Sedang | 10 |
| 10 | Simpan catatan notifikasi | ILF | Sederhana | 7 |
| 11 | Ambil data dari simulasi API sensor | EIF | Sederhana | 5 |
| | **TOTAL UFC** | | | **57** |

### Penilaian 14 Faktor Penyesuaian

| No. | Faktor Pengaruh Sistem | Nilai (0–5) |
| --- | --- | --- |
| 1 | Komunikasi data | 2 |
| 2 | Fungsi terdistribusi | 1 |
| 3 | Kinerja | 2 |
| 4 | Konfigurasi perangkat keras | 1 |
| 5 | Tingkat transaksi | 2 |
| 6 | Masukan data pengguna | 2 |
| 7 | Kemudahan efisiensi pengguna | 3 |
| 8 | Pembaruan data langsung | 2 |
| 9 | Kompleksitas pemrosesan | 2 |
| 10 | Penggunaan kembali | 2 |
| 11 | Kemudahan instalasi | 2 |
| 12 | Kemudahan operasi | 3 |
| 13 | Banyaknya perangkat | 1 |
| 14 | Kemudahan perubahan | 3 |
| | **JUMLAH ΣF** | **28** |

**Perhitungan VAF:**

```
VAF = 0,65 + (0,01 × ΣF)
    = 0,65 + (0,01 × 28)
    = 0,65 + 0,28
    = 0,93
```

### Hasil Akhir Function Point

```
FP  = UFC × VAF
    = 57 × 0,93
    = 53,01
```

### Kesimpulan

Ukuran fungsional proyek **Perancangan Digital Twin Tangki Air untuk Monitoring Ketinggian dan Kondisi Air Secara Real-Time** pada tahap Sprint 1 adalah **53,01 Function Point**.

Nilai ini mencerminkan cakupan pekerjaan yang wajar untuk proyek mahasiswa: pemantauan data, visualisasi, notifikasi, penyimpanan riwayat, dan koneksi data simulasi sesuai tujuan dan ruang lingkup yang disepakati.
