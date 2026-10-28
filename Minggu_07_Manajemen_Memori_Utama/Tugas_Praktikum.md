# Tugas Praktikum Minggu 7: Strategi Alokasi Memori dan Paging

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 7  
**Bobot Penilaian Pertemuan:** 3%  

---

## 1. Rincian Tugas
Selesaikan seluruh instruksi latihan pada [`Praktikum.md`](./Praktikum.md):
1. **Latihan 1 — Contiguous Memory Allocation:**
   - Tabel/diagram alokasi blok memori `[100 KB], [500 KB], [200 KB], [300 KB], [600 KB]` untuk proses `P1 (212 KB)`, `P2 (417 KB)`, `P3 (112 KB)`, dan `P4 (426 KB)` dengan metode **First-Fit**, **Best-Fit**, dan **Worst-Fit**.
   - Sebutkan sisa ukuran masing-masing lubang (*hole*) pada setiap langkah dan identifikasi proses yang gagal dialokasikan akibat fragmentasi eksternal.
   - Kesimpulan algoritma mana yang paling optimal untuk kasus tersebut.
2. **Latihan 2 — Translasi Alamat Sistem Paging:**
   - Perhitungan jumlah *Pages* logis (`16 KB / 4 KB`) dan jumlah *Frames* fisik (`32 KB / 4 KB`).
   - Perhitungan langkah demi langkah nomor *Page* (`p`), *Offset* (`d`), nomor *Frame* (`f`), dan **Physical Address** untuk *Logical Address* `8200`.

## 2. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan dalam format `.pdf` melalui sistem e-Learning sebelum pelaksanaan UTS (Minggu ke-8).
