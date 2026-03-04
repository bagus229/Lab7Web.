# Nama: Bagus aditya hermawan
# Nim: 312410382
# Kelas: I241C
# Matkul: Pemrograman Web 2

## Langkah-Langkah Praktikum
Mengaktifkan ekstensi yang diperlukan melalui XAMPP Control Panel. pilih bagian Apache lalu klik Config/PHP.ini.
##### ![Gambar 1](gambar1.png).

Menghilangkan titik koma (;) pada ekstensi yang diaktifkan. lalu simpan kembali dan restart Apache web server.
##### ![Gambar 1](gambar2.png).

Menginstall Codeigniter 4 dengan cara manual dan menggunakan Composer. setelah menginstall ubah ke extrak file zip Codeigniter ke direktori htdocs/lab11_ci. kemudian Ubah nama direktory framework-4.x.xx menjadi ci4. setelah langkah tadi dilakukan buka browser lalu ketik/salin http://localhost/lab11_ci/ci4/public/.
##### ![Gambar 1](gambar3.png).

Menjalankan CLI dengan memanggil php spark untuk mempermudah proses development. Caranya membuka terminal command prompt. lalu lokasi direktori diarahkan sesuai dengan direktori project yang dibuat.
##### ![Gambar 1](gambar4.png).

Mengaktifkan mode debugging untuk memudahkan developer dalam mengetahui pesan error apabila terjadi kesalahan dalam kode program.
##### ![Gambar 1](gambar5.png).

Dengan cara mengubah nilai konfigurasi pada environment variable CI_ENVIRINMENT menjadi development.
##### ![Gambar 1](gambar6.png).

Lalu ubah nama file env menjadi .env.
##### ![Gambar 1](gambar7.png).

Mencoba error dengan mengubah kode pada file app/Controller/Home.php dan hilangkan titik koma pada akhir kode.
##### ![Gambar 1](gambar8.png).

Berikut adalah struktur direktorinya.
##### ![Gambar 1](gambar9.png).

Router terletak pada file app/config/Routes.php.
##### ![Gambar 1](gambar20.png).

Mendefinisikan route untuk aplikasi. seperti:
```php
$routes->get('/', 'Home::index');
```
Membuat route baru di dalam Routes.php:
```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

Kemudian mengecek route apakah sudah benar dengan menjalankan perintah "php spark routes".
##### ![Gambar 1](gambar10.png).

Lalu akses alamat url yang telah dibuat tadi.
##### ![Gambar 1](gambar11.png).
Akan muncul tampilan error 404. untuk menanganinya dengan membuat Controller page dengan nama page.php pada direktori Controller. 
Lalu file tersebut diisi dengan kode yang telah diberikan.
##### ![Gambar 1](gambar19.png).

Setelah itu kembali ke halaman yang sudah diakses tadi. maka akan muncul hasil sebagai berikut.
##### ![Gambar 1](gambar12.png).

Mengubah status autoroute dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai true menjadi false.
```php$routes->setAutoRoute(true);" - "$routes->setAutoRoute(false);```
lalu tambahkan method baru pada Controller Page seperti berikut.
```php
public function tos()
{
    echo "ini halaman Term of Services";
}
```

Kemudian akses halaman http://localhost/lab11_ci/ci4/tos.
##### ![Gambar 1](gambar13.png).

Membuat View
Membuat file baru dengan nama about.php pada direktori view. kemudian isi kode yang telah diberikan.
```php
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title><?= $title; ?></title>
</head>
<body>
   <h1><?= $title; ?></h1>
   <hr>
   <p><?= $content; ?></p>
</body>
</html>".
```

lalu mengubah method about menjadi seperti berikut:
```php
public function about()
    {
        return view('about', [
            'title'   => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }
```

kemudian refresh halaman yang tadi diakses.
##### ![Gambar 1](gambar14.png).

Membuat layout CS pada direktori public dengan nama style.css.
##### ![Gambar 1](gambar15.png).

Kemudian membuat folder template pada direktori view dan buat file header.php dan footer.php.
header.php:
##### ![Gambar 1](gambar16.png).
footer.php
##### ![Gambar 1](gambar17.png).

lalu ubah file about dengan kode seperti berikut:
##### ![Gambar 1](gambar21.png).

lalu refresh kembali. maka hasil akan muncul seperti berikut.
##### ![Gambar 1](gambar18.png).

## Pertanyaan dan Tugas
Lengkapi kode program untuk menu lainnya yang ada pada Controller Page, sehingga semua
link pada navigasi header dapat menampilkan tampilan dengan layout yang sama.
## Jawab
Membuat file artikel.php seperti yang ada pada navigasi di direktori views. lalu di isi dengan kode yang sama seperti di file about.php.
```php
<?= $this->include('template/header'); ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->include('template/footer');
```
Kemudian menambahkan kode seperti dibawah pada file page.php:
```php
public function artikel()
    {
        return view('artikel', [
            'title'   => 'Halaman Artikel',
            'content' => 'Ini halaman artikel.'
        ]);
    }
```

Kemudian tambahkan routes untuk artikel di dihalaman Routes.php.
```php
<?php

use CodeIgniter\Router\RouteCollection;

/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');
$routes->get('/artikel', 'Page::artikel');
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
```
Setelah menambahkan route untuk bagian artikel dan navigasi lainnya agar navigasinya ketika diklik akan terarah ke halaman artikel. maka jalankan perintah php spark serve di shell xampp.
##### ![Gambar 1](gambar25.png).
Hasil akan muncul seperti gambar dibawah ini.
##### ![Gambar 1](gambar22.png).
##### ![Gambar 1](gambar23.png).
##### ![Gambar 1](gambar24.png).
