# Bab 6 — Algoritme Pencarian dan Asumsi Data

> Pertanyaan utama bukan “algoritme mana paling cepat?”, melainkan “sifat data apa yang membuat langkah pencarian itu benar?”

## 1. Spesifikasi sebelum memilih algoritme

Pencarian dapat berarti menguji keberadaan, mengembalikan satu posisi, posisi pertama, atau semua posisi. Input boleh kosong atau mengandung nilai sama. Keputusan ini mengubah algoritme yang benar. Misalnya binary search biasa yang berhenti saat menemukan target dapat mengembalikan salah satu dari banyak duplikat, bukan selalu indeks pertama.

Untuk larik tidak terurut, linear search membandingkan target dengan elemen satu per satu. Ia memerlukan paling banyak *n* perbandingan, ruang tambahan Θ(1), dan bekerja tanpa syarat pengurutan. Jika target di awal, biayanya Θ(1). Ketika data berubah sering dan hanya dicari sekali, biaya mengurutkan data lebih dahulu mungkin tidak sepadan.

## 2. Binary search: mengapa boleh membuang separuh?

**Syarat:** larik terurut naik dan dapat diakses menurut indeks. Simpan rentang kandidat `[lo, hi)`; mula-mula `[0, n)`. Selama *lo < hi*, pilih *mid = lo + ⌊(hi − lo)/2⌋*. Jika A[mid] < target, semua indeks ≤ mid terlalu kecil, jadi tetapkan *lo = mid + 1*. Jika A[mid] > target, semua indeks ≥ mid terlalu besar, jadi tetapkan *hi = mid*. Jika sama, satu posisi ditemukan.

**Invariant:** jika target ada pada larik, setidaknya satu kemunculannya masih berada dalam rentang kandidat. Setelah perbandingan, urutan larik membenarkan pembuangan satu sisi. Rentang menyusut, sehingga algoritme berhenti. Tanpa data terurut, kesimpulan “semua di kiri lebih kecil” tidak sah.

Ukuran kandidat paling banyak dibagi dua per langkah. Jadi pencarian terburuk Θ(log n), terbaik Θ(1), dan ruang tambahan Θ(1) untuk versi iteratif. Untuk menghitung jumlah perbandingan tepat, tentukan apakah satu putaran menghitung satu perbandingan tiga arah atau dua uji `<` dan `>`.

### Kemunculan pertama dan duplikat

Untuk mencari indeks pertama dengan nilai ≥ target (*lower bound*), saat A[mid] ≥ target jangan berhenti: pertahankan kiri dengan *hi = mid*; saat A[mid] < target, set *lo = mid + 1*. Ketika *lo = hi*, indeks itu adalah posisi pertama ≥ target. Periksa bahwa *lo < n* dan A[lo] = target agar keberadaan target terjamin. Pada [5,5,5,5], target 5 memberi indeks 0; target 8 memberi “tidak ditemukan”. Ini menangani kasus yang muncul di Kuliah 6.

## 3. Memilih strategi menurut data

| Keadaan | Pilihan wajar | Alasannya |
| --- | --- | --- |
| Satu pencarian, data tidak terurut | Linear search | Tidak ada biaya persiapan. |
| Banyak pencarian, data statis dan dapat diurutkan | Urutkan sekali lalu binary search | Total biaya ≈ O(n log n + q log n) untuk *q* pencarian. |
| Data sudah terurut dan akses indeks murah | Binary search | Separuh kandidat dibuang tiap langkah. |
| Hanya perlu keanggotaan rata-rata, hash tersedia | Hash table | Pencarian rata-rata O(1), tetapi worst case bisa lebih buruk dan butuh ruang ekstra. |
| Data terurut tetapi akses hanya sekuensial | Periksa struktur datanya | Binary search atas linked list kehilangan keunggulan akses acak. |

Jump search melompat blok lalu memindai satu blok, dengan ukuran lompatan sekitar √n sehingga Θ(√n) per pencarian pada larik terurut. Interpolation search menebak posisi dari nilai, bisa cepat untuk sebaran nilai yang cukup seragam tetapi memiliki worst Θ(n). Keduanya memerlukan asumsi lebih kuat daripada “data terurut”; untuk pengajaran awal, utamakan linear dan binary search.

