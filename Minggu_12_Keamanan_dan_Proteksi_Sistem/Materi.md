# Bahan Ajar: Minggu 12 - Keamanan dan Proteksi Sistem

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer – Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan:** 12 (Dua Belas) — Semester 5 / 2 SKS  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Bahan Kajian:** BK02/MP-12  

---

## 1. Capaian Pembelajaran (Sub-CPMK) & Indikator

Pada akhir sesi perkuliahan ini, mahasiswa diharapkan mampu:
1. **Membedakan konsep Proteksi (*Protection*) dan Keamanan (*Security*)** pada sistem komputer.
2. **Menerapkan *Principle of Least Privilege* (PoLP)** untuk meminimalkan dampak kerusakan akibat eksploitasi program atau kesalahan sistem.
3. **Menganalisis model Matriks Akses (*Access Matrix Model*)** beserta dua implementasi fisiknya: *Access Control List* (ACL) dan *Capability List*.
4. **Menguasai sistem perizinan berkas Linux (*Linux File Permissions*)**: membaca representasi simbolik (`rwx`) dan menghitung format numerik oktal.
5. **Membedakan fungsi hak akses `rwx` pada File vs Direktori**, serta memahami izin khusus (*SUID*, *SGID*, dan *Sticky Bit*).
6. **Menganalisis peran masker sistem (*Umask*)** dalam pembentukan izin default berkas.
7. **Memahami Rencana Tugas Mahasiswa (RTM) Proyek Akhir** (bobot 30%) yang diluncurkan pada pertemuan ini.

---

## 2. Proteksi vs Keamanan Sistem

Meskipun sering digunakan secara bergantian, sistem operasi membedakan dua istilah ini secara tegas:

- **Proteksi (Protection):** Mekanisme internal sistem operasi yang bertugas mengontrol, membatasi, dan mengawasi akses proses atau pengguna terhadap sumber daya yang didefinisikan di dalam sistem komputer (CPU, RAM, file, perangkat).
- **Keamanan (Security):** Langkah-langkah pertahanan sistem secara menyeluruh terhadap serangan dari luar (*external threats*), seperti serangan malware, pencurian kredensial, modifikasi data tanpa hak, atau serangan *Denial of Service* (DoS).

> *Analogi:* Proteksi adalah kunci pintu kamar di dalam rumah untuk mencegah anggota keluarga saling mengacak barang masing-masing. Keamanan adalah pagar keliling, satpam, dan CCTV yang mencegah pencuri membobol rumah.

---

## 3. Prinsip Hak Akses Terkecil (Principle of Least Privilege / PoLP)

**Principle of Least Privilege (PoLP)** menyatakan bahwa:
> *Setiap pengguna, proses, atau program aplikasi hanya boleh diberikan hak akses seminimal mungkin yang mutlak diperlukan untuk menyelesaikan tugas resminya, dan hak istimewa tersebut harus dibatasi dalam rentang waktu sesingkat mungkin.*

```text
PRINSIP BURUK (Risiko Fatal):           PRINSIP BAIK (Least Privilege):
+---------------------------------+     +---------------------------------+
| Web Server berjalan sebagai     |     | Web Server berjalan sebagai     |
| pengguna 'root' (Hak Penuh)     |     | user non-login 'www-data'       |
|                                 |     | Hak terbatas: Hanya baca HTML   |
+---------------------------------+     +---------------------------------+
                 |                                       |
           Bila diretas...                         Bila diretas...
                 v                                       v
[Peretas menguasai seluruh server!]     [Peretas terisolasi, server aman!]
```

Jika seorang SysAdmin selalu login dan menjalankan aplikasi rutin menggunakan akun `root` (atau Administrator), satu kesalahan pengetikan skrip (seperti `rm -rf /*`) atau satu kerentanan aplikasi web dapat melenyapkan seluruh isi server seketika (*blast radius* tak terbatas).

---

## 4. Model Matriks Akses (Access Matrix Model)

Secara teoritis, status proteksi sistem dimodelkan sebagai sebuah matriks dua dimensi $M$:
- **Baris:** Domain Proteksi ($D_1, D_2, \dots$) yang mewakili Pengguna, Proses, atau Peran.
- **Kolom:** Objek Sistem ($O_1, O_2, \dots$) yang dapat berupa File, Port I/O, Segment Memori, atau Semaphore.
- **Nilai Sel $M[D_i, O_j]$:** Kumpulan hak akses (*Access Rights*) yang diizinkan (misal: `Read`, `Write`, `Execute`).

```text
+----------+---------------+---------------+---------------+
| Domain   | File A        | File B        | Printer 1     |
+----------+---------------+---------------+---------------+
| Dosen    | Read, Write   | Read, Write   | Print         |
| Asisten  | Read          | Read, Write   | Print         |
| Mahasiswa| Read          | -             | -             |
+----------+---------------+---------------+---------------+
```

### Dua Metode Penerapan Matriks Akses di Sistem Operasi:
1. **Access Control List (ACL):**
   - Matriks disimpan secara **per-kolom (melekat pada Objek)**.
   - Setiap file menyimpan daftar subjek yang boleh mengaksesnya: `File A: {Dosen: RW, Asisten: R, Mahasiswa: R}`.
   - Diadopsi oleh sistem file modern (Ext4 POSIX ACL, NTFS Windows).
2. **Capability List:**
   - Matriks disimpan secara **per-baris (melekat pada Subjek/Domain)**.
   - Setiap pengguna memegang serangkaian tiket atau token izin yang tidak dapat dipalsukan untuk membuka objek tertentu.

