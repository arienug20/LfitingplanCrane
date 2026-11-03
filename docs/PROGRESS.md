# Progress dan milestone

Tanggal baseline: 2026-11-02. Paket dokumen selesai disusun; **aplikasi belum dimulai**.
Status operasional tiap task hanya di [TASK_INDEX](TASK_INDEX.md).

| Milestone | Paket yang wajib DONE | Bukti |
|---|---|---|
| M0 Fondasi | FND-001 sampai FND-006 | Belum ada |
| M1 Workspace | MOD-001 sampai MOD-006; PRJ-001 sampai PRJ-006; SITE-001 sampai SITE-006 | Belum ada |
| M2 Single/rigging | CAT-001 sampai CAT-006; SGL-001 sampai SGL-006; RIG-001 sampai RIG-006 | Belum ada |
| M3 Tandem/simulasi | TND-001 sampai TND-006; SIM-001 sampai SIM-006 | Belum ada |
| M4 Review | CLR-001 sampai CLR-006; REV-001 sampai REV-006 | Belum ada |
| M5 Deliverable | OUT-001 sampai OUT-006 | Belum ada |
| M6 Release | VAL-001 sampai VAL-006 dan gate engineering/sumber terselesaikan | Belum ada |

Milestone bukan urutan semua pekerjaan; gunakan DAG task untuk pekerjaan paralel yang diizinkan.
CAT-002/VAL-006 dapat tertahan sumber engineering meskipun fitur demonstrasi lain maju.

## Penghalang lintas task

- G-STD-01: klausul dokumen standar lengkap belum ditelaah; memblokir signoff engineering pada VAL-001/VAL-006.
- G-CAT-01: tabel sumber penuh, hak distribusi, dan transkripsi belum diverifikasi; memblokir katalog aktif CAT-002/VAL-006.
- G-POL-01: policy operasional spesifik proyek belum diberikan; demo policy tidak boleh menjadi persetujuan operasional.

Jangan menandai seluruh proyek BLOCKED: fondasi, kontrak, editor, serta engine dengan fixture sintetis tetap bisa dikerjakan.
