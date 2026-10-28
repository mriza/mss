# Naskah Soal Ujian Akhir Semester (UAS) - Teori Komprehensif

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Sifat Ujian:** Tertutup (*Closed Book*)  
**Durasi:** 90 Menit  
**Bobot:** 20% dari Nilai Akhir  

---

## Bagian A: Soal Konsep & Pemahaman Terapan (30 Poin)

1. **(6 Poin)** Jelaskan apa yang dimaksud dengan fenomena **Thrashing** pada sistem Memori Virtual! Apa penyebab utamanya dan bagaimana cara sistem operasi atau administrator mengatasinya?
2. **(6 Poin)** Bandingkan metode alokasi blok disk **Contiguous Allocation**, **Linked Allocation**, dan **Indexed Allocation (i-node)** dari sisi kecepatan akses acak (*random access*) dan masalah fragmentasi!
3. **(6 Poin)** Apa yang dimaksud dengan **Principle of Least Privilege**? Jika sebuah file konfigurasi database `db_config.env` hanya boleh dibaca dan ditulis oleh pemiliknya (*Owner*), sementara *Group* hanya boleh membaca, dan *Others* tidak boleh memiliki akses sama sekali, tuliskan perintah `chmod` (dalam angka oktal) yang tepat!
4. **(6 Poin)** Jelaskan perbedaan fundamental antara **Virtual Machine (Hypervisor)** dan **Container (Docker)** dari sisi arsitektur kernel, konsumsi memori RAM, dan tingkat isolasi keamanan!
5. **(6 Poin)** Dalam memonitor kinerja server di Linux menggunakan `top` atau `htop`, jelaskan perbedaan gejala antara sistem yang mengalami **CPU-Bound** dengan sistem yang mengalami **I/O-Bound** (perhatikan nilai `%us`, `%wa`, dan *Load Average*)!

---

## Bagian B: Studi Kasus & Perhitungan Analitis (70 Poin)

### Soal 1: Simulasi Page Replacement (25 Poin)
Sebuah proses memiliki urutan pemanggilan halaman memori (*Reference String*) sepanjang 12 referensi sebagai berikut:
**`1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5`**

Apabila sistem hanya mengalokasikan **3 Frames** di RAM (awalnya kosong), gambarkan tabel pergerakan *frame* dan hitunglah total **Page Fault** menggunakan algoritma:
- a. **FIFO (First-In, First-Out)**
- b. **LRU (Least Recently Used)**

### Soal 2: Penjadwalan Disk & Perencanaan RAID (25 Poin)
1. **(15 Poin)** Sebuah hardisk memiliki 200 silinder (`0` s.d. `199`). Saat ini posisi *head* berada pada silinder **60** dan sedang bergerak naik menuju **199**. Antrian permintaan silinder adalah: **`95, 180, 34, 119, 11, 123`**. Hitunglah rute urutan layanan dan **Total Head Movement** menggunakan algoritma:
   - **SSTF (Shortest Seek Time First)**
   - **SCAN (Elevator Algorithm)**
2. **(10 Poin)** Sebuah rumah sakit membutuhkan server penyimpanan rekam medis dengan kapasitas bersih (*usable capacity*) **4 TB**. Tersedia kepingan SSD Enterprise masing-masing berukuran **2 TB**. Server wajib memiliki kecepatan baca/tulis tinggi dan tetap beroperasi tanpa kehilangan data meskipun 1 SSD rusak. Pilihlah antara **RAID 0, RAID 1, RAID 5, atau RAID 10**, tentukan jumlah keping SSD yang harus dipasang, dan jelaskan alasannya!

### Soal 3: Arsitektur Cloud, Kontainer & Evaluasi Kinerja (20 Poin)
Sebuah aplikasi *e-Commerce* mengalami lonjakan pengunjung 10 kali lipat saat acara *Flash Sale* tengah malam. Saat ini aplikasi tersebut berjalan di atas 1 mesin virtual tunggal dan sering mengalami *crash* akibat kehabisan memori (*Out of Memory / OOM*).
1. Jelaskan perbedaan pendekatan **Vertical Scaling (Scale Up)** dan **Horizontal Scaling (Scale Out)** untuk mengatasi masalah tersebut! Mengapa *Horizontal Scaling* dengan **Load Balancer** dan **Auto-Scaling** lebih direkomendasikan?
2. Jika aplikasi dipecah menjadi 3 kontainer Docker (*Nginx*, *Backend API*, dan *PostgreSQL*) di dalam `docker-compose.yml`, mengapa kita wajib menerapkan batas `mem_limit` dan `cpus` pada setiap kontainer?

---

## Kunci Jawaban & Pedoman Penskoran (Pegangan Dosen)

### Bagian A (30 Poin)
1. **Thrashing (6 Poin):** Kondisi di mana sistem menghabiskan lebih banyak waktu untuk menukar halaman memori (*swapping/paging in-out*) antara RAM dan Disk dibandingkan mengeksekusi instruksi CPU. Penyebab: Derajat *multiprogramming* terlalu tinggi sedangkan alokasi *frame* RAM fisik tidak mencukupi *working set* proses. Solusi: Mengurangi jumlah proses aktif, mengoptimalkan kode/memori aplikasi, atau menambah kapasitas RAM fisik.
2. **Alokasi Disk (6 Poin):**
   - *Contiguous*: Akses sekuensial & acak sangat cepat, tetapi menderita fragmentasi eksternal parah dan sulit memperbesar ukuran file.
   - *Linked*: Bebas fragmentasi eksternal, tetapi akses acak sangat lambat (harus menelusuri rantai pointer dari awal).
   - *Indexed (i-node)*: Mendukung akses acak cepat tanpa fragmentasi eksternal karena seluruh pointer blok dikumpulkan dalam blok indeks.
