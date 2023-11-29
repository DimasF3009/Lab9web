# Lab9web

# langkah-langkah praktikum

### Buat file dengan header.php

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="container">
        <header>
            <h1>Modularisasi Menggunakan Require</h1>
        </header>
        <?php 
            $about = "about.php";
            $home="home.php";
            $kontak = "kontak.php"
        ?>
        <nav>
            <a href="<?php echo $home ?>">Home</a>
            <a href="<?php echo $about ?>">Tentang</a>
            <a href="<?php echo $kontak ?>">Kontak</a>
        </nav>
```

### Buat file dengan footer.php

```
<footer>
    <div class="footer">
        <p>&copy; 2021, Informatika, Universitas Pelita Bangsa</p>
    </div>
</footer>
```

### Buat file dengan about.php 

```
<?php require('header.php'); ?>
    <div class="content">
        <h2>Ini Halaman About</h2>
        <p>Ini adalah bagian content dari halaman.</p>
    </div>
<?php require('footer.php'); ?>
```

![about](https://github.com/DimasF3009/Lab9web/assets/115356128/126a1a18-04bc-47ad-b438-f8a0578e43e3)


### Buat file dengan kontak.php 

```
<?php require('header.php'); ?>
    <div class="content">
        <h2>Ini Halaman kontak</h2>
        <p>Ini adalah bagian content dari halaman.</p>
    </div>
<?php require('footer.php'); ?>
```

![kontak](https://github.com/DimasF3009/Lab9web/assets/115356128/b73d825f-56be-4e34-9312-2780151ea01b)


### Buat file dengan home.php

```
<?php require('header.php')?>
<div class="content">
        <h2>Ini Halaman home</h2>
        <p>Ini adalah bagian content dari halaman.</p>
    </div>
<?php require('footer.php');?>
```

![home](https://github.com/DimasF3009/Lab9web/assets/115356128/a776f647-2c3a-4922-a31b-a25c8867ac03)


## Tugas 
Implementasikan konsep modularisasi pada kode program praktikum 8

### Buat file link.php
```
<?php 
    $menu = "index.php";
?>
<p><a href="<?php echo $menu; ?>">Kembali Ke Menu</a></p>
```

### Buat file footer.php
```
<footer>
    <div class="footer">
        <p>&copy; 2021, Informatika, Dimas Firmansyah</p>
    </div>
</footer>
```

## Implementasikan Kode
implementasikan kode footer dan link kedalam main kode atau menu

### Implementasi pada tampilan menu

```
<?php
include("koneksi.php");
// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Data Barang</title>

</head>
<body>
    <div class="container">
        <h1>Data Barang</h1>
        <a href="plus.php"> Tambah Barang</a>
        <div class="main">
            <table>
            <tr>
                <th>Gambar</th>
                <th>Nama Barang</th>
                <th>Katagori</th>
                <th>Harga Jual</th>
                <th>Harga Beli</th>
                <th>Stok</th>
                <th>Aksi</th>
            </tr>
            <?php if($result): ?>
            <?php while($row = mysqli_fetch_array($result)): ?>
            <tr>
                <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=$row['nama'];?>"></td>
                <td><?= $row['nama'];?></td>
                <td><?= $row['kategori'];?></td>
                <td><?= $row['harga_beli'];?></td>
                <td><?= $row['harga_jual'];?></td>
                <td><?= $row['stok'];?></td>
                <td><a href="ubah.php?id=<?= $row['id_barang']; ?>">ubah</a>
                <a href="hapus.php?id=<?= $row['id_barang']; ?>">hapus</a></td>
            </td>
            </tr>
            <?php endwhile; else: ?>
            <tr>
                <td colspan="1">Belum ada data</td>
            </tr>
            <?php endif; ?>
            </table>
        </div>
    </div>
    <?php
        require("footer.php");
    ?>
</body>
</html>
```

### Implementasi pada fitur tambah barang

```
<?php
error_reporting(E_ALL);

include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $nama = htmlspecialchars($_POST['nama']);
    $kategori = htmlspecialchars($_POST['kategori']);
    $harga_jual = floatval($_POST['harga_jual']);
    $harga_beli = floatval($_POST['harga_beli']);
    $stok = intval($_POST['stok']);
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0) {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = 'gambar/' . $filename;

        if (move_uploaded_file($file_gambar['tmp_name'], $destination)) {
            $gambar = 'gambar/' . $filename;
        } else {
            echo "Gagal mengunggah file gambar.";
            exit;
        }
    }

    $sql = 'INSERT INTO data_barang (nama, kategori, harga_jual, harga_beli, stok, gambar) ';
    $sql .= 'VALUES (?, ?, ?, ?, ?, ?)';

    $stmt = mysqli_prepare($conn, $sql);

    if ($stmt) {
        mysqli_stmt_bind_param($stmt, 'ssddis', $nama, $kategori, $harga_jual, $harga_beli, $stok, $gambar);

        $result = mysqli_stmt_execute($stmt);

        if ($result) {
            echo "Data berhasil ditambahkan.";
        } else {
            echo "Gagal mengeksekusi pernyataan SQL: " . mysqli_stmt_error($stmt);
        }

        mysqli_stmt_close($stmt);
    } else {
        echo "Gagal membuat prepared statement: " . mysqli_error($conn);
    }

    mysqli_close($conn);
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css">
    <title>Tambah Barang</title>
