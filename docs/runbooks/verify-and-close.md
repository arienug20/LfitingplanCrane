# Verifikasi dan penutupan task

## Definition of done

- Semua acceptance pada card terpenuhi; implementation mengikuti kontrak dan allowlist/amendment.
- Targeted test benar-benar dijalankan dan test count >0; tidak ada .skip/.todo yang menyembunyikan requirement task.
- Check/build dijalankan setelah tersedia pada foundation; unit/impact tests sesuai perubahan.
- Tidak mengubah fixture expected agar cocok dengan bug. Numerical expected dihitung independen.
- Data DEMO tetap dilabeli; gate operational tidak dilewati.
- Evidence lengkap, index diperbarui, dan handoff memberi satu langkah berikut.

## Evidence pada task card

```text
Date / executor / base revision:
Changed files:
Behavior delivered:
Commands actually run + exit codes + test count:
Acceptance checked:
Known failures / not run and why:
Source/method gate impacts:
Review findings and corrections:
Next task:
```

Review seluruh deliverable terkait sebelum mengomentari. Temuan memakai No | Lokasi | Kutipan (salah) | Jenis masalah |
Penjelasan | Rekomendasi (teks benar). Kutip actual code/value/claim, berikan replacement lengkap.
Tidak membuat temuan palsu bila tidak ada kesalahan. Re-run pemeriksaan yang terpengaruh koreksi.

Coding completed tetapi test belum tersedia/blocked → IN_REVIEW/BLOCKED dengan alasan, bukan DONE.
Promosikan dependency-satisfied task ke READY setelah memeriksa gate. Jangan melanjutkan task baru di luar penugasan batch.
Referensi standar/edisi untuk engineering: [register](../engineering/standards-register.md).
