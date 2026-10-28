# Modul Latihan: Analisis Penjadwalan Disk dan Konfigurasi RAID

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 11

---

## 1. Tujuan Latihan
Mahasiswa mampu menghitung pergerakan lengan (*head movement*) pada *magnetic disk* menggunakan algoritma *Disk Scheduling*, serta mampu membedakan efisiensi dari berbagai level RAID.

## 2. Studi Kasus 1: Penjadwalan Disk
Sebuah *disk* drive memiliki 200 silinder (*cylinders*), diberi nomor 0 hingga 199. Posisi *head* baca/tulis saat ini sedang berada di silinder **50**.

Antrian permintaan (urutan antrian *request*) akses memori saat ini adalah (dalam urutan waktu):
**82, 170, 43, 140, 24, 16, 190**

**Instruksi:**
Hitunglah total jarak (total pergerakan silinder / *total head movement*) untuk masing-masing algoritma penjadwalan berikut:
1. **FCFS (First-Come, First-Served):** *Head* melompat sesuai dengan urutan angka di atas (dari 50 ke 82, lalu 82 ke 170, dsb). Berapa total perpindahannya?
2. **SSTF (Shortest Seek Time First):** Dari 50, carilah angka terdekat dari daftar antrian. Lanjutkan mencari angka terdekat berikutnya dari posisi terakhir. Berapa total perpindahannya?
3. **SCAN (Elevator):** Asumsikan *head* saat ini sedang bergerak **naik (ke arah 199)**. *Head* melayani antrian terdekat yang searah (ke atas), menyentuh ujung akhir disk (199), lalu berbalik arah ke 0, sambil melayani antrian sisa. Berapa total perpindahannya?

---

## 3. Studi Kasus 2: Perencanaan RAID
Sebuah perusahaan berencana membangun Server Database dengan kebutuhan berikut:
1. Prioritas utama adalah kecepatan transaksi baca/tulis yang sangat tinggi.
2. Prioritas kedua adalah keandalan data (jika 1 *hardisk* rusak mendadak, server tidak boleh mati dan data tidak boleh hilang).
3. Kapasitas bersih minimal yang dibutuhkan adalah 2 Terabyte (TB).
4. Anggaran cukup besar, sehingga efisiensi jumlah disk tidak menjadi masalah utama.

Perusahaan akan membeli Hardisk berukuran **1 TB** per kepingnya.

**Instruksi:**
Berdasarkan materi kuliah:
1. Konfigurasi RAID apa yang paling cocok untuk memenuhi **semua** kriteria di atas? (RAID 0, RAID 1, RAID 5, atau RAID 10)? Berikan alasan yang jelas!
2. Jika menggunakan konfigurasi pilihan Anda, **berapa keping hardisk (masing-masing 1 TB)** yang harus dibeli agar mendapat kapasitas *bersih* (usable capacity) sebesar 2 TB?
3. Mengapa RAID 0 atau RAID 1 murni (hanya menggunakan 2 keping) tidak disarankan pada kasus ini?

---

## 4. Laporan Praktikum
Buat penyelesaian sistematis untuk Studi Kasus 1 (tunjukkan rute pergerakannya seperti `50 -> 82 -> 170 ...`) dan hitung matematikanya. Jawab pula argumentasi untuk Studi Kasus 2 dengan logika *System Administrator* yang tepat.
