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
1. Kolom pencarian
```php
<form method="get">
    <input type="text" name="keyword" placeholder="Cari artikel">
    <button type="submit">Cari</button>
</form>
```
Kode ini untuk membuat kolom pencarian agar artikel yang telah dibuat dapat dicari dengan cepat.
##### ![Gambar 1](gambar34.png).

2. Pagination
```php
<?= $pager->links(); ?>
```
Kode ini untuk membuat setiap page agar artikel dapat tersusun rapih.
##### ![Gambar 1](gambar33.png).

3. Tombol kembali pada edit artikel
##### ![Gambar 1](gambar35.png).

4. Tombol kembali pada tambah artikel
##### ![Gambar 1](gambar36.png).


## Langkah-Langkah Praktikum 3

#### Membuat layout utama
Membuat folder layout dan file pada folder tersebut dengan nama main.php lalu isi kode seperti berikut.
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
                <?= $this->renderSection('content') ?>
            </section>
            <aside di="sidebar">
                <?= view_cell('App\\Cells\\ArtikelTerkini::render') ?>
                <div class="widget-box">
                    <h3 class="title">Widget Header</h3>
                    <ul>
                        <li><a href="#">Widget Link</a></li>
                        <li><a href="#">Widget Link</a></li>
                    </ul>
                </div>
                <div class="widget-box">
                    <h3 class="title"></h3>
                    <p>
                        Vestibulum lorem elit, iaculis in nisl volutpat,
                            malesuada tincidunt arcu. Proin in leo fringilla,
vestibulum mi porta,
                        faucibus felis. Integer pharetra est nunc, nec pretium
nunc pretium ac.</p>
                </div>
            </aside>
        </section>
        <footer>
            <p>&copy; 2021 - Universitas Pelita Bangsa</p>
        </footer>
    </div>
</body>
</html>
```

Hasil:
##### ![Gambar 1](gambar37.png).

#### Membuat file view
Mengubah file home.php:
```php
<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->endSection() ?>
```

#### Membuat class view cell
Membuta folder Cells di dalam app/. lalu buat artikelTerkini.php di dalam folder yang telah dibuat. masukan kode seperti berikut:
```php
<?php

namespace App\Cells;

use CodeIgniter\View\Cell;
use App\Models\ArtikelModel;

