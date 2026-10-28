# Bahan Ajar: Minggu 5 - Sinkronisasi dan Konkurensi

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer – Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan:** 5 (Lima) — Semester 5 / 2 SKS  
**Dosen Pengampu:** Melissa Triandini, M.Kom / Tim Dosen  
**Bahan Kajian:** BK02/MP-05  

---

## 1. Capaian Pembelajaran (Sub-CPMK) & Indikator

Pada akhir sesi perkuliahan ini, mahasiswa diharapkan mampu:
1. **Menganalisis penyebab fenomena *Race Condition*** pada eksekusi proses/thread konkuren yang berbagi data bersama (*Shared Memory*).
2. **Merumuskan *The Critical-Section Problem*** dan membuktikan pemenuhan 3 kriteria solusi mutlak: *Mutual Exclusion*, *Progress*, dan *Bounded Waiting*.
3. **Menjelaskan dukungan instruksi perangkat keras atomik** (*Test-and-Set*, *Compare-and-Swap*).
4. **Menerapkan mekanisme penguncian *Mutex Lock*** dan menganalisis trade-off antara *Spinlock (Busy Waiting)* vs *Sleep-Lock*.
5. **Mengimplementasikan *Counting Semaphore* dan *Binary Semaphore*** menggunakan operasi atomik `wait()` dan `signal()`.
6. **Menganalisis solusi masalah klasik sinkronisasi**: *Bounded-Buffer (Producer-Consumer)*, *Readers-Writers*, dan *Dining-Philosophers*.
7. **Memahami konsep abstraksi sinkronisasi tingkat tinggi (*Monitors*)** dan *Condition Variables*.

---

## 2. Latar Belakang Konkurensi dan Bahaya Race Condition

Dalam arsitektur sistem operasi modern, thread atau proses konkuren sering kali perlu berbagi sumber daya memori yang sama (misalnya variabel global, tabel basis data, atau buffer komunikasi). 

Ketika dua alur eksekusi membaca dan memodifikasi data bersama secara simultan tanpa koordinasi, urutan instruksi mesin dapat saling bersilangan (*interleaved*), menghasilkan nilai akhir yang salah dan tidak dapat diprediksi. Kondisi ini disebut **Race Condition**.

### Ilustrasi Race Condition pada Tingkat Instruksi Mesin:
Misalkan terdapat variabel bersama `saldo = 100`. Dua thread melakukan transaksi bersamaan:
- **Thread 1:** Menyetor uang 50 (`saldo = saldo + 50`)
- **Thread 2:** Menarik uang 20 (`saldo = saldo - 20`)

Secara matematika, hasil akhir seharusnya adalah `130`. Namun di tingkat CPU, operasi tersebut diterjemahkan menjadi 3 instruksi mesin:

```text
Thread 1 (Menyetor 50):                  Thread 2 (Menarik 20):
1. LOAD  R1, [saldo]                     1. LOAD  R2, [saldo]
2. ADD   R1, 50                          2. SUB   R2, 20
3. STORE [saldo], R1                     3. STORE [saldo], R2
```

Jika terjadi pergantian konteks (*context switch*) di tengah-tengah eksekusi:
1. Waktu $t_1$: Thread 1 mengeksekusi `LOAD R1, [saldo]` $\rightarrow$ $R1 = 100$.
2. Waktu $t_2$: Thread 1 mengeksekusi `ADD R1, 50` $\rightarrow$ $R1 = 150$. (CPU diputus oleh timer interrupt!).
3. Waktu $t_3$: Thread 2 masuk dan mengeksekusi `LOAD R2, [saldo]` $\rightarrow$ Nilai saldo di RAM masih `100`, maka $R2 = 100$.
4. Waktu $t_4$: Thread 2 mengeksekusi `SUB R2, 20` $\rightarrow$ $R2 = 80$.
5. Waktu $t_5$: Thread 2 mengeksekusi `STORE [saldo], R2` $\rightarrow$ Saldo di RAM ditulis menjadi `80`.
6. Waktu $t_6$: Thread 1 kembali masuk dan mengeksekusi `STORE [saldo], R1` $\rightarrow$ Saldo di RAM ditulis menjadi `150`!

