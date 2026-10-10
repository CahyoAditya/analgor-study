# Bab 1 — Panduan Responsi Pertemuan 1

Lembar responsi pertama terdiri dari lima nomor besar. Nomor 1 mencari titik potong fungsi, nomor 2 menghitung pilihan proyek dan sub-tim, nomor 3 menghitung simpul pada *tree*, nomor 4 menghitung gabungan himpunan, dan nomor 5 memeriksa serta membuktikan pernyataan. Bab ini mengikuti **urutan lima nomor itu**, bukan urutan topik kuliah. Tiap nomor dimulai dari arti pertanyaannya, diikuti satu contoh kecil, lalu pembahasan angka pada lembar responsi.

| Bagian | Asal | Hasil yang dicari |
| --- | --- | --- |
| 1. Titik potong | Responsi 1 nomor 1 | Koordinat $(x,y)$ yang memenuhi dua fungsi. |
| 2. Memilih kelompok | Responsi 1 nomor 2a–c | Banyak kelompok berbeda. |
| 3. *Tree* keputusan | Responsi 1 nomor 3a–b | Banyak simpul pada satu level atau seluruh *tree*. |
| 4. Gabungan himpunan | Responsi 1 nomor 4 | Banyak solusi berbeda yang memenuhi setidaknya satu syarat. |
| 5. Membuktikan klaim | Responsi 1 nomor 5a–e | Bukti umum atau contoh penyangkal. |

Beberapa soal sumber belum menetapkan semua konvensi, dan dua klaim di nomor 5 ternyata salah. Bab ini menyatakan syaratnya dengan jelas dan tidak memaksakan jawaban yang keliru. Setiap perubahan bentuk matematika perlu alasan; bila pembahasan terasa cepat, coba ulangi dengan angka kecil sebelum melanjutkan.

## 1. Titik potong: kapan dua aturan memberi hasil yang sama?

Bayangkan dua aturan mengubah angka masukan $x$ menjadi angka keluaran $y$. Titik potong adalah satu pasangan $(x,y)$ tempat **kedua aturan menerima $x$ yang sama dan mengeluarkan $y$ yang sama**. Misalnya, untuk $f(x)=x+1$ dan $g(x)=3$, pada $x=2$ keduanya bernilai 3. Titik potongnya $(2,3)$. Inilah alasan kita memulai dengan $f(x)=g(x)$. Setelah menemukan $x$, kita tetap harus mencari $y$ dan memeriksa kedua fungsi.

### Cara menjaga persamaan tetap benar

Persamaan $2x+3=11$ adalah contoh pemanasan: kita ingin mengetahui nilai $x$ yang membuat sisi kiri dan kanan sama. Setelah cara ini jelas, kita pakai langkah yang sama untuk dua fungsi pada responsi.

Langkah pertama sering disebut “memindahkan 3 ke kanan”. Ungkapan itu cepat, tetapi menyembunyikan alasannya. Yang sesungguhnya dilakukan ialah **mengurangi 3 pada kedua sisi**:

$$
\begin{aligned}
2x+3&=11 \\
2x+3-3&=11-3 \\
2x&=8.
\end{aligned}
$$

Mengapa boleh? Jika dua benda sama berat, mengambil 3 satuan dari keduanya menjaga keduanya tetap sama berat. Selanjutnya kita **membagi kedua sisi dengan 2**:

$$
\begin{aligned}
2x&=8 \\
\frac{2x}{2}&=\frac{8}{2} \\
x&=4.
\end{aligned}
$$

Pembagian ini sah karena 2 bukan nol. Terakhir, masukkan $x=4$ ke persamaan awal: $2(4)+3=8+3=11$. Pemeriksaan ini menangkap salah hitung sebelum kita melanjutkan.

> **Kebiasaan penting.** Setiap kali suatu suku tampak “berpindah ruas”, tanyakan operasi apa yang sebenarnya diterapkan pada *kedua* sisi. Jika membagi dengan suatu ekspresi, periksa bahwa ekspresi itu tidak nol.