class ArtikelTerkini extends Cell
{
    public function render()
    {
        $model = new ArtikelModel();
        $artikel = $model->orderBy('tanggal', 'DESC')->limit(5)->findALL();

        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

#### Membuat view untuk view cell
Membuat folder component didalam app/Views lalu buat file artikel_terkini.php dengan kode sebagai berikut:
```php
<h3>Artikel Terkini</h3>
<ul>
    <?php foreach ($artikel as $row): ?>
        <li><a href="<?= base_url('/artikel/' . $row['slug']) ?>"><?=
$row['judul'] ?></a></li>
    <?php endforeach; ?>
</ul>
```

# Pertanyaan dan tugas
• Sesuaikan data dengan praktikum sebelumnya, perlu melakukan perubahan field pada
database dengan menambahkan tanggal agar dapat mengambil data artikel terbaru.
```php
$artikel = $model
        ->orderBy('tanggal', 'DESC')
        ->limit(5)
        ->findAll();
```
Kode ini berfungsi untuk mengurutkan data berdasarkan tanggal terbaru dan membatasi jumlah data yang ditampilkan. Dan menambahkan kolom tanggal pada tabel database.
##### ![Gambar 1](gambar37.png).
Pada gambar diatas data artikel berurutan sesuai dengan tanggal dimana artikel tersebut sesuai dengan tanggal terbaru.
• Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan
improvisasi. Hasil langkah-langkah ada di bagian atas.
• Apa manfaat utama dari penggunaan View Layout dalam pengembangan aplikasi?
```
1. Meningkatkan pengalaman UI/UX.
2. Struktur yang rapih.
3. Tampilan menjadi lebih efisien.
4. Membantu aplikasi lebih responsif.
```
• Jelaskan perbedaan antara View Cell dan View biasa.
Perbedaan antara view cell dan View biasa adalah kalau View biasa itu ketika dipanggil harus melalui controller dan tidak fleksibel ketika dipakai dibanyak halaman. sedangkan View Cell ini tanpa memerlukan Controller yang banyak, fleksibel, dan bisa dipakai berulang.
<br>
• Ubah View Cell agar hanya menampilkan post dengan kategori tertentu.
```php
<?php

namespace App\Cells;

use App\Models\ArtikelModel;

class ArtikelTerkini 
{
    public function index()
    {
        $model = new ArtikelModel();

        $data = $model
            ->where('kategori IS NOT NULL')
            ->where('kategori !=', '')
            ->orderBy('tanggal', 'DESC')
            ->findAll();
        $grouped = [];

        foreach ($data as $row) {
            $kategori = $row['kategori'] ?? 'Lainnya';
            $grouped[$kategori][] = $row;
        }

        return view('components/artikel_terkini', [
            'grouped' => $grouped
        ]);
    }
}
```
Dari kode diatas berfungsi untuk memfilter artikel berdasarkan kategori tertentu. Data yang diambil akan ditampilkan pada View Cell.

Mengubah tampilan view/artikel_terkini.php agar tampil perkategori.
```php
<div class="widget-box">
    <h3 class="title">Artikel Terkini</h3>

    <?php foreach ($grouped as $kategori => $items): ?>
        
        <h4><?= $kategori ?></h4>
        <ul>
            <?php foreach ($items as $row): ?>
                <li>
                    <a href="<?= base_url('/artikel/' . $row['slug']) ?>">
                        <?= $row['judul'] ?>
                    </a>
                </li>
            <?php endforeach; ?>
        </ul>

    <?php endforeach; ?>
</div>
```

Hasil:
##### ![Gambar 1](gambar38.png).


## Langkah-Langkah Praktikum 4

#### Membuat tabel user login
Menyiapkan MySQL terlebih dahulu dan menjalankan servernya. lalu buat tabel user.
```
CREATE TABLE user (
 id INT(11) auto_increment,
 username VARCHAR(200) NOT NULL,
 useremail VARCHAR(200),
 userpassword VARCHAR(200),
 PRIMARY KEY(id)
);
```

#### Membuat model user
Membuat file baru di direktori app/Models dengan nama UserModel.php.
```php
<?php
namespace App\Models;
use CodeIgniter\Model;
class UserModel extends Model
{
     protected $table = 'user';
     protected $primaryKey = 'id';
     protected $useAutoIncrement = true;
     protected $allowedFields = ['username', 'useremail', 'userpassword'];
}
```

#### Membuat Controller User
Membuat cotroller baru dengan nama User.php di direktori app/Controllers. lalu menambahkan method index() untuk menampilkan daftar user,  dan method login() untuk proses login.
```php
<?php
namespace App\Controllers;

use App\Models\UserModel;

class User extends BaseController
{
    public function index()
    {
        $title = 'Daftar user';
        $model = new UserModel();
        $users = $model->findAll();
        return view('user/index', compact('users', 'title'));
    }

    public function login()
    {
        helper(['form']);
        $email = $this->request->getPost('email');
        $password = $this->request->getPost('password');
        if (!$email)
        {
            return view('user/login');
        }

        $session = session();
        $model = new UserModel();
        $login = $model->where('useremail', $email)->first();
        if ($login)
        {
            $pass = $login['userpassword'];
            if (password_verify($password, $pass))
            {
                $login_data = [
                    'user_id' => $login['id'],
                    'user_name' => $login ['username'],
                    'user_email' => $login ['useremail'],
                    'logged_in' => TRUE,
                ];

                $session->set($login_data);
                return redirect('admin/artikel');
            }
            else
            {
                $session->setFlashdata("flash_msg", "Password salah.");
                return redirect()->to('/user/login');
            }
        }
        else
        {
            $session->setFlashdata("flash_msg", "email tidak terdaftar.");
            return redirect()->to('/user/login');
        }
    }

    public function logout()
    {
        session()->destroy();
        return redirect()->to('/user/login');
    }
}
```

#### Membuat Vew login
Membuat direktori baru dengan nama user pada direktori app/Views dan buat file dengan nama login.php
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Login</title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="login-wrapper">
            <h1>Sign In</h1>
            <?php if(session()->getFlashdata('flash_msg')):?>
                <div class="alert alert-danger"><?= session()->getFlashdata('flash_msg') ?></div>
            <?php endif;?>
            <form action="" method="post">
                <div class="mb-3">
                    <label for="InputForEmail" class="form-label">Email
address</label>
                    <input type="email" name="email" class="form-control"
id="InputForEmail" value="<?= set_value('email') ?>">
                </div>
                <br>
                <div class="mb-3">
                    <label for="InputForPassword" class="form-
label">Password</label>
                    <input type="password" name="password" class="from-
control" id="InputForPassword">
                </div>
                <br>
                <button type="submit" class="btn btn-
primary">Login</button>
    </div>
</body>
</html>
```

#### Membuat database seeder
Membuat database seeder yang digunakan untuk membuat data dummy dan untuk keperluan ujicoba modul login. masukkan data user dan password kedalam database. jalankan database seeder di CLI pada xampp.
```php spark make:seeder UserSeeder```

Lalu buka file UserSeeder.php di direktori /app/Database/Seeds/UserSeeder.php dan isi dengan kode sebagai berikut.
```php
<?php

namespace App\Database\Seeds;

use CodeIgniter\Database\Seeder;

class UserSeeder extends Seeder
{
    public function run()
    {
        $model = model('UserModel');
        $model->insert([
            'username' => 'admin',
            'useremail' => 'admin@email.com',
            'userpassword' => password_hash('admin123', PASSWORD_DEFAULT),
        ]);
    }
}
```

Ketik kembali di CLI dengan perintah sebagai berikut:
```php spark db:seed UserSeeder```

#### Uji Coba Login

Buka url  http://localhost:8080/user/login. hasil akan sebagai berikut:
##### ![Gambar 1](gambar39.png).

#### Menambahkan Auth Filter
Membuat filter untuk halaman admin. Buat file baru dengan nama Auth.php di direktori app/Filters. isi dengan kode sebagai berikut.
```php
<?php namespace App\Filters;

use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;
use CodeIgniter\Filters\FilterInterface;

class Auth implements FilterInterface
{
    public function before(RequestInterface $request, $arguments = null)
    {
        // jika user belum login
        if(! session()->get('logged_in')){
            // maka redirct ke halaman login
            return redirect()->to('/user/login');
        }
    }

    public function after(RequestInterface $request, ResponseInterface
$response, $arguments = null)
    {
        // Do something here
    }
}
```

Buka file app/Config/Filters.php dana menambahkan kode sebagai berikut.
```'auth' => App\Filters\Auth::class```

```php
public array $aliases = [
        'csrf'          => CSRF::class,
        'toolbar'       => DebugToolbar::class,
        'honeypot'      => Honeypot::class,
        'auth'          => \App\Filters\Auth::class,
        'invalidchars'  => InvalidChars::class,
        'secureheaders' => SecureHeaders::class,
        'cors'          => Cors::class,
        'forcehttps'    => ForceHTTPS::class,
        'pagecache'     => PageCache::class,
        'performance'   => PerformanceMetrics::class,
    ];
```

Kemudian buka file app/Config/Routes.php dan sesuaikan kodenya
```php
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
$routes->group('admin', ['filter' => 'auth'], function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

#### Percobaan akses menu admin
Membuka url alamat http://localhost:8080/admin/artikel. halaman tersebut ketika diakses akan tampak hasil sebagai berikut:
##### ![Gambar 1](gambar40.png).

#### Fungsi logout
Menambahkan method lagout pada Controller User seperti dibawah:
```php
public function logout()
    {
        session()->destroy();
        return redirect()->to('/user/login');
    }
```

Saya menambahkan tombol logout pada halaman dashboard admin dan user.
##### ![Gambar 1](gambar41.png).
##### ![Gambar 1](gambar42.png).

Lalu saya membuat kolom kategori pada tambah artikel.
Input:
```php
<p>
    <input type="text" name="kategori" placeholder="Kategori">
</p>
```

Output:
##### ![Gambar 1](gambar43.png).

## Langkah-Langkah Praktikum 5

#### Membuat pagination
Pagination adalah proses yang digunakan untuk membatasi tampilan yang pajang dari data yang terlalu banyak pada website. Memiliki fungsi untuk memexah tampilan menjadi beberapa halaman tergantung banyaknya data yang ingin ditampilkan pada setiap halaman.

Membuat pagination pada Controller Artikel lalu di modifikasi kode pada method admin_index seperti di modul praktikum 5.
```php
public function admin_index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->paginate(10);
        $pager   = $model->pager;   
        $data = [
            'artikel' => $artikel,
            'pager'   => $pager,
            'title'   => $title,
        ]);
        return view('artikel/admin_index') 
    }
```

Kemudian pada file views/artikel/admin_index.php tambahkan kode dibawah kode deklarasi tabel data.
```php
<?= $pager->links(); ?>
```

Buka kembali menu daftar artikel di web, hasil akan seperti bawah:
##### ![Gambar 1](gambar44.png).

#### Membuat pencarian 
Pencarian data digunakan untuk memfilter data yang dicari.
Buka lagi Controller Artikel, pada method admin_index ubah kode seperti berikut.
```php
public function admin_index()
    {
        $title = 'Daftar Artikel';
        $q = $this->request->getVar('q') ?? '';
        $model = new ArtikelModel();

        if ($q) {
            $model->like('judul', $q);
        }

        $artikel = $model->paginate(2);
        $pager   = $model->pager;   
        $data = [
            'artikel' => $artikel,
            'pager'   => $pager,
            'title'   => $title,
            'q' => $q,
        ]);
        return view('artikel/admin_index') 
    }
```

Lalu buka file views/artikel/admin_index.php dan tambahkan form pencarian sebelum deklarasi tabel seperti berikut:
```php
<form method="get" class="form-search">
   <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data">
   <input type="submit" value="Cari" class="btn btn-primary">
</form>
```

Dan pada link pager ubah seperti berikut:
```php <?= $pager->only(['q'])->links(); ?>```

Kemudian ujicoba kembali halaman web admin artikel. lalu masukkan kata kunci tertentu pada form pencarian.

##### ![Gambar 1](gambar45.png).


## Langkah-Langkah Praktikum 6

#### Relasi Tabel dan Query Buiider
#### 1. Menyiapkan Mysql dan buka database lab_ci4

#### 2. Membuat tabel kategori
Menjalankan query berikut:
```
CREATE TABLE kategori (
         id_kategori INT(11) AUTO_INCREMENT,
         nama_kategori VARCHAR(100) NOT NULL,
         slug_kategori VARCHAR(100),
         PRIMARY KEY (id_kategori)
 );
```
Hasil:
##### ![Gambar 1](gambar46.png).

#### 3. Mengubah tabel artikel
Menambahkan foerign Key id_kategori` pada tabel `artikel` untuk membuat relasi dengan tabel
`kategori`:
```
ALTER TABLE artikel
ADD COLUMN id_kategori INT(11),
ADD CONSTRAINT fk_kategori_artikel
FOREIGN KEY (id_kategori) REFERENCES kategori(id_kategori);
```

#### 4. Membuat model kategori
Membuat file model baru di app/Modles dengan nama KategoriModel.php:
```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class KategoriModel extends Model
{
    protected $table = 'kategori';
    protected $primaryKey = 'id_kategori';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['nama_kategori', 'slug_kategori'];
}
```
#### 5. Membuat model artikel
Modifikasi file tersebut untuk mendefinisikan relasi dengan KategoriModel:
```php
<?php

namespace App\Models;

use CodeIgniter\Model;

Class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul','isi', 'status', 'slug', 'gambar', 'id_kategori'];

    public function getArtikelDenganKategori()
    {
        return $this->db->table('artikel')
                    ->select('artikel.*, kategori.nama_kategori')
                    ->join('kategori', 'kategori.id_kategori = artikel.id_kategori')
                    ->get()
                    ->getResultArray();
    }

}
```

#### 6. Memodifikasi controller artikel
Untuk menggunakan model baru dan menampilkan data relasi:
```php
<?php

namespace App\Controllers;

use App\Models\ArtikelModel;
use App\Models\KategoriModel;


class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->getArtikelDenganKategori(); // Use the new method
        $model->select('artikel.*, kategori.nama_kategori')
              ->join('kategori', 'kategori.id_kategori = artikel.id_kategori', 'left');

        $artikel = $model->orderBy('tanggal', 'DESC')->findAll();
        $q = $this->request->getVar('q');
        return view('artikel/index', compact('artikel', 'title'));
    }

