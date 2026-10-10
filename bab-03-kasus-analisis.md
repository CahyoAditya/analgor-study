# Bab 3 — Best Case, Average Case, dan Worst Case

> Inti bab: kompleksitas tidak melekat pada satu ukuran *n* saja. Susunan data dan letak target juga menentukan jumlah pekerjaan.

## 1. Definisi yang harus dibedakan

Untuk setiap input *x* berukuran *n*, misalkan *C(x)* adalah jumlah operasi dasarnya. Maka:

- **Best case** B(n) = minimum C(x) di antara semua input berukuran *n* yang diizinkan.
- **Worst case** W(n) = maksimum C(x) di antara input tersebut.
- **Average case** A(n) = Σₓ Pr(x) C(x), yaitu nilai harapan menurut distribusi input yang dinyatakan.

Karena B(n) ≤ A(n) ≤ W(n), batas terbaik dan terburuk dapat mengapit rata-rata, tetapi tidak otomatis memberi nilai rata-rata yang tepat. Jika distribusi tidak diberikan, klaim average case biasanya belum terdefinisi. Jangan menyamakan “nilai tengah best dan worst” dengan expected value tanpa alasan.

## 2. Contoh menyeluruh: linear search

Cari target dalam larik panjang *n* dari kiri ke kanan. Jika target di indeks 0, perlu satu perbandingan: best case Θ(1). Jika target di indeks *n − 1* atau tidak ada, perlu *n* perbandingan: worst case Θ(n).

Jika **dijamin ditemukan tepat sekali** dan setiap dari *n* posisi sama mungkin, rata-rata jumlah perbandingan ialah:

A(n) = (1 + 2 + … + n)/n = (n + 1)/2 = Θ(n).

Jika target tidak ditemukan dengan peluang *q*, dan bila ditemukan posisinya seragam, maka A(n) = (1−q)(n+1)/2 + qn. Misalnya *q = 1/4*, A(n) = 3(n+1)/8 + n/4 = (5n + 3)/8. **Mengapa peluang penting?** Pencarian gagal selalu memeriksa semua elemen, jadi rata-rata berubah saat pola penggunaan berubah.

Jika elemen bisa duplikat, definisi “posisi target seragam” tidak lagi otomatis cocok untuk algoritme yang berhenti pada kemunculan pertama. Sebutkan model distribusinya sebelum menghitung.

## 3. Contoh algoritme lain

**Insertion sort:** input sudah terurut butuh satu pemeriksaan per elemen dan hampir tanpa pergeseran, Θ(n). Input urut terbalik memaksa elemen ke-*i* bergeser melewati *i* elemen, sehingga Σᵢ₌₁ⁿ⁻¹ i = Θ(n²). Rata-rata juga Θ(n²) di bawah model permutasi acak, sebab jumlah inversi yang diharapkan adalah n(n−1)/4.

**Binary search:** untuk larik terurut, target tengah memberi best Θ(1); pencarian yang terus membelah sampai habis memberi worst Θ(log n). Rata-rata atas posisi seragam adalah Θ(log n), tetapi bentuk eksaknya bergantung pada ukuran dan peluang target tidak ada.

**Quick sort:** partisi seimbang menghasilkan Θ(n log n), sedangkan partisi sangat timpang memberi Θ(n²). Rata-rata Θ(n log n) memerlukan asumsi seperti urutan input acak atau pivot acak; hanya menulis “pivot tengah” tidak cukup menjamin partisi seimbang karena posisi tengah berbeda dari nilai median.

## 4. Notasi pertumbuhan bukan nama kasus

Big-O adalah batas atas fungsi; worst case adalah pilihan input yang menghasilkan biaya maksimum. Kita bisa menulis W(n) ∈ Θ(n) untuk linear search. Best case-nya B(n) ∈ Θ(1), dan average case pada distribusi di atas A(n) ∈ Θ(n). Kalimat “Big-O = worst case” terlalu menyederhanakan: O(·) juga dapat membatasi fungsi best atau average jika dinyatakan jelas, dan batasnya bisa longgar.

Jika *T(n) = 2n² + 3n + 1*, bukti O(n²): untuk *n ≥ 1*, T(n) ≤ 6n². Bukti Ω(n²): T(n) ≥ 2n². Jadi Θ(n²). Analisis fungsi ini terpisah dari pertanyaan input mana yang menghasilkan T.

## 5. Menaksir perubahan ukuran

Jika T(n) = cn³ dan T(50) = 0,5 detik, maka c = 0,5/50³. Untuk 400 item, rasio ukuran 400/50 = 8; rasio waktu 8³ = 512. Jadi T(400) = **256 detik**. Cara rasio menghindari menghitung *c* secara eksplisit. Namun asumsi model kubik persis, mesin sama, dan overhead diabaikan harus disebut.

Misal tiga algoritme sama-sama 5 detik pada *n = 50*: P dengan model n³, Q n², R n log₂ n. Pada *n = 5000*, faktor ukuran 100. P ≈ 5·100³ = 5.000.000 detik; Q ≈ 5·100² = 50.000 detik; R ≈ 5·[5000 log₂5000/(50 log₂50)] ≈ 1.089 detik. Untuk R, faktor waktunya sekitar 217,72, bukan 100²: faktor 100 dari *n* masih dikalikan rasio logaritma sekitar 2,177. Model ini perkiraan dari titik kalibrasi, bukan janji performa nyata.

## 6. Membandingkan dua fungsi dengan konstanta

Contoh responsi: X(n) = 0,05n log₂ n ms dan Y(n) = 3n ms. X lebih cepat jika 0,05 log₂ n < 3, yakni *n < 2⁶⁰*. Pada *n = 10¹⁰*, log₂ n ≈ 33,22, jadi X lebih cepat. Secara asimtotik Y akhirnya menang. Tunjukkan titik potong agar peserta melihat beda antara keputusan praktis dan kelas pertumbuhan.

