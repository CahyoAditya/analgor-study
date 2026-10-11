# Latihan Bab 5 — Pohon Rekursi dan Master Theorem

Soal di bawah adalah **adaptasi**, bukan salinan soal responsi. Rujuk jawaban nomor asli di [Bab 5](bab-05-algoritme-rekursif.md). Anggap $T(1)=1$ dan ukuran input pangkat pembagi bila diperlukan. Pada tiap soal, tulis jumlah simpul, ukuran submasalah, dan biaya *setiap tingkat* sebelum memakai rumus umum.

## Tingkat 1 — lihat bentuk pohon

1. **Adaptasi A2.** Untuk $T(n)=3T(n/3)+n$, buat tabel tingkat pada $n=9$ sampai daun. Berapa biaya tepatnya?
2. **Adaptasi A1.** Untuk $T(n)=2T(n/4)+n$, buat tabel pada $n=16$. Mengapa tingkat kedua lebih murah daripada akar?
3. **Adaptasi gambar Sensei.** Untuk $T(n)=2T(n/2)+c$ dengan $T(1)=c$, buat tabel $n=8$. Mengapa biaya tiap anak tidak menjadi $c/2$?

## Tingkat 2 — bandingkan deret

4. **Adaptasi A3.** Untuk $T(n)=4T(n/2)+n$, hitung jumlah daun pada $n=8$ dan total biaya dengan $T(1)=1$. Tunjukkan asal $n^2$.
5. **Adaptasi A4.** Untuk $T(n)=7T(n/8)+n$, hitung biaya tingkat 0, 1, dan daun pada $n=64$. Jelaskan mengapa akar mendominasi.
6. **Adaptasi B1 dan B3.** Bandingkan $2T(n/2)+n\log_2n$ dan $9T(n/3)+n^2$. Tulis $a,b,f(n),n^{\log_ba}$ serta kasus Master masing-masing.

## Tingkat 3 — baca biaya algoritme

7. **Adaptasi C1.** TriMergeSort membagi 27 elemen menjadi tiga bagian sama besar dan menggabung secara linear. Berapa biaya gabung total di tiap tingkat jika biaya gabung persis satu langkah per elemen? Apa yang belum diketahui dari nama `MERGE3_IN_PLACE`?
8. **Adaptasi C2.** QuadHistogram pada 16 nilai membuat vektor panjang $K=5$ di tiap daun dan menjumlahkan vektor di tiap simpul dalam. Hitung jumlah daun dan simpul dalam; nyatakan biaya dalam kelipatan $K$.
9. **Transfer konsep.** Mengapa Master Theorem standar tidak langsung berlaku untuk $T(n)=T(n-1)+n$? Selesaikan dengan jumlah $1+2+\cdots+n$.

## Kunci dan alasan

1. Biaya tingkat dalam 9 dan 9; sembilan daun berbiaya 9. Total **27**. Secara umum ada $\log_3n$ tingkat dalam, masing-masing berbiaya $n$, serta $n$ daun.
2. Akar 16, dua anak ukuran 4 total 8, empat daun total 4. Total **28**. Tingkat anak berbiaya $2\cdot(16/4)=8$, yakni setengah biaya akar.
3. Biaya per tingkat $c,2c,4c,8c$; total **$15c$**. Suku $+c$ melekat pada *setiap* panggilan, tanpa bergantung pada ukuran anak. Hanya tinggi pohonnya yang $\log_2n$.
4. Biaya tingkat dalam 8, 16, 32; daun $4^3=64$. Total **120**. Pada $n$ umum, $4^{\log_2n}=n^2$ daun.
5. Akar 64, tujuh anak ukuran 8 total 56, dan 49 daun total 49. Total **169**. Rasio biaya tingkat dalam $7/8<1$, sehingga jumlah seluruh tingkat dibatasi kelipatan tetap dari akar.
6. Pertama: $(a,b,f,n^{\log_ba})=(2,2,n\log n,n)$, kasus 2 dengan satu log tambahan, hasil $\Theta(n\log^2n)$. Kedua: $(9,3,n^2,n^2)$, kasus 2 tanpa log awal, hasil $\Theta(n^2\log n)$.
7. Biaya gabung tingkat dalam **27, 27, 27** pada ukuran 27, 9, dan 3; 27 daun adalah kasus dasar. Total **$81$** bila setiap daun juga berbiaya 1. Nama fungsi tidak memastikan kebutuhan buffer maupun stabilitas penggabungan.
8. Ada **16 daun** dan $(16-1)/3=5$ simpul dalam. Jika masing-masing pembentukan dan penjumlahan vektor dihitung $K$ langkah, total **$(16+5)K=21K=105$** langkah. Koefisien aktual `ADD4` dapat berbeda, tetapi orde tetap $\Theta(nK)$.
9. Ukurannya turun satu, bukan dibagi konstanta. Membuka relasi memberi $n+(n-1)+\cdots+1=n(n+1)/2$, sehingga $\Theta(n^2)$ bila $T(0)$ konstan.
