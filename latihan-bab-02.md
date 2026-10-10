# Latihan Bab 2 — Pertumbuhan Fungsi

Bacaan pendamping: [bab-02-pertumbuhan-fungsi.md](bab-02-pertumbuhan-fungsi.md). Kerjakan soal sebelum membuka pembahasan di bagian bawah. Semua konteks yang dibutuhkan ada pada masing-masing soal.

**Asal soal.** “Adaptasi” berarti isi soal sumber ditulis ulang atau diberi syarat penjelas; “dikembangkan dari” berarti pertanyaan diperluas. Soal baru dibuat untuk panduan ini. Nama dan nomor sumber tercantum pada setiap soal. PDF sumber tidak disertakan di repositori ini.

## Soal

### 1. Daftar tujuh nama

*Tingkat: Mudah.*

**Soal lengkap.** Sebuah pencarian membandingkan target dengan nama-nama dalam daftar yang tidak terurut. Daftar berisi tujuh nama, target tidak ada, dan setiap nama dibandingkan tepat sekali. Berapa perbandingan? Jika daftar berisi $n$ nama dengan kondisi yang sama, berapa $T(n)$?

**Asal:** Soal latihan baru untuk panduan ini.

### 2. Biaya persiapan

*Tingkat: Mudah.*

**Soal lengkap.** Program menyiapkan data selama 12 satuan waktu, lalu memproses setiap item selama 4 satuan. Tulis $T(n)$, $T(5)$, dan $T(10)$.

**Asal:** Soal latihan baru untuk panduan ini.

### 3. Pembagian dua

*Tingkat: Mudah.*

**Soal lengkap.** Sebuah proses selalu membagi kumpulan kandidat menjadi dua bagian sama besar dan meneruskan satu bagian. Mula-mula ada 32 kandidat. Tuliskan ukuran kumpulan sejak 32 sampai tersisa satu, lalu hitung banyak pembagiannya. Anggap 32 adalah pangkat dua sehingga tidak perlu pembulatan.

**Asal:** Soal latihan baru untuk panduan ini.

### 4. Dua batas fungsi linear

*Tingkat: Mudah.*

**Soal lengkap.** Untuk ukuran input integer $n\ge1$, suatu program mempunyai biaya $T(n)=6n+12$. Temukan konstanta positif $c$ dan $n_0$ yang membuktikan $T(n)\in O(n)$. Temukan pula konstanta untuk membuktikan $T(n)\in\Omega(n)$.

**Asal:** Dikembangkan dari bank soal “Latihan Soal K2 - Laju Pertumbuhan dan Kompleksitas Fungsi Algoritme”, nomor 42; pembuktian dua batas ditambahkan.

### 5. Suku kubik

*Tingkat: Sedang.*

**Soal lengkap.** Untuk ukuran input integer $n\ge1$, biaya suatu program adalah $T(n)=5n^3+100n+20$. Cari kelas $\Theta$ yang paling ketat dengan menunjukkan batas atas dan batas bawah berupa kelipatan fungsi yang sama.

**Asal:** Dikembangkan dari bank soal “Latihan Soal K2 - Laju Pertumbuhan dan Kompleksitas Fungsi Algoritme”, nomor 36; pembuktian dua batas ditambahkan.

### 6. Tahap berurutan

*Tingkat: Sedang.*

**Soal lengkap.** Sebuah program menjalankan tahap A satu kali dengan $n^2$ operasi. Setelah A selesai, program menjalankan tahap B satu kali dengan $20n$ operasi. Berapa total operasi dan kelas $\Theta$-nya? Jelaskan mengapa kedua biaya dijumlahkan.

**Asal:** Soal latihan baru untuk panduan ini.

### 7. Panjang loop berubah

*Tingkat: Sedang.*

**Soal lengkap.** Sebuah loop luar memakai $i=1,2,\ldots,n$. Pada putaran dengan nilai $i$, loop dalam menjalankan tepat $i$ perbandingan. Untuk integer $n\ge1$, hitung total saat $n=5$, tulis $F(n)$, dan buktikan kelas $\Theta$-nya.

**Asal:** Soal latihan baru untuk panduan ini.

### 8. Tiga loop panjang $n$

*Tingkat: Sedang.*

