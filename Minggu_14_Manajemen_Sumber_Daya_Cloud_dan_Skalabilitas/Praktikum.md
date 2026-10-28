# Modul Latihan: Konsep Dasar Load Balancing & Arsitektur Cloud

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 14

---

## 1. Tujuan Latihan
Mahasiswa mampu merancang diagram arsitektur manajemen *resource* sistem secara komprehensif, mengadopsi prinsip *Horizontal Scaling* dan *High Availability* di era Cloud Computing.

## 2. Dasar Teori
Dalam arsitektur *Cloud*, manajemen sumber daya (*Resource Management*) tidak lagi terfokus pada satu mesin (seperti *CPU Scheduling* atau *Memory Paging* pada OS lokal), melainkan bergeser pada penyebaran beban (*Load Balancing*) lintas mesin virtual untuk memastikan elastisitas (*Auto-Scaling*) dan keandalan sistem.

## 3. Studi Kasus Perancangan Sistem (Tugas Desain Arsitektur)

Sistem Informasi Akademik (SIAKAD) di kampus Anda setiap awal semester (masa KRS-an) selalu mengalami kendala server lambat (*down*) karena tiba-tiba ribuan mahasiswa mengakses sistem di detik yang sama (*Spike Traffic*).

Dahulu kampus hanya menggunakan 1 buah Server Fisik Besar **(Scale Up/Vertical)**. Namun pendekatan ini ternyata masih gagal dan SIAKAD tetap macet akibat koneksi *database* *timeout*.

Tahun ini, kampus memutuskan memigrasikan SIAKAD ke *Cloud Provider* (misalnya Google Cloud atau AWS) agar bisa menggunakan metode **Scale Out (Horizontal Scaling)**.

**Tugas Anda:**
Rancanglah sebuah desain / *blueprint* arsitektur (dalam bentuk gambar blok diagram sederhana) yang menggunakan konsep **Load Balancer**, **Virtual Machine (Web Server)**, dan **Database Server (Cluster/Terpisah)** agar SIAKAD tidak mati lagi saat KRS-an. 

*Gunakan aplikasi gratis seperti `draw.io` (app.diagrams.net), Visio, atau coret tangan di atas kertas rapi lalu difoto.*

### Syarat dan Aturan Diagram:
1. Pastikan pengunjung (Mahasiswa) tidak langsung menyentuh *Web Server*, melainkan melewati *Load Balancer* terlebih dahulu.
2. Gambarkan setidaknya **3 buah instans Virtual Machine** atau Kontainer (sebagai Web Server) di belakang *Load Balancer* tersebut.
3. Gambarkan blok/sistem **Auto-Scaler** (Kapan kondisi VM akan bertambah jumlahnya, dan kapan akan dikurangi?).
4. Gambarkan **1 buah Database Master** dan **1 buah Database Slave/Replica** (jangan gabungkan *database* di dalam VM Web Server yang sama!).

## 4. Laporan Praktikum
1. Kumpulkan gambar diagram yang Anda buat.
2. Di bawah gambar, berikan **paragraf penjelasan alur kerja sistem tersebut**: (Mulai dari Mahasiswa klik tombol KRS -> menuju Load Balancer -> lalu ke VM nomor sekian -> lalu menyimpan data di Database, dan seterusnya).
3. Jelaskan skenario di sistem Anda: Apa yang akan otomatis terjadi (bagaimana sistem bereaksi) jika seketika 5.000 mahasiswa login bersamaan hingga penggunaan memori ketiga VM menembus 90%?
