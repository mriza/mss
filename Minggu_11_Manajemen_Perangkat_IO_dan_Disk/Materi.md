# Bahan Ajar: Minggu 11 - Manajemen Perangkat I/O, Disk, dan Konfigurasi RAID

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer – Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan:** 11 (Sebelas) — Semester 5 / 2 SKS  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Bahan Kajian:** BK02/MP-11  

---

## 1. Capaian Pembelajaran (Sub-CPMK) & Indikator

Pada akhir sesi perkuliahan ini, mahasiswa diharapkan mampu:
1. **Mengklasifikasikan perangkat I/O** (*Block Devices* vs *Character Devices*) serta membandingkan 3 metode transfer data: *Polling*, *Interrupt-Driven I/O*, dan *Direct Memory Access* (DMA).
2. **Menjelaskan fungsi subsistem I/O kernel**: *I/O Scheduling*, *Buffering*, *Caching*, dan *Spooling*.
3. **Menganalisis komponen waktu akses disk magnetik**: *Seek Time*, *Rotational Latency*, dan *Transfer Time*.
4. **Menghitung dan membandingkan total perpindahan lengan (*Total Head Movement*)** pada algoritma *Disk Scheduling*: FCFS, SSTF, SCAN, dan C-SCAN.
5. **Mengevaluasi arsitektur penyimpanan redundan (RAID)**: memahami mekanisme *Striping*, *Mirroring*, dan *Parity*.
6. **Merancang konfigurasi RAID (RAID 0, 1, 5, 6, dan 10)** berdasarkan kompromi antara performa, toleransi kegagalan (*fault tolerance*), dan kapasitas bersih efektif (*usable capacity*).

---

## 2. Prinsip Perangkat Keras dan Metode Transfer I/O

Perangkat input/output adalah komponen sistem yang memiliki disparitas kecepatan paling ekstrem dibandingkan dengan CPU (kecepatan CPU dalam skala nanodetik, sedangkan mekanik disk/jaringan dalam skala milidetik).

### Klasifikasi Perangkat I/O:
1. **Block Devices (Perangkat Blok):** Menyimpan informasi dalam blok-blok berukuran tetap (misal 512 byte atau 4 KB) yang masing-masing memiliki alamat unik. Setiap blok dapat dibaca atau ditulis secara independen dan acak (*random access*). Contoh: NVMe SSD, HDD, Flash Disk.
2. **Character Devices (Perangkat Karakter):** Mengirim atau menerima aliran data byte demi byte (*stream of bytes*) tanpa struktur blok dan tidak dapat dialamatkan secara acak. Contoh: Keyboard, Mouse, Port Serial UART.

### Tiga Metode Komunikasi Perangkat I/O:

```text
[1. POLLING / BUSY WAITING]     [2. INTERRUPT-DRIVEN I/O]      [3. DIRECT MEMORY ACCESS (DMA)]
+------------------------+      +------------------------+     +------------------------+
| CPU berulang kali cek  |      | CPU perintahkan I/O,   |     | DMA Controller kirim   |
| register status device |      | lalu beralih ke proses |     | seluruh blok data ke   |
| (Siklus CPU terbuang)  |      | lain. Device beri IRQ! |     | RAM tanpa campur CPU!  |
+------------------------+      +------------------------+     +------------------------+
```

- **DMA (Direct Memory Access):** Khusus untuk perangkat blok berkecepatan tinggi. CPU hanya menginisialisasi alamat memori dan ukuran transfer ke chip DMA Controller, lalu DMA memindahkan seluruh data langsung ke RAM fisik. Setelah seluruh blok selesai, DMA Controller hanya memicu tepat **satu interupsi** ke CPU, membebaskan prosesor untuk tugas komputasi lainnya.

---

## 3. Subsistem I/O pada Kernel Sistem Operasi

Kernel OS menyediakan serangkaian layanan terpadu untuk mengelola perangkat keras I/O:

1. **I/O Scheduling:** Mengatur ulang (*reordering*) urutan permintaan akses piranti agar pergerakan fisik perangkat diminimalkan dan efisiensi throughput ditingkatkan.
2. **Buffering:** Menyimpan data sementara di memori selama proses transfer untuk mengatasi perbedaan kecepatan atau ketidaksesuaian ukuran blok antarperangkat.
3. **Caching:** Menyimpan salinan data yang sering diakses di dalam memori RAM berkecepatan tinggi (*Page Cache* di Linux) agar pembacaan berikutnya tidak perlu mengakses piranti lambat.
4. **Spooling (Simultaneous Peripheral Operations On-Line):** Mengantrekan output untuk perangkat yang hanya dapat melayani satu pekerjaan pada satu waktu (misal *printer daemon*).

