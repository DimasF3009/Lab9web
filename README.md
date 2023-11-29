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

### Buat file dengan kontak.php 
```
<?php require('header.php'); ?>
    <div class="content">
        <h2>Ini Halaman kontak</h2>
        <p>Ini adalah bagian content dari halaman.</p>
    </div>
<?php require('footer.php'); ?>
```

### Buat file dengan home.php
```
<?php require('header.php')?>
<div class="content">
        <h2>Ini Halaman home</h2>
        <p>Ini adalah bagian content dari halaman.</p>
    </div>
<?php require('footer.php');?>
``