### Empat pasangan pada nomor 1

**Soal sumber.** Cari titik potong masing-masing pasangan dengan substitusi, eliminasi, atau determinan: (1) $2x+3$ dan $-x+5$; (2) $3x-4$ dan $2x+1$; (3) $x^2-4x+3$ dan $x+1$; (4) $\frac12x+2$ dan $-\frac14x+\frac74$. Pembahasan berikut memakai penyamaan keluaran kedua fungsi.

**Pasangan pertama.** Dalam lembar responsi, ada $f(x)=2x+3$ dan $g(x)=-x+5$. Titik potong berarti satu nilai $x$ menghasilkan nilai $y$ yang sama pada dua fungsi. Karena itu kita mulai dengan menyamakan hasilnya:

$$2x+3=-x+5.$$

Tambahkan $x$ pada kedua sisi agar suku yang memuat $x$ berada bersama: $3x+3=5$. Kurangi 3 pada kedua sisi: $3x=2$. Bagi dengan 3: $x=2/3$. Kita belum selesai karena *titik* memiliki dua koordinat. Masukkan $x=2/3$ ke fungsi yang lebih mudah:

$$y=2(2/3)+3=4/3+9/3=13/3.$$

Pemeriksaan dengan fungsi kedua memberi $-(2/3)+5=-2/3+15/3=13/3$. Jadi titik potongnya $(2/3,13/3)$.

Ada alasan praktis mempelajarinya. Jika $f(n)$ dan $g(n)$ adalah jumlah operasi dua algoritme, titik saat keduanya sama dapat menjadi tempat pilihan yang lebih cepat berubah. Kita masih harus memeriksa **sisi kiri dan kanan** titik itu; kesamaan di satu titik saja belum mengatakan algoritme mana yang lebih baik untuk input lain.

**Contoh kedua, juga dari responsi.** Untuk $f(x)=3x-4$ dan $g(x)=2x+1$, samakan $3x-4=2x+1$. Kurangi $2x$ dari kedua sisi sehingga $x-4=1$. Tambah 4 pada kedua sisi sehingga $x=5$. Kedua fungsi bernilai 11: $3(5)-4=11$ dan $2(5)+1=11$. Titik potongnya $(5,11)$.

**Pasangan ketiga: saat satu fungsi melengkung.** Responsi juga memberi $f(x)=x^2-4x+3$ dan $g(x)=x+1$. Samakan keduanya, lalu kurangi $(x+1)$ pada kedua sisi:

$$
\begin{aligned}
x^2-4x+3&=x+1 \\
x^2-4x+3-x-1&=0 \\
x^2-5x+2&=0.
\end{aligned}
$$

Rumus kuadrat untuk $ax^2+bx+c=0$ ialah $x=(-b\pm\sqrt{b^2-4ac})/(2a)$. Di sini $a=1$, $b=-5$, dan $c=2$. Maka $-b=5$ dan $b^2-4ac=25-8=17$. Kita mendapat dua nilai $x$, yaitu $(5+\sqrt{17})/2$ dan $(5-\sqrt{17})/2$. Untuk masing-masing, $y=x+1$, sehingga titiknya $((5+\sqrt{17})/2,(7+\sqrt{17})/2)$ dan $((5-\sqrt{17})/2,(7-\sqrt{17})/2)$. Dua titik masuk akal: garis dapat memotong parabola di dua tempat.

**Pasangan keempat: pecahan tidak perlu ditakuti.** Dua fungsi lain di responsi adalah $f(x)=\tfrac12x+2$ dan $g(x)=-\tfrac14x+\tfrac74$. Titik potongnya memenuhi

$$\frac12x+2=-\frac14x+\frac74.$$

