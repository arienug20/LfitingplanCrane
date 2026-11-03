# Kontrak crane, chart, dan impor v1

## Definisi

`CraneDefinition`: id, manufacturer, model, regionalVariant, sourceVersionId, geometry (carrier, rotationAxisLocal,
boomHeelLocal, boomSegments, tipOffset, counterweightEnvelope, outriggerPositions), configurations[], geometryStatus.
Geometri `source_verified|approximate|missing`; model kurang data tidak diberi label akurat.
`CraneConfiguration`: id, craneDefinitionId, sourceVersionId, operationMode='stationary_main_boom',
nominalBoomLengthM, telescopeModeId, counterweightKg, counterweightRadiusM, outriggerPresetId,
outriggerExtensionsM[4], sectorId, reevingParts, hookBlockId, stowedAttachmentIds[].
Hanya nilai yang tercakup sumber dapat menjadi konfigurasi aktif. Tidak ada jib/crawler/on-rubber capacity solver A0.
Objek generik demonstrasi boleh memakai fixture configuration terpisah dari merek sungguhan.

## Chart table

`LoadChart`: id, versionId, configurationKey, rows[{radiusM,capacityMassKg}],
deductionRules[], sectorDomain, minBoomAngleRad?, maxBoomAngleRad?, sourceRef,
verification('candidate'|'verified'|'rejected'), verifiedBy?, verifiedAt?, rightsStatus, notes.
ConfigurationKey memasukkan semua field configuration di atas yang memengaruhi rating; ID diganti nilai/source ID yang stabil.
sectorDomain berasal sumber: heading relatif carrier dan interval sudut dinormalisasi; jangan mengasumsikan label 'front'
punya orientasi OEM tertentu. Query di luar domain unsupported. Reeving/hook rating wajib tersedia atau hasil incomplete.

`lookupCapacity(query)`: result status `ok|incomplete|unsupported|invalid`;
success membawa capacityMassKg, chartId/versionId, rowRadiusM, sourceRef, appliedDeductionRuleIds.
Tidak ada zero-capacity fallback. Exact radius dalam tolerance 1e-9 m; tidak interpolate/round-up/nearest.
No matching config/radius/sector → unsupported; missing input/unverified table → incomplete;
negative/NaN/duplicate conflicting rows → invalid. Missing cell tetap missing, tidak menjadi nol.
Konfigurasi nominal fixed saat lift; jangan interpolate boom length. Saat chart coverage belum ada, geometry tetap tampil.

## Import

CSV header wajib `radius_m,capacity_kg`; metadata konfigurasi/sumber di form staging. UTF-8; delimiter comma;
decimal dot; header/unit berbeda perlu mapping eksplisit dan preview konversi. Duplicate radius conflicting ditolak.
PDF: pilih halaman/area/header/unit → text extraction atau OCR → editable candidate table dengan provenance tiap sel.
Jangan menandai chart verified otomatis karena confidence OCR tinggi. Verifikasi membandingkan seluruh selected table,
konfigurasi, notes, source revision dan varian. Bukti/verifier diperlukan untuk status verified.
Source original disimpan sebagai asset/hash atau source record; hak redistribusi diselesaikan sebelum bundling.

## Batas katalog

CAT-002 melengkapi tiga model di [source register](../engineering/crane-source-register.md). Tidak ada full chart siap pakai pada paket docs.
Task lain menggunakan `SYNTHETIC-ONLY` fixture. Katalog publik hanya metadata/link jika izin redistribusi belum ada;
hal tersebut tidak memenuhi acceptance CAT-002 untuk katalog operasional terisi.
Referensi metode: [basis](../engineering/calculation-basis.md), [evaluation](lift-evaluation.md).
