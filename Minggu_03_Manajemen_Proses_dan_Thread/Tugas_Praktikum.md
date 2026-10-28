# Tugas Praktikum Minggu 3: Manajemen Proses di Linux

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 3  
**Bobot Penilaian Pertemuan:** 3%  

---

## 1. Instruksi Pengerjaan
Dokumentasikan seluruh percobaan pada [`Praktikum.md`](./Praktikum.md) (Bagian A, B, dan C) menggunakan struktur pada [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md), lalu jawablah pertanyaan evaluasi berikut secara lengkap pada bagian analisis/tugas laporan Anda:

1. **Sinyal Interupsi Terminal (`Ctrl + C` vs `Ctrl + Z`):** Apa perbedaan utama fungsi dari kombinasi tombol `Ctrl + C` (`SIGINT`) dengan `Ctrl + Z` (`SIGTSTP`) di terminal Linux? Bagaimana perubahan status (*Process State*) proses saat masing-masing kombinasi tombol ditekan?
2. **Hierarki Proses (`PPID`):** Cobalah jalankan perintah `ps -ef`. Apa arti kolom **PPID** pada hasil output tersebut, dan bagaimana kaitannya dengan *System Call* `fork()`?
3. **Eksperimen Terminasi Shell (`kill -9`):** Carilah sebuah proses dengan nama `bash` (gunakan `pgrep bash`). Kemudian bunuh proses tersebut menggunakan `kill -9 <PID_BASH>`. Apa yang terjadi pada terminal Anda, dan mengapa hal tersebut terjadi? Jelaskan!

## 2. Pengumpulan Laporan
- Laporan disusun sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md) lengkap dengan *screenshot* hasil eksekusi terminal.
- Dikumpulkan dalam format `.pdf` ke sistem e-Learning paling lambat H-1 sebelum pertemuan Minggu ke-4.
