# Bab 5 — Algoritme Rekursif dan Teorema Master

> Setiap panggilan rekursif membuat submasalah. Untuk menganalisisnya, hitung **berapa submasalah**, **seberapa kecil**, dan **berapa kerja di luar panggilan**.

## 1. Dari algoritme ke relasi rekurensi

Sebuah prosedur rekursif perlu kasus dasar dan kemajuan menuju kasus dasar. Jika satu panggilan pada ukuran *n* membuat *a* panggilan ukuran sekitar *n/b* dan pekerjaan lain *f(n)*, bentuk umumnya T(n) = aT(n/b) + f(n), dengan T(1) = Θ(1). Dua panggilan berarti *a = 2*; membagi ke tiga bagian berarti *b = 3*. Jangan menyamakan *a* dan *b*.

Contoh binary search: hanya **satu** dari dua bagian yang diteruskan, sehingga T(n) = T(n/2) + Θ(1), bukan 2T(n/2) + Θ(1). Contoh merge sort: **dua** bagian diurutkan dan digabung dalam Θ(n), sehingga T(n) = 2T(n/2) + Θ(n).

Kasus dasar berpengaruh pada bentuk tepat tetapi biasanya tidak pada kelas asimtotik. Untuk kode nyata, pembulatan ukuran submasalah dan biaya alokasi juga perlu dihitung jika relevan.

## 2. Pohon rekurensi: lihat kerja per tingkat

Untuk T(n) = aT(n/b) + cnᵈ, pada kedalaman *i* ada *aⁱ* simpul; ukuran tiap simpul *n/bⁱ*. Jadi biaya nonrekursif tingkat *i* adalah:

*aⁱ · c(n/bⁱ)ᵈ = cnᵈ(a/bᵈ)ⁱ*.

Tinggi pohon sekitar logᵦ n. Jumlah daun sekitar *a^(logᵦ n) = n^(logᵦ a)*. Rasio *r = a/bᵈ* menunjukkan arah kerja:

- *r < 1*: kerja tingkat atas dominan; total Θ(nᵈ), bila *d* sesuai bentuk dan daun lebih kecil.
- *r = 1*: tiap tingkat sebanding; total Θ(nᵈ log n).
- *r > 1*: tingkat bawah/daun dominan; total Θ(n^(logᵦ a)).

Contoh responsi: T(n) = 2T(n/4) + n. Rasio *2/4 = 1/2*, jadi Θ(n). Untuk 3T(n/3) + n, rasio 1, jadi Θ(n log n). Untuk 4T(n/2) + n, rasio 2, jadi Θ(n²). Untuk 7T(n/8) + n, rasio 7/8, jadi Θ(n).

## 3. Substitusi dan pemeriksaan

“Substitusi” bisa berarti membuka relasi berulang atau menebak batas lalu membuktikannya dengan induksi. Contoh T(n) = T(n/2) + 1 untuk *n = 2ᵏ*: T(2ᵏ) = T(2ᵏ⁻¹) + 1 = … = T(1) + k = Θ(log n). Ini juga menjelaskan logaritma sebagai banyaknya pembagian hingga ukuran 1.

Untuk T(n) = T(n−1) + n, membuka relasi memberi n + (n−1) + … + 1 = Θ(n²). **Teorema Master standar tidak berlaku** karena ukuran submasalah adalah *n−1*, bukan *n/b* untuk konstanta *b > 1*.

## 4. Teorema Master standar: cara pakai yang aman

Untuk T(n) = aT(n/b) + f(n), dengan *a ≥ 1, b > 1*, biaya *f(n)* akhirnya taknegatif, dan asumsi teknis terpenuhi, hitung *p = logᵦ a* lalu bandingkan *f(n)* terhadap *nᵖ*.

1. Jika *f(n) = O(n^(p−ε))* untuk suatu ε > 0, maka T(n) = Θ(nᵖ).
2. Jika *f(n) = Θ(nᵖ logᵏ n)* untuk *k ≥ 0*, maka T(n) = Θ(nᵖ logᵏ⁺¹ n).
3. Jika *f(n) = Ω(n^(p+ε))* dan ada *c < 1* sehingga *a f(n/b) ≤ c f(n)* untuk *n* cukup besar, maka T(n) = Θ(f(n)).

Contoh T(n) = 2T(n/2) + n log n: *p = 1*, *f(n) = Θ(n log n)*, jadi kasus kedua dengan *k = 1*: **Θ(n log² n)**. Contoh T(n) = 9T(n/3) + n²: *p = 2*, *k = 0*: **Θ(n² log n)**. Contoh T(n) = 3T(n/3) + n^(3/2): *p = 1*, kasus ketiga dan regularitas berlaku karena 3(n/3)^(3/2) = n^(3/2)/√3: **Θ(n^(3/2))**.