**Soal lengkap.** Tiga loop bersarang masing-masing memakai indeks integer dari 0 sampai sebelum $n$, dengan kenaikan satu. Setiap kombinasi tiga indeks menjalankan tepat satu operasi di bagian terdalam. Berapa operasi terdalam saat $n=3$ dan berapa $F(n)$? Dengan biaya penugasan dan pemeriksaan masing-masing 1, kenaikan indeks 2, serta operasi terdalam 1, buat tabel *Code–Cost–Frequency–Total* dan cari $T(n)$ untuk integer $n\ge1$. Apa kelas $\Theta$-nya?

**Asal:** Adaptasi “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 3a.

### 9. Tiga pola bersarang

*Tingkat: Sedang.*

**Soal lengkap.** Tiga loop bersarang menjalankan satu operasi pada setiap kombinasi indeks. Loop luar mulai dari $i=n$, lalu memakai pembagian bilangan bulat $i\leftarrow\lfloor i/2\rfloor$ selama $i>0$. Loop tengah mulai dari $j=1$, lalu menggandakan $j$ selama $j<n$. Loop terdalam mulai dari $k=0$, lalu menambah 2 selama $k<n$. Hitung operasi terdalam $F(8)$. Dengan biaya penugasan dan pemeriksaan 1 serta pembagian, penggandaan, dan penambahan indeks 2, buat tabel *Code–Cost–Frequency–Total*, cari $T(8)$, dan tentukan kelas $\Theta$ untuk $n>1$.

**Asal:** Adaptasi “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 3b.

### 10. Dua loop berurutan

*Tingkat: Sedang.*

**Soal lengkap.** Loop luar memakai bound = 1, 2, 4, dan seterusnya selama bound $\le n$. Pada setiap putaran luar, loop pertama memakai $j=0,2,4,\ldots<n$; *setelah loop pertama selesai*, loop kedua memakai $j=1,2,4,\ldots<n$. Setiap putaran kedua loop dalam menjalankan satu operasi. Hitung pekerjaan terdalam $F(8)$. Dengan biaya penugasan dan pemeriksaan 1 serta penggandaan dan penambahan indeks 2, buat tabel *Code–Cost–Frequency–Total*, cari $T(8)$, dan tentukan kelas $\Theta$ untuk $n>1$.

**Asal:** Adaptasi “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 3c.

### 11. Paket logaritmik

*Tingkat: Sulit.*

**Soal lengkap.** Dua paket memproses $n>0$ record. Waktu paket A adalah $T_A(n)=0{,}1n\log_2 n$ mikrodetik dan waktu paket B adalah $T_B(n)=5n$ mikrodetik. Cari ukuran saat kedua waktu sama. Paket mana lebih cepat pada $n=2^{40}$ dan $n=2^{60}$? Gunakan satuan yang sama.

**Asal:** Dikembangkan dari “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 2a; ukuran $2^{40}$ dan $2^{60}$ adalah contoh tambahan, bukan angka soal asli.

### 12. Paket akar

*Tingkat: Sulit.*

**Soal lengkap.** Dua paket memproses $n>0$ record. Waktu paket A adalah $T_A(n)=0{,}001n$ milidetik dan waktu paket B adalah $T_B(n)=500\sqrt n$ milidetik. Cari titik potong positif dan tentukan paket lebih cepat saat $n=10^9$.

**Asal:** Adaptasi “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 2b.

### 13. Perkiraan kubik

*Tingkat: Sulit.*

**Soal lengkap.** Sebuah program terukur 1 detik pada ukuran input $n=8$. Jika *diasumsikan* model biayanya tepat sebanding dengan $n^3$ pada $n=8$ dan $n=16$, perkirakan waktu pada $n=16$. Mengapa informasi $O(n^3)$ saja tidak cukup untuk menjamin perkiraan itu?

**Asal:** Soal latihan baru untuk panduan ini.

### 14. Batas longgar

*Tingkat: Sulit.*

**Soal lengkap.** Untuk ukuran input integer $n\ge1$, buktikan fungsi $f(n)=n$ termasuk $O(n^2)$ dengan memberikan konstanta yang sesuai. Kemudian jelaskan mengapa fungsi tersebut tidak termasuk $\Theta(n^2)$.

