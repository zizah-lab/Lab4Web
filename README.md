# Lab4Web - Praktikum 4: CSS Layout

Laporan Praktikum Pemrograman Web: **CSS Layout**.

| | |
|---|---|
| **Nama** | Azizah Rachmatania |
| **NIM** | 312510159 |
| **Kelas** | I251B |
| **Mata Kuliah** | Pemrograman Web |
| **Dosen** | Agung Nugroho |
| **Universitas** | Universitas Pelita Bangsa, Bekasi |

---

## Tujuan Praktikum

1. Memahami struktur dasar pembuatan layout.
2. Memahami konsep box element.
3. Memahami CSS Floating.
4. Memahami HTML 5 Semantic Elements.
5. Membuat layout web sederhana.

## Struktur Folder

```
Lab4Web/
├── Dokumentasi/          # screenshot setiap langkah praktikum
├── lab4_box.html         # latihan Box Element, Float, dan Clearfix
├── lab4_layout/
│   ├── home.html         # halaman layout sederhana
│   └── style.css         # CSS untuk layout
└── README.md
```

## Dasar Teori Singkat

**Box element.** Setiap elemen HTML pada dasarnya adalah sebuah kotak (box) yang tersusun dari empat lapis: *content* (isi), *padding* (jarak isi ke garis tepi), *border* (garis tepi), dan *margin* (jarak ke elemen lain). Konsep inilah yang dipakai untuk mengatur tata letak halaman.

**CSS float dan clear.** Secara bawaan, elemen `div` tampil bertumpuk ke bawah karena sifatnya *block*. Properti `float` membuat elemen "mengambang" ke kiri atau kanan sehingga elemen lain bisa berjajar di sampingnya. Karena elemen yang di-float keluar dari alur normal, elemen setelahnya perlu diatur dengan `clear` agar tidak ikut naik ke samping.

**HTML5 semantic elements.** Tag seperti `<header>`, `<nav>`, `<section>`, `<aside>`, dan `<footer>` memberi arti pada bagian-bagian halaman. Hasilnya kode lebih mudah dibaca manusia dan lebih mudah dipahami mesin (misalnya mesin pencari), dibanding memakai `div` untuk semuanya.

---

## Bagian 1: Box Element dan CSS Float

File: `lab4_box.html`

### Langkah 1: Membuat Box Element dengan CSS Float

Pertama dibuat dokumen HTML dengan sebuah `<header>` berisi judul "Box Element", lalu sebuah `<section>` yang berisi tiga elemen `div` (Div 1, Div 2, Div 3). Masing-masing div diberi class (`div1`, `div2`, `div3`) supaya bisa diberi warna latar yang berbeda.

CSS ditulis di dalam tag `<style>`:

```css
div {
    float: left;
    padding: 10px;
}
.div1 { background: red; }
.div2 { background: yellow; }
.div3 { background: green; }
```

- `float: left` membuat setiap div menempel ke sisi kiri dan berjajar ke samping, tidak lagi bertumpuk ke bawah. Lebar tiap div jadi menyesuaikan isinya.
- `padding: 10px` memberi ruang 10 piksel antara teks dan tepi kotak, sehingga warna latar terlihat lebih lebar dari tulisannya.
- Class `.div1`, `.div2`, `.div3` hanya mengatur warna latar (merah, kuning, hijau) agar batas tiap box terlihat jelas.

**Kode:**

![Kode box element](Dokumentasi/1%20.png)

**Hasil:** tiga kotak berwarna tampil berjajar horizontal dari kiri ke kanan. Tanpa `float`, ketiganya akan tampil memanjang penuh dan bertumpuk ke bawah.

![Hasil box element](Dokumentasi/1.%28hasil%29.png)

### Langkah 2: Mengatur Clearfix

Pada langkah ini ditambahkan `div4` setelah `div3`. Masalahnya, karena `div` sudah diatur `float: left` secara global, `div4` otomatis ikut naik dan berjajar di samping `div3`. Padahal yang diinginkan `div4` berada di baris baru di bawahnya.

Solusinya adalah property `clear`:

```css
.div4 {
    background-color: blue;
    clear: left;
    float: none;
}
```

- `clear: left` menyuruh elemen ini untuk tidak boleh berada di samping elemen yang di-float ke kiri, sehingga ia turun ke baris berikutnya.
- `float: none` membatalkan float bawaan dari selector `div`, jadi `div4` kembali menjadi block biasa yang memanjang selebar halaman.

**Kode:**

![Kode clearfix](Dokumentasi/2%20.png)

