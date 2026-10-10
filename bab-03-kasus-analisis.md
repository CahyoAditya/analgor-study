# Bab 3 — Panduan Responsi Pertemuan 3

Lembar responsi ketiga berisi enam nomor besar. Kita mengikuti urutan itu: membuktikan batas pertumbuhan, memperkirakan waktu saat data bertambah, lalu menghitung biaya tiap baris program. Bayangkan panitia mengolah daftar peserta. Mula-mula panitia ingin tahu bagaimana waktu program bertambah; setelah itu panitia membongkar program untuk melihat *mengapa* pertumbuhannya begitu.

| Nomor | Yang dicari | Cara berpikir utama |
| --- | --- | --- |
| 1a–b | Benar atau salah klaim Big-O | Cari batas yang berlaku untuk semua input besar, atau tunjukkan mengapa mustahil. |
| 2 | Waktu model kubik | Bandingkan ukuran baru dengan ukuran lama. |
| 3 | Pilihan antara X dan Y | Cari titik waktu sama, lalu periksa rentang soal. |
| 4 | Waktu model kubik, kuadrat, dan $n\log n$ | Kalibrasi tiap model dari waktu yang diketahui. |
| 5 | Biaya dua program bersarang | Hitung putaran yang panjangnya berubah. |
| 6a–e | Biaya lima potongan program | Catat biaya dan frekuensi setiap baris. |

Empat pertanyaan yang akan kita ulang: *apa ukuran input, baris mana yang dihitung, berapa kali baris itu berjalan, dan mengapa hasilnya masuk akal untuk input kecil?* Soal latihan lengkap ditempatkan di [Latihan Bab 3](latihan-bab-03.md).

## 1. Big-O: bagaimana membuktikan suatu batas?

Pernyataan $f(n)\in O(g(n))$ berarti ada angka tetap $c>0$ dan batas awal $n_0$ sehingga $0\le f(n)\le c g(n)$ untuk **setiap** $n\ge n_0$. Anggap $cg(n)$ sebagai atap. Satu nilai $n$ yang kebetulan berada di bawah atap belum cukup; semua ukuran setelah $n_0$ harus berada di bawahnya. Sebagai pemanasan, $3n+2\in O(n)$: untuk $n\ge1$, $2\le2n$, jadi $3n+2\le5n$. Kita menemukan $c=5$ dan $n_0=1$.

Sebaliknya, $n^2\notin O(n)$. Andaikan $n^2\le cn$ untuk semua $n$ yang cukup besar. Karena $n>0$, pembagian kedua sisi dengan $n$ memberi $n\le c$. Kita selalu bisa memilih $n>c$. Jadi tidak ada angka tetap $c$ yang cukup besar selamanya. Inilah bentuk alasan yang diperlukan untuk membuktikan suatu klaim *bukan* Big-O.

### 1a. Empat klaim dari lembar responsi

**Soal sumber.** Tentukan benar atau salah: (1) $7n^5-24n^4+10n-2\in O(n^5)$; (2) $2n^3+15n^2+7\notin O(n^2)$; (3) $4n^3+9n+5\in O(n^3)$; (4) $3n^2+8n+12\in O(n^3)$. Ukuran $n$ adalah bilangan bulat positif.

1. **Benar.** Untuk $n\ge4$, $7n^5-24n^4=n^4(7n-24)\ge0$ dan $10n-2>0$, sehingga fungsi tidak negatif. Untuk batas atas, buang suku negatif: $7n^5-24n^4+10n-2\le7n^5+10n\le17n^5$. Pilih $c=17$, $n_0=4$. Kita tidak memakai $n_0=1$ karena polinom ini bernilai negatif pada beberapa input kecil; definisi biaya nonnegatif baru terjamin pada rentang yang dipilih.
2. **Benar.** Andaikan fungsi itu $O(n^2)$, maka $2n^3+15n^2+7\le cn^2$ untuk semua $n$ besar. Membagi dengan $n^2>0$ menghasilkan $2n+15+7/n^2\le c$. Sisi kiri membesar tanpa batas. Mustahil ada $c$ tetap. Perhatikan lambang $\notin$: yang dinilai benar ialah kalimat “fungsi **bukan** $O(n^2)$”.
3. **Benar.** Pada $n\ge1$, $n\le n^3$ dan $1\le n^3$, sehingga $4n^3+9n+5\le(4+9+5)n^3=18n^3$. Pilih $c=18$, $n_0=1$.
4. **Benar, tetapi batasnya longgar.** Untuk $n\ge1$, $3n^2+8n+12\le23n^3$. Pilih $c=23$, $n_0=1$. Batas $O(n^2)$ juga benar karena $3n^2+8n+12\le23n^2$. Jika ingin menyatakan kelas yang rapat, tulis $\Theta(n^2)$. Big-O adalah batas atas, jadi $O(n^3)$ tidak otomatis salah hanya karena ada batas yang lebih rapat.