**Asal:** Soal latihan baru untuk panduan ini.

### 15. Dua fungsi kuadrat

*Tingkat: Sulit.*

**Soal lengkap.** Dua algoritme mempunyai biaya $f_A(n)=2n^2+975n+90$ dan $f_B(n)=n^2+75n+90$ untuk ukuran input integer $n>0$. Adakah ukuran positif ketika B mengerjakan lebih banyak operasi daripada A? Apakah kelas $\Theta$ keduanya sama?

**Asal:** Adaptasi “UTS Analisis Algoritme 2018”, nomor 2a; pertanyaan tentang kelas pertumbuhan ditambahkan.

### 16. Klaim “pasti empat kali”

*Tingkat: Tantangan.*

**Soal lengkap.** Seorang peserta menyatakan: “Jika biaya program termasuk $O(n^2)$, menggandakan ukuran input pasti membuat waktunya empat kali lebih lama.” Apakah pernyataan ini benar untuk semua program dan semua ukuran input? Beri dua alasan dan satu fungsi biaya sebagai contoh.

**Asal:** Soal latihan baru untuk panduan ini.

### 17. Tiga suku pada tabel responsi

*Tingkat: Sedang; terkait responsi nomor 1.*

**Soal lengkap.** Untuk ukuran input integer $n\ge3$, waktu suatu algoritme mengikuti $T(n)=500n+100n^{1{,}5}+50n\log_{10}n$. Tentukan suku yang akhirnya dominan dan kelas Big-O-nya. Jelaskan mengapa koefisien 500 tidak membuat suku $500n$ dominan untuk semua $n$ besar.

**Asal:** Adaptasi baris kedua tabel “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 1; pertanyaan alasan ditambahkan.

### 18. Rata-rata dengan biaya setiap baris sama

*Tingkat: Sedang; terkait responsi nomor 4a.*

**Soal lengkap.** Dua algoritme menghitung rata-rata dari array berisi $n>0$ angka. Rata-1 menjalankan `jml ← 0` sekali, baris `for` sebanyak $n$ kali, penjumlahan sebanyak $n$ kali, dan pembagian akhir sekali. Rata-2 menjalankan dua inisialisasi sekali masing-masing, pemeriksaan `while` sebanyak $n+1$ kali, penjumlahan $n$ kali, kenaikan indeks $n$ kali, dan pembagian akhir sekali. Jika setiap pelaksanaan baris berbiaya satu satuan waktu sesuai model khusus soal ini, buat tabel *Code–Cost–Frequency–Total*. Tentukan $T_1(n)$, $T_2(n)$, biaya saat $n=4$, serta algoritme yang lebih murah.

**Asal:** Dikembangkan dari dua algoritme rata-rata pada “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 4, dengan konvensi satu baris satu satuan pada contoh halaman 3.

### 19. Rata-rata dengan biaya per baris berbeda

*Tingkat: Sulit; terkait responsi nomor 4b.*

**Soal lengkap.** Pakai dua algoritme dan jumlah pelaksanaan baris dari soal 18. Sekarang biaya inisialisasi dan pemeriksaan kondisi masing-masing $\tfrac12$ satuan, baris `for` Rata-1 bernilai 2 satuan, sedangkan setiap penjumlahan, kenaikan indeks, dan pembagian akhir bernilai $1\tfrac12$ satuan. Tentukan kedua fungsi biaya, bandingkan ketika $n=4$, dan jelaskan apakah keduanya memiliki kelas pertumbuhan yang sama. Anggap biaya tersebut berlaku untuk satu baris lengkap sehingga operasi di dalam baris tidak dihitung lagi.

**Asal:** Dikembangkan dari dua algoritme rata-rata pada “Lembar Kerja Responsi Pertemuan 2 Analgor”, nomor 4 dan bobot per baris pada contoh halaman 3.

## Pembahasan

### 1. Daftar tujuh nama

Ada tujuh pekerjaan satu perbandingan, jadi $1+1+1+1+1+1+1=7$. Untuk $n$ nama, jumlahnya $T(n)=n$. Karena persis sebanding dengan $n$, kelasnya $\Theta(n)$.

### 2. Biaya persiapan

