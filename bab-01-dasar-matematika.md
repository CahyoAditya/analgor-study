# Bab 1 — Matematika yang Membuat Analisis Algoritme Masuk Akal

> **Pertanyaan pembuka.** Dua cara sama-sama berhasil mencari nama dalam sebuah daftar yang sudah diurutkan. Cara pertama memeriksa nama dari awal sampai ketemu. Cara kedua berkali-kali membagi bagian daftar yang mungkin berisi nama itu. Mana yang lebih baik? Jawabannya perlu lebih dari sekadar melihat satu kali percobaan: kita harus menjelaskan *kapan* cara itu benar, *berapa banyak* pekerjaan yang dilakukan, dan *mengapa* hitungan tersebut berlaku.

Bab ini dibaca seperti cerita yang bergerak dari satu pertanyaan ke pertanyaan berikutnya. Mulailah dari contoh kecil. Rumus umum baru muncul setelah alasan di baliknya terlihat. Jika sebuah simbol terasa asing, baca kalimat sebelum dan sesudahnya; simbol selalu mewakili sesuatu yang konkret.

## 1. Sebelum menghitung, apa sebenarnya yang sedang kita bahas?

Bayangkan Sensei mencari angka 8 dalam **array** `[4, 1, 8, 2]`. Array adalah daftar data yang dapat diakses melalui posisi. Kita memakai istilah *array* karena istilah itu umum di pemrograman. Dalam contoh ini indeksnya dimulai dari 0. Jadi 4 berada di indeks 0 dan 8 berada di indeks 2. Daftar ini belum diurutkan, sehingga pencarian dengan membagi dua bagian belum boleh dipakai begitu saja.

Salah satu algoritme pencarian sederhana ialah: periksa posisi 0, lalu 1, lalu 2, dan berhenti ketika nilainya 8. Algoritme berarti urutan langkah yang jelas, menerima *input*, menghasilkan *output*, dan berhenti setelah sejumlah langkah berhingga. Untuk contoh tadi, inputnya array serta angka yang dicari; outputnya indeks 2.

Ada dua pertanyaan yang berbeda.

1. **Benarkah hasilnya?** Jika algoritme mengatakan “ketemu di indeks 2”, memang harus ada 8 di sana. Jika mengatakan “tidak ada”, seluruh posisi yang mungkin harus sudah diperiksa.
2. **Berapa pekerjaannya?** Dalam contoh ini angka 8 baru ditemukan pada pemeriksaan ketiga. Jika array berisi satu juta angka, jumlah pemeriksaan mungkin jauh lebih besar.

Kita perlu menyepakati **ukuran input**. Untuk mencari nilai dalam array, pilihan alami ialah $n=$ banyak elemen. Untuk bilangan bulat (*integer*) $N$, ukuran input biasanya banyak *bit* yang dipakai untuk menuliskannya, bukan besarnya $N$ itu sendiri. Angka 1024, misalnya, hanya memerlukan 11 bit dalam representasi biner. Menghitung sampai 1024 berarti melakukan pekerjaan yang jauh lebih banyak daripada 11 langkah.

Kita juga perlu memilih **operasi dasar**, yakni pekerjaan yang dihitung berulang. Dalam pencarian tadi, operasi dasarnya bisa berupa “membandingkan elemen array dengan angka 8”. Dengan definisi itu, contoh tadi memerlukan tiga perbandingan. Pemilihan operasi harus konsisten dari awal sampai akhir; kita tidak boleh menghitung perbandingan pada satu algoritme dan menghitung baris program pada algoritme lain seolah-olah keduanya ukuran yang sama.

Pengukuran dengan stopwatch tetap berguna, tetapi bergantung pada mesin, bahasa, dan input yang dicoba. Matematika membantu menjelaskan pola kerja untuk *semua* input dalam kondisi yang dinyatakan. Itulah alasan bab ini mempelajari aljabar, logika, pembuktian, dan cara menghitung kemungkinan.

## 2. Aljabar adalah cara menjaga dua sisi tetap seimbang

### 2.1 Apa arti tanda sama dengan?

Persamaan $2x+3=11$ mengatakan bahwa sisi kiri dan sisi kanan bernilai sama. Kita ingin mengetahui nilai $x$ yang membuatnya benar.

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

### 2.2 Pertidaksamaan punya satu jebakan tambahan

Untuk $2x+3<11$, kita tetap boleh mengurangi 3 pada kedua sisi: $2x<8$. Membagi dengan 2 yang positif menghasilkan $x<4$.

Tetapi dari $-2x<8$, membagi dengan $-2$ menghasilkan **$x>-4$**, bukan $x<-4$. Arah tanda berbalik karena perkalian bilangan negatif membalik urutan: $1<2$, tetapi $-1>-2$. Periksa dengan $x=0$: persamaan awal memberi $0<8$, benar; hasil $0>-4$ juga benar.

### 2.3 Titik potong dua fungsi: kapan dua biaya sama?

Dalam lembar responsi, ada $f(x)=2x+3$ dan $g(x)=-x+5$. Titik potong berarti satu nilai $x$ menghasilkan nilai $y$ yang sama pada dua fungsi. Karena itu kita mulai dengan menyamakan hasilnya:

$$2x+3=-x+5.$$

Tambahkan $x$ pada kedua sisi agar suku yang memuat $x$ berada bersama: $3x+3=5$. Kurangi 3 pada kedua sisi: $3x=2$. Bagi dengan 3: $x=2/3$. Kita belum selesai karena *titik* memiliki dua koordinat. Masukkan $x=2/3$ ke fungsi yang lebih mudah:

$$y=2(2/3)+3=4/3+9/3=13/3.$$

Pemeriksaan dengan fungsi kedua memberi $-(2/3)+5=-2/3+15/3=13/3$. Jadi titik potongnya $(2/3,13/3)$.

Ada alasan praktis mempelajarinya. Jika $f(n)$ dan $g(n)$ adalah jumlah operasi dua algoritme, titik saat keduanya sama dapat menjadi tempat pilihan yang lebih cepat berubah. Kita masih harus memeriksa **sisi kiri dan kanan** titik itu; kesamaan di satu titik saja belum mengatakan algoritme mana yang lebih baik untuk input lain.

