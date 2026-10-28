# Bahan Ajar: Minggu 14 - Manajemen Sumber Daya Cloud dan Skalabilitas

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer – Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan:** 14 (Empat Belas) — Semester 5 / 2 SKS  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Bahan Kajian:** BK02/MP-14  

---

## 1. Capaian Pembelajaran (Sub-CPMK) & Indikator

Pada akhir sesi perkuliahan ini, mahasiswa diharapkan mampu:
1. **Menjelaskan 5 karakteristik esensial komputasi awan** menurut National Institute of Standards and Technology (NIST).
2. **Membedakan model layanan cloud**: *Infrastructure as a Service* (IaaS), *Platform as a Service* (PaaS), dan *Software as a Service* (SaaS) ditinjau dari pembagian tanggung jawab alokasi sumber daya (*Shared Responsibility Model*).
3. **Menganalisis komparasi skalabilitas vertikal (*Scale Up*) vs skalabilitas horizontal (*Scale Out*)**.
4. **Menguraikan peran dan algoritma penyeimbang beban (*Load Balancing*)**: *Round Robin*, *Least Connections*, dan *IP Hash (Sticky Session)*.
5. **Merancang mekanisme elastisitas otomatis (*Auto-Scaling*)** berbasis metrik ambang batas (*threshold metrics*) dan periode pendinginan (*cooldown period*).
6. **Menyusun arsitektur sistem multi-tingkat (*Multi-Tier High Availability Architecture*)** yang memisahkan lapisan aplikasi *Stateless* dengan lapisan basis data *Stateful*.

---

## 2. Paradigma Komputasi Awan dan Karakteristik NIST

Dalam era modern, manajemen sumber daya sistem telah bergeser dari pengelolaan satu server fisik lokal (*On-Premise*) menuju alokasi dinamis sumber daya tervirtualisasi di komputasi awan (*Cloud Computing*).

Menurut definisi resmi **NIST (National Institute of Standards and Technology)**, komputasi awan memiliki 5 karakteristik mutlak:
1. **On-Demand Self-Service:** Pengguna dapat memesan dan mengonfigurasi kapasitas CPU, memori, dan storage secara otomatis melalui antarmuka web/API tanpa intervensi manual penyedia layanan.
2. **Broad Network Access:** Sumber daya dapat diakses dari mana saja melalui jaringan standar menggunakan berbagai perangkat (laptop, smartphone, workstation).
3. **Resource Pooling:** Sumber daya komputasi fisik milik penyedia awan dikumpulkan bersama (*pooled*) untuk melayani banyak pelanggan secara multi-tenant secara dinamis.
4. **Rapid Elasticity (Elastisitas Cepat):** Kapasitas sumber daya dapat ditambah atau dikurangi secara instan dan otomatis sesuai dinamika lonjakan beban kerja.
5. **Measured Service (Layanan Terukur):** Penggunaan sumber daya (jam vCPU, gigabyte RAM, bandwidth jaringan) dipantau, dikontrol, dan ditagih secara transparan berbasis pemakaian aktual (*Pay-as-you-go*).

---

## 3. Spektrum Model Layanan Cloud (IaaS vs PaaS vs SaaS)

Model layanan awan menentukan seberapa banyak lapisan sumber daya yang dikelola oleh pengguna versus dikelola oleh penyedia awan (*Cloud Provider*):

```text
+-----------------------+     +-----------------------+     +-----------------------+
|  IaaS (Infrastructure)|     |  PaaS (Platform)      |     |  SaaS (Software)      |
+-----------------------+     +-----------------------+     +-----------------------+
| Aplikasi      (User)  |     | Aplikasi      (User)  |     | Aplikasi      (Cloud) |
| Data          (User)  |     | Data          (User)  |     | Data          (Cloud) |
| Runtime       (User)  |     +-----------------------+     | Runtime       (Cloud) |
| Middleware    (User)  |     | Runtime       (Cloud) |     | Middleware    (Cloud) |
| OS & Kernel   (User)  |     | OS & Kernel   (Cloud) |     | OS & Kernel   (Cloud) |
+-----------------------+     | Virtualisasi  (Cloud) |     | Virtualisasi  (Cloud) |
| Virtualisasi  (Cloud) |     | Server Fisik  (Cloud) |     | Server Fisik  (Cloud) |
| Server Fisik  (Cloud) |     | Storage & Net (Cloud) |     | Storage & Net (Cloud) |
+-----------------------+     +-----------------------+     +-----------------------+
Contoh: AWS EC2, GCP Compute   Contoh: Cloud Run, Heroku     Contoh: Gmail, Microsoft 365
```

