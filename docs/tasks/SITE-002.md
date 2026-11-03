# SITE-002 — Background gambar dan PDF

## Tujuan

PNG/JPEG/PDF staging, pilih halaman, opacity/rotate/lock, originalasset persisted.

## Prasyarat dan gate

[SITE-001](SITE-001.md), [PRJ-002](PRJ-002.md)

Tidak ada gate sumber khusus; gunakan data sintetis jika data nyata belum tersedia.

## Bacaan wajib

- [Scene dan background](../contracts/scene-objects.md)
- [Proyek, persistensi dan snapshot](../contracts/project-format.md)

## Kondisi awal

Artefak seluruh dependensi harus tersedia dan terverifikasi. Jika status index tidak cocok dengan filesystem, catat inkonsistensi sebelum coding.
Gunakan baseline project baru, bukan source rekacrane. Tidak perlu membaca semua task lain.

## Batas pekerjaan

Kerjakan perilaku pada card ini. Jangan mengganti metode/satuan/stack, menambah fitur lintas modul,
atau memperbarui snapshot sumber secara diam-diam. Kontrak adalah interface normatif; API yang belum ada dibuat pada allowlist.
Jika kontrak belum mencukupi untuk acceptance, catat amendment/blocker sebelum memilih asumsi baru.

## File yang boleh diubah

- `src/ui/site/BackgroundImport.tsx`
- `src/view2d/Background.tsx`
- `src/application/background.ts`
- `src/ui/shell/Workspace.tsx`
- `tests/e2e/site-002.spec.ts`

Koordinasi `TASK_INDEX.md`, `HANDOFF.md`, dan evidence card dilakukan executor tunggal atau integrator.
Jika `src/ui/shell/Workspace.tsx` tercantum, perubahan di file itu hanya wiring panel/viewport fitur ini;
ini shared integration file dan tidak boleh diubah dua worker bersamaan. UI task harus dapat dicapai dari shell, bukan komponen yatim.
Perubahan path di luar daftar memerlukan amendment tertulis dengan alasan dan dampak; perubahan kontrak memerlukan review.

## Kontrak input/output

PNG/JPEG/PDF staging, pilih halaman, opacity/rotate/lock, originalasset persisted.
Field, unit, reason/status, dan batas metode mengikuti bacaan wajib. Input tidak valid tidak memperoleh angka default tersembunyi.
Fixture test memakai `SYNTHETIC-ONLY`; expected result tidak boleh dihitung dengan fungsi production yang sedang diuji.

## Langkah implementasi

1. Render PDF lokal viaPDF.js dan batas preview4096px.
2. Validasi type/size dan simpan original sebelum mengganti background.
3. Tambahkan pemeriksaan acceptance di bawah pada file test yang dialokasikan bila ada; catat inspeksi UI/source yang tidak otomatis.
4. Jalankan verifikasi dan periksa diff terhadap allowlist. Perbaiki penyebab kegagalan tanpa mengurangi acceptance.

## Acceptance criteria dan test cases

- [ ] PDF page selection benar.
- [ ] File>limit ditolak dengan pesan.
- [ ] Cancel/rusak PDF tidak menghilangkan background lama.
- [ ] API, satuan, source/version, dan perilaku kegagalan konsisten dengan kontrak terkait.
- [ ] Bukti menyebut command aktual, exit status, test count atau inspeksi yang benar-benar dilakukan.

## Perintah verifikasi

Jalankan dari root `liftplan-studio`. Command disediakan oleh [foundation/arsitektur](../ARCHITECTURE.md).
Jangan mengklaim test dijalankan jika harness prasyarat belum tersedia. Tidak memasang tool global atau mengunduh dokumen OEM saat test.

```bash
npm run test:e2e -- tests/e2e/site-002.spec.ts
npm run check
npm run build
```

## Bukti penyelesaian

Belum ada implementasi atau test aplikasi yang dijalankan. Saat eksekusi, isi tanggal/executor/base revision,
changed files, perilaku selesai, command+exit+test count, hasil tiap acceptance, failure tersisa, dan gate impact.
Review memakai kutipan aktual → jenis/penyebab → replacement lengkap, sesuai [runbook](../runbooks/verify-and-close.md).

## Handoff

Perbarui [index](../TASK_INDEX.md) dan [handoff](../HANDOFF.md). Pilih task berikut berdasarkan dependensi yang DONE,
bukan urutan nama file. Jangan memulai task baru di luar batch yang ditugaskan.