3. **Least Privilege & `chmod` (6 Poin):**
   - Memberikan hak akses seminimal mungkin yang diperlukan pengguna/proses untuk menjalankan tugasnya.
   - Owner (`rw-` = `4+2 = 6`), Group (`r--` = `4`), Others (`---` = `0`) -> Perintah: `chmod 640 db_config.env`.
4. **VM vs Kontainer (6 Poin):**
   - VM memvirtualisasi perangkat keras melalui Hypervisor dan menjalankan *Guest OS/Kernel* penuh di tiap VM (ukuran GB, *booting* lambat, konsumsi RAM tinggi, isolasi tingkat hardware sangat kuat).
   - Kontainer (Docker) memvirtualisasi level OS dan berbagi *Kernel Host* yang sama (ukuran MB, *startup* milidetik, hemat RAM, isolasi menggunakan *namespaces* & *cgroups*).
5. **CPU-Bound vs I/O-Bound (6 Poin):**
   - *CPU-Bound*: Utilitas CPU (`%us` / `%sy`) mendekati 100%, *Load Average* tinggi, proses antri di CPU.
   - *I/O-Bound*: Utilitas komputasi CPU (`%us`) rendah, tetapi indikator `%wa` (*I/O Wait*) tinggi dan *Load Average* tetap tinggi karena proses tertahan menunggu operasi baca/tulis disk atau jaringan.

### Bagian B (70 Poin)
1. **Simulasi Page Replacement `1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5` pada 3 Frames (25 Poin):**
   - **a. FIFO:**
     - `1` -> `[1, -, -]` (PF 1)
     - `2` -> `[1, 2, -]` (PF 2)
     - `3` -> `[1, 2, 3]` (PF 3)
     - `4` -> `[4, 2, 3]` (PF 4 - ganti 1)
     - `1` -> `[4, 1, 3]` (PF 5 - ganti 2)
     - `2` -> `[4, 1, 2]` (PF 6 - ganti 3)
     - `5` -> `[5, 1, 2]` (PF 7 - ganti 4)
     - `1` -> `[5, 1, 2]` (Hit)
     - `2` -> `[5, 1, 2]` (Hit)
     - `3` -> `[5, 3, 2]` (PF 8 - ganti 1)
     - `4` -> `[5, 3, 4]` (PF 9 - ganti 2)
     - `5` -> `[5, 3, 4]` (Hit)
     - **Total Page Fault FIFO = 9 Page Faults.**
   - **b. LRU:**
     - `1, 2, 3` -> `[1, 2, 3]` (3 PF)
     - `4` -> `[4, 2, 3]` (PF 4 - ganti 1)
     - `1` -> `[4, 1, 3]` (PF 5 - ganti 2)
     - `2` -> `[4, 1, 2]` (PF 6 - ganti 3)
     - `5` -> `[5, 1, 2]` (PF 7 - ganti 4 karena 4 paling lama tidak diakses)
     - `1` -> Hit
     - `2` -> Hit
     - `3` -> `[3, 1, 2]` (PF 8 - ganti 5 karena 5 paling lama tidak diakses dibanding 1 & 2)
     - `4` -> `[3, 4, 2]` (PF 9 - ganti 1)
     - `5` -> `[3, 4, 5]` (PF 10 - ganti 2)
     - **Total Page Fault LRU = 10 Page Faults.**

2. **Penjadwalan Disk & Perencanaan RAID (25 Poin):**
   - **a. SSTF dari `60` (`95, 180, 34, 119, 11, 123`):**
     - Rute: `60 -> 34 (26) -> 11 (23) -> 95 (84) -> 119 (24) -> 123 (4) -> 180 (57)`
     - **Total Head Movement SSTF** = `26 + 23 + 84 + 24 + 4 + 57 = 218 silinder`.
   - **b. SCAN (Naik menuju `199`) dari `60`:**
     - Rute: `60 -> 95 (35) -> 119 (24) -> 123 (4) -> 180 (57) -> 199 (19) -> 34 (165) -> 11 (23)`
     - **Total Head Movement SCAN** = `(199 - 60) + (199 - 11) = 139 + 188 = 327 silinder`.
   - **c. Perencanaan RAID (4 TB Usable dari keping 2 TB):**
     - **Opsi 1 (RAID 10):** Menggunakan **4 keping SSD @ 2 TB** (total fisik 8 TB, kapasitas bersih 4 TB). Memberikan performa baca/tulis tertinggi (*striping*) sekaligus redundansi *mirroring* instan tanpa overhead komputasi parity.
     - **Opsi 2 (RAID 5):** Menggunakan **3 keping SSD @ 2 TB** (total fisik 6 TB, `(N-1) * 2 TB = 4 TB` kapasitas bersih) dengan *distributed parity*. (Kedua jawaban diterima penuh bila perhitungan jumlah disk dan argumen teknisnya tepat).

3. **Arsitektur Cloud & Pembatasan Kontainer (20 Poin):**
   - *Vertical Scaling* menambah CPU/RAM pada 1 server (terbatas plafon hardware, ada *downtime* dan *Single Point of Failure*). *Horizontal Scaling* menambah jumlah *instance* server di belakang *Load Balancer* secara elastis (*Auto-Scaling* saat *Flash Sale* dan *Scale-In* saat trafik normal) tanpa *downtime*.
   - Penerapan `mem_limit` dan `cpus` mencegah *Noisy Neighbor* — misalnya jika kontainer *Backend API* mengalami lonjakan memori atau *infinite loop*, ia tidak akan menghabiskan seluruh RAM *Host* dan mematikan kontainer *PostgreSQL* atau *Nginx*.
