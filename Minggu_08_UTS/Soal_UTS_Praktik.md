# Naskah Soal Ujian Tengah Semester (UTS) - Praktik & Studi Kasus Terapan

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Durasi:** 90 Menit  
**Lingkungan Kerja:** Terminal Linux & Lembar Kerja Analisis  

---

## Petunjuk Pengerjaan
Ujian praktik ini menguji keterampilan administrasi proses di Linux serta ketepatan analisis pemecahan masalah manajemen sumber daya sistem (Minggu 1–7).

---

## Soal 1: Eksplorasi Hardware & Manajemen Proses Linux (30 Poin)
Di terminal Linux Anda, lakukan langkah-langkah berikut dan dokumentasikan perintah beserta hasilnya:
1. Tampilkan informasi jumlah *core* CPU, ukuran *L1/L2/L3 Cache*, dan total kapasitas RAM sistem Anda menggunakan CLI Linux.
2. Jalankan dua proses latar belakang (*background jobs*):
   ```bash
   sleep 500 &
   sleep 600 &
   ```
3. Tampilkan daftar pekerjaan (*jobs*) yang berjalan beserta **PID** dan **PPID** dari kedua proses `sleep` tersebut menggunakan perintah `ps`.
4. Pindahkan proses pertama ke *foreground* (`fg`), tunda eksekusinya (`Ctrl + Z`), lalu hentikan proses kedua secara paksa menggunakan sinyal `SIGKILL` (`-9`).

---

## Soal 2: Penghindaran Deadlock dengan Banker's Algorithm (35 Poin)
Sebuah server komputasi memiliki 3 tipe sumber daya: **R1 (9 unit), R2 (3 unit), dan R3 (6 unit)** yang digunakan oleh 4 proses (`P0, P1, P2, P3`) dengan kondisi saat ini:

| Proses | Allocation (R1 R2 R3) | Max (R1 R2 R3) |
| :---: | :---: | :---: |
| **P0** | `1  0  0` | `3  2  2` |
| **P1** | `6  1  2` | `6  1  3` |
| **P2** | `2  1  1` | `3  1  4` |
| **P3** | `0  0  2` | `4  2  2` |

**Tugas:**
1. Hitung vektor **Available** saat ini dan matriks **Need** untuk setiap proses.
2. Tunjukkan apakah sistem berada dalam kondisi **Safe** atau **Unsafe**, dan tuliskan **Safe Sequence**-nya!

---

## Soal 3: Translasi Alamat Memori Paging (35 Poin)
Sebuah sistem tertanam menggunakan skema *Paging* dengan ukuran **Page Size = 2 KB (2048 byte)** dan kapasitas **Logical Address Space = 16 KB**. Tabel halaman (*Page Table*) sebuah proses adalah sebagai berikut:
- `Page 0 -> Frame 4`
- `Page 1 -> Frame 7`
- `Page 2 -> Frame 1`
- `Page 3 -> Frame 6`
- `Page 4 -> Frame 2`

**Tugas:**
Hitunglah nomor *Page* (`p`), *Offset* (`d`), dan **Physical Address** (dalam desimal byte) untuk permintaan alamat logika berikut:
1. `Logical Address = 3000`
2. `Logical Address = 9000`

---

## Rubrik Penilaian Ujian Praktik UTS

| Komponen Evaluasi | Indikator Keberhasilan | Bobot |
| :--- | :--- | :---: |
| **Soal 1: Praktik CLI Linux** | Ketepatan penggunaan `lscpu`, `free`, `jobs`, `ps`, `fg`, dan `kill -9` disertai bukti tangkapan layar dan penjelasan PID/PPID. | 30% |
| **Soal 2: Banker's Algorithm** | Ketepatan vektor `Available = (0, 1, 1)`, matriks `Need`, tahapan iterasi `Work = Work + Allocation`, dan urutan `Safe Sequence` (`<P1, P2, P0, P3>`). | 35% |
| **Soal 3: Translasi Paging** | Ketepatan perhitungan `LA 3000` (`p=1, d=952 -> PA = 7*2048 + 952 = 15288`) dan `LA 9000` (`p=4, d=808 -> PA = 2*2048 + 808 = 4904`). | 35% |