**Contoh kedua, juga dari responsi.** Untuk $f(x)=3x-4$ dan $g(x)=2x+1$, samakan $3x-4=2x+1$. Kurangi $2x$ dari kedua sisi sehingga $x-4=1$. Tambah 4 pada kedua sisi sehingga $x=5$. Kedua fungsi bernilai 11: $3(5)-4=11$ dan $2(5)+1=11$. Titik potongnya $(5,11)$.

**Contoh ketiga: pecahan tidak perlu ditakuti.** Dua fungsi lain di responsi adalah $f(x)=\tfrac12x+2$ dan $g(x)=-\tfrac14x+\tfrac74$. Titik potongnya memenuhi

$$\frac12x+2=-\frac14x+\frac74.$$

Penyebut 2 dan 4 membuat hitungan kurang nyaman. Kita boleh mengalikan **kedua sisi** dengan 4, karena 4 bukan nol dan perkalian yang sama mempertahankan kesamaan:

$$
4\left(\frac12x+2\right)=4\left(-\frac14x+\frac74\right).
$$

Distribusikan 4 ke setiap suku, bukan hanya suku pertama. Di kiri, $4(\tfrac12x)=2x$ dan $4(2)=8$. Di kanan, $4(-\tfrac14x)=-x$ dan $4(\tfrac74)=7$. Sekarang persamaannya lebih sederhana: $2x+8=-x+7$. Tambah $x$ pada kedua sisi sehingga $3x+8=7$. Kurangi 8 pada kedua sisi sehingga $3x=-1$. Bagi dengan 3 sehingga $x=-1/3$.

Nilai $y$ dari fungsi pertama ialah $(1/2)(-1/3)+2=-1/6+12/6=11/6$. Dari fungsi kedua, $-(-1/3)/4+7/4=1/12+21/12=22/12=11/6$. Hasil yang sama dari kedua fungsi memastikan titik potongnya $(-1/3,11/6)$. Perhatikan bahwa menghilangkan pecahan di awal hanyalah pilihan untuk memudahkan hitungan; jawaban akhirnya tetap boleh berupa pecahan.

**Saat satu fungsi melengkung.** Responsi juga memberi $f(x)=x^2-4x+3$ dan $g(x)=x+1$. Samakan keduanya, lalu kurangi $(x+1)$ pada kedua sisi:

$$
\begin{aligned}
x^2-4x+3&=x+1 \\
x^2-4x+3-x-1&=0 \\
x^2-5x+2&=0.
\end{aligned}
$$

Rumus kuadrat untuk $ax^2+bx+c=0$ ialah $x=(-b\pm\sqrt{b^2-4ac})/(2a)$. Di sini $a=1$, $b=-5$, dan $c=2$. Maka $-b=5$ dan $b^2-4ac=25-8=17$. Kita mendapat dua nilai $x$, yaitu $(5+\sqrt{17})/2$ dan $(5-\sqrt{17})/2$. Untuk masing-masing, $y=x+1$, sehingga titiknya $((5+\sqrt{17})/2,(7+\sqrt{17})/2)$ dan $((5-\sqrt{17})/2,(7-\sqrt{17})/2)$. Dua titik masuk akal: garis dapat memotong parabola di dua tempat.

### 2.4 Interval: siapa yang termasuk batas?

Notasi $[2,5)$ berarti semua angka dari 2 sampai sebelum 5: angka 2 masuk, angka 5 tidak. Kurung siku `[` atau `]` berarti batas itu termasuk; kurung biasa `(` atau `)` berarti tidak termasuk. Untuk indeks integer, $[2,5)$ berarti indeks 2, 3, dan 4, jadi ada $5-2=3$ posisi.

Ini berguna untuk membagi array tanpa tumpang tindih. Bagian $[0,3)$ memuat indeks 0, 1, 2; bagian $[3,5)$ memuat 3, 4. Kedua bagian menyambung tepat di batas 3 tanpa mengulang posisi 3. Nanti bentuk ini membantu memahami binary search.

## 3. Logika: apa tepatnya yang hendak dibuktikan?

### 3.1 Kalimat, variabel, dan arti “semua”

Pernyataan “$7$ adalah bilangan prima” mempunyai nilai benar. “$7$ adalah bilangan genap” mempunyai nilai salah. Keduanya disebut **proposisi** karena nilai benarnya dapat ditentukan. Kalimat “$x+2=5$” belum punya satu nilai benar atau salah sebelum $x$ diberi nilai atau diberi keterangan seperti “ada $x$” atau “untuk semua $x$”. Pertanyaan dan perintah juga bukan proposisi.

Perhatikan perbedaan besar ini:

- **Ada** bilangan bulat $n$ sehingga $n^2=4$: benar, karena $n=2$ dapat dipakai.
- **Untuk setiap** bilangan bulat $n$, $n^2=4$: salah, karena $n=0$ menghasilkan 0, bukan 4.

Satu contoh yang cocok cukup untuk membuktikan klaim “ada”. Satu contoh yang tidak cocok cukup untuk **membantah** klaim “untuk setiap”. Sebaliknya, mencoba sepuluh contoh yang cocok tetap belum membuktikan klaim untuk semua bilangan: masih ada bilangan lain yang belum dicoba.

### 3.2 “Dan”, “atau”, “tidak”, serta “jika … maka …”

Misalkan $P$ berbunyi “$n$ genap” dan $Q$ berbunyi “$n$ habis dibagi 4”.

- $P\land Q$ berarti keduanya benar.
- $P\lor Q$ berarti setidaknya satu benar; dalam logika matematika, **atau** juga benar jika keduanya benar.
- $\neg P$ berarti $P$ salah.
- $Q\Rightarrow P$ berarti *jika* $n$ habis dibagi 4, *maka* $n$ genap.

Implikasi $Q\Rightarrow P$ benar. Sebab $n=4k$ untuk suatu integer $k$, sehingga $n=2(2k)$ dan $n$ genap. Arah sebaliknya, $P\Rightarrow Q$, salah: $n=6$ genap tetapi tidak habis dibagi 4. Jadi “jika $A$ maka $B$” tidak boleh dibalik begitu saja.

Sebuah implikasi $P\Rightarrow Q$ hanya salah saat $P$ benar tetapi $Q$ salah. Mengapa? Klaim itu menjanjikan apa yang terjadi **bila $P$ terjadi**. Saat $P$ tidak terjadi, janji itu tidak dilanggar. Contohnya, “jika bilangan habis dibagi 4 maka genap” tidak menjadi salah hanya karena kita melihat angka 3 yang tidak habis dibagi 4.

