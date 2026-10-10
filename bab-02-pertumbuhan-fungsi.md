# Bab 2 — Mengapa Waktu Program Bertambah Saat Data Bertambah?

> Pertanyaan bab ini: Ketika daftar berisi 10, 100, lalu sejuta nama, bagaimana pekerjaan pencarian berubah?

Bab ini memakai satu cerita sebagai benang merah. Kita mulai dengan mencari nama dalam daftar, menghitung pekerjaan yang nyata, lalu menulis fungsi biaya. Sesudah itu barulah kita mempelajari laju pertumbuhan dan notasi $O$, $\Omega$, serta $\Theta$. Di bagian akhir, cara yang sama dipakai untuk soal responsi. Setiap contoh menyebut soal lengkapnya terlebih dahulu.

**Peta jalan:** daftar nama → banyak perbandingan → fungsi $T(n)$ → pola pertumbuhan → batas formal → soal loop dan pilihan paket.

## 1. Mencari nama dalam daftar

Sensei mempunyai daftar peserta [Ari, Bima, Citra, Danu, Nisa] yang belum diurutkan. Untuk mencari “Nisa”, kita dapat membandingkan nama pertama dengan target, lalu melanjutkan sampai cocok atau sampai daftar habis.

| Target | Letak | Perbandingan |
| --- | ---: | ---: |
| Ari | Pertama | 1 |
| Citra | Ketiga | 3 |
| Nisa | Kelima | 5 |
| Rani | Tidak ada | 5 |

Kita memilih *banyak nama* sebagai **ukuran input**, ditulis $n$. Kita memilih *satu perbandingan nama dengan target* sebagai **operasi dasar**. Pilihan ini membuat kalimat “program bekerja lebih banyak” dapat dihitung.

**Soal lengkap.** Daftar berisi $n$ nama. Target tidak ada dalam daftar. Berapa perbandingan?

Setiap nama harus dibandingkan sekali. Ada $n$ nama, sehingga

$$
T(n)=\underbrace{1+1+\cdots+1}_{n\text{ kali}}=n.
$$

Untuk lima nama, $T(5)=5$; untuk seratus nama, $T(100)=100$. Namun jika target ada di posisi ketiga, hanya tiga perbandingan. Jadi fungsi tadi berlaku untuk skenario *target tidak ada*. Pada Bab 3, kita akan membedakan kasus terbaik, rata-rata, dan terburuk.

Ukuran input tidak selalu satu angka. Pada perkalian matriks berukuran $n\times m$ dan $m\times p$, ada $np$ posisi hasil dan setiap posisi membutuhkan $m$ perkalian bilangan. Jadi banyak perkalian pada cara biasa ialah $nmp$. Untuk graf, jumlah simpul $V$ dan sisi $E$ sering lebih berguna daripada satu $n$. Ukuran harus mengikuti masalahnya.

## 2. Dari pekerjaan ke biaya

**Soal lengkap.** Persiapan program memerlukan 20 satuan waktu. Memeriksa satu nama memerlukan 3 satuan waktu. Berapa biaya jika semua $n$ nama diperiksa?

Persiapan dilakukan **sekali**, jadi biayanya 20. Pemeriksaan dilakukan **sebanyak $n$ kali**, masing-masing berbiaya 3, jadi $3n$. Kedua pekerjaan dilakukan, sehingga dijumlahkan:

$$
T(n)=20+3n.
$$

Pada $n=5$, biayanya $20+3(5)=35$. Pada $n=100$, biayanya 320; pada $n=200$, 620. Ukuran dua kali lebih besar membuat biaya *hampir* dua kali, tetapi tidak tepat: $620/320=1{,}9375$. Biaya persiapan tetap dibayar sekali.

Ada dua pertanyaan yang harus dipisahkan. “Berapa $T(100)$?” membutuhkan angka 20 dan 3. “Bagaimana biaya tumbuh ketika $n$ sangat besar?” terutama melihat bentuk $n$. Konstanta tidak boleh dihapus ketika menghitung waktu pada ukuran tertentu.

## 3. Empat pola pertumbuhan dari pekerjaan nyata

### 3.1 Konstan

**Soal lengkap.** Program mengambil elemen pertama dari array yang sudah tersedia. Berapa akses elemen pada array berisi 10, 100, atau 1.000 elemen?

