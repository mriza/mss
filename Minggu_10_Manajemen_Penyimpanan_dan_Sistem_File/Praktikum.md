# Modul Praktikum: Navigasi dan Manajemen Sistem File di Linux

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 10

---

## 1. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Menavigasi struktur hirarki (*Tree-structured*) sistem file Linux melalui terminal CLI.
2. Membedakan penggunaan *Absolute Path* dan *Relative Path*.
3. Membuat, memindahkan, dan menghapus file/direktori.
4. Menganalisis penggunaan kapasitas penyimpanan (*Disk Space*).

## 2. Dasar Teori Singkat
Linux menggunakan struktur direktori tunggal berbentuk pohon (*Tree*) yang berpusat pada *Root Directory*, disimbolkan dengan karakter garis miring tunggal (`/`). Berbeda dengan Windows yang menggunakan pemisahan drive letters (C:\, D:\), semua media penyimpanan tambahan di Linux (Flashdisk, Hardisk eksternal) akan "ditempelkan" (di-mount) ke dalam struktur hirarki root ini.

## 3. Alat dan Bahan
1. Mesin Linux (Ubuntu/Debian) fisik, Virtual Machine, WSL2, atau Terminal macOS.

## 4. Langkah Kerja

### A. Navigasi Direktori dan Pathing
1. Buka terminal Anda. Pastikan Anda tahu sedang berada di direktori mana dengan mengetik:
   ```bash
   pwd
   ```
   *(pwd = print working directory)*
2. Pindah ke direktori utama (Root) menggunakan *Absolute Path*:
   ```bash
   cd /
   ```
3. Tampilkan isi direktori tersebut dengan detail:
   ```bash
   ls -la
   ```
4. Pindah kembali ke direktori rumah (*Home*) pengguna Anda. (Simbol tilde `~` adalah *shortcut* untuk direktori Home):
   ```bash
   cd ~
   ```
5. Buatlah hierarki folder untuk latihan ini. Gunakan argumen `-p` untuk membuat direktori bertingkat sekaligus:
   ```bash
   mkdir -p Tugas/OS/Pertemuan10
   ```
6. Pindah ke dalam folder `Pertemuan10` menggunakan **Relative Path**:
   ```bash
   cd Tugas/OS/Pertemuan10
   ```

### B. Membuat, Mengkopi, dan Menghapus File
1. Di dalam folder `Pertemuan10`, buatlah sebuah file teks kosong menggunakan perintah `touch`:
   ```bash
   touch catatan_os.txt
   ```
2. Isikan teks ke dalam file tersebut (menulis ulang isi file) menggunakan perintah `echo` dan *Redirection* (`>`):
   ```bash
   echo "Ini adalah catatan Sistem File." > catatan_os.txt
   ```
3. Buat salinan file (kopi) menjadi file cadangan:
   ```bash
   cp catatan_os.txt backup_catatan.txt
   ```
4. Ubah nama file `backup_catatan.txt` menjadi `rahasia.txt` menggunakan perintah *move* (`mv`):
   ```bash
   mv backup_catatan.txt rahasia.txt
   ```
5. Hapus file `rahasia.txt`:
   ```bash
   rm rahasia.txt
   ```

### C. Monitoring Kapasitas Penyimpanan Disk
Sebagai administrator, kita harus rutin memantau kapasitas *disk* agar tidak kepenuhan.
1. Untuk melihat kapasitas seluruh partisi/disk yang terpasang di sistem dalam format yang mudah dibaca manusia (*Human Readable*):
   ```bash
   df -h
   ```
2. Anda mungkin ingin tahu folder mana yang ukurannya paling besar. Gunakan `du` (*Disk Usage*). Mari kita cek total ukuran folder `Tugas` yang ada di direktori *Home* Anda:
   ```bash
   cd ~
   du -sh Tugas
   ```
   *(Penjelasan: -s artinya summary/total, -h artinya human readable)*

## 5. Tugas / Laporan Praktikum
1. Praktikkan kembali Bagian A langkah 5. Namun kali ini, coba buat struktur folder `Praktikum/Tugas1` dan `Praktikum/Tugas2` **hanya dengan SATU KALI eksekusi perintah `mkdir`**. Tuliskan perintahnya di laporan Anda! (*Hint: Cari tahu penggunaan kurung kurawal `{}` pada Bash*).
2. Tuliskan *output* dari perintah `df -h` komputer Anda (ambil baris untuk filesystem utama `/`). Berapa GigaByte sisa penyimpanan (*Available*) yang masih kosong?
3. Sebutkan perbedaan fungsi paling mendasar dari perintah `rm` dan perintah `rmdir`! Mengapa OS membedakan kedua perintah tersebut?