**Jangan paksa Master:** pada latihan lama T(n) = 4T(n/3) − n, biaya tambahan negatif dan bukan model “jumlah langkah” nonnegatif. T(n) = 0,5T(n/2) + n/log n juga memiliki *a < 1*, sehingga berada di luar versi standar yang diajarkan di sini. Soal seperti ini butuh penjelasan model dan teknik lain; menempel label kasus Master standar tanpa memeriksa syarat tidak sah.

## 5. Contoh adaptasi responsi: tiga dan empat bagian

**TriMergeSort** membagi larik menjadi tiga sublarik, mengurutkan ketiganya, lalu menggabung dalam Θ(n) **jika** operasi merge tiga arah benar-benar linear. Relasinya T(n) = 3T(n/3) + Θ(n), maka Θ(n log n). Nama `MERGE3_IN_PLACE` pada lembar kerja tidak sendiri menjamin kerja linear atau ruang O(1); asumsi biaya merge harus diperiksa pada implementasi.

**QuadHistogram** membagi menjadi empat sublarik lalu menggabungkan empat vektor frekuensi panjang *K*. Relasinya, jika inisialisasi basis dan penggabungan masing-masing Θ(K), ialah T(n,K) = 4T(n/4,K) + Θ(K) untuk *n > 1*. Ada Θ(n) simpul pada pohon 4-ary, masing-masing dapat menyentuh Θ(K) elemen; total **Θ(nK)** untuk cara penulisan ini. Jika *K* dianggap konstanta, menjadi Θ(n). Algoritme iteratif satu histogram dapat bekerja Θ(n+K), sehingga bentuk rekursif yang membuat vektor baru di setiap panggilan punya biaya tambahan. Menyebut T(n) = 4T(n/4) + n tanpa membaca biaya `ADD4` akan keliru.

## 6. Ruang rekursi

Waktu menghitung semua panggilan; ruang stack menghitung kedalaman panggilan aktif. Binary search rekursif memerlukan stack O(log n), sementara versi iteratif O(1) ruang tambahan. Merge sort biasa memakai O(n) buffer gabung dan O(log n) stack; ruang total O(n). Quick sort dapat memakai stack O(n) pada partisi terburuk, atau O(log n) rata-rata dengan pembagian seimbang.

## Contoh perlahan: membaca satu pohon rekurensi

Selesaikan *T(n) = 2T(n/2) + n* dengan *T(1) = 1* dan *n* pangkat dua. Angka 2 berarti **dua panggilan anak**; pembagi 2 berarti **ukuran setiap anak setengah**; tambahan *n* berarti pekerjaan pada satu panggilan ukuran *n* di luar anaknya.

Ambil *n = 8* agar pohonnya terlihat.

| Kedalaman | Jumlah panggilan | Ukuran tiap panggilan | Kerja tambahan seluruh tingkat |
| ---: | ---: | ---: | ---: |
| 0 | 1 | 8 | 8 |
| 1 | 2 | 4 | 2·4 = 8 |
| 2 | 4 | 2 | 4·2 = 8 |
| 3 | 8 | 1 | 8·T(1) = 8 |

Totalnya 8 + 8 + 8 + 8 = 32. Untuk *n* umum, tingkat *i* berisi *2ⁱ* panggilan ukuran *n/2ⁱ*. Hasil kali keduanya *n*. Kedalaman daun memenuhi *n/2ᵏ = 1*, jadi *k = log₂ n*. Ada *k+1* tingkat jika akar dan daun dihitung. Dengan biaya dasar satu, *T(n) = n(log₂ n + 1) = Θ(n log n)*. Jika biaya dasar hanya diketahui Θ(1), rumus tepatnya bisa berubah, tetapi kelasnya tetap.

Sekarang ubah hanya jumlah anak menjadi satu: *T(n) = T(n/2) + 1*. Tiap tingkat hanya satu panggilan dan kerja tetap 1. Dengan *n = 8*, urutannya ukuran 8 → 4 → 2 → 1, sehingga total 4. Untuk *n* umum, Θ(log n). Satu anak versus dua anak adalah alasan binary search dan merge sort memiliki biaya berbeda meskipun sama-sama membelah ukuran.

### Mengapa tidak langsung memakai Teorema Master?

Pertama tulis *a*, *b*, dan *f(n)* dari prosesnya. Periksa apakah *b > 1*, *a ≥ 1*, pekerjaan *f(n)* taknegatif, dan submasalah benar-benar berukuran *n/b* (pembulatan kecil boleh). *T(n−1)+n* tidak memenuhi bentuk itu karena pengurangannya tetap satu, bukan pembagian dengan konstanta. Bila syarat tidak terpenuhi, buka beberapa tingkat atau gunakan induksi; jangan memilih salah satu dari tiga kasus Master hanya karena ada huruf T pada soal.

## Latihan bertingkat

