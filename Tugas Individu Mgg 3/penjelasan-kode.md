# Penjelasan Kode Tugas Individu 3

Dokumen ini berisi penjelasan kode untuk tiga file utama, yaitu `pendaftaran.html`, `detail.html`, dan `style.css`.

## 1. File `pendaftaran.html`

File `pendaftaran.html` digunakan sebagai halaman utama untuk mengisi form pendaftaran mahasiswa.

### Struktur Dasar HTML

```html
<!DOCTYPE html>
<html lang="id">
```

Bagian ini menunjukkan bahwa dokumen menggunakan HTML5. Atribut `lang="id"` menandakan bahwa bahasa utama halaman adalah Bahasa Indonesia.

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

`charset="UTF-8"` digunakan agar karakter teks dapat ditampilkan dengan benar. Tag `viewport` membuat tampilan halaman menyesuaikan ukuran layar, termasuk pada perangkat mobile.

```html
<link rel="stylesheet" href="style.css">
```

Kode ini menghubungkan file HTML dengan file CSS bernama `style.css`, sehingga tampilan halaman dapat diatur menggunakan CSS.

### Bagian Konten Utama

```html
<main class="page-container">
```

Elemen `main` digunakan sebagai wadah utama halaman. Class `page-container` dipakai untuk mengatur layout utama menggunakan CSS.

```html
<section class="card form-card" id="form-pendaftaran">
```

Elemen `section` digunakan sebagai kotak utama form. Class `card` memberi tampilan seperti kartu, sedangkan ID `form-pendaftaran` digunakan untuk styling khusus pada halaman pendaftaran.

### Judul Halaman

```html
<h1>TUGAS INDIVIDU 3</h1>
<p class="subtitle">Form Pendaftaran Mahasiswa</p>
```

`h1` digunakan sebagai judul utama halaman. Paragraf dengan class `subtitle` digunakan sebagai keterangan halaman.

### Form Pendaftaran

```html
<form method="GET" action="detail.html">
```

Form menggunakan method `GET`, sehingga data yang diisi akan dikirim melalui query string pada URL. Atribut `action="detail.html"` berarti setelah tombol submit ditekan, pengguna akan diarahkan ke halaman `detail.html`.

Contoh URL setelah submit:

```text
detail.html?nama=Radit&nim=123&kelas=RA&prodi=Informatika
```

### Input Nama dan NIM

```html
<input type="text" id="nama" name="nama" placeholder="Masukkan nama lengkap" required>
```

Input ini digunakan untuk mengisi nama. Atribut `name="nama"` penting karena nama inilah yang akan muncul pada query string.

```html
<input type="text" id="nim" name="nim" placeholder="Masukkan NIM" required>
```

Input ini digunakan untuk mengisi NIM mahasiswa. Atribut `required` membuat input wajib diisi sebelum form dapat dikirim.

### Dropdown Kelas dan Program Studi

```html
<select id="kelas" name="kelas" required>
```

Elemen `select` digunakan untuk membuat pilihan dropdown kelas. Pilihan yang tersedia adalah RA, RB, RC, dan RD.

```html
<select id="prodi" name="prodi" required>
```

Dropdown ini digunakan untuk memilih Program Studi. Contoh pilihannya adalah Informatika, Sistem Informasi, Teknik Komputer, dan Manajemen Informatika.

### Tombol Submit

```html
<button type="submit">Submit</button>
```

Tombol ini digunakan untuk mengirim data form ke halaman `detail.html`.

## 2. File `detail.html`

File `detail.html` digunakan untuk menampilkan detail data pendaftar dalam bentuk tabel.

### Struktur Dasar

Struktur awal file ini sama seperti `pendaftaran.html`, yaitu menggunakan HTML5, pengaturan bahasa Indonesia, meta viewport, dan menghubungkan file `style.css`.

```html
<title>Detail Pendaftar</title>
<link rel="stylesheet" href="style.css">
```

Judul halaman pada tab browser adalah "Detail Pendaftar", dan file CSS yang digunakan tetap sama.

### Bagian Utama Halaman

```html
<section class="card table-card" id="detail-pendaftar">
```

Bagian ini menjadi wadah utama tabel detail pendaftar. Class `card` memberi tampilan kotak, sedangkan ID `detail-pendaftar` dipakai untuk memberi ukuran khusus pada halaman detail.

### Tabel Data Pendaftar

```html
<table>
```

Elemen `table` digunakan untuk menampilkan data pendaftar secara terstruktur.

```html
<thead>
```

`thead` berisi bagian kepala tabel, yaitu nama kolom.

```html
<th>Nama</th>
<th>NIM</th>
<th>Kelas</th>
<th>Program Studi</th>
```

Bagian ini menampilkan judul kolom tabel.

```html
<tbody id="data-pendaftar">
```

`tbody` digunakan untuk menyimpan isi data tabel. ID `data-pendaftar` digunakan oleh JavaScript agar data dari form dapat ditambahkan ke tabel.

### Data Dummy

Di dalam `tbody`, terdapat beberapa data dummy seperti:

```html
<td>Nur Aulia Larasati</td>
<td>119140008</td>
<td>RB</td>
<td>Informatika</td>
```

Data dummy ini tetap disediakan agar tabel tetap memiliki isi walaupun halaman `detail.html` dibuka langsung tanpa submit dari form.

### Link Kembali

```html
<a class="back-link" href="pendaftaran.html">Kembali ke Form</a>
```

Link ini digunakan untuk kembali ke halaman form pendaftaran.

### Script Penangkap Query String

```html
const params = new URLSearchParams(window.location.search);
```

Kode ini digunakan untuk membaca query string dari URL.

```html
const nama = params.get("nama");
const nim = params.get("nim");
const kelas = params.get("kelas");
const prodi = params.get("prodi");
```

