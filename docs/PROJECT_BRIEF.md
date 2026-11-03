# Project brief — baseline A0

## Pendahuluan

LiftPlan Studio membantu planner dan reviewer menyusun model serta evaluasi pekerjaan lifting dalam area konstruksi.
Dokumen ini menjadi kontrak produk bagi executor. Proyek baru berdiri sendiri, tanpa migrasi dari `rekacrane`.

## Tujuan

Alur wajib: buat proyek → denah/grid → objek/crane → beban/rigging → lintasan → evaluasi → review → PDF/PNG/WebM.
Target desktop Chrome/Edge WebGL2; bahasa Indonesia; operasi inti lokal setelah aplikasi dan aset dimuat.

## Dasar teori dan cakupan

| Kebutuhan | Kelompok task |
|---|---|
| Fondasi, kontrak tipe, proyek lokal, file portabel | FND, MOD, PRJ |
| Denah PNG/JPEG/PDF atau grid manual; layer, snap, ukuran; 2D/3D | SITE |
| Crane parametrik, tiga model awal, chart manual/CSV/PDF | CAT, SGL |
| Beban/CoG, rigging dan single lift | SGL, RIG |
| Tandem statis dua crane, orientasi beban tetap | TND |
| Lintasan, playback, tahapan konstruksi | SIM, REV |
| Clearance dan konflik geometris | CLR |
| Alternatif, komentar, revisi dan kesiapan keluaran | REV |
| PDF teknis, denah/elevasi PNG, WebM | OUT |
| Benchmark, failure cases, integrasi dan rilis | VAL |

Objek: vessel, tank, skid, pipe, column, beam, trailer, box/cylinder obstacle, area polygon, crane dan load.
Geometri disederhanakan dengan ukuran dan accuracy note. Tidak ada CAD/BIM import, akun, backend, kolaborasi simultan,
CPM/resource leveling, upending, ground-reaction solver, structural solver, atau dinamika ayunan pada A0.
Rigging empat kaki hanya memakai rating assembly yang bersumber; tidak ada asumsi pembagian empat sama rata.

## Persamaan dan satuan

Metode normatif: [calculation basis](engineering/calculation-basis.md). Satuan internal SI sesuai [kontrak satuan](contracts/units-and-coordinates.md).
Pengaturan faktor dan batas utilisasi memerlukan basis proyek; tidak ada angka universal tersembunyi.

## Analisis dan penerimaan

- Scene yang sama menghasilkan posisi identik di 2D, 3D, seek, reload, dan export.
- Evaluasi chart mengikat konfigurasi dan versi sumber; nilai tidak tersedia tetap tidak tersedia.
- Radius/jangkauan, demand/capacity, rigging dan tandem memiliki fixture expected-result.
- Perubahan input menginvalidasi hasil; laporan lama tidak dipresentasikan sebagai hasil revisi baru.
- Tidak ada label keselamatan global. Panel menunjukkan evaluasi per pemeriksaan beserta batas metode.
- Preview/demo dengan fixture dapat dikembangkan saat gate engineering masih terbuka; laporan bertanda DRAFT.
- Rilis operasional menunggu seluruh gate pada register engineering dan sumber data.

## Kesimpulan dan rekomendasi

Bangun sesuai DAG task, satu task per executor. Utamakan kontrak dan benchmark sebelum UI engineering.
Model biaya lebih rendah tidak diminta menebak metode atau angka sumber. Keputusan yang belum memiliki bukti menjadi blocker terarah.
Referensi: [standar dan edisi](engineering/standards-register.md), [sumber crane](engineering/crane-source-register.md).