### 1b. Menentukan batas dua fungsi

**Soal sumber.** Tentukan Big-O dan buktikan dengan definisinya untuk (1) $5n+n^4+6$ dan (2) $2+4+6+\cdots+n+4n^2$. Untuk deret kedua, ambil $n$ **genap positif** agar $n$ benar-benar suku terakhir.

Untuk fungsi pertama dan $n\ge1$, $5n\le5n^4$ serta $6\le6n^4$. Karena itu $5n+n^4+6\le12n^4$. Pilih $c=12$, $n_0=1$: hasilnya $O(n^4)$. Fungsi itu juga setidaknya $n^4$, sehingga kelas rapatnya $\Theta(n^4)$.

Pada fungsi kedua ada $n/2$ suku genap. Tulis tiap suku sebagai dua kali bilangan 1 sampai $n/2$:

$$2+4+\cdots+n=2(1+2+\cdots+n/2)=\frac n2\left(\frac n2+1\right)=\frac{n^2}{4}+\frac n2.$$

Mengapa rumus jumlah 1 sampai $m$ adalah $m(m+1)/2$? Pasangkan angka pertama dan terakhir: $1+m$, lalu $2+(m-1)$, dan seterusnya; jumlah pasangan itu menghasilkan rumus tersebut. Tambahkan $4n^2$ dari soal: $f(n)=\frac{17}{4}n^2+\frac12n$. Pada $n\ge2$, $n\le n^2$, jadi $f(n)\le\frac{19}{4}n^2$. Pilih $c=19/4$, $n_0=2$ pada domain genap. Karena $f(n)\ge4n^2$, kelas rapatnya $\Theta(n^2)$. Bila $n$ ganjil, penulisan deret yang berakhir di $n$ tidak cocok dengan pola bilangan genap; batas terakhirnya perlu ditentukan dahulu.

## 2. Mengapa kenaikan input delapan kali membuat waktu 512 kali?

**Soal sumber.** Algoritme mengikuti $T(n)=cn^3$ detik dan memerlukan 0,5 detik untuk 50 item. Berapa waktu untuk 400 item?

Konstanta $c$ sama pada dua pengukuran, jadi kita dapat membandingkan waktu tanpa menghitung $c$:

$$\frac{T(400)}{T(50)}=\frac{c\,400^3}{c\,50^3}=\left(\frac{400}{50}\right)^3=8^3=512.$$

Ukuran menjadi delapan kali; model kubik membuat waktu menjadi $8\times8\times8=512$ kali. Karena waktu awal 0,5 detik, waktu baru $0{,}5\times512=\boxed{256\text{ detik}}$, yaitu 4 menit 16 detik. Hasil ini mengandaikan bentuk $cn^3$ tepat, konstanta tetap, dan kondisi pengukuran sama. Big-O $O(n^3)$ saja tidak cukup untuk memperoleh angka 256.

## 3. Kapan X atau Y lebih cepat?

**Soal sumber.** Untuk $n$ hingga $10^{10}$, waktu X adalah $T_X(n)=0{,}05n\log_2n$ milidetik dan waktu Y adalah $T_Y(n)=3n$ milidetik. Tentukan pilihan di rentang itu dan kapan pilihan berubah.

Waktu lebih kecil berarti lebih cepat. Cari saat keduanya sama. Karena $n>0$, kita boleh membagi **kedua sisi** dengan $n$:

