# Bab 2 — Panduan Responsi Pertemuan 2

Lembar responsi kedua menanyakan empat hal: memilih suku yang paling berpengaruh saat input membesar, memilih paket perangkat lunak pada ukuran data tertentu, menghitung pekerjaan di dalam loop, dan menghitung waktu dua cara mencari rata-rata. Bab ini mengikuti **urutan keempat nomor itu**. Semua bagian memakai satu cerita: panitia mengolah daftar nilai peserta yang terus bertambah. Cerita membantu memahami *mengapa* perhitungan diperlukan; angka dalam pembahasan tetap mengikuti lembar responsi.

| Nomor responsi | Pertanyaan | Hasil yang dicari |
| --- | --- | --- |
| 1 | Dari beberapa bagian biaya, mana yang akhirnya paling besar? | Suku dominan dan batas Big-O tujuh ekspresi. |
| 2a–b | Paket A atau B lebih cepat pada jumlah record yang diminta? | Perbandingan waktu pada rentang input soal. |
| 3a–c | Berapa kali pekerjaan terdalam dijalankan? | Fungsi $F(n)$ dan kelas pertumbuhannya. |
| 4a–b | Bagaimana menghitung waktu setiap baris dua algoritme rata-rata? | Tabel jumlah pelaksanaan, biaya, dan pilihan algoritme. |

**Empat pertanyaan yang dipakai berulang:** apa ukuran inputnya, pekerjaan apa yang dihitung, mengapa operasi hitungnya penjumlahan atau perkalian, dan bagaimana hasilnya diperiksa dengan ukuran kecil? Jangan mengganti hitungan waktu nyata dengan Big-O: keduanya menjawab pertanyaan berbeda.

## 1. Suku dominan: bagian biaya mana yang akhirnya menguasai?

Panitia dapat memakai sebuah program yang pertama kali menyiapkan daftar, lalu membaca setiap nama, lalu membandingkan beberapa pasangan nama. Jika ukuran daftar $n$, masing-masing tahap mungkin memerlukan waktu tetap, waktu sebanding $n$, atau waktu sebanding $n^2$. Waktu total adalah **jumlah** ketiganya karena tahap-tahap itu dikerjakan berurutan. Contohnya $T(n)=5+2n+0{,}01n^2$.

Pada $n=10$, suku $2n$ bernilai 20, sedangkan suku $0{,}01n^2$ baru 1. Namun pada $n=10.000$, keduanya menjadi 20.000 dan 1.000.000. Jadi “dominan” berarti suku yang menguasai *ketika $n$ terus membesar*, bukan suku terbesar pada setiap ukuran. Koefisien kecil tetap penting untuk waktu tepat pada input tertentu.

### Mengapa kita boleh menyebut Big-O?

Kalimat $T(n)\in O(g(n))$ berarti ada bilangan tetap $c>0$ dan $n_0$ sehingga $T(n)\le c g(n)$ untuk **semua** $n\ge n_0$. Ini batas atas, bukan waktu dalam detik dan bukan persamaan $T(n)=g(n)$. Sebagai pemanasan, untuk $T(n)=5+2n+0{,}01n^2$ dan $n\ge1$, kita tahu $1\le n^2$ dan $n\le n^2$. Karena itu

$$
5+2n+0{,}01n^2\le5n^2+2n^2+0{,}01n^2=7{,}01n^2.
$$

Pilih $c=7{,}01$ dan $n_0=1$: terbukti $T(n)\in O(n^2)$. Karena $T(n)\ge0{,}01n^2$, fungsi itu juga punya batas bawah sebanding $n^2$. Bila dua batas diperlukan, kita menulis $T(n)\in\Theta(n^2)$. Lembar responsi nomor 1 hanya meminta *suku dominan dan Big-O*. Menunjukkan batas atas tetap berguna agar jawaban tidak sekadar menebak pangkat tertinggi.

Untuk membandingkan bentuk yang sering muncul, ingat urutan akhirnya: $\log\log n$ tumbuh lebih lambat daripada $\log n$; lalu $\sqrt n=n^{0{,}5}$, $n$, $n\log n$, $n^{1{,}25}$, $n^{1{,}5}$, $n^2$, dan $n^3$. Jika dua suku sama-sama berpangkat $n$, faktor $\log n$ membuat $n\log n$ akhirnya lebih besar daripada $n$; jika pangkatnya berbeda, $n^{1{,}5}$ akhirnya mengalahkan $n\log n$. Basis logaritma yang tetap dan lebih besar dari 1 hanya mengubah faktor pengali, bukan kelasnya.

