# Bab 1 — Dasar Matematika untuk Analisis Algoritme

> Pertanyaan pengajar: mengapa kita perlu logika, kombinatorika, dan pembuktian sebelum menghitung waktu program? Karena hasil analisis adalah klaim untuk *semua* input dalam suatu kelas, bukan sekadar pengamatan pada beberapa contoh.

## 1. Apa yang dihitung dalam analisis algoritme?

Algoritme mengubah input menjadi output melalui langkah berhingga. Dua tuntutannya berbeda: **benar** berarti output memenuhi spesifikasi; **efisien** berarti sumber daya tumbuh cukup lambat ketika ukuran input membesar. Algoritme yang cepat tetapi salah tetap tidak menyelesaikan masalah.

Ukuran input bergantung pada masalah. Untuk mencari elemen dalam larik, ukuran wajar adalah jumlah elemen *n*. Untuk graf, kita sering perlu dua ukuran, jumlah simpul *V* dan sisi *E*. Untuk bilangan bulat *N*, panjang input dalam bit adalah sekitar ⌊log₂ N⌋ + 1, bukan *N*. Perbedaan terakhir penting: loop yang menghitung sampai *N* membutuhkan waktu eksponensial terhadap jumlah bit input dalam keadaan terburuk.

**Operasi dasar** ialah pekerjaan yang kita pilih untuk dihitung, misalnya perbandingan dua elemen. Pilihan itu harus konsisten. Jika analisis memakai model biaya satuan, satu perbandingan atau penjumlahan dianggap O(1); pada bilangan berukuran sangat besar, biaya aritmetika bit perlu dihitung terpisah.

## 2. Proposisi, implikasi, dan kuantor

Proposisi ialah kalimat yang bisa diberi nilai benar atau salah. Kalimat “*n* genap” baru menjadi proposisi setelah *n* ditentukan atau dikuantifikasi. Dalam klaim “untuk setiap bilangan bulat *n*”, satu contoh benar belum membuktikan klaim; satu contoh salah cukup untuk membantahnya.

Implikasi *P ⇒ Q* menyatakan: setiap keadaan yang memenuhi *P* juga memenuhi *Q*. Untuk membuktikannya, mulai dari asumsi *P*, lalu turunkan *Q*. **Kontraposisi** *¬Q ⇒ ¬P* setara secara logis. Kebalikannya, *Q ⇒ P*, tidak otomatis benar. Contoh: “kelipatan 4 pasti genap” benar; “genap pasti kelipatan 4” salah karena 6.

Untuk membantah klaim universal, carilah **contoh penyangkal**. Klaim “*n² + 2* selalu ganjil untuk setiap bilangan positif *n*” salah: jika *n = 2*, hasilnya 6. Untuk membuktikan klaim eksistensial, satu contoh yang memenuhi sudah cukup.

## 3. Tiga cara membuktikan

**Bukti langsung.** Jika *n* genap, tulis *n = 2k* dengan *k* bulat. Maka *3n + 2 = 6k + 2 = 2(3k + 1)*, sehingga genap. Definisi genap dipakai sebagai jembatan dari kata ke aljabar.

**Bukti kontradiksi.** Asumsikan negasi klaim, lalu turunkan sesuatu yang mustahil. Contoh dari responsi: untuk bilangan bulat *a,b*, buktikan *a² − 4b − 1 ≠ 0*. Jika sama dengan nol, *a² = 4b + 1*, sehingga *a² ≡ 1 (mod 4)*. Ini mungkin untuk *a* ganjil! Jadi pernyataan pada lembar itu **salah**: *a = 1, b = 0* memberi nol. Pengajar perlu memeriksa klaim sebelum mencoba membuktikannya.

**Induksi.** Untuk klaim *P(n)* pada semua *n ≥ 1*, buktikan (i) *P(1)*, lalu (ii) dari *P(k)* turunkan *P(k + 1)*. Ini seperti memastikan anak tangga pertama dan hubungan ke tangga berikutnya. Contoh jumlah bilangan 1 sampai *n*:

S(n) = 1 + 2 + … + n = n(n + 1)/2.

- Basis *n = 1*: kedua sisi bernilai 1.
- Hipotesis: S(k) = k(k + 1)/2.
- Langkah: S(k + 1) = S(k) + (k + 1) = k(k + 1)/2 + (k + 1) = (k + 1)(k + 2)/2.

**Mengapa penting?** Rumus ini mengubah jumlah kerja loop segitiga menjadi fungsi kuadrat. Tanpa bukti, rumus mudah dipakai pada batas indeks yang salah.

## 4. Deret dan logaritma

Deret aritmetika 1 + 2 + … + n = n(n + 1)/2 = Θ(n²). Deret geometri 1 + r + r² + … + rᵏ = (rᵏ⁺¹ − 1)/(r − 1) untuk *r ≠ 1*. Bila *r = 2*, jumlahnya 2ᵏ⁺¹ − 1. Bila *0 < r < 1*, jumlahnya dibatasi oleh 1/(1 − r) bahkan saat jumlah suku bertambah.

