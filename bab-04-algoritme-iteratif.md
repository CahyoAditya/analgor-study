# Bab 4 — Panduan Responsi Pertemuan 4: Algoritme Iteratif

Lembar responsi memuat **10 soal iteratif sederhana (A)** dan **10 soal iteratif majemuk (B)**. Kita mengikuti seluruhnya sesuai kode yang tercetak. Ceritanya: catat nilai penghitung, hitung berapa kali tubuh berjalan, lalu hitung biaya baris. Jika kode tidak berhenti, jangan memaksakan rumus waktu selesai.

Latihan tambahan tersedia di [Latihan Bab 4](latihan-bab-04.md).

Sumber: *Lembar Kerja Responsi Pertemuan 4 Analisis Algoritme 2026–2027*, dari `analgor.zip` yang diberikan Sensei. Ambil $n$ bilangan bulat positif. Pembagian bilangan `int` dibulatkan ke bawah. Inisialisasi, perbandingan, dan satu pekerjaan tetap berbiaya 1. `i++`, `i--`, `i*=2`, `n=n/2` berbiaya 2, yakni hitung dan simpan. Kondisi loop dihitung sekali lagi saat gagal; `break` keluar tanpa pemeriksaan terakhir itu. Deklarasi dan input tidak dimasukkan ke $T(n)$ di bawah karena hanya menambah biaya tetap.

*Aturan penting:* Jika soal memberi pekerjaan bertanda $O(n)$ atau $O(n^2)$, itu hanya batas atas. Biaya tepatnya belum diketahui; tulis $C(n)$ untuk satu pekerjaan. Kita dapat memperoleh $\Theta$ hanya jika pekerjaan memang $\Theta$ dari kelas tersebut. Fungsi `sqrt`, `pow`, `printf`, dan `max` diasumsikan berbiaya tetap sesuai model soal. Jika biaya nyata fungsi itu dihitung, $T(n)$ persis bisa berubah.

## Contoh membaca tabel

Untuk `for(i=0; i<n; i++) { kerja; }`, nilai `i` adalah $0,1,\ldots,n-1$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | 1 | 1 |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `kerja` | 1 | $n$ | $n$ |
| **Jumlah** | | | **$5n+2$** |

Kondisi mempunyai $n+1$ pemeriksaan karena setelah `i=n-1` selesai, nilai `i=n` diperiksa dan gagal. Untuk loop bersarang, hitung frekuensi kondisi gagal pada **setiap** pemanggilan loop dalam.

## A. Iteratif sederhana

### A1. `break` membuat pembagian dua tidak terjadi

Kode memulai `i=n`, menguji `i>0`, menjalankan pekerjaan tetap, lalu `break`. Pembaruan `i=i/2` tidak tercapai. Untuk $n>0$:

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=n` | 1 | 1 | 1 |
| `i>0` | 1 | 1 | 1 |
| pekerjaan tetap | 1 | 1 | 1 |
| `break` | 1 | 1 | 1 |
| `i=i/2` | 2 | 0 | 0 |
| **Jumlah** | | | **4** |

Jadi $O(1)$. Jangan menjawab $O(\log n)$ hanya karena melihat `/2`.

### A2. `i=1; i<n; i=i*2`

Contoh $n=9$: `i` bernilai 1, 2, 4, 8. Banyak putaran $r=\lceil\log_2 n\rceil$ untuk $n\ge1$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=1` | 1 | 1 | 1 |
| `i<n` | 1 | $r+1$ | $r+1$ |
| `i=i*2` | 2 | $r$ | $2r$ |
| pekerjaan tetap | 1 | $r$ | $r$ |
| **Jumlah** | | | **$4r+2$** |

Maka $O(\log n)$ untuk input besar. Pada $n=1$, loop nol kali dan total tetap.

### A3. `while(n>0) n=n/2`

Untuk $n=13$, nilai positif yang masuk tubuh ialah 13, 6, 3, 1. Banyak putaran $r=\lfloor\log_2n\rfloor+1$. Tabelnya: kondisi `n>0` berbiaya 1 dan frekuensi $r+1$; pembaruan berbiaya 2 dan frekuensi $r$. Jadi **$T(n)=3r+1=O(\log n)$**. Variabel input `n` berubah selama program.

