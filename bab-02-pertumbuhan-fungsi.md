# Bab 2 — Pertumbuhan Fungsi dan Notasi Asimtotik

> Ide utama: waktu yang terukur pada satu komputer bukan sifat murni algoritme. Kita membandingkan bagaimana jumlah pekerjaan bertambah saat input membesar.

## 1. Dari program ke fungsi biaya

Tentukan dahulu **ukuran input** dan **operasi dasar**. Pada linear search, *n* adalah banyak elemen dan operasi dasarnya perbandingan dengan target. Pada perkalian matriks *A[n × m]* dan *B[m × p]*, jumlah perkalian skalar pada algoritme biasa adalah *nmp*. Sebuah algoritme graf lebih tepat dinyatakan dalam *V* dan *E* daripada dipaksa menjadi satu *n*.

Misal satu operasi memakan waktu *a* dan ada biaya persiapan *b*. Untuk loop *n* kali, T(n) = an + b. Kita menyebutnya Θ(n), tetapi ini tidak berarti semua program Θ(n) sama cepat untuk *n* yang dipakai hari ini. Konstanta, memori, perangkat, dan ambang perpotongan tetap berarti secara praktis.

**Mengapa memakai pertumbuhan?** Pada *n* sangat besar, suku dominan menentukan arah. Untuk *T(n) = 4n² + 100n + 7*, pembagian dengan *n²* memberi 4 + 100/n + 7/n² → 4. Jadi seluruh fungsi tumbuh seorde *n²*.

## 2. O, Ω, dan Θ tanpa menebak

Untuk fungsi taknegatif sesudah suatu *n₀*:

- *f(n) ∈ O(g(n))* jika ada konstanta *c > 0* dan *n₀* sehingga *f(n) ≤ c g(n)* untuk semua *n ≥ n₀*. Ini **batas atas**.
- *f(n) ∈ Ω(g(n))* jika ada *c > 0, n₀* sehingga *f(n) ≥ c g(n)* untuk semua *n ≥ n₀*. Ini **batas bawah**.
- *f(n) ∈ Θ(g(n))* jika keduanya berlaku. Ini **batas ketat**.

Contoh: *f(n) = 3n² + 5n + 2*. Untuk *n ≥ 1*, *n ≤ n²* dan *1 ≤ n²*, sehingga *f(n) ≤ (3+5+2)n² = 10n²*. Juga *f(n) ≥ 3n²*. Maka *f(n) ∈ Θ(n²)*. Konstanta 10 dan 3 tidak harus terbaik; cukup ada.

**Jebakan bahasa:** Pernyataan “f adalah O(n³)” juga benar untuk fungsi Θ(n²), karena O hanya batas atas. Jika ditanya kelas yang *paling ketat* dari pilihan umum, pilih Θ(n²), bukan batas atas longgar. Satu pengukuran waktu tidak membuktikan kelas asimtotik.

## 3. Urutan pertumbuhan

Untuk *n* cukup besar, urutan umum adalah 1 ≺ log n ≺ n ≺ n log n ≺ n² ≺ n³ ≺ 2ⁿ ≺ n!. Simbol ≺ di sini berarti fungsi sebelah kiri tumbuh lebih lambat secara asimtotik. Dasar logaritma positif selain 1 hanya mengubah konstanta: logₐ n = logᵦ n / logᵦ a.

Mengapa *n log n* lebih besar dari *n*? Rasionya log n, yang terus bertambah. Mengapa *n²* lebih besar dari *n log n*? Rasionya n/log n → ∞. Mengapa eksponensial melampaui polinomial? Mengalikan *n* dengan konstanta pada pangkat polinomial jauh lebih lambat dibanding penggandaan faktor 2 tiap kenaikan eksponen.

## 4. Aturan operasi pada biaya

