# Kontrak proyek dan arsip v1

## Domain

`Project`: schemaVersion=1, id, name, location, planNumber, revisionLabel (awal A0), createdAt/updatedAt ISO UTC,
activeScenarioId, scenarios, assets, catalogVersions, policy, reviewFindings, revisionSnapshots.
`Scenario`: id, name, sceneObjects, lifts, stages, annotations, backgroundId|null, northHeadingRad=0.
ID UUID strings dibuat oleh adapter injeksi; domain tidak memanggil clock/random sendiri.
`RevisionSnapshot`: id, projectId, scenarioId, revisionLabel, createdAt, inputHash, engineVersion, frozenInput, results.
Hash SHA-256 atas JSON kanonik: object keys sorted, urutan array bermakna dipertahankan, tanpa field updatedAt/UI selection/playback.
Hash binary asset disimpan terpisah. Hasil evaluasi harus memuat inputHash yang sama dengan snapshot.

## Persistensi

IndexedDB stores `projects`, `assets`, `catalogs`, `snapshots`. Save project+asset references secara transaksi;
tampilkan status saving/saved/error. Autosave debounce 500 ms, flush pada event perubahan fokus bila memungkinkan;
browser close tidak dianggap bukti save sukses. Quota failure tidak mengosongkan in-memory state atau proyek lama.
Project rename/move adalah command domain; kamera aktif, selection, drag preview dan playback clock tidak di-autosave sebagai input engineering.
Laporan lama tetap tersedia sebagai snapshot lama dan diberi label revision/hash asal.

## Arsip .liftplan

ZIP dengan `manifest.json`, `project.json`, `catalogs/<id>.json`, `snapshots/<id>.json`, `assets/<sha256>.<ext>`.
Manifest: format='liftplan', schemaVersion=1, projectId, exportedAt, file entries(path,bytes,sha256).
Tidak ada script/executable, absolute filesystem path, credential, URL blob, atau URL eksternal yang wajib untuk restore.
Background PDF dan image dibawa sebagai asset asli; derived preview bisa diregenerasi.
Impor membaca sandbox staging → cek batas/manifest/hash/schema/referensi/ID → preview → atomic commit.
Failure meninggalkan proyek aktif dan DB lama utuh. Versi >1 ditolak; tidak ada migrasi diam-diam.
Tolak path absolute, `..`, backslash path traversal, duplicate archive entry, symlink, manifest hilang, hash salah, MIME tidak cocok.
Batas: compressed 100 MiB, expanded total 250 MiB, 1000 entries; hitung bytes aktual selama decompression.

## History

Command history: add/remove/update object, change calibration, change load/crane/rigging/path/stage/scenario.
Satu drag committed menjadi satu undo step; preview drag tidak membuat ratusan langkah. Maksimum 100 command/session.
Undo/redo mengubah inputHash dan invalidasi hasil yang bergantung padanya. Impor proyek membuat history baru.
Snapshot immutable di-deep-copy/serialize; perubahan live state tidak memutasinya.
Referensi: [scene](scene-objects.md), [simulation](simulation.md), [findings](findings-and-reports.md).
