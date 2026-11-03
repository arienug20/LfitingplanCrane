# Delegasi dan integrasi

Default satu executor. Bila pengguna/penugasan mengizinkan delegasi, maksimum dua coding worker independen pada baseline.
Task dikatakan independen bila seluruh prasyarat DONE, tidak mengubah file sama, dan tidak mengubah kontrak yang dibaca worker lain.
Tidak boleh menyimpulkan independen hanya karena ID modul berbeda. Periksa allowlist aktual pada kedua card.

Integrator memiliki TASK_INDEX, PROGRESS, HANDOFF, shared types, lockfile dan keputusan kontrak. Worker tidak menimpa file koordinasi.
Gunakan branch/worktree terpisah hanya bila tersedia dan termasuk workflow yang diotorisasi; jika tidak, serial execution.
Sebelum task baru, periksa existing dirty state; jangan auto-stash/reset/cherry-pick tanpa memahami perubahan.

Payload delegasi: task ID, baseline revision/commit atau file digest, card, contract links, allowlist, expected output dan test command.
Worker result: scope selesai, file berubah, behavior, exact command/exit, failures, blocker, dependency/API change, next step.
Tidak perlu mengirim seluruh percakapan, seluruh katalog atau semua task card.

Integrator memeriksa diff, conflict, API dan assumptions; jalankan targeted tests + impact check. Setelah integrasi baru tandai DONE.
Jika worker mengubah kontrak, hentikan integrasi task yang bergantung dan buat amendment. Tidak ada 'last writer wins'.
Delegasi ini tidak merupakan perintah spawn agent saat penyusunan dokumentasi.
Referensi: [close](verify-and-close.md), [status](../TASK_INDEX.md).
