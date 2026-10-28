# Tugas Praktikum Minggu 14: Perancangan Load Balancing & Arsitektur Cloud

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 14  
**Bobot Penilaian Pertemuan:** 10%  

---

## 1. Rincian Tugas
Selesaikan tugas perancangan sistem pada [`Praktikum.md`](./Praktikum.md):
1. **Diagram Blueprint Arsitektur Cloud SIAKAD:**
   - Memuat aliran trafik dari Mahasiswa -> *Load Balancer* -> minimal 3 *Web Server VM/Container* -> *Database Master* & *Database Replica/Slave*, dilengkapi komponen *Auto-Scaler*.
2. **Narasi Alur Kerja Sistem:**
   - Penjelasan teknis bagaimana *Load Balancer* mendistribusikan *request* (misal *Round Robin* / *Least Connections*) dan bagaimana pemisahan *Write* ke *Database Master* serta *Read* ke *Database Replica* mengurangi *bottleneck*.
3. **Analisis Skenario Spike Traffic (5.000 Login Bersamaan / RAM > 90%):**
   - Jelaskan mekanisme *Scale-Out* ketika metrik melewati *threshold* (misal CPU/RAM > 80–90%) dan mekanisme *Scale-In* ketika masa KRS berakhir.
4. **Progres Tugas Besar (BAB II & BAB III):**
   - Lampirkan draf diagram topologi `docker-compose.yml` kelompok Anda (Web Server + Backend + Database) sebagai persiapan presentasi Minggu ke-15.

## 2. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan dalam format `.pdf` ke sistem e-Learning sebelum pertemuan Minggu ke-15.
