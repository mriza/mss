# Modul Praktikum / Tugas: Simulasi Race Condition dan Sinkronisasi

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 5

---

## 1. Tujuan Praktikum
Mahasiswa dapat memahami secara nyata (lewat kode atau studi analitik) bagaimana fenomena *Race Condition* dapat merusak konsistensi data, serta mampu menuliskan alur sinkronisasi logika.

## 2. Studi Kasus: Transaksi Saldo (Race Condition)
Bayangkan sebuah kode *pseudo-code* sistem pemesanan tiket kereta. Sisa tiket (Variabel Global `Tiket = 1`).

Dua fungsi (Thread A dan Thread B) berjalan sangat cepat di waktu bersamaan:

```c
// Kode yang dijalankan oleh Thread A dan Thread B
void beli_tiket() {
    1. int temp = Tiket;       // Baca nilai tiket ke variabel sementara
    2. if (temp > 0) {         // Cek ketersediaan
    3.     temp = temp - 1;    // Kurangi tiket
    4.     Tiket = temp;       // Simpan kembali
    5.     print("Tiket berhasil dibeli!");
    6. } else {
    7.     print("Tiket habis!");
    8. }
}
```

## 3. Tugas Analisis (Langkah Kerja)

### Bagian A: Menemukan Race Condition
Tugas Anda adalah **membuktikan bahwa sistem ini cacat**. 
Buatlah tabel urutan eksekusi CPU (*interleaving*) di mana pada akhirnya **kedua thread berhasil mencetak "Tiket berhasil dibeli!" padahal tiket awalnya hanya ada 1**.

Gunakan format tabel berikut sebagai panduan:
| Waktu | Thread A mengeksekusi baris... | Thread B mengeksekusi baris... | Nilai variabel global `Tiket` |
|---|---|---|---|
| t1 | Baris 1: tempA = Tiket (tempA = 1) | - | 1 |
| t2 | - | Baris 1: tempB = Tiket (tempB = 1) | 1 |
| t3 | Baris 2: if (1 > 0) -> Masuk! | - | 1 |
| t4 | ... *Lanjutkan tabel ini!* ... | ... | ... |

### Bagian B: Menyelesaikan Masalah dengan Mutex Lock
Untuk mengatasi masalah pada Bagian A, kita akan menggunakan Mutex. Tersedia fungsi `acquire_lock(mutex)` dan `release_lock(mutex)`.

1. Salin ulang fungsi `beli_tiket()` di atas.
2. Tambahkan pemanggilan `acquire_lock` dan `release_lock` di baris yang tepat sehingga masalah pada Bagian A tidak mungkin terjadi lagi.
3. Sebutkan baris mana hingga baris mana yang Anda kategorikan sebagai **Critical Section**!

### Bagian C: Semaphore (Counting)
Kantin kampus memiliki 3 buah mesin Microwave. Ada 10 mahasiswa yang ingin memanaskan makanan. Kita dapat memodelkan masalah ini dengan *Counting Semaphore*.
1. Berapakah nilai awal dari Semaphore `S`?
2. Kapan fungsi `wait(S)` dipanggil oleh proses mahasiswa?
3. Kapan fungsi `signal(S)` dipanggil?
4. Apa yang terjadi jika mahasiswa ke-4 datang dan memanggil `wait(S)` ketika ketiga Microwave masih dipakai?

---

## 4. Laporan Praktikum
Jawab ketiga bagian tugas di atas (A, B, dan C) dalam bentuk dokumen laporan yang rapi. Sertakan penjelasan secukupnya untuk setiap jawaban Anda.
