# Naskah Soal Ujian Tengah Semester (UTS) - Teori & Analisis

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Sifat Ujian:** Tertutup / Open Book (Sesuai Instruksi Dosen)  
**Durasi:** 90 Menit  
**Bobot:** 20% dari Nilai Akhir  

---

## Bagian A: Pilihan Ganda / Isian Singkat Konseptual (30 Poin)

1. **(10 Poin)** Apa fungsi utama sistem operasi sebagai *resource manager*? Jelaskan pula perbedaan antara *Time Multiplexing* dan *Space Multiplexing* beserta contohnya!
2. **(10 Poin)** Sebutkan perbedaan utama antara mode kernel (*kernel mode*) dan mode pengguna (*user mode*)! Mengapa pemisahan mode ini mutlak diperlukan oleh sistem operasi?
3. **(10 Poin)** Apa yang dimaksud dengan *System Call*? Berikan minimal 3 contoh *System Call* pada sistem operasi Linux/UNIX beserta fungsinya!

---

## Bagian B: Studi Kasus / Esai Analisis (70 Poin)

1. **(Manajemen Proses - 20 Poin):**  
   Jelaskan perbedaan antara proses tunggal (*single-threaded process*) dengan *multithreading*. Berikan contoh skenario nyata di mana *multithreading* sangat meningkatkan kinerja dan responsivitas aplikasi, serta jelaskan apa saja sumber daya yang dibagi bersama (*shared*) antar-*thread* dalam satu proses!

2. **(Penjadwalan CPU - 25 Poin):**  
   Diketahui terdapat 4 proses (`P1`, `P2`, `P3`, `P4`) dengan *Burst Time* masing-masing **6, 8, 7, 3** (dalam milidetik). Jika seluruh proses tiba pada waktu yang bersamaan (`T = 0`) dengan urutan kedatangan `P1, P2, P3, P4`, gambarkan *Gantt Chart* serta hitunglah *Turnaround Time* (TAT), *Waiting Time* (WT) tiap proses, dan *Average Waiting Time* (AWT) menggunakan algoritma:
   - a. *First-Come, First-Served (FCFS)*
   - b. *Shortest-Job-First (SJF) Non-preemptive*

3. **(Sinkronisasi & Deadlock - 25 Poin):**  
   Deskripsikan apa yang dimaksud dengan *Race Condition*. Bagaimana cara *Mutex* atau *Semaphore* bekerja untuk mencegah terjadinya *Race Condition* pada *Critical Section*? Selanjutnya, sebutkan 4 kondisi Coffman yang dapat menyebabkan penggunaan *lock* berujung pada *Deadlock*!

---

## Kunci Jawaban & Pedoman Penskoran (Pegangan Dosen)

### Bagian A (30 Poin)
1. **OS sebagai Resource Manager (10 Poin):**
   - Mengelola, mengalokasikan, dan mengoordinasikan sumber daya perangkat keras (CPU, RAM, Disk, I/O) secara adil, efisien, dan aman di antara banyak program/pengguna.
   - *Time Multiplexing*: Pembagian sumber daya berdasarkan giliran waktu (contoh: penjadwalan CPU *time-slicing* antar-proses).
   - *Space Multiplexing*: Pembagian sumber daya berdasarkan partisi ruang/kapasitas (contoh: pembagian kapasitas RAM atau blok disk untuk beberapa proses).
2. **Kernel Mode vs User Mode (10 Poin):**
   - *Kernel Mode* (Supervisor/Privileged Mode): CPU dapat mengeksekusi seluruh instruksi perangkat keras termasuk instruksi *privileged* (kontrol I/O, manajemen MMU/Page Table, interrupt).
   - *User Mode*: Aplikasi berjalan dengan akses terbatas hanya pada ruang alamat memorinya sendiri dan dilarang mengakses hardware secara langsung untuk mencegah program *buggy*/berbahaya merusak OS atau data proses lain.
3. **System Call (10 Poin):**
   - Antarmuka terprogram resmi yang digunakan aplikasi di *User Mode* untuk meminta layanan kernel OS (memicu *trap/software interrupt* ke *Kernel Mode*).
   - Contoh: `fork()` (membuat proses baru), `open()`/`read()`/`write()` (operasi file/I/O), `execve()` (menjalankan program), `kill()` (mengirim sinyal ke proses).

### Bagian B (70 Poin)
1. **Single-Threaded vs Multithreading (20 Poin):**
   - *Single-threaded*: Satu alur eksekusi per proses; jika terblokir oleh operasi I/O, seluruh aplikasi ikut berhenti merespons.
   - *Multithreading*: Satu proses memiliki beberapa *thread* eksekusi independen yang berjalan secara konkuren.
   - *Shared Resources*: Berbagi bagian *Code*, *Data* (variabel global/heap), dan *Open Files*, namun masing-masing *thread* memiliki *Register* dan *Stack* sendiri.
   - Contoh nyata: Web Browser (satu *thread* merender antarmuka UI, *thread* lain mengunduh gambar/data jaringan di latar belakang) atau Web Server yang melayani ribuan *request* klien secara paralel.

2. **Perhitungan Penjadwalan CPU (25 Poin):**
   - Data: `P1 = 6 ms`, `P2 = 8 ms`, `P3 = 7 ms`, `P4 = 3 ms` (tiba pada `T = 0`).
   - **a. FCFS (`P1 -> P2 -> P3 -> P4`):**
     - Gantt Chart: `| P1 (0-6) | P2 (6-14) | P3 (14-21) | P4 (21-24) |`
     - Waiting Time (WT): `P1 = 0 ms`, `P2 = 6 ms`, `P3 = 14 ms`, `P4 = 21 ms`
     - **Average Waiting Time (FCFS)** = `(0 + 6 + 14 + 21) / 4 = 41 / 4 = 10,25 ms`
     - Turnaround Time (TAT): `P1 = 6 ms`, `P2 = 14 ms`, `P3 = 21 ms`, `P4 = 24 ms` (Rata-rata TAT = `65 / 4 = 16,25 ms`).
   - **b. SJF Non-Preemptive (`P4 -> P1 -> P3 -> P2`):**
     - Gantt Chart: `| P4 (0-3) | P1 (3-9) | P3 (9-16) | P2 (16-24) |`
     - Waiting Time (WT): `P4 = 0 ms`, `P1 = 3 ms`, `P3 = 9 ms`, `P2 = 16 ms`
     - **Average Waiting Time (SJF)** = `(0 + 3 + 9 + 16) / 4 = 28 / 4 = 7,00 ms`
     - Turnaround Time (TAT): `P4 = 3 ms`, `P1 = 9 ms`, `P3 = 16 ms`, `P2 = 24 ms` (Rata-rata TAT = `52 / 4 = 13,00 ms`).

3. **Sinkronisasi & Deadlock (25 Poin):**
   - *Race Condition*: Kondisi ketika dua atau lebih proses/thread membaca dan memodifikasi data bersama secara bersamaan sehingga hasil akhirnya bergantung pada urutan *interleaving* eksekusi instruksi.
   - *Cara Kerja Semaphore/Mutex*: Melindungi *Critical Section* melalui operasi atomik `wait(S)` / `acquire()` (mengurangi nilai/mengunci; jika tidak tersedia maka proses menunggu) dan `signal(S)` / `release()` (menaikkan nilai/melepas kunci setelah keluar dari *Critical Section*), sehingga menjamin *Mutual Exclusion*.
   - *4 Kondisi Coffman (Deadlock)*: (1) *Mutual Exclusion*, (2) *Hold and Wait*, (3) *No Preemption*, dan (4) *Circular Wait*.