**Hasil:** Div 4 berwarna biru berada di bawah Div 1-3 dan memanjang penuh selebar halaman. Sesuai arahan modul, nilai `clear` lain (`right`, `both`) juga bisa dicoba untuk melihat perbedaannya. Nilai `both` paling aman karena membersihkan float dari kiri maupun kanan.

![Hasil clearfix](Dokumentasi/2.%28hasil%29.png)

---

## Bagian 2: Membuat Layout Web Sederhana

Folder: `lab4_layout/` (file `home.html` dan `style.css`)

### Langkah 3: Membuat Kerangka Layout dengan HTML5 Semantic Elements

Dibuat file `home.html` yang menghubungkan stylesheet lewat `<link rel="stylesheet" href="style.css">`. Seluruh isi halaman dibungkus `<div id="container">`, lalu di dalamnya disusun kerangka dengan elemen semantik:

| Elemen | Fungsi |
|---|---|
| `<header>` | Judul halaman ("Layout Sederhana") |
| `<nav>` | Menu navigasi (Home, Artikel, Kontak, About) |
| `<section id="hero">` | Panel utama berisi sambutan "Hello World!" |
| `<section id="wrapper">` | Pembungkus yang menampung main content dan sidebar |
| `<section id="main">` | Konten utama (kolom kiri) |
| `<aside id="sidebar">` | Konten pendamping (kolom kanan) |
| `<footer>` | Bagian bawah halaman |

Struktur `wrapper` yang membungkus `main` dan `sidebar` disengaja, karena kedua kolom itu nanti akan disusun berdampingan dan perlu satu induk yang sama.

**Kode:**

![Kode kerangka layout](Dokumentasi/3.%20layaout%20sederhana.png)

**Hasil:** tampilan masih polos tanpa warna karena CSS belum ditambahkan. Ini normal, karena HTML hanya mendefinisikan struktur, sedangkan tampilan diatur oleh CSS.

![Hasil kerangka layout](Dokumentasi/3.layaout%20sederhana.png)

### Langkah 4: CSS Dasar dan Header

File `style.css` dimulai dengan beberapa pengaturan dasar:

```css
* {
    margin: 0;
    padding: 0;
}

body {
    line-height: 1;
    font-size: 100%;
    font-family: 'Open Sans', sans-serif;
    color: #5a5a5a;
}

#container {
    width: 980px;
    margin: 0 auto;
    box-shadow: 0 0 1em #cccccc;
}
```

- `@import` memuat font **Open Sans** dari Google Fonts.
- Selector `*` (reset CSS) menghapus margin dan padding bawaan browser, supaya tampilan konsisten di semua browser dan jarak sepenuhnya kita atur sendiri.
- `body` mengatur font, ukuran, dan warna teks abu-abu gelap `#5a5a5a`.
- `#container` dibuat selebar `980px`. `margin: 0 auto` membuat container berada di tengah halaman, dan `box-shadow` memberi bayangan tipis di sekelilingnya.
- `header` diberi `padding: 20px`, dan `header h1` diberi warna abu-abu muda `#b5b5b5` dengan margin `20px 10px`.

**Kode:**

![Kode CSS dasar](Dokumentasi/4%20.png)

**Hasil:** judul "Layout Sederhana" tampil dengan font Open Sans berwarna abu-abu, dan halaman berada di tengah.

![Hasil CSS dasar](Dokumentasi/4.%28hasil%29.png)

### Langkah 5: Membuat Navigasi

```css
nav {
    display: block;
    background-color: #1f5faa;
}
nav a {
    padding: 15px 30px;
    display: inline-block;
    color: #ffffff;
    font-size: 14px;
    text-decoration: none;
    font-weight: bold;
}
nav a.active,
nav a:hover {
    background-color: #2b83ea;
}
```

- `nav` diberi latar biru tua `#1f5faa` sehingga menjadi bar menu selebar container.
- `nav a` memakai `display: inline-block` supaya link berjajar horizontal sekaligus bisa diberi padding. `padding: 15px 30px` memperluas area klik, sedangkan `text-decoration: none` menghilangkan garis bawah link dan `color: #ffffff` membuat teks putih.
- `nav a.active, nav a:hover` memberi warna biru lebih terang `#2b83ea` pada menu yang sedang aktif (`class="active"`) dan pada menu yang sedang di-hover mouse.

**Kode:**

![Kode navigasi](Dokumentasi/5%20.png)