| $P$ | $Q$ | $P\Rightarrow Q$ | Alasan singkat |
| --- | --- | --- | --- |
| Benar | Benar | Benar | Janjinya terpenuhi. |
| Benar | Salah | Salah | Inilah contoh penyangkal. |
| Salah | Benar | Benar | Syaratnya tidak terjadi. |
| Salah | Salah | Benar | Syaratnya tidak terjadi. |

### 3.3 Tiga pola menarik kesimpulan

**Modus ponens.** Jika $P\Rightarrow Q$ dan kita tahu $P$ benar, maka $Q$ benar. Contoh: jika sebuah angka kelipatan 4 maka ia genap; 12 kelipatan 4; jadi 12 genap.

**Modus tollens.** Jika $P\Rightarrow Q$ dan kita tahu $Q$ salah, maka $P$ salah. Contoh: angka kelipatan 4 pasti genap; 7 tidak genap; jadi 7 tidak mungkin kelipatan 4.

**Silogisme.** Jika $P\Rightarrow Q$ dan $Q\Rightarrow R$, maka $P\Rightarrow R$. Contoh: kelipatan 4 berarti genap; genap berarti sisanya 0 bila dibagi 2; jadi kelipatan 4 bersisa 0 bila dibagi 2.

Pola yang *tidak* sah ialah: “Jika $P$ maka $Q$; $Q$ terjadi; jadi $P$ terjadi.” Angka 6 genap ($Q$), tetapi itu tidak membuatnya kelipatan 4 ($P$). Kesalahan arah ini sering muncul ketika kita membaca hasil program lalu menyimpulkan satu-satunya penyebabnya.

### 3.4 “Jika dan hanya jika” serta membalik kata “tidak”

Kalimat “$P$ **jika dan hanya jika** $Q$” ditulis $P\Leftrightarrow Q$. Artinya dua arah harus benar: $P\Rightarrow Q$ **dan** $Q\Rightarrow P$. Misalnya untuk integer $n$, “$n$ genap jika dan hanya jika sisa $n$ dibagi 2 adalah 0”. Arah pertama benar karena $n=2k$ memiliki sisa 0. Arah kedua benar karena angka dengan sisa 0 saat dibagi 2 dapat ditulis $2k$. Jika hanya satu arah yang dibuktikan, frasa “jika dan hanya jika” belum terbukti.

Ada pula aturan untuk menyangkal pernyataan gabungan. Misalkan $P$ berbunyi “tugas sudah dibaca” dan $Q$ berbunyi “tugas sudah dikerjakan”. Kalimat “**tidak benar bahwa** tugas sudah dibaca *dan* dikerjakan” berarti **setidaknya salah satu** belum terjadi. Dalam simbol:

$$\neg(P\land Q)\Leftrightarrow(\neg P\lor\neg Q).$$

Kebalikannya, “tidak benar bahwa tugas sudah dibaca *atau* dikerjakan” berarti **keduanya** belum terjadi:

$$\neg(P\lor Q)\Leftrightarrow(\neg P\land\neg Q).$$

Ini disebut aturan De Morgan. Coba keadaan kecil: jika tugas sudah dibaca tetapi belum dikerjakan, kalimat “belum keduanya selesai” benar. Bentuk $\neg P\lor\neg Q$ juga benar karena $\neg Q$ benar. Pemeriksaan contoh membantu memahami aturan, sedangkan tabel kebenaran lengkap dapat membuktikan bahwa dua bentuk selalu sepadan.

## 4. Pembuktian: dari beberapa contoh menuju semua kasus

### 4.1 Bukti langsung memakai definisi

Soal responsi meminta membuktikan: jika integer $n$ genap, maka $3n+2$ genap. Mulailah dari arti *genap*, bukan dari menebak-nebak angka. Jika $n$ genap, ada integer $k$ dengan $n=2k$. Substitusikan:

$$3n+2=3(2k)+2=6k+2=2(3k+1).$$

Mengapa langkah terakhir cukup? Karena $3k+1$ tetap integer. Bentuk “2 dikali integer” adalah definisi bilangan genap. Bukti ini berlaku untuk setiap $n$ genap, termasuk bilangan negatif dan nol.

**Contoh lain dari responsi: rata-rata tiga bilangan genap berurutan.** Jika bilangan tengahnya $b$, bilangan sebelumnya adalah $b-2$ dan sesudahnya $b+2$. Selisihnya 2 karena kita berpindah dari satu bilangan genap ke bilangan genap berikutnya. Rata-ratanya ialah jumlah ketiganya dibagi banyak bilangan:

$$
\begin{aligned}
\frac{(b-2)+b+(b+2)}{3}
&=\frac{b-2+b+b+2}{3} \\
&=\frac{3b}{3} \\
&=b.
\end{aligned}
$$

Angka $-2$ dan $+2$ saling meniadakan. Ini tidak bergantung pada nilai khusus $b$; itulah yang membuatnya menjadi bukti umum, bukan satu contoh saja.

### 4.2 Kontraposisi: membuktikan dari arah yang lebih mudah

Kita ingin membuktikan: **jika $n^2$ genap, maka $n$ genap**. Membuka bentuk $n^2$ untuk memperoleh bentuk $n$ terasa sulit. Kita bisa memakai pernyataan yang setara secara logis, disebut **kontraposisi**: jika $n$ *tidak* genap, maka $n^2$ *tidak* genap.

Untuk integer, tidak genap berarti ganjil. Tulis $n=2k+1$ dengan $k$ integer. Kuadratkan dengan mengalikan dua kurung:

$$
\begin{aligned}
n^2&=(2k+1)(2k+1) \\
&=4k^2+2k+2k+1 \\
&=4k^2+4k+1 \\
&=2(2k^2+2k)+1.
\end{aligned}
$$

Ekspresi $2k^2+2k$ integer, sehingga hasilnya berbentuk “2 dikali integer ditambah 1”: ganjil. Jadi $n$ ganjil mengharuskan $n^2$ ganjil. Dengan demikian, bila $n^2$ genap, $n$ tidak mungkin ganjil; $n$ harus genap.

### 4.3 Kontradiksi hanya bekerja bila klaimnya benar

