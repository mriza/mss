# Tugas Praktikum Minggu 11: Penjadwalan Disk dan Perencanaan RAID

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 11  
**Bobot Penilaian Pertemuan:** 3%  

---

## 1. Rincian Tugas
Selesaikan kedua studi kasus pada [`Praktikum.md`](./Praktikum.md):
1. **Studi Kasus 1 — Perhitungan Disk Scheduling:**
   - Rute urutan silinder dan perhitungan selisih mutlak (`|next - current|`) mulai dari posisi awal `head = 50` untuk antrian `82, 170, 43, 140, 24, 16, 190` (rentang silinder `0–199`) dengan algoritma:
     - a. **FCFS**
     - b. **SSTF**
     - c. **SCAN** (arah awal menuju `199`)
   - Gambarkan diagram garis pergerakan *head* untuk masing-masing algoritma!
2. **Studi Kasus 2 — Perencanaan Arsitektur RAID Server Database:**
   - Pemilihan level RAID terbaik untuk memenuhi target kecepatan tinggi, *fault-tolerance*, dan kapasitas bersih `2 TB` menggunakan disk `@ 1 TB`.
   - Perhitungan jumlah keping disk fisik yang dibutuhkan.
   - Analisis kelemahan RAID 0 murni dan RAID 1 murni (2 keping) untuk skenario tersebut.

## 2. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan dalam format `.pdf` melalui sistem e-Learning sebelum pertemuan Minggu ke-12.