</head>
<body>
    <div class="container">
        <h1>Tambah Barang</h1>
        <div class="main">
            <form method="post" action="plus.php" enctype="multipart/form-data">
                <div class="input">
                    <label for="nama">Nama Barang</label>
                    <input type="text" name="nama" id="nama" required>
                </div>
                <div class="input">
                    <label for="kategori">Kategori</label>
                    <select name="kategori" id="kategori" required>
                        <option value="Komputer">Komputer</option>
                        <option value="Elektronik">Elektronik</option>
                        <option value="Hand Phone">Hand Phone</option>
                    </select>
                </div>
                <div class="input">
                    <label for="harga_jual">Harga Jual</label>
                    <input type="text" name="harga_jual" id="harga_jual" required>
                </div>
                <div class="input">
                    <label for="harga_beli">Harga Beli</label>
                    <input type="text" name="harga_beli" id="harga_beli" required>
                </div>
                <div class="input">
                    <label for="stok">Stok</label>
                    <input type="text" name="stok" id="stok" required>
                </div>
                <div class="input">
                    <label for="file_gambar">File Gambar</label>
                    <input type="file" name="file_gambar" id="file_gambar" accept="image/*" required>
                </div>
                <div class="submit">
                    <input type="submit" name="submit" value="Simpan">
                </div>
            </form>
            <?php
            require("link.php");
            ?>
        </div>
    </div>
    <?php
        require("footer.php");
    ?>
</body>
</html>
```

### Implementasi pada fitur ubah barang

```
<?php
error_reporting(E_ALL);

include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0) {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . 'gambar/' . $filename;

        if (move_uploaded_file($file_gambar['tmp_name'], $destination)) {
            $gambar = 'gambar/' . $filename;
        }
    }

    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";

    if (!empty($gambar)) {
        $sql .= ", gambar = '{$gambar}' ";
    }

    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);
    header('location: index.php');
}

$id = $_GET['id'];
$sql = "SELECT * FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);

if (!$result) {
    die('Error: Data tidak tersedia');
}

$data = mysqli_fetch_array($result);

function is_select($var, $val) {
    if ($var == $val) {
        return 'selected="selected"';
    }
    return false;
}
?>

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Ubah Barang</title>
</head>

<body>
    <div class="container">
        <h1>Ubah Barang</h1>
        <div class="main">
            <form method="post" action="ubah.php" enctype="multipart/form-data">
                <div class="input">
                    <label>Nama Barang</label>
                    <input type="text" name="nama" value="<?php echo $data['nama']; ?>" />
                </div>
                <div class="input">
                    <label>
                    <select name="kategori">
                        <option <?php echo is_select('Komputer', $data['kategori']); ?> value="Komputer">Komputer</option>
                        <option <?php echo is_select('Elektronik', $data['kategori']); ?> value="Elektronik">Elektronik</option>
                        <option <?php echo is_select('Hand Phone', $data['kategori']); ?> value="Hand Phone">Hand Phone</option>
                    </select>
                    </label>
                </div>
                <div class="input">
                    <label>Harga Jual</label>
                    <input type="text" name="harga_jual" value="<?php echo $data['harga_jual']; ?>" />
                </div>
                <div class="input">
                    <label>Harga Beli</label>
                    <input type="text" name="harga_beli" value="<?php echo $data['harga_beli']; ?>" />
                </div>
                <div class="input">
                    <label>Stok</label>
                    <input type="text" name="stok" value="<?php echo $data['stok']; ?>" />
                </div>
                <div class="input">
                    <label>File Gambar</label>
                    <input type="file" name="file_gambar" />
                </div>
                <div class="submit">
                    <input type="hidden" name="id" value="<?php echo $data['id_barang']; ?>" />
                    <input type="submit" name="submit" value="Simpan" />
                </div>
            </form>
            <?php
            require("link.php");
            ?>
        </div>
    </div>
    <?php
        require("footer.php");
    ?>
</body>
</html>
```



