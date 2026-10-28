# Rencana Pembelajaran Semester (RPS)

**POLITEKNIK PERTANIAN NEGERI PAYAKUMBUH**  
**JURUSAN REKAYASA PERTANIAN DAN KOMPUTER**  
**PROGRAM STUDI TEKNOLOGI REKAYASA KOMPUTER (TRK)**  

---

## 1. Identitas Mata Kuliah

| Komponen | Keterangan |
| :--- | :--- |
| **Nama Mata Kuliah** | **Manajemen Sumberdaya Sistem** |
| **Kode Mata Kuliah** | **MKK56301501** |
| **Satuan Kredit Semester (SKS)** | **2 SKS** (2 x 50 menit Tatap Muka/Lab, 2 x 60 menit Terstruktur, 2 x 60 menit Mandiri per minggu) |
| **Semester / Tahun** | Semester 5 (Lima) / Kurikulum OBE 2024 |
| **Tanggal Penyusunan / Revisi** | 19 Agustus 2026 / Rev. 0 |
| **Bahan Kajian (BK)** | BK02 – Computer Architecture |
| **Mata Kuliah Prasyarat** | MKK56301102 – Organisasi dan Arsitektur Komputer |
| **Penanggung Jawab Mata Kuliah** | **M. Riza Nurtam, M.Kom** (NIP. 197910232008121002) — Pengampu Minggu 9 s.d. 16 |
| **Anggota Pengampu** | **Melissa Triandini, M.Kom** — Pengampu Minggu 1 s.d. 8 |
| **Koordinator Program Studi TRK** | **Rina Novita, S.Pd., M.Kom** (NIP. 199011062022032011) |

---

## 2. Capaian Pembelajaran (CP)

### Capaian Pembelajaran Lulusan (CPL Prodi – Kurikulum OBE 2024)
- **CPL-7:** Mampu menggunakan dan memanfaatkan semua sumber daya teknik, keterampilan dan teknologi perekayasaan modern yang diperlukan dan menangani keterbatasan, serta prediksi dan pemodelan untuk memecahkan masalah rekayasa yang didefinisikan secara luas.
- **CPL-8:** Mampu mengetahui, memilih, merencanakan, serta mengelola basis data yang relevan dalam melakukan eksperimen dan menerapkan pengetahuan komputasi yang diperlukan untuk menganalisa dan merancang perangkat, sistem tertanam ataupun sistem terintegrasi.

### Tujuan Belajar / Capaian Pembelajaran Mata Kuliah (CPMK)
- **TB01:** Memahami peran dan tujuan utama sistem operasi sebagai manajer sumber daya (*Resource Manager*).
- **TB02:** Menganalisis mekanisme manajemen proses, konkurensi, penjadwalan CPU, dan mitigasi *deadlock*.
- **TB03:** Mengevaluasi strategi manajemen memori utama (*contiguous allocation*, *paging*) dan memori virtual (*demand paging*, *page replacement*).
- **TB04:** Menerapkan konsep manajemen penyimpanan (*storage*), hierarki sistem file (*virtual file system*), dan subsistem I/O (*disk scheduling*, RAID).
- **TB05:** Memahami dan mengimplementasikan konsep virtualisasi dan kontainerisasi (Docker) serta komputasi awan (*Cloud Computing*) sebagai bentuk manajemen sumber daya modern yang elastis.
- **TB06:** Melakukan pemantauan (*monitoring*), evaluasi kinerja sistem (*performance evaluation*), identifikasi *bottleneck*, dan perencanaan kapasitas (*capacity planning*).
- **TB07:** Menerapkan prinsip-prinsip keamanan dan proteksi (*Principle of Least Privilege*, file permissions) pada sumber daya sistem operasi.

---

## 3. Deskripsi Singkat Mata Kuliah

