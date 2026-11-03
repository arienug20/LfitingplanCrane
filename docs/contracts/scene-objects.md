# Kontrak objek scene v1

## Objek

`SceneObject`: id, tag unik/scenario, name, kind, pose(position Vec3,yawRad), dimensions(lengthM,widthM,heightM),
layerId, visible, locked, color, geometryAccuracyNote, sourceRefs[] dan properties sesuai kind.
Kind: vessel,tank,skid,pipe,column,beam,trailer,obstacle,zone,crane,load.
Shape proxy: box, verticalCylinder, horizontalCylinder, polygonPrism. Tidak ada arbitrary mesh import A0.
Vessel/pipe horizontal memakai sumbu panjang local +X; cylinder vertikal sepanjang +Z. Origin komponen di pusat footprint pada base Z.
Properties crane/load menyimpan domain ID, bukan salinan berat/chart/CoG.
`Layer`: id,name,visible,locked. Effective visibility = layer.visible && object.visible && stage visibility override.

## Editing

Selection hanya UI state. Object locked atau layer locked tidak bisa digeser/diubah, tetapi bisa dipilih untuk inspeksi.
Snap grid default 0.5 m (dapat diubah positif); snapping on/off tidak mengubah objek sampai command commit.
Drag world XY; elevasi dimasukkan panel. Semua input dimensi memiliki unit label. Duplicate menghasilkan ID dan tag baru.
Remove object dengan lifting reference memerlukan preview daftar referensi; jangan meninggalkan dangling IDs.
Zone polygon: >=3 titik, non-self-intersecting, elevation+height; role work/laydown/access/exclusion.
Zone bukan desain jalan/turning analysis; trailer hanya representasi parametrik pada A0.

## Background

`Background`: assetId, pageIndex (0-based PDF), widthPx,heightPx, worldOrigin, rotationRad, metersPerPixel, opacity, locked.
Kalibrasi dua titik pixel: metersPerPixel = knownDistanceM / pixelDistance. Jarak >0; dua titik berbeda.
Transform background dan objek world disimpan terpisah. Recalibrate background tidak men-scale seluruh objek tanpa command eksplisit.
PDF limit 25 MiB, image 10 MiB. Render preview maksimum sisi 4096 px; original tetap disimpan.
PDF multipage pengguna memilih satu halaman untuk background; chart import dapat membaca halaman lain secara terpisah.
Jika data tidak ada, grid tetap bisa dipakai. PDF tidak menjadi geometri collision otomatis.

## Integrasi viewport

2D/3D membaca objek sama melalui selector. ID selection sama, kamera terpisah. Hide layer tidak menghapus objek atau hasil.
Ukuran clearance berasal engine/proxy world, bukan jarak pixel. Camera presets top/front/side/isometric dan orbit tidak mengubah model.
Reference: [units/coordinates](units-and-coordinates.md), [simulation](simulation.md).