### Tujuh baris pada nomor 1

**Soal sumber.** Anggap setiap ekspresi pada tabel berikut adalah waktu pemrosesan $T(n)$ untuk masalah berukuran $n$. Tentukan suku dominan dan Big-O masing-masing. Baris terakhir pada lembar responsi sudah memuat contoh jawaban. Bentuk ekspresi di bawah ditranskripsikan dari tabel pada halaman 1; tanda koma desimal mengikuti penulisan Indonesia.

| Baris | $T(n)$ dari lembar responsi | Suku dominan | Big-O |
| ---: | --- | --- | --- |
| 1 | $5+0{,}001n^3+0{,}025n$ | $0{,}001n^3$ | $O(n^3)$ |
| 2 | $500n+100n^{1{,}5}+50n\log_{10}n$ | $100n^{1{,}5}$ | $O(n^{1{,}5})$ |
| 3 | $100n+0{,}01n^2$ | $0{,}01n^2$ | $O(n^2)$ |
| 4 | $0{,}01n+100n^2$ | $100n^2$ | $O(n^2)$ |
| 5 | $2n+n^{0{,}5}+0{,}5n^{1{,}25}$ | $0{,}5n^{1{,}25}$ | $O(n^{1{,}25})$ |
| 6 | $100n\log_3n+n^3+100n$ | $n^3$ | $O(n^3)$ |
| 7 | $0{,}003\log_4n+\log_2(\log_2n)$ | $0{,}003\log_4n$ | $O(\log n)$ |

**Baris 1 — mengapa koefisien kecil tidak mengubah jawabannya?** Konstanta 5 tidak bertambah saat $n$ bertambah. Suku $0{,}025n$ bertambah sebanding $n$. Suku $0{,}001n^3$ bertambah sebanding $n^3$. Jika $n$ digandakan, bagian kubik menjadi delapan kali, sedangkan bagian linear hanya dua kali. Untuk $n\ge1$, $5\le5n^3$ dan $0{,}025n\le0{,}025n^3$, sehingga $T(n)\le5{,}026n^3$. Nilai $0{,}001$ yang kecil dapat menunda kapan suku kubik tampak terbesar, tetapi tidak mengubah arah pertumbuhan untuk $n$ besar.

**Baris 2 — mengapa $n^{1{,}5}$ mengalahkan $n\log n$?** Bagi keduanya dengan $n>0$. Pertanyaannya menjadi apakah $\sqrt n$ atau $\log_{10}n$ yang tumbuh lebih cepat. Akar bertambah lebih cepat pada akhirnya. Untuk melihat bahwa koefisien tidak menyelamatkan suku logaritmik, bandingkan rasio $(50n\log_{10}n)/(100n^{1{,}5})=(\log_{10}n)/(2\sqrt n)$; rasio ini menuju nol ketika $n$ membesar. Suku $500n$ juga kalah dari $n^{1{,}5}$ karena rasionya $5/\sqrt n\to0$. Jadi suku tengah dominan.

**Baris 3 dan 4 — mengapa hasilnya sama meski koefisiennya terbalik?** Keduanya mempunyai satu suku linear dan satu suku kuadrat. Di baris 3, $0{,}01n^2$ mungkin kalah dari $100n$ untuk input kecil. Di baris 4, $100n^2$ sudah besar lebih awal. Namun untuk $n$ yang terus membesar, keduanya tetap mengikuti $n^2$. Titik saat dua suku baris 3 sama adalah $100n=0{,}01n^2$, yaitu $n=10.000$ setelah membagi kedua sisi dengan $0{,}01n>0$. Titik itu menjelaskan *kapan* suku kuadrat mulai mengungguli suku linear pada baris tersebut; Big-O menjelaskan *bagaimana* pertumbuhan jangka panjangnya.

**Baris 5 — mengapa pangkat pecahan bisa dominan?** $n^{0{,}5}=\sqrt n$, sedangkan $n^{1{,}25}=n\sqrt[4]n$. Dibandingkan $2n$, suku terakhir mempunyai faktor tambahan $n^{0{,}25}$ yang terus bertambah. Misalnya saat $n=16$, $n^{1{,}25}=16\cdot2=32$. Faktor $0{,}5$ hanya mengalikan hasil; ketika $n$ cukup besar, suku berpangkat $1{,}25$ tetap dominan.