- **IaaS:** Memberikan kendali penuh atas mesin virtual dan konfigurasi sistem operasi kepada administrator sistem.
- **PaaS:** Membebaskan pengembang dari beban pemeliharaan kernel, patching OS, dan konfigurasi jaringan, memungkinkan fokus murni pada kode aplikasi dan data.

---

## 4. Strategi Skalabilitas: Vertical vs Horizontal Scaling

Ketika beban lalu lintas pengguna melonjak drastis (misal saat masa KRS mahasiswa atau acara belanja *Flash Sale*), sistem menghadapi ancaman kelangkaan sumber daya. Dua pendekatan utama untuk mengatasinya adalah:

```text
SKALABILITAS VERTIKAL (Scale Up)          SKALABILITAS HORIZONTAL (Scale Out)
+-------------------------------+         +--------+   +--------+   +--------+
|       1 SERVER RAKSASA        |         | Server |   | Server |   | Server |
|   (Upgrade CPU & RAM Fisik)   |         | Node 1 |   | Node 2 |   | Node 3 |
|                               |         +--------+   +--------+   +--------+
| Risiko: Plafon hardware batas |             ^            ^            ^
| akhir & Downtime saat upgrade |             |------------|------------|
| (Single Point of Failure/SPOF)|                  [ LOAD BALANCER ]
+-------------------------------+         (Trafik dibagi, High Availability)
```

| Parameter | Vertical Scaling (Scale Up) | Horizontal Scaling (Scale Out) |
| :--- | :--- | :--- |
| **Definisi** | Menambah kapasitas CPU core, RAM, dan disk pada **1 mesin tunggal yang sama**. | Menambah **jumlah unit mesin server/kontainer** baru yang bekerja bersama. |
| **Batas Maksimal** | Terbatas oleh plafon spesifikasi fisik motherboard tertinggi yang ada di pasaran. | **Hampir tanpa batas** (dapat menambah puluhan hingga ribuan instans). |
| **Ketersediaan (*Availability*)** | Memiliki titik kegagalan tunggal (*Single Point of Failure*); jika mesin mati, seluruh sistem padam. | **Tinggi (*High Availability*)**; jika 1 instans mati, instans lain tetap melayani. |
| **Downtime** | Membutuhkan *downtime* (restart) saat memperbesar ukuran VM/server. | **Zero-Downtime**; penambahan instans baru dilakukan secara mulus di belakang load balancer. |
| **Biaya** | Sangat mahal secara eksponensial di kelas server spesifikasi ekstrem. | Lebih hemat biaya karena memanfaatkan banyak unit server komoditas berukuran kecil. |

---

## 5. Peran dan Algoritma Load Balancing

**Load Balancer (Penyeimbang Beban)** adalah simpul infrastruktur yang bertindak sebagai pemandu lalu lintas di depan kumpulan server aplikasi, mendistribusikan permintaan klien secara merata agar tidak ada satu server pun yang kewalahan.

### Algoritma Distribusi Beban:
1. **Round Robin:** Mendistribusikan permintaan secara bergantian berurutan ke setiap server ($1 \to 2 \to 3 \to 1 \to \dots$). Sangat efektif jika seluruh mesin backend memiliki spesifikasi perangkat keras yang identik.
2. **Least Connections:** Mengarahkan permintaan baru ke server yang saat itu memiliki jumlah koneksi aktif paling sedikit. Sangat ideal untuk aplikasi dengan durasi sesi transaksi yang bervariasi (seperti streaming atau transaksi database).
3. **IP Hash (Session Affinity / Sticky Sessions):** Menggunakan fungsi hash dari alamat IP klien untuk memastikan bahwa permintaan dari satu pengguna tertentu akan selalu diarahkan ke server backend yang sama, menjaga persistensi sesi login.

### Mekanisme Pemeriksaan Kesehatan (Health Checks):
Load Balancer mengirimkan sinyal ping atau request HTTP `GET /health` berkala (misal tiap 5 detik) ke setiap server backend. Jika sebuah server tidak merespons (mengalami crash atau OOM), Load Balancer secara otomatis mencoret server tersebut dari daftar aktif dan mengalihkan seluruh lalu lintas ke server yang sehat tanpa disadari oleh pengguna.

---

## 6. Otomatisasi Elastisitas Sumber Daya (Auto-Scaling)

Auto-scaling adalah fitur komputasi awan yang secara otomatis menambah (*Scale-Out*) atau mengurangi (*Scale-In*) jumlah instans komputasi aktif berdasarkan pemantauan metrik beban nyata secara real-time.

