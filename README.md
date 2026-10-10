# Panduan Belajar Analisis Algoritme: Kuliah 1–7

Panduan ini ditujukan kepada peserta yang sedang belajar analisis algoritme. Bacalah contoh dari masalahnya, ikuti alasan tiap langkah, lalu coba soal latihan secara mandiri. Urutan bab mengikuti tujuh berkas kuliah. **Bab 1 dan Bab 2 sudah berupa bacaan bertahap bergaya buku.** Masing-masing memiliki 16 latihan dan pembahasan dalam dokumen terpisah. Bab 3–7 masih menggunakan versi ringkas sebelumnya.

| Bab | Bacaan | Pertanyaan inti |
| --- | --- | --- |
| 1 | [Matematika untuk analisis algoritme](bab-01-dasar-matematika.md) | Mengapa aljabar, bukti, induksi, dan penghitungan kemungkinan bekerja? |
| 2 | [Pertumbuhan fungsi](bab-02-pertumbuhan-fungsi.md) | Apa arti biaya sebagai fungsi ukuran input? |
| 3 | [Kasus analisis](bab-03-kasus-analisis.md) | Masukan mana yang menghasilkan best, average, dan worst case? |
| 4 | [Algoritme iteratif](bab-04-algoritme-iteratif.md) | Berapa kali operasi dasar dalam perulangan dilakukan? |
| 5 | [Algoritme rekursif](bab-05-algoritme-rekursif.md) | Bagaimana membentuk dan menyelesaikan relasi rekurensi? |
| 6 | [Pencarian](bab-06-pencarian.md) | Asumsi data apa yang membenarkan strategi pencarian? |
| 7 | [Pengurutan](bab-07-pengurutan.md) | Bagaimana memilih algoritme urut menurut data dan kebutuhan? |

Latihan lengkap: [Bab 1](latihan-bab-01.md) · [Bab 2](latihan-bab-02.md). Setiap soal mencantumkan asalnya. Soal yang ditulis khusus untuk panduan ini diberi label jelas.

## Mulai dari sini jika rumus terasa melompat

Mulai dari Bab 1 bagian 1–5 untuk mengikuti alur pencarian, aljabar, logika, bukti, dan penjumlahan pekerjaan loop. Bagian 6–7 memperluas cara hitung ke pilihan bercabang dan peluang; bagian itu boleh dibaca sesudah inti dipahami. Pada Bab 2, ikuti cerita pencarian nama dari awal sampai akhir sebelum masuk ke soal loop. Coba ulangi tiap contoh dengan angka kecil tanpa melihat penjelasannya. Pada setiap perubahan bentuk, tanyakan: apa yang dihitung, dari mana angka itu berasal, dan mengapa langkah berikutnya sah?

Urutan belajar yang membantu: **Bab 1** untuk deret dan bukti → **Bab 2** untuk mengubah hitungan menjadi Θ → **Bab 3** untuk memahami asumsi peluang → **Bab 4** untuk jumlah operasi loop → **Bab 5** untuk pohon rekursi → **Bab 6–7** untuk menerapkan semuanya pada algoritme. Untuk waktu singkat, pahami satu contoh tuntas per bab sebelum berpindah.

## Cara memakai panduan ini

1. Baca cerita pembuka dan peta jalan bab sebelum masuk ke rumus.
2. Kerjakan ulang contoh sambil menyebut operasi yang dihitung. Jangan langsung melompat ke notasi Big-O.
3. Buka dokumen latihan bab, kerjakan dua soal mudah dan satu soal menantang tanpa melihat pembahasan.
4. Periksa alasan di pembahasan, lalu coba jelaskan ulang dengan urutan **masalah → asumsi → hitungan → alasan → pengecekan dengan input kecil**.

Jika waktu terbatas, dahulukan Bab 1 bagian induksi dan jumlah deret; Bab 2 definisi O/Ω/Θ; Bab 3 expected value; Bab 4 loop bergantung; Bab 5 pohon rekurensi dan syarat Master; Bab 6 invariant binary search; Bab 7 stabilitas dan trade-off. Ketujuh bab saling bertumpu: tanpa penjumlahan deret sulit memahami loop dan pohon rekurensi, sedangkan tanpa asumsi input mudah salah memilih searching/sorting.

## Konvensi

- Ukuran input ditulis *n*; untuk matriks digunakan *m × n*. Basis logaritma 2 kecuali disebut lain. Mengganti basis logaritma mengubah faktor konstan, bukan kelas Θ.
- *T(n)* berarti banyak operasi dasar dalam model biaya yang dinyatakan. Big-O adalah batas atas, Ω batas bawah, Θ batas ketat. Untuk menyebut kelas yang paling informatif, panduan ini biasanya memakai Θ.
- Potongan algoritme ditulis sebagai daftar langkah atau baris berindentasi, agar nyaman dibaca di ponsel. Indeks array dimulai dari 0 kecuali soal sumber memakai indeks 1.
- Soal berlabel **Adaptasi responsi** atau **Adaptasi UTS** disusun ulang dari tema atau angka sumber; bukan salinan ujian resmi atau jaminan akan keluar lagi.
- Beberapa bagian PDF berupa gambar tanpa lapisan teks. Panduan ini memakai bagian yang terbaca dan pengetahuan matematika yang diperiksa kembali; rujuk PDF asli ketika diagram atau potongan program tertentu diperlukan.

## Materi sumber

ZIP yang diberikan berisi tujuh PDF kuliah (Kuliah 1 sampai 7), tujuh PDF lembar kerja responsi (Pertemuan 1 sampai 7), bank soal K1–K7, dan contoh UTS 2018 serta pembahasan UTS 2020–2021. Catatan ini ditulis ulang sebagai panduan belajar; PDF tidak diunggah ulang ke repositori ini. Pada pembahasan UTS 2020–2021 terdapat rekurensi dengan biaya negatif atau koefisien anak pecahan; keduanya tidak boleh langsung dipaksa ke Teorema Master standar. Pada bank soal K4, loop yang mengubah *i* menjadi *i²* dari *i = 1* tidak pernah maju. Koreksi dan alasan matematisnya dijelaskan di bab terkait.