$$0{,}05n\log_2n=3n\iff0{,}05\log_2n=3\iff\log_2n=60\iff n=2^{60}.$$

Logaritma $\log_2n=60$ berarti $2$ dipangkatkan 60 menghasilkan $n$. Karena $\log_2n$ naik saat $n$ naik, X lebih cepat ketika $1\le n<2^{60}$; waktunya sama pada $n=2^{60}$; Y lebih cepat ketika $n>2^{60}$. Batas soal $10^{10}$ masih jauh di bawah $2^{60}\approx1{,}153\times10^{18}$, jadi **pilih X untuk seluruh rentang soal**. Sebagai cek, pada $n=2^{10}$, waktu X $=0{,}5n$ dan Y $=3n$. Perbandingan kelas pertumbuhan saja tidak menjawab pilihan dalam rentang tertentu: koefisien $0{,}05$ juga berpengaruh.

## 4. Tiga model yang sama-sama mulai dari lima detik

**Soal sumber.** P, Q, R masing-masing memerlukan 5 detik untuk 50 item. Kelas yang diberikan ialah $O(n^3)$, $O(n^2)$, dan $O(n\log n)$. Perkirakan waktu untuk 5000 item.

**Asumsi agar angka bisa dihitung:** kita perlakukan waktu tiap program sebagai $c_Pn^3$, $c_Qn^2$, dan $c_Rn\log_2n$, dengan konstanta tetap. Label Big-O sendiri hanya memberi batas atas dan satu pengukuran tidak menentukan waktu tepat. Ukuran baru 5000/50 = 100 kali ukuran lama.

| Program | Faktor dari 50 ke 5000 | Waktu perkiraan |
| --- | --- | ---: |
| P | $100^3=1.000.000$ | $5.000.000$ detik |
| Q | $100^2=10.000$ | $50.000$ detik |
| R | $100\,\dfrac{\log_2 5000}{\log_2 50}\approx217{,}72$ | $\approx1.088{,}6$ detik |

Untuk R, faktor $n$ bertambah 100 kali, tetapi faktor logaritma juga berubah: $\log_2 50\approx5{,}644$ menjadi $\log_2 5000\approx12{,}288$. Rasionya sekitar 2,177. Karena itu $5\times100\times2{,}177\approx1.088{,}6$ detik. Dalam model ini R tercepat pada 5000 item. Mengganti basis log tetap tidak mengubah rasio ini.

## 5. Dari putaran program ke $T(n)$

Untuk nomor 5 dan 6, $n$ adalah **bilangan bulat positif**. Pembagian indeks memakai pembagian bilangan bulat ke bawah. Tanpa pembulatan itu, loop `while (i > 0) { i = i / 2; }` atas bilangan riil positif tidak pernah mencapai nol. Model biaya mengikuti Bab 2: penugasan dan perbandingan sederhana berbiaya 1; `++`, `*= 2`, `*= 3`, atau `/= 2` berbiaya 2 karena ada aritmetika dan penugasan. Kolom *Frequency* menghitung setiap pelaksanaan baris, termasuk satu pemeriksaan kondisi terakhir yang gagal **setiap kali loop dimulai**. Kolom *Total* ialah *Cost* dikali *Frequency*; jumlah semua Total adalah $T(n)$.

### 5a. Loop $j$ memendek ketika $i$ mengecil

**Soal sumber.**

```text
i = n
while (i > 1) {
    j = 1
    while (j < i) {
        k = 0
        while (k < n) { k = k + 1 }
        j = j * 3
    }
    i = floor(i / 2)
}
```

Untuk $n=8$, nilai $i$ yang masuk badan loop ialah 8, 4, 2. Ketika $i=8$, $j=1,3$; ketika $i=4$, $j=1,3$; ketika $i=2$, $j=1$. Jadi loop $j$ total berjalan $2+2+1=5$ kali. Setiap kali itu terjadi, $k$ **dimulai lagi dari nol** dan berjalan delapan kali. Maka baris `k = k + 1` berjalan $5\times8=40$ kali. Panjang loop $j$ berubah, sehingga kita menjumlahkan banyak putaran per nilai $i$, bukan sekadar mengalikan tiga panjang yang dianggap tetap.

