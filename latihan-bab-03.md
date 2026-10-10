# Latihan Bab 3 — Responsi Pertemuan 3

Bacaan pendamping: [Bab 3](bab-03-kasus-analisis.md). Coba soal lebih dahulu, lalu periksa pembahasan. Setiap soal sudah memuat konteks, syarat, dan asalnya. “Adaptasi” berarti angka atau susunan soal sumber diubah; “soal baru” berarti dibuat untuk latihan ini. Lembar sumber berasal dari *Lembar Kerja Responsi Pertemuan 3 Analgor*, semester ganjil 2026–2027, halaman 1–3.

**Aturan biaya untuk soal berkode:** penugasan dan perbandingan sederhana berbiaya 1; `++`, `+=`, `*=`, dan pembagian lalu penugasan berbiaya 2; operasi tetap berbiaya 1. Kondisi loop diperiksa sekali lagi ketika gagal. Pembagian indeks bilangan bulat dibulatkan ke bawah. Bila satu kondisi memuat perkalian dan perbandingan atau modulo dan perbandingan, biayanya 2. Anggap ekspresi kondisi dihitung ulang setiap pemeriksaan. Gunakan tabel **Code–Cost–Frequency–Total** pada soal yang memintanya.

## Soal

### 1. Atap untuk fungsi linear

*Tingkat: Mudah. Asal: Soal baru untuk melatih definisi pada responsi 3 nomor 1.*

**Soal lengkap.** Sebuah program mempunyai biaya $T(n)=4n+7$ untuk bilangan bulat $n\ge1$. Buktikan $T(n)\in O(n)$ dengan memberi angka $c$ dan $n_0$ yang memenuhi definisi. Tentukan juga apakah $T(n)\in O(n^2)$ benar.

### 2. Klaim yang dibantah

*Tingkat: Mudah. Asal: Adaptasi responsi 3 nomor 1a(2); koefisien diubah.*

**Soal lengkap.** Untuk $n\ge1$, biaya sebuah program adalah $T(n)=3n^3+4n^2+1$. Tentukan apakah $T(n)\in O(n^2)$. Jangan hanya menyebut suku dominan; gunakan definisi Big-O untuk membuktikan keputusan.

### 3. Jumlah bilangan genap

*Tingkat: Sedang. Asal: Adaptasi responsi 3 nomor 1b(2); suku tambahan diubah.*

**Soal lengkap.** Ambil $n$ bilangan genap positif. Tentukan Big-O yang rapat untuk $F(n)=2+4+6+\cdots+n+2n^2$. Turunkan jumlah deretnya dan tunjukkan konstanta batas atas serta batas bawah.

### 4. Model kubik pada ukuran baru

*Tingkat: Mudah. Asal: Adaptasi responsi 3 nomor 2; angka 50, 400, dan 0,5 detik diganti.*

**Soal lengkap.** Waktu tepat sebuah model adalah $T(n)=cn^3$ detik dengan $c$ tetap. Pada mesin yang sama, 20 item memerlukan 0,25 detik. Berapa waktu perkiraan untuk 80 item? Tunjukkan perbandingan ukuran dan waktu.

### 5. Dua algoritme dan batas sistem

*Tingkat: Sedang. Asal: Adaptasi responsi 3 nomor 3; kedua koefisien dan batas sistem diganti.*

**Soal lengkap.** Sistem menangani bilangan bulat $1\le n\le10^6$. Waktu A adalah $T_A(n)=0{,}25n\log_2n$ milidetik dan B adalah $T_B(n)=4n$ milidetik. Cari titik waktu sama; jelaskan rentang A lebih cepat dan B lebih cepat; pilih yang lebih cepat pada $n=10^6$.

### 6. Tiga model dari satu pengukuran

*Tingkat: Sedang. Asal: Adaptasi responsi 3 nomor 4; ukuran awal, ukuran akhir, dan waktu diganti.*

**Soal lengkap.** Tiga program P, Q, R masing-masing memerlukan 2 detik pada 16 item. Asumsikan waktu tepatnya berbentuk $c_Pn^3$, $c_Qn^2$, dan $c_Rn\log_2n$ dengan konstanta tetap. Perkirakan waktu ketiganya pada 64 item. Mengapa label Big-O saja tanpa asumsi bentuk tepat tidak cukup untuk memperoleh tiga angka waktu?