**Bencana Data:** Nilai penarikan Thread 2 hilang sepenuhnya (*lost update*). Sistem mencatat saldo 150, padahal seharusnya 130!

---

## 3. Masalah Bagian Kritis (The Critical-Section Problem)

Bagian kode di dalam suatu program yang mengakses dan memanipulasi data bersama disebut **Critical Section**.

```text
do {
    entry section       // Meminta izin masuk ke Critical Section (Locking)
        critical section    // Manipulasi data bersama (Shared Data)
    exit section        // Melepas izin / sinyal selesai (Unlocking)
        remainder section   // Kode komputasi lain yang tidak bersinggungan
} while (true);
```

### Tiga Syarat Mutlak Solusi Critical Section:
Menurut Silberschatz et al. (2019), setiap solusi yang valid wajib memenuhi 3 persyaratan:
1. **Mutual Exclusion (Eksklusi Bersama):** Jika proses $P_i$ sedang mengeksekusi *critical section*-nya, tidak ada proses lain yang diizinkan berada di dalam *critical section* tersebut pada saat yang bersamaan.
2. **Progress (Kemajuan):** Jika tidak ada proses yang sedang berada di *critical section* dan ada beberapa proses yang ingin masuk, hanya proses-proses yang tidak berada di *remainder section* yang boleh berpartisipasi menentukan siapa yang berhak masuk berikutnya, dan keputusan ini tidak boleh ditunda tanpa batas waktu.
3. **Bounded Waiting (Penantian Terbatas):** Harus ada batas jumlah giliran proses lain yang diizinkan masuk ke *critical section* setelah sebuah proses mengajukan permintaan masuk, sebelum permintaan proses tersebut dikabulkan (mencegah terjadinya *starvation*).

---

## 4. Dukungan Perangkat Keras: Instruksi Atomik

Komputer modern menyediakan instruksi bahasa mesin khusus yang dijamin dieksekusi secara **Atomik** (tidak dapat diinterupsi di tengah jalan oleh sinyal apa pun):

1. **Test-and-Set Instruction:** Membaca nilai dari suatu lokasi memori dan langsung menggantinya dengan nilai `true` dalam satu siklus bus tak terputus.
2. **Compare-and-Swap (CAS):** Memeriksa apakah nilai memori saat ini sama dengan nilai dugaan. Jika sama, nilainya diperbarui ke nilai baru secara atomik.

Instruksi atomik tingkat rendah ini menjadi fondasi perangkat keras untuk membangun primitif sinkronisasi tingkat tinggi di sistem operasi: *Mutex* dan *Semaphore*.

---

## 5. Mutex Lock (Mutual Exclusion)

**Mutex** adalah instrumen penguncian biner sederhana. Sebuah proses harus memperoleh (*acquire*) kunci sebelum memasuki *critical section*, dan melepaskan (*release*) kunci tersebut setelah keluar.

```c
acquire() {
    while (!available)
        ; // busy wait (spinlock)
    available = false;
}

release() {
    available = true;
}
```

### Spinlock vs Sleep-Lock:
- **Spinlock (Busy Waiting):** Proses yang menunggu terus-menerus berputar (*looping*) mengecek ketersediaan kunci dalam instruksi CPU. Keuntungannya: Tidak ada overhead *context switch*, sangat cocok untuk penguncian berdurasi super singkat pada sistem multi-core.
- **Sleep-Lock / Blocking Lock:** Jika kunci tidak tersedia, kernel memindahkan proses dari status *Running* ke status *Waiting/Blocked* di antrean antrean tunggu, dan CPU dialokasikan ke proses lain. Begitu kunci dilepas, kernel membangunkannya kembali (*wakeup*). Cocok untuk operasi penguncian yang memakan waktu relatif lama (seperti operasi I/O).

---

## 6. Semaphore (Dijkstra)

Diperkenalkan oleh Edsger Dijkstra pada tahun 1965, **Semaphore** adalah variabel integer `S` yang hanya dapat diakses melalui dua operasi standar atomik yang saling berkebalikan: **`wait()`** (awalnya disebut `P` dari bahasa Belanda *proberen* / mencoba) dan **`signal()`** (awalnya disebut `V` dari *verhogen* / menaikkan).

