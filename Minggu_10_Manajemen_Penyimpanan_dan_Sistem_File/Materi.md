# Bahan Ajar: Minggu 10 - Manajemen Penyimpanan dan Sistem File

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer – Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan:** 10 (Sepuluh) — Semester 5 / 2 SKS  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Bahan Kajian:** BK02/MP-10  

---

## 1. Capaian Pembelajaran (Sub-CPMK) & Indikator

Pada akhir sesi perkuliahan ini, mahasiswa diharapkan mampu:
1. **Menguraikan konsep file, atribut berkas, dan metode akses data** (*Sequential* vs *Direct/Random Access*).
2. **Menganalisis struktur organisasi direktori pohon (*Tree-Structured Directory*)** serta membedakan *Absolute Path* dan *Relative Path*.
3. **Menjelaskan arsitektur *Virtual File System* (VFS) pada Linux** beserta 4 objek utamanya: *superblock*, *inode*, *dentry*, dan *file*.
4. **Menganalisis struktur anatomi *Inode (Index Node)*** dan mekanisme pointer bertingkat (*Multi-level Indexing*).
5. **Membedakan implementasi tautan berkas: *Hard Link* vs *Symbolic Link (Soft Link)***.
6. **Mengevaluasi tiga metode alokasi blok disk**: *Contiguous Allocation*, *Linked Allocation*, dan *Indexed Allocation*.
7. **Memahami strategi manajemen ruang bebas (*Free-Space Management*)** menggunakan *Bit Vector / Bitmap*.

---

## 2. Konsep File dan Atribut Berkas

Dari sudut pandang sistem operasi, **File** adalah abstraksi penyimpanan paling mendasar: sekumpulan byte logis yang saling berhubungan dan disimpan pada media non-volatile (*persisten*).

### Atribut Utama File:
1. **Name:** Nama simbolik file yang dapat dibaca oleh manusia.
2. **Identifier (Inode Number):** Angka unik yang menjadi identitas asli file di dalam sistem file kernel.
3. **Type:** Informasi tipe format berkas (misal file reguler, direktori, socket, pipe, perangkat blok/karakter).
4. **Location:** Pointer yang merujuk ke lokasi fisik blok-blok data di media penyimpanan.
5. **Size:** Ukuran berkas saat ini dalam satuan byte.
6. **Protection:** Hak akses kontrol baca, tulis, dan eksekusi (*Permissions*).
7. **Timestamps:** Waktu pembuatan (*ctime*), waktu modifikasi konten (*mtime*), dan waktu akses terakhir (*atime*).

### Metode Akses File:
- **Sequential Access (Akses Berurutan):** Informasi dibaca baris demi baris dari awal hingga akhir (meniru cara kerja pita kaset/tape). Operasi utama: `read_next()`, `write_next()`.
- **Direct / Random Access (Akses Acak):** Pembacaan atau penulisan data dapat langsung melompat ke posisi byte mana pun secara instan menggunakan fungsi pemindah pointer (*file offset*) seperti `lseek()`. Sangat penting bagi sistem basis data (*database*).

---

## 3. Struktur Direktori dan Konsep Mounting di Linux