**Baris 6 — mengapa kubik mengalahkan $n\log n$?** Suku $100n\log_3n$ boleh tampak besar pada ukuran tertentu. Tetapi $(100n\log_3n)/n^3=100\log_3n/n^2\to0$; suku $100n$ pun menjadi $100/n^2$ jika dibandingkan dengan $n^3$. Dua rasio itu menyusut, sehingga $n^3$ dominan. Dua pekerjaan linear dan logaritmik dijumlahkan dengan pekerjaan kubik, bukan mengubahnya menjadi $n^4$.

**Baris 7 — logaritma di dalam logaritma.** $\log_2(\log_2 n)$ berarti mula-mula hitung $\log_2n$, kemudian ambil logaritmanya lagi; untuk pembahasan ini ambil $n>2$ agar kedua nilainya positif. Contoh $n=2^{16}$ memberi $\log_2n=16$ dan $\log_2(\log_2n)=4$, sedangkan $\log_4n=8$. Angka $0{,}003$ membuat suku pertama kecil pada contoh tersebut, tetapi $\log\log n$ akhirnya tumbuh lebih lambat daripada $\log n$. Karena $\log_4n=\tfrac12\log_2n$, suku pertama sebanding $\log n$, tepat seperti contoh jawaban pada lembar.

**Periksa sebelum lanjut.** Suku dominan adalah *suku asli* seperti $0{,}001n^3$; kolom Big-O membuang koefisien tetap dan menulis kelas seperti $O(n^3)$. Jika diminta waktu pada $n$ tertentu, masukkan $n$ ke **seluruh** ekspresi, jangan hanya ke suku dominan.

## 2. Dua paket: mana yang lebih cepat pada data yang benar-benar diminta?

Nomor 1 menatap pertumbuhan saat $n$ makin besar. Nomor 2 menanyakan keputusan untuk jumlah record yang *dibatasi*. Paket dengan kelas pertumbuhan yang akhirnya lebih baik belum tentu lebih cepat dalam rentang itu, sebab faktor pengalinya berbeda. Anggap panitia harus membeli satu dari dua paket untuk memproses data. Kita samakan satuan, cari tempat waktunya sama, lalu cek di sisi ukuran yang ditanya.

### 2a. Paket dengan $n\log n$ melawan paket linear

**Soal sumber.** Waktu rata-rata A ialah $T_A(n)=0{,}1n\log_2n$ mikrodetik dan B ialah $T_B(n)=5n$ mikrodetik. Mana lebih cepat untuk basis data hingga $10^{12}$ record?

Kedua waktu sudah dalam mikrodetik. Kata “lebih cepat” berarti **waktu lebih kecil**. Kita belum boleh memilih B hanya karena $n$ akhirnya tumbuh lebih lambat daripada $n\log n$; rentangnya dibatasi. Cari ukuran saat keduanya sama:

$$
\begin{aligned}
0{,}1n\log_2n&=5n\\
0{,}1\log_2n&=5 &&\text{bagi kedua sisi dengan }n>0\\
\log_2n&=50 &&\text{bagi kedua sisi dengan }0{,}1\\
n&=2^{50}\approx1{,}126\times10^{15}.
\end{aligned}
$$

Mengapa $\log_2n=50$ menjadi $n=2^{50}$? Logaritma menanyakan “2 dipangkatkan berapa agar menjadi $n$?” Jawabannya 50, jadi $n$ ialah $2^{50}$. Angka ini jauh di atas $10^{12}$. Untuk mengecek sisi yang benar, ambil $n=2^{40}$ yang masih di bawah titik potong: $T_A=0{,}1n(40)=4n<5n=T_B$. Fungsi $\log_2n$ meningkat bersama $n$, sehingga untuk seluruh bilangan record $1\le n\le10^{12}<2^{50}$, $0{,}1\log_2n<5$. Jadi **A lebih cepat dalam rentang soal**. Pada $n=1$, $T_A(1)=0$ menurut model yang diberikan; ini hasil rumus model, bukan janji waktu komputer sesungguhnya nol.

### 2b. Paket linear melawan paket akar

**Soal sumber.** Waktu rata-rata A ialah $T_A(n)=0{,}001n$ milidetik dan B ialah $T_B(n)=500\sqrt n$ milidetik. Mana lebih cepat untuk basis data hingga $10^9$ record?

Satuannya sama. Cari titik potong positif; syarat $n>0$ penting sebelum membagi dengan akar:

$$
\begin{aligned}
0{,}001n&=500\sqrt n\\
0{,}001\sqrt n&=500 &&\text{bagi dengan }\sqrt n>0;\ n=(\sqrt n)^2\\
\sqrt n&=500.000\\
n&=(500.000)^2=250.000.000.000=2{,}5\times10^{11}.
\end{aligned}
$$