### 7. Loop pembagian sederhana

*Tingkat: Mudah. Asal: Adaptasi responsi 3 nomor 6a; kondisi akhir diubah menjadi `i > 1`.*

**Soal lengkap.** Untuk $n\ge1$, jalankan `i=n; while (i>1) { i=floor(i/2); }`. Dengan aturan biaya di awal dokumen, buat tabel Code–Cost–Frequency–Total, cari $T(n)$, dan hitung $T(8)$. Jelaskan mengapa jumlah putaran berbeda dari loop dengan kondisi `i > 0`.

### 8. Dua loop dengan langkah dua

*Tingkat: Sedang. Asal: Soal baru yang mengembangkan responsi 3 nomor 6b dan aturan langkah `+= 2` dari Bab 2.*

**Soal lengkap.** Untuk $n\ge1$, jalankan `for (i=0; i<n; i++) { for (j=0; j<n; j+=2) { operasi O(1); } }`. Buat tabel Code–Cost–Frequency–Total untuk semua baris. Nyatakan $T(n)$ dengan $b=\lceil n/2\rceil$, tentukan kelas $\Theta$, dan cek frekuensi badan untuk $n=5$.

### 9. Loop pembagian yang dimulai ulang

*Tingkat: Sedang. Asal: Adaptasi responsi 3 nomor 6c; ukuran kecil untuk cek ditambahkan.*

**Soal lengkap.** Untuk $n\ge1$, jalankan `for (i=1; i<=n; i++) { j=i; while (j>0) { j=floor(j/2); } }`. Buat tabel Code–Cost–Frequency–Total. Tulis rumus $T(n)$ dengan $L=\sum_{i=1}^n(\lfloor\log_2i\rfloor+1)$, lalu hitung $T(4)$ dan kelas $\Theta$.

### 10. Tiga loop dengan panjang yang berubah

*Tingkat: Sulit. Asal: Adaptasi responsi 3 nomor 5b dan 6e; ditambah pemeriksaan pada $n=2$.*

**Soal lengkap.** Untuk $n\ge1$, jalankan `i=1; while(i<=n) { j=1; while(j<=i) { k=1; while(k<=j) { k*=2; } j++; } i*=2; }`. Buat tabel Code–Cost–Frequency–Total. Nyatakan $T(n)$ memakai $a=\lfloor\log_2n\rfloor+1$, $J=2^a-1$, dan jumlah putaran $k$ yang didefinisikan sendiri. Hitung $T(2)$ dan kelas $\Theta$.

### 11. Kelipatan yang lolos kondisi

*Tingkat: Sulit. Asal: Adaptasi responsi 3 nomor 6d; batas $j\le i^2$ diubah menjadi $j\le2i$.*

**Soal lengkap.** Untuk $n\ge1$, jalankan `for(i=1;i<=n;i++) { for(j=1;j<=2*i;j++) { if(j%i==0) { for(k=1;k<=j;k++) { operasi O(1); } } } }`. Biaya kondisi `j<=2*i` dan `j%i==0` masing-masing 2. Buat tabel Code–Cost–Frequency–Total dengan $M=\sum_{i=1}^ni$ untuk jumlah putaran $j$ dan $K=\sum_{i=1}^n3i$ untuk jumlah putaran $k$. Cari $T(n)$ dan kelas $\Theta$.

### 12. Mengapa asumsi pembagian penting?

*Tingkat: Sedang. Asal: Soal baru untuk memperjelas responsi 3 nomor 6a.*

**Soal lengkap.** Perhatikan `i=3; while(i>0) { i=i/2; }`. Jelaskan hasil bila `i/2` memakai pembagian bilangan bulat ke bawah dan bila memakai bilangan riil tanpa pembulatan. Apakah $T(3)$ yang sama dapat diberikan untuk keduanya? Gunakan tabel biaya yang sama seperti latihan lain untuk kasus pembagian bulat.

## Pembahasan

### 1. Atap untuk fungsi linear

Untuk $n\ge1$, $7\le7n$, maka $4n+7\le11n$. Pilih $c=11$ dan $n_0=1$. Klaim $O(n^2)$ juga benar: $4n+7\le11n\le11n^2$. Kelas rapatnya $\Theta(n)$, tetapi definisi Big-O membolehkan batas atas yang lebih longgar.