Bukti kontradiksi dimulai dengan menganggap pernyataan yang ingin dibuktikan itu salah, lalu menunjukkan asumsi tersebut mustahil. Namun sebelum memakai cara ini, periksa klaimnya. Lembar responsi meminta membuktikan “untuk semua integer $a,b$, $a^2-4b-1\ne0$”. Klaim tersebut **salah**. Ambil $a=1$ dan $b=0$:

$$a^2-4b-1=1^2-4(0)-1=1-0-1=0.$$

Kita menemukan satu pasangan yang membuat hasil nol. Tidak ada bukti kontradiksi yang sah untuk klaim universal yang sudah dipatahkan oleh contoh ini. Coba juga $a=3,b=2$: $9-8-1=0$. Jika menemui soal serupa dalam kelas, jelaskan contoh penyangkal dan kemungkinan ada salah ketik pada pernyataannya; jangan menciptakan “bukti” untuk jawaban yang salah.

### 4.4 Bukti induksi: satu anak tangga dan aturan untuk naik

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

### 4.5 Induksi juga menjelaskan program: loop invariant

Sebuah **loop invariant** adalah pernyataan yang tetap benar setiap kali program kembali ke awal perulangan. Bayangkan kita ingin menghitung $n\times n$ tanpa operasi perkalian. Untuk $n\ge0$, tetapkan mula-mula $S=0$ dan $i=0$. Selama $i<n$, tambahkan $n$ ke $S$, lalu naikkan $i$ sebesar 1. Di akhir, kembalikan $S$.

Untuk $n=3$, keadaan setelah 0, 1, 2, dan 3 putaran berturut-turut adalah $(i,S)=(0,0),(1,3),(2,6),(3,9)$. Polanya ialah **$S=i\times n$**. Kita buktikan, bukan hanya menebak dari tabel.

- **Sebelum putaran pertama:** $i=0$ dan $S=0$, sehingga $S=i n$ karena $0=0\times n$.
- **Jika benar sebelum sebuah putaran:** misalkan $S=i n$. Setelah menambah $n$, nilai baru $S'=S+n=i n+n=(i+1)n$. Setelah menaikkan $i$, nilai baru $i'=i+1$. Karena itu $S'=i'n$. Pola tetap benar.
- **Saat berhenti:** kondisi $i<n$ sudah salah. Karena $i$ naik satu-satu dari 0 dan tidak melompati $n$, saat berhenti $i=n$. Masukkan ke invariant: $S=i n=n\times n=n^2$.

Langkah terakhir penting. “Invariant tetap benar” saja belum cukup; kita juga harus tahu kapan perulangan berhenti dan menghubungkan keadaan saat berhenti dengan hasil yang diminta. Penalaran ini adalah induksi yang diterapkan pada banyak putaran program.

## 5. Barisan, deret, dan simbol sigma: membaca kerja yang berulang

**Barisan** adalah daftar suku, misalnya $2,4,6,8,\ldots$. **Deret** adalah hasil penjumlahannya, misalnya $2+4+6+8+\cdots$. Perbedaan ini kecil tetapi penting: yang satu menjelaskan nilai pada posisi tertentu; yang lain menjelaskan totalnya.

### 5.1 Barisan aritmetika: bertambah dengan selisih tetap

Pada barisan $3,5,7,9,\ldots$, suku pertama $a=3$ dan setiap langkah menambah $d=2$. Mengapa suku ke-$n$ adalah $a+(n-1)d$? Suku pertama belum melakukan penambahan, suku kedua melakukan satu, dan suku ke-$n$ melakukan $n-1$ penambahan. Jadi suku ke-4 ialah $3+(4-1)2=3+6=9$.

Untuk jumlah $1+2+\cdots+n$, rumus bagian induksi menunjukkan $n(n+1)/2$. Jika perulangan melakukan 1 pekerjaan pada putaran pertama, 2 pada putaran kedua, dan seterusnya sampai $n$, total pekerjaan *persis* jumlah itu. Nanti Bab 4 membandingkan rumus persis dengan kelas pertumbuhannya.

### 5.2 Notasi sigma hanya singkatan untuk daftar penjumlahan

Simbol $\sum_{i=1}^{4}i$ dibaca “jumlahkan $i$ dari 1 sampai 4”. Tulis sukunya sebelum memakai rumus:

$$\sum_{i=1}^{4}i=1+2+3+4=10.$$

Huruf $i$ adalah *indeks penjumlahan*: ia mengambil nilai 1, lalu 2, lalu 3, lalu 4. Misalnya $\sum_{i=1}^{4}2i=2(1)+2(2)+2(3)+2(4)=2+4+6+8=20$. Mengganti huruf $i$ menjadi $j$ tidak mengubah hasil jika batas dan ekspresinya juga diganti secara konsisten.

Perhatikan batasnya: $\sum_{i=0}^{n-1}i$ memuat $0,1,\ldots,n-1$, sehingga hasilnya $n(n-1)/2$. Sementara $\sum_{i=1}^{n}i$ memuat $1,2,\ldots,n$ dan hasilnya $n(n+1)/2$. Keduanya punya $n$ suku, tetapi bukan suku yang sama. Coba $n=4$: jumlah pertama $0+1+2+3=6$, jumlah kedua $1+2+3+4=10$.

### 5.3 Barisan geometri: dikali rasio tetap

Barisan $2,6,18,54,\ldots$ dimulai dari $a=2$ dan tiap suku dikali $r=3$. Suku pertama ialah $2\times3^0$, suku kedua $2\times3^1$, dan suku ke-$n$ ialah $2\times3^{n-1}$. Pangkatnya $n-1$ karena belum ada perkalian 3 saat kita masih di suku pertama.

Untuk jumlah $G=1+r+r^2+\cdots+r^k$, kalikan kedua sisi dengan $r$:

$$rG=r+r^2+\cdots+r^k+r^{k+1}.$$

Sekarang kurangi persamaan pertama dari persamaan kedua. Suku $r,r^2,\ldots,r^k$ saling habis, sehingga $rG-G=r^{k+1}-1$. Keluarkan $G$: $(r-1)G=r^{k+1}-1$. Jika $r\ne1$, bagi kedua sisi dengan $r-1$:

$$G=\frac{r^{k+1}-1}{r-1}.$$