Logaritma membalik pemangkatan: log₂ *n = k* berarti 2ᵏ = *n*. Jika ukuran masalah dibagi dua tiap langkah, setelah *k* langkah sisanya sekitar *n/2ᵏ*; berhenti pada 1 berarti *k ≈ log₂ n*. Jika ukuran dikurangi satu tiap langkah, jumlah langkahnya sekitar *n*. Perbedaan “dibagi” versus “dikurangi” menjadi sumber utama O(log n) versus O(n).

## 5. Aturan pencacahan, kombinasi, dan pohon

Jika keputusan pertama punya *a* pilihan dan setiap pilihan punya *b* kelanjutan, aturan perkalian memberi *ab* kemungkinan. Memilih *r* benda dari *n* tanpa memperhatikan urutan memberi C(n,r) = n!/[r!(n−r)!]. Pembagi *r!* muncul karena setiap himpunan yang sama dapat diurutkan dengan *r!* cara.

Contoh responsi: memilih 4 dari 10 proyek menghasilkan C(10,4) = 210 cara; memilih nol proyek menghasilkan C(10,0) = 1 cara, yaitu himpunan kosong. Memilih dua dari lima anggota menghasilkan C(5,2) = 10 cara.

Jika **urutan** justru penting, gunakan permutasi P(n,r) = n!/(n−r)!. Misalnya memilih ketua dan wakil dari lima orang menghasilkan 5·4 = 20 cara, sedangkan memilih dua anggota tanpa jabatan hanya C(5,2) = 10 cara. Hubungannya P(n,r) = C(n,r)·r!: setiap kelompok beranggotakan *r* dapat diurutkan dengan *r!* cara. Aturan penjumlahan dipakai untuk pilihan yang saling lepas (“memilih dari kelompok A **atau** B”); jika kelompoknya tumpang tindih, kurangi irisannya seperti pada bagian berikut.

Untuk setiap dari *n* barang ada keputusan ambil/tidak ambil, sehingga ada 2ⁿ subset. Identitas Σᵣ₌₀ⁿ C(n,r) = 2ⁿ menjumlahkan subset menurut ukurannya. Ini menerangkan mengapa pencarian brute force pada semua subset bisa tumbuh eksponensial.

Pohon keputusan bercabang *b* sampai kedalaman *d*, jika akar berada pada kedalaman 0, memiliki *bˡ* simpul pada kedalaman *l* dan total Σₗ₌₀ᵈ bˡ simpul. Misalnya *b = 2, d = 3*: 1 + 2 + 4 + 8 = 15. Selalu nyatakan apakah “level 1” berarti akar; sumber berbeda bisa memakai konvensi berbeda.

## 6. Inklusi–eksklusi

Menjumlah |A| + |B| menghitung elemen dalam irisan dua kali, sehingga |A ∪ B| = |A| + |B| − |A ∩ B|. Untuk tiga himpunan, tambahkan ukuran masing-masing, kurangi tiga irisan berpasangan, lalu tambahkan kembali irisan ketiganya. Irisan tiga sempat ditambah tiga kali dan dikurangi tiga kali, jadi perlu ditambah sekali.

Contoh responsi: |A| = 50, |B| = 30, |C| = 20; irisan berpasangan 15, 10, 5; irisan tiga 2. Maka |A ∪ B ∪ C| = 50 + 30 + 20 − 15 − 10 − 5 + 2 = **72**.

## 7. Aljabar, selang, dan peluang yang dipakai lagi nanti

**Titik potong fungsi** adalah input *x* yang membuat dua output sama. Untuk *f(x) = 2x + 3* dan *g(x) = −x + 5*, samakan *2x + 3 = −x + 5*, sehingga *3x = 2* dan *x = 2/3*. Substitusi memberi *y = 13/3*. Titik potongnya *(2/3, 13/3)*. Dalam analisis algoritme, titik potong dua fungsi biaya menunjukkan ukuran input saat pilihan yang lebih cepat dapat berubah. Pertidaksamaan menentukan sisi kiri atau kanan yang lebih baik; kesamaan saja belum cukup.

**Notasi interval** membedakan apakah batas ikut masuk: `[a,b)` mencakup *a* dan mengecualikan *b*. Algoritme sering memakai rentang indeks `[lo,hi)` karena panjangnya tepat *hi − lo* dan dua rentang `[lo,mid)` serta `[mid,hi)` bersebelahan tanpa tumpang tindih. Jika *lo = hi*, rentangnya kosong. Ini memudahkan invariant binary search di Bab 6.

**Notasi sigma** menyatakan penjumlahan, misalnya Σᵢ₌₁ⁿ i. Indeks dummy *i* berubah pada setiap suku; *n* ialah batas. Mengganti indeks tanpa mengubah rentang dengan benar menghasilkan kesalahan satu suku. Contoh Σᵢ₌₀ⁿ⁻¹ i = n(n−1)/2, sedangkan Σᵢ₌₁ⁿ i = n(n+1)/2. Keduanya Θ(n²), tetapi nilainya tidak sama.