Dalam model akses langsung, jawabannya satu pada ketiga ukuran: $T(n)=1$. “Konstan” berarti banyak akses yang kita hitung tidak meningkat bersama $n$, bukan berarti semua komputer pasti memerlukan satu detik.

### 3.2 Linear

Pencarian target yang tidak ada memeriksa $n$ nama, jadi $T(n)=n$. Jika jumlah nama digandakan, banyak perbandingan juga digandakan. Itulah pola linear.

### 3.3 Kuadrat

**Soal lengkap.** Untuk setiap satu dari $n$ nama, program membandingkannya dengan *semua* $n$ nama, termasuk dirinya sendiri. Berapa perbandingan?

Nama pertama menghasilkan $n$ perbandingan. Begitu juga nama kedua, sampai nama ke-$n$. Ada $n$ kelompok yang masing-masing berisi $n$ pekerjaan:

$$
T(n)=\underbrace{n+n+\cdots+n}_{n\text{ kelompok}}=n^2.
$$

Untuk $n=4$, hitungannya $4+4+4+4=16$. Untuk $n=8$, hasilnya 64. Dua kali lebih banyak data membuat **dua faktor $n$** sama-sama dua kali, sehingga pekerjaan menjadi empat kali. Jika soal melarang membandingkan nama dengan dirinya atau menganggap pasangan A–B sama dengan B–A, jumlah tepatnya berubah. Bacalah syaratnya.

### 3.4 Logaritmik

**Soal lengkap.** Ada 16 kartu yang *sudah diurutkan*. Setiap langkah memungkinkan kita menentukan separuh mana yang mungkin berisi target dan membuang separuh lain. Berapa pembagian sampai tinggal satu kartu?

Ukuran kandidat berubah $16\to8\to4\to2\to1$. Ada empat panah, jadi empat pembagian. Karena $16=2^4$, banyak pembagian ditulis $\log_2 16=4$. Untuk 32 kartu, dibutuhkan lima pembagian: $32\to16\to8\to4\to2\to1$.

Syarat “sudah diurutkan” penting. Tanpa cara mengetahui separuh yang benar, kita bisa membuang target. Di sini yang dihitung ialah *tingkat pembagian*, bukan jumlah perbandingan tepat dalam semua versi binary search.

| $n$ | 1 | 2 | 4 | 8 | 16 |
| ---: | ---: | ---: | ---: | ---: | ---: |
| $\log_2n$ | 0 | 1 | 2 | 3 | 4 |
| $n$ | 1 | 2 | 4 | 8 | 16 |
| $n^2$ | 1 | 4 | 16 | 64 | 256 |

Tabel membantu melihat pola, tetapi beberapa nilai kecil saja belum membuktikan perilaku untuk semua $n$ besar.

## 4. Mengapa ada suku dominan?

Pertimbangkan $T(n)=4n^2+100n+7$. Pada $n=1$, suku $100n$ lebih besar daripada $4n^2$; jadi “dominan” bukan berarti terbesar pada setiap ukuran. Kita ingin tahu apa yang terjadi ketika $n$ terus membesar.

Karena $n>0$, bagi semua suku dengan $n^2$:

$$
\frac{T(n)}{n^2}
=\frac{4n^2}{n^2}+\frac{100n}{n^2}+\frac7{n^2}
=4+\frac{100}{n}+\frac7{n^2}.
$$

Mengapa $100n/n^2=100/n$? Penyebut $n^2=n\cdot n$. Satu faktor $n$ di atas dan bawah dapat dicoret karena $n\ne0$. Saat $n$ bertambah, $100/n$ dan $7/n^2$ mendekati nol. Perbandingan $T(n)/n^2$ mendekati 4. Jadi bentuk pertumbuhan yang paling menentukan ialah $n^2$.

**Jangan pakai suku dominan sebagai waktu tepat.** Pada $n=10$, $T(10)=4(100)+100(10)+7=1407$, bukan 400. Pengabaian suku kecil hanya menjelaskan laju pertumbuhan.

Mengganti basis logaritma juga hanya mengubah faktor konstan: $\log_a n=\log_b n/\log_b a$ untuk basis positif selain 1. Saat mencari banyak langkah tepat, basisnya tetap perlu diketahui.

## 5. Tiga jenis batas