---

## 4. Struktur Fisik Disk Magnetik dan Komponen Waktu Akses

Sebuah hard disk magnetik konvensional terdiri atas piringan berputar (*Platters*), sumbu pemutar (*Spindle*), dan kepala baca/tulis (*Read/Write Heads*) yang menempel pada lengan mekanik (*Actuator Arm*).

```text
       Lengan Mekanik          Piringan Magnetik Berputar (Platter)
            |                        /=========\
       [Actuator]                   /  Track    \
            |                      |   [Sector]  | <--- Spindle (5400-7200 RPM)
            +====[ Head ]========> \             /
                                    \===========/
```

### Total Waktu Akses Disk (Access Time):
$$\text{Total Access Time} = \text{Seek Time} + \text{Rotational Latency} + \text{Transfer Time}$$

1. **Seek Time (Waktu Cari):** Waktu yang dibutuhkan lengan mekanik untuk menggerakkan *head* ke posisi silinder/track yang dituju. **(Komponen paling lambat, memakan waktu 3–15 milidetik)**.
2. **Rotational Latency (Latensi Rotasi):** Waktu yang dibutuhkan oleh piringan untuk berputar hingga sektor data yang diinginkan tepat berada di bawah *head*. (Rata-rata adalah setengah putaran piringan: $\approx 4,17\text{ ms}$ pada 7200 RPM).
3. **Transfer Time (Waktu Transfer):** Waktu aktual untuk menyalin data magnetik menjadi sinyal listrik ke controller (dalam skala mikrodetik).

> **Tujuan Algoritma Disk Scheduling:** Meminimalkan **Seek Time** (Total Head Movement) agar antrean akses disk selesai secepat mungkin.

---

## 5. Algoritma Penjadwalan Disk (Disk Scheduling)

Misalkan sebuah disk memiliki 200 silinder (nomor `0` s.d. `199`). Posisi head saat ini berada pada silinder **50**. Antrean permintaan akses (*requests queue*) adalah:  
**`82, 170, 43, 140, 24, 16, 190`**

### A. First-Come, First-Served (FCFS)
- Melayani antrean sesuai urutan kedatangan secara linier:  
  `50 -> 82 -> 170 -> 43 -> 140 -> 24 -> 16 -> 190`
- **Total Head Movement:**  
  $$|82-50| + |170-82| + |43-170| + |140-43| + |24-140| + |16-24| + |190-16|$$
  $$= 32 + 88 + 127 + 97 + 116 + 8 + 174 = \mathbf{642\text{ silinder}}.$$
- *Evaluasi:* Sangat adil, namun pergerakan lengan disk sangat liar dan boros waktu.

### B. Shortest Seek Time First (SSTF)
- Dari posisi saat ini, selalu pilih silinder yang **paling dekat jaraknya**:
  1. Dari `50`, yang terdekat adalah `43` (jarak 7).
  2. Dari `43`, yang terdekat adalah `24` (jarak 19).
  3. Dari `24`, yang terdekat adalah `16` (jarak 8).
  4. Dari `16`, yang terdekat adalah `82` (jarak 66).
  5. Dari `82`, yang terdekat adalah `140` (jarak 58).
  6. Dari `140`, yang terdekat adalah `170` (jarak 30).
  7. Dari `170`, yang terdekat adalah `190` (jarak 20).
- Rute: `50 -> 43 -> 24 -> 16 -> 82 -> 140 -> 170 -> 190`.
- **Total Head Movement:**  
  $$7 + 19 + 8 + 66 + 58 + 30 + 20 = \mathbf{208\text{ silinder}}.$$
- *Evaluasi:* Pengurangan drastis dari 642 ke 208 silinder! Namun, rentan terhadap **Starvation** bagi permintaan di silinder jauh jika permintaan baru terus berdatangan di sekitar posisi *head*.

### C. SCAN (Elevator Algorithm)
- Lengan disk bergerak ke satu arah (misalnya naik menuju silinder 199), melayani seluruh permintaan yang searah di depannya, menyentuh ujung akhir disk (199), lalu berbalik arah menuju 0 sambil melayani permintaan yang tertinggal.
- Rute: `50 -> 82 -> 140 -> 170 -> 190 -> 199 -> 43 -> 24 -> 16`.
- **Total Head Movement:**  
  $$(199 - 50) + (199 - 16) = 149 + 183 = \mathbf{332\text{ silinder}}.$$