Jika dua tahap **berurutan**, jumlahkan: T(n) = T₁(n) + T₂(n), dan suku yang dominan menentukan Θ bila tidak terjadi pembatalan. Jika loop **bersarang independen**, kalikan banyak iterasinya. Namun jika batas loop dalam bergantung pada indeks luar, jumlahkan biaya per nilai indeks: Σᵢ Tᵢ. Contoh *j = 1..i* di dalam *i = 1..n* menghasilkan Σᵢ₌₁ⁿ i = n(n+1)/2 = Θ(n²), bukan sekadar “dua loop berarti n²” tanpa alasan.

Jika loop menggandakan *i*: 1, 2, 4, …, 2ᵏ ≤ n, jumlah iterasi ⌊log₂ n⌋ + 1. Jika tiap iterasi mengerjakan *n* langkah, total Θ(n log n).

## 5. Big-O dan pilihan nyata

Perbandingan dari responsi: T_A(n) = 0,1n log₂ n mikrodetik dan T_B(n) = 5n mikrodetik. Untuk *n > 0*, A lebih cepat jika 0,1 log₂ n < 5, yaitu log₂ n < 50 atau *n < 2⁵⁰*. Pada *n = 10¹²*, log₂ n ≈ 39,86, jadi A ≈ 3,986n mikrodetik dan B = 5n mikrodetik: **A lebih cepat pada ukuran itu**, walaupun secara asimtotik B = Θ(n) lebih baik daripada A = Θ(n log n). Titik potong menunjukkan mengapa analisis dan kebutuhan nyata sama-sama penting.

Contoh lain: T_A(n) = 0,001n milidetik dan T_B(n) = 500√n milidetik. Samakan: 0,001n = 500√n ⇒ √n = 500.000 ⇒ *n = 2,5 × 10¹¹*. Untuk *n = 10⁹*, A = 10⁶ ms dan B ≈ 15,81 × 10⁶ ms, jadi A lebih cepat. Untuk input amat besar melewati titik potong, B unggul secara asimtotik.

## 6. Analisis penggandaan ukuran

Jika sebuah algoritme memakan 1 detik pada *n = 8*, pendekatan kasar saat *n = 16* adalah rasio *f(16)/f(8)*, **dengan asumsi** suku dominan sudah cukup mewakili biaya. Untuk Θ(n²), rasio 4; untuk Θ(n³), rasio 8. Untuk Θ(2ⁿ), rasio 2⁸ = 256. Untuk Θ(log₂ n), rasio log₂16/log₂8 = 4/3. Rasio ini bukan jaminan waktu tepat karena konstanta dan biaya tambahan bisa berpengaruh.

### Contoh lengkap: dari hitungan ke batas formal

Misalkan algoritme melakukan *n* perbandingan pada tahap pertama, lalu untuk setiap *i = 1..n* melakukan *i* perbandingan pada tahap kedua. Fungsi biayanya *T(n) = n + Σᵢ₌₁ⁿ i = n + n(n+1)/2 = (n²+3n)/2*. Untuk *n ≥ 1*, batas bawah *T(n) ≥ n²/2*. Karena *n ≤ n²*, batas atas *T(n) ≤ (n²+3n²)/2 = 2n²*. Kedua batas menyatakan *T(n) ∈ Θ(n²)*. Langkah ini lebih kuat daripada sekadar melihat ada loop bersarang: fungsi eksak mengungkap bahwa loop dalam panjangnya berubah.

### Mengapa konstanta tidak dibuang saat memilih sistem?

Notasi Θ mengabaikan konstanta untuk menjelaskan kecenderungan saat *n* membesar, tetapi keputusan penggunaan terjadi pada rentang *n* tertentu. Algoritme *100n* dan *n²* berpotongan pada *n = 100*: untuk *n = 10*, *n²* lebih kecil; untuk *n = 1000*, *100n* lebih kecil. Selain itu, waktu yang benar-benar terukur bisa dipengaruhi cache, bahasa pemrograman, dan biaya masukan/keluaran. Gunakan Θ untuk memahami skala, lalu gunakan batas ukuran dan pengukuran yang relevan untuk memilih implementasi.

## 7. Strategi menyelesaikan soal

