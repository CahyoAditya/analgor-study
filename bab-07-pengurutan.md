# Bab 7 — Algoritme Pengurutan dan Cara Memilihnya

> Mengurutkan berarti menyusun menurut kunci dan aturan yang jelas. Analisis yang baik menyebut waktu, ruang, stabilitas, serta pola input yang membuat algoritme cepat atau lambat.

## 1. Spesifikasi: kunci, urutan, dan stabilitas

Record dapat memiliki beberapa bidang. Misalnya transaksi diurutkan menurut `timestamp` naik, lalu `userId` naik. **Stabil** berarti jika dua record memiliki *kunci pengurutan yang sama*, urutan relatifnya tetap seperti semula. Stabilitas penting ketika dua tahap pengurutan digabung: urutkan kunci sekunder lebih dulu, kemudian kunci primer memakai algoritme stabil. Jika comparator sekaligus membandingkan pasangan `(timestamp, userId)`, stabilitas masih menjaga urutan input bagi pasangan yang sama, tetapi bukan satu-satunya cara mendapatkan urutan dua kunci.

In-place biasanya berarti ruang tambahan kecil di luar input; implementasi rinci bisa berbeda. Perbandingan juga harus konsisten: aturan yang tidak transitif dapat membuat hasil pengurutan tidak bermakna.

## 2. Tiga algoritme kuadratik yang perlu dibedakan

**Insertion sort** menjaga prefiks terurut. Ambil elemen berikutnya sebagai kunci, geser elemen prefiks yang lebih besar ke kanan, lalu sisipkan kunci. Invariant-nya: sebelum iterasi *i*, A[0..i−1] sudah terurut. Best Θ(n) jika data sudah terurut; worst Θ(n²) jika terbalik; ruang tambahan Θ(1). Ia stabil jika hanya menggeser elemen yang **lebih besar**, bukan yang sama. Sangat baik untuk larik kecil atau hampir terurut.

**Selection sort** mencari elemen terkecil pada sisa larik lalu menukarnya ke depan. Jumlah perbandingan selalu n(n−1)/2 = Θ(n²), bahkan ketika input sudah terurut. Ia bisa melakukan hanya O(n) pertukaran, tetapi pertukaran biasa dapat merusak stabilitas. Misal record [2ₐ, 2ᵦ, 1]: menukar 1 ke depan memberi [1, 2ᵦ, 2ₐ], sehingga dua record bernilai 2 berbalik.

**Bubble sort** membandingkan tetangga dan menukar jika salah urut. Setelah satu lintasan penuh, elemen terbesar berada di akhir. Dengan pemeriksaan apakah ada pertukaran, best Θ(n) pada data sudah terurut; tanpa pemeriksaan dini, bahkan best bisa Θ(n²). Worst Θ(n²). Ia stabil bila elemen sama tidak ditukar. Jadi pernyataan “best bubble sort O(n)” memerlukan varian optimisasi yang jelas.

## 3. Merge sort: biaya dan stabilitas

Merge sort membagi larik menjadi dua, mengurutkan masing-masing, lalu menggabung. Relasi T(n) = 2T(n/2) + Θ(n), sehingga Θ(n log n) pada best, average, dan worst untuk implementasi standar. Buffer gabung biasa memerlukan O(n) ruang tambahan.

Pada proses *merge*, bandingkan elemen pertama kedua sisi terurut, ambil yang lebih kecil. Jika nilai sama, ambil dari **sisi kiri lebih dulu**. Mengapa? Semua elemen sisi kiri semula mendahului elemen sisi kanan; keputusan itu mempertahankan urutan relatif. Jika sisi kanan diambil dulu saat sama, implementasi merge menjadi tidak stabil.

Contoh: gabungkan [1ₐ, 3ₐ, 5] dan [1ᵦ, 3ᵦ, 4]. Dengan aturan kiri saat sama, hasil [1ₐ, 1ᵦ, 3ₐ, 3ᵦ, 4, 5]. Subskrip menandai identitas record, bukan nilai kunci.

## 4. Quick sort: mengapa pivot menentukan risiko

Quick sort memilih pivot, mempartisi nilai menurut pivot, lalu mengurutkan subbagian. Partisi satu tingkat membutuhkan Θ(n). Jika kedua sisi cukup seimbang, T(n) ≈ 2T(n/2) + Θ(n) = Θ(n log n). Jika pivot selalu paling kecil atau paling besar, T(n) = T(n−1) + Θ(n) = Θ(n²). Quick sort in-place yang umum **tidak stabil**; ruang stack bergantung pada kedalaman partisi.