Bayangkan tinggi rak. “Paling tinggi dua meter” adalah batas atas. “Paling rendah satu meter” adalah batas bawah. Untuk fungsi, pembatasnya adalah kelipatan fungsi lain yang berlaku mulai suatu ukuran input. Kita membahas fungsi biaya yang tidak negatif.

### 5.1 $O$: batas atas

$f(n)\in O(g(n))$ berarti ada konstanta $c>0$ dan ukuran awal $n_0$ sehingga

$$
f(n)\le c\,g(n)\qquad\text{untuk setiap }n\ge n_0.
$$

**Soal lengkap.** Buktikan $3n+8\in O(n)$. Tunjukkan nilai $c$ dan $n_0$.

Untuk $n\ge1$, berlaku $8\le8n$. Tambahkan $3n$ pada kedua sisi:

$$
3n+8\le3n+8n=11n.
$$

Maka $c=11,n_0=1$ bekerja. Konstanta itu tidak wajib paling kecil; cukup membuat ketaksamaan benar. Kalimat “buang 8” belum menjelaskan alasan; ketaksamaan di atas menjelaskannya.

### 5.2 $\Omega$: batas bawah

$f(n)\in\Omega(g(n))$ berarti ada $c>0,n_0$ sehingga $f(n)\ge c\,g(n)$ untuk semua $n\ge n_0$. Untuk contoh tadi, $3n+8\ge3n$ karena 8 positif. Pilih $c=3,n_0=1$.

### 5.3 $\Theta$: kedua batas sekaligus

$f(n)\in\Theta(g(n))$ berarti ada $c_1,c_2>0,n_0$ sehingga

$$
c_1g(n)\le f(n)\le c_2g(n)\qquad(n\ge n_0).
$$

Kita sudah mendapat $3n\le3n+8\le11n$ pada $n\ge1$. Jadi $3n+8\in\Theta(n)$.

**Soal lengkap.** Buktikan kelas pertumbuhan ketat $f(n)=3n^2+5n+2$.

Untuk $n\ge1$, $n\le n^2$: kalikan $n\ge1$ dengan $n>0$. Juga $1\le n^2$. Maka $5n\le5n^2$ dan $2\le2n^2$. Jumlahkan:

$$
f(n)\le3n^2+5n^2+2n^2=10n^2.
$$

Sebaliknya, $5n+2$ tidak negatif, sehingga $f(n)\ge3n^2$. Jadi $3n^2\le f(n)\le10n^2$ untuk $n\ge1$; kesimpulannya $f(n)\in\Theta(n^2)$.

Batas atas bisa longgar: $n\in O(n^2)$ karena $n\le n^2$ pada $n\ge1$, tetapi $n\notin\Theta(n^2)$. Jika diminta kelas yang paling informatif, cari batas dari kedua sisi.

**Dua istilah berbeda:** *worst case* memilih input yang paling berat di antara input berukuran sama. Big-O menyatakan batas atas untuk fungsi biaya yang telah dipilih. Worst case tidak identik dengan Big-O; Bab 3 menjelaskan kasus-kasusnya.

## 6. Urutan pertumbuhan dan pilihan nyata

Untuk ukuran yang terus membesar, urutan umum ialah

$$
1\prec\log n\prec n\prec n\log n\prec n^2\prec n^3\prec2^n\prec n!.
$$

Tanda $\prec$ berarti fungsi kiri akhirnya tumbuh lebih lambat. $n\log n$ memiliki faktor $\log n$ tambahan dibanding $n$. Untuk membandingkan $n\log n$ dan $n^2$, bagi keduanya dengan $n>0$: tinggal membandingkan $\log n$ dan $n$. Fungsi $2^n$ berlipat dua saat $n$ naik satu; $n!$ menghitung urutan semua $n$ benda berbeda.

Namun kelas pertumbuhan **tidak cukup** untuk memilih program pada ukuran tertentu.

**Soal lengkap.** Paket A membutuhkan $100n$ satuan kerja, sedangkan B membutuhkan $n^2$. Mana lebih murah pada $n=10$ dan $n=1000$? Kapan keduanya sama?

Pada $n=10$, A = 1000 dan B = 100, jadi B lebih murah. Pada $n=1000$, A = 100.000 dan B = 1.000.000, jadi A lebih murah. Untuk titik sama, tulis $100n=n^2$. Karena $n>0$, bagi **kedua sisi** dengan $n$, sehingga $100=n$. Titik potongnya 100. Menguji nilai di kiri dan kanan titik potong menunjukkan arah perbandingan.