Tulis *n* dan operasi dasar, turunkan T(n), sederhanakan suku dominan, lalu beri O/Ω/Θ sesuai pertanyaan. Jika soal meminta membandingkan dua paket pada rentang input tertentu, hitung juga nilai atau titik potongnya; jangan hanya melihat kelas asimtotik.

## Contoh perlahan: dari jumlah operasi ke Θ

Bayangkan tahap pertama memeriksa *n* elemen sekali. Tahap kedua menjalankan *i* perbandingan untuk setiap *i = 1, 2, …, n*. Operasi dasar kita ialah **satu perbandingan**.

1. Tahap pertama berbiaya *n*. Tahap kedua untuk *n = 4* berbiaya *1 + 2 + 3 + 4 = 10*. Jadi seluruhnya 14, bukan *4 + 4·4*.
2. Untuk *n* umum, tulis *T(n) = n + Σᵢ₌₁ⁿ i*. Sigma berarti kita menjumlah panjang loop dalam pada **setiap** nilai *i*.
3. Pasangkan ujung deret: *(1+n), (2+(n−1)), …*. Hasilnya *Σᵢ₌₁ⁿ i = n(n+1)/2*. Maka *T(n) = (n²+3n)/2*.
4. Batas bawah untuk *n ≥ 1*: *T(n) ≥ n²/2*. Batas atas: karena *n ≤ n²*, *3n ≤ 3n²*, sehingga *T(n) ≤ 2n²*.
5. Jadi ada dua konstanta, *1/2* dan *2*, yang mengapit *T(n)* dengan kelipatan *n²*. Inilah alasan *T(n) ∈ Θ(n²)*. Notasi Θ berasal dari **dua ketaksamaan**, bukan dari membuang suku secara ajaib.

Untuk membedakan O dari Θ, perhatikan *n ∈ O(n²)* juga benar saat *n ≥ 1*, sebab *n ≤ n²*. Akan tetapi *n ∉ Θ(n²)*: tidak ada konstanta positif *c* yang membuat *n ≥ cn²* untuk semua *n* besar, karena itu menuntut *1 ≥ cn* selamanya. Jadi jawaban O(n²) bisa benar tetapi kurang tajam.

### Membaca titik potong tanpa menebak

Bandingkan *A(n) = 100n* dan *B(n) = n²* untuk *n > 0*. Cari ukuran ketika sama: *100n = n²*. Bagi dengan *n* karena kita sudah menyatakan *n > 0*, sehingga *n = 100*. Uji satu nilai di kiri, misalnya *n = 10*: A = 1000, B = 100, jadi B lebih murah. Uji satu nilai di kanan, *n = 1000*: A = 100.000, B = 1.000.000, jadi A lebih murah. Kita perlu kedua uji itu sebab persamaan titik potong sendiri belum memberi arah ketaksamaan. Satuan biaya kedua fungsi harus sama agar perbandingannya bermakna.

## Latihan bertingkat

1. **Mudah.** Sederhanakan *T(n) = 7n + 90* ke kelas Θ paling ketat.
2. **Mudah.** Tentukan Θ untuk *5n³ + 100n + 20* dan jelaskan suku dominannya.
3. **Mudah.** Urutkan *log n, n², 2ⁿ, n log n, n* menurut pertumbuhan.
4. **Mudah.** Buktikan *6n + 12 ∈ O(n)* dengan *c* dan *n₀* tertentu.
5. **Sedang — Adaptasi responsi 2.** Bandingkan T_A = 0,1n log₂ n dan T_B = 5n pada *n = 2⁴⁰* dan *n = 2⁶⁰*. Cari titik potong.
6. **Sedang.** Ada dua loop berurutan: pertama *n²* operasi, kedua *20n* operasi. Berikan T(n) dan Θ.
7. **Sedang — Adaptasi responsi 2.** Loop luar membagi *i* dari *n* dengan 2 sampai 0; loop dalam menambah *j* dari 1 dengan faktor 2 sampai ≥ *n*; loop terdalam berjalan *n/2* kali. Berikan Θ untuk *n ≥ 2*.
8. **Sedang.** Jika T(8) = 1 detik dan pekerjaan dominan Θ(n³), perkirakan T(32), beserta syarat perkiraan.
9. **Sulit — Adaptasi responsi 2.** T_A = 0,001n ms, T_B = 500√n ms. Cari titik potong positif dan pilihan pada *n = 10⁹*.
10. **Sulit — Adaptasi UTS 2018.** Bandingkan *f_A(n) = 2n² + 975n + 90* dan *f_B(n) = n² + 75n + 90*. Adakah *n > 0* sehingga B lebih lambat daripada A?
11. **Sulit.** Buktikan *n log₂ n ∈ O(n²)* untuk *n ≥ 2* tanpa memakai limit.
12. **Sulit.** Jelaskan mengapa waktu 1 detik pada *n = 100* tidak cukup untuk menyimpulkan Θ(n), sekalipun grafik kecil tampak lurus.