Linux mengorganisasikan seluruh media penyimpanan ke dalam satu struktur hierarki pohon tunggal (*Single Hierarchical Tree*) yang berpusat pada **Root Directory (`/`)**. Berbeda dengan sistem operasi Windows yang memecah partisi menjadi huruf drive terpisah (`C:\`, `D:\`), Linux menggunakan konsep **Mounting**:
- Setiap partisi disk, SSD eksternal, atau flashdisk baru "ditempelkan" (*mounted*) ke salah satu direktori kosong yang disebut **Mount Point**.
- Misalnya: Partisi `/dev/sdb1` di-mount ke direktori `/mnt/data`.

```text
                  / (Root Directory)
                  |
    +-------+-----+-----+-------+
    |       |     |     |       |
   etc/    home/ bin/  var/    mnt/
            |                   |
          mriza/              data/ (Mount point untuk disk kedua)
            |
         Tugas/
```

- **Absolute Path:** Penulisan alamat direktori yang diawali dari akar tertinggi sistem (`/`), contoh: `/home/mriza/Tugas/catatan.txt`.
- **Relative Path:** Penulisan alamat direktori yang mengacu pada posisi kerja saat ini (*Current Working Directory* / `pwd`), contoh: `Tugas/catatan.txt` atau `../backup/`.

---

## 4. Arsitektur Virtual File System (VFS) pada Linux

Kernel Linux mendukung puluhan jenis sistem file yang sangat berbeda arsitekturnya (seperti Ext4, XFS, Btrfs, FAT32, NTFS, hingga sistem file jaringan NFS). Agar pemrogram tidak perlu menulis kode berbeda untuk setiap tipe disk, Linux menyediakan lapisan abstraksi tingkat tinggi bernama **Virtual File System (VFS)**.

```text
+-------------------------------------------------------------+
|    Aplikasi Pengguna (User Apps: open, read, write, close)  |
+-------------------------------------------------------------+
                              |
+-------------------------------------------------------------+
|           VFS (VIRTUAL FILE SYSTEM INTERFACE)               |
+-------------------------------------------------------------+
         |                     |                     |
+-----------------+   +-----------------+   +-----------------+
| Ext4 File System|   | XFS File System |   | NFS (Network FS)|
+-----------------+   +-----------------+   +-----------------+
         |                     |                     |
+-------------------------------------------------------------+
|               Device Drivers & Block Storage                |
+-------------------------------------------------------------+
```

### Empat Objek Struktur Kunci pada VFS:
1. **Superblock Object:** Menyimpan metadata menyeluruh dari satu sistem file (tipe filesystem, ukuran blok, total inode, jumlah blok bebas).
2. **Inode Object (Index Node):** Mewakili satu file individual tertentu pada disk, menyimpan seluruh metadata file tersebut (kecuali namanya).
3. **Dentry Object (Directory Entry):** Menghubungkan nama file yang diketik manusia dengan nomor Inode-nya di kernel, serta menyusun hierarki pohon direktori di memori (*dentry cache*).
4. **File Object:** Mewakili sebuah file yang sedang dibuka oleh suatu proses di memori (*Open File Table*), mencatat posisi offset baca/tulis saat ini.

---

## 5. Anatomi Inode dan Skema Multi-Level Indexing

Pada sistem file keluarga Unix/Linux (seperti Ext4), setiap file diwakili oleh sebuah struktur **Inode**.

> **Fakta Kritis Linux:**  
> Nama file **TIDAK PERNAH** disimpan di dalam Inode! Nama file hanya disimpan di dalam blok data direktori induknya sebagai pasangan `<Nama File, Nomor Inode>`.

```text
INODE STRUCTURE
+-------------------------------+
| Mode & Hak Akses (rwxr-xr--)  |
| Owner UID / Group GID         |
| File Size (bytes)             |
| Timestamps (atime, mtime, ctime)|
+-------------------------------+
| Direct Blocks (0 s.d. 11)     | ---> [Blok Data 0] ... [Blok Data 11]
| Single Indirect Block Pointer | ---> [Tabel Pointer] ---> [Blok Data...]
| Double Indirect Block Pointer | ---> [Tabel] ---> [Tabel] ---> [Data...]
| Triple Indirect Block Pointer | ---> [Tabel] -> [Tabel] -> [Tabel] -> [Data]
+-------------------------------+
```

### Keunggulan Skema Multi-Level Indexing:
- **Untuk file kecil (misal < 48 KB):** Cukup menggunakan 12 *Direct Block Pointers*. Akses data sangat cepat karena tidak membutuhkan penelusuran pointer perantara.
- **Untuk file raksasa (ukuran Gigabyte hingga Terabyte):** Kernel menggunakan pointer tidak langsung bertingkat (*Single, Double, Triple Indirect*), memungkinkan pengalamatan jutaan blok disk secara fleksibel tanpa membuang ruang metadata untuk file kecil.

### Hard Link vs Symbolic Link:
- **Hard Link:** Entri direktori baru yang menunjuk ke **Nomor Inode yang sama**. File asli dan hard link adalah file yang sama persis secara fisik. Jika file asli dihapus (`rm`), data fisik di disk tidak akan hilang selama *Link Count* pada Inode belum bernilai 0.
- **Symbolic Link (Soft Link):** File baru independen dengan nomor Inode sendiri, yang isi datanya berupa string teks path alamat file target (mirip *Shortcut* di Windows). Jika file target dihapus, symlink menjadi rusak (*Dangling / Broken Link*).

---

## 6. Tiga Metode Alokasi Blok Disk (Disk Space Allocation)

Bagaimana sistem operasi memetakan file logis ke dalam blok-blok fisik hardisk/SSD?

```text
1. CONTIGUOUS ALLOCATION        2. LINKED ALLOCATION          3. INDEXED ALLOCATION
+---+---+---+---+---+           +---+    +---+    +---+        +-------------------+
| 0 | 1 | 2 | 3 | 4 |           | 0 |--->| 7 |--->| 3 |        | Blok Indeks:      |
+---+---+---+---+---+           +---+    +---+    +---+        | Pointer: [0, 7, 3]|
(Blok harus bersebelahan)       (Tiap blok punya pointer)      +-------------------+
```

| Karakteristik | Contiguous Allocation | Linked Allocation | Indexed Allocation (Inode) |
| :--- | :--- | :--- | :--- |
| **Prinsip** | File menempati sekumpulan blok disk fisik yang letaknya berdampingan secara linier. | File disimpan di blok mana pun, tiap blok menyimpan pointer alamat blok berikutnya. | Seluruh pointer blok data dikumpulkan dalam satu blok indeks khusus (*Inode*). |
| **Kecepatan Akses** | Akses sekuensial dan acak (*direct*) sangat cepat (cukup lompat alamat). | Akses sekuensial baik, namun **akses acak sangat lambat** (harus menelusuri rantai dari awal). | **Mendukung akses sekuensial dan akses acak secara sangat cepat**. |
| **Fragmentasi** | Menderita **Fragmentasi Eksternal parah**; sulit memperbesar ukuran file. | **Bebas fragmentasi eksternal**; ukuran file mudah bertambah dinamis. | **Bebas fragmentasi eksternal**; ukuran file dapat bertumbuh sangat besar. |
| **Kelemahan** | Disk cepat penuh oleh celah-celah kecil; memerlukan defragmentasi berkala. | Hilangnya 1 pointer akibat blok rusak membuat sisa file hilang total. | Memerlukan ruang overhead memori untuk menyimpan blok indeks. |

---

## 7. Rangkuman Materi

1. **File** adalah abstraksi logika data persisten, diakses secara berurutan (*Sequential*) atau langsung (*Direct/Random*).
2. Sistem operasi Linux menyatukan seluruh media penyimpanan dalam satu struktur pohon tunggal melalui mekanisme **Mounting**.
3. **VFS** bertindak sebagai antarmuka polimorfik yang menjembatani sistem file heterogen melalui objek *superblock*, *inode*, *dentry*, dan *file*.
4. **Inode** menyimpan seluruh metadata berkas menggunakan skema *multi-level indexing*, terpisah dari nama file yang dikelola oleh objek *dentry*.
5. Metode **Indexed Allocation** menggabungkan keunggulan akses acak cepat tanpa terbebani masalah fragmentasi eksternal.

---

## 8. Referensi Pustaka

- **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons. **Chapter 13: File-System Interface (pp. 531–564); Chapter 14: File-System Implementation & VFS (pp. 571–612).**
- **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson. **Chapter 4: File Systems — Inodes, Implementation, and Directory Management (pp. 287–352).**
- **Nemeth, E., et al. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson. **Chapter 6: The Filesystem (pp. 145–182).**
