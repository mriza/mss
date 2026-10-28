# Bahan Ajar: Minggu 13 - Virtualisasi dan Kontainer (Docker)

**Mata Kuliah:** Manajemen Sumberdaya Sistem (MKK56301501)  
**Program Studi:** Teknologi Rekayasa Komputer (TRK)  
**Jurusan:** Rekayasa Pertanian dan Komputer – Politeknik Pertanian Negeri Payakumbuh  
**Pertemuan:** 13 (Tiga Belas) — Semester 5 / 2 SKS  
**Dosen Pengampu:** M. Riza Nurtam, M.Kom  
**Bahan Kajian:** BK02/MP-13  

---

## 1. Capaian Pembelajaran (Sub-CPMK) & Indikator

Pada akhir sesi perkuliahan ini, mahasiswa diharapkan mampu:
1. **Menjelaskan konsep dasar virtualisasi perangkat keras** dan peran *Virtual Machine Monitor* (VMM / Hypervisor).
2. **Membedakan Hypervisor Tipe 1 (*Bare-Metal*) dan Hypervisor Tipe 2 (*Hosted*)** beserta contoh penggunaannya di industri.
3. **Menganalisis perbedaan arsitektur mendasar antara Mesin Virtual (VM) dan Kontainer (Docker)** dari sisi utilisasi RAM, isolasi kernel, dan kecepatan startup.
4. **Menguraikan dua fitur fundamental kernel Linux yang mendasari kontainer**: *Linux Namespaces* (isolasi lingkungan) dan *Control Groups / Cgroups* (pembatasan sumber daya).
5. **Menerapkan konfigurasi pembatasan sumber daya (*Resource Limits*)** pada Docker untuk mencegah fenomena *Noisy Neighbor*.
6. **Menganalisis struktur *Docker Image Layers* dan sistem file *OverlayFS***.

---

## 2. Paradigma Virtualisasi: Hypervisor Tipe 1 vs Tipe 2

Virtualisasi adalah teknologi yang memungkinkan satu komputer fisik (*Host*) menjalankan beberapa lingkungan komputasi atau sistem operasi terisolasi (*Guest*) secara simultan dengan membagi sumber daya CPU, memori, dan storage.

Perangkat lunak pengendali virtualisasi disebut **Hypervisor** atau **Virtual Machine Monitor (VMM)**:

```text
[HYPERVISOR TIPE 1: BARE-METAL]          [HYPERVISOR TIPE 2: HOSTED]
+-------------------------------+        +-------------------------------+
| App 1 | App 2 | App 3 | App 4 |        | App 1 | App 2 | App 3 | App 4 |
+-------+-------+-------+-------+        +-------+-------+-------+-------+
| Guest | Guest | Guest | Guest |        | Guest | Guest | Guest | Guest |
| OS 1  | OS 2  | OS 3  | OS 4  |        | OS 1  | OS 2  | OS 3  | OS 4  |
+-------+-------+-------+-------+        +-------+-------+-------+-------+
|   HYPERVISOR TIPE 1 (VMM)     |        |   HYPERVISOR TIPE 2 (VMM)     |
| (KVM, VMware ESXi, Proxmox)   |        | (VirtualBox, VMware Workstn)  |
+-------------------------------+        +-------------------------------+
|     PERANGKAT KERAS FISIK     |        |      SISTEM OPERASI HOST      |
|    (Bare-Metal: CPU, RAM)     |        +-------------------------------+
+-------------------------------+        |     PERANGKAT KERAS FISIK     |
                                         +-------------------------------+
```

1. **Hypervisor Tipe 1 (Bare-Metal):**
   - Berjalan langsung di atas perangkat keras fisik komputer tanpa memerlukan sistem operasi perantara.
   - **Karakteristik:** Efisiensi komputasi sangat tinggi, latensi akses I/O sangat rendah, dan memiliki skalabilitas masif.
   - **Contoh:** KVM (*Kernel-based Virtual Machine* di Linux), VMware ESXi, Microsoft Hyper-V Server, Xen, Proxmox VE.
   - **Penerapan:** Standar utama infrastruktur *Data Center* dan penyedia layanan *Cloud Computing* (AWS, Google Cloud, Azure).
2. **Hypervisor Tipe 2 (Hosted):**
   - Berjalan sebagai aplikasi perangkat lunak reguler di atas sistem operasi *Host* yang sudah ada (misalnya aplikasi yang diinstal di atas Windows 11 atau macOS).
   - **Karakteristik:** Sangat mudah dipasang dan digunakan untuk keperluan belajar atau pengujian lokal oleh pengembang, namun memiliki *overhead* kinerja lebih besar.
   - **Contoh:** Oracle VM VirtualBox, VMware Workstation / Fusion, Parallels Desktop.