1. **Mudah.** Tulis relasi T(n) untuk binary search rekursif dan jelaskan nilai *a,b,f(n)*.
2. **Mudah.** Berapa tinggi pohon untuk pembagian ukuran *n* dengan 2 sampai 1?
3. **Mudah.** Selesaikan T(n) = T(n/2) + 1 untuk *n* pangkat dua.
4. **Sedang — Adaptasi responsi 5.** Selesaikan T(n) = 2T(n/4) + n dengan kerja per tingkat.
5. **Sedang — Adaptasi responsi 5.** Selesaikan T(n) = 3T(n/3) + n.
6. **Sedang — Adaptasi responsi 5.** Selesaikan T(n) = 4T(n/2) + n.
7. **Sedang — Adaptasi responsi 5.** Tentukan kasus Master untuk T(n) = 9T(n/3) + n².
8. **Sulit — Adaptasi responsi 5.** Tentukan T(n) untuk TriMergeSort dengan merge linear dan kelasnya.
9. **Sulit — Adaptasi responsi 5.** Jelaskan biaya QuadHistogram jika *K* adalah jumlah kemungkinan nilai dan vektor panjang *K* dibuat pada setiap daun serta digabung di setiap simpul.
10. **Sulit — Adaptasi responsi 5.** Selesaikan T(n) = 2T(n/2) + n log₂ n.
11. **Sulit — Adaptasi UTS 2018.** Selesaikan T(n) = 3T(n/3) + cn² dengan pohon, untuk *c > 0*.
12. **Sulit.** Mengapa T(n) = T(n−1) + n dan T(n) = 4T(n/3) − n tidak boleh langsung diselesaikan dengan Master standar yang baru dipelajari?

### Jawaban dan alasan singkat

1. T(n) = T(n/2) + Θ(1); *a=1, b=2*, karena hanya satu sisi dicari.
2. Sekitar log₂ n tingkat pembagian; termasuk akar dan daun ada ⌊log₂ n⌋+1 tingkat bila *n* pangkat dua.
3. T(n) = T(1) + log₂ n = Θ(log n).
4. Biaya tingkat *i* ialah n(1/2)ⁱ; deret menurun, total Θ(n).
5. Tiap tingkat biaya n, ada Θ(log n) tingkat: Θ(n log n).
6. Biaya tingkat *i* ialah n·2ⁱ; daun mendominasi: Θ(n²).
7. *p = log₃9 = 2* dan *f(n) = n²*, jadi kasus 2: Θ(n² log n).
8. T(n) = 3T(n/3) + Θ(n) = Θ(n log n), dengan asumsi merge benar-benar Θ(n).
9. Ada Θ(n) simpul termasuk daun; Θ(K) kerja per simpul memberi Θ(nK). Jika implementasi berbagi/mengubah satu histogram, relasinya berbeda.
10. Kasus 2 dengan *p = 1, k = 1*: Θ(n log² n).
11. Biaya tingkat *i* = cn²/3ⁱ, jumlahnya Θ(n²); daun Θ(n), sehingga total Θ(n²).
12. Relasi pertama mengecil dengan *n−1*, bukan *n/b*. Relasi kedua memiliki *f(n) = −n*, bertentangan dengan biaya nonnegatif pada teorema standar; model biaya perlu diklarifikasi.

### Pembahasan lebih lengkap: latihan 4 dan 10

**Latihan 4 — kerja mengecil tiap tingkat.** Untuk *T(n)=2T(n/4)+n*, akar berbiaya *n*. Tingkat berikutnya mempunyai dua anak ukuran *n/4*, sehingga total kerja tambahan *2(n/4)=n/2*. Tingkat setelah itu empat anak ukuran *n/16*, total *4(n/16)=n/4*. Jumlah kerja bagian dalam adalah *n + n/2 + n/4 + ··· < 2n*. Akar sendiri sudah memerlukan *n*, sehingga batas bawahnya Ω(n); batas atasnya O(n). Dengan biaya dasar tetap per daun, daun berjumlah *n^(log₄2)=√n*, lebih kecil daripada *n*. Jadi T(n)=Θ(n).

**Latihan 10 — satu faktor log tambahan.** Untuk *T(n)=2T(n/2)+n log₂n*, anggap *n=2ᵐ*. Pada kedalaman *i*, ada *2ⁱ* simpul ukuran *n/2ⁱ*. Tiap simpul berbiaya *(n/2ⁱ)·log₂(n/2ⁱ)*. Kalikan dengan jumlah simpul: biaya tingkat *i* adalah *n(m−i)*. Jumlahkan untuk *i=0..m−1*: *n[m+(m−1)+···+1] = n·m(m+1)/2*. Daun menambah Θ(n). Karena *m=log₂n*, hasil akhirnya Θ(n log²n). Faktor log kedua datang dari penjumlahan biaya yang menurun secara aritmetika antar tingkat.

**Sumber bab:** Kuliah 5; Lembar Kerja Responsi Pertemuan 5; Bank Soal K5; UTS 2018 dan pembahasan UTS 2020–2021 dalam ZIP yang diberikan.
