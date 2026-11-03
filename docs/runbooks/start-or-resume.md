# Mulai atau lanjut — konteks minimum

1. Baca root AGENTS, HANDOFF, satu baris TASK_INDEX, dan task card aktif. Jangan ingest semua docs atau seluruh home folder.
2. Pastikan tugas coding memang diotorisasi; paket ini sendiri hanya dokumentasi.
3. Periksa folder, Git jika tersedia, file belum tersimpan, command availability dan checkpoint. Jangan reset perubahan orang lain.
4. Pilih task READY. Jika dependency belum DONE atau gate task terbuka, pilih task lain yang tidak tergantung gate itu.
5. Baca hanya kontrak yang dirujuk. Jika file prasyarat belum ada padahal status DONE, catat inkonsistensi sebelum melanjutkan.
6. Klaim task IN_PROGRESS pada index dengan executor/session ID dan waktu. Satu task per worker.
7. Implementasikan allowlist; pastikan input/output dan acceptance tidak berubah.
8. Jalankan command card dan pemeriksaan impact. Simpan bukti nyata, perbarui status dan handoff.

Prompt awal singkat:

> Baca AGENTS.md, docs/HANDOFF.md dan docs/TASK_INDEX.md. Kerjakan satu task READY sesuai card dan kontraknya.
> Jangan mengubah scope atau mengarang data engineering. Verifikasi, catat bukti, dan tinggalkan handoff sebelum berhenti.

Tidak perlu memilih model berdasarkan dokumen; runbook model-agnostic. Untuk versi/biaya model, verifikasi sumber resmi saat keputusan itu diminta.
Referensi operasional: [task index](../TASK_INDEX.md), [blocker](handle-blockers.md).
