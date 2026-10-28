# Tugas Praktikum Minggu 5: Simulasi Race Condition dan Sinkronisasi

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 5  
**Bobot Penilaian Pertemuan:** 3%  

---

## 1. Rincian Tugas
Selesaikan ketiga bagian tugas analisis yang terdapat pada [`Praktikum.md`](./Praktikum.md):
1. **Bagian A — Tabel Interleaving Race Condition:** Lengkapi tabel urutan waktu (`t1`, `t2`, `t3`, dst.) yang membuktikan bagaimana Thread A dan Thread B sama-sama berhasil mengeksekusi baris 5 (`print("Tiket berhasil dibeli!")`) meskipun `Tiket` awal hanya bernilai `1`.
2. **Bagian B — Perbaikan Kode dengan Mutex Lock:** Tuliskan kembali fungsi `beli_tiket()` yang telah disisipkan `acquire_lock(mutex)` dan `release_lock(mutex)`, serta jelaskan batas baris *Critical Section*-nya.
3. **Bagian C — Pemodelan Counting Semaphore:** Jawab keempat pertanyaan studi kasus 3 unit Microwave kantin kampus untuk 10 proses mahasiswa (nilai awal `S`, titik pemanggilan `wait(S)` dan `signal(S)`, serta kondisi antrian proses ke-4).

## 2. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan dalam format `.pdf` melalui sistem e-Learning sebelum pertemuan Minggu ke-6.
