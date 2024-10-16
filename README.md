# Penjelasan Kodingan
- Import library yang dibutuhkan
```python
import random
import numpy as np
import matplotlib.pyplot as plt
```

- Definisikan variable warna, tinggi dan lebar dari pohon, jalan, rumah serta warna dari rumput
```python
BASE_COLOR = 0  # Base color for blocks with no items
HOUSE_COLOR = 18  # Color for the house
TREE_COLOR = 11  # Color for the tree
ROAD_COLOR = 6  # Color for the road
GRASS_COLOR = 2  # Background color

# Fixed dimensions for items
TREE_SIZE = 10
HOUSE_WIDTH = 20
HOUSE_HEIGHT = 15
ROAD_WIDTH = 10
```
## Class Tree
Kelas ini digunakan untuk merepresentasikan objek pohon di dalam map. Pohon memiliki beberapa atribut, seperti posisi, ukuran, nama, dan umur. Selain itu, kelas ini juga memiliki beberapa metode yang digunakan untuk mendapatkan gambar representasi dari pohon dan menghitung koordinat kiri atasnya di map.

```python
class Tree:
    def __init__(self, pos):
        self.pos = pos
        self.size = TREE_SIZE
        self.name = "Tree"
        self.age = random.randint(1, 100)

    def get_image(self):
        img = np.ones((self.size, self.size)) * TREE_COLOR
        return img

    def get_topleft(self):
        xleft = self.pos[0] - self.size // 2
        ytop = self.pos[1] - self.size // 2
        return (xleft, ytop)
```
####  Bagian-bagian class Tree:
```
def __init__(self, pos):
        self.pos = pos
        self.size = TREE_SIZE
        self.name = "Tree"
        self.age = random.randint(1, 100)
```
1. ```self.pose```:
    - Tipe: Tuple ```(x, y)```
    - Fungsi: Menyimpan posisi pohon dalam bentuk koordinat ```(x, y)``` pada map. Posisi ini ditentukan saat pohon dibuat. Koordinat ini adalah titik pusat pohon.
2. ```self.size```:
    - Tipe: Integer
    - Fungsi: Menyimpan ukuran dari pohon. Ukuran ini sudah ditentukan sebelumnya oleh variabel ```TREE_SIZE```, yang nilainya diatur sebagai 10. Ukuran ini merupakan dimensi pohon dalam piksel, yaitu ```10x10``` piksel.
3. ```self.name```:
    - Tipe: String
    - Fungsi: Menyimpan nama dari objek pohon, yaitu "Tree". Nama ini bisa digunakan untuk membedakan objek ini dari objek lain seperti rumah atau jalan.
4. ```self.age```:
    - Tipe: Integer
    - Fungsi: Menyimpan usia pohon, yang ditentukan secara acak menggunakan fungsi ```random.randint(1, 100)```. Setiap pohon akan memiliki usia yang berbeda-beda di antara 1 hingga 100 tahun

```python
def get_image(self):
        img = np.ones((self.size, self.size)) * TREE_COLOR
        return img
```
Fungsi ```def get_image(self)```:
Metode ini digunakan untuk menghasilkan representasi visual dari pohon dalam bentuk matriks numpy. Pohon akan ditampilkan sebagai matriks berukuran 10x10 (sesuai dengan TREE_SIZE) yang diisi dengan nilai warna tertentu.

Langkah Kerja:
- ```np.ones((self.size, self.size))```:
    Fungsi ```np.ones``` menghasilkan matriks (array 2D) dengan ukuran ```self.size x self.size```, yaitu ```10x10```, yang diisi dengan nilai 1. Setiap elemen dalam matriks ini merepresentasikan sebuah piksel.
- ```TREE_COLOR```:
    Setiap elemen dalam matriks yang sebelumnya diisi dengan 1 akan dikalikan dengan ```TREE_COLOR```. ```TREE_COLOR``` adalah variabel global yang mendefinisikan warna pohon, dalam hal ini nilainya 11. Jadi, seluruh elemen dalam matriks tersebut diubah menjadi 11, yang akan digunakan sebagai warna pohon dalam representasi map.
