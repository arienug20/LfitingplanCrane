# Aturan executor LiftPlan Studio

## Mulai dan lanjut

1. Baca file ini, [HANDOFF](docs/HANDOFF.md), dan baris tugas pada [TASK_INDEX](docs/TASK_INDEX.md).
2. Periksa kondisi filesystem dan perubahan aktual. Repo belum tentu sudah diinisialisasi Git.
3. Pilih satu task `READY`; baca task card serta kontrak yang ditautkan. Jangan membaca seluruh 78 card.
4. Tandai `IN_PROGRESS`, implementasikan batas task, jalankan verifikasi, lalu buat bukti dan handoff.
5. Task `DONE` memerlukan acceptance criteria dan bukti, bukan sekadar kode yang tampak selesai.

## Sumber kebenaran

- Arahan pengguna terbaru berlaku atas dokumen lokal. Catat perubahan baseline sebelum meneruskan.
- Kontrak data/metode: `docs/contracts/` dan `docs/engineering/calculation-basis.md`.
- Keputusan: `docs/DECISIONS.md`. Arsitektur: `docs/ARCHITECTURE.md`.
- Status task hanya di `docs/TASK_INDEX.md`; task card tidak menyimpan salinan status.
- Bila dua dokumen normatif bertentangan, catat blocker. Jangan memilih aturan secara diam-diam.

## Batas kerja

- Proyek ini baru. Jangan mengubah `../rekacrane`, instruksi global, kredensial, atau proyek lain.
- Saat penugasan hanya dokumentasi, jangan scaffold, memasang dependensi, atau menulis kode aplikasi.
- Saat coding diotorisasi, satu task aktif per executor. Jangan menambah fitur, mengganti stack, atau merombak kontrak di luar card.
- File di luar allowlist card membutuhkan amendment tertulis di handoff sebelum diubah. Jika dampaknya kontrak/arsitektur, jadikan blocker dan pecah task.
- Jangan menghapus pekerjaan pengguna atau menyatakan test lolos tanpa benar-benar menjalankannya.
- File kode baru dan API harus cocok dengan kontrak; komponen UI tidak memuat rumus engineering sendiri.

## Engineering

- Angka pabrikan tidak boleh diciptakan. Fixture sintetis tidak boleh diberi identitas crane sungguhan.
- Data chart kandidat/PDF/OCR tidak aktif untuk evaluasi sebelum verifikasi sumber.
- Tidak ada interpolasi kapasitas default. Di luar tabel/metode menghasilkan status yang ditetapkan kontrak.
- Gate referensi/data yang terbuka mengizinkan development dengan fixture, tetapi memblokir klaim penggunaan operasional.
- Perubahan rumus, satuan, deduction, dan pembagian tandem membutuhkan benchmark dan review independen.
- Jangan mengubah fail menjadi pass dengan menghapus test, melonggarkan toleransi, atau memberi nilai default tersembunyi.

## Delegasi dan konteks

- Default satu executor; delegasi hanya bila penugasan mengizinkan. Maksimum dua coding worker independen untuk baseline ini.
- Jangan memberi dua worker file yang sama. Kontrak inti, lockfile, dan status diintegrasikan berurutan.
- Worker membaca task + kontrak relevan, mengembalikan file berubah, test, hasil, dan blocker. Integrator yang memperbarui status bersama.
- Tidak ada model wajib. Task dibuat agar Luna/Terra maupun executor lain menerima kontrak yang sama.
- Setelah satu acceptance gagal dua kali dengan penyebab sama, rangkum bukti dan lakukan diagnosis terarah; jangan terus mengulang prompt/build yang sama.

## Menutup tugas

Gunakan [verify-and-close](docs/runbooks/verify-and-close.md). Simpan bukti di bagian Evidence pada task card, perbarui index dan handoff.
Jangan commit/push/publish/deploy kecuali termasuk penugasan. Commit hash bersifat opsional bila belum ada Git.
Rujukan: [brief](docs/PROJECT_BRIEF.md), [keputusan](docs/DECISIONS.md), [standar](docs/engineering/standards-register.md).