Mata kuliah ini membahas prinsip-prinsip dasar sistem operasi dalam mengelola sumber daya perangkat keras dan perangkat lunak, serta praktik manajemen sumber daya sistem secara lebih luas pada lingkungan server modern (virtualisasi, kontainer, komputasi awan, dan manajemen kinerja). Mata kuliah menggabungkan fondasi teoritis sistem operasi (*Operating System Internals*) dengan keterampilan terapan dalam administrasi sistem operasi Linux, konfigurasi kontainer Docker, perencanaan arsitektur cloud berkeandalan tinggi (*High Availability*), dan monitoring kinerja sistem.

---

## 4. Matriks Rencana Pembelajaran Semester (16 Pertemuan)

| Minggu | Sub-CPMK / KAD | Bahan Kajian (Materi Pokok) | Bentuk & Metode Pembelajaran | Estimasi Waktu (Menit) | Pengalaman Belajar Mahasiswa | Kriteria & Indikator Penilaian | Dosen Pengampu | Bobot |
| :---: | :--- | :--- | :--- | :---: | :--- | :--- | :---: | :---: |
| **1** | Mampu menjelaskan definisi OS, fungsi OS sebagai *resource manager*, dan jenis sumber daya komputasi. | **BK02/MP-01**: Pengantar Sistem Operasi & Manajemen Sumber Daya (Hardware/Software, Time & Space Multiplexing). | Kuliah, SCL kontekstual, ceramah interaktif, diskusi kasus *memory leak*. | BT: 100'<br>PT: 120'<br>M: 120' | Mempelajari kontrak/RPS; mendiskusikan peran OS; menganalisis memory leak; menyiapkan VM Linux. | Ketepatan menjelaskan peran OS; mengidentifikasi CPU, RAM, disk, I/O; membedakan time & space multiplexing. | Melissa Triandini, M.Kom | **2%** |
| **2** | Mampu menganalisis struktur sistem komputer dan arsitektur dasar sistem operasi. | **BK02/MP-02**: Struktur Sistem Komputer dan OS (Interrupt, Dual-Mode User/Kernel, System Calls, Trap). | Kuliah, SCL problem-based, tanya jawab, demonstrasi CLI. | BT: 100'<br>PT: 120'<br>M: 120' | Menganalisis alur eksekusi instruksi; alur interrupt hardware; mengeksplorasi hardware lewat CLI Linux (`lscpu`, `free`, `strace`). | Ketepatan menjelaskan hubungan CPU, memori, I/O, interrupt cycle, dual-mode, dan penelusuran system call. | Melissa Triandini, M.Kom | **2%** |
| **3** | Mampu membedakan proses dan thread serta menganalisis siklus hidup proses. | **BK02/MP-03**: Manajemen Proses dan Thread (State, PCB, Context Switch, Thread Models, Multiprocessing). | Kuliah & Praktikum, SCL case-based, praktik CLI Linux. | BT: 100'<br>PT: 120'<br>M: 120' | Praktik menampilkan proses (`ps aux`, `pstree`); membaca PID/PPID; menghentikan proses (`kill`); mengelola jobs (`fg`, `bg`). | Ketepatan membedakan proses vs thread; menyusun diagram status proses; mengelola proses foreground/background di Linux. | Melissa Triandini, M.Kom | **3%** |
| **4** | Mampu menghitung dan mengevaluasi algoritma penjadwalan CPU. | **BK02/MP-04**: Penjadwalan CPU (Kriteria CPU Scheduling, FCFS, SJF Preemptive/Non-preemptive, Round Robin, Multilevel Queue). | Kuliah & Latihan Soal, problem-based, studi kasus numerik. | BT: 100'<br>PT: 120'<br>M: 120' | Menggambar Gantt Chart; menghitung CT, TAT, WT, dan AWT; menganalisis *Convoy Effect* dan pengaruh *Time Quantum*. | Ketepatan prosedur hitung, kebenaran Gantt Chart, akurasi nilai TAT & WT, serta argumentasi pemilihan algoritma. | Melissa Triandini, M.Kom | **3%** |
| **5** | Mampu menganalisis race condition dan menerapkan mekanisme sinkronisasi. | **BK02/MP-05**: Sinkronisasi dan Konkurensi (Critical Section Problem, Race Condition, Mutex Lock, Counting Semaphore). | Kuliah & Praktikum, case-based, simulasi logika interleaving. | BT: 100'<br>PT: 120'<br>M: 120' | Menganalisis transaksi data bersamaan; menyusun tabel interleaving; memperbaiki pseudocode transaksi dengan Mutex/Semaphore. | Ketepatan menemukan Critical Section; membuktikan race condition melalui interleaving; menerapkan lock & semaphore. | Melissa Triandini, M.Kom | **3%** |
| **6** | Mampu mendeteksi, menghindari, dan menjelaskan strategi penanganan deadlock. | **BK02/MP-06**: Deadlock (4 Kondisi Coffman, RAG, Banker's Algorithm - Safety & Resource Request, Deteksi & Pemulihan). | Kuliah & Latihan, problem-based, studi kasus matriks sumber daya. | BT: 100'<br>PT: 120'<br>M: 120' | Menggambar RAG; menganalisis cycle deadlock; menghitung matriks Need & Available; menentukan *Safe Sequence*. | Ketepatan analisis kondisi deadlock; akurasi operasi matriks Banker's Algorithm; penentuan Safe Sequence yang valid. | Melissa Triandini, M.Kom | **3%** |
| **7** | Mampu menganalisis strategi alokasi memori utama dan translasi alamat paging. | **BK02/MP-07**: Manajemen Memori Utama (Address Binding, Swapping, First/Best/Worst Fit, Fragmentasi, Paging, TLB, Segmentasi). | Kuliah & Latihan, problem-based, simulasi translasi alamat. | BT: 100'<br>PT: 120'<br>M: 120' | Mensimulasikan contiguous allocation; menghitung sisa fragmentasi; melakukan kalkulasi translasi alamat logika ke fisik (Page to Frame). | Ketepatan pemilihan blok First/Best/Worst Fit; perhitungan fragmentasi eksternal/internal; translasi alamat paging. | Melissa Triandini, M.Kom | **3%** |
| **8** | **Evaluasi Tengah Semester** | **BK02/MP-08: Ujian Tengah Semester (UTS)** | Tes Tulis Teori Analitis & Praktik Mandiri di Laboratorium. | 90' Ujian (BT: 100', PT: 120', M: 120') | Mengerjakan soal teori konsep dan menyelesaikan skenario praktik manajemen proses & translasi memori. | Penguasaan komprehensif konsep dan kemampuan pemecahan studi kasus materi Minggu 1 s.d. 7. | Tim Dosen | **20%** |
| **9** | Mampu menjelaskan mekanisme virtual memory dan mengevaluasi page replacement. | **BK02/MP-09**: Memori Virtual (Demand Paging, Page Fault Handling, FIFO, LRU, Optimal, Belady's Anomaly, Thrashing). | Kuliah & Latihan, case-based, simulasi tabel frame. | BT: 100'<br>PT: 120'<br>M: 120' | Menyusun tabel frame; menghitung total page fault; membandingkan efisiensi algoritma; menganalisis gejala thrashing. | Ketepatan menyusun pergerakan frame; akurasi jumlah Page Fault FIFO/LRU/Optimal; pemahaman penyebab thrashing. | M. Riza Nurtam, M.Kom | **3%** |
| **10** | Mampu mengelola sistem file dan menganalisis struktur penyimpanan. | **BK02/MP-10**: Manajemen Penyimpanan & Sistem File (Struktur Direktori Tree, VFS, Inode, Alokasi Blok Disk, Free Space). | Kuliah & Praktikum CLI Linux, SCL kontekstual. | BT: 100'<br>PT: 120'<br>M: 120' | Praktik navigasi CLI Linux; membuat direktori bertingkat; manipulasi file (`cp`, `mv`, `rm`); analisis disk space (`df -h`, `du -sh`). | Ketepatan penggunaan perintah CLI; pembedaan absolute vs relative path; pemahaman struktur inode dan alokasi blok disk. | M. Riza Nurtam, M.Kom | **3%** |
| **11** | Mampu menganalisis manajemen I/O, penjadwalan disk, dan konfigurasi RAID. | **BK02/MP-11**: Manajemen Perangkat I/O dan Disk (Polling vs Interrupt vs DMA, Disk Scheduling FCFS/SSTF/SCAN, RAID 0/1/5/6/10). | Kuliah & Latihan Desain, problem-based, studi kasus storage server. | BT: 100'<br>PT: 120'<br>M: 120' | Menghitung rute head movement disk scheduling; merancang arsitektur RAID (kapasitas bersih, redundansi, dan performa). | Ketepatan kalkulasi perpindahan head disk; akurasi perhitungan kapasitas efektif RAID; rasionalitas pemilihan level RAID. | M. Riza Nurtam, M.Kom | **3%** |
| **12** | Mampu menerapkan konsep proteksi dan keamanan sumber daya sistem. | **BK02/MP-12**: Keamanan & Proteksi Sistem (Access Matrix, DAC/ACL Linux, File Permissions rwx/oktal, SUID/SGID, Peluncuran Tugas Besar). | Kuliah & Praktikum, case-based, analisis kerentanan izin file. | BT: 100'<br>PT: 120'<br>M: 120' | Praktik inspeksi hak akses (`ls -l`); modifikasi izin (`chmod`) dan kepemilikan (`chown`); penerapan *Principle of Least Privilege*; pembentukan kelompok Proyek Akhir. | Ketepatan membaca izin rwx; konversi notasi simbolik ke oktal; ketepatan pemilihan izin aman; pemahaman prinsip least privilege. | M. Riza Nurtam, M.Kom | **2%** |
| **13** | Mampu membedakan VM dan kontainer serta mengelola resource pada Docker. | **BK02/MP-13**: Virtualisasi dan Kontainer (Hypervisor Type 1/2 vs Docker, Namespaces & Cgroups, Limitasi CPU `--cpus` & RAM `-m`). | Kuliah & Praktikum Proyek, project-based, instalasi & konfigurasi Docker. | BT: 100'<br>PT: 120'<br>M: 120' | Mengelola Docker image & container; menjalankan Nginx; menerapkan batasan memori dan CPU; inspeksi metrik via `docker stats`. | Ketepatan membedakan VM vs Container; keberhasilan konfigurasi batas resource memori & CPU; pembacaan output `docker stats`. | M. Riza Nurtam, M.Kom | **10%** *(bagian proyek)* |
| **14** | Mampu merancang alokasi sumber daya cloud yang skalabel dan berkeandalan tinggi. | **BK02/MP-14**: Manajemen Sumber Daya Cloud & Skalabilitas (IaaS/PaaS, Horizontal vs Vertical Scaling, Load Balancing, Auto-Scaling, HA). | Kuliah & Desain Arsitektur Cloud, project/case-based. | BT: 100'<br>PT: 120'<br>M: 120' | Merancang diagram arsitektur cloud multi-tier (Load Balancer, Web Server autoscaled, Database cluster Master-Slave); analisis spike traffic. | Kesesuaian rancangan arsitektur dengan prinsip load balancing, auto-scaling thresholds, dan pemisahan lapisan database stateful. | M. Riza Nurtam, M.Kom | **10%** *(bagian proyek)* |
| **15** | Mampu memonitor, mengevaluasi, dan memberikan rekomendasi peningkatan kinerja sistem. | **BK02/MP-15**: Monitoring & Evaluasi Kinerja Sistem (USE Method, top, htop, iotop, stress test, nice/renice, Presentasi Proyek Akhir). | Kuliah & Praktikum Stress Test, project-based, presentasi akhir. | BT: 100'<br>PT: 120'<br>M: 120' | Melakukan monitoring real-time; simulasi beban CPU (`stress`); analisis CPU-Bound vs I/O-Bound; tuning prioritas `renice`; mempresentasikan Tugas Besar. | Ketepatan membaca metrik CPU/Memori/IO/Load Average; identifikasi bottleneck; tuning prioritas proses; kualitas presentasi proyek. | M. Riza Nurtam, M.Kom | **10%** *(bagian proyek)* |
| **16** | **Evaluasi Akhir Semester** | **BK02/MP-16: Ujian Akhir Semester (UAS)** | Tes Tulis Teori Komprehensif & Ujian Praktik Laboratorium. | 90' Ujian (BT: 100', PT: 120', M: 120') | Mengerjakan UAS komprehensif yang menguji integrasi materi memori virtual, storage, keamanan, kontainer, cloud, dan evaluasi kinerja. | Ketepatan dan kedalaman analisis studi kasus komprehensif, serta keberhasilan eksekusi tugas praktik laboratorium. | Tim Dosen | **20%** |
| **Total** | | | | **5.440'** | | | | **100%** |