Untuk $r=2$ dan $k=3$, daftar aslinya $1+2+4+8=15$; rumus memberi $(2^4-1)/(2-1)=15$. Jika $r=1$, jangan membagi dengan nol: ada $k+1$ suku yang semuanya 1, jadi jumlahnya $k+1$.

### 5.4 Logaritma adalah pertanyaan “berapa kali dikali?”

$\log_2 8=3$ karena $2^3=8$. Bila jumlah kemungkinan menjadi dua kali lipat pada setiap level pohon, setelah tiga level ada $2^3=8$ kemungkinan. Sebaliknya, jika ukuran masalah dibagi dua terus-menerus, dari 8 menjadi 4, 2, 1; diperlukan tiga pembagian. Dari $n$ ke 1 setelah $k$ pembagian: $n/2^k=1$, maka $2^k=n$ dan $k=\log_2n$ bila $n$ pangkat dua. Jika bukan pangkat dua, pembulatan menentukan hitungan tepat, tetapi idenya tetap sama.

## 6. Menghitung kemungkinan tanpa mendaftar semuanya

### 6.1 Aturan tambah dan kali

Di kantin ada 3 pilihan nasi dan 2 pilihan mi. Jika seseorang memilih **satu nasi atau satu mi**, ada $3+2=5$ pilihan, karena kedua kelompok tidak tumpang tindih. Ini **aturan penjumlahan**.

Jika seseorang memilih **satu nasi dan satu minuman** dari 4 jenis minuman, setiap nasi dapat dipasangkan dengan 4 minuman. Untuk 3 nasi, ada $3\times4=12$ pasangan. Ini **aturan perkalian**. Kata “atau” dan “dan” membantu, tetapi selalu periksa apakah pilihan saling lepas atau apakah semua pasangan diperbolehkan.

### 6.2 Faktorial, urutan, dan mengapa $0!=1$

Ada tiga buku berbeda A, B, C. Untuk menyusunnya berurutan, posisi pertama punya 3 pilihan, posisi kedua tinggal 2, posisi ketiga tinggal 1. Jadi ada $3\times2\times1=6$ susunan. Hasil perkalian $n(n-1)\cdots2\times1$ ditulis $n!$ dan dibaca “$n$ faktorial”.

Mengapa $0!=1$, bukan 0? Menyusun nol benda mempunyai **satu** hasil yang mungkin: susunan kosong. Aturan perkalian mengharuskan perkalian tanpa faktor bernilai 1 agar rumus tetap konsisten. Contoh: $1!=1\times0!$ mengharuskan $0!=1$.

### 6.3 Memilih kelompok berbeda dari memberi jabatan

Lembar responsi meminta memilih 2 orang dari 5 untuk sebuah sub-tim. Jika kita menghitung “orang pertama” lalu “orang kedua”, kita mendapat $5\times4=20$. Namun tim A-B sama dengan B-A: urutan tidak bermakna. Setiap tim dihitung dua kali. Karena itu bagi 2 dan dapatkan $20/2=10$ tim.

Untuk memilih 4 dari 10 proyek, hitungan berurutan adalah $10\times9\times8\times7=5040$. Setiap kelompok 4 proyek yang sama dapat muncul dalam $4!=24$ urutan. Maka banyak kelompok ialah $5040/24=210$. Inilah alasan rumus kombinasi

$$\binom nr=\frac{n!}{r!(n-r)!}.$$

Bagian $n!/(n-r)!$ menghitung pemilihan berurutan sebanyak $r$ benda; bagian $r!$ membuang penghitungan ulang akibat urutan internal yang tidak penting. Jika jabatan *ketua* dan *wakil* berbeda, urutan memang penting, sehingga untuk 2 dari 5 hasilnya $5\times4=20$, bukan 10.

Memilih **nol** proyek dari 10 juga punya satu cara, yaitu tidak memilih proyek mana pun. Rumusnya konsisten: $\binom{10}{0}=10!/(0!10!)=1$.

### 6.4 Mengapa ada $2^n$ subset?

*Subset* berarti pilihan sebagian anggota dari suatu kelompok, termasuk pilihan kosong dan pilihan seluruh anggota. Untuk setiap barang ada dua keputusan: ambil atau tidak. Jika ada 3 barang A, B, C, keputusan yang mungkin berjumlah $2\times2\times2=2^3=8$. Delapan hasilnya: tidak mengambil apa pun; A; B; C; A-B; A-C; B-C; A-B-C.

Ada cara lain menghitungnya: kelompokkan menurut banyak barang yang dipilih. Memilih 0 memberi $\binom30=1$, memilih 1 memberi $\binom31=3$, memilih 2 memberi $\binom32=3$, dan memilih 3 memberi $\binom33=1$. Jumlahnya $1+3+3+1=8$. Untuk $n$ barang, dua cara hitung atas kumpulan hasil yang sama memberi

$$\sum_{r=0}^{n}\binom nr=2^n.$$

Ini juga jawaban soal pertama UTS 2018 tentang mengambil 0 sampai $n$ barang, dengan asumsi tiap barang berbeda dan satu barang hanya bisa diambil sekali. Jika barangnya tidak berbeda atau boleh diambil berkali-kali, modelnya berubah; nyatakan asumsi sebelum memakai rumus.

### 6.5 Pohon keputusan: kemungkinan pada setiap kedalaman

Bayangkan setiap simpul pada sebuah pohon mempunyai 2 anak. Akar ada pada **kedalaman 0**. Pada kedalaman 0 ada 1 simpul; kedalaman 1 ada 2; kedalaman 2 ada 4; kedalaman 3 ada 8. Total sampai kedalaman 3 adalah $1+2+4+8=15$ simpul. Jumlah pada kedalaman $d$ ialah $2^d$ karena setiap perpindahan menggandakan banyak simpul.

Secara umum, bila setiap simpul punya $b$ anak, level kedalaman $d$ memuat $b^d$ simpul. Total dari akar sampai kedalaman $d$ adalah $1+b+b^2+\cdots+b^d$. Rumus deret geometri memberi $(b^{d+1}-1)/(b-1)$ untuk $b\ne1$.

> **Hati-hati membaca soal.** “Level ke-2” bisa berarti kedalaman 1 bila akar disebut level 1, atau kedalaman 2 bila akar disebut level 0. Pada responsi, bagian ini tidak menetapkan konvensi secara tegas. Tulis konvensi yang dipakai: dengan akar level 1 dan 3 cabang per simpul, level 2 berisi 3 simpul; dengan akar level 0, level 2 berisi 9 simpul.

