# Pembuat Jadwal Piket

Aplikasi web satu file (HTML, CSS, JavaScript) untuk menyusun jadwal piket bulanan secara otomatis. Nama peserta dirotasi berurutan mengikuti tanggal kalender, dan hasilnya bisa diunduh sebagai **gambar (PNG)** atau **Excel (.xlsx)**.

Tampilan tabel meniru format jadwal piket di Excel: judul, bulan dan tahun, kolom hari, tanggal dalam kurung diikuti nama, sel abu-abu untuk libur, dan blok `NOTES` di bawah tabel.

## Daftar isi

- [Fitur](#fitur)
- [Cara pakai](#cara-pakai)
- [Contoh hasil](#contoh-hasil)
- [Aturan penyusunan jadwal](#aturan-penyusunan-jadwal)
- [Hasil unduhan](#hasil-unduhan)
- [Menjalankan di lokal](#menjalankan-di-lokal)
- [Deploy ke GitHub Pages](#deploy-ke-github-pages)
- [Kustomisasi](#kustomisasi)
- [Teknologi dan dependensi](#teknologi-dan-dependensi)
- [Penyimpanan data](#penyimpanan-data)
- [Batasan](#batasan)
- [Struktur repositori](#struktur-repositori)
- [Lisensi](#lisensi)

## Fitur

- **Daftar peserta fleksibel:** tambah (bisa banyak nama sekaligus, dipisah koma), edit, hapus, dan ubah urutan dengan tombol panah. Urutan daftar sama dengan urutan giliran.
- **Pilih bulan dan tahun:** tanggal dihitung dari kalender bawaan browser, sehingga selalu sesuai kalender Masehi.
- **Rentang hari piket:** pilih hari mulai dan hari akhir (misalnya Senin sampai Sabtu, atau Senin sampai Jumat). Tabel hanya menampilkan kolom pada rentang tersebut.
- **Tanggal libur:** klik tanggal di tabel untuk menandai libur. Tanggal libur dilewati dan tidak menghabiskan giliran.
- **Giliran pertama bulan ini:** pilih nama yang membuka bulan tersebut, agar rotasi nyambung dari bulan sebelumnya.
- **Tombol "Lanjut ke bulan berikutnya":** pindah ke bulan berikutnya dan otomatis mengisi nama awal yang tepat.
- **Tanggal bulan sebelumnya:** di minggu pertama, tanggal bulan sebelumnya tampil abu-abu lengkap dengan namanya. Opsi ini bisa dimatikan.
- **Judul dan catatan:** judul jadwal dan poin `NOTES` dapat diubah bebas (satu baris menjadi satu poin).
- **Unduh PNG dan Excel:** hasil siap dibagikan atau dicetak.
- **Tema terang dan gelap:** mengikuti pengaturan sistem.
- **Tanpa backend:** semua proses berjalan di browser, data tidak dikirim ke server mana pun.

## Cara pakai

Ada tiga input utama:

| Input | Keterangan |
| --- | --- |
| **Nama peserta** | Daftar peserta piket, berurutan sesuai giliran. |
| **Bulan dan rentang hari** | Bulan, tahun, hari mulai, hari akhir, giliran pertama, serta tanggal libur. |
| **Judul dan catatan** | Judul di baris paling atas dan poin `NOTES` di bawah tabel. |

Langkah singkat:

1. Isi atau ubah daftar nama peserta.
2. Pilih bulan, tahun, hari mulai, dan hari akhir.
3. Pilih siapa yang mendapat giliran pertama bulan itu.
4. Klik tanggal di tabel yang libur (libur nasional, cuti bersama, dan sebagainya).
5. Ubah judul dan catatan bila perlu.
6. Klik **Unduh gambar (PNG)** atau **Unduh Excel (.xlsx)**.
7. Untuk bulan berikutnya, klik **Lanjut ke bulan berikutnya**. Giliran otomatis melanjutkan dari nama terakhir.

## Contoh hasil

September 2026, rentang Senin sampai Sabtu, giliran pertama TRI, daftar peserta: Andit, David, Tri, Lilik, Irsyad, Herri, Sabil.

| SENIN | SELASA | RABU | KAMIS | JUMAT | SABTU |
| --- | --- | --- | --- | --- | --- |
| (31) DAVID | (1) TRI | (2) LILIK | (3) IRSYAD | (4) HERRI | (5) SABIL |
| (7) ANDIT | (8) DAVID | (9) TRI | (10) LILIK | (11) IRSYAD | (12) HERRI |
| (14) SABIL | (15) ANDIT | (16) DAVID | (17) TRI | (18) LILIK | (19) IRSYAD |
| (21) HERRI | (22) SABIL | (23) ANDIT | (24) DAVID | (25) TRI | (26) LILIK |
| (28) IRSYAD | (29) HERRI | (30) SABIL | | | |

Sel `(31) DAVID` berwarna abu-abu karena termasuk bulan sebelumnya (Agustus).

## Aturan penyusunan jadwal

- **Rotasi berurutan:** setiap hari piket yang bukan libur mengambil nama berikutnya dalam daftar, lalu kembali ke nama pertama setelah nama terakhir.
- **Urutan mengikuti tanggal:** giliran diberikan dari tanggal terkecil ke terbesar dalam bulan yang dipilih, hanya untuk hari yang masuk rentang.
- **Libur dilewati:** tanggal libur tidak mendapat nama dan tidak menggeser giliran. Nama yang seharusnya piket di hari libur tetap mendapat giliran pada hari piket berikutnya.
- **Minggu mengikuti hari mulai:** setiap baris tabel dimulai dari hari mulai yang dipilih. Rentang boleh melewati akhir pekan (misalnya Sabtu sampai Selasa).
- **Hari mulai sama dengan hari akhir:** tabel hanya memiliki satu kolom.
- **Tanggal bulan sebelumnya:** namanya dihitung mundur dari giliran pertama bulan berjalan, sehingga urutan tetap konsisten dengan tabel bulan sebelumnya. Tanggal ini dianggap bukan libur.
- **Minggu tanpa tanggal bulan berjalan:** dilewati. Tanggal bulan berikutnya di minggu terakhir dibiarkan kosong.
- **Nama kosong:** entri nama yang kosong diabaikan.

## Hasil unduhan

Nama file otomatis mengikuti bulan dan tahun, misalnya `jadwal-piket-september-2026.png` atau `jadwal-piket-september-2026.xlsx`.

**PNG**
- Resolusi 2x agar tetap tajam saat dicetak atau dibagikan.
- Dibuat langsung di browser menggunakan Canvas.
- Lebar kolom menyesuaikan panjang nama.

**Excel (.xlsx)**
- File Excel asli yang bisa diedit.
- Baris judul dan baris bulan digabung (merge) selebar tabel.
- Border tipis pada seluruh sel tabel, sel abu-abu untuk libur dan tanggal bulan sebelumnya, angka libur merah tebal.
- Blok `NOTES` di bawah tabel.
- Pengaturan cetak landscape dan muat satu halaman lebar.

## Menjalankan di lokal

Tidak perlu instalasi atau proses build.

1. Unduh atau clone repositori ini.
2. Buka `index.html` di browser modern (Chrome, Edge, Firefox, Safari).

Catatan koneksi internet:
- **Excel** memuat pustaka ExcelJS dari CDN, sehingga unduh Excel butuh internet.
- **PNG dan seluruh fitur penyusunan jadwal** berjalan tanpa internet. Tanpa internet, font Figtree dan Archivo diganti font sistem.

## Deploy ke GitHub Pages

1. Pastikan file utama bernama `index.html` di root repositori.
2. Commit dan push ke GitHub.
3. Buka **Settings** lalu **Pages**.
4. Pada **Build and deployment**, pilih **Deploy from a branch**.
5. Pilih branch `main` dan folder `/ (root)`, lalu simpan.
6. Tunggu beberapa menit. Situs tersedia di `https://<username>.github.io/<nama-repositori>/`.

Aplikasi ini juga bisa di-host di layanan statis lain (Netlify, Cloudflare Pages, server web biasa) tanpa konfigurasi tambahan.

## Kustomisasi

Semua pengaturan awal ada di objek `S` di dalam tag `<script>` pada `index.html`:

| Pengaturan | Fungsi |
| --- | --- |
| `title` | Judul jadwal bawaan. |
| `names` | Daftar peserta bawaan. |
| `startDay`, `endDay` | Rentang hari bawaan (indeks pada daftar `DAYS`, 0 = Senin sampai 6 = Minggu). Bawaan: Senin sampai Sabtu. |
| `adjacent` | Menampilkan tanggal bulan sebelumnya secara bawaan. |
| `notes` | Catatan bawaan, satu baris satu poin. |
| `KEY` | Nama kunci `localStorage`. Ubah bila ingin memisahkan data antar versi. |

Warna dan tema diatur lewat variabel CSS di bagian `:root` (`--bg`, `--panel`, `--ink`, `--accent`, dan seterusnya), termasuk versi mode gelap.

## Teknologi dan dependensi

- HTML, CSS, dan JavaScript murni (tanpa framework dan tanpa proses build).
- [ExcelJS](https://github.com/exceljs/exceljs) 4.4.0 via cdnjs, untuk membuat file `.xlsx` beserta format sel.
- Google Fonts: Figtree dan Archivo (opsional, ada font cadangan).
- Canvas API bawaan browser untuk membuat PNG.

## Penyimpanan data

Pengaturan (nama, bulan, rentang hari, libur, judul, catatan) disimpan otomatis di `localStorage` browser dengan kunci `piket-v1`.

- Data hanya ada di browser dan perangkat yang dipakai, tidak dibagikan antar pengguna.
- Menghapus data situs di browser akan mengembalikan pengaturan ke nilai bawaan.
- Jika `localStorage` tidak tersedia, aplikasi tetap berjalan tanpa penyimpanan.

## Batasan

- Libur nasional dan cuti bersama **tidak terisi otomatis**. Tandai manual dengan mengklik tanggal.
- Rentang tahun yang didukung: 2000 sampai 2100.
- Tanggal libur di minggu bulan sebelumnya tidak bisa ditandai dari bulan berjalan. Tandai di bulan aslinya.
- Tanggal bulan sebelumnya pada minggu pertama selalu ditampilkan jika opsinya aktif. Hal ini bisa sedikit berbeda dari tabel Excel manual yang tidak menampilkan minggu perbatasan bulan.
- Unduh Excel memerlukan akses internet ke `cdnjs.cloudflare.com`.

## Struktur repositori

```
.
├── index.html   # seluruh aplikasi (HTML, CSS, JavaScript)
└── README.md    # dokumentasi ini
```

## Lisensi

Tambahkan berkas `LICENSE` sesuai kebutuhan (misalnya MIT) sebelum dipublikasikan.
