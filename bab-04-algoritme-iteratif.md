# Bab 4 — Menganalisis Algoritme Iteratif

> Prinsipnya sederhana: pilih operasi dasar, hitung berapa kali ia dijalankan, lalu jumlahkan. Jumlah loop pada layar bukan rumus kompleksitas.

## 1. Model biaya dan batas loop

Jika setiap eksekusi operasi dasar memerlukan satu satuan waktu, totalnya T(n) = Σ banyak eksekusi. Biaya inisialisasi dan uji kondisi dapat dihitung saat diminta **T(n) persis**; untuk Θ biasanya biaya dominan sudah cukup. Selalu tentukan apakah batas `< n` atau `≤ n`, mulai dari 0 atau 1, dan apakah *n = 0* diperbolehkan.

Contoh: `i ← 0; selama i < n: kerja; i ← i + 1` menjalankan `kerja` tepat *n* kali untuk *n ≥ 0*. Uji kondisi terjadi *n + 1* kali. Jika setiap uji dan kerja diberi biaya 1, biaya dua operasi itu 2n + 1; bila penambahan *i* ikut dihitung, bertambah *n* lagi. Kedua model menghasilkan Θ(n), tetapi T(n) eksak berbeda.

## 2. Tiga pola dasar

**Langkah tetap.** *i = 0, 2, 4, … < n* menghasilkan ⌈n/2⌉ iterasi. Secara asimtotik Θ(n), bukan Θ(n/2) sebagai kelas berbeda.

**Perkalian tetap.** *i = 1, 2, 4, … ≤ n* menghasilkan ⌊log₂ n⌋ + 1 iterasi untuk *n ≥ 1*. Alasannya, nilai setelah *k* kenaikan adalah 2ᵏ. Untuk *i = n, ⌊i/2⌋, …, 1*, jumlah langkah juga Θ(log n).

**Loop berurutan dan bersarang.** Dua loop sepanjang *n* yang dijalankan satu setelah lain memberi sekitar 2n = Θ(n). Jika loop kedua berada di dalam loop pertama dan selalu panjang *n*, biaya *n·n = n²*. Kata “selalu” penting: batas loop dalam bisa bergantung pada loop luar.

## 3. Loop segitiga: jumlah, bukan tebakan

Untuk *i = 1..n*, jalankan *j = 1..i*. Operasi pada tubuh terdalam dieksekusi 1 + 2 + … + n = n(n+1)/2 kali, jadi Θ(n²). Jika *j = 1..n/i* untuk setiap *i*, totalnya mendekati *n Σᵢ₌₁ⁿ 1/i = Θ(n log n)*. Loop bersarang yang tampak serupa dapat menghasilkan kelas berbeda.

Untuk *j* yang mengganda sampai *i*, jumlah pada setiap *i* adalah ⌊log₂ i⌋ + 1. Maka total Σᵢ₌₁ⁿ (⌊log₂ i⌋ + 1) = Θ(n log n). Batas atas: paling banyak *n(log₂ n + 1)*. Batas bawah: setidaknya *n/2* nilai *i ≥ n/2*, masing-masing membutuhkan Θ(log n) langkah.

## 4. Analisis dua potongan responsi

**Potongan pertama** pada responsi 3 memiliki *i* mulai *n* dan dibagi dua sampai ≤ 1; untuk setiap *i*, *j* mulai 1 lalu dikali 3 sampai ≥ *i*; untuk setiap *j*, *k* berjalan dari 0 sampai *n−1*. Jika *n* besar, jumlah *i* adalah Θ(log n). Untuk nilai *i* di separuh awal tingkat, log₃ *i* masih Θ(log n), sehingga total loop *j* pada seluruh level adalah Θ(log² n). Loop *k* mengalikan biaya dengan *n*. Hasilnya **Θ(n log² n)**. Mengalikan tiga jumlah maksimum juga memberi batas atas yang sama; argumen separuh level membuktikan batas bawahnya.

**Potongan kedua** pada responsi 3: *i* menjadi 1, 2, 4, … ≤ *n*; untuk tiap *i*, *j = 1..i*; untuk tiap *j*, *k = 1, 2, 4, … ≤ j*. Biaya tingkat *i* adalah Σⱼ₌₁ⁱ Θ(log(j+1)) = Θ(i log(i+1)). Jumlah biaya pada *i* yang mengganda didominasi tingkat terakhir dan berorde **Θ(n log n)**. Menulis Θ(n² log n) hanya karena tiga lapis loop akan terlalu longgar.

## 5. Invariant dan terminasi

Selain biaya, loop perlu **invariant**: sifat yang benar sebelum dan sesudah tiap iterasi serta membantu membuktikan hasil akhir. Untuk menjumlah 1..n, invariant setelah *i* elemen diproses ialah `sum = 1 + … + i`. Basis awal *i = 0* memberi jumlah 0; setiap penambahan menjaga invariant; saat *i = n*, hasil benar.