---

## 5. Rubrik Penilaian Tugas Besar / Proyek Akhir (Bobot: 30%)

Tugas Besar merupakan proyek integratif manajemen sumber daya sistem (*multi-container Docker with resource limits, load testing, and performance monitoring*).

| No | Komponen Evaluasi Proyek Akhir | Bobot (%) | Deskripsi Indikator Penilaian |
| :---: | :--- | :---: | :--- |
| 1 | **Analisis Kebutuhan & Perumusan Masalah Sumber Daya** | **5%** | Kemampuan merumuskan latar belakang skenario, mengidentifikasi potensi bottleneck sumber daya, dan menetapkan target kapasitas sistem. |
| 2 | **Desain Arsitektur Solusi & Alokasi Sumber Daya** | **7%** | Ketepatan diagram topologi arsitektur sistem (pemisahan Web, Backend API, Database) dan rasionalitas penetapan limit CPU (`cpus`) serta RAM (`mem_limit`). |
| 3 | **Implementasi & Keberfungsian Solusi (`docker-compose`)** | **8%** | Keberhasilan konfigurasi file `docker-compose.yml`, orkestrasi multi-kontainer, keterhubungan antar-layanan (*network isolation*), dan persistensi data (*volumes*). |
| 4 | **Pengujian Beban, Monitoring, & Analisis Kinerja** | **5%** | Pelaksanaan uji beban (*load/stress testing* dengan alat seperti Apache Benchmark/Locust), pencatatan metrik `docker stats`/`htop`, dan analisis perilaku throttling/OOM. |
| 5 | **Dokumentasi, Presentasi, Komunikasi, & Kolaborasi** | **5%** | Kerapian naskah laporan teknis (sesuai format baku), kejelasan demonstrasi sistem langsung, penguasaan materi saat tanya jawab, dan keterbukaan deklarasi AI. |
| **Total** | **Bobot Kumulatif Proyek Akhir** | **30%** | |

