# Tugas Praktikum Minggu 15 & Instrumen Penilaian Tugas Besar

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 15  
**Bobot Penilaian Pertemuan:** 10% (Bagian dari Akumulasi Proyek Akhir 30%)  

---

## 1. Tugas Praktikum Mingguan (Monitoring & Evaluasi Kinerja)
Dokumentasikan langkah kerja pada [`Praktikum.md`](./Praktikum.md) menggunakan [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md) dan jawablah pertanyaan berikut:
1. **Analisis Load Average (`2.50, 1.20, 0.80` pada 4 Core CPU):** Jelaskan arti ketiga angka tersebut (rata-rata beban 1 menit, 5 menit, dan 15 menit terakhir) pada server dengan 4 Core CPU. Apakah server tersebut mengalami *overload*? Jelaskan alasannya!
2. **Dokumentasi Stress Test CPU (`htop` & `stress`):** Lampirkan *screenshot* pengujian langkah C.4 dan jelaskan metrik yang membuktikan saturasi CPU serta perubahan *Load Average*.
3. **Tools Monitoring Jaringan Linux:** Sebutkan dan jelaskan minimal 2 *tools* monitoring lalu lintas jaringan di Linux (misal: `iftop`, `nethogs`, `vnstat`, `bmon`).

---

## 2. Panduan & Rubrik Penilaian Tugas Besar (Bobot 30% Nilai Akhir)

**Deskripsi Proyek:**  
Mahasiswa dalam kelompok (2-3 orang) ditugaskan untuk mengonfigurasi sebuah *environment* server menggunakan Docker. Server tersebut harus menjalankan minimal 3 layanan: Web Server (Nginx), Database (MySQL/PostgreSQL/Redis), dan aplikasi backend sederhana.

**Ketentuan Pengumpulan & Presentasi (Minggu 15):**
1. Menyusun skrip `docker-compose.yml` dengan pembatasan sumber daya (`cpus` & `mem_limit`).
2. Melakukan uji beban (*load testing*) sederhana dan memonitor kinerja (menggunakan `docker stats` / `top` / `htop` / `cAdvisor`).
3. Menyusun laporan akhir sesuai [`Format_Laporan_Tugas_Besar.md`](./Format_Laporan_Tugas_Besar.md) dan mempresentasikan hasilnya (maksimal 10 menit per kelompok).

### Rincian Bobot Penilaian Proyek Akhir (Sesuai RPS 2026):
| No | Komponen Penilaian Proyek Akhir | Bobot (%) |
| :---: | :--- | :---: |
| 1 | Analisis kebutuhan dan perumusan masalah sumber daya | 5% |
| 2 | Desain arsitektur/solusi dan ketepatan alokasi sumber daya | 7% |
| 3 | Implementasi/konfigurasi serta keberfungsian solusi (`docker-compose`) | 8% |
| 4 | Pengujian, monitoring, dan analisis kinerja (*load testing* & *resource limit*) | 5% |
| 5 | Dokumentasi laporan akhir, presentasi, komunikasi, dan kolaborasi | 5% |
| **Total** | **Total Bobot Proyek Akhir** | **30%** |
