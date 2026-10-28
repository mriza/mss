# Format Laporan Tugas Besar (Final Project)
**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh

---

## HALAMAN SAMPUL (COVER)
- **Judul Proyek:** (Misal: Implementasi Multi-Container Web Server dan Monitoring Resource)
- **Daftar Anggota Kelompok (Nama Lengkap & NIM):**
  1. ...
  2. ...
  3. ...
- **Nama Dosen Pengampu:** ...

---

## BAB I: PENDAHULUAN
### 1.1 Latar Belakang
*Jelaskan secara singkat skenario studi kasus proyek yang Anda buat. Mengapa sistem ini dibangun dan apa kegunaan dari masing-masing layanan (Web, Backend, DB).*

### 1.2 Tujuan Proyek
*Jelaskan tujuan teknis dari penyelesaian Tugas Besar ini (kaitkan dengan pembatasan sumber daya dan manajemen sistem).*

---

## BAB II: ARSITEKTUR SISTEM
### 2.1 Topologi / Diagram Layanan
*Buat atau gambarkan diagram arsitektur yang menunjukkan bagaimana *user* mengakses Web Server, bagaimana Web Server terhubung ke Backend, dan Backend ke Database.* (Gunakan *tools* seperti draw.io, atau cukup diagram blok sederhana).

### 2.2 Spesifikasi *Environment*
- Spesifikasi Mesin Host (OS, CPU, RAM)
- Versi Docker & Docker Compose
- *Images* Docker yang digunakan (misal: `nginx:alpine`, `python:3.9-slim`, `postgres:15`)

---

## BAB III: IMPLEMENTASI KONFIGURASI
### 3.1 Penjelasan File `docker-compose.yml`
*Lampirkan *snippet* kode dari `docker-compose.yml` Anda (jangan *screenshot*, gunakan teks *code block*). Jelaskan blok demi blok konfigurasinya (Networks, Volumes, Ports).*

### 3.2 Strategi Pembatasan Sumber Daya (*Resource Limits*)
*Jelaskan alokasi `cpus` dan `mem_limit` yang Anda terapkan pada masing-masing kontainer. Berikan argumen mengapa Anda memberikan alokasi (misal: 512MB) pada *database*, tetapi hanya (256MB) pada Web Server.*

---

## BAB IV: PENGUJIAN DAN MONITORING (*LOAD TESTING*)
### 4.1 Skenario Pengujian Beban
*Alat apa yang digunakan untuk *stress test* (Misal: Apache Benchmark `ab -n 1000 -c 100 http://localhost/`)? Berapa *requests* yang dikirimkan?*

### 4.2 Analisis Kinerja Sistem (Monitoring)
*Tampilkan *screenshot* dari `docker stats` atau `htop` **SAAT** sistem sedang dihantam *load testing**.
- **Analisis:** Apakah sistem mencapai batas limit memori/CPU yang Anda tetapkan di `docker-compose`?
- **Perilaku Sistem:** Apa yang terjadi jika limit tersebut dilewati? Apakah ada kontainer yang di-*kill* oleh OS (OOM Killer), atau hanya melambat (Throttling)?

---

## BAB V: KESIMPULAN
*Tuliskan kesimpulan menyeluruh dari proyek ini terkait efektivitas Docker dalam memanajemen sumber daya (*resource management*) dan isolasi sistem.*

---

## DAFTAR PUSTAKA
*Sebutkan sumber referensi, dokumentasi resmi, atau buku yang digunakan.*

---

## LAMPIRAN
### Lembar Deklarasi Penggunaan AI (*Generative AI Policy*)
*Hapus bagian yang tidak perlu.*
- [ ] Kelompok kami **TIDAK** menggunakan Generative AI sama sekali dalam penyusunan laporan dan kode proyek ini.
- [ ] Kelompok kami **MENGGUNAKAN** Generative AI (Misal: ChatGPT/Gemini/Copilot) dengan rincian pemakaian sebagai berikut:
  1. *Prompt/Tujuan:* (Misal: Mencari tahu cara mengatasi error "Port already in use" pada Nginx)
  2. *Prompt/Tujuan:* (Misal: Meminta penjelasan tentang parameter `mem_reservation` di Docker Compose)
  *(Catatan: Penggunaan AI untuk menghasilkan keseluruhan arsitektur atau tulisan analisis tanpa pemahaman dilarang keras).*