### 6.1 Dua paket dalam responsi: logaritma

**Soal lengkap (adaptasi Responsi Pertemuan 2).** Paket A memerlukan $T_A(n)=0{,}1n\log_2n$ mikrodetik dan paket B $T_B(n)=5n$ mikrodetik. Mana lebih cepat untuk basis data hingga $10^{12}$ record?

Satuannya sama. Samakan biayanya: $0{,}1n\log_2n=5n$. Karena $n>0$, bagi kedua sisi dengan $n$: $0{,}1\log_2n=5$. Bagi dengan $0{,}1$: $\log_2n=50$, yang berarti $n=2^{50}\approx1{,}126\times10^{15}$.

Karena $10^{12}<2^{50}$, pada rentang yang ditanyakan berlaku $0{,}1\log_2n<5$; kalikan dengan $n>0$ dan dapat $T_A(n)<T_B(n)$. Jadi **A lebih cepat**. Pada $n=10^{12}$, $\log_2n\approx39{,}86$, maka A sekitar $3{,}986n$ mikrodetik dan B $5n$. Pada ukuran jauh di atas titik potong, B akhirnya unggul.

### 6.2 Dua paket dalam responsi: akar

**Soal lengkap (adaptasi Responsi Pertemuan 2).** Paket A memerlukan $0{,}001n$ milidetik dan B $500\sqrt n$ milidetik. Mana lebih cepat untuk hingga $10^9$ record?

Samakan: $0{,}001n=500\sqrt n$. Untuk $n>0$, bagi kedua sisi dengan $\sqrt n$. Karena $n=\sqrt n\cdot\sqrt n$, diperoleh $0{,}001\sqrt n=500$. Bagi lagi dengan $0{,}001$: $\sqrt n=500.000$. Kuadratkan kedua sisi: $n=250.000.000.000=2{,}5\times10^{11}$.

Pada $10^9$, A = $10^6$ ms, sedangkan B $\approx1{,}581\times10^7$ ms. Jadi A lebih cepat pada batas soal. Setelah titik potong, B akhirnya lebih cepat karena $\sqrt n$ tumbuh lebih lambat daripada $n$.

## 7. Menghitung loop dari nilai indeksnya

Pada soal responsi, $F(n)$ kita pakai untuk banyak pelaksanaan operasi di bagian terdalam. Jika tiap operasi berbiaya konstan positif, kelas waktu mengikuti $F(n)$. **Tulis nilai indeks untuk ukuran kecil sebelum menggunakan rumus.**

### 7.1 Tiga loop yang panjangnya sama

**Soal lengkap (adaptasi Responsi 2 nomor 3a).** Ada tiga loop bersarang. Masing-masing mulai dari 0, naik satu, dan berhenti sebelum $n$. Bagian terdalam melakukan satu operasi. Berapa operasinya?

Pada $n=2$, setiap indeks mempunyai nilai 0 dan 1. Ada $2\cdot2\cdot2=8$ kombinasi. Untuk $n$ umum, tiap indeks mempunyai $n$ nilai dan panjangnya tidak bergantung pada indeks lain. Maka $F(n)=n\cdot n\cdot n=n^3$, sehingga $\Theta(n^3)$.

### 7.2 Panjang loop dalam berubah

**Soal lengkap.** Indeks luar bernilai $i=1,2,\ldots,n$. Pada tiap nilai $i$, loop dalam melakukan tepat $i$ operasi. Berapa totalnya?

Untuk $n=4$, pekerjaan per putaran ialah 1, 2, 3, dan 4. Total 10, **bukan** $4\cdot4=16$. Secara umum

$$
F(n)=1+2+\cdots+n=\frac{n(n+1)}2.
$$

Rumus jumlah ini berasal dari memasangkan ujung deret, seperti di Bab 1. Untuk $n\ge1$, $n\le n+1\le2n$. Kalikan semua sisi dengan $n/2>0$: $n^2/2\le F(n)\le n^2$. Jadi $F(n)\in\Theta(n^2)$, walaupun nilai tepatnya bukan $n^2$.

### 7.3 Loop yang menggandakan indeks

**Soal lengkap.** Indeks dimulai dari 1, dikali 2 setelah tiap putaran, dan berjalan selama $i<n$. Berapa putaran pada $n=16$ dan $n=17$?