Kode tersebut mengambil nilai dari query string berdasarkan nama parameter yang dikirim dari form.

```html
const tabelData = document.getElementById("data-pendaftar");
```

Kode ini mengambil elemen `tbody` berdasarkan ID `data-pendaftar`.

```html
if (nama && nim && kelas && prodi) {
```

Kondisi ini memeriksa apakah semua data dari form tersedia. Jika tersedia, data akan ditambahkan ke tabel.

```html
const baris = document.createElement("tr");
const data = [nama, nim, kelas, prodi];
```

Kode ini membuat baris tabel baru dan menyimpan data pendaftar ke dalam array.

```html
data.forEach(function (isiData) {
    const kolom = document.createElement("td");
    kolom.textContent = isiData;
    baris.appendChild(kolom);
});
```

Perulangan ini membuat kolom tabel baru untuk setiap data, yaitu nama, NIM, kelas, dan program studi. Penggunaan `textContent` membuat data ditampilkan sebagai teks biasa.

```html
tabelData.prepend(baris);
```

Kode ini menambahkan data hasil submit ke bagian paling atas tabel, sehingga data baru muncul sebelum data dummy.

## 3. File `style.css`

File `style.css` digunakan untuk mengatur tampilan kedua halaman HTML.

## Selector CSS yang Digunakan

Pada file CSS terdapat beberapa jenis selector:

### Tag Selector

Contoh:

```css
body {
    margin: 0;
}
```

Tag selector digunakan untuk memilih elemen HTML langsung berdasarkan nama tag, seperti `body`, `h1`, `form`, `table`, `button`, `label`, `input`, dan `select`.

### Class Selector

Contoh:

```css
.page-container {
    display: flex;
}
```

Class selector menggunakan tanda titik di depan nama class. Contoh class yang digunakan adalah `.page-container`, `.card`, `.subtitle`, `.form-group`, dan `.back-link`.

### ID Selector

Contoh:

```css
#form-pendaftaran {
    max-width: 520px;
}
```

ID selector menggunakan tanda pagar. Contoh ID yang digunakan adalah `#form-pendaftaran` dan `#detail-pendaftar`.

## Pengaturan Layout

```css
.page-container {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
```

Kode ini menggunakan Flexbox untuk meletakkan konten utama di tengah layar secara horizontal dan vertikal.

```css
form {
    display: grid;
    gap: 18px;
}
```

Kode ini menggunakan CSS Grid untuk mengatur jarak antar elemen form.

## Box Model

```css
.card {
    padding: 34px;
    margin: 20px;
    border: 1px solid #e3e8f0;
    box-shadow: 0 18px 40px rgba(42, 63, 95, 0.12);
}
```

Bagian ini memenuhi konsep box model. `padding` memberi jarak di dalam elemen, `margin` memberi jarak di luar elemen, `border` memberi garis tepi, dan `box-shadow` memberi efek bayangan.

## Styling Form

```css
input,
select {
    width: 100%;
    padding: 12px 14px;
    border: 1px solid #cbd5e1;
    border-radius: 6px;
}
```

Kode ini mengatur tampilan input dan dropdown agar memiliki ukuran penuh, jarak dalam yang nyaman, border, dan sudut yang sedikit membulat.

```css
input:focus,
select:focus {
    border-color: #3f67b2;
    box-shadow: 0 0 0 3px rgba(63, 103, 178, 0.16);
}
```

Bagian ini membuat input dan dropdown terlihat aktif ketika sedang dipilih.

## Styling Tombol

```css
button {
    color: #ffffff;
    background: #3f67b2;
    cursor: pointer;
}
```

Tombol diberi warna biru, teks putih, dan cursor pointer agar terlihat dapat diklik.

```css
button:hover {
    background: #31579e;
}
```

Saat tombol diarahkan oleh kursor, warnanya berubah menjadi biru yang lebih gelap.

## Styling Tabel

```css
table {
    width: 100%;
    border-collapse: collapse;
}
```

`border-collapse: collapse` digunakan agar garis antar sel tabel menyatu dan terlihat rapi.

```css
th,
td {
    padding: 14px 16px;
    border: 1px solid #d7deea;
    text-align: left;
}
```

Kode ini memberi jarak dalam pada sel tabel, memberi border, dan membuat teks rata kiri.

```css
tbody tr:nth-child(even) {
    background: #eef3fb;
}

tbody tr:nth-child(odd) {
    background: #ffffff;
}
```

Kode ini memberi warna latar selang-seling pada baris tabel agar data lebih mudah dibaca.

## Responsive Design

```css
@media (max-width: 600px) {
    .card {
        padding: 24px 18px;
        margin: 0;
    }
}
```

Media query ini digunakan agar tampilan tetap rapi pada layar kecil seperti handphone.

## Alur Kerja Program

1. Pengguna membuka `pendaftaran.html`.
2. Pengguna mengisi Nama, NIM, Kelas, dan Program Studi.
3. Pengguna menekan tombol Submit.
4. Data dikirim ke `detail.html` menggunakan method `GET`.
5. Data muncul pada URL sebagai query string.
6. JavaScript di `detail.html` membaca query string tersebut.
7. Data hasil submit ditambahkan ke baris paling atas tabel.
8. Data dummy tetap tersedia di bawah data hasil submit.

## Kesimpulan

Program ini terdiri dari dua halaman utama, yaitu halaman form pendaftaran dan halaman detail pendaftar. Form menggunakan method `GET` untuk mengirim data melalui query string. Halaman detail menampilkan data dalam bentuk tabel dan tetap menyediakan data dummy. Tampilan halaman dibuat menggunakan CSS dengan tag selector, class selector, ID selector, Flexbox, Grid, box model, styling form, dan styling tabel.
