# mysql-server
belajar mysql 
.....................
contoh penambahan tambah pada my dql data 
...............///////////////
Update karyawan set nama='David',alamat='Bandung' where id='david';

....................
contoh penghapusan data  pada my dql data
//////////////////////////////////////
delete from namaTabel where fieldFilter='value';
----------------------------
Sekarang kita akan coba jalankan 
script select data berdasarkan
namanya, klik menu SQL masukan 
script dibawah ini, kemudian jalankan.
......//////////////////
SELECT nama from karyawan
............................

SELECT FILTER
Sql select ini berguna untuk teknik reporting, 
ketika datanya sudah banyak ribuan atau 
ahkan jutaan kita menggunakan select filter ini.

Bagaimana jika kita ingin mengambil
data spesifik yang hanya memiliki umur 20
saja ? nah coba jalankan script dibawah ini.
////////////////////////////////////
SELECT * FROM 'karyawan' WHERE umur=20
......................................

Kita juga dapat melakukan select lebih dari 
satu field, dimana kita bisa menggunakan 
keyword AND, kita coba select filter
berdasarkan field umur dan kelamin.

Jalankan script dibawah ini.
//////////////////////////////////////////////
SELECT nama FROM 'karyawan' WHERE umur=20 AND alamat="Jakarta"
.......................................................














.................................
conection.php
$conect = mysql_connect('localhost',
'root',
'pasword',
'nama file data base')
...........................
menampilkan data"
list.php

menampilkan data karyawan mengunakan php dan html
...........................
<?php 

include ('connection.php'); 

$query = mysqli_query($connect,"SELECT * FROM nama data base");
$results = mysqli_fetch_all($query, MYSQLI_ASSOC);
?>

<html>
<body>
 <table border="1">
        <tr>
            <th>Nama</th>
            <th>Alama</th>
            <th>Umur</th>
            <th>Jenis Kelamin</th>
        </tr>
        <?php foreach($results as $result) : ?>
            <tr>
                <td><?php echo $result['nama']?></td>
                <td><?php echo $result['alamat']?></td>
                <td><?php echo $result['umur']?></td>
                <td><?php echo $result['jenis_kelamin']?></td>
            </tr>
        <?php endforeach ?>
    </table>
</body>
</html>
>
---------------------------------------------------------------
add.php
<a href="add.php">Tambah Data</a>

<?php 

include ('connection.php'); 

$query = mysqli_query($connect,"SELECT * FROM karyawan");
$results = mysqli_fetch_all($query, MYSQLI_ASSOC);
?>
<html>
<body>
    <a href="add.php">Tambah Data</a>  

    <br/><br/>

    <table border="1">
        <tr>
            <th>Nama</th>
            <th>Alama</th>
            <th>Umur</th>
            <th>Jenis Kelamin</th>
        </tr>
        <?php foreach($results as $result) : ?>
            <tr>
                <td><?php echo $result['nama']?></td>
                <td><?php echo $result['alamat']?></td>
                <td><?php echo $result['umur']?></td>
                <td><?php echo $result['jenis_kelamin']?></td>
            </tr>
    </table>
</body>
</html>
___________________________________________
Setelah membuat link 
untuk tambah data seperti 
gambar diatas, 
sekarang kita buat file 
baru dengan nama add.php, 
kemudian masukan
kode di bawah ini untuk
membuat formnya.
----------------------------------------------
<html>
    <form action="insert.php" method="post">
        <label>Nama</label><br/>
        <input type="text" name="nama"/>
        <br/><br/>

        <label>Alamat</label><br/>
        <textarea name="alamat" cols="30" rows="10"/></textarea>
        <br/><br/>

        <label>Umur</label><br/>
        <input type="text" name="umur"/>
        <br/><br/>

        <label>Jenis Kelamin</label><br/>
        <select name="jenis_kelamin">
            <option value>="Pria">Pria</option>
            <option value>="Wanita">Wnita</option>
        </select>

        </button type="submit">Tambah</button>
    </form>
