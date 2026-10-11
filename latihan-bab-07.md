# Latihan Bab 7 — Pengurutan

Latihan ini **adaptasi** dari *Lembar Kerja Responsi Pertemuan 7*. Jawaban nomor asli ada di [Bab 7](bab-07-pengurutan.md). Gunakan indeks mulai 0. Untuk quick sort, tulis dahulu skema partisi dan aturan nilai yang sama; hasil array sementara bergantung pada aturan itu.

## Tingkat 1 — jejak array

1. **Adaptasi A(a).** Jalankan dua iterasi pertama insertion sort pada `[9,5,6,3,3,8,1]`. Sebutkan indeks dan nilai kunci setiap kali.
2. **Adaptasi A(b).** Merge `[3ₐ,5,6,9]` dan `[1,3ᵦ,8]` secara stabil. Tulis urutan elemen yang diambil.
3. **Adaptasi A(c).** Dari array asli, pilih pivot indeks tengah 3, pindahkan ke ujung, lalu lakukan partisi Lomuto dengan syarat `nilai <= pivot`. Tulis array setelah memindahkan pivot, setelah nilai 1, setelah nilai 3 lain, dan setelah pivot ditempatkan.

## Tingkat 2 — alasan algoritme

4. **Adaptasi A(a).** Mengapa insertion sort pada array yang sudah terurut memerlukan $\Theta(n)$, sedangkan pada array terbalik $\Theta(n^2)$?
5. **Adaptasi A(b).** Dua record bernilai 3 memiliki identitas `3ₐ` dan `3ᵦ`, dengan `3ₐ` lebih awal di input. Aturan perbandingan apa yang menjaga urutannya saat merge?
6. **Adaptasi B(a).** Urutkan `(timestamp,userId,amount)` berdasarkan dua kunci pertama. Jelaskan apa yang harus terjadi ketika kedua kunci sama tetapi `amount` berbeda.

## Tingkat 3 — pilih strategi

7. **Adaptasi B(b).** Dengan $K=3$ dan skor `8,1,5,9,2`, jejak himpunan kandidat setelah heap penuh dan setiap skor berikutnya. Apa keluaran menurunnya?
8. **Adaptasi B(b).** Untuk $K\ll n$, tulis batas waktu dan ruang min-heap Top-K termasuk pengurutan hasil. Kapan full sort masuk akal?
9. **Transfer konsep.** Beri contoh tiga record yang membuktikan selection sort dengan pertukaran langsung dapat tidak stabil.

## Kunci dan alasan

1. $i=1$, kunci 5: `[5,9,6,3,3,8,1]`. $i=2$, kunci 6: `[5,6,9,3,3,8,1]`.
2. Ambil **1, 3ₐ, 3ᵦ, 5, 6, 8, 9**. Saat kedua kepala bernilai 3, ambil kiri lebih dahulu.
3. Setelah pivot ke ujung: `[9,5,6,1,3,8,3]`; setelah 1: `[1,5,6,9,3,8,3]`; setelah 3 lain: `[1,3,6,9,5,8,3]`; akhir: **`[1,3,3,9,5,8,6]`**, pivot indeks 2, bagian kiri `[0,1]`, kanan `[3,6]`.
4. Sudah terurut: tidak ada pergeseran dan tiap kunci diperiksa sekali, jadi $\Theta(n)$. Terbalik: pergeseran $1+2+\cdots+(n-1)=\Theta(n^2)$.
5. Pakai **`kiri <= kanan`** saat memilih elemen berikutnya. Nilai sama dari sisi kiri tetap mendahului sisi kanan.
6. Pertahankan urutan asal kedua record itu; inilah stabilitas terhadap pasangan kunci yang sama. `amount` bukan kunci yang diminta.
7. Setelah `8,1,5`: `{1,5,8}`; setelah 9: `{5,8,9}`; setelah 2: tetap `{5,8,9}`. Keluaran **`9,8,5`**.
8. Batas waktu **$O(n\log K+K\log K)$**, ruang **$O(K)$**. Full sort wajar bila seluruh atau hampir seluruh urutan diperlukan, banyak permintaan berbeda akan dijawab, atau pengukuran nyata lebih menguntungkan.
9. `[2ₐ,2ᵦ,1]` menjadi `[1,2ᵦ,2ₐ]` setelah minimum ditukar ke depan. Dua record kunci 2 berubah urutan.
