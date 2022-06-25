| Nama      | Risky HariAdi |
| ----------- | ----------- |
| NIM     | 312010124    |
| Kelas   | TI.20.A.1        |

# <span style="color: blue">Praktikum 13 | Framework Lanjutan (Modul Login)</span>

## 1. Membuat Table User
- Jalankan ``Apache, MySql`` pada Xampp, Akses browser http://localhost/phpmyadmin.
- Buat tabel dengan nama ``artikel``.
    ```sql
        CREATE TABLE user (
        id INT(11) auto_increment,
        username VARCHAR(200) NOT NULL,
        useremail VARCHAR(200),
        userpassword VARCHAR(200),
        PRIMARY KEY(id)
        );
    ```
![Foto](Foto/5.1.png)
<br>

## 2. Membuat Model User
- Terletak di folder `app/Models`, buat file `UserModel.php`.
![Foto](Foto/18.2.png)
<br>

## 3. Membuat Controller User
- Terletak di folder `app/Controllers`, buat file `User.php`.
![Foto](Foto/18.3.png)
<br>

## 4. Membuat View Login
- Terletak di folder `app/Views`, buat folder baru dengan nama `user`, buat file `login.php` di dalamnya.
![Foto](Foto/18.4.1.png)
<br>

## 5. Membuat Database Seeder
- Untuk keperluan uji coba.
- Masuk ke direktori ci4, kemudian ketikkan kode:
``php spark make:seeder UserSeeder``
![Foto](Foto/18.4.png)
<br>

- Terletak di folder `app/Database/Seeds`, buka file `UserSeeder.php`, kemudian edit menjadi berikut:
![Foto](Foto/18.4.png)
<br>

- Buka kembali CLI, kemudian ketik perintah berikut:
``php spark db:seed UserSeeder``
![Foto](Foto/18.4.2.png)
<br>

- Berikut data yang sudah ditambah pada tabel `user`. Dengan mengakses ``http://localhost/phpmyadmin``.

<br>![Foto](Foto/18.7.png)

- Buka file `.env`, kemudian hapus `#` pada `app.sessionX`
![Foto](Foto/18.8.png)
<br>

- Akses kembali url ``http://localhost:8080/user/login``
![Foto](Foto/18.9.png)
<br>

## 6. Menambah Auth Filter
- Terletak di folder `app/Filters`, buat file `Auth.php`
![Foto](Foto/18.7.1.png)
<br>

- Kemudian pada folder `app/Config`, edit isi file `Filters.php` menjadi berikut:
```php
<?php

namespace Config;

use CodeIgniter\Config\BaseConfig;
use CodeIgniter\Filters\CSRF;
use CodeIgniter\Filters\DebugToolbar;
use CodeIgniter\Filters\Honeypot;
use App\Filters\Auth;
use App\Filters\Noauth;
//use CodeIgniter\Filters\InvalidChars;
//use CodeIgniter\Filters\SecureHeaders;

class Filters extends BaseConfig
{
    /**
     * Configures aliases for Filter classes to
     * make reading things nicer and simpler.
     *
     * @var array
     */
    public $aliases = [
        'csrf'          => CSRF::class,
        'toolbar'       => DebugToolbar::class,
        'honeypot'      => Honeypot::class,
        'auth'          => Auth::class,
        'noauth'          => Noauth::class,
        //'invalidchars'  => InvalidChars::class,
        //'secureheaders' => SecureHeaders::class,
    ];

    /**
     * List of filter aliases that are always
     * applied before and after every request.
     *
     * @var array
     */
    public $globals = [
        'before' => [
            // 'honeypot',
            // 'csrf',
            // 'invalidchars',
        ],
        'after' => [
            'toolbar',
            // 'honeypot',
            // 'secureheaders',
        ],
    ];

    /**
     * List of filter aliases that works on a
     * particular HTTP method (GET, POST, etc.).
     *
     * Example:
     * 'post' => ['csrf', 'throttle']
     *
     * @var array
     */
    public $methods = [];

    /**
     * List of filter aliases that should run on any
     * before or after URI patterns.
     *
     * Example:
     * 'isLoggedIn' => ['before' => ['account/*', 'profiles/*']]
     *
     * @var array
     */

    public $filters = [
        'auth' => ['before' =>
            [
                'admin/*',
            ]
        ]
    ];
}
```

- Untuk mencobanya, akses ``http://localhost:8080/artikel``, kemudian tambah menjadi ``http://localhost:8080/admin/artikel`` lalu tekan enter.
![Foto](Foto/19.00.png)
<br>

- Otomatis akan dialihkan untuk login terlebih dahulu.
![Foto](Foto/19.001.png)
<br>

- Mencoba masuk dengan email `admin@email.com`, dan password `admin123`, kemudian tekan `login`.
![Foto](Foto/19.01.png)
<br>

- Berhasil masuk sebagai admin, dan semua menu dapat diakses.Untuk mencobanya klik menu `Artikel`.
![Foto](Foto/19.1.2.png)
<br>

- Kemudian klik menu `Login Admin`, untuk diarahkan ke ``http://localhost:8080/admin/artikel``.
![Foto](Foto/19.02.png)
<br>

- Maka akan masuk ke menu admin sebelumnya, tidak login ulang.
![Foto](Foto/19.1.2.png)
<br>

## 7. Membuat Fungsi Logout
- Menambah method logout().
- Terletak di folder `app/Controllers`, buka file `User.php`, kemudian edit menjadi berikut:
![Foto](Foto/19.02.03.png)
<br>

- Untuk mencobanya, klik menu `Logout`.
![Foto](Foto/19.1.2.png)
<br>

- Maka akan langsung diarahkan untuk login ulang, sebelum bisa mengakses menu admin.
![Foto](Foto/18.9.png)
<br>

- Namun, untuk ``http://localhost:8080/artikel`` masih dapat diakses.
![Foto](Foto/19.03.png)
<br>

</div>