# Modul Praktikum: Manajemen Proses di Linux

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 3

---

## 1. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Menampilkan daftar proses yang sedang berjalan pada sistem operasi Linux.
2. Memahami hirarki proses (*Parent* dan *Child*).
3. Menggunakan perintah dasar manajemen proses seperti `ps`, `kill`, `pkill`.
4. Mengelola proses di latar depan (*Foreground*) dan latar belakang (*Background*) menggunakan `bg`, `fg`, dan operator `&`.

## 2. Dasar Teori Singkat
Dalam Linux, setiap tugas yang berjalan adalah sebuah proses. Setiap proses diidentifikasi dengan nomor unik yang disebut **PID (Process ID)**. Proses pertama yang dijalankan oleh kernel Linux saat *booting* memiliki PID 1 (biasanya `systemd` atau `init`), dan semua proses lain adalah *Child* (turunan) dari proses PID 1 tersebut.

Manajemen proses melalui terminal CLI (*Command Line Interface*) sangat krusial bagi administrator sistem untuk mengatasi aplikasi yang *hang* atau memonitor layanan (*services*).

## 3. Alat dan Bahan
1. Mesin Linux (Ubuntu/Debian) fisik, *Virtual Machine*, atau WSL2.
2. Terminal (Bash/Zsh).

## 4. Langkah Kerja

### A. Melihat Status Proses (The `ps` command)
1. Buka terminal Anda.
2. Untuk melihat proses di sesi terminal Anda saat ini, cukup ketik:
   ```bash
   ps
   ```
3. Untuk melihat seluruh proses di dalam sistem (lengkap dengan nama *user* dan argumen *command*), gunakan:
   ```bash
   ps aux
   ```
4. Untuk melihat struktur hirarki proses (seperti pohon), gunakan:
   ```bash
   pstree
   ```
   *(Jika `pstree` belum ada, instal dengan `sudo apt install psmisc`)*

### B. Menghentikan Proses (`kill`)
Kita akan membuat proses tidur panjang, lalu kita "bunuh" (hentikan secara paksa).
1. Jalankan perintah ini (ini akan memblokir terminal Anda karena berjalan di *foreground*):
   ```bash
   sleep 1000
   ```
2. Tekan kombinasi tombol `Ctrl + Z` di keyboard. Ini tidak mematikan `sleep`, tetapi menunda (*suspend/stopped*) proses tersebut dan mengembalikannya ke latar belakang.
3. Cari nilai PID dari `sleep` tadi:
   ```bash
   ps aux | grep sleep
   ```
4. Gunakan PID tersebut untuk mengirim sinyal *Terminated* (SIGTERM/15):
   ```bash
   kill <PID_SLEEP_TADI>
   ```
   *(Atau `kill -9 <PID>` untuk menghentikan paksa tanpa toleransi - SIGKILL)*

### C. Foreground dan Background Jobs
1. Jalankan proses di latar belakang sejak awal dengan menambahkan simbol `&`:
   ```bash
   sleep 3000 &
   sleep 4000 &
   ```
2. Lihat daftar "pekerjaan" (*jobs*) di terminal Anda:
   ```bash
   jobs
   ```
3. Pindahkan salah satu proses tersebut ke latar depan (*Foreground*) agar dapat kita kontrol langsung:
   ```bash
   fg %1
   ```
   *(Angka 1 disesuaikan dengan nomor job di kurung siku `[1]` dari hasil perintah `jobs`)*
4. Tekan `Ctrl + C` untuk membatalkan proses yang ada di *foreground* tersebut.

## 5. Tugas / Laporan Praktikum
1. Apa perbedaan utama fungsi dari kombinasi tombol `Ctrl + C` dengan `Ctrl + Z` di terminal Linux?
2. Cobalah jalankan perintah `ps -ef`. Apa arti kolom **PPID** pada hasil output tersebut?
3. Carilah sebuah proses dengan nama `bash` (gunakan `pgrep bash`). Kemudian bunuh proses tersebut menggunakan `kill -9 <PID_BASH>`. Apa yang terjadi pada terminal Anda, dan mengapa hal tersebut terjadi? Jelaskan!
