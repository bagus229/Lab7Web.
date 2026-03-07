# Nama: Bagus aditya hermawan
# Nim: 312410382
# Kelas: I241C
# Matkul: Pemrograman Web 2

## Langkah-Langkah Praktikum 1
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

## Langkah-Langkah Praktikum 2

#### Membuat database: studi kasus data artikel.
Membuat database dengan nama lab_ci4.
```
CREATE DATABASE lab_ci4;
```

Kemudian membuat tabel.
```
CREATE TABLE artikel (
 id INT(11) auto_increment,
 judul VARCHAR(200) NOT NULL,
 isi TEXT,
 gambar VARCHAR(200),
 status TINYINT(1) DEFAULT 0,
 slug VARCHAR(200),
 PRIMARY KEY(id)
);
```
#### Konfigurasi koneksi database
Membuat konfigurasi untuk menghubungkan dengan database server dengan menggunakan file .env.
##### ![Gambar 1](gambar26.png).

#### Membuat model
Membuat model proses data artikel. dengan membuat file pada direktori app/Models dengan nama ArtikelModel.php. lalu isi dengan kode seperti berikut:
```php
<?php

namespace App\Models;

use CodeIgniter\Model;

Class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primarykey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul','isi', 'status', 'slug', 
'gambar'];

}
```

#### Membuat controller
Membuat Controller baru dengan nama Artikel.php pada direktori app/Controllers dan isi dengan kode seperti berikut:
```php
<?php

namespace App\Controllers;

use App\Models\ArtikelModel;

class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }
```

#### Membuat view
Membuat view dengan file baru dengan nama index.php. isi dengan kode sebagai berikut:
```php
<?= $this->include('template/header'); ?>

<?php if($artikel): foreach($artikel as $row): ?>
<article class="entry">
    <h2><a href="<?= base_url('/artikel/' . $row['slug']);?>"><?=
$row['judul']; ?></a>
</h2>
    <img src="<?= base_url('/gambar/' . $row['gambar']);?>" alt="<?=
$row['judul']; ?>">
    <p><?= substr($row['isi'], 0, 200); ?></p>
</article>
<hr class="divider" />
<?php endforeach; else: ?>
<article class="entry">
    <h2>Belum ada data.</h2>
</article>
<?php endif; ?>

<?= $this->include('template/footer'); ?>
```
Lalu mencoba pada url yang telah diberikan yakni http://localhost:8080/artikel. hasil seperti gambar dibawah.
##### ![Gambar 1](gambar27.png).
Menambahkan data pada database.
```
INSERT INTO artikel (judul, isi, slug) VALUE
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah menjadi standar contoh teks sejak tahun 1500an, saat seorang tukang cetak yang tidak dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk menjadi sebuah buku contoh huruf.', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum bukanlah teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin klasik dari era 45 sebelum masehi, hingga bisa dipastikan usianya telah mencapai lebih dari 2000 tahun.', 'artikel-kedua');
```
Buka kembali halaman yang tadi lalu di refresh akan muncul data yang telan dimasukkan.
Hasil sebagai berikut:
##### ![Gambar 1](gambar28.png).

#### Membuat tampilan detail artikel
Menambahkan fungsi baru pada Contorller Artikel dengan nama view(). isi dengan kode seperti berikut.
```php
public function view($slug)
    {
        $model = new ArtikelModel();
        $artikel = $model->where([
            'slug' => $slug
        ])->first();

        // Menampilkan error apabila data tidak ada.
        if (!$artikel)
        {
            throw PageNotFoundException::forPageNotFound();
        }
        $title = $artikel['judul'];
        return view('artikel/detail', compact('artikel', 'title'));
    }
```

#### Membuat view detail
Membuat view baru pada app/views/artikel dengan nama detail.php. isi file dengan kode sebagai berikut.
```php
<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>
    <img src="<?= base_url('/gambar/' . $artikel['gambar']);?>" alt="<?=
$artikel['judul']; ?>">
    <p><?= $artikel['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```

#### Membuat routing untuk artikel data
Tambahkan routing pada Routes.php.
```php$routes->get('/artikel/(:any)', 'Artikel::view/$1');```.
##### ![Gambar 1](gambar29.png).

#### Membuat menu admin
Membuat method baru pada Controller Artikel dengan nama admin_index(). isi dengan kode sebagai berikut:
```php
public function admin_index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findALL();
        return view('artikel/admin_index', compact('artikel', 'title'));
    }
```
Membuat view admin dengan nama admin_index.php.
```php
<?= $this->include('template/admin_header'); ?>

<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </thead>
    <tbody>
    <?php if($artikel): foreach($artikel as $row): ?>
    <tr>
        <td><?= $row['id']; ?></td>
        <td>
            <b><?= $row['judul']; ?></b>
            <p><small><?= substr($row['isi'], 0, 50); ?></small></small></p>
        </td>
        <td><?= $row['status']; ?></td>
        <td>
            <a class="btn" href="<?= base_url('/admin/artikel/edit/' .
$row['id']);?>">Ubah</a>
            <a class="btn btn-danger" onclick="return confirm('Yakin
menghapus data?');" href="<?= base_url('/admin/artikel/delete/' .
$row['id']);?>">Hapus</a>
        </td>
    </tr>
    <?php endforeach; else: ?>
    <tr>
        <td colspan="4">Belum ada data</td>
    </tr>
    <?php endif; ?>
    </tbody>
    <tfoot>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </tfoot>
</table>

<?= $this->include('template/admin_footer'); ?>
```

Menambahkan routing menu admin:
```
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```
Akses menu admin dengan url http://localhost:8080/admin/artikel.

##### ![Gambar 1](gambar30.png).

#### Menambah data artikel
Menambahkan fungis dengan nama add() pada Controller Artikel.
```php
public function add()
    {
        // validasi data.
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();

        if ($isDataValid)
        {
            $artikel = new ArtikelModel();
            $artikel->insert([
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
                'slug' => url_title($this->request->getPost('judul')),
            ]);
            return redirect('admin/artikel');
        }
        $title = "Tambah Artikel";
        return view('artikel/form_add', compact('title'));
    }
```

Lalu membuat view form tambah dengan nama form_add.php.
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
    <input type="text" name="judul">
    </p>
    <p>
    <textarea name="isi" cols="50" rows="10"></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

Kemudian akses http://localhost:8080/admin/artikel/add.
##### ![Gambar 1](gambar31.png).

#### Mengubah data
Menambahkan fungsi pada Artikel.php dengan nama edit().
```php
public function edit($id)
    {
        $artikel = new ArtikelModel();
        // validasi data.
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();
        
        if ($isDataValid)
        {
            $artikel->update($id, [
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
            ]);
            return redirect('admin/artikel');
        }
        
        // ambil data lama
        $data = $artikel->where('id', $id)->first();
        $title = "Edit Artikel";
        return view('artikel/form_edit', compact('title', 'data'));
    }
```

Kemudian membuat view untuk form edit dengan nama form_edit.php
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <input type="text" name="judul" value="<?= $data['judul'];?>" >
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"><?=
$data['isi'];?></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```
Hasil akan seperti berikut:
##### ![Gambar 1](gambar32.png).

#### Menghapus data 
Menambahkan funsgi delete pada Artikel.php dengan nama delete().
```php
public function delete($id)
    {
        $artikel = new ArtikelModel();
        $artikel->delete($id);
        return redirect('admin/artikel');
    }
```

## Pertanyaan dan Tugas
Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan improvisasi.