**Hasil:** menu berubah menjadi bar biru dengan teks putih tebal, dan menu "Home" ditandai warna biru lebih terang karena berstatus aktif.

![Hasil navigasi](Dokumentasi/5.%28hasil%29.png)

### Langkah 6: Membuat Hero Panel

Hero panel adalah bagian sambutan di bawah menu. Isinya berupa judul `Hello World!`, satu paragraf teks, dan link `Learn more »`.

```css
#hero {
    background-color: #e4e4e5;
    padding: 50px 20px;
    margin-bottom: 20px;
}
#hero h1 {
    margin-bottom: 20px;
    font-size: 35px;
}
#hero p {
    margin-bottom: 20px;
    font-size: 18px;
    line-height: 25px;
}
```

- `#hero` diberi latar abu-abu muda dan `padding: 50px 20px` agar isinya punya ruang lega di atas-bawah (50px) dan kiri-kanan (20px). `margin-bottom: 20px` memberi jarak ke bagian di bawahnya.
- `#hero h1` memperbesar judul menjadi 35px, sedangkan `#hero p` mengatur ukuran teks 18px dengan tinggi baris 25px agar nyaman dibaca.

**Kode:**

![Kode hero panel](Dokumentasi/6%20.png)

**Hasil:** muncul panel abu-abu lebar berisi judul dan paragraf di bawah menu.

![Hasil hero panel](Dokumentasi/6.%28hasil%29.png)

### Langkah 7: Mengatur Layout Main dan Sidebar, Sidebar Widget, dan Footer

Di sinilah konsep float dipakai untuk membuat layout dua kolom:

```css
#main {
    float: left;
    width: 640px;
    padding: 20px;
}
#sidebar {
    float: left;
    width: 260px;
    padding: 20px;
}
```

Kedua elemen di-float ke kiri sehingga berdampingan. Lebar total `640 + 260 = 900px` ditambah padding `20px` di kiri-kanan masing-masing (`40 + 40 = 80px`) menjadi `980px`, tepat sama dengan lebar `#container`. Jika angkanya melebihi 980px, salah satu kolom akan turun ke bawah.

Di dalam sidebar ditambahkan dua **widget**, yaitu *Widget Header* (daftar lima link) dan *Widget Text* (satu paragraf), dengan styling:

```css
.widget-box {
    border: 1px solid #eee;
    margin-bottom: 20px;
}
.widget-box .title {
    padding: 10px 16px;
    background-color: #428bca;
    color: #fff;
}
.widget-box ul { list-style-type: none; }
.widget-box li { border-bottom: 1px solid #eee; }
.widget-box li a {
    padding: 10px 16px;
    color: #333;
    display: block;
    text-decoration: none;
}
.widget-box li:hover a { background-color: #eee; }
```

- Tiap widget dibungkus border tipis, dengan judul berlatar biru `#428bca` dan teks putih.
- `list-style-type: none` menghilangkan bullet pada daftar, dan `border-bottom` memberi garis pemisah antar link.
- Link memakai `display: block` agar seluruh baris bisa diklik, dan berubah abu-abu saat di-hover.

Terakhir, footer diatur:

```css
footer {
    clear: both;
    background-color: #1d1d1d;
    padding: 20px;
    color: #eee;
}
```

`clear: both` sangat penting di sini. Karena `#main` dan `#sidebar` di-float, tanpa `clear: both` footer akan naik dan menumpuk di samping kolom. Dengan property ini footer dipaksa turun ke bawah kedua kolom.

**Kode:**

![Kode sidebar dan widget](Dokumentasi/7%20.png)

**Hasil:** sidebar dengan dua widget tampil di sisi kanan, dan footer berlatar hitam berada di paling bawah. Kolom kiri (`#main`) masih kosong karena belum diisi.

![Hasil sidebar dan widget](Dokumentasi/7.%28hasil%29.png)

### Langkah 8: Menambahkan Elemen pada Main Content (Box)

Kolom kiri diisi dengan satu `div.row` yang berisi tiga `div.box`. Tiap box memuat gambar bulat, heading, paragraf singkat, dan link "View detail".

```css
.box {
    display: block;
    float: left;
    width: 33.333333%;
    box-sizing: border-box;
    padding: 0 10px;
    text-align: center;
}
.image-circle { border-radius: 50%; }
.row {
    margin: 0 -10px;
    box-sizing: border-box;
}
.row:after, .row:before,
.entry:after, .entry:before {
    content: '';
    display: table;
}
.row:after,
.entry:after { clear: both; }
```

