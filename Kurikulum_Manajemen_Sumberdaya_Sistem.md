# Kurikulum Mata Kuliah: Manajemen Sumberdaya Sistem

**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer  
**Perguruan Tinggi:** Politeknik Pertanian Negeri Payakumbuh  
**Tahun Kurikulum:** Kurikulum OBE 2024  

---

## 1. Identitas Mata Kuliah

- **Nama Mata Kuliah:** Manajemen Sumberdaya Sistem
- **Kode Mata Kuliah:** MKK56301501
- **Satuan Kredit Semester (SKS):** 2 SKS
- **Semester:** 5 (Lima)
- **Alokasi Waktu per Minggu:** 
  - Belajar Terbimbing (BT): 2 x 50 menit (100 menit tatap muka/praktikum laboratorium)
  - Penugasan Terstruktur (PT): 2 x 60 menit (120 menit)
  - Belajar Mandiri (M): 2 x 60 menit (120 menit)
  - *Total Beban Waktu:* 340 menit/minggu (Total 16 minggu = 5.440 menit ~ 2 SKS sesuai SN-Dikti & standar Politeknik)
- **Mata Kuliah Prasyarat:** MKK56301102 – ORGANISASI DAN ARSITEKTUR KOMPUTER
- **Rumpun Bahan Kajian (BK):** BK02 – Computer Architecture
- **Dosen Pengampu:**
  1. **M. Riza Nurtam, M.Kom** (Penanggung Jawab Mata Kuliah — NIP. 197910232008121002)
  2. **Melissa Triandini, M.Kom** (Anggota Pengampu)
- **Koordinator Program Studi TRK:** Rina Novita, S.Pd., M.Kom (NIP. 199011062022032011)

---

## 2. Deskripsi Mata Kuliah

Mata kuliah **Manajemen Sumberdaya Sistem** membahas prinsip-prinsip dasar sistem operasi dalam mengelola sumber daya perangkat keras (*hardware*) dan perangkat lunak (*software*), serta praktik manajemen sumber daya sistem secara lebih luas pada infrastruktur komputasi modern. Mata kuliah ini menggabungkan fondasi teoritis arsitektur sistem operasi (*Operating System Internals*) dengan keterampilan terapan administrasi sistem Linux, virtualisasi kontainer (Docker), arsitektur komputasi awan (*Cloud Computing*), dan pemantauan serta rekayasa kinerja (*System Performance & Capacity Planning*).

Kurikulum dirancang selaras dengan standar internasional **ACM/IEEE-CS Computer Science Curricula** (area *OS - Operating Systems*) dan **Information Technology Curricula** (area *System Administration & Cloud Infrastructure*), serta diintegrasikan dengan kerangka *Outcome-Based Education* (OBE) TRK Politani Payakumbuh.

---

## 3. Capaian Pembelajaran Lulusan (CPL Prodi) yang Dibebankan

Mata kuliah ini mendukung pencapaian profil lulusan TRK melalui dua CPL utama:
- **CPL-7:** Mampu menggunakan dan memanfaatkan semua sumber daya teknik, keterampilan dan teknologi perekayasaan modern yang diperlukan dan menangani keterbatasan, serta prediksi dan pemodelan untuk memecahkan masalah rekayasa yang didefinisikan secara luas.
- **CPL-8:** Mampu mengetahui, memilih, merencanakan, serta mengelola basis data yang relevan dalam melakukan eksperimen dan menerapkan pengetahuan komputasi yang diperlukan untuk menganalisa dan merancang perangkat, sistem tertanam ataupun sistem terintegrasi.

---

## 4. Capaian Pembelajaran Mata Kuliah (CPMK / Tujuan Belajar)

Ditransformasikan ke dalam 7 Tujuan Belajar (TB) terukur:
- **TB01 (CPMK 1):** Memahami peran dan tujuan utama sistem operasi sebagai manajer sumber daya (*Resource Manager*).
- **TB02 (CPMK 2):** Menganalisis mekanisme manajemen proses, konkurensi, penjadwalan CPU, dan mitigasi *deadlock*.
- **TB03 (CPMK 3):** Mengevaluasi strategi manajemen memori utama (*RAM allocation*, *paging*) dan memori virtual (*demand paging*, *page replacement*).
- **TB04 (CPMK 4):** Menerapkan konsep manajemen penyimpanan (*block storage*), hierarki sistem file (*virtual file system*), dan subsistem I/O (*disk scheduling*, RAID).
- **TB05 (CPMK 5):** Memahami dan mengimplementasikan konsep virtualisasi (Hypervisor) dan kontainerisasi (Docker) serta komputasi awan (*Cloud Computing*) sebagai bentuk manajemen sumber daya modern yang elastis dan berkeandalan tinggi (*High Availability*).
- **TB06 (CPMK 6):** Melakukan pemantauan (*monitoring*), evaluasi kinerja (*performance evaluation*), identifikasi *bottleneck*, dan perencanaan kapasitas (*capacity planning*) pada sistem operasi server.
- **TB07 (CPMK 7):** Menerapkan prinsip-prinsip keamanan dan proteksi (*Principle of Least Privilege*, kontrol akses DAC/ACL, mitigasi ancaman) pada sumber daya sistem komputer.

---

## 5. Pemetaan Bahan Kajian (BK) dan Topik ACM Curricula