### 6.6 Menghitung gabungan yang tumpang tindih

Misalkan A adalah siswa yang suka matematika dan B adalah siswa yang suka pemrograman. Jika ada 5 siswa di A dan 4 siswa di B, belum tentu ada 9 siswa berbeda. Orang yang masuk kedua kelompok terhitung dua kali. Bila irisan $A\cap B$ berisi 2 siswa, jumlah yang berada di setidaknya satu kelompok ialah $5+4-2=7$.

Untuk tiga kelompok A, B, C, mula-mula jumlahkan $|A|+|B|+|C|$. Kurangi tiga irisan pasangan karena anggota dua kelompok dihitung dua kali. Namun anggota yang berada di **ketiganya** semula dihitung tiga kali lalu dikurangi tiga kali, sehingga hasil sementara nol. Tambahkan irisan tiga sekali agar tiap orang dihitung satu kali:

$$
\begin{aligned}
|A\cup B\cup C|={}&|A|+|B|+|C| \\
&-|A\cap B|-|A\cap C|-|B\cap C| \\
&+|A\cap B\cap C|.
\end{aligned}
$$

Pada soal responsi, ukurannya berturut-turut 50, 30, 20; irisan pasangan 15, 10, 5; irisan tiga 2. Hitung perlahan: $50+30+20=100$; jumlah tiga irisan pasangan $15+10+5=30$; jadi sementara $100-30=70$; tambahkan 2 sehingga hasilnya **72**. Menulis setiap subtotal membantu menghindari lupa mengembalikan irisan tiga.

## 7. Peluang, sisa pembagian, dan hitungan langkah: jembatan ke bab berikutnya

### 7.1 Rata-rata yang berbobot peluang

Bayangkan ada empat kartu yang sama peluangnya untuk terambil: satu kartu bertanda “target di awal” dan tiga kartu bertanda “target tidak ada”. Karena keempat kartu sama mungkin, peluang kasus pertama $1/4$ dan peluang kasus kedua $3/4$. Kedua peluang berjumlah $1/4+3/4=1$, karena tepat salah satu kasus harus terjadi. Jika kartunya tidak sama peluangnya, kita tidak boleh memakai banyak kartu sebagai peluang tanpa alasan tambahan.

Misalkan sebuah pencarian perlu 1 perbandingan ketika target berada di awal array dan 5 perbandingan ketika target tidak ada. Jika peluang kasus pertama $1/4$ dan kasus kedua $3/4$, rata-rata banyak perbandingan ialah

$$E=\frac14(1)+\frac34(5)=\frac14+\frac{15}4=\frac{16}4=4.$$

Mengapa bukan $(1+5)/2=3$? Karena dua kasus itu tidak sama sering. **Nilai harapan** memberi bobot berdasarkan peluang. Angka 4 bukan janji bahwa setiap pencarian memakai tepat 4 perbandingan; setiap kejadian tetap memakai 1 atau 5. Bab 3 akan mengulas asumsi peluang dengan lebih hati-hati.

### 7.2 Sisa pembagian dapat menggantikan daftar kasus panjang

$17\equiv5\pmod{12}$ berarti 17 dan 5 berbeda sebesar kelipatan 12: $17-5=12$. Keduanya juga memiliki sisa 5 jika dibagi 12. Simbol ini berguna untuk mengelompokkan angka menurut sisa pembagiannya.

Contoh: bilangan ganjil berbentuk $2k+1$. Kuadratnya $4k^2+4k+1=4k(k+1)+1$. Karena $4k(k+1)$ kelipatan 4, sisa kuadrat bilangan ganjil bila dibagi 4 adalah 1. Bentuk singkatnya $n^2\equiv1\pmod4$ untuk $n$ ganjil. Kita tidak perlu mencoba semua bilangan ganjil satu per satu.

### 7.3 Mengapa kondisi loop diperiksa satu kali lebih banyak?

Perhatikan prosedur: mulai dengan $i=1$; selama $i\le n$, lakukan satu pekerjaan lalu naikkan $i$ sebesar 1. Untuk $n=3$, kondisi diperiksa saat $i=1$ (benar), $i=2$ (benar), $i=3$ (benar), dan $i=4$ (salah). Badan loop berjalan 3 kali, tetapi kondisi diperiksa **4 kali**. Secara umum: $n$ pemeriksaan yang berhasil, ditambah satu pemeriksaan terakhir yang menyebabkan berhenti, jadi $n+1$.

Jika pekerjaan pada putaran ke-$i$ memerlukan $i$ operasi, totalnya bukan $n$ tetapi $1+2+\cdots+n=n(n+1)/2$. Dari sini matematika bab ini mulai berubah menjadi analisis algoritme yang sesungguhnya.

## 8. Cara memeriksa pemahaman sebelum mengajar

Ketika menemui soal baru, ajukan lima pertanyaan secara berurutan.

1. Apa objek konkretnya: angka, elemen array, kelompok, atau langkah program?
2. Apa yang berubah dan apa yang tetap: nilai $n$, posisi, banyak pilihan, atau peluang?
3. Apa yang harus dibuktikan untuk **semua** kasus, dan apa yang cukup diperiksa dengan satu contoh?
4. Operasi apa yang dilakukan pada kedua sisi persamaan, atau alasan apa yang membolehkan tiap perubahan bentuk?
5. Dapatkah hasilnya diperiksa dengan contoh kecil seperti $n=1,2,3$?

Contoh kecil adalah alat pemeriksa, bukan pengganti bukti umum. Jika contoh kecil tidak cocok, ada kesalahan. Jika cocok, kita masih perlu alasan mengapa hal yang sama berlaku untuk semua input.

## 9. Latihan bertingkat

Tutup pembahasan di bawah terlebih dahulu. Untuk soal yang diadaptasi dari responsi atau ujian lama, istilah dan susunannya ditulis ulang agar bisa dikerjakan tanpa melihat PDF. Label *adaptasi* bukan berarti teks soal ini salinan resmi.