- *Evaluasi:* Bebas dari starvation dan pergerakan lengan teratur seperti lift gedung.

---

## 6. Arsitektur Redundant Array of Independent Disks (RAID)

Teknologi **RAID** menggabungkan beberapa keping media penyimpanan fisik independen menjadi satu unit logis penyimpanan besar untuk meningkatkan **Performa** (melalui pembagian paralel data) dan/atau **Keandalan / Fault Tolerance** (melalui redundansi data).

### Tiga Pilar Mekanisme RAID:
1. **Data Striping (Pembagian Data):** Memecah file logis menjadi blok-blok kecil (*stripes*) yang disebar melintasi beberapa hard disk secara simultan untuk melipatgandakan kecepatan baca/tulis.
2. **Mirroring (Pencerminan):** Menyalin seluruh data secara identik ke hard disk cadangan secara real-time untuk toleransi kerusakan 100%.
3. **Parity (Paritas):** Menghitung nilai verifikasi matematis (menggunakan operasi logika `XOR` $\oplus$) pada blok data. Jika 1 disk rusak, isi data blok yang hilang dapat dihitung kembali (*reconstructed*) secara instan dari disk yang tersisa.

---

## 7. Taksonomi Level-Level RAID Populer

| Level RAID | Nama Konsep | Minimal Disk | Kapasitas Bersih Usable | Toleransi Kerusakan (Fault Tolerance) | Karakteristik Performa | Penggunaan Ideal |
| :---: | :--- | :---: | :---: | :---: | :--- | :--- |
| **RAID 0** | Striping Tanpa Paritas | 2 | $N \times S$ (100%) | **0 Disk** (Jika 1 disk rusak, seluruh data musnah). | Sangat Tinggi (Baca & Tulis paralel). | *Scratch disk*, rendering video non-kritis. |
| **RAID 1** | Pure Mirroring | 2 | $\frac{N}{2} \times S$ (50%) | **1 Disk per pasang** mirror. | Baca cepat, Tulis normal (menulis ganda). | OS Boot drive, server file penting anggaran kecil. |
| **RAID 5** | Distributed Parity | 3 | $(N - 1) \times S$ | **1 Disk rusak**. | Baca sangat cepat, Tulis ada *parity write penalty*. | File server umum, data warehouse. |
| **RAID 6** | Dual Distributed Parity | 4 | $(N - 2) \times S$ | **2 Disk rusak** bersamaan. | Toleransi tinggi, komputasi parity ganda (P+Q). | Storage archive kapasitas raksasa (>10 TB). |
| **RAID 10 (1+0)** | Mirrored Striping | 4 (Genap) | $\frac{N}{2} \times S$ (50%) | **Minimal 1 disk per sub-array**, hingga 2 disk jika berbeda mirror. | **Performa Tertinggi** tanpa overhead komputasi parity. | **Server Database Transaksional (OLTP), Mission-Critical**. |

---

## 8. Rangkuman Materi

1. Piranti I/O dikelola melalui **DMA** untuk membebaskan CPU dari siklus transfer byte data yang lambat.
2. **Seek Time** mendominasi waktu akses hard disk mekanik.
3. Penjadwalan disk bertujuan meminimalkan pergerakan lengan: **SSTF** memberikan rute terpendek namun rentan *starvation*, sedangkan **SCAN** menjamin keadilan pelayanan secara teratur.
4. **RAID** menyatukan disk independen untuk performa (*Striping*) dan keandalan (*Mirroring / Parity*).
5. Pemilihan arsitektur RAID (seperti **RAID 10** vs **RAID 5**) adalah kompromi teknis antara kecepatan transaksi, kapasitas bersih, dan ketahanan terhadap kegagalan hardware.

---

## 9. Referensi Pustaka

- **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons. **Chapter 11: Mass-Storage Structure & Disk Scheduling (pp. 455–488); Chapter 12: I/O Systems (pp. 497–524).**
- **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson. **Chapter 5: Input/Output — DMA, Disks, RAID Architecture (pp. 355–428).**
- **Nemeth, E., et al. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson. **Chapter 8: Storage & RAID Configuration (pp. 209–244).**