Titik potong itu di atas $10^9$. Pada batas soal, $T_A(10^9)=1.000.000$ milidetik, sedangkan $T_B(10^9)=500\sqrt{10^9}\approx15.811.388$ milidetik. A lebih cepat. Kita juga dapat membandingkan tanpa menghitung dua angka besar: bagi ketaksamaan $0{,}001n<500\sqrt n$ dengan $\sqrt n>0$. Ini setara dengan $0{,}001\sqrt n<500$, benar ketika $n<2{,}5\times10^{11}$. Maka **A lebih cepat untuk seluruh rentang $1\le n\le10^9$**. B baru unggul setelah titik potong meskipun fungsi akar tumbuh lebih lambat.

**Mengapa langkah ini penting?** Pada 2a, A yang mengandung logaritma menang dalam rentang soal, tetapi akhirnya B menang. Pada 2b, A yang linear menang dalam rentang soal, tetapi akhirnya B yang berakar menang. Jadi jangan menjawab pilihan paket hanya dari simbol $O(\cdot)$; pakai fungsi waktu dan batas $n$ yang diberikan.

## 3. Loop: hitung pekerjaan, bukan sekadar jumlah kata `for`

Sekarang panitia menulis program untuk memproses daftar. $F(n)$ berarti **jumlah pelaksanaan pekerjaan pada bagian paling dalam**. Untuk menghitung seluruh pekerjaan, gunakan $T(n)$: jumlah kolom *Total* dari setiap baris, termasuk pemeriksaan kondisi yang terakhir kali bernilai salah. Pada tabel di bawah, penugasan atau perbandingan berbiaya 1, `x++`, `x += 2`, `x *= 2`, dan `x /= 2` berbiaya 2 karena masing-masing melakukan operasi aritmetika lalu menyimpan hasilnya. Pekerjaan tetap di badan loop berbiaya 1. Ini adalah **model hitung yang dipilih**, bukan ukuran waktu nyata komputer. Kita mulai dengan $n=8$ agar setiap nilai indeks dapat dilihat, lalu menulis rumus umum.

Dalam tabel, *Frequency* adalah banyaknya suatu baris dijalankan, sedangkan *Total* = *Cost* $\times$ *Frequency*. Untuk batas `x < n`, nilai terakhir yang mencapai atau melewati $n$ tetap diperiksa satu kali. Karena itu loop `x = 0; x < n; x += 2` berjalan $\lceil n/2\rceil$ kali, bukan selalu tepat $n/2$; misalnya $n=5$ memberi nilai 0, 2, 4. Loop `x = n; x > 0; x = \lfloor x/2\rfloor` berjalan $\lfloor\log_2 n\rfloor+1$ kali untuk $n\ge1$; untuk $n=8$ nilainya 8, 4, 2, 1. Nilai awal dan tanda batas selalu menentukan apakah rumus logaritma perlu pembulatan atau tambahan 1.

**Aturan sederhana.** Dua tahap yang berjalan **berurutan** dijumlahkan. Loop yang benar-benar **bersarang**, dengan panjang dalam yang sama pada setiap putaran luar, dikalikan. Jika panjang dalam berubah mengikuti indeks luar, jumlahkan pekerjaan per putaran luar satu demi satu. Batas $j<n$ tidak memasukkan $n$; batas $bound\le n$ memasukkan $n$.

### 3a. Tiga loop bersarang yang masing-masing panjangnya $n$

**Soal sumber.** Loop $i$, $j$, dan $k$ masing-masing mengambil nilai integer $0,1,\ldots,n-1$. Loop $j$ ada di dalam $i$, loop $k$ di dalam $j$, dan setiap kombinasi menjalankan satu pekerjaan tetap. Tentukan $F(n)$ dan kelasnya.

Untuk $n=2$, pasangan $(i,j)$ adalah $(0,0),(0,1),(1,0),(1,1)$: ada empat. Untuk *setiap* pasangan, $k$ bisa 0 atau 1: dua pekerjaan. Jadi $F(2)=4\cdot2=8$. Pada $n$ umum, setiap indeks punya $n$ nilai, dan panjang $j$ maupun $k$ tidak bergantung pada nilai indeks luarnya. Karena itu

$$F(n)=\underbrace{n\cdot n\cdot n}_{\text{tiga pilihan indeks}}=n^3\in\Theta(n^3).$$