1. **Mudah — persamaan.** Selesaikan $3x+4=19$. Tuliskan operasi yang dilakukan pada kedua sisi dan periksa jawabannya.
2. **Mudah — interval.** Indeks integer apa saja dalam $[2,6)$? Mengapa banyaknya sama dengan $6-2$?
3. **Mudah — logika.** Apakah “$x+2=5$” merupakan proposisi sebelum $x$ diberi nilai? Ubah menjadi dua proposisi berbeda, satu benar dan satu salah.
4. **Mudah — pembuktian langsung; adaptasi responsi 1.** Buktikan: jika integer $n$ genap, $3n+2$ genap.
5. **Mudah — deret.** Hitung $1+2+\cdots+20$ dengan rumus dan periksa dengan cara memasangkan suku ujung.
6. **Sedang — titik potong; adaptasi responsi 1.** Temukan titik potong $f(x)=3x-4$ dan $g(x)=2x+1$. Periksa pada kedua fungsi.
7. **Sedang — kombinasi; adaptasi responsi 1.** Ada 5 anggota. Berapa sub-tim dua orang yang berbeda? Jelaskan mengapa hasilnya bukan $5\times4$.
8. **Sedang — pohon; adaptasi responsi 1.** Akar berada pada kedalaman 0. Setiap simpul memiliki 2 anak sampai kedalaman 3. Berapa simpul pada kedalaman 3 dan berapa total simpul?
9. **Sedang — himpunan; adaptasi responsi 1.** Diberikan $|A|=50$, $|B|=30$, $|C|=20$, $|A\cap B|=15$, $|A\cap C|=10$, $|B\cap C|=5$, dan $|A\cap B\cap C|=2$. Berapa anggota $A\cup B\cup C$? Terangkan mengapa irisan tiga ditambahkan.
10. **Sedang — induksi; adaptasi responsi 1.** Buktikan $1+2+\cdots+n=n(n+1)/2$ untuk setiap integer $n\ge1$. Jangan melewati langkah menyamakan penyebut.
11. **Sulit — klaim salah; adaptasi responsi 1.** Nilailah klaim “untuk semua integer positif $n$, $n^2+2$ ganjil”. Berikan bukti bila benar atau contoh penyangkal bila salah. Dapatkah klaim diperbaiki dengan syarat tambahan?
12. **Sulit — klaim salah; adaptasi responsi 1.** Nilailah klaim “untuk setiap integer $a,b$, $a^2-4b-1\ne0$”. Jelaskan mengapa permintaan untuk membuktikannya dengan kontradiksi tidak dapat dipenuhi seperti tertulis.
13. **Sulit — parabola; adaptasi responsi 1.** Cari semua titik potong $y=x^2-4x+3$ dan $y=x+1$. Jelaskan asal dua jawabannya.
14. **Sulit — subset; adaptasi UTS 2018.** Ada $n$ barang yang berbeda, setiap barang boleh diambil paling banyak sekali. Berapa cara memilih 0 sampai $n$ barang? Buktikan dengan keputusan per barang dan dengan mengelompokkan hasil menurut banyak barang yang diambil.
15. **Sulit — induksi baru.** Buktikan $1+3+5+\cdots+(2n-1)=n^2$ untuk $n\ge1$. Jelaskan dengan jelas dari mana suku $2k+1$ muncul pada langkah $k\to k+1$.
16. **Sulit — program.** Sebuah loop dimulai dengan $S=0,i=0$. Selama $i<n$, ia melakukan $S\leftarrow S+2$ dan $i\leftarrow i+1$. Untuk $n\ge0$, tulis invariant yang menghubungkan $S$ dan $i$, buktikan sebelum loop, sesudah satu putaran, dan saat berhenti. Apa hasil akhirnya?

## 10. Pembahasan latihan, tanpa lompatan langkah

### 1. Persamaan

Mulai dari $3x+4=19$. Kurangi 4 pada **kedua** sisi: $3x+4-4=19-4$, sehingga $3x=15$. Bagi kedua sisi dengan 3: $x=5$. Pemeriksaan: $3(5)+4=15+4=19$. Jadi $x=5$ benar.

### 2. Interval

$[2,6)$ memasukkan 2 dan mengecualikan 6. Indeks integer yang tersisa: 2, 3, 4, 5. Ada empat angka. Selisih batas $6-2=4$ cocok karena kita mulai dari 2 dan berhenti tepat sebelum 6.

### 3. Proposisi

Kalimat $x+2=5$ belum menjadi proposisi tertutup karena nilai $x$ belum ditentukan. “Untuk $x=3$, $x+2=5$” benar sebab $3+2=5$. “Untuk $x=4$, $x+2=5$” salah sebab $4+2=6\ne5$. Sekarang masing-masing punya nilai benar atau salah yang jelas.

### 4. Bukti langsung

Karena $n$ genap, tulis $n=2k$ untuk suatu integer $k$. Maka $3n+2=3(2k)+2=6k+2=2(3k+1)$. Nilai $3k+1$ integer, sehingga $3n+2$ berbentuk $2$ kali integer. Itu persis definisi genap.

### 5. Jumlah 1 sampai 20

Rumus memberi $20(20+1)/2=20\times21/2=10\times21=210$. Cara pasangan: $(1+20)=(2+19)=\cdots=(10+11)=21$. Ada 10 pasangan, sehingga jumlahnya $10\times21=210$. Dua cara saling memeriksa.

### 6. Titik potong

Samakan output: $3x-4=2x+1$. Kurangi $2x$ pada kedua sisi: $x-4=1$. Tambahkan 4 pada kedua sisi: $x=5$. Masukkan ke fungsi pertama: $y=3(5)-4=11$. Fungsi kedua juga memberi $y=2(5)+1=11$. Jadi titiknya $(5,11)$.

### 7. Tim dua orang

Jika urutan dicatat, ada 5 pilihan orang pertama dan 4 pilihan orang kedua, total $5\times4=20$. Tim A-B dan B-A sama, sehingga setiap tim muncul dua kali. Bagi 20 dengan 2: ada **10** tim. Rumus kombinasi memberi hasil yang sama, $\binom52=5!/(2!3!)=(5\times4)/(2\times1)=10$.

### 8. Pohon biner

Kedalaman 0 berisi 1 simpul. Karena setiap simpul punya 2 anak, kedalaman 1 berisi 2, kedalaman 2 berisi 4, dan kedalaman 3 berisi 8. Jadi pada kedalaman 3 ada **8** simpul. Totalnya $1+2+4+8=15$. Jangan menghitung hanya tiga level: dari kedalaman 0 sampai 3 terdapat empat level.

