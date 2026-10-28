# Minggu 15: Monitoring dan Evaluasi Kinerja Sistem

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Bahan Kajian / Kode:** BK02 / MP-15  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 50 Menit (BT: 2x50', PT: 2x60', M: 2x60')  
**Bobot Penilaian:** 10% (Praktikum Monitoring & Presentasi Tugas Besar)  

---

## 1. Kemampuan Akhir yang Direncanakan (Sub-CPMK)
Mahasiswa mampu memonitor, mengevaluasi, dan memberikan rekomendasi peningkatan kinerja sistem.

## 2. Kriteria & Indikator Penilaian
- **Kriteria:** Ketepatan membaca metrik CPU, memori, I/O, *load average*, mengidentifikasi *bottleneck*, dan memberi rekomendasi peningkatan kapasitas.
- **Indikator:**
  1. Menjelaskan 4 sinyal emas (*Four Golden Signals* Google SRE: *Latency, Traffic, Errors, Saturation*).
  2. Membedakan gejala dan penanganan bottleneck **CPU-Bound**, **Memory-Bound**, dan **I/O-Bound**.
  3. Menggunakan *tools* `top`, `htop`, `iotop`, dan `stress` di Linux serta mengelola prioritas proses dengan `nice` dan `renice`.
  4. Mempresentasikan dan mendemonstrasikan hasil pengujian beban (*Load Testing*) proyek akhir Tugas Besar (*Multi-Container Docker*).

## 3. Pengalaman Belajar Mahasiswa
Melakukan monitoring *real-time* di Linux; menjalankan simulasi beban dengan `stress`; mengidentifikasi *CPU/Memory/I/O bound*; mengatur nilai *niceness* proses; serta mempresentasikan proyek akhir di depan kelas.

---

## 4. Daftar Dokumen Mingguan
1. [`Materi.md`](./Materi.md) — Bahan ajar monitoring kinerja sistem, *The Golden Signals*, investigasi bottleneck (CPU/Memory/I/O Bound), dan evolusi *tools* monitoring.
2. [`Praktikum.md`](./Praktikum.md) — Modul praktikum monitoring & evaluasi kinerja sistem (`htop`, `iotop`, `stress`, `nice`, `renice`).
3. [`Tugas_Praktikum.md`](./Tugas_Praktikum.md) — Tugas praktikum monitoring Minggu 15 serta Panduan & Rubrik Penilaian Tugas Besar (30%).
4. [`Format_Laporan_Tugas_Besar.md`](./Format_Laporan_Tugas_Besar.md) — Format baku penulisan Laporan Tugas Besar (*Final Project*).