Penyebut 2 dan 4 membuat hitungan kurang nyaman. Kita boleh mengalikan **kedua sisi** dengan 4, karena 4 bukan nol dan perkalian yang sama mempertahankan kesamaan:

$$
4\left(\frac12x+2\right)=4\left(-\frac14x+\frac74\right).
$$

Distribusikan 4 ke setiap suku, bukan hanya suku pertama. Di kiri, $4(\tfrac12x)=2x$ dan $4(2)=8$. Di kanan, $4(-\tfrac14x)=-x$ dan $4(\tfrac74)=7$. Sekarang persamaannya lebih sederhana: $2x+8=-x+7$. Tambah $x$ pada kedua sisi sehingga $3x+8=7$. Kurangi 8 pada kedua sisi sehingga $3x=-1$. Bagi dengan 3 sehingga $x=-1/3$.

Nilai $y$ dari fungsi pertama ialah $(1/2)(-1/3)+2=-1/6+12/6=11/6$. Dari fungsi kedua, $-(-1/3)/4+7/4=1/12+21/12=22/12=11/6$. Hasil yang sama dari kedua fungsi memastikan titik potongnya $(-1/3,11/6)$. Perhatikan bahwa menghilangkan pecahan di awal hanyalah pilihan untuk memudahkan hitungan; jawaban akhirnya tetap boleh berupa pecahan.

**Periksa sebelum berpindah nomor.** Untuk setiap pasangan, tanyakan: mengapa kedua fungsi disamakan; operasi apa yang dilakukan pada **kedua** sisi; apakah jawaban sudah memuat $x$ dan $y$; apakah kedua fungsi benar-benar memberi $y$ yang sama? Perhatikan bahwa pasangan ketiga menghasilkan dua titik karena persamaan kuadratnya memiliki dua akar nyata.

## 2. Memilih proyek dan sub-tim: kapan urutan dihitung?

Nomor ini tidak lagi mencari titik potong. Yang dihitung sekarang ialah **berapa kelompok pilihan yang berbeda**. Sebelum memakai rumus, bedakan kelompok dari urutan. Memilih proyek A lalu B menghasilkan kelompok yang sama dengan memilih B lalu A. Sebaliknya, jika A menjadi ketua dan B menjadi wakil, menukar mereka menghasilkan penugasan berbeda.

**Contoh kecil.** Dari empat nama A, B, C, D, pilih dua anggota tanpa jabatan. Kelompoknya AB, AC, AD, BC, BD, CD: enam. Hitungan berurutan $4\times3=12$ memasukkan AB dan BA secara terpisah. Karena setiap kelompok terhitung dua kali, bagi dengan $2!=2$ dan dapatkan enam. Penjelasan ini menjadi dasar untuk angka yang lebih besar.

### Tiga pertanyaan pada nomor 2

**2a.** Manajer perusahaan memilih empat proyek dari sepuluh proyek yang berbeda. Urutan memilih tidak membedakan kelompok proyek. **2b.** Manajer memilih nol proyek dari sepuluh proyek. **2c.** Lima anggota proyek membentuk sub-tim dua orang dengan peran sama. Berapa cara pada masing-masing keadaan?

Di kantin ada 3 pilihan nasi dan 2 pilihan mi. Jika seseorang memilih **satu nasi atau satu mi**, ada $3+2=5$ pilihan, karena kedua kelompok tidak tumpang tindih. Ini **aturan penjumlahan**.

Jika seseorang memilih **satu nasi dan satu minuman** dari 4 jenis minuman, setiap nasi dapat dipasangkan dengan 4 minuman. Untuk 3 nasi, ada $3\times4=12$ pasangan. Ini **aturan perkalian**. Kata “atau” dan “dan” membantu, tetapi selalu periksa apakah pilihan saling lepas atau apakah semua pasangan diperbolehkan.

### Faktorial, urutan, dan mengapa $0!=1$

