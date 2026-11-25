# Ujian Tengah Semester (UTS) - Keamanan Jaringan
**Tahun Akademik:** Ganjil 2026/2027  
**Kelas:** TIF RP 24D CNS  
**Dosen Pengampu:** Yasti Aisyah Primianjani, S.Kom., M.S.F.  

---

## Identitas Mahasiswa & Penentuan Kasus
* **Nama:** Ega Silfhia
* **NIM:** `24552011313`
* **Perhitungan Kasus:** 
  * Jumlah digit NIM: `2 + 4 + 5 + 5 + 2 + 0 + 1 + 1 + 3 + 1 + 3 = 27`
  * Operasi Modulo: `27 mod 10 = 7`
* **Kasus Terpilih:** **Kasus 7**

---

## Parameter Khusus Kasus 7
Seluruh konfigurasi dan pengujian pada lab lokal menggunakan parameter berikut:

| Parameter | Nilai |
| :--- | :--- |
| **Nomor Kasus** | `7` |
| **Kondisi NIM** | `7` |
| **Container Target** | `target-k7` |
| **Volume Docker** | `vol-k7` |
| **File Laporan** | `laporan-k7.txt` |
| **Kata Sandi Enkripsi** | `kunci-k7-2026` |
| **Domain DNS** | `k7.exfil.lab` |
| **File Handshake (Tugas 4)** | `handshake-k7.cap` |
| **Wordlist (Tugas 4)** | `wordlist-k7.txt` |

> **Peringatan Keamanan:** Semua serangan hanya boleh dijalankan di lingkungan lab lokal dengan konfigurasi jaringan `internal: true`. Dilarang keras memindai atau menyerang host di luar lingkungan lab.

---

## Daftar Tugas (Kasus 7)

### Tugas 1 (Pertemuan 1): Docker, Volume, dan Compose
* Buat volume Docker bernama `vol-k7`. Tulis NIM `24552011313` ke dalam file `laporan-k7.txt` di dalam volume tersebut dari sebuah container, hapus container tersebut, lalu baca kembali file `laporan-k7.txt` dari container baru yang memasang volume `vol-k7`.
* Jalankan Docker Compose dengan dua service (`target-k7` dan `attacker`), lalu akses halaman web target dari container `attacker`.
* **Bukti yang dilampirkan:** Isi file `laporan-k7.txt` dari container baru dan tampilan halaman nginx `target-k7` yang diakses dari `attacker`.

### Tugas 2 (Pertemuan 2): Kriptografi
* Enkripsi file `laporan-k7.txt` dengan algoritma **AES-256** menggunakan kata sandi `kunci-k7-2026`. Hitung nilai hash **SHA-256** dari file sebelum enkripsi dan setelah hasil dekripsi.
* Buat sertifikat *self-signed* dengan Common Name (`CN`) sesuai domain kasus yakni `k7.exfil.lab`, lalu tampilkan bagian *Subject* dan *Issuer*-nya.
* **Bukti yang dilampirkan:** Dua nilai hash SHA-256 yang identik, detail *Subject* dan *Issuer* sertifikat, serta penjelasan dalam **dua kalimat** mengenai perbedaan antara sertifikat *self-signed* dan sertifikat yang ditandatangani oleh Certificate Authority (CA).

### Tugas 3 (Pertemuan 3): ARP Spoofing
* Jalankan tiga container (`korban`, `gateway`, dan `penyerang`) dalam satu jaringan terisolasi. Catat tabel ARP pada `korban` sebelum dan sesudah serangan *ARP spoofing* dilancarkan oleh `penyerang`.
* Pulihkan tabel ARP `korban` dengan menambahkan entri *static ARP* yang mengarah ke MAC address `gateway` yang sebenarnya.
* **Bukti yang dilampirkan:** Perbandingan tabel ARP `korban` (MAC `gateway` berubah saat *spoofing* dan kembali normal setelah mitigasi) serta penjelasan **satu metode mitigasi** selain *static ARP*.

### Tugas 4 (Pertemuan 4): Analisis Handshake WPA2
* Lakukan analisis *handshake* WPA2 pada file `handshake-k7.cap` menggunakan wordlist `wordlist-k7.txt` dengan perkakas `aircrack-ng`.
* **Bukti yang dilampirkan:** Kata sandi yang berhasil ditemukan (atau pesan `KEY NOT FOUND`), disertai penjelasan mengenai **empat langkah (4-way handshake) WPA2**.

### Tugas 5 (Pertemuan 5): ICMP dengan Scapy
* Kirim paket *ICMP echo request* ke container korban menggunakan skrip Scapy yang telah disediakan pada sumber lab, lalu tangkap dan baca balasannya.
* **Bukti yang dilampirkan:** Nilai *Time to Live* (TTL) dan tipe ICMP dari paket balasan, serta penjelasan mengenai cara kerja ***smurf attack***.

### Tugas 6 (Pertemuan 6): SYN Flood dan Three-Way Handshake
* Catat jumlah koneksi berstatus `SYN_RECV` pada `target-k7` sebelum serangan. Jalankan serangan *SYN flood* selama **15 detik**, lalu catat kembali jumlah `SYN_RECV` saat serangan berlangsung.
* Tangkap paket jaringan menggunakan `tcpdump` saat satu koneksi HTTP normal dibuat.
* **Bukti yang dilampirkan:** Perbandingan jumlah `SYN_RECV` sebelum dan saat serangan, tangkapan paket `SYN`, `SYN-ACK`, dan `ACK` dari `tcpdump`, serta penjelasan **satu metode mitigasi** serangan *SYN flood*.

### Tugas 7 (Pertemuan 7): DNS Exfiltration
* Konversi NIM `24552011313` ke dalam format heksadesimal (*hex*), lalu kirimkan string hex tersebut sebagai subdomain menuju server DNS lab (`<hex-nim>.k7.exfil.lab`).
* Simpan log DNS, analisis log tersebut menggunakan skrip deteksi yang disediakan, lalu *decode* kembali nilai hex menjadi NIM asli (`24552011313`).
* **Bukti yang dilampirkan:** Label hex yang terdeteksi di dalam log DNS, pesan NIM hasil *decode*, penjelasan mengapa teknik *DNS exfiltration* sulit diblokir oleh firewall konvensional, serta **satu indikator deteksinya**.

---

## Struktur Pengumpulan
Seluruh output terminal, tangkapan layar/bukti, dan jawaban analisis dikumpulkan dalam satu berkas utama bernama **`jawaban.md`** melalui e-learning sesuai ketentuan mata kuliah.
```[cite: 1, 2, 3]
