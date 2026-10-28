# Modul Praktikum: Proteksi Sistem dan File Permissions

**Mata Kuliah:** Manajemen Sumberdaya Sistem
**Program Studi:** Teknologi Rekayasa Komputer, Politeknik Pertanian Negeri Payakumbuh
**Pertemuan Ke-:** 12

---

## 1. Tujuan Praktikum
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Membaca hak akses (ACL/Permission) sebuah file/direktori di Linux.
2. Mengubah hak akses menggunakan format simbolik dan numerik (Oktal) dengan `chmod`.
3. Mengubah kepemilikan file dengan `chown`.
4. Mengaplikasikan *Principle of Least Privilege* dalam simulasi sederhana.

## 2. Dasar Teori
Di Linux, setiap file memiliki **Pemilik (User/Owner)** dan **Grup (Group)**. Hak aksesnya dibagi menjadi tiga kelompok (User, Group, Others) dan tiga jenis aksi:
- **Read (r):** Angka 4. Bisa membaca isi file (atau melihat isi direktori).
- **Write (w):** Angka 2. Bisa mengubah/menghapus file (atau menambah/menghapus file di dalam direktori).
- **Execute (x):** Angka 1. Bisa menjalankan file sebagai program (atau masuk ke dalam direktori dengan perintah `cd`).

Jika melihat *output* `drwxr-xr--`, huruf pertama `d` berarti direktori. Tiga huruf berikutnya `rwx` (User/Owner), berikutnya `r-x` (Group), dan tiga huruf terakhir `r--` (Others/Publik).

## 3. Alat dan Bahan
- Terminal Linux (Ubuntu, Debian, atau WSL2).

## 4. Langkah Kerja

### A. Membaca dan Menganalisis Permissions
1. Buka terminal, buat file rahasia:
   ```bash
   echo "Kata sandi super rahasia: 12345" > secret.txt
   ```
2. Cek izin bawaan (*default*) dari file tersebut:
   ```bash
   ls -l secret.txt
   ```
3. Anda mungkin akan melihat hasil seperti `-rw-rw-r--` atau `-rw-r--r--`. Artinya, siapa pun (*Others*) saat ini bisa membaca file rahasia Anda!

### B. Mengubah Hak Akses Menggunakan Angka (Octal)
Kita ingin menerapkan *Principle of Least Privilege*. File `secret.txt` HANYA boleh dibaca dan ditulis oleh si Pemilik. Grup dan Orang Lain sama sekali tidak boleh membaca.
1. Gunakan mode numerik.
    - User (r+w) = 4 + 2 = 6
    - Group (tidak ada) = 0
    - Others (tidak ada) = 0
2. Ubah aksesnya dengan perintah:
   ```bash
   chmod 600 secret.txt
   ```
3. Verifikasi perubahannya:
   ```bash
   ls -l secret.txt
   ```
   *(Harusnya berubah menjadi `-rw-------`)*

### C. Mengubah Kepemilikan (Chown)
*(Peringatan: Langkah ini memerlukan privilese `sudo`)*
1. Buat file tugas untuk kelompok mahasiswa:
   ```bash
   touch proyek_kelompok.txt
   ```
2. Ubah hak milik (Owner) file tersebut ke pengguna **root** (sebagai simulasi dosen), namun biarkan grup tetap milik *user* Anda:
   ```bash
   sudo chown root proyek_kelompok.txt
   ```
3. Cek propertinya dengan `ls -l`.
4. Sekarang cobalah ubah isi filenya dengan *user* biasa Anda:
   ```bash
   echo "Saya mencoba mengedit" > proyek_kelompok.txt
   ```
   *(Anda pasti akan mendapat pesan error: Permission denied, karena Anda bukan lagi Owner, dan hak Write tidak diberikan ke Group atau Others)*

## 5. Tugas / Laporan Praktikum
1. Jika seorang dosen memberikan hak akses **`chmod 754 laporan.pdf`**, jelaskan rincian izin apa saja yang dimiliki oleh *Owner*, *Group*, dan *Others* (jelaskan satu per satu menggunakan huruf r, w, dan x)!
2. Jika Anda membuat *script bash* `hello.sh` dan Anda (Pemilik) ingin menjalankannya, kombinasi angka apa (dari rentang `600` s/d `777`) yang **paling aman** (least privilege) untuk perintah `chmod ___ hello.sh`? Berikan argumen rasional mengapa Anda tidak menggunakan `777`!