**Terminasi** memerlukan ukuran yang bergerak menuju batas. Soal bank K4 menulis pola `i ← 1; selama i ≤ n: i ← i²`. Untuk *n ≥ 1*, *i* tetap 1 selamanya karena 1² = 1. Jadi tidak ada kompleksitas selesai yang wajar; loop tidak berhenti. Jika mulai dari *i = 2* dan *n ≥ 2*, nilai 2, 4, 16, 256, …, sehingga jumlah langkah Θ(log log n). Detail nilai awal mengubah seluruh jawaban.

## 6. Biaya bit dan input lain

Analisis Θ(1) untuk penjumlahan atau perkalian aritmetika memakai model biaya satuan. Jika nilai tumbuh menjadi angka ribuan bit, biaya operasi itu tidak lagi tetap. Begitu pula perkalian matriks biasa *A[n × m] · B[m × p]* memerlukan Θ(nmp) perkalian skalar, bukan Θ(n³) kecuali ketiganya sama besar.

## 7. Cara mengajar

Sebelum menyederhanakan, buat tabel 3–4 nilai kecil: indeks luar, jumlah langkah dalam, biaya tingkat. Dari pola itu tulis jumlah Σ. Periksa satu kasus batas seperti *n = 1*. Jika indeks tidak berubah atau menjauhi syarat berhenti, jangan memberi Big-O seolah program selesai.

## Latihan bertingkat

1. **Mudah.** Loop *i = 0..n−1* melakukan satu perbandingan tiap iterasi. Berapa perbandingan dan Θ-nya?
2. **Mudah.** Dua loop sepanjang *n* berjalan berurutan. Berapa operasi tubuh jika masing-masing satu operasi per iterasi?
3. **Mudah.** Loop *i = 1; i ≤ n; i ← 2i*. Berapa iterasi tepat untuk *n = 20*?
4. **Sedang.** Loop *i = 1..n* berisi loop *j = 1..i*. Turunkan T(n) tepat untuk operasi tubuh.
5. **Sedang.** Loop *i = 1..n* berisi loop *j = 1,2,4,… ≤ n*. Berikan Θ dan alasan.
6. **Sedang — Adaptasi responsi 2.** Tiga loop penuh sepanjang *n* berada bersarang. Berapa operasi tubuh dan Θ?
7. **Sedang — Adaptasi responsi 2.** Loop luar *bound = 1,2,4,… ≤ n*. Di setiap tingkat ada satu loop Θ(n) lalu loop Θ(log n). Berikan Θ total.
8. **Sulit — Adaptasi responsi 3.** Analisis *i* dibagi 2 dari *n*, *j* dikali 3 dari 1 sampai *i*, dan *k* maju satu dari 0 sampai *n−1*.
9. **Sulit — Adaptasi responsi 3.** Analisis *i* dikali 2 sampai *n*; *j* berjalan 1..*i*; *k* dikali 2 sampai *j*.
10. **Sulit.** Untuk *i = 1..n*, loop dalam berjalan *⌊n/i⌋* kali. Buktikan Θ(n log n).
11. **Sulit — Koreksi bank K4.** Apa yang terjadi pada `i ← 1; selama i ≤ n: i ← i²` untuk *n ≥ 1*? Bagaimana jika mulai dari 2?
12. **Sulit.** Rancang loop yang menghitung jumlah bilangan genap 1..*n* dalam Θ(1), lalu jelaskan mengapa benar.

### Jawaban dan alasan singkat

1. Tepat *n*, jadi Θ(n).
2. Tepat *2n*, jadi Θ(n); dua tahap dijumlah, bukan dikalikan.
3. Nilainya 1, 2, 4, 8, 16; **5** iterasi.
4. Σᵢ₌₁ⁿ i = **n(n+1)/2**, jadi Θ(n²).
5. Tiap *i* menjalankan ⌊log₂ n⌋+1 langkah, jadi *n(⌊log₂ n⌋+1) = Θ(n log n)* untuk *n ≥ 2*.
6. Tepat *n³* operasi tubuh, Θ(n³).
7. Ada Θ(log n) tingkat, tiap tingkat Θ(n + log n) = Θ(n), jadi Θ(n log n).
8. **Θ(n log² n)**; biaya pada setiap tingkat *i* ialah Θ(n log i), lalu jumlahkan sepanjang tingkat pembagian dua.
9. **Θ(n log n)**; tingkat terakhir sendiri Θ(n log n), sedangkan jumlah seluruh tingkat tak melebihi konstanta kali itu.
10. *n Σᵢ₌₁ⁿ 1/i − n < Σ⌊n/i⌋ ≤ n Σ1/i*. Jumlah harmonik Θ(log n), jadi Θ(n log n).
11. Mulai 1 tidak berhenti untuk *n ≥ 1*. Mulai 2, setelah *k* kuadrat nilainya 2^(2ᵏ); jumlah langkah sampai melewati *n* adalah Θ(log log n) untuk *n* cukup besar.
12. Ambil *k = ⌊n/2⌋*. Jumlah 2 + 4 + … + 2k = 2·k(k+1)/2 = **k(k+1)**; jumlah operasi aritmetika tetap di model biaya satuan.

**Sumber bab:** Kuliah 4; Lembar Kerja Responsi Pertemuan 2–4; Bank Soal K4; UTS 2018 dalam ZIP yang diberikan.
