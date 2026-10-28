# Tugas Praktikum Minggu 12: Proteksi Sistem dan File Permissions

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 12  
**Bobot Penilaian Pertemuan:** 2%  

---

## 1. Instruksi Pengerjaan
Dokumentasikan seluruh langkah percobaan pada [`Praktikum.md`](./Praktikum.md) (Bagian A, B, dan C) menggunakan struktur pada [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md), lalu jawablah pertanyaan analisis berikut:

1. **Analisis Permission `chmod 754 laporan.pdf`:** Jelaskan rincian izin akses yang dimiliki oleh *Owner*, *Group*, dan *Others* baik dalam representasi oktal (`7`, `5`, `4`) maupun simbolik (`r`, `w`, `x`)!
2. **Penerapan Principle of Least Privilege pada Script (`hello.sh`):** Jika Anda membuat *script bash* `hello.sh` dan hanya Anda (Pemilik) yang perlu menjalankannya, kombinasi angka oktal berapa yang **paling aman** (misal `700`) untuk perintah `chmod ___ hello.sh`? Jelaskan risiko keamanan sistem apabila administrator memberikan `chmod 777` pada file *script* yang dapat dieksekusi!
3. **Pembentukan Kelompok Tugas Besar:** Daftarkan anggota kelompok Tugas Besar Anda (2–3 orang) sesuai panduan pada [`RTM_Tugas_Besar.md`](./RTM_Tugas_Besar.md).

## 2. Pengumpulan
- Susun laporan sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md).
- Kumpulkan dalam format `.pdf` melalui sistem e-Learning sebelum pertemuan Minggu ke-13.