Untuk rumus umum, tetapkan $m=\lfloor\log_2n\rfloor$, yaitu banyak putaran $i$, dan $i_t=\lfloor n/2^t\rfloor$ untuk $t=0,\ldots,m-1$. Banyak nilai $j$ pada satu $i_t>1$ ialah $\lceil\log_3i_t\rceil$: nilai $j$ berawal dari $3^0=1$ lalu menjadi $3^1,3^2,\ldots$ selama masih $<i_t$. Sebut totalnya

$$S=\sum_{t=0}^{m-1}\lceil\log_3 i_t\rceil.$$

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = n` | 1 | $1$ | $1$ |
| `i > 1` | 1 | $m+1$ | $m+1$ |
| `i = floor(i / 2)` | 2 | $m$ | $2m$ |
| `j = 1` | 1 | $m$ | $m$ |
| `j < i` | 1 | $S+m$ | $S+m$ |
| `j = j * 3` | 2 | $S$ | $2S$ |
| `k = 0` | 1 | $S$ | $S$ |
| `k < n` | 1 | $S(n+1)$ | $Sn+S$ |
| `k = k + 1` | 2 | $Sn$ | $2Sn$ |
| **Jumlah** | | | **$T(n)=2+5m+5S+3nS$** |

Cek $n=8$: $m=3$, $S=5$, maka $T(8)=162$. Paling banyak ada sekitar $\log_2n$ nilai $i$, masing-masing dengan paling banyak sekitar $\log_3n$ nilai $j$: ini memberi batas atas $S=O(\log^2n)$. Pada kira-kira separuh putaran awal, $i$ masih setidaknya $\sqrt n$, sehingga setiap putaran tersebut mempunyai jumlah $j$ sebanding $\log n$: ini memberi batas bawah. Jadi $S=\Theta(\log^2n)$ dan $\boxed{T(n)=\Theta(n\log^2n)}$.

### 5b. Loop $j$ memanjang ketika $i$ membesar

**Soal sumber.**

```text
i = 1
while (i <= n) {
    j = 1
    while (j <= i) {
        k = 1
        while (k <= j) { k *= 2 }
        j++
    }
    i *= 2
}
```

Untuk $n=4$, $i$ bernilai 1, 2, 4. Banyak nilai $j$ berturut-turut 1, 2, 4, jadi `k = 1` terjadi $1+2+4=7$ kali. Tetapi panjang loop $k$ bergantung pada **nilai $j$**: $j=1$ memberi satu putaran; $j=2$ memberi dua; $j=4$ memberi tiga. Total putaran $k$ pada ketiga putaran $i$ ialah $1+(1+2)+(1+2+2+3)=12$.

Untuk $n\ge1$, tulis $a=\lfloor\log_2n\rfloor+1$. Nilai $i$ adalah $2^0,2^1,\ldots,2^{a-1}$ dan jumlah seluruh putaran $j$ ialah $J=\sum_{t=0}^{a-1}2^t=2^a-1$. Pada nilai $j$, loop $k$ berjalan $h(j)=\lfloor\log_2j\rfloor+1$ kali. Karena $j$ dimulai ulang pada setiap nilai $i$, total putaran $k$ adalah

$$H=\sum_{t=0}^{a-1}\sum_{j=1}^{2^t}(\lfloor\log_2j\rfloor+1).$$

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = 1` | 1 | $1$ | $1$ |
| `i <= n` | 1 | $a+1$ | $a+1$ |
| `i *= 2` | 2 | $a$ | $2a$ |
| `j = 1` | 1 | $a$ | $a$ |
| `j <= i` | 1 | $J+a$ | $J+a$ |
| `j++` | 2 | $J$ | $2J$ |
| `k = 1` | 1 | $J$ | $J$ |
| `k <= j` | 1 | $H+J$ | $H+J$ |
| `k *= 2` | 2 | $H$ | $2H$ |
| **Jumlah** | | | **$T(n)=2+5a+5J+3H$** |