### 2. Klaim yang dibantah

Andaikan $3n^3+4n^2+1\le cn^2$ untuk semua $n$ besar. Pembagian dengan $n^2>0$ memberi $3n+4+1/n^2\le c$. Sisi kiri terus bertambah saat $n$ naik, sehingga memilih $n>c/3$ yang cukup besar membantahnya. Jadi $T(n)\notin O(n^2)$.

### 3. Jumlah bilangan genap

Ada $n/2$ suku: $2+4+\cdots+n=2(1+\cdots+n/2)=\frac{n^2}{4}+\frac n2$. Maka $F(n)=\frac94n^2+\frac12n$. Untuk $n\ge2$, $F(n)\le\frac{11}{4}n^2$ karena $n\le n^2$. Sementara itu $F(n)\ge\frac94n^2$. Dua batas ini membuktikan $F(n)\in\Theta(n^2)$; salah satu pilihan konstanta ialah $c_{atas}=11/4$, $c_{bawah}=9/4$, $n_0=2$ pada $n$ genap.

### 4. Model kubik pada ukuran baru

Rasio ukuran $80/20=4$. Rasio waktu $4^3=64$. Jadi $T(80)=0{,}25\times64=16$ detik. Faktor $c$ saling membatalkan dalam $T(80)/T(20)$.

### 5. Dua algoritme dan batas sistem

Samakan $0{,}25n\log_2n=4n$. Karena $n>0$, bagi dengan $0{,}25n$: $\log_2n=16$, sehingga titiknya $n=2^{16}=65.536$. A lebih cepat untuk $1\le n<65.536$; keduanya sama pada 65.536; B lebih cepat di atas itu. Karena $10^6>65.536$, B lebih cepat pada batas sistem. Pemeriksaan: $\log_2 10^6\approx19{,}93$, sehingga faktor waktu A $0{,}25\times19{,}93\approx4{,}98$ per $n$, lebih besar dari 4 per $n$ milik B.

### 6. Tiga model dari satu pengukuran

Ukuran bertambah $64/16=4$ kali. P memerlukan $2\times4^3=128$ detik; Q $2\times4^2=32$ detik. Untuk R, $\log_2 16=4$ dan $\log_2 64=6$, sehingga faktornya $4\times6/4=6$ dan waktunya $2\times6=12$ detik. Label Big-O memberi batas atas pertumbuhan untuk input besar; ia tidak memberi persamaan waktu tepat, konstanta, atau biaya tambahan lain. Angka di sini bergantung pada asumsi model tepat pada soal.

### 7. Loop pembagian sederhana

Untuk $n\ge1$, banyak putaran adalah $m=\lfloor\log_2n\rfloor$, sebab nilai 1 **tidak** masuk badan loop. Pada $n=8$, nilai yang masuk badan ialah 8, 4, 2: tiga putaran.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=n` | 1 | $1$ | $1$ |
| `i>1` | 1 | $m+1$ | $m+1$ |
| `i=floor(i/2)` | 2 | $m$ | $2m$ |
| **Jumlah** | | | **$T(n)=3m+2$** |

$T(8)=3(3)+2=11$. Jika syaratnya `i>0`, nilai 1 masih masuk dan ada satu putaran tambahan, sehingga jumlahnya $\lfloor\log_2n\rfloor+1$.

### 8. Dua loop dengan langkah dua

Nilai $j$ adalah $0,2,4,\ldots<n$, sebanyak $b=\lceil n/2\rceil$ pada setiap nilai $i$. Langkah `j+=2` tetap berbiaya 2; angka dua di sini mengubah frekuensi, bukan biaya operasi aritmetika-plus-penugasannya.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=0` | 1 | $1$ | $1$ |
| `i<n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j=0` | 1 | $n$ | $n$ |
| `j<n` | 1 | $n(b+1)$ | $nb+n$ |
| `j+=2` | 2 | $nb$ | $2nb$ |
| Operasi tetap | 1 | $nb$ | $nb$ |
| **Jumlah** | | | **$T(n)=4nb+5n+2=\Theta(n^2)$** |

Untuk $n=5$, $j$ bernilai 0, 2, 4, jadi $b=3$ dan badan berjalan $5\times3=15$ kali.

### 9. Loop pembagian yang dimulai ulang

