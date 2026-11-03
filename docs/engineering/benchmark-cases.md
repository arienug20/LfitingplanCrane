# Benchmark sintetis A0

## Pendahuluan dan tujuan

Fixture berikut bukan data pabrikan. Gunakan nama `SYNTHETIC-ONLY`, provenance `test_fixture`, purpose `demo`.
Expected result dihitung terpisah dari implementasi production. Jangan membuat expected dengan memanggil fungsi yang diuji.

## Dasar teori

Statika dan konversi SI pada [basis](calculation-basis.md). Demo policy eksplisit: semua factors=1,
utilizationLimitPct=100, minimumClearanceM=0.5, sourceRef='SYNTHETIC-POLICY', reviewState='demo'.
Setiap test menyatakan ledger/deduction yang berlaku; field kosong bukan nol.

## Persamaan dan expected result

| ID | Input | Expected |
|---|---|---|
| B-UNIT | m=1000 kg; g=9.80665 | W=9806.65 N |
| B-COORD | world(2,3,4); yaw pi/2 untuk local(1,0,0) | Three(2,4,-3); rotated(0,1,0) |
| B-CHART | radius 8/10/12 m; capacity 12000/10000/8000 kg; exact config verified | r=10→10000 kg; r=9→unsupported; no interpolation |
| B-SINGLE | 9000 kg cargo, hook/rigging=0 eksplisit, r=10, chart10000 kg | 88259.85 N; U=90% |
| B-FACTOR | B-SINGLE; payloadFactor=1.1 | physical=88259.85 N; design=97085.835 N; U=99% |
| B-DEDUCT | gross demand cargo9000+hook500 kg, C10000 kg; fixture rule says hook not pre-deducted | U=95%; hook masuk sekali |
| B-NET | chart9500 kg explicitly net of hook500; cargo9000+hook500 physical | comparison U=9000/9500*100=94.7368421053%; physical tetap9500kg*g |
| B-TANDEM | A=(0,0,0), B=(10,0,0), shared m10000 kg, CoG=(4,0,0) | RA=58839.9 N; RB=39226.6 N; RA+RB=98066.5 N |
| B-TANDEM-MID | same CoG=(5,0,0) | RA=RB=49033.25 N |
| B-TANDEM-ACC | B-TANDEM + specific A accessory100kg; capA8000kg/capB5000kg | A demand6100kg*g; UA=76.25%; UB=80%; controlling B |
| B-TANDEM-OFF | CoG=(4,1,0) or span=0 or CoG beyond supports | off-line unsupported; zero span invalid; negative reaction unsupported |
| B-RIG | V=9806.65 N; symmetric 2-leg; theta60degree from vertical | each T=9806.65 N; theta90degree unsupported |
| B-MAT | external R=100000 N, A=2m² | q=50000Pa=50kPa; tidak ada reaction solver |
| B-CAL | pixel distance200; known distance10m | 0.05 m/pixel |
| B-TIME | position(0,0,0) at0s to(10,0,0) at10s | t5→(5,0,0), seek/replay sama |
| B-SAMPLE | translation10m/10s, maxstep0.1m/0.1s, no rotation | 101 samples termasuk dua endpoint |
| B-CLEAR | axis-aligned boxes separated face gap0.25m; threshold0.5m | conflict; gap0.75m→clear_at_resolution |
| B-STALE | current hashB, worker response hashA | response tidak dipasang; readiness false |

## Analisis dan failure matrix

Wajib additional cases: missing WLL/policy/config, unverified PDF, inconsistent duplicate radius, kN/N mismatch,
truncated archive, unknown schema, quota failure, dangling ID, cancellation, unsupported codec, sample limit.
Toleransi [units contract](../contracts/units-and-coordinates.md). U nominal dibulatkan hanya saat display.
Numerical bench dapat pass saat gate standar belum selesai; hasil itu tidak menutup G-STD-01.

## Kesimpulan

VAL-001 mencatat independent recomputation beserta metode dan sumber. Bagi temuan, kutip nilai aktual salah,
jelaskan penyebab, lalu tetapkan expected yang benar. Referensi standar/edisi: [register](standards-register.md).
