# Modul Latihan: Strategi Alokasi Memori dan Paging

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 7

---

## 1. Tujuan Latihan
Mahasiswa mampu mensimulasikan mekanisme alokasi memori berdekatan (*Contiguous Allocation*) dengan berbagai algoritma, serta mampu melakukan translasi alamat logika ke fisik pada skema *Paging*.

## 2. Latihan 1: Contiguous Allocation (First-Fit, Best-Fit, Worst-Fit)
Diberikan status memori utama saat ini memiliki urutan lubang (blok memori kosong) dengan kapasitas sebagai berikut (dalam Kilobytes/KB):
**[100 KB], [500 KB], [200 KB], [300 KB], [600 KB]**

Terdapat 4 buah proses yang datang secara berurutan dan meminta memori sebesar:
- P1 = 212 KB
- P2 = 417 KB
- P3 = 112 KB
- P4 = 426 KB

**Instruksi:**
Gambarkan status akhir lubang memori setelah keempat proses tersebut dialokasikan menggunakan algoritma berikut. Jika ada proses yang tidak kebagian memori (karena fragmentasi eksternal), sebutkan proses yang mana!

1. **Simulasi First-Fit:** (Proses dialokasikan pada lubang PERTAMA yang ukurannya mencukupi).
2. **Simulasi Best-Fit:** (Proses dialokasikan pada lubang yang ukurannya PALING PAS / sisanya paling kecil).
3. **Simulasi Worst-Fit:** (Proses dialokasikan pada lubang yang ukurannya PALING BESAR).
4. Dari ketiga algoritma di atas untuk kasus ini, manakah yang paling optimal sehingga semua proses bisa masuk?

---

## 3. Latihan 2: Translasi Alamat pada Sistem Paging
Sebuah sistem komputer memiliki arsitektur sebagai berikut:
- Menggunakan skema *Paging* murni.
- Kapasitas **Logical Memory** adalah 16 KB.
- Kapasitas **Physical Memory** adalah 32 KB.
- Ukuran 1 *Page* (dan 1 *Frame*) adalah **4 KB** (4096 bytes).

**Instruksi:**
1. Ada berapa jumlah *Pages* yang dimiliki sistem ini secara logika? *(Cara: Logical Memory / Page Size)*.
2. Ada berapa jumlah *Frames* fisik yang dimiliki sistem ini?
3. Diketahui sebuah **Page Table** untuk Proses A berisi pemetaan berikut:
    - Page 0 -> Frame 5
    - Page 1 -> Frame 2
    - Page 2 -> Frame 7
    - Page 3 -> Frame 0
   
   Jika CPU meminta instruksi pada alamat logika (**Logical Address**) `8200` (dalam hitungan desimal byte), hitunglah **Physical Address**-nya secara fisik di RAM!
   
   **Hint Cara Menghitung:**
    - Cari tahu alamat `8200` ini jatuh di *Page* nomor berapa. (Nomor Page `p` = Logical Address / Page Size).
    - Cari tahu *Offset* (*sisa byte*)-nya. (Offset `d` = Logical Address % Page Size).
    - Lihat di tabel, *Page* `p` berada di *Frame* nomor berapa (`f`).
    - Rumus Physical Address = (`f` * Page Size) + `d`.

---

## 4. Laporan Praktikum
Susun jawaban perhitungan Latihan 1 dan Latihan 2 dengan urutan langkah (cara kerja) yang terstruktur agar mudah dinilai. Kumpulkan pada *platform e-Learning* sesuai tenggat waktu.