Pada $n=16$, nilai yang diproses ialah 1, 2, 4, 8: empat putaran. Nilai 16 tidak masuk karena syaratnya $i<16$. Pada $n=17$, nilai 16 ikut: lima putaran. Untuk $n>1$, banyak putaran tepatnya $\lceil\log_2n\rceil$. Jika syarat berubah menjadi $i\le n$, hitungan tepat pada pangkat dua berubah. Selalu baca tanda $<$ dan $\le$.

### 7.4 Tiga pola bersarang dari responsi

**Soal lengkap (adaptasi Responsi 2 nomor 3b).** Loop $i$ mulai dari $n$, dibagi dua dengan pembagian bilangan bulat selama $i>0$. Di dalamnya loop $j$ mulai dari 1, dikalikan 2 selama $j<n$. Di dalamnya lagi loop $k$ mulai dari 0, ditambah 2 selama $k<n$. Hitung operasi terdalam untuk $n=8$, lalu kelasnya.

Untuk $n=8$, nilai $i$: 8, 4, 2, 1 (empat); $j$: 1, 2, 4 (tiga); $k$: 0, 2, 4, 6 (empat). Ketiganya bersarang, jadi $4\cdot3\cdot4=48$.

Untuk $n>1$, banyak nilai masing-masing ialah $\lfloor\log_2n\rfloor+1$, $\lceil\log_2n\rceil$, dan $\lceil n/2\rceil$. Maka

$$
F(n)=(\lfloor\log_2n\rfloor+1)\lceil\log_2n\rceil\lceil n/2\rceil
\in\Theta(n\log^2n).
$$

Dua faktor pertama tumbuh seperti $\log n$; faktor terakhir seperti $n$. Jadi tiga loop di sini **bukan** $\Theta(n^3)$.

### 7.5 Dua loop *berurutan* di dalam loop luar

**Soal lengkap (adaptasi Responsi 2 nomor 3c).** Loop luar menggunakan nilai bound = 1, 2, 4, ... selama bound $\le n$. Pada setiap putaran luar, loop pertama memakai $j=0,2,4,\ldots<n$. *Sesudahnya*, loop kedua memakai $j=1,2,4,\ldots<n$. Tiap putaran dalam melakukan satu operasi. Hitung untuk $n=8$ dan kelasnya.

Pada $n=8$, bound bernilai 1, 2, 4, 8: empat putaran. Loop pertama memakai 0, 2, 4, 6: empat operasi. Loop kedua memakai 1, 2, 4: tiga operasi. Karena kedua loop dalam **berurutan**, biaya satu putaran luar $4+3=7$, bukan $4\cdot3$. Total $4(7)=28$.

Secara umum,

$$
F(n)=(\lfloor\log_2n\rfloor+1)
\left(\lceil n/2\rceil+\lceil\log_2n\rceil\right)
\in\Theta(n\log n).
$$

Jumlah dalam kurung tumbuh seperti $n$; jumlah itu diulang sekitar $\log n$ kali.

## 8. Jika ukuran input digandakan

**Soal lengkap (tema Kuliah 2).** Sebuah algoritme memerlukan 1 detik pada ukuran 8. Perkirakan waktu pada ukuran 16 jika model pekerjaan dominannya berturut-turut $1$, $\log_2n$, $n$, $n\log_2n$, $n^2$, $n^3$, atau $2^n$.

Jika waktu kira-kira $a f(n)$ dengan konstanta mesin $a$ yang sama pada kedua ukuran, perbandingan waktunya kira-kira $f(16)/f(8)$: faktor $a$ saling habis.

| Model $f(n)$ | Rasio $f(16)/f(8)$ | Perkiraan |
| --- | ---: | ---: |
| $1$ | 1 | 1 detik |
| $\log_2n$ | $4/3$ | $4/3$ detik |
| $n$ | $16/8=2$ | 2 detik |
| $n\log_2n$ | $(16\cdot4)/(8\cdot3)=8/3$ | $8/3$ detik |
| $n^2$ | $16^2/8^2=4$ | 4 detik |
| $n^3$ | $16^3/8^3=8$ | 8 detik |
| $2^n$ | $2^{16}/2^8=256$ | 256 detik |

Ini **perkiraan bersyarat**, bukan akibat otomatis dari label Big-O. $T(n)=n$ juga termasuk $O(n^2)$, tetapi rasionya ketika digandakan adalah dua, bukan empat. Bahkan $T(n)=n^2+1000$ tidak mempunyai rasio tepat empat pada 8 dan 16.

