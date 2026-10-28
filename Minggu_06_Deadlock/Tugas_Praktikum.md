# Tugas Praktikum Minggu 6: Analisis RAG dan Banker's Algorithm

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 6  
**Bobot Penilaian Pertemuan:** 3%  

---

## 1. Rincian Tugas
Selesaikan seluruh instruksi latihan pada [`Praktikum.md`](./Praktikum.md):
1. **Studi Kasus 1 — Resource Allocation Graph (RAG):**
   - Gambar diagram RAG untuk P1, P2, P3 dan R1 (1 instans), R2 (2 instans), R3 (1 instans).
   - Analisis keberadaan *cycle* (`P1 -> R2 -> P2 -> R1 -> P1`) dan jelaskan mengapa keberadaan *cycle* pada sumber daya dengan lebih dari 1 instans (`R2`) belum tentu menyebabkan *Deadlock* (perhatikan peran P3!).
2. **Studi Kasus 2 — Banker's Algorithm:**
   - Tabel perhitungan *Total Allocation*, vektor *Available* awal `(A, B, C)`, dan matriks *Need* untuk P0 s.d. P4.
   - Simulasi iterasi *Safety Algorithm* langkah demi langkah beserta pembaruan vektor `Work / Available` setiap kali sebuah proses selesai dieksekusi.
   - Penulisan *Safe Sequence* akhir (contoh: `<P1, P3, P4, P0, P2>` atau urutan valid lainnya).

## 2. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan dalam format `.pdf` ke sistem e-Learning sebelum pertemuan Minggu ke-7.