### A4. `i=0; i<sqrt(n); i++`

Ada $r=\lceil\sqrt n\rceil$ putaran. Misalnya $n=10$: `i=0,1,2,3`, empat putaran. Tabelnya sama seperti contoh pembuka dengan $n$ diganti $r$, sehingga **$T(n)=5r+2=O(\sqrt n)$**.

### A5. `i=n; i>1; i--`

Nilai yang diproses $n,n-1,\ldots,2$, sehingga $r=n-1$ putaran. Inisialisasi 1; kondisi $r+1$; `printf` $r$; penurunan indeks $2r$. Maka **$T(n)=4r+2=4n-2=O(n)$**. Nilai 1 hanya diperiksa sebagai kondisi gagal.

### A6. `i=2; i<n; i=pow(i,2)`

Nilai `i`: 2, 4, 16, 256, dan seterusnya. Sesudah $t$ pembaruan, nilainya $2^{2^t}$. Untuk $n>2$, banyak putaran $r=\lceil\log_2(\log_2n)\rceil$; untuk $n\le2$, $r=0$. Dengan `pow` dianggap berbiaya tetap, tabel seperti A2 memberi **$T(n)=4r+2=O(\log\log n)$** untuk $n$ besar. Nilai awal 2 penting: mulai 1 akan tetap 1 selamanya.

### A7. `i=1; i<sqrt(n); i=i*2`

Banyak putaran $r=\lceil\log_2\sqrt n\rceil=\lceil\tfrac12\log_2n\rceil$ untuk $n\ge1$. Tabel seperti A2 memberi **$T(n)=4r+2=O(\log n)$**. Faktor setengah tidak mengubah orde.

### A8. `i=2; i<n; i=i*2`, tubuh $O(n)$

Banyak putaran $r=\max(0,\lceil\log_2n\rceil-1)$. Jika biaya satu tubuh $C(n)$, **$T(n)=3r+2+rC(n)$**. Dengan $C(n)=O(n)$ diperoleh $O(n\log n)$. Jika $C(n)=\Theta(n)$, barulah hasilnya $\Theta(n\log n)$.

### A9. `i=0; i<n+n+n; i++`, tubuh $O(n^2)$

Loop berjalan $3n$ kali. Dengan biaya satu tubuh $C(n)$, tabel dasar memberi **$T(n)=9n+2+3nC(n)$**, jika seluruh evaluasi batas dianggap satu perbandingan. Maka $O(n^3)$; bila $C(n)=\Theta(n^2)$, hasil rapatnya $\Theta(n^3)$. Menghitung dua penjumlahan pada kondisi secara terpisah mengubah koefisien, bukan orde.

### A10. `i=0; i<n*n; i++`, tubuh tetap

Loop berjalan $n^2$ kali. Bila `n*n` dianggap batas yang sudah tersedia, tabel dasar memberi **$T(n)=5n^2+2=O(n^2)$**. Bila perkalian dievaluasi setiap pemeriksaan, tambahkan $n^2+1$ unit untuk perkalian itu. Kedua model berorde sama.

## B. Iteratif majemuk

### B1. Dua loop penuh

`i=0..n-1` dan, untuk tiap `i`, `j=0..n-1`. Tubuh `printf` berjalan $n^2$ kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | 1 | 1 |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j=0` | 1 | $n$ | $n$ |
| `j<n` | 1 | $n(n+1)$ | $n^2+n$ |
| `j++` | 2 | $n^2$ | $2n^2$ |
| `printf` | 1 | $n^2$ | $n^2$ |
| **Jumlah** | | | **$4n^2+5n+2$** |

Jadi $O(n^2)$. Pemeriksaan `j<n` gagal sekali pada **setiap** nilai `i`.

### B2. Loop dalam sampai akar

Untuk setiap `i=0..n-1`, `j` berjalan dari 0 selama `j<sqrt(n)`. Tulis $q=\lceil\sqrt n\rceil$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | 1 | 1 |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j=0` | 1 | $n$ | $n$ |
| `j<sqrt(n)` | 1 | $n(q+1)$ | $nq+n$ |
| `j++` | 2 | $nq$ | $2nq$ |
| pekerjaan tetap | 1 | $nq$ | $nq$ |
| **Jumlah** | | | **$4nq+5n+2$** |