## 9. Urutan kerja saat mengerjakan soal

1. Sebutkan ukuran input dan operasi yang dihitung.
2. Nyatakan skenario atau syarat: target ada di mana, data sudah terurut atau belum, dan pembagian indeks memakai bilangan bulat atau bukan.
3. Coba $n=4$ atau $n=8$; tulis nilai indeks satu per satu.
4. Jumlahkan tahap yang berurutan. Kalikan loop bersarang jika panjangnya independen. Jika panjang loop dalam bergantung pada indeks luar, jumlahkan pekerjaan per indeks.
5. Tulis fungsi tepat bila mungkin, lalu buktikan $O$, $\Omega$, atau $\Theta$ sesuai pertanyaan.
6. Untuk memilih program pada rentang nyata, samakan satuan, cari titik potong, lalu uji ukuran yang ditanyakan.

## 10. Latihan bertingkat

1. **Mudah.** Daftar tidak terurut berisi tujuh nama. Target tidak ada dan tiap nama dibandingkan sekali. Berapa perbandingan? Tulis $T(n)$ untuk $n$ nama.
2. **Mudah.** Program menyiapkan data selama 12 satuan waktu, lalu memproses setiap item selama 4 satuan. Tulis $T(n)$, $T(5)$, dan $T(10)$.
3. **Mudah.** Daftar terurut memiliki 32 kandidat. Tuliskan seluruh ukuran kelompok saat terus dibagi dua sampai satu, lalu hitung pembagiannya.
4. **Mudah.** Buktikan $6n+12\in O(n)$ dengan $c,n_0$. Apakah juga $\Omega(n)$?
5. **Sedang.** Untuk $T(n)=5n^3+100n+20$, tentukan $\Theta$ paling ketat dengan batas atas dan bawah untuk $n\ge1$.
6. **Sedang.** Tahap A melakukan $n^2$ operasi, lalu tahap B melakukan $20n$. Berapa total dan kelasnya? Mengapa tidak dikalikan?
7. **Sedang.** Untuk setiap $i=1,2,\ldots,n$, program melakukan $i$ perbandingan. Hitung untuk $n=5$, tulis $F(n)$, dan buktikan kelasnya.
8. **Sedang, adaptasi Responsi 2 nomor 3a.** Tiga loop bersarang, masing-masing dari 0 sampai sebelum $n$, naik satu. Hitung operasi terdalam untuk $n=3$ dan $n$ umum.
9. **Sedang, adaptasi Responsi 2 nomor 3b.** Tiga loop bersarang: $i$ mulai $n$ lalu dibagi dua dengan pembagian bulat selama positif; $j$ mulai 1 lalu dikali dua selama $j<n$; $k$ mulai 0 lalu ditambah dua selama $k<n$. Hitung untuk $n=8$ dan tentukan $\Theta$.
10. **Sedang, adaptasi Responsi 2 nomor 3c.** Loop luar menggandakan bound mulai 1 selama bound $\le n$. Di dalamnya ada dua loop berurutan: $j=0,2,4,\ldots<n$, lalu $j=1,2,4,\ldots<n$. Hitung untuk $n=8$ dan tentukan $\Theta$.
11. **Sulit, adaptasi Responsi 2 nomor 2a.** Paket A memerlukan $0{,}1n\log_2n$ mikrodetik dan B $5n$. Cari titik potong. Pilih pada $n=2^{40}$ dan $n=2^{60}$.
12. **Sulit, adaptasi Responsi 2 nomor 2b.** Paket A memerlukan $0{,}001n$ milidetik dan B $500\sqrt n$. Cari titik potong positif dan pilih pada $n=10^9$.
13. **Sulit.** Algoritme terukur 1 detik pada $n=8$. Perkirakan pada $n=16$ jika model dominannya $n^3$. Mengapa label $O(n^3)$ saja tidak memastikan angka itu?
14. **Sulit.** Tunjukkan $n\in O(n^2)$ untuk $n\ge1$, lalu jelaskan mengapa $n\notin\Theta(n^2)$.
15. **Sulit, adaptasi UTS 2018.** $f_A(n)=2n^2+975n+90$ dan $f_B(n)=n^2+75n+90$, untuk $n>0$. Adakah ukuran positif saat B memerlukan lebih banyak pekerjaan? Apakah kelas $\Theta$ keduanya sama?
16. **Tantangan.** Seseorang berkata, “Kompleksitas $O(n^2)$ berarti waktu pasti empat kali jika input digandakan.” Beri dua alasan mengapa belum tentu dan satu fungsi contoh.