Ada tiga buku berbeda A, B, C. Untuk menyusunnya berurutan, posisi pertama punya 3 pilihan, posisi kedua tinggal 2, posisi ketiga tinggal 1. Jadi ada $3\times2\times1=6$ susunan. Hasil perkalian $n(n-1)\cdots2\times1$ ditulis $n!$ dan dibaca “$n$ faktorial”.

Mengapa $0!=1$, bukan 0? Menyusun nol benda mempunyai **satu** hasil yang mungkin: susunan kosong. Aturan perkalian mengharuskan perkalian tanpa faktor bernilai 1 agar rumus tetap konsisten. Contoh: $1!=1\times0!$ mengharuskan $0!=1$.

### Jawaban 2a dan 2c: kelompok berbeda dari jabatan

Lembar responsi meminta memilih 2 orang dari 5 untuk sebuah sub-tim. Jika kita menghitung “orang pertama” lalu “orang kedua”, kita mendapat $5\times4=20$. Namun tim A-B sama dengan B-A: urutan tidak bermakna. Setiap tim dihitung dua kali. Karena itu bagi 2 dan dapatkan $20/2=10$ tim.

Untuk memilih 4 dari 10 proyek, hitungan berurutan adalah $10\times9\times8\times7=5040$. Setiap kelompok 4 proyek yang sama dapat muncul dalam $4!=24$ urutan. Maka banyak kelompok ialah $5040/24=210$. Inilah alasan rumus kombinasi

$$\binom nr=\frac{n!}{r!(n-r)!}.$$

Bagian $n!/(n-r)!$ menghitung pemilihan berurutan sebanyak $r$ benda; bagian $r!$ membuang penghitungan ulang akibat urutan internal yang tidak penting. Jika jabatan *ketua* dan *wakil* berbeda, urutan memang penting, sehingga untuk 2 dari 5 hasilnya $5\times4=20$, bukan 10.

Lihat lagi angka 5040 sebelum membaginya. Proyek pertama mempunyai 10 kemungkinan. Setelah satu proyek diambil, proyek yang sama tidak boleh diambil ulang, sehingga pilihan kedua tinggal 9. Sesudah dua proyek berbeda diambil, pilihan ketiga tinggal 8; pilihan keempat tinggal 7. Karena **setiap** pilihan pertama dapat diikuti **setiap** pilihan kedua yang tersisa, kita mengalikan $10\times9\times8\times7$, bukan menjumlahkannya. Setelah empat proyek terpilih, baru kita buang pengulangan urutan dengan membagi 24. Pembagian sah karena setiap kelompok empat proyek berbeda mempunyai tepat 24 susunan, tanpa pengecualian.

**Jawaban 2b perlu dibedakan dari jumlah proyek.** Jika tidak ada proyek yang dipilih, jumlah proyek terpilih adalah nol. Namun hanya ada **satu** kelompok yang memenuhi keputusan itu, yakni kelompok kosong. Jadi $\binom{10}{0}=1$, bukan nol. Angka $0!=1$ membuat rumus kombinasi konsisten dengan alasan ini.

Bayangkan peserta diminta menulis semua hasil dari keputusan “ambil nol proyek”. Daftarnya berisi satu baris: `{}`. Daftar itu tidak mempunyai anggota proyek, tetapi tetap merupakan **satu hasil pilihan**. Perbedaan antara “banyak anggota hasil” dan “banyak hasil yang mungkin” sering menjadi sumber jawaban nol yang keliru.

Pada 2a hasilnya $\binom{10}{4}=210$; pada 2b hasilnya 1; pada 2c hasilnya $\binom52=10$. Untuk 2c, daftar AB, AC, AD, AE, BC, BD, BE, CD, CE, DE memeriksa bahwa tidak ada pasangan terlewat. Jika soal mengganti sub-tim menjadi ketua dan wakil, pembagian oleh 2 tidak dilakukan dan hasilnya 20. **Baca syarat urutan sebelum memilih rumus.**