    public function admin_index()
    {
        $title = 'Daftar Artikel (Admin)';
        $q = $this->request->getVar('q') ?? '';
        $model = new ArtikelModel();
        $kategori_id = $this->request->getVar('kategori_id') ?? '';

        if ($q) {
            $model->like('judul', $q);
        }

        $data = [
            'title'   => $title,
            'q' => $q,
            'kategori_id' => $kategori_id,
        ];

        $builder = $model->table('artikel')
                         ->select('artikel.*, kategori.nama_kategori')
                                  ->join('kategori', 'kategori.id_kategori = artikel.id_kategori');

        // Apply search filter if keyword is provided
        if ($q != '') {
            $builder->like('artikel.judul', $q);
        }

        // Apply category filter if category_id is provided
        if ($kategori_id != '') {
            $builder->where('artikel.id_kategori', $kategori_id);
        }

        // Apply pagination
        $data['artikel'] = $builder->paginate(10);
        $data['pager'] = $model->pager;

        // Fetch all categories for the filter dropdown
        $kategoriModel = new KategoriModel();
        $data['kategori'] = $kategoriModel->findAll();
        return view('artikel/admin_index', $data);
    }

    public function add()
    {
        // Validation...
        if ($this->request->getMethod() == 'post' && $this->validate([
            'judul' => 'required',
               'id_kategori' => 'required|integer' // Ensure id_kategori is required and an integer
        ])) {
            $model = new ArtikelModel();
            $model->insert([
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
                'slug' => url_title($this->request->getPost('judul')),
                'id_kategori' => $this->request->getPost('id_kategori')
            ]);
            return redirect()->to('/admin/artikel');
        } else {
            $kategoriModel = new KategoriModel();
            $data['kategori'] = $kategoriModel->findAll(); 
            $data['title'] = "Tambah Artikel";
            return view('artikel/form_add', $data);
        }
    }

