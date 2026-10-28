# Minggu 13: Virtualisasi dan Kontainer (Docker)

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Bahan Kajian / Kode:** BK02 / MP-13  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 50 Menit (BT: 2x50', PT: 2x60', M: 2x60')  
**Bobot Penilaian:** 10% (Praktikum & Tahap 1 Proyek Akhir)  

---

## 1. Kemampuan Akhir yang Direncanakan (Sub-CPMK)
Mahasiswa mampu membedakan *virtual machine* dan kontainer serta mengelola *resource* pada Docker.

## 2. Kriteria & Indikator Penilaian
- **Kriteria:** Ketepatan konsep virtualisasi dan keberhasilan konfigurasi *container* beserta pembatasan CPU/RAM.
- **Indikator:**
  1. Membedakan Hypervisor Tipe 1 (*Bare-Metal*), Hypervisor Tipe 2 (*Hosted*), dan Kontainer (*OS-level Virtualization*).
  2. Menjalankan *image* dan *container* Docker (`docker pull`, `docker run`, `docker ps`, `docker stop`, `docker rm`).
  3. Menerapkan pembatasan sumber daya memori (`-m 512m`) dan CPU (`--cpus="0.5"`) pada kontainer.
  4. Membaca dan menganalisis metrik penggunaan sumber daya kontainer secara *real-time* menggunakan `docker stats`.

## 3. Pengalaman Belajar Mahasiswa
Mengelola *image* dan *container* Docker; menjalankan web server Nginx terisolasi; membatasi alokasi *resource* CPU/RAM; serta mendokumentasikan hasil `docker stats`.

---

## 4. Daftar Dokumen Mingguan
1. [`Materi.md`](./Materi.md) — Bahan ajar virtualisasi, Hypervisor Tipe 1 & 2, Virtual Machine vs Kontainer, dan ekosistem Docker.
2. [`Praktikum.md`](./Praktikum.md) — Modul praktikum manajemen sumber daya menggunakan kontainer (Docker).
3. [`Tugas_Praktikum.md`](./Tugas_Praktikum.md) — Tugas laporan praktikum Docker & Rubrik Penilaian Proyek Praktikum Virtualisasi/Docker.
4. [`RTM_Tugas_Besar.md`](./RTM_Tugas_Besar.md) — Panduan Rencana Tugas Mahasiswa (RTM) untuk implementasi multi-container Tugas Besar.
