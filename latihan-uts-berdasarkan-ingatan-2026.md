# Latihan UTS Analisis Algoritme — berdasarkan ingatan ujian 2026

> Ini **soal latihan baru**, bukan rekonstruksi soal UTS yang persis. Sensei mengingat sekitar 30–40 soal, terutama loop bersarang dengan sigma, loop logaritmik, dua relasi rekursif, batas waktu komputer, dua titik potong fungsi biaya, serta pemilihan algoritme pencarian dan pengurutan. Angka dan kode yang tidak diingat dibuat khusus untuk latihan.

## Aturan yang dipakai

- Kecuali disebut lain, `n` bilangan bulat positif, `kerja()` berbiaya konstan, dan setiap loop memperbarui penghitung sesuai kode. Hitung frekuensi `kerja()`; jika diminta jumlah uji kondisi, sertakan uji terakhir yang gagal.
- `i *= 2` berarti `i = 2*i`. Pembagian bulat seperti `i /= 2` dibulatkan ke bawah. `log n` berarti logaritma basis 2 kecuali basis lain ditulis.
- Untuk relasi rekursif, anggap `T(1)=Θ(1)` dan, jika perlu, `n` pangkat dari pembagi agar tidak terganggu pembulatan.
- Pada soal waktu, satu operasi yang disebut = satu instruksi. Penyederhanaan ini penting: kelas Θ saja tidak cukup untuk memutuskan apakah batas 0,5 detik terpenuhi; konstanta dan jumlah instruksi harus diketahui.

## A. Loop, sigma, dan logaritma (1–12)

**1. Segitiga naik.** Tentukan frekuensi `kerja()` dan Θ waktunya.

```text
for (i = 1; i < n; i++)
    for (j = 0; j < i; j++) kerja();
```

**2. Segitiga turun.** Ganti loop dalam nomor 1 menjadi `for (j=i; j<n; j++) kerja();`. Hitung frekuensi tepatnya.

**3. Batas inklusif.** `i` berjalan dari 1 sampai `n`, dan `j` dari 1 sampai `i`, keduanya inklusif. Nyatakan jumlah kerja dengan sigma dan rumus tertutup.

**4. `while` bersarang.** Hitung kerja, pembaruan `j`, uji `j<i`, dan uji `i<n` untuk `n=5`. Kemudian berikan frekuensi kerja untuk `n` umum.

```text
i = 1;
while (i < n) {
    j = 0;
    while (j < i) {
        kerja();
        j = j + 1;
    }
    i = i + 1;
}
```

**5. Penghitung tidak diatur ulang.** Pindahkan `j=0` pada nomor 4 ke sebelum `while (i<n)`. Berapa kali `kerja()` untuk `n=5` dan `n` umum? Mengapa berbeda?

**6. Kuadrat per putaran.** Untuk tiap `i=1..n`, loop dalam berjalan dari `j=1` sampai `i*i`. Nyatakan frekuensi dan Θ dengan rumus `Σi²`.

**7. Batas logaritmik.** Untuk `n=16`, daftar nilai `i` dan frekuensi kerja; lanjutkan ke `n` umum.

```text
i = 1;
while (i < n) { kerja(); i = i * 2; }
```

**8. Loop dalam logaritmik.** `i=1..n`; untuk setiap `i`, `j` mulai 1 dan digandakan selama `j<=i`. Tuliskan sigma frekuensi dan Θ-nya. Cek nilai untuk `n=4`.

**9. Dua loop logaritmik.** `i` mulai 1 dan digandakan selama `i<=n`; setiap putaran, `j` mulai 1 dan digandakan selama `j<=n`. Hitung untuk `n=8`, lalu tulis Θ.

**10. Log dari batas yang berubah.** `i` mulai 1 dan digandakan selama `i<=n`; setiap putaran, `j` mulai 1 dan digandakan selama `j<=i`. Hitung untuk `n=8`, lalu tulis Θ. Bedakan dari nomor 9.