## 3. *Tree* keputusan: hitung tiap lapisan dahulu

Nomor 2 menghitung kelompok akhir. Pada nomor 3, yang dihitung adalah **simpul pada proses bercabang**. Akar adalah titik awal; satu cabang adalah satu kemungkinan keputusan; anak adalah simpul sesudah keputusan. Kedalaman menyatakan banyak langkah dari akar. Di sini akar berkedalaman 0. Jika akar punya dua anak, kedalaman 1 berisi dua simpul. Bila tiap anak itu juga punya dua anak, kedalaman 2 berisi empat. Kita mengalikan banyak simpul sebelumnya dengan banyak cabang per simpul.

### Jawaban 3a: kedalaman tiga dan dua cabang

**Soal sumber.** Sebuah algoritme pencarian memakai *tree* kombinatorial dengan kedalaman $d=3$. Setiap simpul yang belum menjadi daun mempunyai $b=2$ cabang. Berapa jumlah seluruh simpulnya?

| Kedalaman | Simpul pada lapisan itu | Jumlah dari akar sampai lapisan itu |
| ---: | ---: | ---: |
| 0 | 1 | 1 |
| 1 | $1\times2=2$ | $1+2=3$ |
| 2 | $2\times2=4$ | $3+4=7$ |
| 3 | $4\times2=8$ | $7+8=15$ |

Jadi pada kedalaman terakhir ada 8 simpul, sedangkan **seluruh *tree* ada 15 simpul**. Dari kedalaman 0 sampai 3 ada empat lapisan, bukan tiga. Jawaban 8 akan tepat jika soalnya hanya menanyakan banyak simpul pada kedalaman 3.

Secara umum, bila setiap simpul punya $b$ anak, kedalaman $d$ memuat $b^d$ simpul. Total dari akar sampai kedalaman $d$ adalah $1+b+b^2+\cdots+b^d$. Mulailah dari tabel seperti di atas ketika batas kedalaman belum jelas; rumus hanya menyingkat penjumlahan yang sudah dipahami.

### Jawaban 3b: “level ke-2” perlu konvensi

**Soal sumber.** Sebuah *tree* mempunyai empat level, dengan tiga cabang pada setiap simpul, lalu ditanya banyak simpul pada level ke-2. Lembar sumber tidak menyebut apakah akar dihitung sebagai level 1 atau level 0. Jika **akar level 1**, level 1 berisi 1 dan level 2 berisi $1\times3=\boxed{3}$. Jika **akar level 0**, level 1 berisi 3 dan level 2 berisi $3\times3=\boxed{9}$. Dalam penomoran sehari-hari, akar sebagai level 1 lazim dipakai untuk pertanyaan ini; jawabannya 3 **dengan konvensi itu**. Sebutkan konvensi saat menjawab.

| Lapisan fisik dari akar | Jika akar disebut level 1 | Jika akar disebut level 0 | Banyak simpul |
| ---: | ---: | ---: | ---: |
| Akar | 1 | 0 | 1 |
| Satu langkah dari akar | 2 | 1 | $1\times3=3$ |
| Dua langkah dari akar | 3 | 2 | $3\times3=9$ |
| Tiga langkah dari akar | 4 | 3 | $9\times3=27$ |

Tabel itu menunjukkan bahwa *tree* fisiknya sama; hanya **nama lapisannya** yang bergeser. Empat level pada soal memberi cukup lapisan untuk kedua penomoran. Jika pengajar menetapkan satu konvensi di kelas, ikuti konvensi tersebut dan tulis di awal jawaban.

## 4. Gabungan himpunan: satu solusi dihitung sekali