```mermaid
graph TD
    Monitor[Cloud Monitoring: Cek Rata-Rata CPU Seluruh Instans] --> Check{Rata-Rata CPU > 75%?}
    Check -- Ya (Beban Tinggi) --> ScaleOut[Trigger Auto-Scaler: Tambah +2 Instans VM/Kontainer Baru]
    ScaleOut --> Cooldown[Masuk Cooldown Period 300 detik]
    Check -- Tidak --> CheckLow{Rata-Rata CPU < 25%?}
    CheckLow -- Ya (Sepi Pengunjung) --> ScaleIn[Trigger Auto-Scaler: Kurangi 1 Instans (Hemat Biaya)]
    CheckLow -- Tidak --> Normal[Kapasitas Sesuai, Pertahankan]
```

### Parameter Kunci Auto-Scaling:
- **Min Instances & Max Instances:** Menetapkan batas jumlah server paling sedikit (misal minimal 2 instans demi redundansi) dan paling banyak (misal maksimal 10 instans demi membatasi anggaran biaya).
- **Trigger Metrics:** Metrik yang dijadikan acuan, umumnya rata-rata utilisasi CPU (>75%), penggunaan memori, atau panjang antrean permintaan HTTP.
- **Cooldown Period (Periode Pendinginan):** Jeda waktu tunggu (misal 5 menit) setelah penambahan server baru sebelum sistem diizinkan melakukan scaling berikutnya. Hal ini mencegah terjadinya **Osilasi / Flapping** (server ditambah dan dihapus berulang-ulang dalam tempo cepat akibat fluktuasi sesaat).

---

## 7. Arsitektur Multi-Tier Berkeandalan Tinggi (High Availability)

Kunci sukses arsitektur cloud adalah memisahkan lapisan aplikasi berdasarkan persistensi data:

```text
[ INTERNET: 5.000 MAHASISWA LOGIN KRS ]
                  |
                  v
       [ CLOUD LOAD BALANCER ]
                  |
    +-------------+-------------+
    |                           |
    v (HTTP Request)            v (HTTP Request)
+-----------------------+   +-----------------------+
| WEB / BACKEND API #1  |   | WEB / BACKEND API #2  |  <--- STATELESS LAYER
| (Kontainer Nginx+App) |   | (Kontainer Nginx+App) |       (Dapat di-auto-scale bebas)
+-----------------------+   +-----------------------+
            \                   /
             \ (Query SQL)     / (Query SQL)
              v               v
    +-----------------------------------------------+
    |         DATABASE CLUSTER (STATEFUL)           |
    |  +-------------------+  +-------------------+ |
    |  |  DATABASE MASTER  |->|  DATABASE REPLICA | |  <--- DATA PERSISTENCE LAYER
    |  |  (Operasi WRITE)  |  |  (Operasi READ)   | |       (Data tersimpan aman)
    |  +-------------------+  +-------------------+ |
    +-----------------------------------------------+
```

1. **Stateless Web/App Tier:** Kontainer aplikasi web tidak menyimpan data sesi atau file penting di disk lokalnya (data sesi disimpan di memory cache bersama seperti Redis). Hal ini membuat kontainer web dapat dibuat, digandakan, atau dimusnahkan kapan saja oleh auto-scaler tanpa risiko data hilang.
2. **Stateful Database Tier:** Data akademik disimpan di cluster database terpisah yang menerapkan replikasi **Master-Replica**:
   - Transaksi modifikasi data (mahasiswa klik "Simpan KRS") dikirim ke **Database Master**.
   - Permintaan pembacaan data (melihat jadwal kuliah, melihat nilai) dialihkan ke **Database Replica**, mencegah database utama mengalami kelumpuhan koneksi.

---

## 8. Rangkuman Materi

1. Komputasi awan menyediakan manajemen sumber daya dengan karakteristik **Rapid Elasticity** dan model pembayaran berbasis pemakaian.
2. **Horizontal Scaling (Scale Out)** jauh lebih unggul dibandingkan Vertical Scaling dalam menjamin elastisitas dan *High Availability*.
3. **Load Balancer** mendistribusikan beban secara dinamis melalui algoritma seperti *Round Robin* dan mengisolasi kegagalan lewat *Health Checks*.
4. **Auto-Scaling** menyesuaikan jumlah instans komputasi secara real-time terhadap grafik beban, dilindungi oleh *Cooldown Period*.
5. Pemisahan arsitektur antara **Stateless Application Layer** dan **Stateful Database Layer** adalah standar industri dalam merancang sistem skala besar yang tangguh.

---

## 9. Referensi Pustaka

- **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson. **Chapter 7: Virtualization and the Cloud — Cloud Architecture & Scaling (pp. 515–530).**
- **Nemeth, E., et al. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson. **Chapter 29: Cloud Computing Architecture & Management (pp. 887–916).**
- **NIST Special Publication 800-145.** *The NIST Definition of Cloud Computing*.
