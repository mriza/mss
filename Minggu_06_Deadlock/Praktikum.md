# Modul Latihan: Analisis Resource Allocation Graph dan Banker's Algorithm

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 6

---

## 1. Tujuan Latihan
Mahasiswa mampu mendeteksi terjadinya *Deadlock* melalui representasi visual *Resource Allocation Graph* (RAG) dan mampu mensimulasikan penghindaran *Deadlock* menggunakan *Banker's Algorithm*.

## 2. Studi Kasus 1: Resource Allocation Graph (RAG)
Diberikan himpunan Proses (P) dan Sumber Daya (R) sebagai berikut:
- Terdapat proses P1, P2, P3.
- Terdapat sumber daya R1 (1 instans), R2 (2 instans), R3 (1 instans).
- Kondisi saat ini:
  - P1 menahan (Hold) R1, dan meminta (Request) R2.
  - P2 menahan salah satu instans R2, menahan R3, dan meminta R1.
  - P3 menahan salah satu instans R2, dan tidak meminta apa-apa.

**Instruksi:**
1. Gambarkan visualisasi dari RAG berdasarkan deskripsi di atas. Gunakan lingkaran untuk Proses dan kotak (berisi titik) untuk Sumber Daya.
2. Analisis graf yang Anda buat: Apakah terdapat siklus (*cycle*) di dalam graf tersebut?
3. Apakah sistem berada dalam keadaan *Deadlock*? Jelaskan alasan Anda secara logis!

---

## 3. Studi Kasus 2: Banker's Algorithm (Penghindaran Deadlock)
Sebuah sistem memiliki 3 jenis sumber daya: **A (Total 10 unit), B (Total 5 unit), dan C (Total 7 unit)**. Terdapat 5 proses (P0 hingga P4). Sistem saat ini berada pada waktu T0 dengan status berikut:

| Proses | Allocation (A B C) | Max Need (A B C) |
|---|---|---|
| P0 | 0 1 0 | 7 5 3 |
| P1 | 2 0 0 | 3 2 2 |
| P2 | 3 0 2 | 9 0 2 |
| P3 | 2 1 1 | 2 2 2 |
| P4 | 0 0 2 | 4 3 3 |

**Instruksi Perhitungan:**
1. Hitung total sumber daya yang sedang dialokasikan (*Total Allocation*) untuk A, B, dan C.
2. Hitung jumlah sumber daya yang saat ini masih tersedia di sistem (**Available = Total System - Total Allocation**).
3. Buatlah matriks **Need** (*Need = Max - Allocation*). Ini adalah sisa sumber daya yang mungkin masih akan diminta oleh masing-masing proses.
4. Simulasikan eksekusi menggunakan algoritma keamanan (*Safety Algorithm*). Cari proses mana yang *Need*-nya lebih kecil atau sama dengan *Available*. Jika ada, asumsikan proses tersebut dieksekusi sampai selesai, dan ia akan mengembalikan seluruh *Allocation*-nya menjadi tambahan *Available*.
5. Tuliskan **Safe Sequence** (urutan eksekusi proses yang aman) sehingga semua proses dapat selesai tanpa terjadi *Deadlock*.

---

## 4. Laporan Praktikum
Tuliskan penyelesaian langkah demi langkah untuk Studi Kasus 1 dan Studi Kasus 2 di atas. Pastikan Anda menunjukkan perhitungan matriks *Available* dan *Need* yang berubah-ubah pada setiap iterasi eksekusi di Studi Kasus 2.
