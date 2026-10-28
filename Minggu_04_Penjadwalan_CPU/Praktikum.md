# Modul Latihan: Analisis dan Perhitungan Algoritma Penjadwalan CPU

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 4

---

## 1. Tujuan Latihan
Mahasiswa mampu secara mandiri menghitung dan membuat *Gantt Chart* untuk menganalisis metrik *Turnaround Time (TAT)* dan *Waiting Time (WT)* dari berbagai algoritma penjadwalan CPU.

## 2. Definisi Penting
- **Arrival Time (AT):** Waktu kedatangan sebuah proses ke dalam sistem.
- **Burst Time (BT):** Lama waktu yang dibutuhkan proses untuk dieksekusi oleh CPU.
- **Completion Time (CT):** Waktu saat proses selesai dieksekusi.
- **Turnaround Time (TAT) = CT - AT:** Total durasi proses sejak datang hingga selesai.
- **Waiting Time (WT) = TAT - BT:** Durasi proses berada dalam antrian tanpa dieksekusi.

---

## 3. Studi Kasus 1: First-Come, First-Served (FCFS)
Diberikan himpunan proses berikut yang tiba pada waktu `AT = 0` dengan urutan kedatangan P1, P2, P3.
| Proses | Burst Time (ms) |
|---|---|
| P1 | 24 |
| P2 | 3 |
| P3 | 3 |

**Instruksi:**
1. Gambarkan *Gantt Chart* dari urutan eksekusi FCFS di atas.
2. Hitung *Waiting Time* masing-masing proses. (P1 menunggu 0ms, P2 menunggu P1 selesai, dsb).
3. Hitung *Average Waiting Time* (Rata-rata waktu tunggu).
4. Bagaimana jika urutan kedatangannya dibalik menjadi P2, P3, P1? Hitung kembali *Average Waiting Time*-nya. Apa kesimpulan yang bisa Anda ambil dari fenomena ini? (*Hint: Convoy Effect*).

---

## 4. Studi Kasus 2: Shortest Job First (SJF) - Non-Preemptive
Diberikan tabel proses dengan waktu kedatangan (*Arrival Time*) yang berbeda-beda:
| Proses | Arrival Time | Burst Time |
|---|---|---|
| P1 | 0 | 7 |
| P2 | 2 | 4 |
| P3 | 4 | 1 |
| P4 | 5 | 4 |

**Instruksi:**
1. Pada waktu `T=0`, hanya P1 yang tiba. Sehingga P1 pasti dieksekusi lebih dulu. Karena *Non-Preemptive*, P1 tidak bisa dihentikan hingga selesai (T=7).
2. Pada `T=7`, periksa siapa saja yang sudah tiba dan ada di antrian *Ready*. Pilih yang *Burst Time*-nya paling kecil.
3. Gambarkan *Gantt Chart* lengkapnya.
4. Hitung TAT dan WT untuk seluruh proses.

---

## 5. Studi Kasus 3: Round Robin (RR)
Gunakan proses berikut yang tiba secara bersamaan pada `AT = 0`, dengan urutan P1, P2, P3.
- **Time Quantum (q) = 4 milidetik**

| Proses | Burst Time |
|---|---|
| P1 | 24 |
| P2 | 3 |
| P3 | 3 |

**Instruksi:**
1. Gambarkan *Gantt Chart*. (P1 masuk, dieksekusi 4ms, lalu diputus. P2 dieksekusi 3ms dan selesai. P3 dieksekusi 3ms dan selesai. P1 masuk lagi...).
2. Hitung *Turnaround Time* untuk masing-masing proses.
3. Hitung *Waiting Time* untuk masing-masing proses.

---

## 6. Laporan Praktikum
Buatlah penyelesaian dari ketiga studi kasus di atas dengan rapi (tabel dan *Gantt Chart* bisa dibuat secara manual di kertas lalu di-*scan* / difoto jelas, atau digambar menggunakan Excel/Word). Kumpulkan melalui *Learning Management System* / e-Learning kampus sesuai tenggat waktu yang disepakati.
