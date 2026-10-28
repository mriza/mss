# Rencana Tugas Mahasiswa (RTM) - Tugas Besar (Proyek Akhir)

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Bobot SKS:** 2 SKS  
**Semester:** 5 (Lima)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  

---

## 1. Tujuan Tugas

Mahasiswa secara kolaboratif mampu merancang, mengonfigurasi, mendeploy, membatasi alokasi sumber daya (*CPU & Memory limits*), menguji beban (*load/stress testing*), dan memonitor kinerja sebuah sistem layanan terintegrasi (*multi-container*) menggunakan teknologi virtualisasi kontainer Docker dan Docker Compose.

---

## 2. Uraian Tugas

### a. Obyek Garapan
*Deployment* arsitektur aplikasi *multi-tier client-server* yang terdiri dari minimal 3 layanan independen berbasis kontainer, disertai konfigurasi manajemen batas sumber daya sistem (*resource limits*), pengujian ketahanan terhadap lonjakan beban (*stress test*), serta analisis evaluasi kinerja (*system monitoring*).

### b. Yang Harus Dikerjakan dan Batasan Teknis
Mahasiswa bekerja dalam kelompok (2–3 orang) dan wajib menyelesaikan tahapan berikut:

1. **Perancangan Arsitektur Sistem:**
   - Menyusun topologi layanan yang memisahkan antara lapisan *Reverse Proxy / Web Server* (misal: Nginx), *Backend Application API* (misal: Python FastAPI/Flask, Node.js Express, atau Go), dan *Database Server* (misal: PostgreSQL, MySQL, atau Redis).
2. **Implementasi File `docker-compose.yml`:**
   - Mendefinisikan ketiga layanan dalam satu file orkestrasi `docker-compose.yml`.
   - Mengatur isolasi jaringan internal (*Docker bridge network*) antar-kontainer.
   - Mengatur persistensi data (*Docker Named Volume*) pada layanan database agar data tidak hilang saat kontainer di-restart.
3. **Manajemen Sumber Daya (*Resource Quotas*):**
   - Mengatur batas maksimal memori (`mem_limit` atau `deploy.resources.limits.memory`) untuk masing-masing layanan (misal: Nginx = 128 MB, Backend = 256 MB, Database = 512 MB).
   - Mengatur kuota pemakaian CPU (`cpus` atau `deploy.resources.limits.cpus`) secara terukur untuk mencegah fenomena *Noisy Neighbor*.
4. **Pengujian Beban (*Load / Stress Testing*):**
   - Menghantam server dengan uji beban menggunakan *tools* seperti Apache Benchmark (`ab -n 2000 -c 100 http://localhost/`), Locust, atau `k6`.
5. **Monitoring dan Evaluasi Kinerja:**
   - Merekam dinamika utilisasi CPU, memori, I/O, dan status kontainer selama uji beban berlangsung menggunakan `docker stats`, `htop`, atau `ctop`.
   - Menganalisis apakah terjadi *CPU Throttling*, pelonjakan *Load Average*, atau penghentian paksa oleh *OOM Killer*.
6. **Penyusunan Laporan Teknis & Presentasi:**
   - Menyusun naskah laporan sesuai format baku [`Format_Laporan_Tugas_Besar.md`](../Minggu_15_Monitoring_dan_Evaluasi_Kinerja_Sistem/Format_Laporan_Tugas_Besar.md).
   - Mempersiapkan slide dan demonstrasi sistem secara langsung (*live demo*).

### c. Jadwal dan Tahapan Pengerjaan
- **Minggu ke-12:** Peluncuran RTM, pembentukan kelompok (2–3 orang), dan perumusan studi kasus aplikasi.
- **Minggu ke-13:** Penyusunan topologi, penulisan `docker-compose.yml`, dan implementasi alokasi limit memori serta CPU.
- **Minggu ke-14:** Integrasi arsitektur cloud, pengujian konektivitas antarlayanan, dan persiapan skenario uji beban.
- **Minggu ke-15:** Pelaksanaan *stress test*, pencatatan metrik monitoring, penyerahan laporan akhir, dan presentasi kelompok (demonstrasi langsung 10 menit + tanya jawab 5 menit).

### d. Luaran Tugas (*Deliverables*)
1. **Laporan Akhir Tugas Besar** dalam format `.pdf` (mengacu pada template baku).
2. **Repositori Kode / Arsip Konfigurasi** (`.zip`) yang berisi:
   - File `docker-compose.yml`
   - Direktori kode aplikasi / konfigurasi pendukung (Nginx config, Dockerfile)
   - Skrip pengujian beban
3. **Presentasi Demonstrasi Langsung** di hadapan dosen pengampu dan rekan kelas.

---

## 3. Rubrik Penilaian Proyek Akhir (Bobot: 30% Nilai Akhir Mata Kuliah)

Penilaian dilakukan secara objektif mengacu pada rubrik resmi RPS 2026:

| No | Komponen Evaluasi Proyek Akhir | Bobot (%) | Indikator Keberhasilan Penilaian |
| :---: | :--- | :---: | :--- |
| 1 | **Analisis Kebutuhan & Perumusan Masalah Sumber Daya** | **5%** | Ketajaman analisis skenario kebutuhan layanan, pemetaan risiko bottleneck, dan justifikasi teknis pemilihan spesifikasi resource. |
| 2 | **Desain Arsitektur Solusi & Alokasi Sumber Daya** | **7%** | Ketepatan diagram arsitektur multi-tier, rasionalitas penetapan kuota CPU (`cpus`) dan RAM (`mem_limit`) untuk setiap lapisan layanan. |
| 3 | **Implementasi & Keberfungsian Solusi (`docker-compose`)** | **8%** | Keberhasilan eksekusi `docker compose up`, isolasi network, persistensi volume database, dan kebersihan sintaks konfigurasi. |
| 4 | **Pengujian Beban, Monitoring, & Analisis Kinerja** | **5%** | Metodologi stress test yang terukur, kelengkapan data metrik `docker stats`/`htop`, dan kedalaman analisis fenomena sistem (throttling/OOM). |
| 5 | **Dokumentasi, Presentasi, Komunikasi, & Kolaborasi** | **5%** | Kerapian laporan teknis, keterbukaan deklarasi pemanfaatan Generative AI, kelancaran demonstrasi live system, dan penguasaan tanya jawab. |
| **Total** | **Bobot Kumulatif Proyek Akhir** | **30%** | |

---

**Dosen Pengampu Mata Kuliah:**  
**M. Riza Nurtam, M.Kom**  
NIP. 197910232008121002