</html>
-----------------------------------------------

Insert Data


<?php

include('connection.php');

//karena form menggunakan method post kita gunakan $_POST
$nama = $_POST['nama']; //index didalamnya sesuai dengan input name yang ada di form
$alamat = $_POST['alamat'];
$umur = $_POST['umur'];
$jenis_kelamin = $_POST['jenis_kelamin'];

$insert = mysqli_query($connect,"INSERT INTO karyawan SET nama='$nama', alamat='$alamat', umur='$umur', jenis_kelamin='$jenis_kelamin' "); 

if($insert) 
    header('Location:list.php'); //Jika berhasil akan di arahkan ke halaman list.php
else
    echo 'Input data gagal'; //jika gagal akan keluar pesan tersebut
Sekarang kita coba buka localhost/latihan-crud/add.php kemudian inputka
---------------------------------------------------------------
Update Data

Untuk melakukan update data sebenernya logic nya sama seperti yang sudah kita pelajari 
sebelumnya untuk melakukan edit data pada phpmyadmin, dimana kita d
apat mengedit data satu persatu sesuai dengan id datanya.

Yang perlu kita buat pertama adalah
 link untuk edit data,
kita buka file list.php kemudian
 kita tambahkan judul baru 
pada tabel dengan nama pilihan
 dimana didalamnya terdapat link edt.
__________________________________________________________
<td>
   <a href="edit.php?id=<?php echo $result['id']?>">Edit</a> 
</td>


--------------------------------------------------
Kode diatas digunakan untuk membuat link
edit, dimana ketika di klik akan di
arahkan ke edit.php yang dimana 
setiap link tersebut menyimpan data spesifik 
id dari setiap data yang 
nantinya dapat kita olah pada file edit.php.
-------------------------------------------------------
Kemudian tambahkan kode diatas kedalam file list.php .
-----------------------------------------------------------
<?php 

include ('connection.php'); 

$query = mysqli_query($connect,"SELECT * FROM karyawan");
$results = mysqli_fetch_all($query, MYSQLI_ASSOC);
?>

<html>
<body>
    <a href="add.php">Tambah Data</a>  

     <br/><br/>

    <table border="1">
        <tr>
            <th>Nama</th>
            <th>Alama</th>
            <th>Umur</th>
            <th>Jenis Kelamin</th>
            <th>Pilihan</th>
        </tr>
        <?php foreach($results as $result) : ?>
            <tr>
                <td><?php echo $result['nama']?></td>
                <td><?php echo $result['alamat']?></td>
                <td><?php echo $result['umur']?></td>
                <td><?php echo $result['jenis_kelamin']?></td>
                <td>
                    <a href="edit.php?id=<?php echo $result['id']?>">Edit</a> 
                </td>
            </tr>
    </table>
</body>
</html>
--------------------------------------------
Jika kita lihat pada gambar diatas
maka sekarang sudah terdapat link edit
dimana dimana setiap link tersebut
menyimpan id sesuai dengan datanya, 
seperti dapat kita lihat pada bagian
pojok kiri bawah pada gambar diatas.
----------------------------------------------
Selanjutnya kita buat file 
nama edit.php dimana nantinya
data yang akan kita edit di 
tampilkan dalam form edit ini
-----------------------------------------


include('connection.php');

$id = $_GET['id']; // Untuk mengambil id yang dilempar dari form list.php

$query = mysqli_query($connect,"SELECT * FROM karyawan WHERE id='$id' LIMIT 1"); //mengambil data sesuai dengan id nya
$result = mysqli_fetch_all($query, MYSQLI_ASSOC);
?>