**11. Tiga loop, satu linear.** Tambahkan loop `k=0..n-1` berisi `kerja()` pada bagian terdalam nomor 10. Berapa frekuensi tepat untuk `n=8` dan Θ umum?

**12. Pembagian dua.** `i=n`; selama `i>0`, jalankan `kerja()` lalu `i=floor(i/2)`. Daftar nilai untuk `n=13`, frekuensi kerja dan uji, serta Θ.

## B. Relasi rekursif (13–17)

Tentukan Θ masing-masing. Tunjukkan biaya setiap tingkat atau gunakan Teorema Master dengan alasan singkat.

13. `T(n) = 2T(n/2) + n`.
14. `T(n) = 4T(n/4) + n²`.
15. `T(n) = 2T(n/2) + 1`.
16. `T(n) = T(n/2) + n`.
17. `T(n) = 3T(n/3) + n log₂ n`.

## C. Komputer dan batas waktu (18–21)

Komputer menjalankan **10⁷ instruksi/detik**. Batas waktu **0,5 detik** berarti anggaran tepat **5×10⁶ instruksi**. Untuk `n=10⁵`, tentukan apakah fungsi hitungan berikut memenuhi batas. Anggap `log` basis 2.

18. `I_A(n)=20n` dan `I_B(n)=50n`.
19. `I_C(n)=n⌈log₂ n⌉` dan `I_D(n)=4n⌈log₂ n⌉`.
20. `I_E(n)=n√n` dan `I_F(n)=n²/10⁴`.
21. Diketahui hanya algoritme G berkelas `Θ(n log n)` dan H berkelas `Θ(n)`. Tanpa konstanta atau hitungan instruksi, bisakah batas waktu dipastikan untuk `n=10⁵`? Jelaskan.

## D. Membandingkan dua algoritme (22–25)

Pada nomor 22–24, biaya adalah jumlah instruksi, `n` bilangan bulat positif, dan biaya lebih kecil berarti lebih cepat.

22. Algoritme A memerlukan `F_A(n)=n²−8n+30`; B memerlukan `F_B(n)=4n+3`. Cari semua titik potong dan rentang ketika masing-masing lebih cepat.
23. Hitung biaya A dan B nomor 22 untuk `n=2,3,6,9,10` sebagai pemeriksaan hasil.
24. Algoritme C memerlukan `n²+10`, D memerlukan `12n+10`. Tentukan titik potong dan pemenang untuk semua `n≥1`.
25. Jika hanya diberi `A=Θ(n²)` dan `B=Θ(n)`, apakah nilai `n` tepat ketika B mulai lebih cepat dapat ditentukan? Apa yang tetap bisa disimpulkan?

## E. Kasus pencarian (26–29)

26. Ada 100.000 nomor mahasiswa belum terurut dan hanya **satu** pencarian. Pilih linear search atau urutkan dahulu lalu binary search. Tulis perkiraan kelas waktu total dan syarat pilihan.
27. Ada 100.000 nomor mahasiswa **sudah terurut** dan 1.000 pencarian. Bandingkan linear search terburuk per pencarian dengan binary search.
28. Matriks berukuran `m×k` terurut menaik dalam tiap baris dan elemen terakhir suatu baris tidak lebih besar dari elemen pertama baris berikutnya. Pilih strategi pencarian dan Θ jumlah perbandingan.
29. Jika matriks nomor 28 hanya dijamin terurut **per baris**, bolehkah seluruh matriks dianggap satu array terurut untuk binary search? Berikan alasan dan satu strategi yang sah.

## F. Kasus pengurutan (30–32)

