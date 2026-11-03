# Kontrak evaluasi lifting v1

## Entry point

`evaluateLift(input: EvaluationInput): LiftEvaluation` pure, deterministic, tanpa DOM/DB/network.
Input: snapshotId,inputHash,engineVersion,mode(single|tandem), load, craneStates[], chartVersions[], riggingLedger,
sampledStates[], policy, methodEvidence. UI membangun input immutable; worker tidak menjadi sumber metode.
Policy: id, version, purpose(demo|operational), sourceRef, payloadFactor, riggingFactor, hookFactor, utilizationLimitPct,
minimumClearanceM, reviewState. Semua faktor >0. Limit 0<value<=100; clearance >=0.
Tidak ada policy kosong yang diperlakukan 1.0/100%. Demo fixture memakai nilai eksplisit dan bertanda DEMO.

## Hasil

Status: `pass|exceeds|incomplete|unsupported|invalid`. Prioritas aggregate: invalid, unsupported, incomplete, exceeds, pass.
Check terpisah tetap disimpan meski aggregate gagal. Missing kapasitas atau demand → null, bukan 0 atau NaN.
`LiftEvaluation`: snapshotId,inputHash,engineVersion,methodStatus(demo|reviewed), status, checks[], samples[], controlling,
sourceVersions[], policyVersionId, findings[]. `CheckResult`: id,type,status,actual|null,limit|null,unit,sourceRefs[],reasonCode.
Samples memuat tS, craneId, radiusM, hookHeightM, physicalForceN, designDemandN, ratedCapacityN|null, utilizationPct|null.
controlling memilih utilisasi tertinggi yang valid; tie waktu paling awal lalu craneId lexical. Jangan mengabaikan sample unsupported
dan menyebut seluruh lintasan pass. Hasil yang salah hash/revisi tidak dipasang ke live state.

## Demand dan rating

Physical = m*g tanpa policy factors. Design dihitung linear per komponen dengan faktor kategori yang eksplisit.
Gross chart: semua suspended components masuk demand; deductions ditambah sekali menurut source rules.
Net chart: hanya components yang source nyatakan sudah dikurangi dikeluarkan dari perbandingan demand; ledger tetap menampilkan physical.
Konversi ratedCapacityKg*g. U=100*designDemandN/ratedCapacityN. Kapasitas <=0 invalid.
Reeving/line pull/hook rating diperiksa sebagai limit terpisah; data hilang incomplete, bukan dianggap cukup.
Aturan deduction harus memiliki ID, component basis, mass equivalent kg dan asal; rule unknown menahan evaluation.

## Worker

`{requestId,inputHash,input}` → `{requestId,inputHash,result|error}`. Respons terbaru saja jika hash sesuai current input.
Cancellation tidak menjadi pass; output partial diberi incomplete. Error engine tidak menghapus proyek.
Snapshot mencatat hash + version; rounding hanya presentasi.

## Evaluasi demonstrasi dan engineering gate

Engine fixture tetap dapat dihitung walau gate referensi belum terpenuhi; methodStatus=demo dan readiness operational=false.
Gate tidak menyembunyikan exceed/invalid. Signoff operational perlu source verified, policy reviewed dan methodEvidence lengkap.
Referensi: [basis](../engineering/calculation-basis.md), [standar](../engineering/standards-register.md).