Untuk tiap $i$, badan `while` berjalan $h(i)=\lfloor\log_2i\rfloor+1$ kali. Karena `j=i` dikerjakan lagi pada tiap putaran luar, pemeriksaan `j>0` berjumlah $L+n$, bukan $L+1$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=1` | 1 | $1$ | $1$ |
| `i<=n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j=i` | 1 | $n$ | $n$ |
| `j>0` | 1 | $L+n$ | $L+n$ |
| `j=floor(j/2)` | 2 | $L$ | $2L$ |
| **Jumlah** | | | **$T(n)=3L+5n+2$** |

Pada $n=4$, $L=1+2+2+3=8$, jadi $T(4)=24+20+2=46$. Karena $L=\Theta(n\log n)$, kelas biayanya $\Theta(n\log n)$.

### 10. Tiga loop dengan panjang yang berubah

Definisikan $H=\sum_{t=0}^{a-1}\sum_{j=1}^{2^t}(\lfloor\log_2j\rfloor+1)$. Nilai $i$ adalah $1,2,4,\ldots\le n$; $J$ menghitung seluruh nilai $j$; $H$ menghitung seluruh nilai $k$ di semua pengulangan.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=1` | 1 | $1$ | $1$ |
| `i<=n` | 1 | $a+1$ | $a+1$ |
| `i*=2` | 2 | $a$ | $2a$ |
| `j=1` | 1 | $a$ | $a$ |
| `j<=i` | 1 | $J+a$ | $J+a$ |
| `j++` | 2 | $J$ | $2J$ |
| `k=1` | 1 | $J$ | $J$ |
| `k<=j` | 1 | $H+J$ | $H+J$ |
| `k*=2` | 2 | $H$ | $2H$ |
| **Jumlah** | | | **$T(n)=2+5a+5J+3H$** |

Pada $n=2$, $a=2$, $J=1+2=3$, dan $H=1+(1+2)=4$. Jadi $T(2)=2+10+15+12=39$. Karena $J=\Theta(n)$ dan $H=\Theta(n\log n)$, hasilnya $\Theta(n\log n)$.

### 11. Kelipatan yang lolos kondisi

Untuk tiap $i$, $j$ mengambil $1,\ldots,2i$: total $2i$ putaran. Yang habis dibagi $i$ hanya $j=i$ dan $j=2i$: dua kondisi benar. Jadi inisialisasi `k=1` ada $2n$ kali. Operasi terdalam per $i$ ialah $i+2i=3i$, sehingga jumlahnya $K=3M$. Jumlah seluruh putaran $j$ ialah $2M$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=1` | 1 | $1$ | $1$ |
| `i<=n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j=1` | 1 | $n$ | $n$ |
| `j<=2*i` | 2 | $2M+n$ | $4M+2n$ |
| `j++` | 2 | $2M$ | $4M$ |
| `j%i==0` | 2 | $2M$ | $4M$ |
| `k=1` | 1 | $2n$ | $2n$ |
| `k<=j` | 1 | $K+2n$ | $K+2n$ |
| `k++` | 2 | $K$ | $2K$ |
| Operasi tetap | 1 | $K$ | $K$ |
| **Jumlah** | | | **$T(n)=2+10n+12M+4K$** |

Periksa koefisien $n$: pemeriksaan dan kenaikan $i$ menyumbang $3n$, inisialisasi $j$ dan pemeriksaan gagalnya $3n$, dan inisialisasi serta pemeriksaan gagal $k$ menyumbang $4n$: total $10n$. Karena $M=n(n+1)/2$ dan $K=3M$, $T(n)=2+10n+24M=12n^2+22n+2=\Theta(n^2)$.

### 12. Mengapa asumsi pembagian penting?

Dengan pembagian bilangan bulat, urutannya $3,1,0$. Badan berjalan dua kali dan kondisi diperiksa tiga kali:

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i=3` | 1 | $1$ | $1$ |
| `i>0` | 1 | $3$ | $3$ |
| `i=floor(i/2)` | 2 | $2$ | $4$ |
| **Jumlah** | | | **$T(3)=8$** |

Dengan pembagian riil tanpa pembulatan, urutannya $3,1{,}5,0{,}75,\ldots$ dan tetap positif dalam matematika riil: loop tidak berhenti. Karena perilakunya berbeda, tidak ada satu nilai $T(3)$ hingga yang berlaku untuk kedua arti `/` itu.
