# Latihan Bab 4 — Algoritme Iteratif

Soal ini adalah **adaptasi latihan** dari *Lembar Kerja Responsi Pertemuan 4 Analisis Algoritme 2026–2027*. Materi lengkap dan jawaban seluruh nomor asli ada di [Bab 4](bab-04-algoritme-iteratif.md). Pada setiap soal, anggap $n$ bilangan bulat positif, pembagian `int` dibulatkan ke bawah, perbandingan dan pekerjaan sederhana berbiaya 1, sedangkan `++`, `--`, perkalian atau pembagian yang sekaligus menugaskan hasil berbiaya 2. Uji kondisi terakhir yang gagal tetap dihitung.

Bayangkan Sensei mengamati penghitung pada program pengolahan daftar peserta. Jangan menebak kelas pertumbuhan dari jumlah loop di layar. Tulis nilai yang dilewati, hitung frekuensi, lalu susun tabel **Code–Cost–Frequency–Total**.

## Tingkat 1: satu penghitung

1. **Adaptasi A1.** `i=n; while(i>0) { kerja; break; i=i/2; }`. Untuk $n=16$, berapa kali `kerja`, kondisi, dan pembaruan `i` berjalan? Buat tabel biaya. Apa Big-O-nya?
2. **Adaptasi A2.** `for(i=1; i<17; i=i*2) kerja;`. Daftarkan nilai `i`, lalu hitung jumlah uji kondisi termasuk yang gagal. Ulangi dengan batas umum $n$.
3. **Adaptasi A3.** `while(n>0) n=n/2;` untuk $n=13$. Tuliskan nilai `n` sebelum setiap pembagian. Mengapa frekuensinya $\lfloor\log_2n\rfloor+1$ dan bukan tepat $\log_2n$?
4. **Adaptasi A4.** `for(i=0; i<sqrt(n); i++) kerja;` untuk $n=10$. Berapa putaran? Apa yang berubah jika syaratnya `i<=sqrt(n)`?

## Tingkat 2: biaya per pekerjaan

5. **Adaptasi A8.** Loop `i=2; i<n; i=i*2` memanggil pekerjaan yang memeriksa seluruh $n$ peserta sekali. Tulis $T(n)$ dengan $r=\max(0,\lceil\log_2n\rceil-1)$ dan biaya pekerjaan $C(n)=n$. Jelaskan mengapa hasilnya $\Theta(n\log n)$ untuk $n$ besar.
6. **Adaptasi A9.** Loop berjalan $3n$ kali. Pekerjaan di dalamnya hanya diketahui $O(n^2)$. Tuliskan batas atas waktu dan jelaskan mengapa label itu saja belum membuktikan batas bawah $\Omega(n^3)$.

## Tingkat 3: loop majemuk

7. **Adaptasi B1–B2.** Bandingkan dua loop dalam berikut untuk tiap `i=0..n-1`: (a) `j=0..n-1`, (b) `j=0` selama `j<sqrt(n)`. Untuk $n=10$, berapa kali pekerjaan tubuh masing-masing dijalankan? Tulis frekuensi pemeriksaan `j`.
8. **Adaptasi B3–B4.** Pada program pertama, `count=0` diletakkan sebelum `for(i=0;i<n;i++)`; pada program kedua, `count=0` diletakkan di awal tiap putaran `i`. Keduanya mempunyai `while(count<i) count++`. Buat jejak untuk $n=4$ dan turunkan jumlah pembaruan untuk $n$ umum.
9. **Adaptasi B7.** `i` berjalan dari $\lfloor n/2\rfloor$ sampai $n$; tiap `i`, `j` berjalan dari 1 sampai $n-\lfloor n/2\rfloor$; tiap `j`, `k` mengganda dari 1 sampai $n$. Hitung banyak pekerjaan tubuh dan banyak uji kondisi `k` untuk $n=4$ dan untuk $n$ umum.
10. **Adaptasi B8.** `i=0` selama `i<=sqrt(n)`; `j` turun dari $n$ sampai 1; `k` mengganda dari 1 selama `k<=n`. Untuk $n=4$, hitung frekuensi tubuh dan uji `k`. Lalu tentukan Big-O.
11. **Adaptasi B9.** Array mempunyai $M$ elemen. Program mengunjungi tiap elemen sekali dan melakukan dua perbandingan tetap. Tulis frekuensi operasi. Jelaskan mengapa $O(M)$ tidak otomatis berarti hasil program benar.
12. **Adaptasi B10.** Perhatikan `for(j=0; j<2*m; i+=2)` untuk $m>0$. Nilai apa yang diperiksa, nilai apa yang diubah, dan mengapa loop tidak selesai? Usulkan pembetulan *sebagai program baru*, lalu hitung banyak iterasinya bila mulai `j=0` dan memakai `j+=2`.

## Kunci dan alasan

1. `kerja` sekali, syarat sekali, pembaruan nol. `break` langsung keluar, sehingga $O(1)$.
2. Nilai 1, 2, 4, 8, 16: lima pekerjaan dan enam uji. Untuk $n$, pekerjaan $\lceil\log_2n\rceil$ dan uji satu lebih banyak.
3. 13, 6, 3, 1: empat pembagian dan lima uji. Pembulatan ke bawah membuat bilangan bulat menjadi nol setelah nilai 1 dibagi 2.
4. Nilai 0, 1, 2, 3: empat putaran. Dengan `<=`, tetap empat untuk $n=10$ karena $\sqrt{10}$ bukan bulat; bila $n=9$, `<=` menambah nilai 3 sehingga menjadi empat, sedangkan `<` hanya tiga.
5. Inisialisasi 1, uji $r+1$, pembaruan $2r$, pekerjaan $nr$. Jadi $T(n)=3r+2+nr$, dan $r=\Theta(\log n)$ untuk input besar.
6. $3n$ pekerjaan masing-masing paling mahal $O(n^2)$ memberi $O(n^3)$. Pekerjaan itu bisa saja berbiaya konstan, sehingga tidak ada jaminan $\Omega(n^3)$.
7. (a) 100 pekerjaan dan $10(10+1)=110$ uji `j`; (b) $10\lceil\sqrt{10}\rceil=40$ pekerjaan dan $10(4+1)=50$ uji.
8. Penghitung di luar: frekuensi tubuh per nilai `i` adalah 0, 1, 1, 1, total $n-1$. Penghitung di dalam: 0, 1, 2, 3, total $n(n-1)/2$.
9. Untuk $n=4$, jumlah `i` ialah 3, `j` ialah 2, `k` ialah 3: tubuh 18 dan uji `k` $3\cdot2\cdot4=24$. Secara umum, tulis $a=n-\lfloor n/2\rfloor+1$, $b=n-\lfloor n/2\rfloor$, $r=\lfloor\log_2n\rfloor+1$; hasilnya $abr$ tubuh dan $ab(r+1)$ uji.
10. Untuk $n=4$, `i` tiga kali, `j` empat kali, `k` tiga kali: 36 tubuh dan $3\cdot4\cdot4=48$ uji `k`. Secara umum $O(n\sqrt n\log n)$.
11. Elemen dikunjungi $M$ kali, dua perbandingan per elemen berarti $2M$ perbandingan. Kompleksitas menghitung pekerjaan; kebenaran bergantung pada cara hasil disimpan.
12. Syarat memeriksa `j`, pembaruan mengubah `i`; `j` tetap 0 dan $0<2m$ selalu benar. Dengan `j+=2`, nilai `j=0,2,\ldots,2m-2`, jadi tepat $m$ putaran bila $m$ bilangan bulat positif.