**Peluang dan nilai harapan** diperlukan saat input tidak selalu sama. Jika biaya suatu operasi ialah 1 ketika target berada di posisi pertama dan *n* ketika tidak ada, dengan peluang masing-masing *p* dan *(1−p)*, rata-ratanya *p·1 + (1−p)·n*. Nilai harapan bukan “pilih biaya tengah”; ia memberi bobot pada kemungkinan. Bab 3 mengembangkan ini untuk semua posisi target.

## 8. Cara menjelaskannya kepada peserta

Tanyakan dahulu: “Pernyataan ini berlaku untuk satu contoh atau semua *n*?” Lalu minta peserta menyebut definisi yang dipakai. Untuk soal pencacahan, tanyakan “apakah urutan berpengaruh?” sebelum memilih permutasi atau kombinasi. Untuk jumlah pekerjaan, gambar 3–4 level kecil sebelum menulis rumus umum.

## Latihan bertingkat

Kerjakan tanpa melihat bagian jawaban. Label **Adaptasi** menyatakan bentuk soal ditulis ulang dari sumber yang disebut.

1. **Mudah.** Apakah “*x + 2 = 5*” tanpa nilai atau kuantor untuk *x* merupakan proposisi? Jelaskan.
2. **Mudah.** Buktikan: jika *n* kelipatan 6, maka *n* genap dan kelipatan 3.
3. **Mudah.** Hitung 1 + 2 + … + 20 dan sebutkan mengapa rumusnya berlaku.
4. **Mudah.** Ada 6 buku berbeda; pilih 2 tanpa memedulikan urutan. Berapa cara?
5. **Sedang — Adaptasi responsi 1.** Pilih 4 dari 10 proyek. Jelaskan mengapa bukan 10 × 9 × 8 × 7.
6. **Sedang — Adaptasi responsi 1.** Pohon biner berkedalaman 4 dengan akar kedalaman 0: berapa daun dan seluruh simpul?
7. **Sedang.** Buktikan Σᵢ₌₁ⁿ (2i − 1) = n² dengan induksi.
8. **Sedang — Adaptasi responsi 1.** Hitung |A ∪ B ∪ C| untuk data 50, 30, 20; irisan pasangan 15, 10, 5; irisan tiga 2.
9. **Sulit — Adaptasi responsi 1.** Tentukan semua titik potong *y = x² − 4x + 3* dan *y = x + 1*. Periksa dengan substitusi.
10. **Sulit — Adaptasi responsi 1.** Periksa klaim “*a² − 4b − 1 ≠ 0* untuk setiap *a,b* bulat”. Berikan bukti atau contoh penyangkal.
11. **Sulit — Adaptasi UTS 2018.** Untuk *n* barang, buktikan jumlah pilihan mengambil 0 sampai *n* barang adalah 2ⁿ dengan dua cara berbeda.
12. **Sulit.** Jika satu keputusan memiliki 3 pilihan di tiap level selama *d* level, berapa total simpul dari akar sampai kedalaman *d*? Beri bentuk tertutup.

### Jawaban dan alasan singkat

1. Belum; kebenarannya bergantung pada *x*. “Untuk *x = 3*” atau “ada *x* sehingga…” menjadikannya proposisi.
2. Tulis *n = 6k = 2(3k) = 3(2k)*.
3. 20·21/2 = **210**; rumus diperoleh melalui pasangan ujung atau induksi.
4. C(6,2) = 6·5/2 = **15**; dua urutan untuk pasangan yang sama dihitung sekali.
5. C(10,4) = **210**. Perkalian itu menghitung setiap kelompok 4! kali karena urutan proyek tidak berpengaruh.
6. Daun 2⁴ = **16**; total 1 + 2 + 4 + 8 + 16 = **31**.
7. Basis 1 = 1². Jika jumlah sampai *k* adalah *k²*, tambah 2(k+1)−1 = 2k+1 sehingga menjadi *(k+1)²*.
8. **72**, dengan prinsip inklusi–eksklusi.
9. Samakan: *x² − 4x + 3 = x + 1*, jadi *x² − 5x + 2 = 0*. Maka *x = (5 ± √17)/2* dan *y = (7 ± √17)/2* dengan tanda yang sama.
10. Salah. *a = 1, b = 0* memberi *1 − 0 − 1 = 0*. Soal tidak boleh “dibuktikan” bila klaimnya salah.
11. Pertama, dua pilihan independen untuk tiap barang memberi 2ⁿ. Kedua, kelompokkan menurut banyak barang: Σᵣ₌₀ⁿ C(n,r) = (1+1)ⁿ = 2ⁿ.
12. Σₗ₌₀ᵈ 3ˡ = **(3ᵈ⁺¹ − 1)/2**. Kedalaman *d* memuat *d + 1* level termasuk akar.

**Sumber bab:** Kuliah 1; Lembar Kerja Responsi Pertemuan 1; Bank Soal K1; UTS 2018 dalam ZIP yang diberikan.