Persiapan terjadi sekali, pemrosesan terjadi $n$ kali: $T(n)=12+4n$. Untuk lima item $T(5)=12+4(5)=32$; untuk sepuluh item $T(10)=12+4(10)=52$. Lima item tambahan menambah $5\cdot4=20$ satuan.

### 3. Pembagian dua

Urutannya $32\to16\to8\to4\to2\to1$. Ada lima panah, jadi lima pembagian. Cek: $2^5=32$, maka $\log_2 32=5$.

### 4. Dua batas fungsi linear

Untuk $n\ge1$, $12\le12n$. Tambahkan $6n$: $6n+12\le18n$. Jadi $c=18,n_0=1$ membuktikan $O(n)$. Karena 12 tidak negatif, $6n+12\ge6n$; $c=6,n_0=1$ membuktikan $\Omega(n)$. Dua batas memberi $\Theta(n)$.

### 5. Suku kubik

Untuk $n\ge1$, $n\le n^3$ dan $1\le n^3$. Maka $100n\le100n^3$ dan $20\le20n^3$, sehingga $T(n)\le125n^3$. Karena suku tambahan tidak negatif, $T(n)\ge5n^3$. Dua batas ini membuktikan $\Theta(n^3)$.

### 6. Tahap berurutan

Totalnya $T(n)=n^2+20n$, sebab tahap kedua tidak diulang pada setiap operasi tahap pertama. Pada $n\ge1$, $n\le n^2$, sehingga $n^2\le T(n)\le21n^2$. Maka $\Theta(n^2)$.

### 7. Panjang loop berubah

Untuk $n=5$, $1+2+3+4+5=15$. Umumnya $F(n)=n(n+1)/2$. Pada $n\ge1$, $n\le n+1\le2n$. Kalikan semua ruas dengan $n/2>0$: $n^2/2\le F(n)\le n^2$. Jadi $\Theta(n^2)$. Nilai tepat pada $n=5$ tetap 15, bukan 25.

### 8. Tiga loop panjang $n$

Untuk $n=3$, tiap indeks bisa 0, 1, atau 2. Ada $3\cdot3\cdot3=27$ kombinasi, sehingga $F(n)=n^3$. Tabel *Code–Cost–Frequency–Total* lengkap ada pada Bab 2 bagian 3a: jumlah kolom Total memberi $T(n)=4n^3+5n^2+5n+2$. Keduanya $\Theta(n^3)$.

### 9. Tiga pola bersarang

Pada $n=8$, $i$ bernilai 8, 4, 2, 1 (4 nilai); $j$ bernilai 1, 2, 4 (3 nilai); $k$ bernilai 0, 2, 4, 6 (4 nilai). Jadi $F(8)=4\cdot3\cdot4=48$. Umumnya $F(n)=abc$ dengan $a=\lfloor\log_2n\rfloor+1$, $b=\lceil\log_2n\rceil$, $c=\lceil n/2\rceil$. Tabel lengkap pada Bab 2 bagian 3b memberi $T(n)=2+5a+5ab+4abc$, sehingga $T(8)=274$ dan kelasnya $\Theta(n\log^2n)$.

### 10. Dua loop berurutan

Pada $n=8$, luar mempunyai 1, 2, 4, 8 (4 putaran); loop dalam pertama 0, 2, 4, 6 (4); kedua 1, 2, 4 (3). Maka $F(8)=4(4+3)=28$. Umumnya $F(n)=a(b+c)$ dengan $a=\lfloor\log_2n\rfloor+1$, $b=\lceil n/2\rceil$, dan $c=\lceil\log_2n\rceil$. Tabel lengkap pada Bab 2 bagian 3c memberi $T(n)=2+7a+4a(b+c)$, sehingga $T(8)=142$ dan kelasnya $\Theta(n\log n)$.

### 11. Paket logaritmik

Setarakan, bagi dengan $n>0$, lalu dengan $0{,}1$: $\log_2n=50$, maka titik potong $n=2^{50}$. Pada $2^{40}$, A berbiaya $4n<5n$, jadi A lebih cepat. Pada $2^{60}$, A berbiaya $6n>5n$, jadi B lebih cepat.

### 12. Paket akar