Jadi $O(n\sqrt n)$. Untuk $n=10$, tubuh berjalan $10\cdot4=40$ kali.

### B3. `count` tidak diulang dari nol

Gambar menaruh `count=0` **sebelum** loop `i=0..n-1`. Di dalamnya, `while(count<i)` menaikkan `count`. Pada $n=4$, setiap $i=1,2,3$ hanya membutuhkan **satu** kenaikan; seluruh tubuh `while` berjalan $n-1$ kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `count=0`, `i=0` | 1 per baris | 1 per baris | 2 |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `count<i` | 1 | $2n-1$ | $2n-1$ |
| `sum=sum+count` | 2 | $n-1$ | $2n-2$ |
| `count++` | 2 | $n-1$ | $2n-2$ |
| **Jumlah** | | | **$9n-2$** |

Jadi $O(n)$, **bukan $O(n^2)$**. Gambar tidak menginisialisasi `sum`; nilai keluarannya dalam C tidak dapat dipercaya. Hitungan putaran berlaku bila operasi tubuh dapat dijalankan.

### B4. `c=0` di dalam loop luar

Sekarang `c` diatur nol pada setiap nilai `i`, jadi `while(c<i)` berjalan $i$ kali. Jumlahnya $q=0+1+\cdots+(n-1)=n(n-1)/2$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `c=0` sebelum loop, `i=0` | 1 per baris | 1 per baris | 2 |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `c=0` dalam loop | 1 | $n$ | $n$ |
| `c<i` | 1 | $q+n$ | $q+n$ |
| `sum=sum+c` | 2 | $q$ | $2q$ |
| `c++` | 2 | $q$ | $2q$ |
| **Jumlah** | | | **$5q+5n+3$** |

Jadi $O(n^2)$. `sum` pada gambar juga belum diinisialisasi; ini adalah hitungan frekuensi, bukan hasil penjumlahan.

### B5. Batas pangkat tiga yang sama

Loop luar `i=0; i<=pow(n,3); i++` berjalan $q=n^3+1$ kali. Kondisi `if(i<=pow(n,3))` selalu benar selama berada dalam tubuh loop, sehingga `printf` juga $q$ kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | 1 | 1 |
| syarat `for` | 1 | $q+1$ | $q+1$ |
| `i++` | 2 | $q$ | $2q$ |
| syarat `if` | 1 | $q$ | $q$ |
| `printf` | 1 | $q$ | $q$ |
| **Jumlah** | | | **$5q+2=5n^3+7$** |

Jadi $O(n^3)$. Analisis matematika ini menganggap `pow(n,3)` menghasilkan $n^3$ tepat; hasil pecahan komputer bisa bermasalah untuk angka sangat besar.

### B6. Tiga loop, tetapi `k` dimulai dari `n`