Pemeriksaan: untuk $n=3$, ada $3\cdot3\cdot3=27$ kombinasi. Tiga loop menghasilkan kubik **di soal ini** karena ketiganya berjalan sepanjang $n$ dan bersarang; jumlah kata `for` saja tidak cukup untuk menyimpulkan kubik.

Jika ketiga loop ditulis `for (i=0; i<n; i++)`, lalu `for (j=0; j<n; j++)`, lalu `for (k=0; k<n; k++)` dengan satu pekerjaan tetap di dalamnya, perhitungan **seluruh baris** menjadi:

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = 0` | 1 | $1$ | $1$ |
| `i < n` | 1 | $n+1$ | $n+1$ |
| `i++` | 2 | $n$ | $2n$ |
| `j = 0` | 1 | $n$ | $n$ |
| `j < n` | 1 | $n(n+1)$ | $n^2+n$ |
| `j++` | 2 | $n^2$ | $2n^2$ |
| `k = 0` | 1 | $n^2$ | $n^2$ |
| `k < n` | 1 | $n^2(n+1)$ | $n^3+n^2$ |
| `k++` | 2 | $n^3$ | $2n^3$ |
| Pekerjaan tetap | 1 | $n^3$ | $n^3$ |
| **Jumlah** | | | **$T(n)=4n^3+5n^2+5n+2$** |

Perhatikan perbedaan $F(n)=n^3$ dan $T(n)=4n^3+5n^2+5n+2$. Yang pertama hanya menghitung pekerjaan terdalam; yang kedua juga menghitung pengendali loop. Keduanya tetap $\Theta(n^3)$.

### 3b. Membagi, menggandakan, dan melangkah dua

**Soal sumber.** Loop luar dimulai dari $i=n$, terus memakai pembagian bilangan bulat $i\leftarrow\lfloor i/2\rfloor$ selama $i>0$. Di dalamnya $j$ dimulai dari 1 dan digandakan selama $j<n$. Di dalamnya lagi $k$ dimulai dari 0 dan bertambah 2 selama $k<n$. Setiap kombinasi menjalankan satu pekerjaan tetap. Tentukan $F(n)$ dan kelasnya.

Untuk $n=8$, tulis nilainya sebelum menebak rumus:

| Indeks | Nilai yang dipakai | Banyak nilai | Mengapa berhenti? |
| --- | --- | ---: | --- |
| $i$ | 8, 4, 2, 1 | 4 | Setelah 1 dibagi dua sebagai integer, hasilnya 0. |
| $j$ | 1, 2, 4 | 3 | Nilai berikutnya 8, tidak memenuhi $j<8$. |
| $k$ | 0, 2, 4, 6 | 4 | Nilai berikutnya 8, tidak memenuhi $k<8$. |

Pada setiap nilai $i$, ketiga loop dalam dimulai lagi dari nilai awalnya. Pada setiap nilai $j$, loop $k$ juga diulang. Jadi $F(8)=4\cdot3\cdot4=48$. Bukan $4+3+4$, karena ketiga pekerjaan tersarang.

Untuk integer $n>1$, loop $i$ memiliki $\lfloor\log_2n\rfloor+1$ nilai. Loop $j$ memiliki $\lceil\log_2n\rceil$ nilai: untuk $n=8$, pangkat 2 yang lebih kecil dari 8 ialah $2^0,2^1,2^2$. Loop $k$ memiliki $\lceil n/2\rceil$ nilai, karena dari setiap dua angka berurutan kita mengambil satu angka genap mulai dari nol. Maka

$$
F(n)=\bigl(\lfloor\log_2n\rfloor+1\bigr)
\bigl(\lceil\log_2n\rceil\bigr)
\bigl(\lceil n/2\rceil\bigr)
\in\Theta(n\log^2n).
$$

Mengapa ada kuadrat pada logaritma? Dua loop pertama masing-masing memiliki sekitar $\log_2n$ putaran, sehingga hasil perkaliannya sekitar $(\log_2n)^2$. Loop ketiga menyumbang sekitar $n/2$. Untuk $n=1$, loop $j$ tidak berjalan dan $F(1)=0$; rumus tepat di atas juga memberi nol. Pernyataan $\Theta(n\log^2n)$ dipakai untuk input yang cukup besar.

Untuk menghitung biaya semua baris, misalkan $a=\lfloor\log_2n\rfloor+1$, $b=\lceil\log_2n\rceil$, dan $c=\lceil n/2\rceil$. Loop $j$ dimulai ulang $a$ kali; loop $k$ dimulai ulang $ab$ kali. Pembagian `i` memakai pembagian bilangan bulat.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `i = n` | 1 | $1$ | $1$ |
| `i > 0` | 1 | $a+1$ | $a+1$ |
| `i = floor(i/2)` | 2 | $a$ | $2a$ |
| `j = 1` | 1 | $a$ | $a$ |
| `j < n` | 1 | $a(b+1)$ | $a(b+1)$ |
| `j *= 2` | 2 | $ab$ | $2ab$ |
| `k = 0` | 1 | $ab$ | $ab$ |
| `k < n` | 1 | $ab(c+1)$ | $ab(c+1)$ |
| `k += 2` | 2 | $abc$ | $2abc$ |
| Pekerjaan tetap | 1 | $abc$ | $abc$ |
| **Jumlah** | | | **$T(n)=2+5a+5ab+4abc$** |

Saat $n=8$, $a=4$, $b=3$, dan $c=4$. Jadi $F(8)=48$, sedangkan $T(8)=2+5(4)+5(4)(3)+4(4)(3)(4)=274$ menurut model biaya ini.

### 3c. Dua loop dalam berurutan pada setiap putaran luar

**Soal sumber.** Loop luar memakai $bound=1,2,4,\ldots$ selama $bound\le n$. Pada *setiap* putaran luar, loop dalam pertama memakai $j=0,2,4,\ldots<n$ dan melakukan satu pekerjaan per nilai. Setelah loop pertama selesai, loop dalam kedua memakai $j=1,2,4,\ldots<n$ dan melakukan satu pekerjaan per nilai. Tentukan $F(n)$ dan kelasnya.

Untuk $n=8$, loop luar mempunyai 1, 2, 4, 8: empat putaran. Loop dalam pertama mempunyai 0, 2, 4, 6: empat pekerjaan. Loop dalam kedua mempunyai 1, 2, 4: tiga pekerjaan. Karena dua loop dalam **tidak saling membungkus**, satu putaran luar berisi $4+3=7$ pekerjaan, bukan $4\cdot3=12$. Seluruhnya $F(8)=4(7)=28$.

Secara umum, banyak putaran luar $\lfloor\log_2n\rfloor+1$ untuk $n\ge1$; loop pertama $\lceil n/2\rceil$; loop kedua $\lceil\log_2n\rceil$ untuk $n>1$ dan nol untuk $n=1$. Maka

$$
F(n)=\bigl(\lfloor\log_2n\rfloor+1\bigr)
\left(\lceil n/2\rceil+\lceil\log_2n\rceil\right)
\in\Theta(n\log n)\quad(n\text{ cukup besar}).
$$

Bagian dalam kurung tumbuh seperti $n$, karena $n/2$ akhirnya lebih besar daripada $\log n$. Bagian luar tumbuh seperti $\log n$. Inilah alasan kelasnya $n\log n$, sedangkan 3b menjadi $n\log^2n$. Bentuk kurung pada rumus mencerminkan letak kurung pada program: *jumlah dua pekerjaan dalam* dikalikan *jumlah pengulangan luar*.

Untuk biaya seluruh baris, tulis $a=\lfloor\log_2n\rfloor+1$, $b=\lceil n/2\rceil$, dan $c=\lceil\log_2n\rceil$. Kedua loop `j` berjalan **berurutan**; tiap loop diinisialisasi kembali pada setiap putaran `bound`.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| `bound = 1` | 1 | $1$ | $1$ |
| `bound <= n` | 1 | $a+1$ | $a+1$ |
| `bound *= 2` | 2 | $a$ | $2a$ |
| `j = 0` (loop pertama) | 1 | $a$ | $a$ |
| `j < n` (loop pertama) | 1 | $a(b+1)$ | $a(b+1)$ |
| `j += 2` | 2 | $ab$ | $2ab$ |
| Pekerjaan tetap pertama | 1 | $ab$ | $ab$ |
| `j = 1` (loop kedua) | 1 | $a$ | $a$ |
| `j < n` (loop kedua) | 1 | $a(c+1)$ | $a(c+1)$ |
| `j *= 2` | 2 | $ac$ | $2ac$ |
| Pekerjaan tetap kedua | 1 | $ac$ | $ac$ |
| **Jumlah** | | | **$T(n)=2+7a+4a(b+c)$** |

Saat $n=8$, $a=4$, $b=4$, dan $c=3$: $F(8)=4(4+3)=28$, sedangkan $T(8)=2+7(4)+4(4)(4+3)=142$. Keduanya tetap $\Theta(n\log n)$.

## 4. Rata-rata: mengapa dua program dengan hasil sama punya biaya berbeda?

Panitia mempunyai array nilai $A[1],A[2],\ldots,A[n]$ dan ingin menghitung rata-ratanya. Kedua algoritme pada lembar responsi menjumlahkan nilai yang sama lalu membagi dengan $n$. Karena itu **hasil rata-ratanya sama** untuk $n>0$; yang dibandingkan adalah jumlah pekerjaan. Jika $n=4$ dan nilainya 2, 4, 6, 8, keduanya memberi $(2+4+6+8)/4=5$.

**Soal sumber nomor 4.** Pelajari contoh penghitungan $F(n)$ pada halaman 3, kemudian isi jumlah pelaksanaan (*kali*) dan satuan waktu (*waktu*) untuk Rata-1 dan Rata-2 pada dua tabel perbandingan di halaman 4. Tentukan algoritme yang lebih baik. Lembar memperlihatkan dua cara menghitung: setiap baris berbiaya satu satuan, dan biaya menurut jenis instruksi. Di sini Plana memakai konvensi yang tertulis pada contoh agar setiap baris bisa diperiksa.

### Mengapa kondisi `while` diperiksa $n+1$ kali?

Rata-1 memakai bentuk `for i = 1 sampai n`: inisialisasi jumlah, pengulangan penjumlahan $n$ kali, lalu pembagian sekali. Rata-2 memakai `while i <= n`: inisialisasi $i$ dan jumlah, memeriksa syarat, menjumlahkan dan menaikkan $i$ selama syarat benar, lalu membagi sekali. Pada $n=4$, syarat `i <= 4` diperiksa saat $i=1,2,3,4$ (benar) **dan** saat $i=5$ (salah, untuk keluar). Jadi ada lima pemeriksaan. Tanpa pemeriksaan terakhir, program belum tahu kapan berhenti.

Pada contoh lembar, baris `for` Rata-1 dihitung $n$ kali sebagai satu baris pengulangan. Itu **konvensi penyederhanaan**; penghitungan yang memisahkan inisialisasi, pemeriksaan akhir, dan kenaikan indeks `for` akan memberi fungsi tepat berbeda. Bagian 4a dan 4b mengikuti bobot khusus yang diminta oleh lembar responsi, sedangkan bagian 3 memakai bobot operasi sederhana seperti `i++` = 2. Karena bobotnya berbeda, jangan mencampur hasil tepat keduanya dalam satu tabel.

### 4a. Setiap pelaksanaan baris berbiaya satu satuan

**Soal lengkap.** Dengan konvensi satu pelaksanaan baris = satu satuan waktu, isilah tabel untuk $n=4$ dan $n$ umum. Baris `for` Rata-1 dihitung $n$ kali, sedangkan pemeriksaan `while` Rata-2 dihitung $n+1$ kali, sesuai contoh lembar.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| Rata-1: `jml ← 0` | 1 | 1 | 1 |
| Rata-1: `for i ← 1 to n` | 1 | $n$ | $n$ |
| Rata-1: `jml ← jml + A[i]` | 1 | $n$ | $n$ |
| Rata-1: `rata ← jml/n` | 1 | 1 | 1 |
| **Jumlah Rata-1** | | | **$T_1(n)=2+2n$** |
| Rata-2: `i ← 1` | 1 | 1 | 1 |
| Rata-2: `jml ← 0` | 1 | 1 | 1 |
| Rata-2: cek `i <= n` | 1 | $n+1$ | $n+1$ |
| Rata-2: `jml ← jml + A[i]` | 1 | $n$ | $n$ |
| Rata-2: `i ← i + 1` | 1 | $n$ | $n$ |
| Rata-2: `rata ← jml/n` | 1 | 1 | 1 |
| **Jumlah Rata-2** | | | **$T_2(n)=4+3n$** |

Untuk Rata-1, dua baris sekali jalan menghasilkan 2, dan dua baris yang masing-masing berjalan $n$ kali menghasilkan $2n$. Untuk Rata-2, tiga baris sekali jalan ditambah **satu pemeriksaan akhir** menghasilkan 4, lalu pemeriksaan berhasil, penjumlahan, dan kenaikan indeks masing-masing menyumbang $n$: total $4+3n$. Pada $n=4$, tabel memberi 10 dan 16, sesuai menghitung satu per satu. Selisih $T_2(n)-T_1(n)=2+n>0$ untuk $n>0$, jadi **Rata-1 lebih murah menurut model 4a**.

### 4b. Biaya tiap jenis instruksi berbeda

**Soal lengkap.** Hitung ulang dua algoritme dengan bobot *per baris* pada contoh lembar. Baris penugasan sederhana dan pemeriksaan logika bernilai $\tfrac12$ satuan; baris `for` Rata-1 bernilai 2 satuan; baris gabungan `jml ← jml + A[i]`, `i ← i + 1`, dan `rata ← jml/n` masing-masing bernilai $1\tfrac12$ satuan. Lembar memperlakukan baris gabungan sebagai satu biaya tetap; jangan menghitung operasi penyusunnya dua kali.

| Code | Cost | Frequency | Total |
| --- | ---: | ---: | ---: |
| Rata-1: `jml ← 0` | $\tfrac12$ | 1 | $\tfrac12$ |
| Rata-1: `for i ← 1 to n` | $2$ | $n$ | $2n$ |
| Rata-1: `jml ← jml + A[i]` | $1\tfrac12$ | $n$ | $1\tfrac12n$ |
| Rata-1: `rata ← jml/n` | $1\tfrac12$ | 1 | $1\tfrac12$ |
| **Jumlah Rata-1** | | | **$T_1(n)=2+3\tfrac12n$** |
| Rata-2: `i ← 1` | $\tfrac12$ | 1 | $\tfrac12$ |
| Rata-2: `jml ← 0` | $\tfrac12$ | 1 | $\tfrac12$ |
| Rata-2: cek `i <= n` | $\tfrac12$ | $n+1$ | $\tfrac12n+\tfrac12$ |
| Rata-2: `jml ← jml + A[i]` | $1\tfrac12$ | $n$ | $1\tfrac12n$ |
| Rata-2: `i ← i + 1` | $1\tfrac12$ | $n$ | $1\tfrac12n$ |
| Rata-2: `rata ← jml/n` | $1\tfrac12$ | 1 | $1\tfrac12$ |
| **Jumlah Rata-2** | | | **$T_2(n)=3+3\tfrac12n$** |

Periksa konstanta Rata-2: $\tfrac12+\tfrac12+\tfrac12+1\tfrac12=3$. Periksa bagian yang berulang: $\tfrac12n+1\tfrac12n+1\tfrac12n=3\tfrac12n$. Pada $n=4$, Rata-1 memakai $2+3{,}5(4)=16$ satuan dan Rata-2 memakai $3+3{,}5(4)=17$ satuan. Selisihnya selalu 1 satuan dalam **model bobot 4b**. Jadi Rata-1 tetap lebih murah menurut model ini, tetapi alasannya berbeda dari 4a. Keduanya tetap $\Theta(n)$ karena sama-sama mengolah $n$ nilai. Kelas yang sama tidak berarti waktu tepatnya sama.

**Batas kesimpulan.** Tabel halaman 4 menyediakan tempat kosong tanpa menetapkan bobot baru untuk perbandingan kedua. Di sini 4a dan 4b memakai *dua konvensi contoh* pada halaman 3 supaya kedua perbandingan dapat dikerjakan secara transparan. Jika pengajar memberi bobot lain untuk 4b, ganti kolom “biaya per kali” lalu jumlahkan ulang; jangan menganggap angka waktu di atas berlaku untuk semua model komputer. Perintah `for` pada program nyata pun dapat diurai lebih rinci, sehingga model hitung yang berbeda dapat menghasilkan fungsi tepat lain walaupun kelasnya tetap linear.

## Cara memakai bab ini saat mengerjakan responsi

1. Untuk nomor 1, tulis semua suku, bandingkan pertumbuhannya saat $n$ besar, lalu pisahkan *suku dominan* dari *kelas Big-O*.
2. Untuk nomor 2, samakan satuan, selesaikan persamaan waktu kedua paket, dan cek seluruh rentang $n$ yang ditanyakan.
3. Untuk nomor 3, tulis nilai indeks pada $n$ kecil. Jumlahkan loop berurutan dan kalikan loop bersarang hanya setelah melihat jumlah putarannya.
4. Untuk nomor 4, isi kolom “kali” dahulu, baru kalikan bobot waktu. Pemeriksaan `while` yang terakhir tetap dihitung meskipun badan loop tidak dijalankan.

Latihan bertingkat tersedia di [Latihan Bab 2](latihan-bab-02.md). Soal latihan ditulis dengan konteks dan asal masing-masing. **Sumber utama bab:** *Lembar Kerja Responsi Pertemuan 2 Analgor, semester ganjil 2026–2027*, halaman 1–4. Ungkapan soal di sini ditulis ulang untuk belajar; contoh panitia dan input kecil ditambahkan sebagai penjelas.
