# Arsitektur A0

## Modul dan arah dependensi

`domain → engine → application/state → UI`; storage/catalog/export adalah adapter yang membaca domain.
Domain dan engine tidak mengimpor React, DOM, IndexedDB, Three.js, PDF.js, atau clock global.
Renderer tidak menghitung kapasitas. Report tidak menghitung ulang rumus: ia membaca snapshot hasil.

```text
src/
  domain/       types, validation, units, coordinates
  engine/       chart, geometry, single, rigging, tandem, clearance
  application/  project, history, snapshot, worker, readiness
  state/        project store, selection, playback
  storage/      IndexedDB, archive codec, migrations
  catalog/      crane definitions, source records, import staging
  simulation/   path evaluation, sample schedule, stage state
  ui/           shell, project, site, crane, load, rigging, review
  view2d/       SVG scene and tools
  view3d/       Three.js scene, cameras, proxies
  export/       report model, PDF, drawing, PNG, WebM
tests/
  unit/         pure modules and controlled adapters
  e2e/          real user flows in Chromium
  fixtures/     synthetic clearly labelled, no manufacturer impersonation
public/catalog/ vetted source manifest and permitted assets
```

Filenames autoritatif per task card. Shared files yang sudah dibuat task sebelumnya hanya ditambah API terkait;
jangan mengganti seluruh file. Kontrak diekspresikan sebagai tipe TypeScript pada MOD tasks.

## Stack dan command contract

React + TypeScript strict + Vite; npm dengan `package-lock.json`; Zustand; Dexie; SVG; Three.js/React Three Fiber;
PDF.js; OCR lokal lazy-loaded; fflate untuk ZIP; @react-pdf/renderer untuk PDF; Vitest; Playwright Chromium.
FND-001 memilih versi stabil yang kompatibel saat eksekusi, mencatat versi Node/npm/dependensi pada handoff,
dan mengunci dependency tree. Jangan memakai `latest` pada manifest yang disimpan atau menambah stack kedua.
Pilihan runtime harus memenuhi engines semua dependensi; jangan mengasumsikan versi Node mesin sekarang.

| Command | Disediakan | Perilaku |
|---|---|---|
| `npm ci` | FND-001 menghasilkan lockfile | Instalasi reproduksibel |
| `npm run dev` / `npm run build` | FND-001 | Vite dev dan typecheck + production build |
| `npm run check` | FND-002 | TypeScript noEmit + ESLint, tanpa rewrite |
| `npm run test:unit -- tests/unit/<file>.test.ts` | FND-003 | Vitest run; file kosong/tidak ditemukan harus gagal |
| `npm run test:e2e -- tests/e2e/<file>.spec.ts` | FND-004 | Playwright Chromium; webServer dikelola config |
| `npm run verify` | FND-006 | check + unit suite + build |

Command ini **belum ada** pada paket dokumentasi; task fondasi membuatnya. Jangan melaporkan command gagal karena
belum ada `package.json` sebagai bug aplikasi sebelum FND-001. Untuk task pertama gunakan verifikasi bootstrap pada card.
Test fixture/playwright asset lokal; tidak mengakses situs pabrikan atau mengunduh standar saat menjalankan test.

## Pemrosesan dan performa

Engine pure menerima input snapshot immutable. Worker mengirim requestId + inputHash; UI membuang respons usang.
Pekerjaan OCR/ZIP/render laporan dibatasi, dapat dibatalkan, dan tidak menimpa proyek aktif sebelum validasi.
Playback memakai clock injeksi dan fungsi `stateAt(t)`; hasil tidak bergantung urutan frame.
Target performa diuji pada VAL-005; nilai benchmark dan perangkat dicatat, bukan dijanjikan tanpa pengukuran.

## Batas publikasi

Tidak ada deployment, akun, GitHub push, atau akses publik dalam task A0. Hosting Sites hanya dievaluasi saat penugasan publikasi;
baca skill Sites saat itu. Model lokal ini tidak memerlukan backend. Rujukan: [decisions](DECISIONS.md), [kontrak](contracts/project-format.md).
