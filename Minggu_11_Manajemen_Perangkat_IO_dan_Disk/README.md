# Minggu 11: Manajemen Perangkat I/O, Disk Scheduling & RAID

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Bahan Kajian / Kode:** BK02 / MP-11  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 50 Menit (BT: 2x50', PT: 2x60', M: 2x60')  
**Bobot Penilaian:** 3%  

---

## 1. Kemampuan Akhir yang Direncanakan (Sub-CPMK)
Mahasiswa mampu menganalisis manajemen I/O, penjadwalan disk (*disk scheduling*), dan konfigurasi RAID.

## 2. Kriteria & Indikator Penilaian
- **Kriteria:** Ketepatan perhitungan perpindahan *head* disk dan argumentasi pemilihan level RAID.
- **Indikator:**
  1. Membedakan mekanisme komunikasi CPU–I/O (*Polling*, *Interrupt-driven I/O*, dan *Direct Memory Access* / DMA).
  2. Menghitung total perpindahan silinder (*total head movement*) pada algoritma *Disk Scheduling* (**FCFS**, **SSTF**, dan **SCAN**).
  3. Memilih dan merancang konfigurasi **RAID** (RAID 0, RAID 1, RAID 5, RAID 10) sesuai kebutuhan kinerja, redundansi, dan kapasitas bersih (*usable capacity*).

## 3. Pengalaman Belajar Mahasiswa
Menghitung rute *disk scheduling*; serta merancang konfigurasi RAID untuk server database berdasarkan studi kasus kebutuhan perusahaan.

---

## 4. Daftar Dokumen Mingguan
1. [`Materi.md`](./Materi.md) — Bahan ajar subsistem I/O, *Polling vs Interrupt vs DMA*, algoritma *Disk Scheduling* (FCFS, SSTF, SCAN, C-SCAN), dan tingkatan RAID.
2. [`Praktikum.md`](./Praktikum.md) — Modul latihan analisis penjadwalan disk dan perencanaan konfigurasi RAID.
3. [`Tugas_Praktikum.md`](./Tugas_Praktikum.md) — Panduan laporan latihan *Disk Scheduling* dan arsitektur RAID Minggu 11.
