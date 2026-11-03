# Basis perhitungan A0 — metode development, belum signoff operasional

## 1. Pendahuluan

Engine menyediakan evaluasi transparan dalam batas model; bukan sertifikasi crane, desain struktur, atau izin lifting.
Dokumen ini mengunci metode untuk coding dengan fixture. Status standar/sumber terdapat pada register terkait.

## 2. Tujuan

Menentukan persamaan, unit, asumsi dan respons kegagalan agar executor tidak merancang metode baru saat membuat UI.
Setiap hasil menyimpan inputHash, engineVersion, source version dan policy; semua massa ditelusuri ke ledger.

## 3. Dasar teori dan asumsi

Statika benda kaku, gaya hook vertikal, base crane diam, ground level sesuai basis chart yang dipilih.
Crane tidak dilendutkan melalui solver struktur; boom geometry sederhana memiliki accuracy note. Wind/deflection/soil
tidak dinyatakan memenuhi hanya karena utilisasi lolos. Catatan dan batas pabrikan wajib dibawa ke hasil.
Tandem: dua resultant support vertikal, span horizontal >0; combined shared CoG berada pada garis proyeksi kedua support.
Jika CoG off-line, gaya vertikal dua titik saja tidak dapat menyeimbangkan seluruh momen; hasil unsupported.
Tidak ada upending, ground contact transition, orientasi berubah atau negative support reaction yang diklem menjadi nol.

## 4. Persamaan dan satuan

- Berat: W=m*g; m kg, g=9.80665 m/s², W N.
- Combined CoG: c=sum(m_i*p_i)/sum(m_i) untuk shared components; p_i world m.
- Radius: r=norm((hook-axis).xy), m. Hook height adalah world Z hook; available height dibanding model heel/tip/drop.
- Untuk span D=norm((B-A).xy), u=(B-A).xy/D, a=dot((c-A).xy,u), b=D-a.
  R_A=W*b/D; R_B=W*a/D. Valid a,b>=0, serta residual cross-line CoG sesuai tolerance metode.
- Equilibrium: sum F=0 dan sum((p_i-c) cross F_i)=0. Gaya N, momen N*m. Check nilai residual, bukan hanya R_A+R_B.
- Hitung physical tanpa factors. Untuk design, statika linear dievaluasi lagi memakai berat tiap kategori dikali policy factor,
  sehingga distribusi massa shared tidak kehilangan moment contribution. Crane-specific accessories tidak dimasukkan shared CoG.
- Demand tiap crane = allocated shared design reaction + own crane-specific rigging/hook forces. Gross/net adjustment
  hanya sesuai daftar deduction source; komponen yang sama tidak boleh dihitung dua kali.
- Rating chart: C_N=C_kg*g. Utilisasi U=100*D_N/C_N. Exceeds jika U>policy limit, bukan hanya >100.
- Dua sling simetris: T=V/(2*cos(theta)), theta dari vertikal. Check geometri/sumber WLL sebelum membandingkan.
- Tekanan mat q=R_external/A, Pa; R_external dari data reaksi tersumber, A m². Tidak menghitung reaksi dari total berat/4.

Cross-line CoG numeric tolerance 1e-6 m; tolerance residual lain di kontrak satuan. Ini batas numerik model, bukan toleransi
keselamatan lapangan. Geometri crane menggunakan inverse relation fixed boom terhadap heel dan hook-drop, dengan limits sumber.

## 5. Analisis, invalid dan sumber

Mass/length nonfinite atau negatif invalid. Missing source/policy/rating incomplete. Kondisi di luar geometri/metode unsupported.
Tidak semua status dihentikan pada error pertama: tampilkan check lain yang masih terdefinisi tanpa menghasilkan angka semu.
Chart hanya exact source configuration dan exact radius A0; lintasan dengan gap coverage tidak memperoleh pass keseluruhan.
Metode rated assembly hanya demand vs supplied WLL; tidak mendesain lug, shackle, sling material, atau spreader.
Faktor pengangkatan/limit utilisasi belum ditentukan standar secara universal dalam dokumen ini; wajib basis proyek.

## 6. Kesimpulan dan rekomendasi

Implementasikan metode yang dibatasi ini, uji benchmark, dan pertahankan operationalReady=false sampai G-STD-01,
G-CAT-01, G-POL-01 terselesaikan. Temuan memerlukan quote/objek → jenis/penyebab → teks/metode pengganti lengkap.
Referensi: [ASME dan edisi](standards-register.md), [sumber crane](crane-source-register.md), [benchmark](benchmark-cases.md).
