# Tugas Praktikum Minggu 4: Analisis dan Perhitungan Penjadwalan CPU

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 4  
**Bobot Penilaian Pertemuan:** 3%  

---

## 1. Rincian Tugas
Selesaikan seluruh studi kasus yang terdapat pada dokumen [`Praktikum.md`](./Praktikum.md):
1. **Studi Kasus 1 — First-Come, First-Served (FCFS):**
   - *Gantt Chart*, tabel CT/TAT/WT, dan *Average Waiting Time* untuk urutan `P1, P2, P3`.
   - *Gantt Chart*, tabel CT/TAT/WT, dan *Average Waiting Time* untuk urutan `P2, P3, P1`.
   - Analisis perbandingan kedua urutan terkait fenomena *Convoy Effect*.
2. **Studi Kasus 2 — Shortest Job First (SJF) Non-Preemptive:**
   - *Gantt Chart* lengkap untuk P1, P2, P3, P4 dengan waktu kedatangan berbeda.
   - Tabel perhitungan CT, TAT (`CT - AT`), WT (`TAT - BT`), serta rata-rata TAT dan WT.
3. **Studi Kasus 3 — Round Robin (RR) dengan Quantum `q = 4 ms`:**
   - *Gantt Chart* per potongan *quantum* 4 ms.
   - Tabel perhitungan CT, TAT, dan WT masing-masing proses beserta nilai rata-ratanya.

## 2. Pertanyaan Diskusi Tambahan
- Mengapa pemilihan ukuran *Time Quantum* (`q`) pada algoritma *Round Robin* tidak boleh terlalu besar dan tidak boleh terlalu kecil (kaitkan dengan *Context Switch Overhead*)?

## 3. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan file `.pdf` ke e-Learning sebelum pertemuan Minggu ke-5.