---

## 3. Komparasi Arsitektur: Virtual Machine vs Container

Perkembangan teknologi komputasi awan melahirkan paradigma **Kontainerisasi** (*Containerization*), yang sering disebut sebagai virtualisasi tingkat sistem operasi (*OS-Level Virtualization*).

```text
VIRTUAL MACHINE (Berat / Heavyweight)      CONTAINER (Ringan / Lightweight)
+-----------------------------------+     +-----------------------------------+
| App A     | App B     | App C     |     | App A     | App B     | App C     |
+-----------+-----------+-----------+     +-----------+-----------+-----------+
| Bins/Libs | Bins/Libs | Bins/Libs |     | Bins/Libs | Bins/Libs | Bins/Libs |
+-----------+-----------+-----------+     +-----------------------------------+
| Guest OS  | Guest OS  | Guest OS  |     |      DOCKER CONTAINER ENGINE      |
| (Kernel A)| (Kernel B)| (Kernel C)|     +-----------------------------------+
+-----------------------------------+     |     SHARED HOST OS KERNEL         |
|            HYPERVISOR             |     |   (Satu Kernel Dipakai Bersama)   |
+-----------------------------------+     +-----------------------------------+
|         INFRASTRUKTUR / HW        |     |         INFRASTRUKTUR / HW        |
+-----------------------------------+     +-----------------------------------+
```

| Parameter Perbandingan | Virtual Machine (VM) | Container (Docker) |
| :--- | :--- | :--- |
| **Arsitektur Kernel** | Setiap VM membawa **Guest OS Kernel terpisah secara penuh**. | Seluruh kontainer **berbagi satu Kernel Host yang sama**. |
| **Ukuran Disk Image** | Berukuran sangat besar (**Gigabytes**, 2 GB – 20 GB). | Berukuran sangat kecil (**Megabytes**, 10 MB – 500 MB). |
| **Waktu Hidup (*Startup*)** | Lambat (**hitungan menit**, karena harus boot OS lengkap). | Sangat instan (**milidetik hingga hitungan detik**). |
| **Konsumsi Memori RAM** | Boros (setiap VM memesan kuota RAM fisik secara statis). | Sangat hemat (hanya menggunakan RAM yang dibutuhkan proses). |
| **Tingkat Isolasi** | Sangat kuat (isolasi berbasis hardware via instruksi CPU VT-x). | Kuat (isolasi logika berbasis fitur kernel *namespaces* & *cgroups*). |

---

## 4. Dua Pilar Kernel Linux Penggerak Kontainer

Banyak pemula mengira Docker adalah program emulator mandiri. Pada kenyataannya, kontainer adalah **proses reguler Linux** yang dibungkus oleh dua fitur canggih kernel Linux:

### A. Linux Namespaces (Isolasi Visibilitas)
Namespaces menyajikan ilusi kepada proses di dalam kontainer bahwa ia adalah satu-satunya proses yang berjalan di komputer tersebut:
- **PID Namespace:** Mengisolasi pohon proses. Di dalam kontainer, proses aplikasi utama melihat dirinya sebagai **PID 1**, padahal di mesin Host ia memiliki PID biasa (misal PID 4520).
- **Mount Namespace:** Mengisolasi sistem file. Kontainer memiliki direktori root `/` mandiri, terpisah dari direktori host.
- **Network Namespace:** Memberikan antarmuka jaringan virtual independen, alamat IP internal sendiri, port sendiri, dan tabel routing sendiri.
- **UTS Namespace:** Memberikan nama host (*hostname*) tersendiri bagi kontainer.
- **User Namespace:** Memungkinkan pengguna di dalam kontainer menjadi `root` (UID 0) untuk kemudahan administrasi, namun di mesin Host sebenarnya dipetakan sebagai pengguna biasa tanpa hak istimewa (*non-privileged UID*).