### Definisi Operasi Atomik Standar:
```c
wait(S) {
    while (S <= 0)
        ; // tunggu (atau pindah ke blocked queue)
    S--;
}

signal(S) {
    S++;
}
```

### Jenis-Jenis Semaphore:
1. **Binary Semaphore:** Nilai integer hanya berkisar antara `0` dan `1`. Fungsinya identik dengan Mutex Lock.
2. **Counting Semaphore:** Nilai integer dapat berkisar dari `0` hingga `N` tak terbatas. Digunakan untuk mengendalikan akses ke suatu sumber daya yang memiliki sejumlah unit instans terbatas (misalnya kumpulan koneksi database atau 3 keping printer).

---

## 7. Masalah-Masalah Klasik Sinkronisasi

### A. The Bounded-Buffer Problem (Producer-Consumer)
- Terdapat kumpulan buffer berukuran tetap ($N$ slot).
- Satu atau lebih proses *Producer* menghasilkan data ke buffer, sementara proses *Consumer* mengambil data dari buffer.
- **Sinkronisasi:** Producer tidak boleh menulis jika buffer sudah penuh ($N$), dan Consumer tidak boleh membaca jika buffer kosong ($0$).
- Diselesaikan menggunakan 3 Semaphore: `mutex` (melindungi buffer), `empty` (menghitung slot kosong), dan `full` (menghitung slot terisi).

### B. The Readers-Writers Problem
- Beberapa proses membaca (*Readers*) dan beberapa memodifikasi (*Writers*) basis data bersama.
- Jika dua Reader membaca bersamaan, tidak ada masalah konsistensi. Namun jika Writer sedang menulis, tidak boleh ada proses lain (baik Reader maupun Writer lain) yang mengakses data secara bersamaan.

### C. The Dining-Philosophers Problem
- Lima filsuf duduk melingkar mengelilingi meja dengan 5 sumpit di antara mereka. Untuk makan, seorang filsuf harus memegang 2 sumpit (kiri dan kanan).
- Merupakan model representasi klasik dari masalah alokasi sumber daya di antara proses yang saling bersaing tanpa menimbulkan *Deadlock* dan *Starvation*.

---

## 8. Abstraksi Tingkat Tinggi: Monitors

Meskipun Semaphore sangat kuat, kesalahan penulisan urutan kode (misal memanggil `signal()` sebelum `wait()`, atau lupa memanggil `signal()`) dapat merusak keseluruhan sistem atau menimbulkan deadlock permanen.

Untuk mengatasi ini, bahasa pemrograman modern dan sistem operasi menyediakan konstruksi **Monitor**:
- Monitor adalah tipe data abstrak tingkat tinggi yang menjamin bahwa hanya ada satu thread yang aktif di dalam monitor pada satu waktu (*Built-in Mutual Exclusion*).
- Programmer tidak perlu memanggil *lock/unlock* secara eksplisit.
- Menggunakan variabel kondisi (**Condition Variables**) dengan metode `wait()` dan `signal()` untuk mengatur urutan penantian dan pemanggilan antar-thread.

---

## 9. Rangkuman Materi

1. **Race Condition** terjadi ketika eksekusi konkuren tanpa proteksi menghasilkan kerusakan integritas data bersama.
2. Solusi *Critical-Section* wajib memenuhi: **Mutual Exclusion**, **Progress**, dan **Bounded Waiting**.
3. **Mutex** menjamin proteksi biner (satu pemegang kunci), dapat diimplementasikan sebagai *Spinlock* (efisien untuk durasi pendek) atau *Blocking Lock*.
4. **Counting Semaphore** mengelola akses kuota terhadap sumber daya berjumlah banyak ($N$).
5. Desain sinkronisasi yang baik mencegah bahaya turunan: inkonsistensi data, *Starvation*, dan *Deadlock*.

---

## 10. Referensi Pustaka

- **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons. **Chapter 6: Synchronization Tools (pp. 257–310); Chapter 7: Synchronization Examples (pp. 317–344).**
- **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson. **Chapter 2: Interprocess Communication, Race Conditions, Mutexes & Semaphores (pp. 129–147).**