- `width: 33.333333%` dengan `float: left` membuat tiga box berjajar sama lebar (1/3 dari lebar `.row`).
- `box-sizing: border-box` membuat padding dihitung di dalam lebar, sehingga tiga box tidak melebihi 100% dan tidak turun baris.
- `border-radius: 50%` mengubah gambar persegi menjadi lingkaran.
- `.row` diberi `margin: 0 -10px` untuk mengimbangi `padding: 0 10px` pada box, supaya tepi kiri-kanan tetap rata dengan kolom.
- Blok `.row:after` adalah teknik **clearfix**. Karena semua isi `.row` di-float, tinggi `.row` akan "runtuh" menjadi nol. Pseudo-element `:after` dengan `clear: both` memaksa `.row` tetap membungkus anak-anaknya, sehingga elemen sesudahnya (artikel) tidak ikut naik.

**Kode:**

![Kode box](Dokumentasi/8%20.png)

**Hasil:** tiga kolom (oranye, biru, tosca) tampil sejajar di kolom kiri, dengan sidebar di kanannya.

![Hasil box](Dokumentasi/8.%28hasil%29.png)

### Langkah 9: Menambahkan Content Artikel

Di bawah `.row` (masih di dalam `#main`) ditambahkan dua `<article class="entry">`, masing-masing berisi judul `<h2>`, gambar 150x150, dan paragraf. Antar artikel dipisahkan garis `<hr class="divider">`.

```css
.divider {
    border: 0;
    border-top: 1px solid #eeeeee;
    margin: 40px 0;
}
.entry { margin: 15px 0; }
.entry h2 { margin-bottom: 20px; }
.entry p { line-height: 25px; }
.entry img {
    float: left;
    border-radius: 5px;
    margin-right: 15px;
}
.entry .right-img { float: right; }
```

- `.divider` mengubah garis `<hr>` bawaan menjadi garis tipis abu-abu dengan jarak 40px di atas dan bawah.
- `.entry img` membuat gambar di-float ke kiri, sehingga teks mengalir di sebelah kanannya. `margin-right: 15px` memberi jarak antara gambar dan teks.
- `.entry .right-img` menimpa float menjadi `right`, sehingga pada artikel kedua gambar berpindah ke kanan dan teks mengalir di sebelah kirinya.
- Clearfix `.entry:after` (dari langkah 8) memastikan tinggi artikel ikut menyesuaikan tinggi gambar yang di-float.

**Kode:**

![Kode artikel](Dokumentasi/9%20.png)

**Hasil akhir:** halaman lengkap dengan header, menu, hero panel, tiga box, dua artikel (gambar kiri dan gambar kanan), sidebar widget, dan footer.

![Hasil akhir layout](Dokumentasi/9.%28hasil%29.png)

---

## Validasi HTML

Dokumen divalidasi menggunakan [W3C Nu Html Checker](https://validator.w3.org/nu/) untuk memastikan tidak ada kesalahan penulisan, misalnya tag yang tidak tertutup atau atribut yang salah. Hasilnya: **Document checking completed. No errors or warnings to show.**

![Hasil validasi](Dokumentasi/10%20%28validasi%29.png)

---

## Cara Menjalankan

1. Clone repository ini:
   ```bash
   git clone https://github.com/<username>/Lab4Web.git
   ```
2. Buka folder `Lab4Web` di VS Code.
3. Buka `lab4_box.html` atau `lab4_layout/home.html` dengan Live Server, atau langsung buka file-nya di browser.

> Catatan: gambar pada layout memakai `dummyimage.com`, jadi perlu koneksi internet agar gambar tampil.

## Kesimpulan

Dari praktikum ini dapat disimpulkan bahwa:

- Setiap elemen HTML adalah sebuah box (content, padding, border, margin) yang menjadi dasar penyusunan layout.
- Properti `float` memungkinkan elemen disusun berdampingan, misalnya kolom main content dan sidebar. Namun float mengeluarkan elemen dari alur normal, sehingga diperlukan `clear` atau teknik clearfix agar elemen sesudahnya (seperti footer) tidak rusak posisinya.
- Elemen semantik HTML5 (`header`, `nav`, `section`, `aside`, `footer`) membuat struktur halaman lebih jelas dibanding memakai `div` saja.
- Lebar elemen perlu dihitung dengan teliti (termasuk padding), dan `box-sizing: border-box` membantu agar total lebar tidak melebihi container.
- Kesalahan kecil seperti `</div>` yang kurang dapat merusak seluruh layout, sehingga indentasi yang rapi dan validasi HTML sangat membantu.
