# Kontrak beban dan rigging v1

## Beban

`Load`: id, sceneObjectId, massKg, cogLocal(Vec3), liftingPoints[{id,localPosition}], massSourceRef,
cogSourceRef, uncertaintyNote. Titik angkat/CoG bisa di luar shape proxy untuk data riil tetapi menghasilkan warning,
bukan diam-diam dipindahkan ke pusat geometri. Mass harus >0 untuk evaluation.
Load orientation yaw tetap selama tandem. Single juga menggunakan vertical hook above combined suspended CoG;
load yaw dapat ditetapkan per langkah hanya jika rigging mengikuti constraint dan check geometri.

## Assembly

`RiggingComponent`: id, kind(sling|shackle|spreader|hookBlock), ownMassKg, wllN,
ratingBasis, sourceRef, certificateRef?, geometry, connectionIds[]. WLL dalam N; rating tonne dikonversi g tepat sekali.
`RiggingAssembly`: id, loadId, craneId, components, lowerPointIds, hookPoint, method('single_vertical'|'symmetric_two_leg'|'rated_assembly'),
manufacturerAssemblyRatingN?, sourceRef, connections, massAllocation.
Tidak ada sizing struktur beam/lug/shackle. User memasukkan rating bersumber; aplikasi membandingkan demand.

## Metode A0

- Single vertical: load line vertikal, demand sama dengan gaya yang dialokasikan pada assembly.
- Symmetric two leg: lower points satu elevasi, equal length/sudut, hook di atas midpoint dan combined CoG di garis vertikal itu.
  Vertical load V terbagi dua; T=V/(2*cos(theta)), theta dari vertikal, 0<=theta<pi/2.
  Geometry tidak simetris atau resultan tidak setimbang → unsupported, bukan asumsi dua sama rata.
- Rated assembly: membandingkan gaya total pada assembly terhadap rating konfigurasi pabrikan yang cocok.
  Empat kaki tidak dihitung masing-masing W/4. Jika konfigurasi/rating tidak cocok → incomplete/unsupported.
- Hitch, bending efficiency, temperature dan derating hanya dari rating/config sumber; tidak ada faktor universal.

## Massa dan constraint

Setiap ownMass dihitung sekali. `massAllocation` membedakan shared-below-hook dengan local position pada load,
atau crane-specific dengan craneId. Shared components ikut combined CoG statis; crane-specific accessories ditambah ke demand crane itu.
Hook block selalu crane-specific dan terpisah dari payload. Beban di hook tidak termasuk berat crane/counterweight.
RIG-004 mengeluarkan ledger componentId→mass/force/allocation; SGL/TND memakai ledger sama.
WLL missing bukan unlimited. Slack, sudut horizontal, dangling connections dan ketidakcocokan panjang dilaporkan.
Referensi: [calculation basis](../engineering/calculation-basis.md), [benchmark](../engineering/benchmark-cases.md).