## 11. Pembahasan latihan tanpa lompatan

### 1. Daftar tujuh nama

**Soal.** Tujuh nama diperiksa ketika target tidak ada; cari pula $T(n)$.

Ada tujuh pekerjaan satu perbandingan, jadi $1+1+1+1+1+1+1=7$. Untuk $n$ nama, jumlahnya $T(n)=n$. Karena persis sebanding dengan $n$, kelasnya $\Theta(n)$.

### 2. Biaya persiapan

**Soal.** Persiapan 12 satuan dan 4 satuan per item.

Persiapan terjadi sekali, pemrosesan terjadi $n$ kali: $T(n)=12+4n$. Untuk lima item $T(5)=12+4(5)=32$; untuk sepuluh item $T(10)=12+4(10)=52$. Lima item tambahan menambah $5\cdot4=20$ satuan.

### 3. Pembagian dua

**Soal.** Dari 32 kandidat sampai satu.

Urutannya $32\to16\to8\to4\to2\to1$. Ada lima panah, jadi lima pembagian. Cek: $2^5=32$, maka $\log_2 32=5$.

### 4. Dua batas fungsi linear

**Soal.** Buktikan batas $6n+12$.

Untuk $n\ge1$, $12\le12n$. Tambahkan $6n$: $6n+12\le18n$. Jadi $c=18,n_0=1$ membuktikan $O(n)$. Karena 12 tidak negatif, $6n+12\ge6n$; $c=6,n_0=1$ membuktikan $\Omega(n)$. Dua batas memberi $\Theta(n)$.

### 5. Suku kubik

**Soal.** Buktikan kelas $5n^3+100n+20$.

Untuk $n\ge1$, $n\le n^3$ dan $1\le n^3$. Maka $100n\le100n^3$ dan $20\le20n^3$, sehingga $T(n)\le125n^3$. Karena suku tambahan tidak negatif, $T(n)\ge5n^3$. Dua batas ini membuktikan $\Theta(n^3)$.

### 6. Tahap berurutan

**Soal.** $n^2$ operasi disusul $20n$ operasi.

Totalnya $T(n)=n^2+20n$, sebab tahap kedua tidak diulang pada setiap operasi tahap pertama. Pada $n\ge1$, $n\le n^2$, sehingga $n^2\le T(n)\le21n^2$. Maka $\Theta(n^2)$.

### 7. Panjang loop berubah

**Soal.** Pada nilai $i$ dilakukan $i$ perbandingan, dari $i=1$ sampai $n$.

Untuk $n=5$, $1+2+3+4+5=15$. Umumnya $F(n)=n(n+1)/2$. Pada $n\ge1$, $n\le n+1\le2n$. Kalikan semua ruas dengan $n/2>0$: $n^2/2\le F(n)\le n^2$. Jadi $\Theta(n^2)$. Nilai tepat pada $n=5$ tetap 15, bukan 25.

### 8. Tiga loop panjang $n$

**Soal.** Tiga loop bersarang masing-masing mempunyai $n$ nilai indeks.

Untuk $n=3$, tiap indeks bisa 0, 1, atau 2. Ada $3\cdot3\cdot3=27$ kombinasi. Umumnya $F(n)=n^3$, sehingga $\Theta(n^3)$.

### 9. Tiga pola bersarang

**Soal.** Indeks luar dibagi dua, tengah dikali dua, dalam ditambah dua.

Pada $n=8$, $i$ bernilai 8, 4, 2, 1 (4 nilai); $j$ bernilai 1, 2, 4 (3 nilai); $k$ bernilai 0, 2, 4, 6 (4 nilai). Total $4\cdot3\cdot4=48$. Umumnya $F(n)=(\lfloor\log_2n\rfloor+1)\lceil\log_2n\rceil\lceil n/2\rceil$, sehingga $\Theta(n\log^2n)$.

### 10. Dua loop berurutan

**Soal.** Loop luar menggandakan bound; di dalamnya dua loop berjalan satu setelah yang lain.

