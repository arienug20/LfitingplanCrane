# Menangani blocker tanpa kehilangan track

Jenis: ENV (runtime/permission/dependency tool), CONTRACT (kontradiksi/interface), SOURCE (data OEM/standar),
METHOD (di luar basis), TEST (expected atau verifikasi belum jelas), SCOPE (perubahan di luar task).

Catat ID unik BLK-<task>-<nomor>, task, exact error/quote, langkah reproduksi, input tersanitasi,
expected vs actual, upaya yang telah dilakukan, file terdampak, keputusan/bukti yang diperlukan, dan task lain yang masih bisa maju.
Jangan menyertakan credential, token, commercial/payroll, atau seluruh log sensitif.

Aturan:

- Beri BLOCKED hanya pada task terdampak; kontrak dan gate tidak ditafsir sebagai persetujuan engineering.
- Dua kegagalan sama → diagnosis terarah dan catatan; jangan loop instalasi/build/prompt tanpa informasi baru.
- Tanpa angka OEM, gunakan fixture terpisah untuk feature development dan biarkan katalog nyata belum aktif.
- Tanpa standar lengkap, uji model statis sebagai demo; tidak mengarang klausul/approval.
- Gate sumber hanya ditutup dengan evidence yang disebut register. Ubah tanggal/status setelah bukti nyata tersedia.
- Bila filesystem gagal, hentikan klaim saved. Laporkan lokasi dan error; jangan membuat file di proyek lain sebagai jalan pintas.
- Eskalasi hanya keputusan yang tidak dapat diperoleh dari inspeksi/read-only yang diizinkan.

Keluar blocker: catat bukti perbaikan, periksa prasyarat ulang, ubah menjadi READY, lalu resume dari checkpoint terakhir.
Lihat [PROGRESS](../PROGRESS.md) untuk gate global dan [HANDOFF](../HANDOFF.md) untuk konteks sesi.
