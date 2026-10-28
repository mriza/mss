# Mata Kuliah: Manajemen Sumberdaya Sistem

**Kode Mata Kuliah:** MKK56301501  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer - Politeknik Pertanian Negeri Payakumbuh  
**Semester / SKS:** Semester 5 / 2 SKS (Belajar Terbimbing: 2 x 50' Tatap Muka/Lab, Penugasan Terstruktur: 2 x 60', Belajar Mandiri: 2 x 60' per Minggu — Total 5.440 Menit per Semester)  
**Dosen Pengampu:**  
- **M. Riza Nurtam, M.Kom** (Penanggung Jawab Mata Kuliah — Pengampu Minggu 9 s.d. 16)  
- **Melissa Triandini, M.Kom** (Anggota Pengampu — Pengampu Minggu 1 s.d. 8)  

---

## Deskripsi Mata Kuliah

Mata kuliah ini membahas prinsip-prinsip dasar sistem operasi dalam mengelola sumber daya perangkat keras dan perangkat lunak (CPU, memori utama, memori virtual, penyimpanan, perangkat I/O, dan keamanan), serta praktik manajemen sumber daya sistem modern meliputi virtualisasi kontainer (Docker), arsitektur komputasi awan (*Cloud Computing*), dan pemantauan kinerja (*System Monitoring & Capacity Planning*).

---

## Dokumen Utama Mata Kuliah (Folder Utama)

1. **Kurikulum & Silabus:** [`Kurikulum_Manajemen_Sumberdaya_Sistem.md`](./Kurikulum_Manajemen_Sumberdaya_Sistem.md) | [`Kurikulum_Manajemen_Sumberdaya_Sistem.odt`](./Kurikulum_Manajemen_Sumberdaya_Sistem.odt)
2. **Rencana Pembelajaran Semester (RPS):** [`RPS Manajemen Sumberdaya Sistem 2026.docx`](./RPS%20Manajemen%20Sumberdaya%20Sistem%202026.docx) | [`RPS_Manajemen_Sumberdaya_Sistem.md`](./RPS_Manajemen_Sumberdaya_Sistem.md) | [`RPS_Manajemen_Sumberdaya_Sistem.odt`](./RPS_Manajemen_Sumberdaya_Sistem.odt)
3. **Distribusi Tugas Dosen:** [`Distribusi Tugas Manajemen Sumberdaya Sistem 2026.docx`](./Distribusi%20Tugas%20Manajemen%20Sumberdaya%20Sistem%202026.docx) | [`Distribusi Tugas Manajemen Sumberdaya Sistem 2026.pdf`](./Distribusi%20Tugas%20Manajemen%20Sumberdaya%20Sistem%202026.pdf)
4. **Kontrak Perkuliahan:** [`Kontrak_Perkuliahan.md`](./Kontrak_Perkuliahan.md) | [`Kontrak_Perkuliahan.odt`](./Kontrak_Perkuliahan.odt)
5. **Format Laporan Praktikum:** [`Format_Laporan_Praktikum.md`](./Format_Laporan_Praktikum.md) | [`Format_Laporan_Praktikum.odt`](./Format_Laporan_Praktikum.odt)
6. **Buku Referensi Utama (PDF):**
   - Silberschatz, A., Galvin, P. B., & Gagne, G. (2019). *Operating System Concepts* (10th Global Edition). Wiley.
   - Tanenbaum, A. S., & Bos, H. (2022). *Modern Operating Systems* (5th Edition). Pearson.
   - Nemeth, E., Snyder, G., Hein, T. R., Whaley, B., & Mackin, D. (2017). *UNIX and Linux System Administration Handbook* (5th Edition). Pearson.

---

## Distribusi Kegiatan Perkuliahan Per Minggu (Minggu 1 – 16)

| Minggu | Kode BK/MP | Topik Pembelajaran | Kegiatan Belajar & Metode | Dosen Pengampu | Bobot | Folder Mingguan |
| :---: | :---: | :--- | :--- | :--- | :---: | :--- |
| **1** | BK02/MP-01 | Pengantar Sistem Operasi & Manajemen Sumber Daya | Kuliah, diskusi kasus *memory leak*, persiapan VM Linux | Melissa Triandini, M.Kom | 2% | [`Minggu_01_Pengantar_OS_dan_Manajemen_Sumber_Daya`](./Minggu_01_Pengantar_OS_dan_Manajemen_Sumber_Daya/) |
| **2** | BK02/MP-02 | Struktur Sistem Komputer dan Sistem Operasi | Kuliah, analisis *interrupt* & *system call*, eksplorasi CLI | Melissa Triandini, M.Kom | 2% | [`Minggu_02_Struktur_Sistem_Komputer_dan_OS`](./Minggu_02_Struktur_Sistem_Komputer_dan_OS/) |
| **3** | BK02/MP-03 | Manajemen Proses dan Thread | Kuliah & Praktikum (`ps`, `pstree`, `kill`, `jobs`, `fg`, `bg`) | Melissa Triandini, M.Kom | 3% | [`Minggu_03_Manajemen_Proses_dan_Thread`](./Minggu_03_Manajemen_Proses_dan_Thread/) |
| **4** | BK02/MP-04 | Penjadwalan CPU (FCFS, SJF, Round Robin) | Kuliah & Latihan perhitungan *Gantt Chart*, TAT, WT | Melissa Triandini, M.Kom | 3% | [`Minggu_04_Penjadwalan_CPU`](./Minggu_04_Penjadwalan_CPU/) |
| **5** | BK02/MP-05 | Sinkronisasi dan Konkurensi | Kuliah & Praktikum simulasi *Race Condition*, *Mutex*, *Semaphore* | Melissa Triandini, M.Kom | 3% | [`Minggu_05_Sinkronisasi_dan_Konkurensi`](./Minggu_05_Sinkronisasi_dan_Konkurensi/) |
| **6** | BK02/MP-06 | Deadlock | Kuliah & Latihan *Resource Allocation Graph* & *Banker's Algorithm* | Melissa Triandini, M.Kom | 3% | [`Minggu_06_Deadlock`](./Minggu_06_Deadlock/) |
| **7** | BK02/MP-07 | Manajemen Memori Utama | Kuliah & Latihan *First/Best/Worst-Fit* & Translasi *Paging* | Melissa Triandini, M.Kom | 3% | [`Minggu_07_Manajemen_Memori_Utama`](./Minggu_07_Manajemen_Memori_Utama/) |
| **8** | BK02/MP-08 | **Ujian Tengah Semester (UTS)** | Evaluasi Teori & Studi Kasus Materi Minggu 1–7 | Tim Dosen | **20%** | [`Minggu_08_UTS`](./Minggu_08_UTS/) |
| **9** | BK02/MP-09 | Memori Virtual | Kuliah & Latihan simulasi *Page Replacement* (FIFO, LRU, Optimal) | M. Riza Nurtam, M.Kom | 3% | [`Minggu_09_Memori_Virtual`](./Minggu_09_Memori_Virtual/) |
| **10** | BK02/MP-10 | Manajemen Penyimpanan dan Sistem File | Kuliah & Praktikum navigasi sistem file Linux & *disk space* (`df`, `du`) | M. Riza Nurtam, M.Kom | 3% | [`Minggu_10_Manajemen_Penyimpanan_dan_Sistem_File`](./Minggu_10_Manajemen_Penyimpanan_dan_Sistem_File/) |
| **11** | BK02/MP-11 | Manajemen Perangkat I/O dan Disk | Kuliah & Latihan *Disk Scheduling* (FCFS, SSTF, SCAN) & desain RAID | M. Riza Nurtam, M.Kom | 3% | [`Minggu_11_Manajemen_Perangkat_IO_dan_Disk`](./Minggu_11_Manajemen_Perangkat_IO_dan_Disk/) |
| **12** | BK02/MP-12 | Keamanan dan Proteksi Sistem | Kuliah & Praktikum *File Permissions* (`chmod`, `chown`) & peluncuran Tugas Besar | M. Riza Nurtam, M.Kom | 2% | [`Minggu_12_Keamanan_dan_Proteksi_Sistem`](./Minggu_12_Keamanan_dan_Proteksi_Sistem/) |
| **13** | BK02/MP-13 | Virtualisasi dan Kontainer (Docker) | Kuliah, Praktikum Docker *resource limit* (`--cpus`, `-m`) & Proyek Akhir | M. Riza Nurtam, M.Kom | 10% | [`Minggu_13_Virtualisasi_dan_Kontainer`](./Minggu_13_Virtualisasi_dan_Kontainer/) |
| **14** | BK02/MP-14 | Manajemen Sumber Daya Cloud & Skalabilitas | Kuliah & Proyek perancangan arsitektur *Load Balancing* & *Auto-Scaling* | M. Riza Nurtam, M.Kom | 10% | [`Minggu_14_Manajemen_Sumber_Daya_Cloud_dan_Skalabilitas`](./Minggu_14_Manajemen_Sumber_Daya_Cloud_dan_Skalabilitas/) |
| **15** | BK02/MP-15 | Monitoring dan Evaluasi Kinerja Sistem | Kuliah, Praktikum (`htop`, `iotop`, `stress`, `nice`/`renice`) & Presentasi Tugas Besar | M. Riza Nurtam, M.Kom | 10% | [`Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem`](./Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem/) |
| **16** | BK02/MP-16 | **Ujian Akhir Semester (UAS)** | Evaluasi Komprehensif Materi Minggu 9–15 | Tim Dosen | **20%** | [`Minggu_16_UAS`](./Minggu_16_UAS/) |

---

## Struktur Direktori Repositori

```text
Manajemen Sumberdaya Sistem/
├── README.md
├── Kurikulum_Manajemen_Sumberdaya_Sistem.md / .odt
├── RPS Manajemen Sumberdaya Sistem 2026.docx
├── RPS_Manajemen_Sumberdaya_Sistem.md / .odt
├── Distribusi Tugas Manajemen Sumberdaya Sistem 2026.docx / .pdf
├── Kontrak_Perkuliahan.md / .odt
├── Format_Laporan_Praktikum.md / .odt
├── [Buku Referensi Utama .pdf]
├── Minggu_01_Pengantar_OS_dan_Manajemen_Sumber_Daya/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_02_Struktur_Sistem_Komputer_dan_OS/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_03_Manajemen_Proses_dan_Thread/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_04_Penjadwalan_CPU/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_05_Sinkronisasi_dan_Konkurensi/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_06_Deadlock/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_07_Manajemen_Memori_Utama/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_08_UTS/
│   ├── README.md
│   ├── Soal_UTS_Teori.md
│   └── Soal_UTS_Praktik.md
├── Minggu_09_Memori_Virtual/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_10_Manajemen_Penyimpanan_dan_Sistem_File/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_11_Manajemen_Perangkat_IO_dan_Disk/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_12_Keamanan_dan_Proteksi_Sistem/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   ├── Tugas_Praktikum.md
│   └── RTM_Tugas_Besar.md
├── Minggu_13_Virtualisasi_dan_Kontainer/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   ├── Tugas_Praktikum.md
│   └── RTM_Tugas_Besar.md
├── Minggu_14_Manajemen_Sumber_Daya_Cloud_dan_Skalabilitas/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   └── Tugas_Praktikum.md
├── Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem/
│   ├── README.md
│   ├── Materi.md
│   ├── Praktikum.md
│   ├── Tugas_Praktikum.md
│   └── Format_Laporan_Tugas_Besar.md
└── Minggu_16_UAS/
    ├── README.md
    ├── Soal_UAS_Teori.md
    └── Soal_UAS_Praktik.md
```

---

## Navigasi Cepat Kegiatan Per Minggu

| Minggu | Topik Utama | Materi Kuliah | Modul Praktikum / Latihan | Tugas / Evaluasi |
| :---: | :--- | :---: | :---: | :---: |
| **I** | Pengantar OS & Manajemen Sumber Daya | [Materi.md](./Minggu_01_Pengantar_OS_dan_Manajemen_Sumber_Daya/Materi.md) | [Praktikum.md](./Minggu_01_Pengantar_OS_dan_Manajemen_Sumber_Daya/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_01_Pengantar_OS_dan_Manajemen_Sumber_Daya/Tugas_Praktikum.md) |
| **II** | Struktur Sistem Komputer dan OS | [Materi.md](./Minggu_02_Struktur_Sistem_Komputer_dan_OS/Materi.md) | [Praktikum.md](./Minggu_02_Struktur_Sistem_Komputer_dan_OS/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_02_Struktur_Sistem_Komputer_dan_OS/Tugas_Praktikum.md) |
| **III** | Manajemen Proses dan Thread | [Materi.md](./Minggu_03_Manajemen_Proses_dan_Thread/Materi.md) | [Praktikum.md](./Minggu_03_Manajemen_Proses_dan_Thread/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_03_Manajemen_Proses_dan_Thread/Tugas_Praktikum.md) |
| **IV** | Penjadwalan CPU (FCFS, SJF, RR) | [Materi.md](./Minggu_04_Penjadwalan_CPU/Materi.md) | [Praktikum.md](./Minggu_04_Penjadwalan_CPU/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_04_Penjadwalan_CPU/Tugas_Praktikum.md) |
| **V** | Sinkronisasi dan Konkurensi | [Materi.md](./Minggu_05_Sinkronisasi_dan_Konkurensi/Materi.md) | [Praktikum.md](./Minggu_05_Sinkronisasi_dan_Konkurensi/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_05_Sinkronisasi_dan_Konkurensi/Tugas_Praktikum.md) |
| **VI** | Deadlock (RAG & Banker's Algorithm) | [Materi.md](./Minggu_06_Deadlock/Materi.md) | [Praktikum.md](./Minggu_06_Deadlock/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_06_Deadlock/Tugas_Praktikum.md) |
| **VII** | Manajemen Memori Utama (Fit & Paging) | [Materi.md](./Minggu_07_Manajemen_Memori_Utama/Materi.md) | [Praktikum.md](./Minggu_07_Manajemen_Memori_Utama/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_07_Manajemen_Memori_Utama/Tugas_Praktikum.md) |
| **VIII** | Ujian Tengah Semester (UTS) | [README.md](./Minggu_08_UTS/README.md) | [Soal_UTS_Praktik.md](./Minggu_08_UTS/Soal_UTS_Praktik.md) | [Soal_UTS_Teori.md](./Minggu_08_UTS/Soal_UTS_Teori.md) |
| **IX** | Memori Virtual (Demand Paging, FIFO, LRU) | [Materi.md](./Minggu_09_Memori_Virtual/Materi.md) | [Praktikum.md](./Minggu_09_Memori_Virtual/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_09_Memori_Virtual/Tugas_Praktikum.md) |
| **X** | Manajemen Penyimpanan dan Sistem File | [Materi.md](./Minggu_10_Manajemen_Penyimpanan_dan_Sistem_File/Materi.md) | [Praktikum.md](./Minggu_10_Manajemen_Penyimpanan_dan_Sistem_File/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_10_Manajemen_Penyimpanan_dan_Sistem_File/Tugas_Praktikum.md) |
| **XI** | Manajemen Perangkat I/O, Disk & RAID | [Materi.md](./Minggu_11_Manajemen_Perangkat_IO_dan_Disk/Materi.md) | [Praktikum.md](./Minggu_11_Manajemen_Perangkat_IO_dan_Disk/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_11_Manajemen_Perangkat_IO_dan_Disk/Tugas_Praktikum.md) |
| **XII** | Keamanan dan Proteksi Sistem | [Materi.md](./Minggu_12_Keamanan_dan_Proteksi_Sistem/Materi.md) | [Praktikum.md](./Minggu_12_Keamanan_dan_Proteksi_Sistem/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_12_Keamanan_dan_Proteksi_Sistem/Tugas_Praktikum.md) |
| **XIII** | Virtualisasi dan Kontainer (Docker) | [Materi.md](./Minggu_13_Virtualisasi_dan_Kontainer/Materi.md) | [Praktikum.md](./Minggu_13_Virtualisasi_dan_Kontainer/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_13_Virtualisasi_dan_Kontainer/Tugas_Praktikum.md) |
| **XIV** | Manajemen Sumber Daya Cloud & Skalabilitas | [Materi.md](./Minggu_14_Manajemen_Sumber_Daya_Cloud_dan_Skalabilitas/Materi.md) | [Praktikum.md](./Minggu_14_Manajemen_Sumber_Daya_Cloud_dan_Skalabilitas/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_14_Manajemen_Sumber_Daya_Cloud_dan_Skalabilitas/Tugas_Praktikum.md) |
| **XV** | Monitoring dan Evaluasi Kinerja Sistem | [Materi.md](./Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem/Materi.md) | [Praktikum.md](./Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem/Praktikum.md) | [Tugas_Praktikum.md](./Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem/Tugas_Praktikum.md) |
| **XVI** | Ujian Akhir Semester (UAS) | [README.md](./Minggu_16_UAS/README.md) | [Soal_UAS_Praktik.md](./Minggu_16_UAS/Soal_UAS_Praktik.md) | [Soal_UAS_Teori.md](./Minggu_16_UAS/Soal_UAS_Teori.md) |