    public function edit($id)
    {
        $model = new ArtikelModel();
        if ($this->request->getMethod() == 'post' && $this->validate([
            'judul' => 'required',
            'id_kategori' => 'required|integer'
        ])) {
            $model->update($id, [
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
                'id_kategori' => $this->request->getPost('id_kategori')
            ]);
        return redirect()->to('/admin/artikel');
    } else {
        $data['artikel'] = $model->find($id);
        $kategoriModel = new KategoriModel();
        $data['kategori'] = $kategoriModel->asObject()->findAll(); // Fetch categories for the form
        $data['title'] = "Edit Artikel";
        return view('artikel/form_edit', $data);
    }
}

    public function delete($id)
    {
        $model = new ArtikelModel();
        $model->delete($id);
        return redirect()->to('/admin/artikel');
    }

    public function view($slug)
    {
        $model = new ArtikelModel();
        $data['artikel'] = $model->where('slug', $slug)->first();
        if (empty($data['artikel'])) {
            throw new \CodeIgniter\Exceptions\PageNotFoundException('Cannot find the article.');
    }

        $data['title'] = $data['artikel']['judul'];
        return view('artikel/detail', $data);
    }
    

}
```

#### 7. Memodifikasi view
Menyesuaikan floder view/artikel untuk masing-masing view di index.php:
```php
<?= $this->include('template/header'); ?>

<?php if ($artikel): foreach ($artikel as $row): ?>
    <article class="entry">
            <h2><a href="<?= base_url('/artikel/' . $row['slug']); ?>"><?=
$row['judul']; ?></a></h2>
        <p>Kategori: <?= $row['nama_kategori'] ?></p>
         <img src="<?= base_url('/gambar/' . $row['gambar']); ?>" alt="<?=
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
admin_index.php:
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<br>
<div class="row mb-3">
    <div class="col-md-6">
        <form method="get" class="form-inline">
            <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari judul artikel" class="form-control mr-2">
            <select name="kategori_id" class="form-control mr-2">
                <option value="">Semua Kategori</option>
               <?php foreach ($kategori as $k): ?>
    <option value="<?= $k['id_kategori']; ?>" <?= ($kategori_id == $k['id_kategori']) ? 'selected' : ''; ?>>
        <?= $k['nama_kategori']; ?>
    </option>
<?php endforeach; ?>
            </select>
            <input type="submit" value="Cari" class="btn btn-primary">
        </form>
    </div>
</div>

<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Kategori</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </thead>
    <tbody>
        <?php if (count($artikel) > 0): ?>
            <?php foreach ($artikel as $row): $row = (object)$row; ?>
                <tr>
                    <td><?= $row->id; ?></td>
                    <td>
                         <b><?= $row->judul; ?></b>
                        <p><small><?= substr($row->isi, 0, 50); ?></small></p>
                    </td>
                    <td><?= $row->nama_kategori; ?></td>
                    <td><?= $row->status; ?></td>
                    <td>
                                <a class="btn btn-sm btn-info" href="<?=
base_url('/admin/artikel/edit/' . $row->id); ?>">Ubah</a>
                            <a class="btn btn-sm btn-danger" onclick="return
confirm('Yakin menghapus data?');" href="<?=
base_url('/admin/artikel/delete/' . $row->id); ?>">Hapus</a>
                    </td>
                </tr>
                    <?php endforeach; ?>
                <?php else: ?>
                    <tr>
                        <td colspan="5">Tidak ada data.</td>
                    </tr>
                <?php endif; ?>
    </tbody>
</table>

<?= $pager->only(['q', 'kategori_id'])->links(); ?>