## 4. Pencarian pada matriks terurut penuh

Responsi 6 menyatakan A adalah matriks *m × n* yang semua elemennya terurut dari baris pertama sampai terakhir; selain syarat elemen terakhir baris *i* ≤ elemen pertama baris berikutnya, **setiap baris juga harus terurut** untuk menyimpulkan urutan total. Dengan kedua syarat itu, bayangkan matriks sebagai larik virtual panjang *mn*. Posisi datar *p* memetakan ke baris *⌊p/n⌋* dan kolom *p mod n*. Terapkan binary search: Θ(log(mn)) perbandingan dan Θ(1) ruang ekstra.

Jika hanya diketahui syarat antarbaris tetapi isi tiap baris acak, larik virtual tidak terurut; binary search tidak sah. Jika setiap baris terurut tetapi batas antarbaris tidak disusun, strategi dapat berbeda. Menyebut asumsi tambahan ini lebih penting daripada menghafal jawaban Θ(log mn).

## 5. Tugas pendamping dari responsi: pemangkatan modulo

Responsi 6 juga meminta menghitung *aⁿ mod m*. Metode lurus mengalikan *a* sebanyak *n* kali lalu mengambil modulo, membutuhkan Θ(n) perkalian dalam model satuan dan bilangan perantara bisa sangat besar. Mengambil modulo setelah **setiap** kali mengalikan menjaga hasil di bawah *m* karena `(xy) mod m = ((x mod m)(y mod m)) mod m`; jumlah iterasi masih Θ(n), tetapi ukuran bilangan jauh lebih terkendali.

**Repeated squaring** memakai representasi biner *n*. Simpan `hasil ← 1`, `basis ← a mod m`, `sisa ← n`. Pada tiap langkah, jika *sisa* ganjil, set `hasil ← hasil·basis mod m`; lalu set `basis ← basis² mod m` dan `sisa ← ⌊sisa/2⌋`. Ketika *sisa = 0*, `hasil` adalah *aⁿ mod m*. Invariant-nya: `hasil · basis^sisa ≡ aⁿ (mod m)`. Karena *sisa* dibagi dua tiap putaran, diperlukan Θ(log(n+1)) perkalian modular untuk *n ≥ 1*. Untuk *n = 0*, hasil 1 mod *m*; anggap *m > 0*.

Contoh *3¹³ mod 7*: 13 = 8 + 4 + 1. Kuadrat modular berturut-turut 3¹ ≡ 3, 3² ≡ 2, 3⁴ ≡ 4, 3⁸ ≡ 2 (mod 7). Kalikan yang dipilih: 2·4·3 = 24 ≡ **3 (mod 7)**. Ini contoh lain bagaimana pembagian dua memunculkan logaritma.

## 6. Tugas pendamping: submatriks (n−1) × (n−1) dengan jumlah maksimum

Dari matriks *n × n*, submatriks kontigu ukuran *(n−1) × (n−1)* hanya memiliki **empat** posisi: buang baris atas/bawah dan kolom kiri/kanan. Hitung jumlah seluruh elemen S dalam Θ(n²), jumlah tiap baris pinggir dan tiap kolom pinggir. Untuk posisi yang membuang baris *r* dan kolom *c*, jumlahnya `S − jumlahBaris[r] − jumlahKolom[c] + A[r,c]`; sel pojok yang terbuang dua kali harus ditambah kembali. Memilih maksimum dari empat nilai memerlukan O(1) setelah penjumlahan. Total Θ(n²) waktu dan O(1) ruang tambahan bila hanya jumlah empat baris/kolom pinggir yang disimpan. Jika “submatriks” boleh memilih baris dan kolom tidak kontigu, definisinya perlu diperjelas; soal ini ditafsirkan kontigu.

## Contoh perlahan: apa yang dibuang binary search?

Cari 9 dalam larik terurut *[1, 3, 5, 7, 9, 11, 13]*. Indeks dimulai dari 0 dan rentang kandidat ditulis `[lo, hi)`, artinya *lo* termasuk dan *hi* tidak termasuk. Mula-mula `[0,7)` berarti indeks 0 sampai 6.

