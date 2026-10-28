# Modul Praktikum: Eksplorasi Informasi Hardware, Interrupts, dan System Calls di Linux

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 2  

---

## 1. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Mengeksplorasi arsitektur CPU, hierarki *cache*, memori utama (RAM), dan perangkat *block storage* menggunakan perintah CLI Linux (`lscpu`, `free -m`, `lsblk`).
2. Mengamati tabel interupsi perangkat keras secara nyata melalui sistem file semu `/proc/interrupts`.
3. Melacak pemanggilan *System Call* yang dilakukan oleh program ruang pengguna (*User Mode*) menuju kernel (*Kernel Mode*) menggunakan utilitas `strace`.

## 2. Dasar Teori Singkat
Sistem operasi Linux menyediakan antarmuka transparansi sumber daya perangkat keras melalui utilitas standar dan sistem file virtual `/proc`. Selain itu, setiap perintah sederhana yang dijalankan pengguna di terminal (seperti `ls` atau `cat`) sebenarnya tidak mengakses disk atau layar secara langsung, melainkan memicu puluhan *System Calls* (seperti `openat()`, `read()`, `write()`, `close()`) yang mengalihkan mode eksekusi CPU dari *User Mode* ke *Kernel Mode*.

## 3. Alat dan Bahan
1. Mesin Linux (Ubuntu/Debian) fisik, *Virtual Machine*, atau WSL2.
2. Terminal (Bash/Zsh) dan paket `strace` (`sudo apt install strace -y`).

## 4. Langkah Kerja

### A. Menginspeksi Arsitektur CPU dan Hierarki Cache (`lscpu`)
1. Buka terminal Linux Anda.
2. Jalankan perintah berikut untuk menampilkan detail arsitektur prosesor:
   ```bash
   lscpu
   ```
3. Catat informasi penting yang tampil:
   - `Architecture` (misal: `x86_64` atau `aarch64`)
   - `CPU(s)`, `Thread(s) per core`, dan `Core(s) per socket`
   - `Model name`
   - Ukuran `L1d cache`, `L1i cache`, `L2 cache`, dan `L3 cache` (sesuai konsep *Storage Hierarchy* pada materi kuliah).

### B. Menginspeksi Memori Utama dan Block Storage (`free` & `lsblk`)
1. Periksa kondisi memori utama (RAM) dan ruang *Swap* dalam satuan Megabyte:
   ```bash
   free -m
   ```
   Perhatikan kolom `total`, `used`, `free`, `buff/cache`, dan `available`.
2. Periksa daftar perangkat penyimpanan blok (*block devices* seperti disk dan partisi):
   ```bash
   lsblk
   ```

### C. Mengamati Hardware Interrupts (`/proc/interrupts`)
1. Tampilkan daftar interupsi yang ditangani oleh masing-masing *core* CPU:
   ```bash
   cat /proc/interrupts | head -n 25
   ```
2. Perhatikan bagaimana setiap lini interupsi (seperti timer lokal `LOC`, keyboard `i8042`, atau disk/network controller) memiliki penghitung jumlah interupsi per CPU core.

### D. Melacak System Calls dengan `strace`
1. Pastikan `strace` sudah terinstal:
   ```bash
   sudo apt update && sudo apt install -y strace
   ```
2. Jalankan perintah sederhana `echo "Halo Kernel"` sambil melacak *System Call* yang terjadi di belakang layar:
   ```bash
   strace echo "Halo Kernel"
   ```
3. Perhatikan pada baris-baris terakhir output `strace`, Anda akan menemukan pemanggilan sistem:
   ```text
   write(1, "Halo Kernel\n", 12) = 12
   exit_group(0)                 = ?
   ```
   Baris `write(1, ...)` membuktikan bahwa untuk mencetak teks ke layar (file descriptor `1` / `stdout`), program harus meminta layanan kernel melalui *System Call* `write()`.

## 5. Tugas / Laporan Praktikum
Kerjakan soal latihan dan analisis pada [`Tugas_Praktikum.md`](./Tugas_Praktikum.md).