30. Satu juta transaksi perlu diurutkan menurut `(waktu, id_pengguna)`; transaksi dengan kedua kunci sama harus tetap mengikuti urutan semula. Pilih algoritme dan jelaskan waktu serta ruang tambahan untuk implementasi array standar.
31. Sepuluh juta skor masuk sebagai aliran. Simpan hanya 100 skor tertinggi, tanpa mengurutkan semua data. Pilih cara dan hitung waktu serta ruang dalam `N` dan `K=100`.
32. Array yang hampir terurut berisi 1.000 elemen; tiap elemen bergeser paling jauh beberapa posisi dari lokasi akhirnya. Bandingkan insertion sort dengan merge sort. Kapan insertion sort bisa lebih efisien, dan apa batas terburuknya?

---

# Kunci dan pembahasan

## A. Loop, sigma, dan logaritma

1. Untuk nilai `i`, loop dalam bekerja `i` kali. Jadi `Σ(i=1..n−1) i = n(n−1)/2 = Θ(n²)`. Nilai `i=1,2,3,4` saat `n=5` menghasilkan `1+2+3+4=10`.
2. Pada nilai `i`, `j=i..n−1` memberi `n−i` kerja. `Σ(i=1..n−1)(n−i) = n(n−1)/2 = Θ(n²)`.
3. `Σ(i=1..n) Σ(j=1..i) 1 = Σ(i=1..n)i = n(n+1)/2 = Θ(n²)`. Perbedaan batas inklusif mengubah hitungan tepat.
4. Saat `n=5`, nilai `i` ialah 1,2,3,4 dan frekuensi `kerja()` per baris ialah 1,2,3,4. Jumlah kerja dan pembaruan `j`: **10**. Uji `j<i`: `(1+1)+(2+1)+(3+1)+(4+1)=14`. Uji `i<n`: **5**, termasuk uji gagal saat `i=5`. Secara umum kerja `Σ(i=1..n−1)i=n(n−1)/2=Θ(n²)`; uji dalam `n(n−1)/2+(n−1)`.
5. `j` kini tetap bertambah di antara putaran luar. Untuk `n=5`, banyak kerja per `i` ialah 1,1,1,1; total **4**. Pada akhir putaran dengan `i=r`, nilai `j=r`, sehingga putaran berikutnya hanya menambah satu. Untuk `n` umum frekuensi `n−1=Θ(n)`, dengan asumsi `n≥1`.
6. `Σ(i=1..n)i²=n(n+1)(2n+1)/6=Θ(n³)`. Pekerjaan dalam bergantung pada `i`, jadi jangan mengalikan `n` dengan frekuensi putaran terakhir saja.
7. Untuk `n=16`, nilai `i` ialah 1,2,4,8: **4** kerja dan **5** uji. Umumnya `⌈log₂ n⌉` kerja untuk `n≥1`, sehingga Θ(log n) untuk `n≥2`.
8. Untuk `i≥1`, `j` bernilai `1,2,4,...` sampai `i`, sehingga frekuensinya `⌊log₂ i⌋+1`. Total `Σ(i=1..n)(⌊log₂ i⌋+1)=Θ(n log n)` untuk `n≥2`. Untuk `n=4`, jumlahnya `1+2+2+3=8`.
9. Untuk `n=8`, tiap loop memiliki nilai 1,2,4,8, jadi **4×4=16** kerja. Umumnya `(⌊log₂ n⌋+1)²=Θ((log n)²)` untuk `n≥2`.
10. Untuk `n=8`, frekuensi per `i=1,2,4,8` ialah 1,2,3,4; total **10**. Jika `n=2^m`, total `Σ(r=0..m)(r+1)=(m+1)(m+2)/2`. Umumnya tetap `Θ((log n)²)`, tetapi hitungan tepat berbeda dari nomor 9.
11. Pada `n=8`, masing-masing dari 10 putaran dalam nomor 10 memanggil `kerja()` delapan kali: **80**. Jika `n=2^m`, total `n(m+1)(m+2)/2 = Θ(n(log n)²)`.
12. Nilai sebelum pembagian: 13,6,3,1. Jadi **4** kerja, **5** uji, dan Θ(log n). Untuk `n≥1`, frekuensi tepat `⌊log₂ n⌋+1`.