<html>
    <form action="insert.php" method="post">

        <input type="hidden" name="id" value=<?php echo $result[0]['id']?>> <!--untuk menyimpan id tanpa menampilkan data id pada form-->

        <label>Nama</label><br/>
        <input type="text" name="nama" value="<?php echo $result[0]['nama']?>"/> <!--menampilkan data sesuai dr variabel $result diatas-->
        <br/><br/>

        <label>Alamat</label><br/>
        <textarea name="alamat" cols="30" rows="10"/>value="<?php echo $result[0]['alamat']?>"</textarea>
        <br/><br/>

        <label>Umur</label><br/>
        <input type="text" name="umur"/>
        <br/><br/>

        <label>Jenis Kelamin</label><br/>
        <select name="jenis_kelamin">
            <option value>="Pria"<?php echo ($result[0]['jenis_kelamin'] == 'Pria') ? 'selected' : '';?> >Pria</option>
            <option value>="Wanita" "<?php echo ($result[0]['jenis_kelamin'] == 'Wanita') ? 'selected' : '';?> >Wnita</option>
        </select>

        </button type="submit">Perbaharui</button>
    </form>
</html>
-------------------------------------------
Nah sekarang kita perlu membuat handler
untuk menyimpan file yang sudah diisikan
pada 
form edit kedalam database, kita buat 
file update.php, kemudian 
masukan kode seperti dibawah ini.
-------------------------------------------
<?php

include('connection.php'); // Mengkoneksikan dengan database

$id = $_POST['id'];
// Karena form menggunakan method post kita gunakan $_POST
$nama = $_POST['nama']; // Index didalamnya sesuai dengan input name yang ada di form
$alamat = $_POST['alamat'];
$umur = $_POST['umur'];
$jenis_kelamin = $_POST['jenis_kelamin'];

$update = mysqli_query($connect,"UPDATE karyawan SET nama='$nama', alamat='$alamat', umur='$umur', jenis_kelamin='$jenis_kelamin' WHERE id='$id' "); //menggunakan kondisi where untuk menyimpan dengan data spesifik

if($update) 
    header('Location:list.php'); // Jika berhasil akan di arahkan ke halaman list.php
else
    echo 'Input data gagal'; // Jika gagal akan keluar pesan tersebut
?>
----------------------------------------------------
Delete Data
Setelah kita sudah berhasil menambahkan 
fitur update sekarang kita akan tambahkan
fitur delete , dimana sebenarnya konsepnya 
tidak jauh berbeda dengan update 
data karena kita perlu mengirim
data spesifik dari data yang akan kita hapus.

Langsung saja, yang perlu kita 
buat adalah menambahkan 
link delete pada file list.php.
----------------------------------------
<?php 

include ('connection.php'); 

$query = mysqli_query($connect,"SELECT * FROM karyawan");
$results = mysqli_fetch_all($query, MYSQLI_ASSOC);
?>

<html>
<body>
    <a href="add.php">Tambah Data</a>  

     <br/><br/>

    <table border="1">
        <tr>
            <th>Nama</th>
            <th>Alama</th>
            <th>Umur</th>
            <th>Jenis Kelamin</th>
            <th>Pilihan</th>
        </tr>
        <?php foreach($results as $result) : ?>
            <tr>
                <td><?php echo $result['nama']?></td>
                <td><?php echo $result['alamat']?></td>
                <td><?php echo $result['umur']?></td>
                <td><?php echo $result['jenis_kelamin']?></td>
                <td>
                    <a href="edit.php?id=<?php echo $result['id']?>">Edit</a> 
                    <a href="delete.php?id=<?php echo $result['id']?>">Delete</a> 
                </td>
            </tr>
        <?php endforeach;?>
    </table>
</body>
</html>
-------------------------------------
Jika sudah menambahkan link delete,
sekarang kita perlu 
handler untuk menghapus data 
dari database, kita buat
file dengan nama delete
.php masukan kode dibawah ini.
-------------------------------------------
<?php

include('connection.php');//mengkoneksikan database

$id = $_GET('id'); //mengambil id yang di parsing dari halaman list.php

$delete = mysqli_query($connect, "DELETE FORM karyawan WHERE id='$id'); //megnghapus data spesifik

if($delete)
    header('Location : list.php'); 
else
    echo 'Delete data gagal';
    ----------------------------------------