Cek $n=4$: $a=3$, $J=7$, $H=12$, sehingga $T(4)=2+15+35+36=88$. Karena $2^{a-1}\le n<2^a$, $J=\Theta(n)$. Setiap $h(j)$ paling banyak $a$, sehingga $H=O(n\log n)$. Pada banyak $j$ dalam putaran $i$ terakhir, $h(j)$ juga sebanding $\log n$, sehingga $H=\Omega(n\log n)$. Maka $\boxed{T(n)=\Theta(n\log n)}$.

## 6. Lima potongan program dan biaya tiap baris

**Soal sumber.** Lembar meminta biaya $T(n)$ dan kompleksitas untuk potongan a–e dengan proses dasar berbiaya satu satuan. Panduan ini memecah satu baris menjadi proses dasarnya sebagaimana Bab 2: penugasan atau perbandingan sederhana = 1; aritmetika lalu penugasan = 2. Pada `j <= i*i`, perkalian batas dan perbandingan = 2 **jika batas dihitung ulang setiap pemeriksaan**. Pada `j % i == 0`, modulo dan perbandingan = 2. Operasi tetap dalam badan loop = 1. Jika satu baris utuh diperlakukan sebagai satu unit, koefisien $T(n)$ akan berbeda, tetapi kelas $\Theta$ tidak berubah. Menyatakan aturan biaya sebelum menghitung membuat jawabannya dapat diperiksa.

### 6a. Membagi $i$ sampai nol

**Soal sumber:** `i=n; while (i>0) { i=i/2; }`.

Pada $n=8$, nilai $i$ yang masuk badan loop ialah 8, 4, 2, 1: empat putaran. Nilai berikutnya nol, lalu kondisi diperiksa sekali lagi. Untuk $n\ge1$, sebut $h=\lfloor\log_2n\rfloor+1$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = n` | 1 | $1$ | $1$ |
| `i > 0` | 1 | $h+1$ | $h+1$ |
| `i = floor(i/2)` | 2 | $h$ | $2h$ |
| **Jumlah** | | | **$T(n)=3h+2=\Theta(\log n)$** |

Jadi $T(8)=14$. Jumlah putaran badan ialah $\lfloor\log_2n\rfloor+1$, bukan selalu persis $\log_2n$.

### 6b. Dua loop penuh sepanjang $n$

**Soal sumber:** `for (i=1; i<=n; i++) { for (j=1; j<=n; j++) { operasi O(1); } }`.

Pada $n=2$, pasangan $(i,j)$ ialah $(1,1),(1,2),(2,1),(2,2)$; badan bekerja empat kali. Loop $j$ dimulai ulang pada setiap nilai $i$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = 1` | 1 | $1$ | $1$ |
| `i <= n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j = 1` | 1 | $n$ | $n$ |
| `j <= n` | 1 | $n(n+1)$ | $n^2+n$ |
| `j++` | 2 | $n^2$ | $2n^2$ |
| Operasi tetap | 1 | $n^2$ | $n^2$ |
| **Jumlah** | | | **$T(n)=4n^2+5n+2=\Theta(n^2)$** |

### 6c. Panjang loop dalam tergantung nilai $i$

**Soal sumber:** `for (i=1; i<=n; i++) { j=i; while (j>0) { j=j/2; } }`.

Untuk $i=1,2,3,4$, banyak putaran `while` ialah 1, 2, 2, 3; totalnya 8. Tulis $h(i)=\lfloor\log_2i\rfloor+1$ dan $L=\sum_{i=1}^n h(i)$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = 1` | 1 | $1$ | $1$ |
| `i <= n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j = i` | 1 | $n$ | $n$ |
| `j > 0` | 1 | $L+n$ | $L+n$ |
| `j = floor(j/2)` | 2 | $L$ | $2L$ |
| **Jumlah** | | | **$T(n)=3L+5n+2=\Theta(n\log n)$** |

Batas atasnya jelas karena tiap $h(i)\le\lfloor\log_2n\rfloor+1$. Batas bawahnya berasal dari setidaknya separuh nilai $i$ yang cukup besar: masing-masing memerlukan putaran sebanding $\log n$. Jadi menjumlahkannya menghasilkan $n\log n$, bukan $n^2$.

### 6d. Hanya kelipatan $i$ yang membuka loop $k$

**Soal sumber:**

```text
for (i = 1; i <= n; i++)
    for (j = 1; j <= i * i; j++)
        if (j % i == 0)
            for (k = 1; k <= j; k++)
                operasi O(1)