### Menyusun distribusi average case dengan benar

Ambil linear search pada empat posisi. Jika peluang target di posisi 1, 2, 3, dan 4 masing-masing 0,4; 0,3; 0,2; 0,1, nilai harapan perbandingannya adalah *0,4·1 + 0,3·2 + 0,2·3 + 0,1·4 = 2*. Asumsi posisi seragam justru menghasilkan *(1+2+3+4)/4 = 2,5*. Kedua hasil sah untuk distribusi berbeda; tidak ada “average case” tunggal tanpa model peluang.

Jika juga ada kemungkinan tidak ditemukan, tambahkan satu keadaan biaya *n* dengan peluangnya. Pastikan seluruh peluang berjumlah 1. Untuk distribusi besar, kita sering tidak menghitung semua input satu per satu; kita kelompokkan keadaan yang mempunyai biaya sama atau memakai linearitas harapan, seperti saat menghitung inversi insertion sort.

**Mengapa worst case tetap berguna?** Ia memberi jaminan batas bagi semua input yang diizinkan, termasuk yang jarang tetapi mahal. **Mengapa average case juga berguna?** Ia menggambarkan beban tipikal jika model peluang mewakili penggunaan nyata. Pilih ukuran yang sesuai dengan kebutuhan, dan sebutkan modelnya.

## 7. Hal yang sering luput saat mengajar

Tanyakan “apakah target pasti ada?”, “semua posisi sama mungkin?”, “apakah data terurut?”, dan “apakah biaya operasi setara?” sebelum menghitung rata-rata. Bila soal tidak menjawab, tulis asumsi eksplisit lalu selesaikan di bawah asumsi tersebut.

## Latihan bertingkat

1. **Mudah.** Pada linear search 8 elemen, berapa perbandingan bila target ada di indeks 0, indeks 7, atau tidak ada?
2. **Mudah.** Jelaskan beda maksimum biaya dan nilai harapan biaya.
3. **Mudah.** Berikan best dan worst case linear search dalam Θ.
4. **Sedang.** Jika target dijamin ada dan seragam di 7 posisi, hitung rata-rata perbandingan tepat.
5. **Sedang.** Jika target tidak ada dengan peluang 1/2 dan bila ada posisinya seragam di *n* posisi, turunkan A(n).
6. **Sedang.** Buktikan *2n² + 3n + 1 ∈ Θ(n²)* dengan konstanta eksplisit.
7. **Sedang.** Mengapa “pivot elemen tengah” pada quick sort tidak menjamin pembagian sama besar? Beri larik contoh.
8. **Sulit — Adaptasi responsi 3.** Model kubik memerlukan 0,5 s untuk 50 elemen. Berapa waktu perkiraan untuk 400 elemen?
9. **Sulit — Adaptasi responsi 3.** Bandingkan X(n) = 0,05n log₂ n dan Y(n) = 3n. Di mana X lebih cepat, sama, dan lebih lambat?
10. **Sulit.** Untuk insertion sort atas permutasi acak dari *n* nilai berbeda, jelaskan mengapa nilai harapan jumlah inversi adalah n(n−1)/4.
11. **Sulit — Adaptasi responsi 3.** P, Q, R masing-masing 5 detik saat *n = 50*, dengan model n³, n², dan n log₂ n. Perkirakan waktu saat *n = 5000*.
12. **Sulit.** Apakah B(n) = Θ(1) dan W(n) = Θ(n) cukup untuk menyimpulkan A(n) = Θ(n)? Bangun distribusi linear search yang menjadi contoh penyangkal jika perlu.

### Jawaban dan alasan singkat

1. Berturut-turut **1, 8, 8** perbandingan.
2. Maksimum memilih input termahal; nilai harapan menimbang tiap input dengan peluangnya.
3. Best Θ(1), worst Θ(n).
4. (1+…+7)/7 = 28/7 = **4**.
5. A(n) = ½·n + ½·(n+1)/2 = (3n+1)/4 = Θ(n).
6. Untuk *n ≥ 1*, *2n² ≤ T(n) ≤ 6n²*; ambil konstanta 2 dan 6.
7. Indeks tengah tidak sama dengan median nilai. Misal [2, 3, 1, 4, 5]: pivot pada indeks tengah bernilai 1, menghasilkan sisi kosong dan sisi berisi empat nilai.
8. **256 detik**, karena 0,5·(400/50)³ = 0,5·512.
9. X lebih cepat untuk *0 < n < 2⁶⁰*, sama di *2⁶⁰*, dan lebih lambat di atasnya; anggap *n ≥ 1* agar log terdefinisi sesuai model.
10. Ada C(n,2) pasangan. Pada permutasi seragam, masing-masing pasangan terbalik dengan peluang 1/2. Linearitas harapan memberi C(n,2)/2 = n(n−1)/4.
11. P **5.000.000 s**, Q **50.000 s**, R sekitar **1.089 s**. Untuk R, hitung 5·100·(log₂5000/log₂50) ≈ 1.088,6; tiga angka bergantung pada model skala yang diasumsikan.
12. Tidak. Jika target hampir selalu di posisi pertama, misalnya peluang 1−1/n di indeks 0 dan 1/n tidak ditemukan, A(n) = (1−1/n)·1 + (1/n)·n = 2−1/n = Θ(1), meskipun worst Θ(n).

**Sumber bab:** Kuliah 3; Lembar Kerja Responsi Pertemuan 3; Bank Soal K3 dalam ZIP yang diberikan.