**Cara menulis sigma ketika batas berubah:** tentukan dulu banyak putaran dalam sebagai fungsi `i`, lalu jumlahkan untuk seluruh nilai `i`. Pada nomor 4, jumlahnya `Σi`; pada nomor 8, `Σ(⌊log₂ i⌋+1)`; pada nomor 10, yang dijumlahkan ialah 1,2,3,... karena `i` sendiri mengganda. Banyaknya kata `while` tidak menentukan orde.

## B. Relasi rekursif

13. **Θ(n log n).** Pada tingkat ke-`d`, ada `2^d` submasalah berukuran `n/2^d`; total kerja nonrekursif tingkat itu `2^d×(n/2^d)=n`. Ada `log₂ n` tingkat sebelum daun, lalu Θ(n) daun.
14. **Θ(n²).** Tingkat ke-`d` berbiaya `4^d(n/4^d)²=n²/4^d`. Jumlah geometrinya didominasi akar: `n²(1+1/4+...) = Θ(n²)`. Daun berjumlah `n`, lebih kecil dari `n²`.
15. **Θ(n).** Pohon biner mempunyai `n` daun dan `n−1` simpul internal bila `n` pangkat dua. Jika kerja tetap tiap simpul, jumlah simpul `2n−1`.
16. **Θ(n).** Hanya satu submasalah per tingkat; biayanya `n+n/2+n/4+... < 2n` dan sedikitnya `n`.
17. **Θ(n(log n)²).** Di tingkat `d`, kerja total `n log₂(n/3^d)`. Ada Θ(log n) tingkat, dengan nilai logaritma menurun secara aritmetis; jumlahnya Θ(n(log n)²). Dalam Teorema Master, `n^{log₃3}=n` dan faktor tambahan `log n` menaikkan pangkat log hasil menjadi 2.

## C. Komputer dan batas waktu

18. `I_A=2.000.000` → **0,2 detik, memenuhi**. `I_B=5.000.000` → **0,5 detik, tepat memenuhi**.
19. `⌈log₂ 100.000⌉=17`. `I_C=1.700.000` → **0,17 detik, memenuhi**. `I_D=6.800.000` → **0,68 detik, tidak memenuhi**. Dua fungsi sama-sama Θ(n log n), tetapi konstanta berbeda.
20. `I_E=100.000√100.000≈31.622.777` → sekitar **3,162 detik, tidak memenuhi**. `I_F=(100.000)²/10.000=1.000.000` → **0,1 detik, memenuhi**. Pada input ini, fungsi kuadratik dengan konstanta kecil justru lebih cepat daripada fungsi `n√n` tersebut.
21. **Tidak bisa dipastikan.** Θ menghilangkan konstanta. Misalnya `n log₂ n` sekitar 1,66 juta, tetapi `4n log₂ n` sekitar 6,64 juta; yang pertama memenuhi, yang kedua tidak. Hal serupa berlaku untuk `n` dan `100n`.

## D. Membandingkan dua algoritme

22. Kurangkan: `F_A−F_B=n²−12n+27=(n−3)(n−9)`. Titik potong **n=3 dan n=9**. Untuk bilangan bulat positif, B lebih cepat pada **1–2** dan **n≥10**; A lebih cepat pada **4–8**; keduanya sama pada **3 dan 9**. Di antara akar, hasil kali dua faktor negatif; di luar akar, hasil kali positif.
23. Tabel pemeriksaan:

   | n | A | B | Lebih cepat |
   | ---: | ---: | ---: | --- |
   | 2 | 18 | 11 | B |
   | 3 | 15 | 15 | Sama |
   | 6 | 18 | 27 | A |
   | 9 | 39 | 39 | Sama |
   | 10 | 50 | 43 | B |

