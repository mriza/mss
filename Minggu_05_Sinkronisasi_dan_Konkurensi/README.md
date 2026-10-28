# Minggu 5: Sinkronisasi dan Konkurensi

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Bahan Kajian / Kode:** BK02 / MP-05  
**Dosen Pengampu:** Melissa Triandini, M.Kom  
**Alokasi Waktu:** 3 x 50 Menit (BT: 2x50', PT: 2x60', M: 2x60')  
**Bobot Penilaian:** 3%  

---

## 1. Kemampuan Akhir yang Direncanakan (Sub-CPMK)
Mahasiswa mampu menganalisis *race condition* dan menerapkan mekanisme sinkronisasi.

## 2. Kriteria & Indikator Penilaian
- **Kriteria:** Ketepatan menemukan *critical section* dan memilih mekanisme sinkronisasi yang sesuai.
- **Indikator:**
  1. Membuktikan terjadinya *Race Condition* melalui tabel urutan eksekusi (*interleaving*) instruksi CPU.
  2. Mengidentifikasi baris kode yang termasuk *Critical Section* beserta 3 syarat penyelesaiannya (*Mutual Exclusion, Progress, Bounded Waiting*).
  3. Menerapkan *Mutex Lock* (`acquire_lock` / `release_lock`) pada pseudocode.
  4. Menjelaskan cara kerja *Binary Semaphore* dan *Counting Semaphore* (`wait` / `signal`).

## 3. Pengalaman Belajar Mahasiswa
Menganalisis kasus transaksi tiket bersamaan; menyusun tabel *interleaving*; serta memodifikasi pseudocode menggunakan *mutex lock* dan *counting semaphore*.

---

## 4. Daftar Dokumen Mingguan
1. [`Materi.md`](./Materi.md) — Bahan ajar konkurensi, *race condition*, *critical section*, *mutex*, dan *semaphore*.
2. [`Praktikum.md`](./Praktikum.md) — Modul praktikum/tugas simulasi *race condition* dan sinkronisasi.
3. [`Tugas_Praktikum.md`](./Tugas_Praktikum.md) — Panduan laporan praktikum dan analisis sinkronisasi Minggu 5.
