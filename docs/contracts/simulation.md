# Kontrak lintasan, tahap, dan waktu v1

## Data

`LiftPlan`: id,mode,loadId,craneIds,riggingAssemblyIds,waypoints[],policyId.
`Waypoint`: id,tS>=0,loadPosition(Vec3),loadYawRad, action(hoist|slew|luff|hold),notes.
Time strict increasing, >=2 waypoints; satu hold diwakili dua waypoint pada posisi sama dengan t berbeda.
Crane base tidak berpindah selama satu lift. Perubahan panjang boom, outrigger atau counterweight membuat lift/config baru.
Tandem yaw dan elevasi relatif antar attachment tetap; no upending. Hook target dari transform lifting point + assembly geometry,
bukan dua garis bergerak bebas yang memanjang/memendek agar animasi tampak cocok.

## Kinematika deterministik

`stateAt(plan,tS)`: clamp ke rentang untuk viewport; engine meminta waktu dalam rentang.
Load translation linear piecewise. Single yaw shortest-arc interpolation hanya jika endpoint constraint valid; tandem yaw konstan.
Derive hook position, radius dan boom luff/slew dari model heel/tip/hook-drop. Main boom nominal length fixed;
nonreal solution/limits violated unsupported. Jangan men-scale boom untuk mengejar hook.
Hoist mengubah hook-drop, slew mengubah heading boom, luff mengubah angle; validator memastikan action sesuai geometri.
Playback speed hanya clock, tidak mengubah physical inputs atau waktu plan. Tidak mensimulasikan kecepatan/dinamika OEM.

## Sampling

`samplePlan`: masukkan seluruh waypoint dan subdivide segmen agar translation <=0.10 m, yaw/boom angle <=1 degree,
time step <=0.10 s. Gunakan batas yang paling rapat, deterministic, include endpoints tanpa duplikasi.
Tandai settings dalam result. Batas 20000 samples; jika terlampaui batalkan dengan reason `sampling_limit`,
jangan coarsen diam-diam. Jangkauan/evaluasi chart dan clearance mengonsumsi sample schedule sama.
Chart exact-only bisa menghasilkan banyak sample unsupported; tampilkan coverage dan controlling valid subset secara eksplisit.
Tidak boleh menyimpulkan capacity pass untuk seluruh lintasan dari dua endpoint yang tersedia.

## Tahapan

`ConstructionStage`: id,name,order,durationS,notes,objectOverrides[{objectId,visible,pose?}],activeLiftId|null.
Setiap tahap menyimpan full effective overrides dari baseline scenario, bukan delta dari tahap sebelumnya.
Seek langsung sama dengan sequential playback. Maksimum satu lift aktif per tahap; tandem adalah satu lift dengan dua crane.
Stage duration adalah durasi presentasi, bukan jadwal CPM. Task membuat prepared/rigging/trial-lift/lift/place/de-rig contoh.
Referensi: [scene](scene-objects.md), [evaluation](lift-evaluation.md).