Pada *tree*, jalur yang berbeda dihitung sebagai jalur berbeda. Pada nomor 4, satu solusi dapat memenuhi A dan B sekaligus. Menjumlahkan semua kelompok mentah akan menghitung solusi tersebut dua kali. **Himpunan** adalah kelompok anggota; **irisan** $A\cap B$ berisi anggota yang ada di A **dan** B; **gabungan** $A\cup B$ berisi anggota yang ada di A **atau** B, termasuk keduanya.

**Contoh kecil.** A = {Ani, Budi, Cici} dan B = {Budi, Cici, Dedi}. Jumlah ukuran $|A|+|B|=3+3=6$ menghitung Budi dan Cici dua kali. Karena $|A\cap B|=2$, jumlah orang berbeda ialah $3+3-2=4$: Ani, Budi, Cici, Dedi.

### Nomor 4: tiga kondisi yang tumpang tindih

**Soal sumber.** Dalam proyek optimisasi, A, B, dan C menyatakan solusi yang memenuhi tiga kondisi. Diketahui $|A|=50$, $|B|=30$, $|C|=20$, $|A\cap B|=15$, $|A\cap C|=10$, $|B\cap C|=5$, dan $|A\cap B\cap C|=2$. Berapa solusi berbeda yang memenuhi **setidaknya satu** kondisi?

Kata “setidaknya satu” berarti $|A\cup B\cup C|$. Berikut alasan rumusnya dan penghitungan langkah demi langkah.

Untuk tiga kelompok A, B, C, mula-mula jumlahkan $|A|+|B|+|C|$. Kurangi tiga irisan pasangan karena anggota dua kelompok dihitung dua kali. Namun anggota yang berada di **ketiganya** semula dihitung tiga kali lalu dikurangi tiga kali, sehingga hasil sementara nol. Tambahkan irisan tiga sekali agar tiap orang dihitung satu kali:

$$
\begin{aligned}
|A\cup B\cup C|={}&|A|+|B|+|C| \\
&-|A\cap B|-|A\cap C|-|B\cap C| \\
&+|A\cap B\cap C|.
\end{aligned}
$$

Pada soal responsi, ukurannya berturut-turut 50, 30, 20; irisan pasangan 15, 10, 5; irisan tiga 2. Hitung perlahan: $50+30+20=100$; jumlah tiga irisan pasangan $15+10+5=30$; jadi sementara $100-30=70$; tambahkan 2 sehingga hasilnya **72**. Menulis setiap subtotal membantu menghindari lupa mengembalikan irisan tiga.

**Pemeriksaan tanpa rumus.** Tepat di ketiga kondisi ada 2 solusi. Tepat di A dan B ada $15-2=13$; tepat di A dan C ada $10-2=8$; tepat di B dan C ada $5-2=3$. Hanya A ada $50-13-8-2=27$; hanya B ada $30-13-3-2=12$; hanya C ada $20-8-3-2=7$. Ketujuh daerah ini tidak tumpang tindih, sehingga jumlahnya $27+12+7+13+8+3+2=72$. Ini memeriksa hasil dari rumus, sekaligus menunjukkan setiap solusi terhitung tepat satu kali.

## 5. Pembuktian: apakah klaimnya benar untuk semua bilangan?

Empat nomor sebelumnya meminta satu angka atau titik. Nomor 5 meminta alasan untuk kalimat yang memakai kata **setiap**. Sepuluh contoh yang cocok belum membuktikan setiap bilangan. Sebaliknya, satu contoh yang tidak cocok cukup untuk membantah klaim “setiap”. Maka sebelum mencari bukti, uji dulu klaimnya dengan nilai kecil.

Bilangan bulat (*integer*) meliputi bilangan negatif, nol, dan positif. Bilangan genap berbentuk $2k$ untuk suatu integer $k$; bilangan ganjil berbentuk $2k+1$. Bentuk ini menjelaskan semua bilangan dalam kelompok tersebut, bukan hanya contoh yang kebetulan dipilih.

### 5a: bukti langsung tentang bilangan genap

**Soal sumber.** Jika integer $n$ genap, buktikan $3n+2$ genap. Kita memakai definisi genap.