Pada $n=8$, luar mempunyai 1, 2, 4, 8 (4 putaran); loop dalam pertama 0, 2, 4, 6 (4); kedua 1, 2, 4 (3). Setiap putaran luar berbiaya $4+3=7$, total $4(7)=28$. Umumnya $F(n)=(\lfloor\log_2n\rfloor+1)(\lceil n/2\rceil+\lceil\log_2n\rceil)$, sehingga $\Theta(n\log n)$.

### 11. Paket logaritmik

**Soal.** Bandingkan $0{,}1n\log_2n$ dengan $5n$ pada $2^{40}$ dan $2^{60}$.

Setarakan, bagi dengan $n>0$, lalu dengan $0{,}1$: $\log_2n=50$, maka titik potong $n=2^{50}$. Pada $2^{40}$, A berbiaya $4n<5n$, jadi A lebih cepat. Pada $2^{60}$, A berbiaya $6n>5n$, jadi B lebih cepat.

### 12. Paket akar

**Soal.** Bandingkan $0{,}001n$ dan $500\sqrt n$ pada $10^9$.

Setarakan. Bagi kedua ruas dengan $\sqrt n>0$: $0{,}001\sqrt n=500$. Bagi dengan $0{,}001$: $\sqrt n=500.000$. Kuadratkan: $n=2{,}5\times10^{11}$. Pada $10^9$, A = $10^6$ ms dan B $\approx1{,}581\times10^7$ ms; A lebih cepat.

### 13. Perkiraan kubik

**Soal.** Satu detik pada 8; perkirakan pada 16.

Rasionya $16^3/8^3=(16/8)^3=8$, jadi perkiraannya delapan detik *jika* model kubik sudah dominan pada dua ukuran itu. Label $O(n^3)$ hanya batas atas. Fungsi $T(n)=n$ juga berada dalam $O(n^3)$, tetapi rasionya dua.

### 14. Batas longgar

**Soal.** Tunjukkan $n\in O(n^2)$, tetapi bukan $\Theta(n^2)$.

Untuk $n\ge1$, $n\le n^2$; pilih $c=1,n_0=1$. Agar $\Theta(n^2)$, harus ada $c_1>0$ sehingga $n\ge c_1n^2$ untuk semua $n$ besar. Bagi dengan $n>0$: $1\ge c_1n$. Sisi kanan terus bertambah; ketaksamaan tidak mungkin terus berlaku.

### 15. Dua fungsi kuadrat

**Soal.** Bandingkan $2n^2+975n+90$ dengan $n^2+75n+90$ untuk $n>0$.

Kurangkan B dari A: $(2n^2-n^2)+(975n-75n)+(90-90)=n^2+900n>0$. Maka A selalu lebih besar, sehingga B tidak pernah lebih lambat menurut fungsi biaya ini. Keduanya tetap $\Theta(n^2)$: sama-sama diapit oleh kelipatan $n^2$ untuk $n$ besar. Kelas sama tidak berarti biaya tepat sama.

### 16. Klaim “pasti empat kali”

**Soal.** Apakah $O(n^2)$ menjamin rasio empat saat $n$ digandakan?

Tidak. Pertama, $O(n^2)$ hanya batas atas. $T(n)=n$ juga memenuhinya tetapi rasionya dua. Kedua, bahkan fungsi $\Theta(n^2)$ dapat memiliki biaya tambahan. $T(n)=n^2+1000$ berubah dari 1100 pada $n=10$ menjadi 1400 pada $n=20$, bukan 4400. Rasio empat hanya pendekatan ketika suku kuadrat sudah dominan.

## 12. Ringkasan untuk tutor

Mulailah dengan lima nama dan hitung perbandingannya. Setelah peserta melihat asal $T(n)$, jelaskan tiga batas lewat satu fungsi yang diapit dua ketaksamaan. Untuk soal loop, tulis nilai indeks pada $n=8$ sebelum memakai logaritma. Untuk memilih paket, samakan satuan, cari titik potong, dan uji ukuran yang benar-benar ditanyakan.

**Sumber:** *Kuliah 2 Analgor 2026–2027*, *Lembar Kerja Responsi Pertemuan 2*, bank soal K2, dan UTS 2018 dari arsip Sensei. Soal berlabel adaptasi ditulis ulang untuk belajar. Bagian responsi yang berupa gambar tanpa teks terbaca tidak dipakai untuk mengklaim hitungan tertentu.
