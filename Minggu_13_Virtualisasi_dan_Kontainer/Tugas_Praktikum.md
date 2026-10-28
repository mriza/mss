# Tugas Praktikum & Instrumen Penilaian Minggu 13: Virtualisasi dan Kontainer (Docker)

**Mata Kuliah:** Manajemen Sumberdaya Sistem  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan Ke-:** 13  
**Bobot Penilaian Pertemuan:** 10%  

---

## 1. Tugas Praktikum Mingguan
Dokumentasikan seluruh langkah kerja pada [`Praktikum.md`](./Praktikum.md) (Bagian A, B, dan C) sesuai [`Format_Laporan_Praktikum.md`](../Format_Laporan_Praktikum.md), kemudian jawab pertanyaan berikut:
1. **Analisis Metrik `docker stats`:** Lampirkan *screenshot* dari hasil perintah `sudo docker stats web_terbatas` pada langkah C.2 dan jelaskan arti masing-masing kolom (`CONTAINER ID`, `NAME`, `CPU %`, `MEM USAGE / LIMIT`, `MEM %`, `NET I/O`, `BLOCK I/O`, `PIDS`).
2. **Urgensi Pembatasan Sumber Daya (*Resource Isolation*):** Mengapa pembatasan penggunaan CPU (`--cpus`) dan Memori (`-m`) pada kontainer aplikasi server sangat penting dalam Manajemen Sumberdaya Sistem (kaitkan dengan fenomena *Noisy Neighbor* dan *OOM Killer*)?
3. **Tantangan Kebijakan Restart Otomatis (*Restart Policy*):** Praktikkan cara menjalankan kontainer Nginx yang otomatis melakukan *restart* ketika mengalami *crash* atau ketika mesin server di-*reboot* (parameter `--restart unless-stopped` atau `--restart always`). Lampirkan perintah dan bukti verifikasinya (`docker inspect`).

---

## 2. Rubrik Penilaian Proyek Praktikum (Virtualisasi / Docker)
Digunakan untuk mengevaluasi tugas praktikum mahasiswa pada pertemuan terkait *Virtual Machines* atau *Containerization*.

| Kriteria | Sangat Baik (80-100) | Baik (70-79.9) | Cukup (60-69.9) | Kurang (<60) | Bobot |
|---|---|---|---|---|---|
| **Pemahaman Konsep** | Menjelaskan konsep dengan sangat jelas dan akurat. | Menjelaskan konsep dengan baik, ada sedikit kekurangan minor. | Konsep dasar dipahami, namun penjelasan kurang terstruktur. | Gagal menjelaskan konsep dasar dengan benar. | 30% |
| **Implementasi Teknis**| Konfigurasi berhasil tanpa error, efisien, sesuai panduan. | Konfigurasi berhasil, terdapat error kecil yang bisa diatasi. | Konfigurasi kurang sempurna, beberapa fungsi tidak berjalan. | Gagal melakukan konfigurasi/setup dasar. | 40% |
| **Laporan & Dokumentasi**| Laporan lengkap, log/screenshot disertakan jelas, analisis tajam. | Laporan cukup lengkap, disertai dokumentasi yang cukup. | Laporan ala kadarnya, dokumentasi kurang relevan. | Tidak ada laporan atau dokumentasi tidak disertakan. | 30% |
