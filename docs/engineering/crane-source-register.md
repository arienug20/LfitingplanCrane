# Register sumber crane — A0

## Pendahuluan dan tujuan

Katalog awal memuat tiga model berikut. Link resmi ditemukan saat perencanaan; angka chart belum ditranskripsi/diverifikasi.
Ini backlog bukti untuk CAT-002, bukan katalog aktif siap perhitungan.

## Dasar sumber

| Source ID | Model/varian target | Sumber resmi | Status |
|---|---|---|---|
| OEM-LIE-001 | Liebherr LTM 1100-5.3, metric | [Produk dan technical data](https://www.liebherr.com/en-ca/mobile-and-crawler-cranes/mobile-cranes/ltm-mobile-cranes/ltm-1100-5-3-4678822) | Link ditemukan; dokumen/configuration/version belum di-freeze |
| OEM-GRO-001 | Grove GMK4100L-2, metric | [Produk](https://www.manitowoc.com/grove/all-terrain-cranes/gmk4100l-2), [metric product guide](https://www.manitowoc.com/media/15987/download) | Link ditemukan; transkripsi dan hak distribusi pending |
| OEM-TAD-001 | Tadano GR-1000EX-4, metric/AUS sesuai dokumen | [Produk/spec sheet](https://www.tadano.com/oceania/en/lifting-equipment/rough-terrain-cranes/gr-1000ex-4/) | Jangan menyamakan varian regional; tabel belum diverifikasi |

## Persamaan dan satuan

Konversi mengikuti [units](../contracts/units-and-coordinates.md). Jangan memakai kapasitas nominal marketing sebagai rated capacity
pada seluruh radius. Model LTM 1100-5.3, GMK4100L-2 dan GR-1000EX-4 adalah identitas berbeda; angka tidak dipertukarkan.

## Analisis dan acceptance CAT-002

Untuk setiap model: rekam URL, retrievedAt, file hash, document title/revision, regional variant, page, configuration,
catatan chart, limits, dimensional source dan rightsStatus. Isi satu konfigurasi stationary main boom bersumber,
seluruh baris radius tabel konfigurasi tersebut, serta geometri yang diperlukan; dokumentasikan batas subset yang diisi.
Pemilihan subset pertama: main boom tanpa jib, stationary outriggers sesuai tabel sumber; bila ada beberapa tabel,
pilih counterweight maksimum yang dicantumkan dengan kondisi outrigger eksplisit dan rekam alasan pemilihan.
Jangan memaksakan preset bila kondisi tersebut tidak tersedia pada sumber: catat model blocker.
Review seluruh sel dan notes; bukan sampling beberapa angka. Source asli hanya dibundel jika haknya mengizinkan.
Metadata + link boleh disiapkan, tetapi tidak memenuhi target katalog terisi sampai kapasitas/configuration diverifikasi.

## Kesimpulan dan gate G-CAT-01

Gate terbuka sampai data+notes+geometry penting+rights diverifikasi. Fixture diberi `SYNTHETIC-ONLY`, manufacturer=null,
tidak ditampilkan sebagai salah satu dari tiga crane nyata. Tidak ada download otomatis dalam unit test.
Referensi: [chart contract](../contracts/crane-and-chart.md), [standar](standards-register.md).