- ```Return```:
    Metode ini mengembalikan matriks numpy berukuran 10x10 yang berisi nilai 11, yang mewakili warna dari pohon.

```python
def get_topleft(self):
        xleft = self.pos[0] - self.size // 2
        ytop = self.pos[1] - self.size // 2
        return (xleft, ytop)
```
Fungsi```def get_topleft(self)```: 
Metode ini digunakan untuk menghitung koordinat kiri atas dari pohon. Koordinat ini diperlukan untuk menempatkan gambar pohon di dalam map.

Langkah Kerja:
1. ```self.pos[0] - self.size // 2```:
    - ```self.pos[0]```: Ini adalah posisi x dari pohon yang disimpan di atribut pos (titik pusat pohon). Misalnya, jika pohon berada pada koordinat (50, 50), maka self.pos[0] adalah 50.
    - ```self.size // 2```: Ini adalah setengah dari ukuran pohon, yaitu 10 // 2 = 5. Dengan membagi ukuran pohon menjadi dua, kita bisa menemukan jarak dari pusat pohon ke tepi kiri.
    - ```xleft```: Dengan mengurangkan setengah ukuran pohon dari posisi x (titik pusat), kita mendapatkan koordinat x dari sisi kiri pohon. Misalnya, jika posisi x adalah 50 dan ukuran pohon 10, maka sisi kiri pohon adalah 50 - 5 = 45.
2.	```self.pos[1] - self.size // 2```:
    - Proses ini mirip dengan perhitungan x, tetapi untuk sumbu y (atas/bawah). Ini digunakan untuk menghitung koordinat y dari sisi atas pohon.
    - Misalnya, jika posisi y pohon adalah 50, maka sisi atas pohon adalah 50 - 5 = 45.
3. ```Return```:
    - Metode ini mengembalikan tuple ```(xleft, ytop)``` yang merupakan koordinat dari sudut kiri atas pohon. Koordinat ini diperlukan untuk menempatkan gambar pohon di posisi yang benar pada map, karena posisi yang disimpan (di atribut pos) adalah pusat pohon, bukan sudutnya.

## Class House
Kelas House digunakan untuk merepresentasikan objek rumah di dalam map. Setiap rumah memiliki atribut seperti posisi, lebar, tinggi, nama, dan umur. Selain itu, kelas ini memiliki metode untuk menggambar rumah dalam bentuk matriks (array) dan menghitung koordinat kiri atasnya untuk menempatkannya di map.
```python
class House:
    def __init__(self, pos):
        self.pos = pos
        self.width = HOUSE_WIDTH
        self.height = HOUSE_HEIGHT
        self.name = "House"
        self.age = random.randint(1, 100)

    def get_image(self):
        img = np.ones((self.height, self.width)) * HOUSE_COLOR
        return img

    def get_topleft(self):
        xleft = self.pos[0] - self.width // 2
        ytop = self.pos[1] - self.height // 2
        return (xleft, ytop)
```
### Bagian-Bagian Class House
```python
 def __init__(self, pos):
        self.pos = pos
        self.width = HOUSE_WIDTH
        self.height = HOUSE_HEIGHT
        self.name = "House"
        self.age = random.randint(1, 100)
```
1. ```self.pos```:
    - Tipe: Tuple (x, y)
    - Fungsi: Menyimpan posisi rumah dalam bentuk koordinat (x, y) pada map. Posisi ini ditentukan ketika rumah dibuat dan merepresentasikan titik pusat rumah.
2. ```self.width```:
    - Tipe: Integer
    - Fungsi: Menyimpan lebar rumah. Lebar ini ditentukan oleh variabel HOUSE_WIDTH, yang sudah didefinisikan sebelumnya sebagai 20 piksel. Lebar ini tetap untuk setiap rumah yang dibuat.
3. ```self.height```:
    - Tipe: Integer
    - Fungsi: Menyimpan tinggi rumah, yang ditentukan oleh variabel HOUSE_HEIGHT sebesar 15 piksel. Sama seperti width, tinggi ini juga tetap untuk setiap rumah.