“Pivot elemen tengah” berarti mengambil posisi tengah, bukan median nilai. Pada larik tertentu, nilai di posisi tengah dapat menjadi terkecil dan memberi partisi buruk. Untuk latihan responsi yang meminta hasil satu langkah partisi, hasil larik **bergantung pada skema partisi** (Hoare, Lomuto, tiga arah) dan cara menangani nilai sama. Nyatakan skemanya sebelum memberi indeks batas; tidak ada satu susunan hasil yang universal.

## 5. Heap sort dan batas metode perbandingan

Heap sort membangun max-heap lalu berulang kali memindah elemen terbesar ke ujung. Membangun heap Θ(n), setiap ekstraksi Θ(log n), total Θ(n log n) pada worst case dan O(1) ruang tambahan untuk larik in-place. Heap sort biasa tidak stabil.

Untuk pengurutan berbasis **perbandingan** atas *n* kunci berbeda, pohon keputusan harus membedakan *n!* urutan input; tinggi terburuk paling sedikit log₂(n!) = Ω(n log n). Itulah alasan merge/heap sort Θ(n log n) sudah optimal dalam model perbandingan umum. Counting sort tidak melanggar batas ini karena memakai informasi tambahan: kunci bilangan bulat dalam rentang terbatas.

## 6. Counting sort, radix sort, dan batas kunci

Counting sort menghitung frekuensi kunci 0..*k*, membuat jumlah kumulatif, lalu menempatkan record ke output. Biaya Θ(n + k) waktu dan Θ(n + k) ruang jika memakai output terpisah. **Versi stabil** memindai input dari kanan ke kiri saat memakai jumlah kumulatif sebagai posisi terakhir tiap kunci. Bila *k* sangat besar dibanding *n*, memori dan waktu inisialisasi menjadi masalah.

Contoh kunci [2,5,3,0,2,3,0,3]: frekuensi untuk 0..5 adalah [2,0,2,3,0,1], kumulatif [2,2,4,7,7,8], hasil terurut [0,0,2,2,3,3,3,5]. Jika menghitung record dengan data tambahan, stabilitas penempatan perlu diperhatikan.

Radix sort mengurutkan digit dari digit paling rendah ke paling tinggi memakai pengurutan stabil pada tiap digit. Jika ada *d* digit dan basis digit *b*, biaya Θ(d(n+b)). Kebenarannya bergantung pada stabilitas tiap putaran: urutan yang sudah ditentukan oleh digit lebih rendah tidak boleh rusak ketika digit lebih tinggi diproses.

## 7. Kasus responsi: data besar dan Top-K

Untuk 3 juta transaksi dengan kunci utama timestamp dan sekunder userId, merge sort stabil memberi O(n log n) waktu dan O(n) ruang tambahan; comparator pasangan memastikan kedua kunci dipakai. Jika data tidak muat memori, *external merge sort* lebih cocok, tetapi analisis I/O perlu ditambahkan.

Untuk hanya *K = 1000* skor terbesar dari *n = 20 juta* angka, pertahankan **min-heap** berukuran K. Masukkan K pertama; untuk tiap nilai berikutnya, jika lebih besar dari akar heap, ganti akar dan perbaiki heap. Biaya O(n log K) dalam batas sederhana, lebih tepat O(n log K + K log K) termasuk mengurutkan isi heap menurun di akhir; ruang O(K). Membangun heap awal bisa O(K). Full sort O(n log n) masuk akal bila hampir seluruh urutan juga dibutuhkan, data sudah hampir terurut dan algoritme adaptif cocok, atau faktor implementasi lebih menguntungkan pada ukuran aktual.

## 8. Ringkasan keputusan

| Algoritme | Best | Worst | Ruang ekstra umum | Stabil pada implementasi standar? |
| --- | --- | --- | --- | --- |
| Insertion | Θ(n) | Θ(n²) | O(1) | Ya, jika sama tidak digeser |
| Selection | Θ(n²) | Θ(n²) | O(1) | Tidak dengan pertukaran biasa |
| Bubble dengan keluar dini | Θ(n) | Θ(n²) | O(1) | Ya, jika sama tidak ditukar |
| Merge | Θ(n log n) | Θ(n log n) | O(n) | Ya, jika kiri didahulukan saat sama |
| Quick in-place biasa | Θ(n log n) pada partisi seimbang | Θ(n²) | O(log n) rata-rata stack, O(n) worst | Umumnya tidak |
| Heap | Θ(n log n) | Θ(n log n) | O(1) | Tidak |
| Counting untuk rentang 0..k | Θ(n+k) | Θ(n+k) | O(n+k) | Ya, bila penempatan stabil |

