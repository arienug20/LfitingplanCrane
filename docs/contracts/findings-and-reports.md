# Kontrak temuan, review, dan keluaran v1

## Finding

`Finding`: id,code,category(data|geometry|capacity|rigging|method|clearance|review), severity(info|warning|error),
messageId,params,objectIds[],stageId?,liftId?,tS?,sourceRef?,resolution(open|resolved|accepted_with_reason),
resolutionNote?,revisionSnapshotId?. Engine finding tidak bisa dihapus lewat tombol resolve.
Manual comment dapat resolved; computed finding berubah saat input diperbaiki dan re-evaluation.
Accepted_with_reason tidak mengganti failed engineering check menjadi pass.

## Clearance

Input proxies world + sample schedule + pair policy. Broadphase AABB lalu narrowphase box/cylinder/convex prism proxy;
nonconvex polygon dipecah atau ditolak jelas, tidak diberi clear. Hit termasuk seluruh boom/counterweight/load/rigging envelope.
Exclude intentional connection hanya explicit pair ID + alasan (contoh sling-load attachment), bukan seluruh layer.
Obstacle tersembunyi masih ikut analisis kecuali analysisEnabled=false yang tercatat pada laporan.
Output pair IDs, first conflict t, minDistanceM, thresholdM, proxy accuracy, settings/sampleCount.
Pass ditulis 'Tidak ditemukan konflik pada model dan resolusi ini'; tidak disebut continuous collision proof.
Negative separation/penetration menjadi conflict; minimumClearance dari policy, bukan warna UI.

## Readiness dan snapshot

`assessReadiness(snapshot)` mengeluarkan demoExportAllowed, operationalReady, blockers[], warnings[].
Demo export tersedia dengan DRAFT/DEMO dan missing-data list. OperationalReady=false jika source/method/policy gate terbuka,
hasil stale, missing samples, failed checks atau unresolved error. Aplikasi tidak memberi sertifikat safe/approved.
Report model dan gambar/video memakai immutable snapshot yang sama. Setelah live edit, snapshot lama tetap berlabel revisinya.

## Keluaran

PDF: cover, document number, revision/history, pendahuluan, tujuan, dasar teori, persamaan/satuan, analisis,
kesimpulan/rekomendasi, input tables, chart provenance, per-crane controlling, rigging ledger, findings, assumptions,
denah/elevasi, referensi standar+edisi, lampiran. Bahasa Indonesia, unit eksplisit; tidak mengarang nama reviewer/tanda tangan.
Drawing A3 landscape: border/title block(no,title,scale or NTS,units,date,revision), grid, north, legend, notes, sources.
Plan/elevation tags sama dengan model. PNG 3840x2160 untuk presentasi; scale printed hanya jika ukuran output ditetapkan,
selain itu NTS + scale bar. Revision cloud/triangle untuk anotasi perubahan yang pengguna tentukan.
WebM: canvas gabungan scene + overlay revision/snapshot ID/time/stage. Cek MediaRecorder.isTypeSupported,
pilih vp9 lalu vp8 lalu webm supported; bila tidak tersedia beri pesan, bukan file kosong. A0 tidak menjanjikan MP4.
Export tidak mengunggah proyek, tidak membuka akses publik, dan tidak menghitung rumus paralel sendiri.
Referensi: [standar](../engineering/standards-register.md), [project format](project-format.md).
