# kelurahan-lahendong.github.io
# Situs Informasi Kelurahan Lahendong

Situs informasi Kelurahan Lahendong, Kecamatan Tomohon Selatan, Kota Tomohon, Sulawesi Utara —
disusun oleh Mahasiswa KKT Unsrat Angkatan 149. Sengaja tidak menyebut diri situs resmi pemerintah;
footer mengingatkan pengunjung untuk memastikan keperluan administrasi ke kantor kelurahan.
HTML + Tailwind (CDN) + JavaScript biasa — tanpa build step.
Situs informasi Kelurahan Lahendong, Kecamatan Tomohon Selatan, Kota Tomohon, disusun oleh Mahasiswa KKT
Unsrat Angkatan 149 sebagai sarana informasi. Untuk keperluan administrasi, pengunjung diminta memastikan
ke Kantor Kelurahan.

| Dokumen | Untuk |
|---|---|
| **README** (berkas ini) | Admin: mengelola isi lewat spreadsheet & mengganti foto |
| [**docs/PANDUAN-TEKNIS.md**](docs/PANDUAN-TEKNIS.md) | Pengembang: struktur repo, alur data, fungsi kunci, resep mengubah kode |
| [**docs/DESIGN-SPEC.md**](docs/DESIGN-SPEC.md) | Aturan desain: warna, tipografi, komponen |

Situs terbit: <https://kelurahan-lahendong.github.io/> (alamat lama `vercoooo.github.io/web-lahendong/` dialihkan ke sini —
lihat [Pindah alamat](docs/PANDUAN-TEKNIS.md#pindah-alamat-situs)).

## Cara kerja: spreadsheet → situs

Semua **isi** situs (angka, nama, teks, daftar) dibaca dari satu Google Sheet setiap kali halaman
dibuka. Mengubah sel di sheet = mengubah isi situs; hasilnya tampil saat halaman dimuat ulang.
Kode hanya menentukan **tampilan**.

| Tab sheet | Tampil di halaman | Isi |
|---|---|---|
| `profil` | Profil, Kontak, Layanan, Penduduk, Beranda, header & footer | Alamat, telepon, email & jam layanan; letak, koordinat, luas, ketinggian, suhu; batas wilayah; visi & misi; tahun & sumber data |
| `sejarah` | Profil (bagian Sejarah) | Satu baris per bagian: `judul` & `isi` (baris berawalan `- ` menjadi butir) |
| `lingkungan` | Penduduk, Beranda (angka ringkas), Pemerintahan (kartu lingkungan) | Satu baris per lingkungan — **semua total dihitung dari sini** |
| `aparat` | Pemerintahan (struktur), Beranda (pimpinan), Kontak | Satu baris per aparat |
| `kontak` | Kontak | Nomor darurat & layanan umum selain aparat |
| `wisata` | Wisata, detail wisata, Beranda | Satu baris per destinasi — **daftar destinasi tetap**, hanya keterangannya yang diubah |
| `layanan` | Layanan, Beranda (daftar surat) | Satu baris per jenis surat |

Tabel yang sama, beserta arti setiap kolom, ada di tab `petunjuk` pada spreadsheet.

**Tidak diatur dari spreadsheet:** judul dan kalimat pengantar tiap halaman (berkas HTML),
**semua foto** (lihat [Foto](#foto-statis-diatur-pengembang)), peta wilayah (`img/umum/peta-wilayah.png` — tampil otomatis bila ada), dan
halaman **KKT Unsrat Angkatan 149** (`kkt.html`, tidak ada di menu atas; ditautkan dari footer lewat tombol
"Kenali Tim KKT Unsrat 149", Tautan Cepat, dan baris kredit):
datanya ditulis di `DATA_KKT` pada awal [`assets/js/halaman/kkt.js`](assets/js/halaman/kkt.js) —
nama, NIM, fakultas, peran (opsional), serta dosen lapangan (pembimbing & pengawas), periode, dan
paragraf "tentang". Foto mahasiswa otomatis `img/kkt/<nim>.webp`.

## Mengelola spreadsheet

Spreadsheet dirancang agar sulit salah isi:

- **Tidak ada kode/id yang perlu dikarang.** Setiap baris dikenali dari kolom pertamanya
  (nama, jabatan, judul) — kolom yang judulnya berwarna hijau tua. Situs membuat kodenya sendiri:
  "Danau Linow" → `wisata-detail.html?id=danau-linow`.
- **Tidak ada angka yang ditulis dua kali.** Jumlah penduduk, KK, laki-laki/perempuan, jumlah jiwa per
  lingkungan, dan jumlah lingkungan dihitung dari tab `lingkungan`.
- **Dropdown** untuk isian pilihan: `tampil`, `kategori`, `atasan` (aparat, diambil dari kolom jabatan), dan
  `nama` di tab `wisata` (daftar destinasi tetap).
- **Catatan di judul kolom**: arahkan kursor ke judul kolom untuk melihat arti dan contohnya.
- **Halaman [Cek Data](https://kelurahan-lahendong.github.io/cek-data.html)** memeriksa seluruh sheet
  dan menunjukkan setiap isian yang keliru: kolom salah ketik, atasan tidak ditemukan, angka tidak valid,
  destinasi wisata yang tidak terdaftar, nama kembar, sampai deret angka yang mirip NIK. Buka setelah mengedit.
