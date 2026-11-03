# Task index — status otoritatif

Baseline A0: **78 task aplikasi; 0 DONE**. Penyusunan dokumentasi bukan penyelesaian task aplikasi.
READY berarti prasyarat teknis tersedia; mulai coding hanya setelah penugasan coding. Saat paket ini diserahkan belum ada implementasi.

Lifecycle: TODO → READY → IN_PROGRESS → IN_REVIEW → DONE; BLOCKED memerlukan issue/evidence.
Perubahan status, executor, dan evidence dicatat pada baris ini. Task card tidak menyimpan status kedua.

| ID / task | Dependensi langsung | Status | Gate | Executor / evidence |
|---|---|---|---|---|
| [FND-001 — Bootstrap proyek web baru](tasks/FND-001.md) | — | READY | — | Belum ditugaskan |
| [FND-002 — Pemeriksaan tipe dan lint nonmutating](tasks/FND-002.md) | [FND-001](tasks/FND-001.md) | TODO | — | Belum ditugaskan |
| [FND-003 — Harness unit test deterministik](tasks/FND-003.md) | [FND-002](tasks/FND-002.md) | TODO | — | Belum ditugaskan |
| [FND-004 — Harness E2E Chromium](tasks/FND-004.md) | [FND-003](tasks/FND-003.md) | TODO | — | Belum ditugaskan |
| [FND-005 — App shell dan navigasi Indonesia](tasks/FND-005.md) | [FND-004](tasks/FND-004.md) | TODO | — | Belum ditugaskan |
| [FND-006 — Build dan verifikasi gabungan](tasks/FND-006.md) | [FND-005](tasks/FND-005.md) | TODO | — | Belum ditugaskan |
| [MOD-001 — Konversi dan parsing satuan](tasks/MOD-001.md) | [FND-003](tasks/FND-003.md) | TODO | — | Belum ditugaskan |
| [MOD-002 — Transform koordinat dan heading](tasks/MOD-002.md) | [MOD-001](tasks/MOD-001.md) | TODO | — | Belum ditugaskan |
| [MOD-003 — Identitas dan validasi dasar](tasks/MOD-003.md) | [MOD-001](tasks/MOD-001.md) | TODO | — | Belum ditugaskan |
| [MOD-004 — Tipe scene dan background](tasks/MOD-004.md) | [MOD-002](tasks/MOD-002.md), [MOD-003](tasks/MOD-003.md) | TODO | — | Belum ditugaskan |
| [MOD-005 — Tipe crane, load, rigging, lift dan stage](tasks/MOD-005.md) | [MOD-003](tasks/MOD-003.md) | TODO | — | Belum ditugaskan |
| [MOD-006 — Tipe project, snapshot, result dan finding](tasks/MOD-006.md) | [MOD-004](tasks/MOD-004.md), [MOD-005](tasks/MOD-005.md) | TODO | — | Belum ditugaskan |
| [PRJ-001 — Buat, pilih dan ubah proyek](tasks/PRJ-001.md) | [MOD-006](tasks/MOD-006.md), [FND-005](tasks/FND-005.md) | TODO | — | Belum ditugaskan |
| [PRJ-002 — IndexedDB dan autosave transaksional](tasks/PRJ-002.md) | [PRJ-001](tasks/PRJ-001.md) | TODO | — | Belum ditugaskan |
| [PRJ-003 — Recovery dan staging impor](tasks/PRJ-003.md) | [PRJ-002](tasks/PRJ-002.md) | TODO | — | Belum ditugaskan |
| [PRJ-004 — Codec arsip .liftplan v1](tasks/PRJ-004.md) | [PRJ-003](tasks/PRJ-003.md) | TODO | — | Belum ditugaskan |
| [PRJ-005 — Command history undo/redo](tasks/PRJ-005.md) | [PRJ-001](tasks/PRJ-001.md) | TODO | — | Belum ditugaskan |
| [PRJ-006 — Snapshot, canonical hash dan stale result](tasks/PRJ-006.md) | [PRJ-004](tasks/PRJ-004.md), [PRJ-005](tasks/PRJ-005.md) | TODO | — | Belum ditugaskan |
| [SITE-001 — Grid dan kalibrasi berskala](tasks/SITE-001.md) | [MOD-002](tasks/MOD-002.md), [FND-005](tasks/FND-005.md) | TODO | — | Belum ditugaskan |
| [SITE-002 — Background gambar dan PDF](tasks/SITE-002.md) | [SITE-001](tasks/SITE-001.md), [PRJ-002](tasks/PRJ-002.md) | TODO | — | Belum ditugaskan |
| [SITE-003 — Alat editing dan panel properti](tasks/SITE-003.md) | [SITE-001](tasks/SITE-001.md), [PRJ-005](tasks/PRJ-005.md), [MOD-004](tasks/MOD-004.md) | TODO | — | Belum ditugaskan |
| [SITE-004 — Pustaka objek parametrik](tasks/SITE-004.md) | [SITE-003](tasks/SITE-003.md) | TODO | — | Belum ditugaskan |
| [SITE-005 — Viewport 3D dari domain scene](tasks/SITE-005.md) | [SITE-004](tasks/SITE-004.md), [MOD-002](tasks/MOD-002.md) | TODO | — | Belum ditugaskan |
| [SITE-006 — Kamera, ukuran dan inspeksi](tasks/SITE-006.md) | [SITE-005](tasks/SITE-005.md) | TODO | — | Belum ditugaskan |
| [CAT-001 — Registry konfigurasi crane](tasks/CAT-001.md) | [MOD-005](tasks/MOD-005.md), [MOD-001](tasks/MOD-001.md) | TODO | — | Belum ditugaskan |
| [CAT-002 — Katalog awal tiga model tersumber](tasks/CAT-002.md) | [CAT-001](tasks/CAT-001.md) | TODO | G-CAT-01 | Belum ditugaskan |
| [CAT-003 — Chart editor manual dan CSV](tasks/CAT-003.md) | [CAT-001](tasks/CAT-001.md), [PRJ-002](tasks/PRJ-002.md) | TODO | — | Belum ditugaskan |
| [CAT-004 — Ekstraksi PDF dan OCR staging](tasks/CAT-004.md) | [CAT-003](tasks/CAT-003.md), [SITE-002](tasks/SITE-002.md) | TODO | — | Belum ditugaskan |
| [CAT-005 — Verifikasi dan versi chart immutable](tasks/CAT-005.md) | [CAT-003](tasks/CAT-003.md), [PRJ-002](tasks/PRJ-002.md) | TODO | — | Belum ditugaskan |
| [CAT-006 — Lookup chart exact configuration](tasks/CAT-006.md) | [CAT-005](tasks/CAT-005.md), [MOD-006](tasks/MOD-006.md) | TODO | — | Belum ditugaskan |
| [SGL-001 — Editor beban, CoG dan titik angkat](tasks/SGL-001.md) | [MOD-005](tasks/MOD-005.md), [SITE-003](tasks/SITE-003.md) | TODO | — | Belum ditugaskan |
| [SGL-002 — Geometri crane parametrik](tasks/SGL-002.md) | [CAT-001](tasks/CAT-001.md), [SITE-005](tasks/SITE-005.md) | TODO | — | Belum ditugaskan |
| [SGL-003 — Jangkauan dan inverse geometry](tasks/SGL-003.md) | [SGL-002](tasks/SGL-002.md), [SGL-001](tasks/SGL-001.md), [MOD-002](tasks/MOD-002.md) | TODO | — | Belum ditugaskan |
| [SGL-004 — Demand ledger dan gross/net adjustment](tasks/SGL-004.md) | [MOD-006](tasks/MOD-006.md), [RIG-004](tasks/RIG-004.md) | TODO | — | Belum ditugaskan |
| [SGL-005 — Evaluator single dan limit independen](tasks/SGL-005.md) | [SGL-004](tasks/SGL-004.md), [CAT-006](tasks/CAT-006.md), [SGL-003](tasks/SGL-003.md) | TODO | — | Belum ditugaskan |
| [SGL-006 — Evaluasi lintasan dan controlling single](tasks/SGL-006.md) | [SGL-005](tasks/SGL-005.md), [SIM-003](tasks/SIM-003.md), [MOD-006](tasks/MOD-006.md) | TODO | — | Belum ditugaskan |
| [RIG-001 — Registry komponen dan rating rigging](tasks/RIG-001.md) | [MOD-005](tasks/MOD-005.md) | TODO | — | Belum ditugaskan |
| [RIG-002 — Assembly koneksi dan editor](tasks/RIG-002.md) | [SGL-001](tasks/SGL-001.md), [RIG-001](tasks/RIG-001.md) | TODO | — | Belum ditugaskan |
| [RIG-003 — Geometri sling dan constraint](tasks/RIG-003.md) | [RIG-002](tasks/RIG-002.md), [MOD-002](tasks/MOD-002.md) | TODO | — | Belum ditugaskan |
| [RIG-004 — Ledger massa dan alokasi](tasks/RIG-004.md) | [RIG-001](tasks/RIG-001.md), [RIG-002](tasks/RIG-002.md) | TODO | — | Belum ditugaskan |
| [RIG-005 — Tegangan dan rating assembly](tasks/RIG-005.md) | [RIG-003](tasks/RIG-003.md), [RIG-004](tasks/RIG-004.md) | TODO | — | Belum ditugaskan |
| [RIG-006 — Panel hasil dan temuan rigging](tasks/RIG-006.md) | [RIG-005](tasks/RIG-005.md), [SITE-005](tasks/SITE-005.md) | TODO | — | Belum ditugaskan |
| [TND-001 — Geometri dua support dan validasi CoG](tasks/TND-001.md) | [SGL-001](tasks/SGL-001.md), [RIG-004](tasks/RIG-004.md), [MOD-002](tasks/MOD-002.md) | TODO | — | Belum ditugaskan |
| [TND-002 — Solver keseimbangan statis tandem](tasks/TND-002.md) | [TND-001](tasks/TND-001.md) | TODO | — | Belum ditugaskan |
| [TND-003 — Alokasi demand aksesori per crane](tasks/TND-003.md) | [TND-002](tasks/TND-002.md), [RIG-004](tasks/RIG-004.md), [SGL-004](tasks/SGL-004.md) | TODO | — | Belum ditugaskan |
| [TND-004 — Evaluasi kapasitas kedua crane](tasks/TND-004.md) | [TND-003](tasks/TND-003.md), [SGL-005](tasks/SGL-005.md) | TODO | — | Belum ditugaskan |
| [TND-005 — Koordinasi dua hook sepanjang lintasan](tasks/TND-005.md) | [TND-004](tasks/TND-004.md), [SIM-002](tasks/SIM-002.md), [RIG-003](tasks/RIG-003.md) | TODO | — | Belum ditugaskan |
| [TND-006 — Batas metode dan integrasi evaluator tandem](tasks/TND-006.md) | [TND-005](tasks/TND-005.md), [RIG-005](tasks/RIG-005.md), [MOD-006](tasks/MOD-006.md), [SGL-006](tasks/SGL-006.md) | TODO | — | Belum ditugaskan |
| [SIM-001 — Waypoint dan lintasan editor](tasks/SIM-001.md) | [SGL-001](tasks/SGL-001.md), [SITE-003](tasks/SITE-003.md) | TODO | — | Belum ditugaskan |
| [SIM-002 — Kinematika single fixed boom](tasks/SIM-002.md) | [SIM-001](tasks/SIM-001.md), [SGL-003](tasks/SGL-003.md), [RIG-003](tasks/RIG-003.md) | TODO | — | Belum ditugaskan |
| [SIM-003 — Sample schedule deterministik](tasks/SIM-003.md) | [SIM-002](tasks/SIM-002.md), [MOD-006](tasks/MOD-006.md) | TODO | — | Belum ditugaskan |
| [SIM-004 — Playback dan seek](tasks/SIM-004.md) | [SIM-003](tasks/SIM-003.md), [FND-005](tasks/FND-005.md) | TODO | — | Belum ditugaskan |
| [SIM-005 — State tahapan independen](tasks/SIM-005.md) | [SIM-004](tasks/SIM-004.md), [PRJ-006](tasks/PRJ-006.md) | TODO | — | Belum ditugaskan |
| [SIM-006 — Panel parameter simulasi berjalan](tasks/SIM-006.md) | [SIM-004](tasks/SIM-004.md), [SGL-006](tasks/SGL-006.md), [TND-006](tasks/TND-006.md) | TODO | — | Belum ditugaskan |
| [CLR-001 — Proxy geometri analisis](tasks/CLR-001.md) | [SITE-005](tasks/SITE-005.md), [SGL-002](tasks/SGL-002.md), [RIG-003](tasks/RIG-003.md) | TODO | — | Belum ditugaskan |
| [CLR-002 — Kebijakan pasangan dan kontak sengaja](tasks/CLR-002.md) | [CLR-001](tasks/CLR-001.md) | TODO | — | Belum ditugaskan |
| [CLR-003 — Jarak dan penetration proxy](tasks/CLR-003.md) | [CLR-002](tasks/CLR-002.md), [MOD-002](tasks/MOD-002.md) | TODO | — | Belum ditugaskan |
| [CLR-004 — Pemeriksaan sepanjang lintasan](tasks/CLR-004.md) | [CLR-003](tasks/CLR-003.md), [SIM-003](tasks/SIM-003.md), [TND-005](tasks/TND-005.md) | TODO | — | Belum ditugaskan |
| [CLR-005 — Resolusi, coverage dan temuan konflik](tasks/CLR-005.md) | [CLR-004](tasks/CLR-004.md) | TODO | — | Belum ditugaskan |
| [CLR-006 — Navigasi lokasi konflik](tasks/CLR-006.md) | [CLR-005](tasks/CLR-005.md), [SIM-004](tasks/SIM-004.md), [SITE-006](tasks/SITE-006.md) | TODO | — | Belum ditugaskan |
| [REV-001 — Editor tahapan pelaksanaan](tasks/REV-001.md) | [SIM-005](tasks/SIM-005.md) | TODO | — | Belum ditugaskan |
| [REV-002 — Duplikasi dan isolasi skenario](tasks/REV-002.md) | [PRJ-006](tasks/PRJ-006.md), [REV-001](tasks/REV-001.md) | TODO | — | Belum ditugaskan |
| [REV-003 — Perbandingan alternatif](tasks/REV-003.md) | [REV-002](tasks/REV-002.md), [SGL-006](tasks/SGL-006.md), [TND-006](tasks/TND-006.md), [CLR-005](tasks/CLR-005.md) | TODO | — | Belum ditugaskan |
| [REV-004 — Komentar dan status review](tasks/REV-004.md) | [PRJ-006](tasks/PRJ-006.md), [SITE-006](tasks/SITE-006.md) | TODO | — | Belum ditugaskan |
| [REV-005 — Kesiapan ekspor dan gate engineering](tasks/REV-005.md) | [REV-004](tasks/REV-004.md), [CAT-005](tasks/CAT-005.md), [SGL-006](tasks/SGL-006.md), [TND-006](tasks/TND-006.md), [CLR-005](tasks/CLR-005.md) | TODO | — | Belum ditugaskan |
| [REV-006 — Checkpoint dan perbandingan revisi](tasks/REV-006.md) | [REV-003](tasks/REV-003.md), [REV-005](tasks/REV-005.md) | TODO | — | Belum ditugaskan |
| [OUT-001 — Immutable export bundle](tasks/OUT-001.md) | [PRJ-006](tasks/PRJ-006.md), [REV-005](tasks/REV-005.md) | TODO | — | Belum ditugaskan |
| [OUT-002 — Template laporan teknis](tasks/OUT-002.md) | [OUT-001](tasks/OUT-001.md) | TODO | — | Belum ditugaskan |
| [OUT-003 — Tabel perhitungan dan provenance laporan](tasks/OUT-003.md) | [OUT-002](tasks/OUT-002.md), [SGL-006](tasks/SGL-006.md), [TND-006](tasks/TND-006.md), [RIG-005](tasks/RIG-005.md) | TODO | — | Belum ditugaskan |
| [OUT-004 — Layout denah, elevasi dan title block](tasks/OUT-004.md) | [OUT-001](tasks/OUT-001.md), [SITE-006](tasks/SITE-006.md) | TODO | — | Belum ditugaskan |
| [OUT-005 — Ekspor PDF dan PNG](tasks/OUT-005.md) | [OUT-003](tasks/OUT-003.md), [OUT-004](tasks/OUT-004.md) | TODO | — | Belum ditugaskan |
| [OUT-006 — Rekam simulasi WebM](tasks/OUT-006.md) | [OUT-001](tasks/OUT-001.md), [SIM-006](tasks/SIM-006.md), [OUT-004](tasks/OUT-004.md) | TODO | — | Belum ditugaskan |
| [VAL-001 — Verifikasi engineering independen](tasks/VAL-001.md) | [SGL-006](tasks/SGL-006.md), [TND-006](tasks/TND-006.md), [RIG-005](tasks/RIG-005.md), [CAT-006](tasks/CAT-006.md) | TODO | G-STD-01 | Belum ditugaskan |
| [VAL-002 — Matriks input gagal dan batas metode](tasks/VAL-002.md) | [SGL-006](tasks/SGL-006.md), [TND-006](tasks/TND-006.md), [CLR-005](tasks/CLR-005.md), [CAT-004](tasks/CAT-004.md) | TODO | — | Belum ditugaskan |
| [VAL-003 — Ketahanan proyek dan recovery](tasks/VAL-003.md) | [PRJ-006](tasks/PRJ-006.md), [CAT-005](tasks/CAT-005.md), [SITE-002](tasks/SITE-002.md) | TODO | — | Belum ditugaskan |
| [VAL-004 — Integrasi single/tandem sampai keluaran](tasks/VAL-004.md) | [REV-006](tasks/REV-006.md), [OUT-005](tasks/OUT-005.md), [OUT-006](tasks/OUT-006.md), [CLR-006](tasks/CLR-006.md) | TODO | — | Belum ditugaskan |
| [VAL-005 — Performa dan kompatibilitas](tasks/VAL-005.md) | [VAL-004](tasks/VAL-004.md) | TODO | — | Belum ditugaskan |
| [VAL-006 — Release checklist dan handover executor](tasks/VAL-006.md) | [VAL-001](tasks/VAL-001.md), [VAL-002](tasks/VAL-002.md), [VAL-003](tasks/VAL-003.md), [VAL-004](tasks/VAL-004.md), [VAL-005](tasks/VAL-005.md), [CAT-002](tasks/CAT-002.md), [FND-006](tasks/FND-006.md) | TODO | G-STD-01, G-CAT-01, G-POL-01 | Belum ditugaskan |

## Aturan kesiapan

Promosikan TODO ke READY hanya jika seluruh dependensi DONE dan gate khusus task telah tersedia.
CAT-002 bukan prasyarat evaluator fixture: CAT-001/005/006 menyediakan jalur sintetis. VAL-006 tetap menunggu katalog dan review nyata.
Status gate global ada di [PROGRESS](PROGRESS.md) dan register sumber/metode. Jangan menutup gate dengan test sintetis.

## Aturan penambahan

Jangan mengganti ID yang sudah dipakai. Split/amendment mempertahankan parent reference; tambahkan ID baru dan dependency serta acceptance yang jelas.
Catat perubahan baseline di [DECISIONS](DECISIONS.md). Tidak ada estimasi PIC manusia atau model wajib dalam index ini.
