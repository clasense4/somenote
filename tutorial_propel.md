#Tutorial Propel

Propel adalah ORM (Object Relational Mapper). ORM sendiri jika dilihat dari definisi nya, yaitu routing dari object PHP ke Database (MySQL, MSSQL, SQLITE, POSTGRE). Jadi dengan menggunakan object PHP, oleh ORM di translasi kan ke bahasa SQL.

##Membuat Object

Untuk membuat model di propel itu sangat mudah, namun pastikan seluruh script telah di generate dengan menggunakan perintah `propel-gen`. Jika sudah berhasil, di folder utama project, akan muncul folder `build\` yang isinya `classes`, `conf`, dan `sql`.

Studi kasus yang digunakan disini adalah menggunakan project `spin13`, dan menggunakan tabel `Pengguna`.

    <?php

    require_once ('startup.php');
    error_reporting(E_ALL);

    // Pilih 1 data dari pengguna
    $pengguna1 = PenggunaPeer::doSelectOne(new Criteria());
    print_r($pengguna1);
    echo "<hr>";

    // Ini Cara yang digunakan dalam tutorial propel
    // output sama, namun cara penggunaan sedikit berbeda
    $pengguna2 = PenggunaQuery::create();
    print_r($pengguna2);

Object telah dibuat, dan untuk menggunakan, Kita dapat memanipulasi menggunakan object `$pengguna`. Jika menggunakan ide `Zend Studio`, cukup ketikkan `$pengguna->` dan tekan tombol `CTRL + SPACE`, maka fungsi auto complete akan muncul. Itulah salah satu yang menjadi kekuatan Propel ORM ini.

##Seleksi dan filter data

* Seleksi data (Semua)

        <?php

        require_once ('startup.php');
        error_reporting(E_ALL);

        // Pilih semua data dari Tabel pengguna
        $pengguna = PenggunaPeer::doSelect(new Criteria());

        // Output adalah semua array dari tabel pengguna
        print_r($pengguna);

* Seleksi data dengan filter

        <?php

        require_once ('startup.php');
        error_reporting(E_ALL);
        
        // Buat criteria
        $c = new Criteria();

        // Pilih Username dengan value `admin313`
        $c->add(PenggunaPeer::USERNAME, "admin313");

        // Pilih semua data dari Tabel pengguna
        $pengguna = PenggunaPeer::doSelect($c);

        // Output adalah object dari tabel pengguna
        // dengan value `admin313`
        print_r($pengguna);

##Insert data

    <?php

    require_once ('startup.php');
    error_reporting(E_ALL);

    // Buat object pengguna
    $pengguna = new Pengguna();

    // Nama = fajri313
    $pengguna->setNama("fajri313");

    // Email = clasense4@gmail.com
    $pengguna->setEmail("clasense4@gmail.com");

    // SatkerId = 11
    $pengguna->setSatkerId(11);

    // Save
    $pengguna->save();

    // Output adalah array hasil insert
    print_r($pengguna);

##Hapus Data

    <?php

    require_once ('startup.php');
    error_reporting(E_ALL);

    // Hapus user dengan ID 10
    $pengguna = PenggunaPeer::retrieveByPK(10);
    $pengguna->delete();
    