| Langkah | Rentang kandidat | mid | A[mid] | Keputusan |
| ---: | --- | ---: | ---: | --- |
| 1 | `[0,7)` | 3 | 7 | 7 < 9, buang indeks 0..3; menjadi `[4,7)` |
| 2 | `[4,7)` | 5 | 11 | 11 > 9, buang indeks 5..6; menjadi `[4,5)` |
| 3 | `[4,5)` | 4 | 9 | Sama; target ditemukan di indeks 4 |

Mengapa langkah pertama boleh membuang **semua** indeks 0..3? Karena larik terurut naik: setiap elemen di kiri atau sama dengan indeks 3 bernilai paling besar 7, jadi tidak mungkin 9. Tanpa sifat terurut, satu perbandingan di indeks tengah tidak memberi informasi tentang elemen lain. Invariant-nya: selama target ada, ia masih berada di rentang kandidat. Tiap keputusan mempertahankan invariant sekaligus mengecilkan rentang, sehingga proses berhenti.

Jika yang diminta adalah **kemunculan pertama** pada [5,5,5,5], berhenti pada nilai sama tidak cukup: indeks tengah bisa 2 padahal indeks 0 juga cocok. Gunakan pencarian batas bawah: ketika nilai tengah ≥ target, pertahankan bagian kiri dengan *hi = mid*. Dengan begitu indeks yang mungkin lebih awal tidak dibuang. Setelah *lo = hi*, periksa bahwa indeks masih di dalam larik dan nilainya benar-benar sama dengan target.

### Pemangkatan modulo tanpa lompatan

Untuk *3¹³ mod 7*, simpan hasil 1, basis 3, sisa eksponen 13. Karena 13 ganjil, kalikan hasil dengan basis: hasil 3. Kuadratkan basis: 3² mod 7 = 2; bagi sisa menjadi 6. Saat 6 genap, hasil tetap 3; basis menjadi 2² mod 7 = 4; sisa menjadi 3. Saat 3 ganjil, hasil menjadi 3·4 mod 7 = 5; basis menjadi 4² mod 7 = 2; sisa menjadi 1. Saat 1 ganjil, hasil menjadi 5·2 mod 7 = 3; sisa menjadi 0. Jadi jawabannya 3. Pada setiap baris, *hasil·basis^sisa* tetap setara dengan *3¹³* modulo 7; itulah alasan langkah kuadrat dan pembagian dua aman.

## Latihan bertingkat

1. **Mudah.** Linear search pada 10 elemen tidak terurut: berapa perbandingan terburuk jika target tidak ada?
2. **Mudah.** Mengapa binary search salah pada [2, 9, 1, 8] meskipun dapat mengakses indeks tengah?
3. **Mudah.** Berapa langkah pembagian dua untuk menyusutkan 64 kandidat menjadi paling banyak 1?
4. **Sedang.** Jalankan binary search pada [1,3,5,7,9,11,13] untuk target 9; tulis indeks tengah yang diperiksa dengan rentang `[lo,hi)`.
5. **Sedang.** Pada [5,5,5,5], apa hasil lower bound untuk target 5 dan target 8?
6. **Sedang.** Ada 1.000 elemen belum terurut dan hanya satu pencarian. Bandingkan biaya kasar mengurutkan lalu binary search dengan linear search.
7. **Sedang — Adaptasi responsi 6.** Matriks 3 × 4 terurut penuh. Jelaskan pemetaan indeks datar *p = 9* ke indeks baris dan kolom mulai 0.
8. **Sulit — Adaptasi responsi 6.** Diberi syarat hanya A[i][n−1] ≤ A[i+1][0], tanpa jaminan tiap baris terurut. Apakah binary search virtual benar? Berikan contoh penyangkal.
9. **Sulit — Adaptasi responsi 6.** Hitung *3¹³ mod 7* dengan repeated squaring dan banyak putaran *sisa* sampai nol.
10. **Sulit.** Buktikan invariant `hasil·basis^sisa ≡ aⁿ (mod m)` untuk langkah saat *sisa* ganjil dan genap.
11. **Sulit — Adaptasi responsi 6.** Matriks 3 × 3 memiliki baris [1,2,3], [4,5,6], [7,8,9]. Berapa jumlah maksimum submatriks kontigu 2 × 2? Tunjukkan empat kandidat.
12. **Sulit.** Jika ada *q* pencarian pada larik statis belum terurut, bandingkan O(qn) dengan O(n log n + q log n); kapan pengurutan awal masuk akal secara orde, dan faktor apa yang masih perlu diperhatikan?