---

## 5. Sistem Kontrol Akses Tradisional Linux (DAC & File Permissions)

Sistem operasi Linux menerapkan model *Discretionary Access Control* (DAC) di mana pemilik berkas (*Owner*) berhak menentukan siapa saja yang boleh mengakses berkas miliknya.

### Tiga Kategori Pengguna:
1. **User / Owner (`u`):** Akun pengguna yang membuat dan memiliki file tersebut.
2. **Group (`g`):** Sekumpulan pengguna yang tergabung dalam grup yang sama dengan file.
3. **Others (`o`):** Seluruh pengguna lain di sistem di luar Owner dan Group.

### Tiga Hak Akses Dasar dan Nilai Bobot Oktal:
Setiap kelompok memiliki 3 bit izin (`rwx`):
- **Read (`r`):** Bernilai **4** (Biner: `100`).
- **Write (`w`):** Bernilai **2** (Biner: `010`).
- **Execute (`x`):** Bernilai **1** (Biner: `001`).

```text
Output 'ls -l':
  -   r w x   r - x   r - -
[Tipe][ Owner ][ Group ][ Others]
  -   (4+2+1) (4+0+1) (4+0+0)
         7       5       4
```

### Perbedaan Kritis Fungsi `rwx` pada File vs Direktori:

| Izin | Perilaku pada FILE | Perilaku pada DIREKTORI |
| :---: | :--- | :--- |
| **Read (`r`)** | Membaca isi data teks/biner file (misal dengan perintah `cat`, `less`). | Melihat daftar nama-nama berkas yang ada di dalam folder tersebut (dengan perintah `ls`). |
| **Write (`w`)** | Mengubah isi data di dalam file (menulis, mengedit, atau menimpa). | **Membuat file baru, mengubah nama file, atau menghapus file** di dalam direktori tersebut! |
| **Execute (`x`)** | Menjalankan berkas sebagai program eksekutabel atau *script bash*. | **Memasuki direktori** (`cd /path/folder`) dan mengakses metadata file di dalamnya. |

> **Peringatan Penting:** Tanpa izin `x` pada suatu direktori, pengguna **TIDAK BISA** masuk ke folder tersebut meskipun memiliki izin `r`!

---

## 6. Hak Akses Khusus: SUID, SGID, dan Sticky Bit

Linux menyediakan 3 bit perizinan khusus untuk kebutuhan sistem tertentu:

1. **SUID (Set User ID - Bit Oktal 4000 / `rws------`):**
   - Diterapkan pada file eksekutabel. Ketika program dijalankan oleh pengguna biasa, program tersebut dieksekusi dengan hak istimewa **pemilik file (biasanya `root`)**, bukan hak pengguna yang memanggilnya.
   - Contoh: Perintah `/usr/bin/passwd` memiliki izin `-rwsr-xr-x`. Pengguna biasa dapat mengubah password-nya sendiri (yang mengharuskan penulisan ke file sensitif `/etc/shadow`) secara aman melalui program tersebut.
2. **SGID (Set Group ID - Bit Oktal 2000 / `rwxr-s---`):**
   - Jika diterapkan pada direktori, setiap file baru yang dibuat di dalam direktori tersebut akan secara otomatis mewarisi grup induknya, memudahkan kolaborasi kelompok.
3. **Sticky Bit (Bit Oktal 1000 / `rwxrwxrwt`):**
   - Diterapkan pada direktori publik bersama (seperti direktori `/tmp`).
   - Meskipun semua orang memiliki hak tulis penuh (`rwx`), **hanya pemilik file yang bersangkutan yang diizinkan menghapus filenya**. Pengguna lain dilarang menghapus file milik orang lain.

---

## 7. Nilai Bawaan Berkas dan Konsep Umask

Saat file atau folder baru dibuat, hak akses awalnya ditentukan oleh pengurangan hak maksimal sistem dengan nilai **`umask`** (User Mask):
- Hak akses maksimal standar direktori: `777` (`rwxrwxrwx`).
- Hak akses maksimal standar file reguler: `666` (`rw-rw-rw-` tanpa izin eksekusi otomatis demi keselamatan).

Jika nilai umask sistem adalah `022`:
- Izin awal direktori baru: `777 - 022 = 755` (`drwxr-xr-x`).
- Izin awal file baru: `666 - 022 = 644` (`-rw-r--r--`).

---

## 8. Rangkuman Materi

1. **Proteksi** mengawal alokasi hak akses internal sumber daya, sedangkan **Keamanan** membentengi sistem dari ancaman luar.
2. **Principle of Least Privilege** membatasi hak akses ke batas paling minimal guna mengisolasi dampak bencana sistem.
3. Model **Matriks Akses** diimplementasikan di Linux melalui **Access Control Lists (ACL)** dan izin standar `rwx`.
4. Izin file dan direktori memiliki semantik yang berbeda: hak hapus file ditentukan oleh hak `w` pada direktori induknya.
5. Bit khusus **SUID**, **SGID**, dan **Sticky Bit** memberikan fleksibilitas delegasi izin aman di lingkungan multi-pengguna.

---

## 9. Referensi Pustaka

- **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons. **Chapter 16: Security (pp. 649–690); Chapter 17: Protection & Access Matrix (pp. 697–728).**
- **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson. **Chapter 9: Security & Protection Mechanisms (pp. 637–710).**
- **Nemeth, E., et al. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson. **Chapter 5: Security Principles & File Permissions (pp. 95–144).**