### Jawaban dan alasan singkat

1. Θ(n), karena konstanta 90 menjadi relatif kecil saat *n* tumbuh.
2. Θ(n³); rasio suku lain terhadap *n³* menuju nol.
3. log n ≺ n ≺ n log n ≺ n² ≺ 2ⁿ.
4. Untuk *n ≥ 1*, 6n + 12 ≤ 18n; ambil *c = 18, n₀ = 1*.
5. Saat 2⁴⁰, A = 4n < 5n; saat 2⁶⁰, A = 6n > 5n. Sama pada *n = 2⁵⁰*.
6. T(n) = n² + 20n, jadi Θ(n²). Tahap berurutan dijumlah.
7. Θ(n log² n). Dua loop pertama masing-masing Θ(log n), yang terdalam Θ(n). Batas yang tepat dapat mengubah konstanta, tidak kelas.
8. Faktor ukuran 4 memberi faktor 4³ = 64, jadi sekitar **64 detik**, hanya bila model kubik dominan dan kondisi mesin sama.
9. *n = 2,5 × 10¹¹*. Pada 10⁹, A = 10⁶ ms dan B ≈ 1,581 × 10⁷ ms; A lebih cepat.
10. Tidak. *f_B − f_A = −n² − 900n < 0* untuk *n > 0*. Keduanya Θ(n²), tetapi konstanta dan suku linear tetap menentukan urutan ini.
11. Untuk *n ≥ 2*, log₂ n ≤ n, sehingga n log₂ n ≤ n²; ambil *c = 1, n₀ = 2*.
12. Banyak fungsi berpotongan pada satu titik; misalnya *n* dan *n²/100* sama pada *n = 100* tetapi kelas pertumbuhannya berbeda.

### Pembahasan lebih lengkap: latihan 5 dan 11

**Latihan 5 — dua waktu dengan satuan sama.** Tulis *A = 0,1n log₂n* dan *B = 5n*. Untuk *n = 2⁴⁰*, *log₂n = 40*, jadi *A = 4n* dan *B = 5n*: A lebih cepat. Untuk *n = 2⁶⁰*, *A = 6n*, sehingga B lebih cepat. Cari titik sama dengan *0,1n log₂n = 5n*. Karena *n > 0*, bagi kedua sisi dengan *n*: *0,1 log₂n = 5*, lalu *log₂n = 50*, jadi *n = 2⁵⁰*. Tanda perbandingan berubah setelah titik itu.

**Latihan 11 — bukti batas atas.** Kita ingin menunjukkan *n log₂n ≤ c n²* sejak suatu *n₀*. Untuk *n ≥ 2*, berlaku *log₂n ≤ n*; misalnya pertumbuhan pangkat dua melampaui pertumbuhan linear, dan ketaksamaan ini juga dapat dibuktikan dengan induksi untuk bilangan bulat. Kalikan kedua sisi dengan *n > 0*: *n log₂n ≤ n²*. Jadi pilih *c = 1* dan *n₀ = 2*. Ingat: ini hanya membuktikan O(n²); kelas ketat fungsi tersebut tetap Θ(n log n).

**Sumber bab:** Kuliah 2; Lembar Kerja Responsi Pertemuan 2; Bank Soal K2; UTS 2018 dalam ZIP yang diberikan.