## Contoh perlahan: ikuti keadaan larik

### Insertion sort

Urutkan *[9,5,6,3]* naik. Anggap bagian sebelum indeks *i* sudah terurut. Saat *i = 1*, kunci 5 dibandingkan dengan 9. Karena 9 > 5, geser 9 ke kanan lalu letakkan 5 pada ruang yang kosong: *[5,9,6,3]*. Saat *i = 2*, kunci 6 dibandingkan dengan 9; geser 9, lalu bandingkan 6 dengan 5 dan berhenti karena 5 ≤ 6. Hasilnya *[5,6,9,3]*. Saat *i = 3*, kunci 3 melewati 9, 6, dan 5, sehingga hasil akhir *[3,5,6,9]*.

Mengapa bagian yang telah diproses tetap terurut? Kita hanya menggeser elemen yang lebih besar dari kunci dan menaruh kunci tepat setelah elemen terakhir yang tidak lebih besar. Bila dua kunci sama, jangan geser yang lama: aturan itu menjaga urutan relatifnya dan membuat algoritme stabil. Pada input terbalik, kunci ke-*i* melintasi *i* elemen; total pergeseran *1+2+···+(n−1) = n(n−1)/2*, sehingga worst Θ(n²).

### Merge: nilai sama harus diputuskan dengan sengaja

Gabungkan kiri *[1ₐ,3ₐ,5]* dan kanan *[1ᵦ,3ᵦ,4]*. Bandingkan kepala 1ₐ dan 1ᵦ: sama, ambil 1ₐ dari kiri lebih dulu. Berikutnya ambil 1ᵦ karena 1ᵦ < 3ₐ. Bandingkan 3ₐ dan 3ᵦ: sama, ambil 3ₐ dari kiri. Lalu ambil 3ᵦ, 4, dan sisa 5. Hasilnya *[1ₐ,1ᵦ,3ₐ,3ᵦ,4,5]*. Tanda bawah hanya membedakan identitas record. Bila saat sama kita mengambil kanan dulu, 1ᵦ mendahului 1ₐ padahal urutan asalnya kebalikan; stabilitas rusak.

### Mengapa quick sort dapat menjadi kuadratik?

Jika sebuah partisi memisahkan *n* elemen menjadi dua bagian hampir sama, kedalaman pohon sekitar log₂ *n*. Setiap tingkat total memeriksa sekitar *n* elemen, sehingga total sekitar *n log n*. Jika pivot selalu elemen terkecil, ukuran masalah berikutnya *n−1*, lalu *n−2*, dan seterusnya. Kerja partisinya menjadi sekitar *n + (n−1) + ··· + 1 = Θ(n²)*. Posisi pivot di tengah larik tidak menjamin nilainya median; itulah sebabnya posisi tengah saja tidak menjamin pembagian seimbang.

## Latihan bertingkat

1. **Mudah.** Jalankan dua iterasi pertama insertion sort pada [9,5,6,3,3,8,1]. Tunjukkan kunci dan larik setelah setiap iterasi.
2. **Mudah.** Kapan insertion sort mencapai Θ(n)? Jelaskan dari jumlah pergeseran.
3. **Mudah.** Berapa perbandingan selection sort untuk *n = 6*?
4. **Sedang.** Mengapa merge harus memilih elemen kiri lebih dahulu bila kunci sama agar stabil?
5. **Sedang.** Gabungkan [1ₐ,3ₐ,5] dan [1ᵦ,3ᵦ,4] secara stabil.
6. **Sedang.** Tuliskan frekuensi dan jumlah kumulatif counting sort untuk [2,5,3,0,2,3,0,3].
7. **Sedang.** Jelaskan beda pivot pada indeks tengah dan median nilai dalam quick sort.
8. **Sulit — Adaptasi responsi 7.** Untuk transaksi `(timestamp,userId,amount)`, pilih cara mengurutkan utama timestamp dan sekunder userId sambil mempertahankan urutan bagi pasangan kunci yang sama; nyatakan biaya dan ruang.
9. **Sulit — Adaptasi responsi 7.** Rancang cara mengeluarkan 1000 skor terbesar dari 20 juta angka dalam urutan menurun. Jelaskan biaya waktu dan ruang.
10. **Sulit — Adaptasi responsi 7.** Mengapa pertanyaan “hasil partisi quick sort dengan pivot tengah” belum menentukan satu larik hasil jika skema partisi tidak disebut?
11. **Sulit.** Berikan contoh tiga record yang menunjukkan selection sort dengan pertukaran biasa tidak stabil.
12. **Sulit.** Jelaskan mengapa counting sort Θ(n+k) tidak bertentangan dengan batas Ω(n log n) untuk sorting berbasis perbandingan.