<?= $this->include('template/admin_footer'); ?>
```

form_add.php:
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <label for="judul">Judul</label>   
    <input type="text" name="judul" id="judul" required>
    </p>
    <p>
        <label for="isi">Isi</label>
        <textarea name="isi" id="isi" cols="50" rows="10"></textarea>
    </p>
    <p>
        <label for="id_kategori">Kategori</label>
        <select name="id_kategori" id="id_kategori" required>
            <?php foreach($kategori as $k): ?>
                <option value="<?= $k['id_kategori']; ?>"><?= $k['nama_kategori']; ?></option>
            <?php endforeach; ?>
        </select>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p><br>
    <a href="<?= base_url('admin/artikel'); ?>" class="btn btn-large">Kembali</a></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

form_edit.php:
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <label for="judul">Judul</label>
         <input type="text" name="judul" value="<?= $artikel['judul']; ?>"
id="judul" required>
    </p>
    <p>
        <label for="isi">Isi</label>
        <textarea name="isi" id="isi" cols="50" rows="10"><?= $artikel['isi'];
    ?></textarea>
    </p>
    <p>
        <label for="id_kategori">Kategori</label>
        <select name="id_kategori" id="id_kategori" required>
            <?php foreach($kategori as $k): ?>
                         <option value="<?= $k->id_kategori; ?>" <?=
($artikel['id_kategori'] == $k->id_kategori) ? 'selected' : ''; ?>><?=
$k->nama_kategori; ?></option>
            <?php endforeach; ?>
        </select>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p><br>
    <a href="<?= base_url('admin/artikel'); ?>" class="btn btn-large">Kembali</a></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

#### 8. Testing
-Menampilkan daftar artikel dengan nama kategori.
hasil:
#### ![Gambar 1](gambar47.png).
-Menambah artikel baru dengan memilih kategorinya.
hasil:
#### ![Gambar 1](gambar48.png).
#### ![Gambar 1](gambar49.png).
-Mengedit artikel dan mengubah kategorinya.
hasilnya:
#### ![Gambar 1](gambar50.png).
#### ![Gambar 1](gambar51.png).
-Menghapus artikel.
hasil:
Sebelum:
#### ![Gambar 1](gambar49.png).
Sesudah:
#### ![Gambar 1](gambar52.png).

Pertanyaan dan Tugas
1. Selesaikan semua langkah praktikum di atas.
2. Modifikasi tampilan detail artikel (artikel/detail.php) untuk menampilkan nama kategori
artikel.
```php
<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>

    <p><b>Kategori:</b> <?= $artikel['nama_kategori']; ?></p>

    <img src="<?= base_url('/gambar/' . $artikel['gambar']); ?>" 
         alt="<?= $artikel['judul']; ?>">

    <p><?= $artikel['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```
#### ![Gambar 1](gambar53.png).
4. Tambahkan fitur untuk menampilkan daftar kategori di halaman depan (opsional).
```php
<?= $this->include('template/header'); ?>

<?php if ($artikel): foreach ($artikel as $row): ?>
    <article class="entry">
            <h2><a href="<?= base_url('/artikel/' . $row['slug']); ?>"><?=
$row['judul']; ?></a></h2>
        <p>Kategori: <?= $row['nama_kategori'] ?></p>
         <img src="<?= base_url('/gambar/' . $row['gambar']); ?>" alt="<?=
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
#### ![Gambar 1](gambar54.png).
5. Buat fungsi untuk menampilkan artikel berdasarkan kategori tertentu (opsional).

## Langkah-Langkah Praktikum 7
#### Upload gambar pada artikel
Menambahkan fungsi unggah pada cotroller di method add:
```php
public function add()
    {
        // Validation...
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();
        if ($this->request->getMethod() == 'post' && $this->validate([
            'judul' => 'required',
               'id_kategori' => 'required|integer' // Ensure id_kategori is required and an integer
        ])) {
            $file = $this->request->getFile('gambar');
            $file->move(ROOTPATH . 'public/gambar');
            $model = new ArtikelModel();
            $model->insert([
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
                'slug' => url_title($this->request->getPost('judul')),
                'id_kategori' => $this->request->getPost('id_kategori'),
                'gambar' => $file->getName(),
            ]);
            return redirect()->to('/admin/artikel');
        } else {
            $kategoriModel = new KategoriModel();
            $data['kategori'] = $kategoriModel->findAll(); 
            $data['title'] = "Tambah Artikel";
            return view('artikel/form_add', $data);
        }
    }
```
Method yang sudah digunakan guna menambahkan gambar artikel berita.

Menambahkan kode tombol input gambar pada  views/artikel/form_add.php:
```php
<p>
 <input type="file" name="gambar">
</p>
```
Lalu menyesuaikan tag form dengan menambhakna ecrypt type:
```php
<form action="" method="post" enctype="multipart/form-data">
```
Kode tersebut ditambahkan agar fungsi input gambar dapat bekerja dengan baik.
Kemudian uji coba upload gambar pada tambah artikel.
#### ![Gambar 1](gambar55.png).
#### ![Gambar 1](gambar56.png).
```php
<?php if (!empty($row->gambar)): ?>
                            <img src="<?= base_url('/gambar/' . $row->gambar); ?>" width="80" style="display:block; margin-bottom:5px;">
                        <?php endif; ?>
```
kode ini berguna untuk menampilkan pada halaman daftar artikel admin.
#### ![Gambar 1](gambar57.png).
#### ![Gambar 1](gambar58.png).


## Langkah-Langkah Praktikum 8: AJAX
AJAX atau Asynchronous JavaScript and XML merupakan gabungan dari teknologi pengembangan aplikasi web yang membuat aplikasi web menjadi lebih responsif terhadap interaksi pengguna. 
Keutungan menggunakan AJAX:
```
- Meningkatkan User Experience (UX).
- Menghemat Bandwidth.
- Mempertahankan State Aplikasi.
```
```
Contoh:
- Live chat applications
- Autocomplete suggestions
- Real-time updates
- Validasi formulir secara real-time
```

Langakah-langkah Praktikum sebagai berikut:

#### Menambahkan Pustaka jQuery
mendownload pustaka tersebut terlebih dahulu dan diekstrak filenya. setelah di ekstrak taruh pada folder public/assets/js.
#### ![Gambar 1](gambar59.png).

#### Memebuat model
Membuat AJAX Controller agar model dapat diakses melalui AJAX.
```php
<?php

namespace App\Controllers;

use CodeIgniter\Controller;
use CodeIgniter\HTTP\Request;
use CodeIgniter\HTTP\Response;
use App\Models\ArtikelModel;

class  AjaxController extends Controller
{
    public function index()
    {
        return view('ajax/index');
    }

    public function getData()
    {
        $q = $this->request->getVar('q') ?? '';
        $kategori_id = $this->request->getVar('kategori_id') ?? '';
    
        $model = new ArtikelModel();
        
        $builder = $model->db->table('artikel')
            ->select('artikel.*, kategori.nama_kategori')
            ->join('kategori', 'kategori.id_kategori = artikel.id_kategori', 'left');
    
        if ($q != '') {
            $builder->like('artikel.judul', $q);
        }
    
        if ($kategori_id != '') {
            $builder->where('artikel.id_kategori', $kategori_id);
        }
    
        $data = $builder->get()->getResultArray();
    
        return $this->response->setJSON($data);
    }

    public function delete($id)
    {
        $model = new ArtikelModel();
        $data = $model->delete($id);

        $data = [
            'status' => 'OK'
        ];

        return $this->response->setJSON($data);
    }

    public function store()
    {
        $model = new ArtikelModel();

        $file = $this->request->getFile('gambar');
        $namaGambar = '';
        if ($file && $file->isValid() && !$file->hasMoved()) {
            $file->move(ROOTPATH . 'public/gambar');
            $namaGambar = $file->getName();
        }

        $model->insert([
            'judul'       => $this->request->getPost('judul'),
            'isi'         => $this->request->getPost('isi'),
            'slug'        => url_title($this->request->getPost('judul')),
            'id_kategori' => $this->request->getPost('id_kategori'),
            'gambar'      => $namaGambar,
        ]);

        return $this->response->setJSON(['status' => 'OK']);
    }

    public function getById($id)
    {
        $model = new ArtikelModel();
        $data = $model->find($id);
        return $this->response->setJSON($data);
    }

    public function update($id)
    {
        $model = new ArtikelModel();

        $file = $this->request->getFile('gambar');
        $namaGambar = $this->request->getPost('gambar_lama');
        if ($file && $file->isValid() && !$file->hasMoved()) {
            $file->move(ROOTPATH . 'public/gambar');
            $namaGambar = $file->getName();
        }

        $model->update($id, [
            'judul'       => $this->request->getPost('judul'),
            'isi'         => $this->request->getPost('isi'),
            'slug'        => url_title($this->request->getPost('judul')),
            'id_kategori' => $this->request->getPost('id_kategori'),
            'gambar'      => $namaGambar,
        ]);

        return $this->response->setJSON(['status' => 'OK']);
    }
}
```
Fungsi:
- mengirim data JSON menggunakan AJAX,
- Penghubung database,
- Pengelola CRUD artikel,
- Menampilkan data artikel.

Membuat view
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<br>

<div class="row mb-3">
    <div class="col-md-6">
        <form id="filterForm" class="form-inline">
            <input type="text" name="q" id="q" placeholder="Cari judul artikel" class="form-control mr-2">
            
            <select name="kategori_id" id="kategori_id" class="form-control mr-2">
                <option value="">Semua Kategori</option>
                <?php foreach ($kategori as $k): ?>
                    <option value="<?= $k['id_kategori']; ?>">
                        <?= $k['nama_kategori']; ?>
                    </option>
                <?php endforeach; ?>
            </select>

            <button type="submit" class="btn btn-primary">Cari</button>
        </form>
    </div>
</div>

<table class="table" id="artikelTable">
    <thead>
        <tr>
            <th>ID</th>
            <th>Gambar</th>
            <th>Judul</th>
            <th>Kategori</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="6">Loading data...</td>
        </tr>
    </tbody>
</table>

<script src="<?= base_url('assets/js/jquery-4.0.0.min.js') ?>"></script>

<script>
$(document).ready(function() {

    function loadData(q = '', kategori_id = '') {
        $('#artikelTable tbody').html('<tr><td colspan="6">Loading data...</td></tr>');

        $.ajax({
            url: "<?= base_url('ajax/getData') ?>",
            method: "GET",
            data: {
                q: q,
                kategori_id: kategori_id
            },
            dataType: "json",
            success: function(data) {
                var html = '';

                if (data.length > 0) {
                    for (var i = 0; i < data.length; i++) {
                        var row = data[i];

                        html += '<tr>';
                        html += '<td>' + row.id + '</td>';

                        html += '<td>';
                        if (row.gambar) {
                            html += '<img src="<?= base_url('/gambar/') ?>' + row.gambar + '" width="80">';
                        }
                        html += '</td>';

                        html += '<td><b>' + row.judul + '</b><br><small>' + row.isi.substring(0,50) + '</small></td>';
                        html += '<td>' + row.nama_kategori + '</td>';
                        html += '<td>' + row.status + '</td>';

                        html += '<td>';
                        html += '<a href="<?= base_url('/admin/artikel/edit/') ?>' + row.id + '" class="btn btn-sm btn-info">Ubah</a> ';
                        html += '<a href="#" class="btn btn-sm btn-danger btn-delete" data-id="' + row.id + '">Hapus</a>';
                        html += '</td>';

                        html += '</tr>';
                    }
                } else {
                    html = '<tr><td colspan="6">Tidak ada data</td></tr>';
                }

                $('#artikelTable tbody').html(html);
            }
        });
    }

    // Load awal
    loadData();

    // Filter
    $('#filterForm').submit(function(e) {
        e.preventDefault();
        var q = $('#q').val();
        var kategori_id = $('#kategori_id').val();
        loadData(q, kategori_id);
    });

    // Delete
    $(document).on('click', '.btn-delete', function(e) {
        e.preventDefault();
        var id = $(this).data('id');

        if (confirm('Yakin hapus data?')) {
            $.ajax({
                url: "<?= base_url('admin/artikel/delete/') ?>" + id,
                method: "GET",
                success: function() {
                    loadData();
                }
            });
        }
    });

});
</script>

<?= $this->include('template/admin_footer'); ?>
```
Fungsi:
- Menampilkan data artikel secara AJAX,
- Melakukan pencarian artikel,
- Filter berdasarkan kategori,
- Menghapus artikel tanpa reload halaman.

#### ![Gambar 1](gambar60.png).

#### Pertanyaan dan Tugas
Selesaikan programnya sesuai Langkah-langkah yang ada. Tambahkan fungsi untuk
tambah dan ubah data. Anda boleh melakukan improvisasi.
Memnambahkan pada file form add dan form edit.
form add:
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form id="formTambah" action="" method="post" enctype="multipart/form-data">
    <?= csrf_field(); ?>
    <p>
        <label for="judul">Judul</label>   
    <input type="text" name="judul" id="judul" required>
    </p>
    <p>
        <label for="isi">Isi</label>
        <textarea name="isi" id="isi" cols="50" rows="10"></textarea>
    </p>
    <p>
        <label for="id_kategori">Kategori</label>
        <select name="id_kategori" id="id_kategori" required>
            <?php foreach($kategori as $k): ?>
                <option value="<?= $k['id_kategori']; ?>"><?= $k['nama_kategori']; ?></option>
            <?php endforeach; ?>
        </select>
        <p>
            <input type="file" name="gambar">
        </p>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p><br>
    <a href="<?= base_url('admin/artikel'); ?>" class="btn btn-large">Kembali</a></p>
</form>

<script src="<?= base_url('assets/js/jquery-4.0.0.min.js') ?>"></script>
<script>
$('#formTambah').submit(function(e) {
    e.preventDefault();
    var formData = new FormData(this);
    $.ajax({
        url: "<?= base_url('ajax/store') ?>",
        method: "POST",
        data: formData,
        processData: false,
        contentType: false,
        success: function(res) {
            if (res.status == 'OK') {
                alert('Artikel berhasil ditambahkan!');
                window.location.href = "<?= base_url('admin/artikel') ?>";
            }
        },
        error: function() {
            alert('Gagal menyimpan data!');
        }
    });
});
</script>

<?= $this->include('template/admin_footer'); ?>
```
Fungsi:
- Menyimpan data realtime,
- Redirect otomatis setelah berhasil.
- Menyimpan artikel ke database tanpa reload halaman.
Hasil:
#### ![Gambar 1](gambar61.png).

form edit:
```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form id="formUbah" action="" method="post" enctype="multipart/form-data">
    <p>
        <label for="judul">Judul</label>
         <input type="text" name="judul" value="<?= $artikel['judul']; ?>"
id="judul" required>
    </p>
    <p>
        <label for="isi">Isi</label>
        <textarea name="isi" id="isi" cols="50" rows="10"><?= $artikel['isi'];
    ?></textarea>
    </p>
    <p>
        <label for="id_kategori">Kategori</label>
        <select name="id_kategori" id="id_kategori" required>
            <?php foreach($kategori as $k): ?>
                         <option value="<?= $k->id_kategori; ?>" <?=
($artikel['id_kategori'] == $k->id_kategori) ? 'selected' : ''; ?>><?=
$k->nama_kategori; ?></option>
            <?php endforeach; ?>
        </select>
    </p>
    <p>
        <?php if($artikel['gambar']): ?>
            <img src="<?= base_url('/gambar/' . $artikel['gambar']) ?>" width="150"><br><br>
        <?php endif; ?>
        <label for="gambar">Ubah Gambar</label>
        <input type="file" name="gambar" id="gambar">
        <input type="hidden" name="gambar_lama" value="<?= $artikel['gambar']; ?>">
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p><br>
    <a href="<?= base_url('admin/artikel'); ?>" class="btn btn-large">Kembali</a></p>
</form>

<script src="<?= base_url('assets/js/jquery-4.0.0.min.js') ?>"></script>
<script>
$('#formUbah').submit(function(e) {
    e.preventDefault();
    var formData = new FormData(this);
    $.ajax({
        url: "<?= base_url('ajax/update/' . $artikel['id']) ?>",
        method: "POST",
        data: formData,
        processData: false,
        contentType: false,
        success: function(res) {
            if (res.status == 'OK') {
                alert('Artikel berhasil diubah!');
                window.location.href = "<?= base_url('admin/artikel') ?>";
            }
        },
        error: function() {
            alert('Gagal mengubah data!');
        }
    });
});
</script>

<?= $this->include('template/admin_footer'); ?>
```
Fungsi:
- Redirect ke halaman admin artikel setelah berhasil update,
- Submit form ubah artikel menggunakan AJAX
Hasil:
#### ![Gambar 1](gambar62.png).



## Langkah-Langkah Praktikum 9: Implementasi AJAX Pagination dan Search
#### 1. Persiapan
Siapkan MySQL server berjalan, pastikan tabel artikel dan kategori suda terisi, dan pastikan library jQuery sudah terpasang.

#### 2. Modifikasi Controller Artikel
Mengubah method pada admin index di file Artikel.php. Agar data dalam format JSON jika request AJAX.
```php
public function admin_index()
    {
        $title = 'Daftar Artikel (Admin)';
        $model = new ArtikelModel();

        $q = $this->request->getVar('q') ?? '';
        $kategori_id = $this->request->getVar('kategori_id') ?? '';
        $page = $this->request->getVar('page') ?? 1;

        $builder = $model->select('artikel.*, kategori.nama_kategori')
                         ->join('kategori', 'kategori.id_kategori = artikel.id_kategori');

        if ($q != '') {
            $builder->like('artikel.judul', $q);
        }
        if ($kategori_id != '') {
            $builder->where('artikel.id_kategori', $kategori_id);
        }

        $sort = $this->request->getVar('sort') ?? '';
        if ($sort == 'judul_asc') $builder->orderBy('artikel.judul', 'ASC');
        if ($sort == 'judul_desc') $builder->orderBy('artikel.judul', 'DESC');
        if ($sort == 'id_asc') $builder->orderBy('artikel.id', 'ASC');
        if ($sort == 'id_desc') $builder->orderBy('artikel.id', 'DESC');

        $artikel = $builder->paginate(5, 'default', $page);
        $pager = $model->pager;

        $data = [
            'title'       => $title,
            'q'           => $q,
            'kategori_id' => $kategori_id,
            'artikel'     => $artikel,
            'pager'       => $pager,
        ];

        if ($this->request->isAJAX()) {
            $data['pager'] = $pager->getDetails();
            return $this->response->setJSON($data);
        } else {
            $kategoriModel = new KategoriModel();
            $data['kategori'] = $kategoriModel->findAll();
            return view('artikel/admin_index', $data);
        }
    }
```
Penjelasan fungsi:
- nomor halaman untuk pagination, default halaman 1,
- Menerapkan pagination dengan nomor halaman yang diberikan,
- Kata kunci pencarian judul artikel, default kosong,
- Return JSON berisi artikel dan detail pager (getDetails()) untuk pagination.

#### 3. Modifikasi View
```php
<?= $this->include('template/admin_header'); ?>
<h2><?= $title; ?></h2>
<br>

<div id="loading-indicator" style="display:none; text-align:center; padding: 20px;">
    <div class="spinner-border text-primary" role="status">
        <span class="sr-only">Loading data...</span>
    </div>
</div>

<div class="row mb-3">
    <div class="col-md-8">
        <form id="filterForm" class="form-inline">
            <input type="text" name="q" id="q" placeholder="Cari judul artikel" class="form-control mr-2">

            <select name="kategori_id" id="kategori_id" class="form-control mr-2">
                <option value="">Semua Kategori</option>
                <?php foreach ($kategori as $k): ?>
                    <option value="<?= $k['id_kategori']; ?>">
                        <?= $k['nama_kategori']; ?>
                    </option>
                <?php endforeach; ?>
            </select>

            <select name="sort" id="sort" class="form-control mr-2">
                <option value="">Urutkan</option>
                <option value="id_asc">ID Terkecil</option>
                <option value="id_desc">ID Terbesar</option>
                <option value="judul_asc">Judul A-Z</option>
                <option value="judul_desc">Judul Z-A</option>
            </select>

            <button type="submit" class="btn btn-primary">Cari</button>
        </form>
    </div>
</div>

<div id="article-container"></div>
<br>
<div id="pagination-container" class="pagination"></div>


<script src="<?= base_url('assets/js/jquery-4.0.0.min.js') ?>"></script>
<script>
$(document).ready(function () {
    const articleContainer = $('#article-container');
    const paginationContainer = $('#pagination-container');

    const fetchData = (url) => {
        $('#loading-indicator').show();
        $('#article-container').html('');
        $('#pagination-container').html('');

        $.ajax({
            url: url,
            type: 'GET',
            dataType: 'json',
            headers: {
                'X-Requested-With': 'XMLHttpRequest'
            },
            success: function (data) {
                renderArticles(data.artikel);
                renderPagination(data.pager, data.q, data.kategori_id);
            },
            error: function () {
                $('#article-container').html('<div class="alert alert-danger">Gagal memuat data.</div>');
            },
            complete: function () {
                $('#loading-indicator').hide();
            }
        });
    };

    const renderArticles = (articles) => {
        let html = '<table class="table table-bordered table-striped">';
        html += '<thead><tr><th>ID</th><th>Gambar</th><th>Judul</th><th>Kategori</th><th>Status</th><th>Aksi</th></tr></thead><tbody>';

        if (articles && articles.length > 0) {
            articles.forEach(row => {
                html += `<tr>
                    <td>${row.id}</td>
                    <td>
                        ${row.gambar
                            ? `<img src="<?= base_url('/gambar/') ?>${row.gambar}" width="80">`
                            : '-'}
                    </td>
                    <td><b>${row.judul}</b><br><small>${row.isi.substring(0, 50)}</small></td>
                    <td>${row.nama_kategori}</td>
                    <td>${row.status}</td>
                    <td>
                        <a href="<?= base_url('/admin/artikel/edit/') ?>${row.id}" class="btn btn-sm btn-info">Ubah</a>
                        <a href="#" class="btn btn-sm btn-danger btn-delete" data-id="${row.id}">Hapus</a>
                    </td>
                </tr>`;
            });
        } else {
            html += '<tr><td colspan="6" class="text-center">Tidak ada data.</td></tr>';
        }

        html += '</tbody></table>';
        $('#article-container').html(html);
    };

    const renderPagination = (pager, q, kategori_id) => {
        if (!pager || pager.pageCount <= 1) return;
                    
        let sort = $('#sort').val();
        let html = '<nav><ul class="pagination">';
                    
        for (let i = 1; i <= pager.pageCount; i++) {
            let url = `<?= base_url('/admin/artikel') ?>?page=${i}&q=${q ?? ''}&kategori_id=${kategori_id ?? ''}&sort=${sort ?? ''}`;
            html += `<li class="page-item ${i == pager.currentPage ? 'active' : ''}">
                        <a class="page-link pagination-link" href="${url}">${i}</a>
                     </li>`;
        }
                    
        html += '</ul></nav>';
        paginationContainer.html(html);
    };

    $('#filterForm').on('submit', function (e) {
        e.preventDefault();
        const q = $('#q').val();
        const kategori_id = $('#kategori_id').val();
        const sort = $('#sort').val();
        fetchData(`<?= base_url('/admin/artikel') ?>?q=${q}&kategori_id=${kategori_id}&sort=${sort}`);
    });

    $('#kategori_id').on('change', function () {
        $('#filterForm').trigger('submit');
    });

    $('#sort').on('change', function () {
        $('#filterForm').trigger('submit');
    });


    $(document).on('click', '.pagination-link', function (e) {
        e.preventDefault();
        const url = $(this).attr('href');
        if (url && url !== '#') {
            fetchData(url);
        }
    });

    $(document).on('click', '.btn-delete', function (e) {
        e.preventDefault();
        const id = $(this).data('id');
        if (confirm('Yakin hapus data ini?')) {
            $.ajax({
                url: `<?= base_url('admin/artikel/delete/') ?>${id}`,
                method: 'GET',
                success: function () {
                    $('#filterForm').trigger('submit');
                },
                error: function () {
                    alert('Gagal menghapus data.');
                }
            });
        }
    });

    fetchData('<?= base_url('/admin/artikel') ?>');
});
</script>

<?= $this->include('template/admin_footer'); ?>
```
Penjelasan fungsi:
- jQuery mengirim request ke server secara otomatis
- Form tidak reload halaman
- Tidak memakai tabel artikel dan pagination secara langsung.

Hasil/Output:
#### ![Gambar 1](gambar63.png).

#### Pertanyaan dan Tugas
1. Selesaikan semua langkah praktikum di atas.
2. Modifikasi tampilan data artikel dan pagination sesuai kebutuhan desain.
```php
table-bordered table-striped
```
menambahkan class tersebut agar tabel artikel lebih mudah untuk dibaca.

3. Tambahkan indikator loading saat data sedang diambil dari server.
```php
$('#loading-indicator').show();  // saat AJAX mulai
// ...
complete: function () {
    $('#loading-indicator').hide();  // saat AJAX selesai
}
```
ketika request ke server dimulai, indikator ditampilkan. Setelah server mengembalikan response berhasil atau gagal, idikator disembunyikan kembali melalui callback complete di AJAX. indikator ini memberi tahu pengguna bahwa data sedang diproses.
Hasil:
#### ![Gambar 1](gambar64.png).
#### ![Gambar 1](gambar63.png).
4. Implementasikan fitur sorting (mengurutkan artikel berdasarkan judul, dll.) dengan AJAX.
```php
<select name="sort" id="sort" class="form-control mr-2">
                <option value="">Urutkan</option>
                <option value="id_asc">ID Terkecil</option>
                <option value="id_desc">ID Terbesar</option>
                <option value="judul_asc">Judul A-Z</option>
                <option value="judul_desc">Judul Z-A</option>
</select>

$sort = $this->request->getVar('sort') ?? '';
        if ($sort == 'judul_asc') $builder->orderBy('artikel.judul', 'ASC');
        if ($sort == 'judul_desc') $builder->orderBy('artikel.judul', 'DESC');
        if ($sort == 'id_asc') $builder->orderBy('artikel.id', 'ASC');
        if ($sort == 'id_desc') $builder->orderBy('artikel.id', 'DESC');
```
Dapat merubah dropdown sesuai keingingan berdasarkan urutan: pilihan ID Terkecil, ID Terbesar, Judul A-Z, dan Judul Z-A. form otomatis ter-submit dan mengirim parameter sort ke server tanpa reload halaman.
Hasil.
berdasarkan urutan abjad:
#### ![Gambar 1](gambar65.png).
berdasarkan urutan ID:
#### ![Gambar 1](gambar66.png).
