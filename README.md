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