24. `C−D=n²−12n=n(n−12)`. Untuk `n≥1`, titik potong yang relevan **n=12**; `n=0` berada di luar domain. C lebih cepat untuk **1≤n≤11**, sama pada 12, D lebih cepat untuk **n≥13**.
25. **Tidak.** Konstanta dan suku orde rendah diperlukan untuk mencari ambang tepat. Yang dapat disimpulkan ialah B pada akhirnya lebih cepat untuk `n` cukup besar, karena pertumbuhan linear lebih lambat daripada kuadratik; titik mulainya belum diketahui.

## E. Kasus pencarian

26. **Linear search** untuk satu pencarian pada data yang belum terurut: terburuk Θ(n), tanpa biaya persiapan. Mengurutkan dahulu dengan algoritme perbandingan umum memerlukan Θ(n log n), baru kemudian Θ(log n). Syaratnya data memang belum punya indeks atau struktur lain yang sudah tersedia.
27. **Binary search** pada data yang sudah terurut: paling banyak sekitar `⌈log₂(100.001)⌉=17` pemeriksaan per pencarian, jadi sekitar **17.000** untuk 1.000 pencarian; linear search terburuk **100.000.000** pemeriksaan. Kedua angka perbandingan ini adalah batas kasar, bukan waktu mesin terukur.
28. Karena urutan setiap baris *dan* batas antarbaris dijamin, matriks bisa dilihat sebagai array virtual panjang `mk`. Gunakan **binary search**, Θ(log(mk)) perbandingan dan Θ(1) ruang tambahan dengan indeks baris/kolom yang dihitung.
29. **Tidak.** Baris `[1,100]` dan `[2,3]` masing-masing terurut, tetapi urutan datar `[1,100,2,3]` tidak. Salah satu strategi sah ialah binary search pada tiap baris: `O(m log k)` perbandingan terburuk. Jika batas nilai tiap baris diketahui, beberapa baris bisa dilewati, tetapi analisisnya perlu syarat tambahan.

## F. Kasus pengurutan

30. **Merge sort stabil** dengan pembanding pasangan `(waktu,id_pengguna)` dan saat sama memilih elemen kiri lebih dulu. Waktu Θ(N log N), buffer tambahan Θ(N) untuk array standar. Stabilitas harus dipastikan pada implementasi, bukan hanya pada nama algoritmenya.
31. Pertahankan **min-heap berukuran K=100**. Bandingkan skor baru dengan akar; jika lebih besar, ganti akar dan pulihkan heap. Waktu `O(N log K)`, ruang `O(K)`; untuk K tetap 100, waktu terhadap N adalah Θ(N) bila setiap skor setidaknya diperiksa sekali. Jika keluaran akhir harus terurut, tambahkan `O(K log K)`.
32. **Insertion sort** dapat efektif bila perpindahan yang dibutuhkan sedikit: waktunya Θ(n+I), dengan `I` jumlah inversi; jika tiap elemen paling jauh `d` posisi, `I=O(nd)`, jadi untuk `d` kecil mendekati linear. Merge sort selalu Θ(n log n) untuk implementasi standar. Namun insertion sort tetap memiliki terburuk Θ(n²) pada input umum; bila jaminan “hampir terurut” tidak pasti, merge sort memberi batas terburuk yang lebih kuat.

## Cara memakai latihan

Kerjakan nomor 1, 4, 8, 10, 13, 14, 19, 22, 27, dan 30 dulu. Untuk setiap loop, tulis nilai penghitung pada input kecil sebelum menulis sigma. Untuk soal perbandingan, hitung **selisih dua fungsi**, cari akarnya, lalu uji satu nilai pada setiap rentang. Untuk rekursi, tulis biaya per tingkat sebelum memilih rumus.

**Asal pola:** ingatan Sensei tentang UTS Analisis Algoritme 13 Oktober 2026. Soal dan angka dalam dokumen ini disusun ulang sebagai latihan; tidak diklaim berasal dari naskah ujian.