### Jawaban dan alasan singkat

1. Iterasi *i=1*: kunci 5, hasil **[5,9,6,3,3,8,1]**. Iterasi *i=2*: kunci 6, hasil **[5,6,9,3,3,8,1]**.
2. Saat sudah terurut, tiap kunci dibandingkan secukupnya dan tidak bergeser: Θ(n) total.
3. 6·5/2 = **15** perbandingan.
4. Elemen sisi kiri muncul lebih dahulu pada input asal; memilihnya saat sama mempertahankan urutan itu.
5. **[1ₐ,1ᵦ,3ₐ,3ᵦ,4,5]**.
6. Frekuensi 0..5: **[2,0,2,3,0,1]**. Kumulatif: **[2,2,4,7,7,8]**.
7. Indeks tengah hanya posisi; median nilai membagi banyak elemen di kiri dan kanan secara seimbang menurut nilai. Keduanya dapat berbeda.
8. Gunakan merge sort stabil dengan comparator pasangan `(timestamp,userId)`: O(n log n) waktu, O(n) buffer; pasangan yang sama tetap pada urutan awal bila aturan merge stabil.
9. Min-heap ukuran K = 1000, lalu sort isi heap menurun: O(n log K + K log K) waktu, O(K) ruang. Nilai lebih kecil dari akar saat heap penuh tidak perlu disimpan.
10. Hoare dan Lomuto memindahkan elemen dengan aturan berbeda, sementara duplikat dapat ditempatkan pada sisi berbeda. Nyatakan skema dan tie rule sebelum menentukan hasil.
11. **[2ₐ,2ᵦ,1]** menjadi **[1,2ᵦ,2ₐ]** setelah menukar minimum ke depan; urutan dua kunci 2 berbalik.
12. Batas Ω(n log n) mengasumsikan hasil diperoleh hanya dari perbandingan antar kunci. Counting sort mengindeks rentang kunci 0..*k* dan menghitung frekuensi, sehingga memakai operasi dan asumsi tambahan.

### Pembahasan lebih lengkap: latihan 6 dan 9

**Latihan 6 — counting sort.** Dari [2,5,3,0,2,3,0,3], kunci 0 muncul dua kali, 1 nol, 2 dua, 3 tiga, 4 nol, dan 5 satu. Jadi frekuensi untuk 0..5 adalah [2,0,2,3,0,1]. Jumlah kumulatif dihitung dari kiri: 2; 2+0=2; 2+2=4; 4+3=7; 7+0=7; 7+1=8. Hasilnya [2,2,4,7,7,8]. Angka 7 pada kunci 3 berarti tujuh elemen bernilai **paling besar 3**, bukan frekuensi kunci 3. Inilah yang dipakai untuk menentukan batas posisi di output.

**Latihan 9 — mengapa min-heap untuk skor terbesar?** Simpan 1000 skor kandidat. Akar min-heap ialah yang paling kecil **di antara kandidat yang disimpan**. Untuk tiap skor baru, jika tidak lebih besar daripada akar, sudah ada 1000 kandidat yang sekurangnya sebesar skor itu, jadi skor baru tidak perlu disimpan. Jika lebih besar, ganti akar dan pulihkan sifat heap dalam O(log 1000). Ulangi untuk 20 juta skor: O(n log K) sebagai batas sederhana, dengan ruang O(K). Terakhir keluarkan atau urutkan K kandidat untuk mendapatkan urutan menurun, menambah O(K log K). Akar heap bukan skor terkecil dari seluruh input; ia hanya ambang kandidat saat itu.

**Sumber bab:** Kuliah 7; Lembar Kerja Responsi Pertemuan 7; Bank Soal K7; pembahasan UTS 2020–2021 dalam ZIP yang diberikan.