### B. Control Groups (Cgroups) — Penjaga Alokasi Sumber Daya
Jika *Namespaces* bertugas menjawab: *"Apa saja yang boleh DILIHAT oleh kontainer?"*, maka *Cgroups* bertugas menjawab: *"Seberapa banyak sumber daya yang boleh DIGUNAKAN oleh kontainer?"*.
- Cgroups mengukur dan menerapkan plafon batas (*hard limit / soft limit*) terhadap:
  1. **CPU:** Membatasi kuota siklus eksekusi CPU (misal maksimal 50% dari 1 core).
  2. **Memory:** Membatasi kapasitas RAM maksimal (misal maksimal 512 MB). Jika kontainer melampaui batas ini, cgroups memicu *OOM Killer* khusus untuk kontainer tersebut tanpa memengaruhi host.
  3. **Block I/O:** Membatasi kecepatan baca/tulis disk (*throttling disk bandwidth*).
  4. **PIDs:** Membatasi jumlah maksimal proses turunan untuk mencegah serangan *Fork Bomb*.

---

## 5. Mencegah Fenomena "Noisy Neighbor" pada Server Produksi

Pada lingkungan server multi-tenant di mana banyak aplikasi berjalan berdampingan di satu mesin fisik:
- **Masalah Noisy Neighbor:** Jika Kontainer Layanan A mengalami kebocoran memori (*Memory Leak*) atau *infinite loop* CPU, tanpa pembatasan sumber daya, Kontainer A akan rakus memonopoli 100% CPU dan seluruh RAM server fisik. Akibatnya, Kontainer Layanan B (misal database pelanggan) menjadi lambat parah atau mati mendadak.
- **Solusi Manajemen Sumber Daya Docker:** Administrator mewajibkan penerapan kuota eksplisit saat menjalankan kontainer atau di dalam file `docker-compose.yml`:

```bash
# Menjalankan Nginx dengan batas memori ketat 256MB dan jatah CPU maksimal 0.5 core:
docker run -d \
  --name web_aman \
  -p 8080:80 \
  --memory="256m" \
  --memory-swap="512m" \
  --cpus="0.5" \
  --restart unless-stopped \
  nginx:alpine
```

### Memonitor Utilisasi Real-Time dengan `docker stats`:
Perintah `docker stats` membaca metrik langsung dari subsistem `/sys/fs/cgroup/` Linux dan menyajikannya secara real-time:
```text
CONTAINER ID   NAME        CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       PIDS
7a1b2c3d4e5f   web_aman    0.04%     12.4MiB / 256MiB      4.84%     1.2kB / 0B    2
```

---

## 6. Anatomi Image Layers dan OverlayFS

Docker Image dibangun menggunakan konsep lapisan bertumpuk (*Stacked Layers*) yang bersifat **Read-Only**:
- Setiap baris instruksi di dalam `Dockerfile` (seperti `FROM ubuntu`, `RUN apt install`, `COPY app`) menghasilkan satu layer baru.
- Jika terdapat 10 kontainer yang menggunakan basis image `ubuntu:22.04`, kesepuluh kontainer tersebut **berbagi layer image read-only yang sama di disk**, menghemat ruang penyimpanan secara masif.
- Saat kontainer dijalankan, sistem file penyatu **OverlayFS** menempelkan satu lapisan tipis **Read-Write Layer (Container Layer)** di paling atas. Setiap modifikasi file hanya disimpan pada layer tipis ini menggunakan prinsip *Copy-on-Write* (COW).

---

## 7. Rangkuman Materi

1. **Virtualisasi Tipe 1** mengontrol hardware langsung (*Bare-Metal*) untuk performa enterprise, sedangkan **Tipe 2** berjalan di atas OS Host.
2. **Kontainer** memberikan efisiensi tinggi dibandingkan VM dengan meniadakan duplikasi *Guest OS*, berbagi satu kernel Linux yang sama.
3. Kontainer dibangun di atas dua mekanisme kernel Linux: **Namespaces** (isolasi visibilitas) dan **Cgroups** (kuota batas sumber daya).
4. Pengaturan batas `--memory` dan `--cpus` mutlak diperlukan dalam manajemen sistem untuk membasmi risiko **Noisy Neighbor**.
5. Sistem file bertingkat (**OverlayFS**) memungkinkan penggunaan ulang layer image secara hemat ruang disk.

---

## 8. Referensi Pustaka

- **Silberschatz, A., Galvin, P. B., & Gagne, G. (2019).** *Operating System Concepts* (10th Global Edition). John Wiley & Sons. **Chapter 18: Virtual Machines & Containers (pp. 735–770).**
- **Tanenbaum, A. S., & Bos, H. (2022).** *Modern Operating Systems* (5th Edition). Pearson. **Chapter 7: Virtualization and the Cloud (pp. 473–530).**
- **Nemeth, E., et al. (2017).** *UNIX and Linux System Administration Handbook* (5th Edition). Pearson. **Chapter 26: Virtualization (pp. 821–854); Chapter 27: Containers (pp. 855–886).**
