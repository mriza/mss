# Modul Latihan: Simulasi Algoritma Page Replacement

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 9

---

## 1. Tujuan Latihan
Mahasiswa mampu menghitung dan membandingkan tingkat efisiensi dari berbagai algoritma *Page Replacement* (FIFO, LRU, dan Optimal) berdasarkan jumlah *Page Fault* yang dihasilkan.

## 2. Dasar Teori
Dalam sistem *Demand Paging*, ketika RAM sudah penuh dan sebuah proses membutuhkan *Page* baru dari disk, OS harus melakukan *Page Replacement* (Penggantian Page). Kinerja algoritma diukur dari seberapa sedikit *Page Fault* yang terjadi untuk suatu *Reference String* (urutan panggilan memori) tertentu.

## 3. Studi Kasus (Soal Latihan)
Diketahui sebuah program melakukan panggilan data ke memori (*Reference String*) dengan urutan nomor *Page* sebagai berikut:

**7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2, 1, 2, 0, 1, 7, 0, 1**

Asumsikan bahwa sistem (RAM) hanya memiliki alokasi memori fisik sebanyak **3 Frames (3 slot kosong)** untuk proses ini. Pada awalnya, semua *frame* masih kosong.

**Instruksi:**
Gambarkan tabel pergerakan *Page* pada *Frames* dan hitung total jumlah **Page Fault** untuk masing-masing algoritma di bawah ini!

### Latihan A: FIFO (First In, First Out)
- **Aturan:** *Page* yang diganti (dikeluarkan) adalah *page* yang paling pertama dimasukkan ke dalam *frame* (paling tua).
- Susun tabel dari langkah awal (memasukkan 7, 0, 1) hingga selesai, tandai langkah mana saja yang menghasilkan *Page Fault*!

### Latihan B: LRU (Least Recently Used)
- **Aturan:** *Page* yang diganti adalah *page* yang paling lama **tidak diakses/dipanggil** di masa lalu.
- Susun tabel pergerakan *frame* dan hitung total *Page Fault*-nya!

### Latihan C: Optimal Page Replacement
- **Aturan:** *Page* yang diganti adalah *page* yang **paling lama tidak akan diakses di masa depan**. (Anda harus melihat ke sisa deretan angka di depan).
- Susun tabel pergerakan *frame* dan hitung total *Page Fault*-nya!

## 4. Evaluasi dan Laporan Praktikum
1. Tuliskan kesimpulan Anda: Algoritma mana yang menghasilkan *Page Fault* paling sedikit (terbaik) dan mana yang paling banyak (terburuk) pada studi kasus di atas?
2. Apakah Algoritma Optimal bisa diimplementasikan ke dalam kode Sistem Operasi sungguhan di dunia nyata? Berikan analisis/alasan Anda!
3. (Tugas Tambahan) Jika ukuran slot ditambah menjadi **4 Frames**, ujilah kembali dengan metode FIFO. Apakah jumlah *Page Fault*-nya berkurang, bertambah, atau tetap? *(Fenomena ini dikenal sebagai Belady's Anomaly jika ternyata bertambah).*
