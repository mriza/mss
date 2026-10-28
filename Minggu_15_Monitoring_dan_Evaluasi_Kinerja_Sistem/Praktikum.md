# Modul Praktikum: Monitoring & Evaluasi Kinerja Sistem

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 15

---

## 1. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Menggunakan berbagai *utility command-line* Linux untuk memonitor beban sistem.
2. Membaca dan menganalisis metrik CPU, Memori, dan I/O Disk.
3. Melakukan identifikasi *bottleneck* atau proses yang memberatkan sistem.
4. Menerapkan manajemen *process priority* menggunakan `nice` dan `renice`.

## 2. Dasar Teori Singkat
Monitoring adalah langkah proaktif dalam manajemen sumber daya sistem. Seorang SysAdmin perlu tahu seberapa sehat server mereka. Tiga komponen utama yang sering menjadi *bottleneck* (penyempitan kinerja) adalah:
- **CPU Bound:** Terlalu banyak proses komputasi yang memaksa CPU bekerja 100%.
- **Memory Bound:** RAM habis, sistem menggunakan partisi *Swap* (di HDD/SSD) yang sangat lambat.
- **I/O Bound:** Proses antri panjang menunggu giliran baca/tulis ke disk atau jaringan.

## 3. Alat dan Bahan
1. Mesin Linux (Ubuntu/Debian) fisik, *virtual machine*, atau WSL2.
2. Utility: `top`, `htop`, `iotop`, `stress` (untuk simulasi beban).

## 4. Langkah Kerja

### A. Persiapan (Instalasi Tools Tambahan)
1. Buka terminal Anda.
2. Update *repository* dan install alat bantu monitoring (*htop*) serta simulasi (*stress*):
   ```bash
   sudo apt update
   sudo apt install htop iotop stress -y
   ```

### B. Monitoring Real-time dengan Htop
1. Ketikkan perintah: `htop`
2. Perhatikan bagian atas (*Header*):
    - Bar CPU (angka 1, 2, dst menunjukkan jumlah core).
    - Mem (Memory) & Swp (Swap).
    - *Load Average* (1 min, 5 min, 15 min). Angka ini menunjukkan rata-rata panjang antrian proses.
3. Gunakan tombol `F6` (*SortBy*) untuk mengurutkan proses berdasarkan `PERCENT_CPU` atau `PERCENT_MEM`.
4. Keluar dari *htop* dengan menekan tombol `F10` atau `q`.

### C. Simulasi Beban CPU (Stress Test)
1. Buka DUA jendela terminal berdampingan.
2. Di **Terminal 1**, jalankan `htop`. Amati penggunaan CPU, seharusnya cukup rendah.
3. Di **Terminal 2**, jalankan perintah stress untuk membebani 2 *core* CPU selama 60 detik:
   ```bash
   stress --cpu 2 --timeout 60s
   ```
4. Kembali ke **Terminal 1** (`htop`). Amati bagaimana bar CPU melonjak tajam ke 100% dan metrik *Load Average* mulai naik secara berkala.
5. Perhatikan proses bernama `stress` pasti berada di daftar teratas penggunaan CPU.

### D. Manajemen Prioritas Proses (Nice & Renice)
Di Linux, prioritas CPU (Niceness) berkisar dari -20 (Paling diprioritaskan) hingga 19 (Paling santai/rendah). Default semua proses adalah 0.

1. Jalankan `stress` lagi dengan prioritas terendah (19) di *background*:
   ```bash
   nice -n 19 stress --cpu 1 --timeout 120s &
   ```
2. Cek di `htop`, cari proses `stress`, lihat kolom `NI` (Nice), nilainya pasti menunjukkan angka 19.
3. Anda dapat mengubah prioritas saat proses sedang berjalan (misal kita ingin menaikkannya kembali ke 0). Cari nilai PID-nya di `htop`, lalu:
   ```bash
   sudo renice -n 0 -p <PID_STRESS_YANG_TADI>
   ```

## 5. Tugas / Laporan Praktikum
1. Pada bagian B, apa arti dari nilai *Load Average* `2.50, 1.20, 0.80` pada sebuah server yang memiliki **4 Core CPU**? Apakah server tersebut sedang mengalami *overload*? Jelaskan alasan logisnya!
2. Ambil *screenshot* layar Anda pada saat pengujian langkah C.4, dan tunjukkan metrik manakah yang membuktikan bahwa CPU sedang sibuk berat.
3. Sebutkan dan jelaskan secara singkat minimal 2 (dua) *tools* monitoring di Linux yang khusus memantau beban lalu lintas Jaringan (*Network Traffic*)!
