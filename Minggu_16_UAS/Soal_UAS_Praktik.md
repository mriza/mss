# Naskah Soal Ujian Akhir Semester (UAS) - Praktik Laboratorium

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Durasi:** 90 Menit  
**Lingkungan Kerja:** Mesin Linux (Ubuntu/Debian/WSL2) dengan Docker & `htop`/`stress`  

---

## Petunjuk Pengerjaan
Kerjakan ketiga skenario administrasi sumber daya sistem di bawah ini secara langsung pada terminal Linux Anda. Catat seluruh perintah yang dijalankan dan ambil tangkapan layar (*screenshot*) hasil verifikasinya.

---

## Skenario 1: Manajemen Sistem File & Proteksi Hak Akses (30 Poin)
1. Buatlah struktur direktori `/tmp/uas_mss_<NIM>/{config,logs,scripts}` hanya dengan **satu baris perintah `mkdir`**.
2. Di dalam folder `config`, buatlah file `rahasia_server.conf` berisi nama lengkap dan NIM Anda.
3. Terapkan *Principle of Least Privilege* pada `rahasia_server.conf` sehingga **hanya Owner** yang dapat membaca dan menulis (`rw-`), sedangkan *Group* dan *Others* sama sekali tidak memiliki akses (`---`).
4. Di dalam folder `scripts`, buatlah skrip `cek_storage.sh` yang menampilkan kapasitas partisi utama (`/`) menggunakan `df -h` dan ukuran folder `/tmp/uas_mss_<NIM>` menggunakan `du -sh`. Berikan izin eksekusi yang paling aman (`700`) dan jalankan skrip tersebut!

---

## Skenario 2: Pembatasan Sumber Daya Kontainer Docker (40 Poin)
1. Jalankan sebuah kontainer web server **Nginx** (`nginx:alpine` atau `nginx:latest`) di latar belakang (`-d`) dengan ketentuan manajemen sumber daya berikut:
   - Nama kontainer: `uas_web_<NIM>`
   - Port *forwarding*: Port `8088` pada *Host* diarahkan ke port `80` pada kontainer.
   - Batas Memori Utama (*Memory Limit*): **`256m`** (256 MB).
   - Batas Alokasi CPU (*CPU Quota*): **`0.5`** core.
   - Kebijakan *restart*: `unless-stopped`.
2. Tampilkan bukti bahwa kontainer berjalan dan batas memori `256MiB` telah aktif menggunakan perintah `docker stats --no-stream uas_web_<NIM>`.

---

## Skenario 3: Simulasi Beban & Manajemen Prioritas Proses (30 Poin)
1. Jalankan simulasi beban CPU sebanyak 1 *worker* di latar belakang selama 120 detik dengan nilai prioritas rendah (**Niceness = 15**) menggunakan perintah `nice` dan `stress`.
2. Buka `htop`, temukan PID dari proses `stress` tersebut, dan tunjukkan kolom `NI` bernilai `15` serta persentase pemakaian CPU-nya.
3. Ubah prioritas proses `stress` yang sedang berjalan tersebut menjadi **Niceness = 5** menggunakan perintah `sudo renice`, lalu buktikan perubahannya pada tampilan `htop` atau `ps -o pid,ni,comm -p <PID>`.

---

## Rubrik Penilaian Ujian Praktik UAS

| Komponen Evaluasi | Indikator Keberhasilan | Bobot |
| :--- | :--- | :---: |
| **Skenario 1: Sistem File & Proteksi** | Ketepatan ekspansi `mkdir -p`, konfigurasi oktal `chmod 600` & `chmod 700`, serta eksekusi skrip `df -h` & `du -sh` tanpa error. | 30% |
| **Skenario 2: Kontainer & Resource Limit** | Keberhasilan eksekusi `docker run -d -p 8088:80 --name ... -m 256m --cpus="0.5" --restart unless-stopped nginx` dan verifikasi `docker stats`. | 40% |
| **Skenario 3: Monitoring & Tuning Prioritas** | Ketepatan penggunaan `nice -n 15 stress --cpu 1 --timeout 120s &`, pembacaan metrik `htop`, dan perubahan prioritas dengan `renice`. | 30% |