### Jawaban dan alasan singkat

1. **10** perbandingan.
2. Urutan tidak terjaga; dari perbandingan dengan elemen tengah kita tidak tahu sisi mana yang aman dibuang.
3. **6** pembagian karena 64/2⁶ = 1; jumlah putaran pencarian bisa berbeda satu menurut kapan berhenti.
4. Awal *mid = 3* (nilai 7), lanjut `[4,7)` dengan *mid = 5* (nilai 11), lanjut `[4,5)` dengan *mid = 4* (nilai 9). Indeks tengah: **3, 5, 4**.
5. Target 5 memberi indeks **0**. Target 8 memberi insertion point **4**; karena di luar larik, target tidak ditemukan.
6. Linear search O(n) tanpa persiapan. Mengurutkan O(n log n) lalu O(log n) pencarian, biasanya lebih mahal untuk satu pencarian saja.
7. *p = 9*: baris ⌊9/4⌋ = **2**, kolom 9 mod 4 = **1**.
8. Tidak. Contoh [[9,1],[10,2]] memenuhi 1 ≤ 10 tetapi baris pertama dan kedua tidak terurut; urutan datar [9,1,10,2] merusak dasar binary search.
9. Hasil **3**; *sisa*: 13 → 6 → 3 → 1 → 0, jadi **4** putaran.
10. Jika genap *s = 2t*, setelah basis dikuadratkan dan sisa jadi *t*, `hasil·(basis²)^t = hasil·basis^s`. Jika ganjil *s = 2t+1*, hasil dikalikan basis lalu basis dikuadratkan: `(hasil·basis)(basis²)^t = hasil·basis^s`. Semua kesetaraan modulo *m*.
11. Kandidat kiri atas 12, kanan atas 16, kiri bawah 24, kanan bawah **28**. Maksimum 28.
12. Secara orde, pengurutan awal menarik bila *q* cukup besar dibanding log n: *qn* versus *n log n + q log n*. Konstanta, biaya pembaruan data, ruang, dan apakah pencarian perlu mempertahankan urutan asli tetap penting.

### Pembahasan lebih lengkap: latihan 9 dan 11

**Latihan 9 — repeated squaring.** Catat keadaan *(hasil, basis, sisa)* setelah tiap putaran, selalu modulo 7. Awalnya *(1,3,13)*. Karena 13 ganjil, hasil menjadi 3; basis menjadi 3² mod 7 = 2; sisa 6, jadi *(3,2,6)*. Karena 6 genap, hasil tetap 3; basis menjadi 4; sisa 3, jadi *(3,4,3)*. Karena 3 ganjil, hasil menjadi 3·4 mod 7 = 5; basis menjadi 4² mod 7 = 2; sisa 1, jadi *(5,2,1)*. Karena 1 ganjil, hasil menjadi 5·2 mod 7 = 3; sisa 0. Ada empat putaran dan hasilnya 3.

**Latihan 11 — empat jendela.** Pada matriks tiga kali tiga, jendela 2×2 hanya bisa berawal di (baris 0 atau 1, kolom 0 atau 1). Kiri atas berisi 1+2+4+5 = 12. Kanan atas 2+3+5+6 = 16. Kiri bawah 4+5+7+8 = 24. Kanan bawah 5+6+8+9 = 28. Bandingkan keempat jumlah itu: maksimum 28. Empat kandidat muncul karena untuk tiap dimensi hanya ada *3−2+1 = 2* posisi awal.

**Sumber bab:** Kuliah 6; Lembar Kerja Responsi Pertemuan 6; Bank Soal K6 dalam ZIP yang diberikan.