Setarakan. Bagi kedua ruas dengan $\sqrt n>0$: $0{,}001\sqrt n=500$. Bagi dengan $0{,}001$: $\sqrt n=500.000$. Kuadratkan: $n=2{,}5\times10^{11}$. Pada $10^9$, A = $10^6$ ms dan B $\approx1{,}581\times10^7$ ms; A lebih cepat.

### 13. Perkiraan kubik

Rasionya $16^3/8^3=(16/8)^3=8$, jadi perkiraannya delapan detik *jika* model kubik sudah dominan pada dua ukuran itu. Label $O(n^3)$ hanya batas atas. Fungsi $T(n)=n$ juga berada dalam $O(n^3)$, tetapi rasionya dua.

### 14. Batas longgar

Untuk $n\ge1$, $n\le n^2$; pilih $c=1,n_0=1$. Agar $\Theta(n^2)$, harus ada $c_1>0$ sehingga $n\ge c_1n^2$ untuk semua $n$ besar. Bagi dengan $n>0$: $1\ge c_1n$. Sisi kanan terus bertambah; ketaksamaan tidak mungkin terus berlaku.

### 15. Dua fungsi kuadrat

Kurangkan B dari A: $(2n^2-n^2)+(975n-75n)+(90-90)=n^2+900n>0$. Maka A selalu lebih besar, sehingga B tidak pernah lebih lambat menurut fungsi biaya ini. Keduanya tetap $\Theta(n^2)$: sama-sama diapit oleh kelipatan $n^2$ untuk $n$ besar. Kelas sama tidak berarti biaya tepat sama.

### 16. Klaim “pasti empat kali”

Tidak. Pertama, $O(n^2)$ hanya batas atas. $T(n)=n$ juga memenuhinya tetapi rasionya dua. Kedua, bahkan fungsi $\Theta(n^2)$ dapat memiliki biaya tambahan. $T(n)=n^2+1000$ berubah dari 1100 pada $n=10$ menjadi 1400 pada $n=20$, bukan 4400. Rasio empat hanya pendekatan ketika suku kuadrat sudah dominan.

### 17. Tiga suku pada tabel responsi

Bandingkan masing-masing suku dengan $n^{1{,}5}$. Rasio $500n/(100n^{1{,}5})=5/\sqrt n$ menuju nol. Rasio $50n\log_{10}n/(100n^{1{,}5})=\log_{10}n/(2\sqrt n)$ juga menuju nol. Jadi $100n^{1{,}5}$ dominan dan $T(n)\in O(n^{1{,}5})$. Koefisien 500 hanya menggeser ukuran ketika suku-suku saling menyusul; ia tidak mengubah pangkat $n$.

### 18. Rata-rata dengan biaya setiap baris sama

Gunakan tabel pada Bab 2 bagian 4a. Untuk Rata-1 ada dua baris yang berjalan sekali dan dua baris yang berjalan $n$ kali, sehingga $T_1(n)=2+2n$ dan $T_1(4)=10$. Untuk Rata-2, dua inisialisasi dan satu pembagian menyumbang 3; pemeriksaan `while` menyumbang $n+1$; penjumlahan dan kenaikan indeks menyumbang $2n$. Maka $T_2(n)=3+(n+1)+2n=4+3n$ dan $T_2(4)=16$. Selisihnya $T_2-T_1=n+2>0$, jadi Rata-1 lebih murah menurut bobot ini.

### 19. Rata-rata dengan biaya per baris berbeda

Gunakan tabel pada Bab 2 bagian 4b. Rata-1: inisialisasi dan pembagian akhir memberi $\tfrac12+1\tfrac12=2$; pengulangan dan penjumlahan memberi $2n+1\tfrac12n=3\tfrac12n$. Jadi $T_1(n)=2+3\tfrac12n$ dan $T_1(4)=16$. Rata-2: dua inisialisasi, satu pemeriksaan akhir, dan pembagian memberi $\tfrac12+\tfrac12+\tfrac12+1\tfrac12=3$; pemeriksaan yang berhasil, penjumlahan, dan kenaikan indeks memberi $\tfrac12n+1\tfrac12n+1\tfrac12n=3\tfrac12n$. Jadi $T_2(n)=3+3\tfrac12n$ dan $T_2(4)=17$. Rata-1 lebih murah satu satuan dalam model ini; keduanya $\Theta(n)$.
