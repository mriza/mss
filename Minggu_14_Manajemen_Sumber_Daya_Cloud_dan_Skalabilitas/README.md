# Minggu 14: Manajemen Sumber Daya Cloud & Skalabilitas

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Bahan Kajian / Kode:** BK02 / MP-14  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Alokasi Waktu:** 3 x 50 Menit (BT: 2x50', PT: 2x60', M: 2x60')  
**Bobot Penilaian:** 10% (Proyek Desain Arsitektur & Tahap 2 Proyek Akhir)  

---

## 1. Kemampuan Akhir yang Direncanakan (Sub-CPMK)
Mahasiswa mampu merancang alokasi sumber daya *cloud* yang skalabel dan memiliki *high availability*.

## 2. Kriteria & Indikator Penilaian
- **Kriteria:** Kesesuaian arsitektur dengan *load balancing*, *horizontal scaling*, *auto-scaling*, dan pemisahan *database*.
- **Indikator:**
  1. Menjelaskan model layanan komputasi awan (**IaaS**, **PaaS**, dan **SaaS**) serta pergeseran *CapEx* ke *OpEx*.
  2. Membedakan *Vertical Scaling* (*Scale Up*) dan *Horizontal Scaling* (*Scale Out*).
  3. Merancang *blueprint* arsitektur *Cloud* untuk Sistem Informasi Akademik (SIAKAD) dengan *Load Balancer*, *Auto-Scaler*, dan replikasi *Database* (*Master-Replica*).
  4. Menjelaskan alur distribusi *request* dan mekanisme elastisitas saat terjadi lonjakan trafik (*Spike Traffic*).

## 3. Pengalaman Belajar Mahasiswa
Merancang diagram *Load Balancer – VM/Container – Database*; menentukan skenario *auto-scaling* dan *high availability*; serta mengintegrasikan desain topologi ke dalam proyek Tugas Besar.

---

## 4. Daftar Dokumen Mingguan
1. [`Materi.md`](./Materi.md) — Bahan ajar *Cloud Computing* (IaaS, PaaS, SaaS), *Vertical vs Horizontal Scaling*, *Load Balancing*, *Auto-Scaling*, dan *Kubernetes*.
2. [`Praktikum.md`](./Praktikum.md) — Modul latihan perancangan arsitektur *Load Balancing* & *Horizontal Scaling* SIAKAD di Cloud.
3. [`Tugas_Praktikum.md`](./Tugas_Praktikum.md) — Panduan laporan desain arsitektur Cloud & kemajuan konfigurasi `docker-compose.yml` Tugas Besar Minggu 14.
