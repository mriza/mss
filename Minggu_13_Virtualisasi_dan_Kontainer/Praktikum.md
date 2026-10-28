# Modul Praktikum: Manajemen Sumber Daya Menggunakan Kontainer (Docker)

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 13

---

## 1. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Menjelaskan perbedaan antara mesin virtual (Virtual Machine) dan Kontainer.
2. Melakukan instalasi dasar dan konfigurasi Docker Engine.
3. Menggunakan perintah dasar Docker untuk mengelola *image* dan *container*.
4. Membatasi penggunaan sumber daya (CPU & RAM) pada kontainer.

## 2. Dasar Teori Singkat
Kontainer (seperti Docker) menyediakan mekanisme virtualisasi pada level sistem operasi (OS-level virtualization). Berbeda dengan *Hypervisor* yang membutuhkan OS tamu (Guest OS) terpisah untuk tiap Virtual Machine, kontainer berbagi kernel OS dari mesin *Host*, sehingga jauh lebih ringan, cepat saat dihidupkan, dan hemat sumber daya.

Dalam manajemen sumber daya sistem, kita dapat dengan mudah membatasi seberapa besar sebuah aplikasi (di dalam kontainer) boleh menggunakan CPU dan Memori, mencegah satu aplikasi memonopoli *resource* server (mencegah isu *noisy neighbor*).

## 3. Alat dan Bahan
1. Komputer / Laptop dengan OS Linux (Ubuntu direkomendasikan) atau Windows dengan WSL2.
2. Akses internet untuk mengunduh *image*.
3. Akses terminal / command prompt.

## 4. Langkah Kerja

### A. Instalasi dan Uji Coba Awal (Hanya jika belum terinstal)
1. Buka terminal Anda.
2. Pastikan docker terinstal dengan mengetikkan:
   ```bash
   docker --version
   ```
3. Uji coba dengan menjalankan kontainer hello-world:
   ```bash
   sudo docker run hello-world
   ```

### B. Manajemen Image dan Kontainer Dasar
1. Unduh *image* Ubuntu berukuran kecil:
   ```bash
   sudo docker pull ubuntu:latest
   ```
2. Jalankan kontainer dari *image* tersebut secara interaktif:
   ```bash
   sudo docker run -it --name my_ubuntu ubuntu:latest /bin/bash
   ```
3. Di dalam kontainer, coba cek penggunaan RAM (ketik `free -m`). Kemudian keluar dari kontainer dengan mengetik `exit`.
4. Cek kontainer yang sedang berjalan:
   ```bash
   sudo docker ps
   ```
5. Cek semua kontainer (termasuk yang berhenti):
   ```bash
   sudo docker ps -a
   ```

### C. Pembatasan Sumber Daya Sistem (CPU & Memory)
Pada tahap ini, kita akan menjalankan sebuah web server (Nginx) tetapi membatasi penggunaan memori maksimal hanya 512MB dan batas CPU.

1. Jalankan kontainer Nginx di latar belakang (`-d`), petakan port 8080 host ke 80 kontainer (`-p`), dengan batasan memori 512MB (`-m`) dan membatasi CPU hanya 0.5 core (`--cpus`):
   ```bash
   sudo docker run -d -p 8080:80 --name web_terbatas -m 512m --cpus="0.5" nginx
   ```
2. Cek status penggunaan *resource* dari kontainer tersebut secara real-time menggunakan perintah:
   ```bash
   sudo docker stats web_terbatas
   ```
   *(Perhatikan kolom LIMIT untuk memori, pastikan menunjukkan angka sekitar 512MB)*
3. Buka browser dan akses `http://localhost:8080` untuk memastikan web server berjalan.
4. Hentikan dan hapus kontainer setelah selesai:
   ```bash
   sudo docker stop web_terbatas
   sudo docker rm web_terbatas
   ```

## 5. Tugas / Laporan Praktikum
1. Ambil *screenshot* dari hasil perintah `docker stats` pada langkah C.2 dan jelaskan apa arti masing-masing kolom pada *output* tersebut!
2. Mengapa membatasi penggunaan CPU dan Memori pada aplikasi server sangat penting dalam Manajemen Sumberdaya Sistem?
3. (Tantangan) Cari tahu dan praktikkan bagaimana cara menjalankan kontainer yang otomatis akan *restart* jika terjadi *crash* atau server di-*reboot*! Tuliskan perintahnya di laporan.