Loop `i` sepanjang $n$, loop `j` sepanjang $n^2$, dan loop `k` turun dari $n$ sampai 1. Karena itu `count=count+k` berjalan $n\cdot n^2\cdot n=n^4$ kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | 1 | 1 |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j=0` | 1 | $n$ | $n$ |
| `j<n*n` | 1 | $n^3+n$ | $n^3+n$ |
| `j++` | 2 | $n^3$ | $2n^3$ |
| `k=n` | 1 | $n^3$ | $n^3$ |
| `k>0` | 1 | $n^4+n^3$ | $n^4+n^3$ |
| `k--` | 2 | $n^4$ | $2n^4$ |
| `count=count+k` | 2 | $n^4$ | $2n^4$ |
| **Jumlah** | | | **$5n^4+5n^3+5n+2$** |

`count=0` sebelum loop menambah satu. Menghitung perkalian `n*n` pada setiap syarat secara terpisah menambah biaya berorde $n^3$, tetapi hasil tetap $O(n^4)$.

### B7. Tiga batas yang berbeda

Pada gambar, `i` mulai `n/2` sampai `n`; `j` mulai 1 selama `j+n/2<=n`; `k` mengganda dari 1 sampai `n`. Tulis $h=\lfloor n/2\rfloor$, $a=n-h+1$ (banyak `i`), $b=n-h$ (banyak `j`), dan $r=\lfloor\log_2n\rfloor+1$ (banyak `k`). Tubuh `count++` berjalan $abr$ kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=n/2` | 1 | 1 | 1 |
| `i<=n` | 1 | $a+1$ | $a+1$ |
| `i++` | 2 | $a$ | $2a$ |
| `j=1` | 1 | $a$ | $a$ |
| `j+h<=n` | 1 | $a(b+1)$ | $ab+a$ |
| `j++` | 2 | $ab$ | $2ab$ |
| `k=1` | 1 | $ab$ | $ab$ |
| `k<=n` | 1 | $ab(r+1)$ | $abr+ab$ |
| `k=k*2` | 2 | $abr$ | $2abr$ |
| `count++` | 2 | $abr$ | $2abr$ |
| **Jumlah** | | | **$5abr+5ab+5a+2$** |

`count=0` menambah 1. Karena $a,b=\Theta(n)$ dan $r=\Theta(\log n)$ untuk input besar, hasilnya $O(n^2\log n)$. Untuk $n=4$, tubuh berjalan $3\cdot2\cdot3=18$ kali.

### B8. Akar, turun satu, lalu mengganda

Loop `i=0; i<=sqrt(n); i++` berjalan $a=\lfloor\sqrt n\rfloor+1$ kali. Loop `j=n; j>=1; j--` berjalan $n$ kali pada tiap `i`. Loop `k=1; k<=n; k=k*2` berjalan $r=\lfloor\log_2n\rfloor+1$ kali pada tiap `j`. Jadi `printf` berjalan $anr$ kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | 1 | 1 |
| `i<=sqrt(n)` | 1 | $a+1$ | $a+1$ |
| `i++` | 2 | $a$ | $2a$ |
| `j=n` | 1 | $a$ | $a$ |
| `j>=1` | 1 | $a(n+1)$ | $an+a$ |
| `j--` | 2 | $an$ | $2an$ |
| `k=1` | 1 | $an$ | $an$ |
| `k<=n` | 1 | $an(r+1)$ | $anr+an$ |
| `k=k*2` | 2 | $anr$ | $2anr$ |
| `printf` | 1 | $anr$ | $anr$ |
| **Jumlah** | | | **$4anr+5an+5a+2$** |

Jadi $O(n\sqrt n\log n)$. Cek $n=4$: $3\cdot4\cdot3=36$ cetakan.

### B9. Array dengan $M$ elemen

Program menetapkan `top=arr[0]` dan `best=arr[0]`, lalu mengunjungi $M$ elemen dan menjalankan dua `max` setiap putaran. Jika setiap baris penugasan beserta `max` dianggap satu unit abstrak:

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| dua inisialisasi nilai | 1 per baris | 1 per baris | 2 |
| `i=0` | 1 | 1 | 1 |
| `i<M` | 1 | $M+1$ | $M+1$ |
| `i++` | 2 | $M$ | $2M$ |
| dua baris `max` | 1 per baris | $M$ per baris | $2M$ |
| `printf` | 1 | 1 | 1 |
| **Jumlah** | | | **$5M+5$** |

Jika `max` dan penugasan dihitung masing-masing satu, tambahkan $2M$; tetap $O(M)$. Syaratnya $M\ge1$ agar `arr[0]` ada. Kode tersebut **tidak benar untuk mencari dua nilai terbesar**: `top` diperbarui dulu, lalu `best=max(top,best)`, sehingga keduanya akhirnya sama-sama maksimum. Biaya waktu dan kebenaran hasil perlu dibedakan.

### B10. Pembaruan variabel keliru: program tidak berhenti