4. ```self.name```:
    - Tipe: String
    - Fungsi: Menyimpan nama dari objek, yaitu "House". Nama ini membedakan rumah dari objek lain seperti pohon atau jalan.
5. ```self.age```:
    - Tipe: Integer
    - Fungsi: Menyimpan usia rumah dalam bentuk angka acak yang dihasilkan oleh fungsi random.randint(1, 100). Setiap rumah memiliki usia antara 1 hingga 100 tahun.
```python
def get_image(self):
    img = np.ones((self.height, self.width)) * HOUSE_COLOR
    return img
```
Metode ini menghasilkan gambar atau representasi visual dari rumah dalam bentuk matriks numpy (array 2D) berisi nilai warna tertentu untuk rumah.

Langkah Kerja:
1.	```np.ones((self.height, self.width))```:
Fungsi np.ones membuat matriks berukuran self.height x self.width (15x20 piksel), di mana semua nilai elemennya diinisialisasi menjadi 1. Setiap elemen dalam matriks ini merepresentasikan satu piksel dari gambar rumah.
2.	```HOUSE_COLOR```:
Setiap elemen di dalam matriks yang awalnya bernilai 1 kemudian dikalikan dengan HOUSE_COLOR. HOUSE_COLOR adalah variabel global yang mendefinisikan warna rumah (dalam hal ini, bernilai 18). Jadi, seluruh elemen dalam matriks tersebut menjadi 18, yang digunakan sebagai warna rumah pada map.
3.	```Return```:
Metode ini mengembalikan matriks numpy berukuran 15x20 piksel yang berisi nilai 18, merepresentasikan gambar rumah yang akan ditempatkan pada map.

```python
def get_topleft(self):
    xleft = self.pos[0] - self.width // 2
    ytop = self.pos[1] - self.height // 2
    return (xleft, ytop)
```
Metode ini digunakan untuk menghitung koordinat kiri atas dari rumah berdasarkan posisi pusatnya. Koordinat ini diperlukan untuk menentukan posisi rumah yang tepat di dalam map.

Langkah Kerja:
1.	```self.pos[0] - self.width // 2```:
    - ```self.pos[0]```: Ini adalah posisi x dari pusat rumah, disimpan dalam atribut pos. Jika pusat rumah berada pada titik ```(50, 50)```, maka ```self.pos[0]``` adalah 50.
    - ```self.width // 2```: Ini adalah setengah dari lebar rumah, yaitu```20 // 2 = 10```. Dengan menghitung setengah lebar rumah, kita dapat mengetahui jarak dari pusat rumah ke tepi kiri.
    - ```xleft```: Dengan mengurangkan setengah dari lebar rumah dari posisi pusat x, kita mendapatkan koordinat x dari sudut kiri rumah. Misalnya, jika lebar rumah 20 piksel dan posisi x rumah 50, maka sisi kiri rumah berada pada ```50 - 10 = 40```.
2. ```self.pos[1] - self.height // 2```:
    - ```self.pos[1]```: Ini adalah posisi y dari pusat rumah (50 dalam contoh).
    - ```self.height // 2```: Ini adalah setengah dari tinggi rumah, yaitu ```15 // 2``` = 7. Jadi, jarak dari pusat rumah ke tepi atas adalah 7 piksel.
    -```ytop```: Dengan mengurangkan setengah dari tinggi rumah dari posisi pusat y, kita mendapatkan koordinat y dari sudut kiri atas rumah. Jika posisi y rumah adalah 50, maka sudut kiri atas rumah ada pada ```50 - 7 = 43```.
3.	```Return```:
Metode ini mengembalikan tuple (xleft, ytop), yang merupakan koordinat dari sudut kiri atas rumah. Koordinat ini digunakan untuk menempatkan gambar rumah di lokasi yang tepat pada map, karena posisi yang disimpan (self.pos) adalah pusat rumah, bukan tepi kirinya.
