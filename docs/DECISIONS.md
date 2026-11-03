# Keputusan baseline A0

Status `LOCKED` adalah keputusan implementasi, bukan klaim engineering sudah tersertifikasi.
Perubahan memerlukan ID ADR baru, alasan, kontrak/task terdampak, dan pengujian migrasi.

| ID | Status | Keputusan | Alasan/konsekuensi |
|---|---|---|---|
| ADR-001 | LOCKED | Proyek baru; tanpa reuse otomatis rekacrane | Mencegah asumsi kode lama |
| ADR-002 | LOCKED | Dokumentasi dulu; coding kemudian | Penugasan pengguna |
| ADR-003 | LOCKED | Satu domain model untuk 2D/3D/simulasi/export | Tidak ada posisi alternatif tersembunyi |
| ADR-004 | LOCKED | SI internal; scene Z-up, pivot sumbu putar crane eksplisit | Mencegah radius dari pusat carrier |
| ADR-005 | LOCKED | IndexedDB + arsip .liftplan versi 1 | Tanpa akun/server; backup portabel |
| ADR-006 | LOCKED | Pure engine terpisah dari UI dan worker adapter | Determinisme dan test murah |
| ADR-007 | LOCKED | Chart exact-match konfigurasi dan radius; tidak interpolasi | Tidak mengarang kapasitas kondisi antara |
| ADR-008 | LOCKED | PDF/OCR hanya kandidat sampai verifikasi | Angka ekstraksi bisa salah |
| ADR-009 | LOCKED | Tandem beban kaku, dua gaya vertikal, orientasi tetap | Metode statis terbatas dan dapat diuji |
| ADR-010 | LOCKED | Rigging empat kaki lewat sourced assembly rating | Tidak menebak distribusi statis tak tentu |
| ADR-011 | LOCKED | Faktor demand dan ambang berasal dari policy bersumber | Demo policy tidak berlaku operasional |
| ADR-012 | LOCKED | Laporan/gambar/video dari satu immutable snapshot | Konsistensi revisi |
| ADR-013 | LOCKED | Satu task/executor; default tanpa delegasi | Mengurangi biaya konteks dan konflik |
| ADR-014 | LOCKED | Tidak menganggap jawaban agent lain sebagai bukti kelulusan | Integrator memverifikasi |
| ADR-015 | LOCKED | Tidak ada status global safe/approved | UI menampilkan pemeriksaan dan gate yang belum terpenuhi |
| ADR-016 | LOCKED | WebM A0, bukan janji MP4 | Kemampuan canvas browser dan codec diperiksa |
| ADR-017 | LOCKED | Katalog tiga model di register; konfigurasi yang belum ada tetap kosong | Tidak membuat data fiktif |
| ADR-018 | LOCKED | Batas input awal PDF 25 MiB, gambar 10 MiB, arsip 100 MiB compressed/250 MiB expanded, 1000 entry | Mencegah freeze/ZIP bomb; batas diberi pesan |
| ADR-019 | LOCKED | Kontrak v1 tidak menerima NaN/Infinity/ID ganda atau path arsip traversal | Impor atomik |
| ADR-020 | LOCKED | Sektor chart harus supplied/source-matched; tidak menebak sistem OEM dari heading | Variasi pabrikan |

Gate yang belum lengkap tidak menjadi keputusan bebas untuk executor: lihat [register standar](engineering/standards-register.md)
dan [register sumber](engineering/crane-source-register.md). Kekurangan didokumentasikan dengan bukti dan task terkait.