Gambar terakhir menulis loop `for(j=m/4; j<m/2; i+=2)`, berikutnya `for(j=0; j<2*m; i+=2)`, dan terdalam `for(k=0; j<2*m; i+=2)`. Syarat memeriksa `j`, tetapi pembaruan malah mengubah `i`. Untuk $m>0$, loop `j=0; j<2*m; i+=2` mempertahankan `j=0`, sehingga syarat selalu benar. Program tidak selesai; **$T(n)$ waktu sampai selesai dan Big-O-nya tidak terdefinisi**. Loop terdalam juga memeriksa `j` sementara tidak mengubah `j`. Variabel `m` pun tidak dideklarasikan pada potongan gambar; jika tidak disediakan dari luar, program gagal dikompilasi. Mengganti `i+=2` menjadi `j+=2` atau `k+=2` berarti menganalisis program lain.

## Ringkasan jawaban

| Nomor | Frekuensi tubuh utama | Big-O pada model soal |
| --- | --- | --- |
| A1 | 1 | $O(1)$ |
| A2 | $\lceil\log_2n\rceil$ | $O(\log n)$ |
| A3 | $\lfloor\log_2n\rfloor+1$ | $O(\log n)$ |
| A4 | $\lceil\sqrt n\rceil$ | $O(\sqrt n)$ |
| A5 | $n-1$ | $O(n)$ |
| A6 | $\lceil\log_2\log_2n\rceil$ untuk $n>2$ | $O(\log\log n)$ |
| A7 | $\lceil\tfrac12\log_2n\rceil$ | $O(\log n)$ |
| A8 | $\Theta(\log n)$ pekerjaan berbiaya $O(n)$ | $O(n\log n)$ |
| A9 | $3n$ pekerjaan berbiaya $O(n^2)$ | $O(n^3)$ |
| A10 | $n^2$ | $O(n^2)$ |
| B1 | $n^2$ | $O(n^2)$ |
| B2 | $n\lceil\sqrt n\rceil$ | $O(n\sqrt n)$ |
| B3 | $n-1$ | $O(n)$ |
| B4 | $n(n-1)/2$ | $O(n^2)$ |
| B5 | $n^3+1$ | $O(n^3)$ |
| B6 | $n^4$ | $O(n^4)$ |
| B7 | $abr$ seperti di atas | $O(n^2\log n)$ |
| B8 | $anr$ seperti di atas | $O(n\sqrt n\log n)$ |
| B9 | $M$ | $O(M)$ |
| B10 | tidak selesai untuk $m>0$ | tidak terdefinisi |

## Latihan bertingkat

1. **Mudah, adaptasi A1.** Hapus `break`; untuk $n=13$, tulis nilai `i` dan berapa kali kondisi diuji. *Cek:* $13,6,3,1$ dan lima uji.
2. **Mudah, adaptasi A4.** Untuk $n=10$, berapa kali tubuh berjalan? *Cek:* empat kali, sebab $0,1,2,3<\sqrt{10}$.
3. **Sedang, adaptasi B2.** Untuk $n=10$, hitung pekerjaan tubuh seluruhnya. *Cek:* $10\lceil\sqrt{10}\rceil=40$.
4. **Sedang, adaptasi B3–B4.** Pindahkan `count=0` dari luar ke dalam loop `i`. Mengapa jumlah tubuh berubah dari $n-1$ menjadi $n(n-1)/2$? Tulis jejak untuk $n=4$.
5. **Sulit, adaptasi B7.** Untuk $n=4$, hitung banyak `count++` dan banyak pemeriksaan kondisi `k<=n`. *Cek:* 18 kenaikan dan $3\cdot2\cdot(3+1)=24$ pemeriksaan.
6. **Sulit, adaptasi B10.** Sebutkan variabel yang diperiksa dan yang diperbarui pada tiap loop bermasalah. Jelaskan mengapa loop tidak maju menuju kondisi berhenti.

Urutan yang aman untuk soal baru: *catat nilai indeks → periksa apakah indeks berubah → hitung tubuh dan uji kondisi → susun tabel Cost–Frequency–Total → baru ambil suku dominan*. Jika batas loop dalam bergantung pada indeks luar, jumlahkan frekuensinya menurut tiap nilai luar.