```

Pada $i=2$, $j$ bernilai 1, 2, 3, 4. Kondisi benar hanya pada $j=2$ dan $j=4$, sehingga operasi terdalam terjadi $2+4=6$ kali. Secara umum, kelipatan $i$ sampai $i^2$ ialah $i,2i,\ldots,i\cdot i$. Kita perlu tiga jumlah yang berbeda:

$$N=\sum_{i=1}^n i^2,\qquad M=\sum_{i=1}^n i=\frac{n(n+1)}2,\qquad K=\sum_{i=1}^n\sum_{q=1}^i qi=\frac12\sum_{i=1}^n(i^3+i^2).$$

$N$ menghitung semua putaran $j$, $M$ menghitung banyak kondisi yang benar, dan $K$ menghitung seluruh putaran $k$. Untuk $n=2$: $N=5$, $M=3$, $K=1+(2+4)=7$.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = 1` | 1 | $1$ | $1$ |
| `i <= n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j = 1` | 1 | $n$ | $n$ |
| `j <= i*i` | 2 | $N+n$ | $2N+2n$ |
| `j++` | 2 | $N$ | $2N$ |
| `j % i == 0` | 2 | $N$ | $2N$ |
| `k = 1` | 1 | $M$ | $M$ |
| `k <= j` | 1 | $K+M$ | $K+M$ |
| `k++` | 2 | $K$ | $2K$ |
| Operasi tetap | 1 | $K$ | $K$ |
| **Jumlah** | | | **$T(n)=2+6n+6N+2M+4K=\Theta(n^4)$** |

Cek $n=2$: $T(2)=2+12+30+6+28=78$. Mengapa pangkat empat? Bagian dominan $K$ memuat $\sum i^3$, dan $\sum_{i=1}^n i^3=[n(n+1)/2]^2=\Theta(n^4)$. Sebaliknya, $N=\Theta(n^3)$ dan $M=\Theta(n^2)$, jadi keduanya lebih kecil ketika $n$ membesar. Menyimpan `i*i` sekali per $i$ akan mengubah biaya tepat, bukan kelas pertumbuhannya.

### 6e. Kode yang sama dengan nomor 5b

**Soal sumber:** `i=1; while (i<=n) { j=1; while (j<=i) { k=1; while (k<=j) { k*=2; } j++; } i*=2; }`.

Kode ini identik dengan potongan kedua nomor 5. Dengan $a=\lfloor\log_2n\rfloor+1$, $J=2^a-1$, dan $H=\sum_{t=0}^{a-1}\sum_{j=1}^{2^t}(\lfloor\log_2j\rfloor+1)$, jumlah pelaksanaan tiap baris juga sama:

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = 1` | 1 | $1$ | $1$ |
| `i <= n` | 1 | $a+1$ | $a+1$ |
| `i *= 2` | 2 | $a$ | $2a$ |
| `j = 1` | 1 | $a$ | $a$ |
| `j <= i` | 1 | $J+a$ | $J+a$ |
| `j++` | 2 | $J$ | $2J$ |
| `k = 1` | 1 | $J$ | $J$ |
| `k <= j` | 1 | $H+J$ | $H+J$ |
| `k *= 2` | 2 | $H$ | $2H$ |
| **Jumlah** | | | **$2+5a+5J+3H$** |

Jadi hasilnya

$$\boxed{T(n)=2+5a+5J+3H=\Theta(n\log n).}$$

Ini pemeriksaan silang: jika dua potongan identik menghasilkan rumus berbeda, ada frekuensi atau biaya yang tertinggal.

**Sumber utama:** *Lembar Kerja Responsi Pertemuan 3 Analgor*, semester ganjil 2026–2027, halaman 1–3, dari arsip materi yang diberikan Sensei. Pernyataan soal ditulis ulang untuk belajar. Asumsi pembagian bulat, domain $n$, dan model biaya dinyatakan karena memengaruhi hasil tepat.