Kita mulai dari klaim pendek: jika integer $n$ genap, maka $3n+2$ genap. Mulailah dari arti *genap*, bukan dari menebak-nebak angka. Jika $n$ genap, ada integer $k$ dengan $n=2k$. Substitusikan:

$$3n+2=3(2k)+2=6k+2=2(3k+1).$$

Mengapa langkah terakhir cukup? Karena $3k+1$ tetap integer. Bentuk “2 dikali integer” adalah definisi bilangan genap. Bukti ini berlaku untuk setiap $n$ genap, termasuk bilangan negatif dan nol.

### 5b: satu contoh menyangkal klaim “selalu ganjil”

**Soal sumber.** “Untuk setiap bilangan bulat positif $n$, $n^2+2$ pasti ganjil.” Pilih $n=2$, yang memenuhi syarat positif. Hasilnya $2^2+2=4+2=6$, sebuah bilangan genap. Maka klaim ini **salah**; tidak ada bukti sah untuk kalimat seperti tertulis. Jika ingin memperbaikinya, tambah syarat bahwa $n$ ganjil. Untuk $n=2k+1$, diperoleh $n^2+2=4k^2+4k+3=2(2k^2+2k+1)+1$, berbentuk ganjil. Tambahan syarat ini merupakan perbaikan, bukan bagian dari soal sumber.

### 5c: rata-rata tiga bilangan genap berurutan

**Soal sumber.** Jika $a,b,c$ tiga bilangan genap berurutan, buktikan rata-ratanya sama dengan $b$. Jika bilangan tengahnya $b$, bilangan sebelumnya adalah $b-2$ dan sesudahnya $b+2$. Selisihnya 2 karena kita berpindah dari satu bilangan genap ke bilangan genap berikutnya. Rata-ratanya ialah jumlah ketiganya dibagi banyak bilangan:

$$
\begin{aligned}
\frac{(b-2)+b+(b+2)}{3}
&=\frac{b-2+b+b+2}{3} \\
&=\frac{3b}{3} \\
&=b.
\end{aligned}
$$

Angka $-2$ dan $+2$ saling meniadakan. Ini tidak bergantung pada nilai khusus $b$; itulah yang membuatnya menjadi bukti umum, bukan satu contoh saja.

### 5d: kontradiksi tidak dapat membuktikan klaim salah

Bukti kontradiksi dimulai dengan menganggap pernyataan yang ingin dibuktikan itu salah, lalu menunjukkan asumsi tersebut mustahil. Namun sebelum memakai cara ini, periksa klaimnya. Lembar responsi meminta membuktikan “untuk semua integer $a,b$, $a^2-4b-1\ne0$”. Klaim tersebut **salah**. Ambil $a=1$ dan $b=0$:

$$a^2-4b-1=1^2-4(0)-1=1-0-1=0.$$

Kita menemukan satu pasangan yang membuat hasil nol. Tidak ada bukti kontradiksi yang sah untuk klaim universal yang sudah dipatahkan oleh contoh ini. Coba juga $a=3,b=2$: $9-8-1=0$. Jika menemui soal serupa dalam kelas, jelaskan contoh penyangkal dan kemungkinan ada salah ketik pada pernyataannya; jangan menciptakan “bukti” untuk jawaban yang salah.

### 5e: induksi untuk jumlah $1+2+\cdots+n$

**Soal sumber.** Untuk setiap integer positif $n$, buktikan bahwa $1+2+\cdots+n=\frac{n(n+1)}2$. Memeriksa $n=1,2,3$ membantu menemukan kesalahan, tetapi belum cukup untuk semua $n$. Induksi menunjukkan bagaimana kebenaran untuk satu nilai membawa kebenaran ke nilai berikutnya.

Sering kita hendak membuktikan $P(n)$ untuk **setiap** integer $n\ge1$. Memeriksa $n=1,2,3$ hanya menunjukkan tiga kasus. Induksi memerlukan dua bagian:

1. **Basis:** $P(1)$ benar.
2. **Langkah:** untuk setiap $k\ge1$, jika $P(k)$ benar, maka $P(k+1)$ juga benar.

Dari basis kita memperoleh $P(1)$. Langkah memberi $P(2)$ dari $P(1)$, kemudian $P(3)$ dari $P(2)$, dan seterusnya. Itulah sebabnya dua bagian tersebut cukup untuk semua integer mulai dari 1.

**Contoh: jumlah $1+2+\cdots+n$.** Kita ingin membuktikan

$$S(n)=1+2+\cdots+n=\frac{n(n+1)}2.$$

Untuk basis $n=1$, sisi kiri adalah 1. Sisi kanan $1(1+1)/2=2/2=1$. Cocok.

Sekarang anggap pernyataan benar untuk suatu $k$, yakni $S(k)=k(k+1)/2$. Ini disebut *hipotesis induksi*; kita belum boleh menganggap rumus untuk $k+1$ sudah benar. Jumlah sampai $k+1$ adalah jumlah lama **ditambah satu suku baru**, bukan ditambah seluruh daftar lagi:

$$S(k+1)=S(k)+(k+1).$$

Ganti $S(k)$ memakai hipotesis:

$$S(k+1)=\frac{k(k+1)}2+(k+1).$$

Untuk menjumlahkan pecahan, samakan penyebut. Tulis $(k+1)=2(k+1)/2$. Maka

$$
\begin{aligned}
S(k+1)&=\frac{k(k+1)}2+\frac{2(k+1)}2 \\
&=\frac{k(k+1)+2(k+1)}2.
\end{aligned}
$$

Kedua suku pembilang memiliki faktor $(k+1)$. Keluarkan faktor itu:

$$S(k+1)=\frac{(k+1)(k+2)}2.$$

Ini tepat rumus awal dengan $n$ diganti $k+1$: $(k+1)((k+1)+1)/2$. Jadi langkah induksi selesai. Basis dan langkah bersama-sama membuktikan rumus untuk setiap $n\ge1$.

**Mengapa rumusnya masuk akal sebelum dibuktikan?** Tulis jumlah dari kiri ke kanan dan dari kanan ke kiri:

$$S=1+2+\cdots+n,$$
$$S=n+(n-1)+\cdots+1.$$

Jika tiap kolom dijumlah, selalu diperoleh $n+1$. Ada $n$ kolom. Jadi $2S=n(n+1)$; karena setiap jumlah dihitung dua kali, bagi kedua sisi dengan 2: $S=n(n+1)/2$. Cara pasangan ini memberi intuisi; induksi memastikan rumus berlaku untuk semua $n$.

**Cara membaca nomor 5:** tentukan dulu apakah pernyataannya benar; bila salah, tunjukkan satu contoh penyangkal; bila benar, pakai definisi atau induksi dan jelaskan mengapa tiap langkah berlaku untuk semua nilai yang disyaratkan.

## Latihan dan sumber

[Latihan Bab 1](latihan-bab-01.md) memisahkan soal dari bacaan utama. Kerjakan menurut nomor responsi yang sedang dipelajari. Setiap soal menyebut konteks serta asalnya.

Sumber utama bab ini ialah **Lembar Kerja Responsi Pertemuan 1 Analgor, semester ganjil 2025–2026**, nomor 1–5. Soal sumber ditulis ulang agar dapat dibaca tanpa membuka PDF; penjelasan, contoh kecil, dan pemeriksaan tambahan disusun untuk panduan ini. PDF asli tidak diunggah ulang. Pada nomor 3b, konvensi level tidak ditetapkan tegas. Pada nomor 5b dan 5d, klaim yang tercetak salah sebagaimana tertulis, sehingga ditampilkan contoh penyangkal.
