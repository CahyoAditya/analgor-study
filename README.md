# Panduan Belajar Analisis Algoritme: Kuliah 1–7

Panduan ini membantu calon tutor memahami *mengapa* suatu analisis benar, lalu berlatih menjelaskannya. Urutan bab mengikuti tujuh berkas kuliah dalam materi yang diberikan. Setiap bab memuat konsep, contoh kerja, kesalahan yang sering terjadi, serta sedikitnya sepuluh latihan bertingkat dengan jawaban atau petunjuk pemeriksaan.

| Bab | Bacaan | Pertanyaan inti |
| --- | --- | --- |
| 1 | [Dasar matematika](bab-01-dasar-matematika.md) | Bagaimana membuktikan klaim dan menghitung banyak kemungkinan? |
| 2 | [Pertumbuhan fungsi](bab-02-pertumbuhan-fungsi.md) | Apa arti biaya sebagai fungsi ukuran input? |
| 3 | [Kasus analisis](bab-03-kasus-analisis.md) | Masukan mana yang menghasilkan best, average, dan worst case? |
| 4 | [Algoritme iteratif](bab-04-algoritme-iteratif.md) | Berapa kali operasi dasar dalam perulangan dilakukan? |
| 5 | [Algoritme rekursif](bab-05-algoritme-rekursif.md) | Bagaimana membentuk dan menyelesaikan relasi rekurensi? |
| 6 | [Pencarian](bab-06-pencarian.md) | Asumsi data apa yang membenarkan strategi pencarian? |
| 7 | [Pengurutan](bab-07-pengurutan.md) | Bagaimana memilih algoritme urut menurut data dan kebutuhan? |

## Cara memakai panduan ini untuk mengajar

1. Baca bagian **Intuisi** dan **Mengapa** pada setiap bab. Jelaskan kembali tanpa melihat teks.
2. Kerjakan contoh sambil menyebut operasi yang sedang dihitung. Jangan langsung melompat ke notasi Big-O.
3. Tutup jawaban latihan, kerjakan dua soal mudah dan satu soal menantang per bab. Periksa *alasan* di pembahasan, bukan hanya hasil akhir.
4. Saat mengajar, pakai pola **masalah → asumsi → hitungan → alasan → pengecekan dengan input kecil**. Minta peserta menjelaskan asumsi mereka sebelum memakai rumus.

Jika waktu terbatas, dahulukan Bab 1 bagian induksi dan jumlah deret; Bab 2 definisi O/Ω/Θ; Bab 3 expected value; Bab 4 loop bergantung; Bab 5 pohon rekurensi dan syarat Master; Bab 6 invariant binary search; Bab 7 stabilitas dan trade-off. Ketujuh bab saling bertumpu: tanpa penjumlahan deret sulit memahami loop dan pohon rekurensi, sedangkan tanpa asumsi input mudah salah memilih searching/sorting.

## Konvensi

- Ukuran input ditulis *n*; untuk matriks digunakan *m × n*. Basis logaritma 2 kecuali disebut lain. Mengganti basis logaritma mengubah faktor konstan, bukan kelas Θ.
- *T(n)* berarti banyak operasi dasar dalam model biaya yang dinyatakan. Big-O adalah batas atas, Ω batas bawah, Θ batas ketat. Untuk menyebut kelas yang paling informatif, panduan ini biasanya memakai Θ.
- Potongan algoritme ditulis sebagai daftar langkah atau baris berindentasi, agar nyaman dibaca di ponsel. Indeks larik dimulai dari 0 kecuali soal sumber memakai indeks 1.
- Soal berlabel **Adaptasi responsi** atau **Adaptasi UTS** disusun ulang dari tema atau angka sumber; bukan salinan ujian resmi atau jaminan akan keluar lagi.
- Beberapa bagian PDF berupa gambar tanpa lapisan teks. Panduan ini memakai bagian yang terbaca dan pengetahuan matematika yang diperiksa kembali; rujuk PDF asli ketika diagram atau potongan program tertentu diperlukan.

## Materi sumber

ZIP yang diberikan berisi `Kuliah 1–7 Analgor 2026-2027.pdf`, `LEMBAR KERJA RESPONSI PERTEMUAN 1–7 ANALGOR.pdf`, bank soal K1–K7, dan contoh UTS 2018 serta pembahasan UTS 2020–2021. Catatan ini ditulis ulang sebagai panduan belajar; PDF tidak diunggah ulang ke repositori ini. Pada pembahasan UTS 2020–2021 terdapat rekurensi dengan biaya negatif atau koefisien anak pecahan; keduanya tidak boleh langsung dipaksa ke Teorema Master standar. Pada bank soal K4, loop yang mengubah *i* menjadi *i²* dari *i = 1* tidak pernah maju. Koreksi dan alasan matematisnya dijelaskan di bab terkait.
