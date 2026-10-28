# Tugas Praktikum Minggu 2: Struktur Sistem Komputer dan Sistem Operasi

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 2  
**Bobot Penilaian Pertemuan:** 2%  

---

## 1. Pertanyaan Tugas & Analisis
Setelah menyelesaikan langkah kerja pada [`Praktikum.md`](./Praktikum.md), jawablah pertanyaan berikut di dalam laporan praktikum Anda:

1. **Hierarki Penyimpanan pada Sistem Anda:** Berdasarkan hasil perintah `lscpu`, `free -m`, dan `lsblk` di komputer/VM Anda, susunlah tabel hierarki penyimpanan nyata dari sistem Anda mulai dari L1 Cache, L2 Cache, L3 Cache, RAM, hingga Disk utama beserta masing-masing kapasitasnya!
2. **Analisis Dual-Mode Operation:** Mengapa sistem operasi modern memisahkan mode eksekusi menjadi *User Mode* dan *Kernel Mode*? Apa bahaya yang dapat terjadi pada manajemen sumber daya sistem jika aplikasi pengguna diizinkan mengeksekusi instruksi I/O atau mengakses alamat memori fisik secara langsung tanpa *Kernel Mode*?
3. **Observasi System Call (`strace`):** Jalankan perintah `strace -c ls` di terminal Linux Anda (opsi `-c` menampilkan tabel ringkasan jumlah panggilan *system call*). Lampirkan *screenshot* hasilnya dan sebutkan 3 nama *system call* teratas yang dipanggil oleh perintah `ls` beserta fungsi dasarnya!

## 2. Format Pengumpulan
- Gunakan template laporan pada [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan laporan dalam format `.pdf` melalui sistem e-Learning sebelum pertemuan Minggu ke-3.