| Kode Bahan Kajian | Topik Pembelajaran | Kaitan ACM / IEEE Curricula | Minggu Ke- |
| :---: | :--- | :--- | :---: |
| **BK02/MP-01** | Pengantar Sistem Operasi & Manajemen Sumber Daya Komputasi | `OS/Overview of Operating Systems` | 1 |
| **BK02/MP-02** | Struktur Sistem Komputer, Dual-Mode, Interupsi, dan System Calls | `OS/Operating System Principles` | 2 |
| **BK02/MP-03** | Manajemen Proses, Thread, Siklus Hidup, dan PCB | `OS/Concurrency & Scheduling` | 3 |
| **BK02/MP-04** | Penjadwalan CPU (FCFS, SJF, Round Robin, Multilevel Queue) | `OS/CPU Scheduling` | 4 |
| **BK02/MP-05** | Sinkronisasi dan Konkurensi (Race Condition, Mutex, Semaphore) | `OS/Concurrency & Synchronization` | 5 |
| **BK02/MP-06** | Deadlock: Karakterisasi Coffman, RAG, Banker's Algorithm | `OS/Deadlock Management` | 6 |
| **BK02/MP-07** | Manajemen Memori Utama: Swapping, Partitioning, Paging, Segmentasi | `OS/Memory Management` | 7 |
| **BK02/MP-08** | **Ujian Tengah Semester (UTS)** | Evaluasi Teori & Praktik Tengah Semester | 8 |
| **BK02/MP-09** | Memori Virtual: Demand Paging, Page Fault, FIFO, LRU, Thrashing | `OS/Virtual Memory` | 9 |
| **BK02/MP-10** | Manajemen Penyimpanan dan Sistem File (VFS, Inode, Directory Tree) | `OS/File Systems & Storage` | 10 |
| **BK02/MP-11** | Manajemen Perangkat I/O, Disk Scheduling, dan Arsitektur RAID | `OS/Device Management & Storage` | 11 |
| **BK02/MP-12** | Keamanan dan Proteksi Sistem: Access Matrix, File Permissions, PoLP | `OS/Security and Protection` | 12 |
| **BK02/MP-13** | Virtualisasi & Kontainer: Hypervisor, Docker, Cgroups & Namespaces | `IT/Virtualization & Cloud` | 13 |
| **BK02/MP-14** | Manajemen Sumber Daya Cloud: IaaS, PaaS, Load Balancing, Auto-Scaling | `IT/Cloud Infrastructure` | 14 |
| **BK02/MP-15** | Monitoring & Evaluasi Kinerja Sistem: USE Method, htop, tuning | `IT/System Administration` | 15 |
| **BK02/MP-16** | **Ujian Akhir Semester (UAS)** | Evaluasi Komprehensif Akhir Semester | 16 |

---

## 6. Sistem Penilaian dan Evaluasi OBE

Sesuai dengan pedoman akademik Politeknik Pertanian Negeri Payakumbuh dan RPS resmi 2026:

| No | Komponen Evaluasi | Bobot (%) | Keterangan |
| :---: | :--- | :---: | :--- |
| 1 | **Kehadiran dan Keaktifan** | **5%** | Presensi minimal 80%, kedisiplinan, partisipasi diskusi kelas |
| 2 | **Kuis dan Tugas Mandiri** | **10%** | Penugasan analitis dan pemecahan studi kasus mandiri |
| 3 | **Praktikum (Laporan Mingguan)** | **15%** | Laporan berkala modul lab Linux sesuai format baku |
| 4 | **Tugas Besar (Proyek Akhir)** | **30%** | Proyek perancangan & penerapan multi-kontainer Docker, monitoring, dan stress test (rubrik 5 sub-kriteria) |
| 5 | **Ujian Tengah Semester (UTS)** | **20%** | Ujian teori dan praktik materi Minggu 1 s.d. 7 |
| 6 | **Ujian Akhir Semester (UAS)** | **20%** | Ujian teori komprehensif dan praktik materi Minggu 9 s.d. 15 |
| **Total** | | **100%** | |

### Konversi Nilai Standar Politan:
- **A** : 80,00 – 100 (Nilai Mutu: 4,00 / Sangat Baik)
- **AB**: 75,00 – 79,99 (Nilai Mutu: 3,50 / Baik Sekali)
- **B** : 70,00 – 74,99 (Nilai Mutu: 3,00 / Baik)
- **BC**: 65,00 – 69,99 (Nilai Mutu: 2,50 / Cukup Baik)
- **C** : 60,00 – 64,99 (Nilai Mutu: 2,00 / Cukup)
- **D** : 50,00 – 59,99 (Nilai Mutu: 1,00 / Kurang)
- **E** : < 50,00 (Nilai Mutu: 0,00 / Gagal - Mengulang)

---

## 7. Buku Referensi Utama

Semua materi kuliah dan laboratorium merujuk langsung pada buku teks berstandar internasional yang tersedia dalam repositori ini:

1. **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons. ISBN: 978-1-119-45408-3.
2. **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson Education. ISBN: 978-0-137-61879-8.
3. **Nemeth, E., Snyder, G., Hein, T. R., Whaley, B., & Mackin, D. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson Education. ISBN: 978-0-134-27755-4.
4. **ACM/IEEE-CS. (2013).** *Computer Science Curricula 2013: Curriculum Guidelines for Undergraduate Degree Programs in Computer Science*.
5. **ACM/IEEE-CS. (2020).** *Computing Curricula 2020 (CC2020): Paradigms for Future Computing Curricula*.