---

## 6. Komponen Penilaian dan Konversi Nilai Huruf Mutu

### Komponen Evaluasi Terintegrasi:
1. Kehadiran dan Keaktifan Kelas : **5%**
2. Kuis dan Tugas Mandiri : **10%**
3. Praktikum (Laporan Mingguan) : **15%**
4. Tugas Besar (Proyek Akhir) : **30%**
5. Ujian Tengah Semester (UTS) : **20%**
6. Ujian Akhir Semester (UAS) : **20%**
- **Total Nilai Akhir : 100%**

### Standar Konversi Nilai:
- **A**  (4,00) : 80,00 – 100,00 (Sangat Baik)
- **AB** (3,50) : 75,00 – 79,99 (Baik Sekali)
- **B**  (3,00) : 70,00 – 74,99 (Baik)
- **BC** (2,50) : 65,00 – 69,99 (Cukup Baik)
- **C**  (2,00) : 60,00 – 64,99 (Cukup)
- **D**  (1,00) : 50,00 – 59,99 (Kurang - Ujian Ulang/Mengulang)
- **E**  (0,00) : < 50,00 (Gagal - Wajib Mengulang)

---

## 7. Referensi Pustaka Resmi

1. **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons.
2. **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson Education.
3. **Nemeth, E., Snyder, G., Hein, T. R., Whaley, B., & Mackin, D. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson Education.
4. **ACM/IEEE-CS. (2013).** *Computer Science Curricula 2013: Curriculum Guidelines for Undergraduate Degree Programs in Computer Science*.
5. **ACM/IEEE-CS. (2020).** *Computing Curricula 2020 (CC2020): Paradigms for Future Computing Curricula*.