### 9. Gabungan tiga himpunan

Jumlah ukuran awal $50+30+20=100$. Kurangi irisan pasangan $15+10+5=30$, sehingga tersisa 70. Tambahkan irisan tiga 2 sehingga $|A\cup B\cup C|=72$. Anggota yang berada di ketiga kelompok semula dihitung 3 kali, lalu dikurangi 3 kali; tambahan terakhir membuatnya terhitung tepat 1 kali.

### 10. Induksi jumlah bilangan pertama

Basis $n=1$: kiri 1, kanan $1(2)/2=1$. Anggap benar untuk $n=k$, sehingga $1+\cdots+k=k(k+1)/2$. Untuk $k+1$, tambahkan satu suku baru: $1+\cdots+k+(k+1)=k(k+1)/2+(k+1)$. Tulis suku kedua sebagai $2(k+1)/2$, karena $2/2=1$. Jumlahkan pembilang: $[k(k+1)+2(k+1)]/2$. Keluarkan $(k+1)$: $(k+1)(k+2)/2$. Itu bentuk rumus untuk $n=k+1$. Basis dan langkah induksi selesai.

### 11. Pernyataan $n^2+2$ selalu ganjil

Klaimnya salah. Pilih $n=2$, yang positif: $n^2+2=4+2=6$, genap. Satu contoh ini cukup membantah kata “untuk semua”. Pernyataan dapat diperbaiki menjadi: **jika $n$ positif dan ganjil, maka $n^2+2$ ganjil**. Sebab $n=2k+1$ menghasilkan $n^2+2=4k^2+4k+3=2(2k^2+2k+1)+1$, yaitu bentuk ganjil.

### 12. Pernyataan $a^2-4b-1\ne0$

Ambil $a=1$ dan $b=0$. Keduanya integer dan $1^2-4(0)-1=0$. Jadi klaim universal itu salah. Permintaan “buktikan dengan kontradiksi” tidak dapat menghasilkan bukti yang sah untuk kalimat seperti tertulis. Contoh penyangkal harus disampaikan lebih dulu.

### 13. Titik potong parabola dan garis

Titik potong memenuhi $x^2-4x+3=x+1$. Kurangi $x+1$ pada kedua sisi sehingga $x^2-5x+2=0$. Dalam rumus kuadrat, $a=1,b=-5,c=2$. Diskriminannya $b^2-4ac=(-5)^2-4(1)(2)=25-8=17$, positif. Karena akar kuadrat bilangan positif memiliki dua tanda, diperoleh $x=(5+\sqrt{17})/2$ dan $x=(5-\sqrt{17})/2$. Dari $y=x+1$, koordinat $y$ masing-masing $(7+\sqrt{17})/2$ dan $(7-\sqrt{17})/2$. Kedua jawaban muncul karena persamaan kuadratnya mempunyai dua akar real.

### 14. Memilih 0 sampai $n$ barang

Cara pertama: setiap barang punya dua keputusan independen, ambil atau tidak. Untuk $n$ barang berbeda, aturan perkalian memberi $2\times2\times\cdots\times2=2^n$ hasil. Cara kedua: bila tepat $r$ barang diambil, ada $\binom nr$ hasil. Nilai $r$ boleh 0, 1, dan seterusnya sampai $n$. Kelompok-kelompok ini tidak tumpang tindih dan mencakup semua hasil, sehingga jumlahnya $\sum_{r=0}^{n}\binom nr$. Karena kedua cara menghitung kumpulan hasil yang sama, jumlah tersebut sama dengan $2^n$. Untuk $n=3$, periksa $1+3+3+1=8=2^3$.

### 15. Jumlah bilangan ganjil pertama

Basis $n=1$: kiri 1, kanan $1^2=1$. Anggap jumlah $k$ suku ganjil pertama adalah $k^2$. Suku ganjil ke-$j$ berbentuk $2j-1$; maka suku setelah suku ke-$k$ memiliki indeks $j=k+1$ dan nilainya $2(k+1)-1=2k+1$. Jumlah baru ialah $k^2+(2k+1)=k^2+2k+1=(k+1)^2$. Itu rumus yang harus ditunjukkan untuk $k+1$. Jadi klaim berlaku untuk setiap $n\ge1$.

### 16. Loop yang menambahkan 2

Invariant-nya $S=2i$. Sebelum loop, $S=0$ dan $i=0$, sehingga $0=2(0)$. Andaikan sebelum suatu putaran $S=2i$. Setelah perintah pertama, $S'=S+2=2i+2=2(i+1)$. Setelah perintah kedua, $i'=i+1$, sehingga $S'=2i'$ dan invariant tetap benar. Untuk $n\ge0$, $i$ mulai dari 0 dan naik satu-satu sampai kondisi $i<n$ salah, yakni saat $i=n$. Maka $S=2i=2n$. Jumlah putarannya tepat $n$; bila $n=0$, loop tidak berjalan dan hasil 0 tetap sesuai.

## Sumber dan batas pemakaian

Materi inti dan tema soal bab ini diturunkan dari **Kuliah 1 Analisis Algoritme 2026–2027**, **Lembar Kerja Responsi Pertemuan 1**, **Latihan Soal K1**, dan **UTS Analisis Algoritme 2018** dalam arsip yang diberikan Sensei. Buku *Introduction to Algorithms*, edisi ketiga, oleh Cormen, Leiserson, Rivest, dan Stein dipakai sebagai contoh **alur penyajian**: mulai dari masalah, gagasan, alasan, lalu latihan. Cerita, kalimat, dan pembahasan di sini ditulis sendiri; bab ini tidak menyalin uraian buku tersebut. Beberapa slide kuliah berupa gambar sehingga teks yang diekstrak tidak memuat setiap detail visual; untuk gambar tertentu, lihat PDF aslinya.

**Lanjutkan ke [Bab 2 — Pertumbuhan Fungsi](bab-02-pertumbuhan-fungsi.md)** setelah bisa menjelaskan sendiri mengapa jumlah $1+\cdots+n$ bernilai $n(n+1)/2$ dan mengapa suatu loop yang berjalan $n$ kali memeriksa kondisinya $n+1$ kali.
