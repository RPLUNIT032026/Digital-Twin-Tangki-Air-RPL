# Perencanaan Proyek

**Judul:** Digital Twin Tangki Air untuk Monitoring Ketinggian dan Penghentian Pengisian Otomatis

## 1. Project Charter

### Latar Belakang
Pengisian tangki yang dipantau secara manual bisa menyebabkan air meluap. Sistem ini dibuat untuk memantau ketinggian air dan menghentikan pengisian secara otomatis saat air mencapai batas yang ditentukan.

### Tujuan
- Memantau ketinggian air secara real-time.
- Memungkinkan admin mengatur batas maksimum air.
- Membunyikan alarm saat batas tercapai.
- Menghentikan pengisian air secara otomatis.

### Anggota Tim

| Nama | NIM | Peran |
|---|---|---|
| Dekna Mutiara Ramadhani | 240504080 | Ketua Tim |
| Nur Aimi Nadia Binti Hanafiah | 240504077 | Analisis Sistem dan Desain |
| Meisya Amelia Lubis | 240504088 | Pengembangan Sistem dan Database |

## 2. Product Backlog

| ID | Fitur | Keterangan | Prioritas |
|---|---|---|---|
| PBI-01 | Atur batas air | Admin mengatur batas maksimum ketinggian | Tinggi |
| PBI-02 | Baca sensor | Sistem menerima data ketinggian air | Tinggi |
| PBI-03 | Tampilan tangki | Sistem menampilkan ketinggian air | Tinggi |
| PBI-04 | Status air | Sistem menunjukkan apakah batas tercapai | Tinggi |
| PBI-05 | Alarm otomatis | Alarm berbunyi saat batas tercapai | Tinggi |
| PBI-06 | Penghentian otomatis | Pompa berhenti atau katup menutup | Tinggi |
| PBI-07 | Pengujian | Memastikan sensor, alarm, dan penghentian bekerja | Tinggi |

## 3. Perhitungan Function Point

Perhitungan ini merupakan estimasi awal.

### Daftar Fungsi

| No. | Fungsi | Jenis | Bobot |
|---|---|---|---:|
| 1 | Mengatur batas maksimum | EI | 3 |
| 2 | Menerima data sensor | EI | 3 |
| 3 | Menampilkan tangki dan ketinggian | EO | 5 |
| 4 | Menampilkan status air | EO | 4 |
| 5 | Mengaktifkan alarm dan perintah berhenti | EO | 5 |
| 6 | Menyimpan batas maksimum | ILF | 7 |
| 7 | Mengambil data sensor eksternal | EIF | 5 |
| | **Total UFC** | | **32** |

Keterangan: EI = input, EO = output, ILF = penyimpanan data internal, EIF = data dari sumber luar.

### Faktor Penyesuaian

Jumlah nilai 14 faktor penyesuaian diperkirakan **29**.

**VAF = 0,65 + (0,01 × 29) = 0,94**

**FP = UFC × VAF = 32 × 0,94 = 30,08**

Jadi, estimasi ukuran sistem adalah **30,08 Function Point**. Nilai ini dapat berubah setelah sistem selesai dirancang dan diuji.

## Kesimpulan

Sistem ini memantau ketinggian air tangki. Admin menentukan batas maksimum. Ketika air mencapai atau melewati batas tersebut, sensor mengirim data ke sistem, alarm berbunyi, dan pengisian berhenti secara otomatis.
