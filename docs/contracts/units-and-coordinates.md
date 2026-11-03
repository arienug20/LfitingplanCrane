# Kontrak satuan dan koordinat v1

Normatif untuk MOD-001/002 dan seluruh engine. Perubahan memerlukan ADR dan migrasi fixture.

## Nilai

Internal: length m, mass kg, force N, pressure Pa, angle rad, time s. Display kg/t, N/kN, Pa/kPa, mm/m, rad/degree.
`g = 9.80665 m/s²`; 1 metric tonne = 1000 kg. Jangan menyamakan ton pendek AS dengan metric tonne.
Chart kapasitas disimpan sebagai mass-equivalent kg dengan asal satuan tercatat; konversi ke N tepat sekali saat evaluasi.
Parsing input kosong menghasilkan incomplete, bukan nol. NaN/Infinity, panjang negatif, massa negatif dan faktor <=0 invalid.
Dimensi komponen harus >0; koordinat dan elevasi boleh negatif. Parsing desimal UI mendukung koma atau titik tunggal,
tanpa pemisah ribuan; `1,234.5` ditolak sebagai ambigu. Payload file JSON hanya angka JSON, bukan string berformat lokal.

## Sistem koordinat

- World right-handed: X timur, Y utara, Z atas. `Vec3 = { x: number; y: number; z: number }` dalam m.
- SceneObject.pose: position world dan yaw CCW dari +X, rad. Rotasi pitch/roll objek belum didukung.
- Crane heading adalah clockwise dari +Y; `yaw = pi/2 - heading`. UI memberi label konvensinya.
- Titik angkat/CoG disimpan load-local; `world = position + rotateZ(yaw, local)`.
- Crane rotation axis dan boom heel merupakan titik eksplisit dalam model, tidak disamakan dengan origin carrier.
- SVG world-to-screen: `(ox + scale*x, oy - scale*y)`; `scale` px/m. Pan/zoom tidak memutasi koordinat objek.
- Three.js default Y-up adapter: world `(x,y,z)` menjadi render `(x,z,-y)`. Engine tetap Z-up.
- Radius horizontal diukur dari sumbu putar crane ke proyeksi hook, bukan jarak 3D atau panjang boom.
- North arrow mengikuti +Y world; rotasi background tidak mengubah definisi world.

## API dan toleransi

`convertLength`, `convertMass`, `convertForce`, `convertPressure`, `toRadians`, `toDegrees`,
`localToWorld`, `worldToLocal`, `worldToScreen`, `screenToWorld`, `worldToThree`.
UI membulatkan tampilan; engine memakai presisi penuh. Toleransi default test analitis: absolute 1e-6 N/m dan
relative 1e-9 (mana yang lebih longgar). Residual gaya engineering: max(1e-3 N, 1e-6*totalForceN);
residual momen: max(1e-3 N*m, 1e-6*totalForceN*max(1,spanM)). Toleransi ini numerik, bukan acceptance keselamatan.
Chart exact match memakai absolute 1e-9 m untuk noise representasi saja; tidak melakukan snapping radius operasional.

Fixture: 1 t→1000 kg→9806.65 N; world (2,3,4)→Three (2,4,-3); yaw pi/2 memetakan local (1,0,0) ke (0,1,0).
Referensi metode: [calculation basis](../engineering/calculation-basis.md).
