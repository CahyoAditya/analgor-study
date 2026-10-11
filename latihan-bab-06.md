# Latihan Bab 6 — Pemangkatan Modulo dan Pencarian

Latihan ini **adaptasi** dari *Lembar Kerja Responsi Pertemuan 6*. Pembahasan nomor asli ada di [Bab 6](bab-06-pencarian.md). Gunakan $m>0$ untuk modulo dan indeks matriks mulai 0. Jelaskan alasan tiap langkah sebelum menulis orde waktu.

## Tingkat 1 — ikuti nilai

1. **Adaptasi A1–A2.** Hitung $2^5\bmod7$ dengan mengalikan dahulu lalu modulo di akhir, kemudian dengan modulo di setiap langkah. Tulis semua nilai sementara.
2. **Adaptasi A3.** Hitung $3^{13}\bmod7$ dengan pemangkatan biner. Tulis `(hasil,basis,sisa)` setelah setiap putaran.
3. **Adaptasi B.** Cari 9 pada `[[1,3,5],[7,9,11]]` dengan array virtual. Tulis posisi datar yang diperiksa dan pemetaan baris-kolomnya.

## Tingkat 2 — uji syarat

4. **Adaptasi B.** Apakah `[[2,1],[3,4]]` boleh dicari dengan binary search virtual bila satu-satunya syarat yang diberikan ialah elemen terakhir baris pertama $\le$ elemen pertama baris kedua? Tunjukkan letak masalahnya.
5. **Adaptasi C.** Pada matriks `[[1,2,3],[4,5,6],[7,8,9]]`, hitung jumlah keempat jendela kontigu $2\times2$ dan pilih maksimum.
6. **Adaptasi C.** Untuk matriks $n\times n$ dengan nilai boleh negatif, tulis rumus jumlah calon setelah membuang baris $r$ dan kolom $c$. Mengapa sel $A[r][c]$ harus ditambah kembali?

## Tingkat 3 — pertanggungjawabkan kompleksitas

7. **Adaptasi A.** Mengapa $n$ perkalian besar pada metode pertama dan $n$ perkalian modular pada metode kedua tidak selalu sama lama di komputer, walaupun keduanya $\Theta(n)$ dalam model biaya satuan?
8. **Adaptasi B.** Bila matriks berisi $m$ baris dan $n$ kolom serta urutan totalnya terjamin, berapa pembandingan kasus terburuk untuk binary search secara orde? Apa yang terjadi jika salah satu dimensi nol?
9. **Adaptasi C.** Bandingkan banyak calon submatriks $(n-1)\times(n-1)$ untuk tafsir kontigu dan tafsir bebas memilih baris serta kolom. Mengapa keduanya tetap dapat diselesaikan dalam $\Theta(n^2)$ waktu?

## Kunci dan alasan

1. Tanpa modulo: $2,4,8,16,32$, lalu $32\bmod7=4$. Dengan modulo: $2,4,1,2,4$. Kedua cara memberi **4**.
2. Dari `(1,3,13)`, berturut-turut `(3,2,6)`, `(3,4,3)`, `(5,2,1)`, `(3,4,0)`. Hasil **3**.
3. $p=3$ menunjuk `(1,0)` bernilai 7; $p=5$ menunjuk `(1,2)` bernilai 11; $p=4$ menunjuk `(1,1)` bernilai **9**.
4. **Belum boleh.** Hubungan $1\le3$ antarbaris benar, tetapi baris pertama `[2,1]` sendiri tidak terurut. Array virtual `[2,1,3,4]` tidak monoton.
5. Kiri atas **12**, kanan atas **16**, kiri bawah **24**, kanan bawah **28**. Maksimum **28**.
6. **$S-R_r-C_c+A[r][c]$**. Sel persilangan masuk ke jumlah baris dan kolom sehingga terkurangi dua kali, padahal hanya perlu dibuang sekali.
7. Bilangan $a^i$ pada metode pertama terus membesar, sehingga biaya perkalian serta ruang meningkat. Pada metode kedua, sisa dibatasi kurang dari $m$, walaupun hasil kali dua sisa tetap perlu ditangani dengan aman.
8. **$O(\log(mn))$** perbandingan pada kasus terburuk untuk $mn>0$; bila dimensi nol, tidak ada elemen dan pencarian langsung gagal dalam $O(1)$.
9. Kontigu: **4** calon, yakni dua pilihan posisi tiap dimensi. Bebas: **$n^2$** calon, yakni pilihan satu baris dan satu kolom yang dibuang. Membaca semua $n^2$ elemen saja memerlukan $\Theta(n^2)$; setelah jumlah baris/kolom disiapkan, setiap calon dapat dihitung dalam $O(1)$.
