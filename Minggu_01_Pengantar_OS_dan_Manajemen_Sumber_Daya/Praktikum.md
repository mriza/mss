# Modul Praktikum: Persiapan Lingkungan Linux dan Observasi Awal Sumber Daya

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 1  

---

## 1. Tujuan Praktikum
Setelah menyelesaikan kegiatan ini, mahasiswa diharapkan mampu:
1. Menyiapkan lingkungan kerja sistem operasi Linux (melalui VirtualBox, VMware, atau WSL2) dengan alokasi sumber daya (vCPU, RAM, dan Virtual Disk) yang terukur.
2. Mengidentifikasi pembagian sumber daya antara *Host OS* dan *Guest OS* sebagai wujud nyata *Space Multiplexing* dan *Time Multiplexing*.
3. Menjalankan perintah dasar terminal Linux untuk memverifikasi identitas kernel dan sumber daya sistem.

## 2. Dasar Teori Singkat
Seluruh kegiatan praktikum pada mata kuliah Manajemen Sumberdaya Sistem membutuhkan akses ke terminal sistem operasi berbasis UNIX/Linux. Ketika Anda menjalankan Linux di dalam *Virtual Machine* (seperti Oracle VirtualBox) atau *Windows Subsystem for Linux* (WSL2), Anda sedang mempraktikkan konsep alokasi sumber daya secara langsung: sebagian kapasitas RAM fisik dan *core* prosesor pada laptop (*Host*) dibagi untuk sistem operasi tamu (*Guest*).

## 3. Alat dan Bahan
1. Laptop/PC dengan RAM minimal 4 GB (direkomendasikan 8 GB).
2. Oracle VirtualBox + ISO Ubuntu 22.04/24.04 LTS (atau WSL2 Ubuntu pada Windows 10/11, atau instalasi Linux *native*).
3. Koneksi internet untuk pembaruan paket dasar.

## 4. Langkah Kerja

### A. Alokasi Sumber Daya Mesin Virtual (Jika Menggunakan VirtualBox)
1. Buka aplikasi **Oracle VirtualBox** dan klik **New**.
2. Beri nama VM: `Ubuntu-MSS-NIM` (ganti `NIM` dengan NIM Anda) dan pilih file ISO Ubuntu.
3. Pada bagian **Hardware (Alokasi Sumber Daya)**:
   - **Base Memory (RAM):** Alokasikan maksimal 25%–50% dari RAM fisik laptop Anda (contoh: `2048 MB` untuk laptop 8 GB RAM). Jangan melewati batas hijau agar *Host OS* tidak mengalami *starvation* memori.
   - **Processors (CPU):** Alokasikan `1` atau `2` vCPU.
4. Pada bagian **Virtual Hard Disk**:
   - Alokasikan minimal `20 GB` (*Dynamically Allocated* / *Pre-allocate* tidak dicentang agar hemat ruang disk fisik).
5. Selesaikan instalasi Ubuntu hingga Anda dapat masuk ke dalam sesi Terminal.

*(Catatan: Jika menggunakan **WSL2**, buka PowerShell sebagai Administrator dan jalankan `wsl --install -d Ubuntu`, lalu buat akun pengguna Linux Anda).*

### B. Verifikasi Sistem Operasi dan Kernel
1. Buka aplikasi **Terminal** di Linux Anda.
2. Tampilkan informasi nama rilis distribusi Linux yang terpasang:
   ```bash
   cat /etc/os-release
   ```
3. Tampilkan informasi versi kernel Linux dan arsitektur prosesor:
   ```bash
   uname -a
   ```
4. Cek berapa lama sistem telah menyala (*uptime*) dan rata-rata beban awal sistem:
   ```bash
   uptime
   ```

### C. Observasi Awal Sumber Daya Sistem
1. Cek ringkasan kapasitas memori RAM dan Swap (dalam Megabyte):
   ```bash
   free -m
   ```
2. Cek ringkasan kapasitas ruang penyimpanan disk:
   ```bash
   df -h /
   ```
3. Bandingkan angka total RAM pada `free -m` di Linux dengan jumlah RAM yang Anda alokasikan saat mengatur VM (atau total RAM laptop Anda pada Task Manager Windows).

## 5. Tugas / Laporan Praktikum
Kerjakan instruksi pada dokumen [`Tugas_Praktikum.md`](./Tugas_Praktikum.md) dan susun menggunakan format baku pada [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
