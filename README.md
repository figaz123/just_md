# Penjelasan Kodingan
- Import library yang dibutuhkan
```python
import random
import numpy as np
import matplotlib.pyplot as plt
```

- Definisikan variable warna, tinggi dan lebar dari tree, road, house serta warna dari rumput
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
Kelas ini digunakan untuk merepresentasikan objek tree di dalam map. Tree memiliki beberapa atribut, seperti posisi, ukuran, nama, dan umur. Selain itu, kelas ini juga memiliki beberapa metode yang digunakan untuk mendapatkan gambar representasi dari tree dan menghitung koordinat kiri atasnya di map.

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
    - Fungsi: Menyimpan posisi tree dalam bentuk koordinat ```(x, y)``` pada map. Posisi ini ditentukan saat tree dibuat. Koordinat ini adalah titik pusat tree.
2. ```self.size```:
    - Tipe: Integer
    - Fungsi: Menyimpan ukuran dari tree. Ukuran ini sudah ditentukan sebelumnya oleh variabel ```TREE_SIZE```, yang nilainya diatur sebagai 10. Ukuran ini merupakan dimensi tree dalam piksel, yaitu ```10x10``` piksel.
3. ```self.name```:
    - Tipe: String
    - Fungsi: Menyimpan nama dari objek tree, yaitu "Tree". Nama ini bisa digunakan untuk membedakan objek ini dari objek lain seperti house atau road.
4. ```self.age```:
    - Tipe: Integer
    - Fungsi: Menyimpan usia tree, yang ditentukan secara acak menggunakan fungsi ```random.randint(1, 100)```. Setiap tree akan memiliki usia yang berbeda-beda di antara 1 hingga 100 tahun

```python
def get_image(self):
        img = np.ones((self.size, self.size)) * TREE_COLOR
        return img
```
Fungsi ```def get_image(self)```:
Metode ini digunakan untuk menghasilkan representasi visual dari tree dalam bentuk matriks numpy. Tree akan ditampilkan sebagai matriks berukuran 10x10 (sesuai dengan TREE_SIZE) yang diisi dengan nilai warna tertentu.

Langkah Kerja:
- ```np.ones((self.size, self.size))```:
    Fungsi ```np.ones``` menghasilkan matriks (array 2D) dengan ukuran ```self.size x self.size```, yaitu ```10x10```, yang diisi dengan nilai 1. Setiap elemen dalam matriks ini merepresentasikan sebuah piksel.
- ```TREE_COLOR```:
    Setiap elemen dalam matriks yang sebelumnya diisi dengan 1 akan dikalikan dengan ```TREE_COLOR```. ```TREE_COLOR``` adalah variabel global yang mendefinisikan warna tree, dalam hal ini nilainya 11. Jadi, seluruh elemen dalam matriks tersebut diubah menjadi 11, yang akan digunakan sebagai warna tree dalam representasi map.
- ```Return```:
    Metode ini mengembalikan matriks numpy berukuran 10x10 yang berisi nilai 11, yang mewakili warna dari tree.

```python
def get_topleft(self):
        xleft = self.pos[0] - self.size // 2
        ytop = self.pos[1] - self.size // 2
        return (xleft, ytop)
```
Fungsi```def get_topleft(self)```: 
Metode ini digunakan untuk menghitung koordinat kiri atas dari tree. Koordinat ini diperlukan untuk menempatkan gambar tree di dalam map.

Langkah Kerja:
1. ```self.pos[0] - self.size // 2```:
    - ```self.pos[0]```: Ini adalah posisi x dari tree yang disimpan di atribut pos (titik pusat tree). Misalnya, jika tree berada pada koordinat (50, 50), maka self.pos[0] adalah 50.
    - ```self.size // 2```: Ini adalah setengah dari ukuran tree, yaitu 10 // 2 = 5. Dengan membagi ukuran tree menjadi dua, kita bisa menemukan jarak dari pusat tree ke tepi kiri.
    - ```xleft```: Dengan mengurangkan setengah ukuran tree dari posisi x (titik pusat), kita mendapatkan koordinat x dari sisi kiri tree. Misalnya, jika posisi x adalah 50 dan ukuran tree 10, maka sisi kiri tree adalah 50 - 5 = 45.
2.	```self.pos[1] - self.size // 2```:
    - Proses ini mirip dengan perhitungan x, tetapi untuk sumbu y (atas/bawah). Ini digunakan untuk menghitung koordinat y dari sisi atas tree.
    - Misalnya, jika posisi y tree adalah 50, maka sisi atas tree adalah 50 - 5 = 45.
3. ```Return```:
    - Metode ini mengembalikan tuple ```(xleft, ytop)``` yang merupakan koordinat dari sudut kiri atas tree. Koordinat ini diperlukan untuk menempatkan gambar tree di posisi yang benar pada map, karena posisi yang disimpan (di atribut pos) adalah pusat tree, bukan sudutnya.

## Class House
Kelas House digunakan untuk merepresentasikan objek house di dalam map. Setiap house memiliki atribut seperti posisi, lebar, tinggi, nama, dan umur. Selain itu, kelas ini memiliki metode untuk menggambar house dalam bentuk matriks (array) dan menghitung koordinat kiri atasnya untuk menempatkannya di map.
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
    - Fungsi: Menyimpan posisi house dalam bentuk koordinat (x, y) pada map. Posisi ini ditentukan ketika house dibuat dan merepresentasikan titik pusat house.
2. ```self.width```:
    - Tipe: Integer
    - Fungsi: Menyimpan lebar house. Lebar ini ditentukan oleh variabel HOUSE_WIDTH, yang sudah didefinisikan sebelumnya sebagai 20 piksel. Lebar ini tetap untuk setiap house yang dibuat.
3. ```self.height```:
    - Tipe: Integer
    - Fungsi: Menyimpan tinggi house, yang ditentukan oleh variabel HOUSE_HEIGHT sebesar 15 piksel. Sama seperti width, tinggi ini juga tetap untuk setiap house.
4. ```self.name```:
    - Tipe: String
    - Fungsi: Menyimpan nama dari objek, yaitu "House". Nama ini membedakan house dari objek lain seperti tree atau road.
5. ```self.age```:
    - Tipe: Integer
    - Fungsi: Menyimpan usia house dalam bentuk angka acak yang dihasilkan oleh fungsi random.randint(1, 100). Setiap house memiliki usia antara 1 hingga 100 tahun.
```python
def get_image(self):
    img = np.ones((self.height, self.width)) * HOUSE_COLOR
    return img
```
Metode ini menghasilkan gambar atau representasi visual dari house dalam bentuk matriks numpy (array 2D) berisi nilai warna tertentu untuk house.

Langkah Kerja:
1.	```np.ones((self.height, self.width))```:
Fungsi np.ones membuat matriks berukuran self.height x self.width (15x20 piksel), di mana semua nilai elemennya diinisialisasi menjadi 1. Setiap elemen dalam matriks ini merepresentasikan satu piksel dari gambar house.
2.	```HOUSE_COLOR```:
Setiap elemen di dalam matriks yang awalnya bernilai 1 kemudian dikalikan dengan HOUSE_COLOR. HOUSE_COLOR adalah variabel global yang mendefinisikan warna house (dalam hal ini, bernilai 18). Jadi, seluruh elemen dalam matriks tersebut menjadi 18, yang digunakan sebagai warna house pada map.
3.	```Return```:
Metode ini mengembalikan matriks numpy berukuran 15x20 piksel yang berisi nilai 18, merepresentasikan gambar house yang akan ditempatkan pada map.

```python
def get_topleft(self):
    xleft = self.pos[0] - self.width // 2
    ytop = self.pos[1] - self.height // 2
    return (xleft, ytop)
```
Metode ini digunakan untuk menghitung koordinat kiri atas dari house berdasarkan posisi pusatnya. Koordinat ini diperlukan untuk menentukan posisi house yang tepat di dalam map.

Langkah Kerja:
1.	```self.pos[0] - self.width // 2```:
    - ```self.pos[0]```: Ini adalah posisi x dari pusat house, disimpan dalam atribut pos. Jika pusat house berada pada titik ```(50, 50)```, maka ```self.pos[0]``` adalah 50.
    - ```self.width // 2```: Ini adalah setengah dari lebar house, yaitu```20 // 2 = 10```. Dengan menghitung setengah lebar house, kita dapat mengetahui jarak dari pusat house ke tepi kiri.
    - ```xleft```: Dengan mengurangkan setengah dari lebar house dari posisi pusat x, kita mendapatkan koordinat x dari sudut kiri house. Misalnya, jika lebar house 20 piksel dan posisi x house 50, maka sisi kiri house berada pada ```50 - 10 = 40```.
2. ```self.pos[1] - self.height // 2```:
    - ```self.pos[1]```: Ini adalah posisi y dari pusat house (50 dalam contoh).
    - ```self.height // 2```: Ini adalah setengah dari tinggi house, yaitu ```15 // 2``` = 7. Jadi, jarak dari pusat house ke tepi atas adalah 7 piksel.
    -```ytop```: Dengan mengurangkan setengah dari tinggi house dari posisi pusat y, kita mendapatkan koordinat y dari sudut kiri atas house. Jika posisi y house adalah 50, maka sudut kiri atas house ada pada ```50 - 7 = 43```.
3.	```Return```:
Metode ini mengembalikan tuple (xleft, ytop), yang merupakan koordinat dari sudut kiri atas house. Koordinat ini digunakan untuk menempatkan gambar house di lokasi yang tepat pada map, karena posisi yang disimpan (self.pos) adalah pusat house, bukan tepi kirinya.

# Class Road
Kelas Road digunakan untuk merepresentasikan objek road pada map. Setiap objek road memiliki atribut seperti posisi, panjang, dan lebar. Selain itu, kelas ini memiliki metode untuk menggambarkan road dalam bentuk matriks (array) dan menghitung koordinat kiri atas road untuk penempatan di map.

```python
class Road:
    def __init__(self, pos, length):
        self.pos = pos
        self.length = length
        self.width = ROAD_WIDTH
        self.name = "Road"

    def get_image(self):
        img = np.ones((self.length, self.width)) * ROAD_COLOR
        return img

    def get_topleft(self):
        xleft = self.pos[0] - self.width // 2
        ytop = self.pos[1]  # start_y is at the top of the road
        return (xleft, ytop)
```
## Bagian-Bagian Class Road
```python
def __init__(self, pos, length):
        self.pos = pos
        self.length = length
        self.width = ROAD_WIDTH
        self.name = "Road"
```
1. ```self.pos```:
    - Tipe: Tuple ```(x, y)```
    - Fungsi: Menyimpan posisi tengah dari road dalam bentuk koordinat (x, y) pada map. Posisi ini direpresentasikan oleh self.pos yang menentukan di mana road akan ditempatkan.
2. ```self.length```:
    - Tipe: Integer
    - Fungsi: Menyimpan panjang road, yang diberikan sebagai parameter ketika objek Road dibuat. Panjang ini akan menentukan seberapa jauh road terbentang secara vertikal di map.
3. ```self.width```:
    - Tipe: Integer
    - Fungsi: Menyimpan lebar road yang sudah ditentukan oleh variabel global ```ROAD_WIDTH```. Nilai lebar road ini tetap untuk setiap road yang dibuat, dan dalam contoh ini lebarnya adalah 10 piksel.

```python
def get_image(self):
        img = np.ones((self.length, self.width)) * ROAD_COLOR
        return img
```
Metode ini menghasilkan gambar atau representasi visual dari road dalam bentuk matriks numpy (array 2D) yang berisi nilai warna tertentu untuk road.

Langkah Kerja:
1.	```np.ones((self.length, self.width))```:
    - Fungsi np.ones membuat sebuah matriks dengan ukuran panjang x lebar road (yaitu self.length x self.width). Matriks ini berisi nilai 1 di semua elemennya. Ukuran dari matriks ini ditentukan oleh panjang dan lebar road.
    - Misalnya, jika panjang road adalah 60 piksel dan lebarnya 10 piksel, matriks yang dihasilkan adalah berukuran 60 x 10.
2.	```ROAD_COLOR```:
    - Setiap elemen dalam matriks yang awalnya bernilai 1 kemudian dikalikan dengan nilai ROAD_COLOR, yang merupakan variabel global yang mendefinisikan warna road (dalam contoh ini, nilainya adalah 6). Jadi, seluruh elemen dalam matriks akan menjadi 6, yang merepresentasikan warna road pada map.
3.	```Return```:
    Metode ini mengembalikan matriks numpy berukuran (self.length x self.width) yang berisi nilai 6 untuk merepresentasikan road. Matriks ini akan digunakan untuk menggambarkan road di map.

```python
def get_topleft(self):
        xleft = self.pos[0] - self.width // 2
        ytop = self.pos[1]  # start_y is at the top of the road
        return (xleft, ytop)
```
Fungsi ini digunakan untuk menghitung koordinat kiri atas dari road berdasarkan posisi tengahnya. Koordinat kiri atas ini diperlukan untuk menempatkan gambar road di lokasi yang tepat di map.
Langkah Kerja:
1.	```xleft = self.pos[0] - self.width // 2```:
    - ```self.pos[0]```: Ini adalah posisi ```x``` dari tengah road. Misalnya, jika pusat road berada pada titik ```(100, 50)```, maka ```nilai - self.pos[0]``` adalah ```100```.
    - ```self.width // 2```: Ini adalah setengah dari lebar road. Dengan membagi lebar road dengan 2, kita bisa mengetahui jarak dari pusat road ke tepi kirinya. Jika lebar road adalah 10 piksel, maka setengah lebarnya adalah 5.
    - ```xleft```: Untuk mendapatkan koordinat x dari sudut kiri road, kita mengurangkan setengah dari lebar road dari posisi tengah x. Misalnya, jika x pusat road adalah 100, maka koordinat kiri road adalah 100 - 5 = 95.
2.	```ytop = self.pos[1]```:
    - ```self.pos[1]```: Ini adalah posisi y dari titik tengah road, yang diambil langsung tanpa perubahan. Dalam contoh ini, misalnya nilai y adalah 50, maka koordinat y atas dari road juga adalah 50.
3.	```Return```:
    Metode ini mengembalikan tuple ```(xleft, ytop)```, yang merupakan koordinat dari sudut kiri atas road. Koordinat ini digunakan untuk menentukan di mana road akan digambar di map, karena titik posisi yang disimpan adalah titik tengah, sedangkan gambar harus dimulai dari sudut kiri atas.

# Class Block()
```python
class Block:
    def __init__(self, size, topleft):
        self.size = size
        self.topleft = topleft
        self.items = []  # List to hold items

    def add_item(self, item):
        self.items.append(item)

    def check_overlap(self, new_item):
        """Checks if the new item overlaps with existing items in the block."""
        new_item_topleft = new_item.get_topleft()
        new_item_size = new_item.get_image().shape  # Get the size of the new item

        for item in self.items:
            item_topleft = item.get_topleft()
            item_size = item.get_image().shape  # Get the size of the existing item

            # Check if the new item overlaps with the existing item
            if (new_item_topleft[0] < item_topleft[0] + item_size[1] and
                new_item_topleft[0] + new_item_size[1] > item_topleft[0] and
                new_item_topleft[1] < item_topleft[1] + item_size[0] and
                new_item_topleft[1] + new_item_size[0] > item_topleft[1]):
                return True  # Overlap detected

        return False  # No overlap
```
Fungsi ini digunakan untuk menghasilkan gambar dari sebuah **block**, termasuk latar belakang (rumput) dan objek-objek yang ada di dalam block seperti tree, house, atau road. Gambar yang dihasilkan adalah numpy array yang mewakili warna dan ukuran dari elemen-elemen yang ada dalam block tersebut. Fungsi ini juga memastikan bahwa objek-objek ditampilkan dalam urutan tertentu dan ditempatkan pada koordinat yang benar.
## Bagian-Bagian Class Block()
1. ```grid = np.ones((self.size,self.size))*GRASS_COLOR``` 
    - np.ones((self.size, self.size)) membuat sebuah numpy array dua dimensi berukuran self.size x self.size, di mana setiap elemen array diisi dengan angka 1.
    - GRASS_COLOR: Seluruh elemen array tersebut dikalikan dengan warna rumput (GRASS_COLOR), sehingga seluruh block diinisialisasi sebagai rumput.
    - Jadi, grid akan merepresentasikan area block dengan latar belakang rumput sebelum objek lain seperti tree, house, atau road ditambahkan.

Contoh: Jika ukuran block adalah ```120x120```, maka grid akan berisi array 120x120 yang setiap elemennya memiliki nilai ```GRASS_COLOR```.

```for item in self.items: topleft = item.get_topleft() img = item.get_image()```

```self.items``` adalah daftar objek (tree, house, atau road) yang telah ditambahkan ke dalam block. Fungsi ini akan menggambar setiap objek tersebut dalam urutan mereka ada di dalam list.

Untuk setiap item di dalam list:
- ```item.get_topleft()``` mendapatkan koordinat sudut kiri atas dari objek. Ini menentukan di mana objek akan ditempatkan di dalam grid block.
- item.get_image() mengambil gambar dari objek berupa numpy array. Ukuran dan warnanya tergantung pada objek (misalnya, tree, house, atau road).

```cx_start = max(0, topleft[0])
ry_start = max(0, topleft[1])
cx_stop = min(cx_start + img.shape[1], self.size)
ry_stop = min(ry_start + img.shape[0], self.size)
```

-	```cx_start``` dan ```ry_start``` adalah koordinat awal (x dan y) dari sudut kiri atas objek di dalam grid.
-	Fungsi ```max(0, topleft[0])``` memastikan bahwa koordinat ```x``` dari objek tidak di luar batas kiri block (harus >= 0).
-	Fungsi ```min(cx_start + img.shape[1], self.size)``` memastikan bahwa ujung kanan objek tidak melebihi ukuran block.
-	```cx_stop``` adalah titik di mana objek berakhir di koordinat x dan ```ry_stop``` adalah titik akhir di koordinat y.
-	```img.shape[1]``` dan ```img.shape[0]``` memberikan lebar dan tinggi dari objek tersebut.

```
if ry_start < self.size and cx_start < self.size:
    grid[ry_start:ry_stop, cx_start:cx_stop] = img[:ry_stop - ry_start, :cx_stop - cx_start]
```
Penjelasan:
```if ry_start < self.size and cx_start < self.size```: 
- Memastikan bahwa objek tidak melebihi ukuran block di koordinat y dan x.
- Jika objek pas dalam block, bagian dari grid yang sesuai dengan koordinat objek akan diisi dengan nilai gambar objek.

```grid[ry_start:ry_stop, cx_start:cx_stop] = img[:ry_stop - ry_start, :cx_stop - cx_start]```:
- Potongan gambar dari objek (dari awal hingga akhir di kedua sumbu x dan y) akan ditempatkan pada posisi yang sesuai di dalam grid.
- Misalnya, jika ada tree dengan ukuran 10x10 piksel, dan ```cx_start = 50```, ```ry_start = 20```, maka grid dari (50, 20) hingga (60, 30) akan diisi dengan warna tree.
- 

# Class Map
```python
class Map:
    def __init__(self, map_shape, blocksize):
        self.map_shape = map_shape
        self.blocksize = blocksize
        self.blocks = []

        for r in range(map_shape[0]):
            for c in range(map_shape[1]):
                new_block = Block(blocksize, (r * blocksize, c * blocksize))
                self.blocks.append(new_block)

    def generate_rgb_view(self):
        rgb_view = np.zeros((self.map_shape[0] * self.blocksize, self.map_shape[1] * self.blocksize))
        for block in self.blocks:
            block_image = block.generate_image()
            cx_start, ry_start = block.topleft
            rgb_view[ry_start:ry_start + self.blocksize, cx_start:cx_start + self.blocksize] = block_image
        return rgb_view

    def generate_thermal_view(self, base_temp=20):
        # Initialize the thermal view with the base temperature for all pixels
        thermal_view = np.ones((self.map_shape[0] * self.blocksize, self.map_shape[1] * self.blocksize)) * base_temp

        for block in self.blocks:
            cx_start, ry_start = block.topleft
            block_temp = np.ones((self.blocksize, self.blocksize)) * base_temp  # Local block temperature

            # Apply the temperature effects based on items in the block
            for item in block.items:
                item_img = item.get_image()
                topleft = item.get_topleft()
                item_x_start = max(0, topleft[0])
                item_y_start = max(0, topleft[1])
                item_x_end = min(item_x_start + item_img.shape[1], self.blocksize)
                item_y_end = min(item_y_start + item_img.shape[0], self.blocksize)

                # Check for valid indices
                if item_y_start < self.blocksize and item_x_start < self.blocksize:
                    if isinstance(item, House):
                        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 5  # House adds 5°C
                    elif isinstance(item, Tree):
                        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 2  # Tree adds 2°C
                    elif isinstance(item, Road):
                        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 1  # Road adds 1°C

            # Ensure the thermal view indices are valid
            if ry_start + self.blocksize <= thermal_view.shape[0] and cx_start + self.blocksize <= thermal_view.shape[1]:
                thermal_view[ry_start:ry_start + self.blocksize, cx_start:cx_start + self.blocksize] += block_temp

        return thermal_view
```
Kelas Map berfungsi untuk merepresentasikan map yang terdiri dari kumpulan block. Setiap block di dalam map bisa berisi objek seperti tree, house, atau road. Map memiliki dua jenis tampilan, yaitu RGB view untuk representasi visual (warna) dan thermal view untuk representasi suhu.

## Bagian-bagian Class Map()
```python
def __init__(self, map_shape, blocksize):
        self.map_shape = map_shape
        self.blocksize = blocksize
        self.blocks = []

        for r in range(map_shape[0]):
            for c in range(map_shape[1]):
                new_block = Block(blocksize, (r * blocksize, c * blocksize))
                self.blocks.append(new_block)
```
Inisialisasi sebuah objek map.
1. Parameter:
    - map_shape: Ukuran map dalam bentuk tuple (row, col) yang menunjukkan jumlah baris dan kolom block.
    - blocksize: Ukuran dari setiap block dalam map, dalam satuan piksel.

2. Inisialisasi properti:
    - self.map_shape: Menyimpan ukuran Map dalam bentuk baris dan kolom.
    - self.blocksize: Menyimpan ukuran block dalam satuan piksel.
    - self.blocks: List yang akan menyimpan objek-objek block.

Membuat objek-objek block:
```
for r in range(map_shape[0]):
    for c in range(map_shape[1]):
        new_block = Block(blocksize, (r * blocksize, c * blocksize))
        self.blocks.append(new_block)
```

1. Melakukan looping melalui jumlah baris ```(r)``` dan kolom ```(c)``` dari map.
2. Untuk setiap kombinasi baris dan kolom, dibuat objek Block baru dengan ukuran yang sudah ditentukan.
    - Block(blocksize, (r * blocksize, c * blocksize)): Membuat block dengan ukuran blocksize dan menentukan posisi awal (topleft) block di grid map berdasarkan indeks baris dan kolom.
    - Semua objek block ditambahkan ke dalam list self.blocks.

```
def generate_rgb_view(self):
        rgb_view = np.zeros((self.map_shape[0] * self.blocksize, self.map_shape[1] * self.blocksize))
        for block in self.blocks:
            block_image = block.generate_image()
            cx_start, ry_start = block.topleft
            rgb_view[ry_start:ry_start + self.blocksize, cx_start:cx_start + self.blocksize] = block_image
        return rgb_view
```
Menghasilkan representasi visual map dalam format RGB view.

Inisialisasi grid kosong:

```rgb_view = np.zeros((self.map_shape[0] * self.blocksize, self.map_shape[1] * self.blocksize))```

•	Membuat numpy array dua dimensi yang ukurannya sesuai dengan ukuran seluruh map (baris ukuran block, kolom ukuran block).
•	Semua elemen array diinisialisasi dengan nilai 0.

Menggambar setiap block di map:
```
for block in self.blocks:
    block_image = block.generate_image()
    cx_start, ry_start = block.topleft
    rgb_view[ry_start:ry_start + self.blocksize, cx_start:cx_start + self.blocksize] = block_image
```
1. Looping melalui setiap block yang ada di map:
    - block.generate_image(): Memanggil fungsi dari objek block untuk menghasilkan gambar dari block tersebut, termasuk objek yang ada di dalamnya.
    - block.topleft: Mendapatkan koordinat topleft dari block untuk menempatkannya di dalam grid map.
    - Mengisi grid: Gambar block akan ditempatkan pada koordinat yang sesuai di dalam rgb_view dengan rentang dari ry_start hingga ry_start + blocksize dan cx_start hingga cx_start + blocksize.

2. Mengembalikan hasil:
    Setelah seluruh block ditempatkan di grid map, fungsi akan mengembalikan rgb_view yang berisi representasi visual dari seluruh map.

``` 
def generate_thermal_view(self, base_temp=20):
        # Initialize the thermal view with the base temperature for all pixels
        thermal_view = np.ones((self.map_shape[0] * self.blocksize, self.map_shape[1] * self.blocksize)) * base_temp

        for block in self.blocks:
            cx_start, ry_start = block.topleft
            block_temp = np.ones((self.blocksize, self.blocksize)) * base_temp  # Local block temperature

            # Apply the temperature effects based on items in the block
            for item in block.items:
                item_img = item.get_image()
                topleft = item.get_topleft()
                item_x_start = max(0, topleft[0])
                item_y_start = max(0, topleft[1])
                item_x_end = min(item_x_start + item_img.shape[1], self.blocksize)
                item_y_end = min(item_y_start + item_img.shape[0], self.blocksize)

                # Check for valid indices
                if item_y_start < self.blocksize and item_x_start < self.blocksize:
                    if isinstance(item, House):
                        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 5  # House adds 5°C
                    elif isinstance(item, Tree):
                        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 2  # Tree adds 2°C
                    elif isinstance(item, Road):
                        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 1  # Road adds 1°C

            # Ensure the thermal view indices are valid
            if ry_start + self.blocksize <= thermal_view.shape[0] and cx_start + self.blocksize <= thermal_view.shape[1]:
                thermal_view[ry_start:ry_start + self.blocksize, cx_start:cx_start + self.blocksize] += block_temp
```

Menghasilkan representasi suhu map dalam format thermal view, dengan suhu dasar yang dapat disesuaikan.

Langkah-langkah:
1.	Inisialisasi grid suhu
    ```thermal_view = np.ones((self.map_shape[0] * self.blocksize, self.map_shape[1] * self.blocksize)) * base_temp```
    Membuat numpy array dua dimensi yang berisi nilai suhu dasar (base_temp) untuk setiap piksel di dalam map.
2.	Looping melalui setiap block:
    ```python
    for block in self.blocks:
        cx_start, ry_start = block.topleft
        block_temp = np.ones((self.blocksize, self.blocksize)) * base_temp  
    ```
3. Looping melalui setiap block di map:
    Untuk setiap block, inisialisasi array dua dimensi block_temp dengan suhu dasar (base_temp) yang merepresentasikan suhu di dalam block.
    
4. Menerapkan efek suhu berdasarkan objek dalam block:
    ```python
    for item in block.items:
        item_img = item.get_image()
        topleft = item.get_topleft()
        item_x_start = max(0, topleft[0])
        item_y_start = max(0, topleft[1])
        item_x_end = min(item_x_start + item_img.shape[1], self.blocksize)
        item_y_end = min(item_y_start + item_img.shape[0], self.blocksize)
    ```

    Looping melalui setiap objek di dalam block:
    - ```item.get_image()```: Mendapatkan gambar dari objek (misalnya house, tree, atau road).
    - ```item.get_topleft()```: Mendapatkan koordinat atas-kiri dari objek di dalam block.
    - Menentukan posisi objek: Menghitung koordinat awal dan akhir dari objek di grid block.

5. Meningkatkan suhu berdasarkan objek:
    ```python
    if isinstance(item, House):
        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 5
    elif isinstance(item, Tree):
        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 2
    elif isinstance(item, Road):
        block_temp[item_y_start:item_y_end, item_x_start:item_x_end] += 1
    ```
    - Jika objek adalah house, suhu di area tersebut dinaikkan 5°C.
    - Jika objek adalah tree, suhu dinaikkan 2°C.
    - Jika objek adalah road, suhu dinaikkan 1°C.

6.	Mengisi suhu block ke dalam map suhu:
```thermal_view[ry_start:ry_start + self.blocksize, cx_start:cx_start + self.blocksize] += block_temp```
    Menambahkan nilai suhu lokal dari block_temp ke area yang sesuai di thermal_view berdasarkan posisi topleft block.

7.	Mengembalikan hasil:
    ```return thermal_view```
    Setelah seluruh block diproses dan suhu diperbarui, fungsi mengembalikan thermal_view, yaitu representasi suhu dari map.


# Fungsi simulation_loop
```python
def simulation_loop(map_obj, steps=24):
    for step in range(steps):
        if step < 8:  # Early morning, cool temperatures (11-15°C)
            base_temp = 11 + (step * (15 - 11) / 8)
        elif step < 12:  # Midday, peak temperatures (15-24°C)
            base_temp = 15 + (step - 8) * (24 - 15) / 4
        elif step < 17:  # Afternoon, decreasing temperature (24-18°C)
            base_temp = 24 - (step - 12) * (24 - 18) / 5
        else:  # Evening/night, cool down to 11°C (18-11°C)
            base_temp = 18 - (step - 17) * (18 - 11) / 7

        print(f"Simulation Step {step + 1}, Base Temperature: {base_temp:.2f}°C")
        thermal_view = map_obj.generate_thermal_view(base_temp=base_temp)

        # Create a new figure for each simulation step
        fig, ax = plt.subplots(1, 2, figsize=(12, 6))

        # Plot RGB View
        img_rgb = ax[0].imshow(map_obj.generate_rgb_view(), vmin=0, vmax=20)
        ax[0].set_title("RGB View")
        fig.colorbar(img_rgb, ax=ax[0])

        # Plot Thermal View
        img_thermal = ax[1].imshow(thermal_view, cmap="hot", vmin=0, vmax=50)
        ax[1].set_title(f"Thermal View at Step {step + 1}")
        fig.colorbar(img_thermal, ax=ax[1])

        plt.tight_layout()
        plt.show()
```

Fungsi simulation_loop() digunakan untuk mensimulasikan perubahan suhu dan menampilkan visualisasi map dalam bentuk RGB View dan Thermal View pada setiap langkah waktu (step) yang telah ditentukan.
Fungsi ini berroad dalam loop, di mana setiap iterasi dari loop mewakili satu langkah waktu dalam sehari, dengan perubahan suhu yang terjadi sesuai dengan waktu tersebut (pagi, siang, sore, malam).

## Penjelasan Bagian Fungsi simulation_loop
Parameter
- ```map_obj```: Ini adalah objek dari kelas Map, yang berisi semua block dan item di dalam map. Map ini akan digunakan untuk menghasilkan tampilan visual (RGB) dan tampilan suhu (thermal).
- ```steps=24```: Menentukan jumlah langkah dalam simulasi, defaultnya adalah 24 langkah, yang bisa dianggap sebagai simulasi selama 24 jam (1 hari penuh).

1. Looping Melalui Langkah-Langkah Simulasi
    ```for step in range(steps)```:
    - ```for step in range(steps)```: Membuat loop untuk melakukan simulasi selama 24 langkah (atau sesuai dengan jumlah steps yang diberikan).
    - ```step``` akan menjadi indeks untuk setiap langkah simulasi, dimulai dari 0 hingga 23 (karena steps=24).

2. Menentukan Suhu Dasar (base_temp) untuk Setiap Waktu
    Di setiap langkah, suhu dasar (temperatur) berubah berdasarkan waktu simulasi yang dibagi menjadi 4 fase: pagi, siang, sore, dan malam. Setiap fase memiliki rentang suhu yang berbeda-beda.
    - Pagi *(Langkah 0-7, Suhu 11°C - 15°C)*:
        ```
        if step < 8:  
                Base_temp = 11 + (step * (15 - 11) / 8)
        ```
        a. ```if step < 8```: Untuk langkah 0 hingga 7, dianggap sebagai pagi hari dengan suhu dasar antara 11°C hingga 15°C.
        b. ```base_temp = 11 + (step * (15 - 11) / 8)```: Menghitung suhu dasar secara linear dari 11°C ke 15°C selama 8 langkah.
    - Siang (Langkah 8-11, Suhu 15°C - 24°C)
        ```
        elif step < 12:  
            base_temp = 15 + (step - 8) * (24 - 15) / 4
        ```
        - ```elif step < 12```: Untuk langkah 8 hingga 11, dianggap sebagai waktu siang dengan suhu dasar antara 15°C hingga 24°C.
        - ```base_temp = 15 + (step - 8) * (24 - 15) / 4```: Suhu meningkat secara linear dari 15°C ke 24°C selama 4 langkah (siang).

    - Sore (Langkah 12-16, Suhu 24°C - 18°C)
        ```python
        elif step < 17:  
           base_temp = 24 - (step - 12) * (24 - 18) / 5
        ```
        a. elif step < 17: Langkah 12 hingga 16 adalah waktu sore dengan suhu menurun dari 24°C ke 18°C.
        b. base_temp = 24 - (step - 12) * (24 - 18) / 5: Suhu berangsur-angsur turun selama 5 langkah.
    - Malam (Langkah 17-23, Suhu 18°C - 11°C)
        ```
        else:  
            base_temp = 18 - (step - 17) * (18 - 11) / 7
        ```
        a. Langkah 17 hingga 23 dianggap sebagai malam hari, dengan suhu menurun dari 18°C ke 11°C.
        b. Suhu turun secara bertahap selama 7 langkah malam.

3. Cetak Informasi Suhu
    ```print(f"Simulation Step {step + 1}, Base Temperature: {base_temp:.2f}°C")```
    Ini mencetak informasi ke konsol tentang langkah simulasi saat ini dan suhu dasar yang digunakan dalam langkah tersebut. base_temp akan dicetak dengan 2 angka desimal.

4. Menghasilkan Tampilan Thermal
    ```thermal_view = map_obj.generate_thermal_view(base_temp=base_temp)```
    Fungsi generate_thermal_view(base_temp) digunakan untuk menghasilkan tampilan suhu (thermal view) berdasarkan suhu dasar yang telah dihitung. Ini menggunakan objek map map_obj untuk menghitung pengaruh setiap item (seperti house, tree, road) terhadap suhu.
    Suhu dasar akan ditambahkan dengan efek suhu dari item, misalnya:
    - House menambah 5°C.
    - Tree menambah 2°C.
    - Road menambah 1°C.

5. Membuat Gambar Visualisasi (Plotting)
    Fungsi ini kemudian menampilkan dua plot: RGB View dan Thermal View.
    - Membuat Layout untuk Gambar
    ```python
    fig, ax = plt.subplots(1, 2, figsize=(12, 6))
    ```
    plt.subplots(1, 2): Membuat dua area plot dalam satu baris.
    figsize=(12, 6): Mengatur ukuran gambar menjadi 12 unit lebar dan 6 unit tinggi.
    - Plotting RGB View
        ```
        img_rgb = ax[0].imshow(map_obj.generate_rgb_view(),vmin=0, vmax=20)
        ax[0].set_title("RGB View")
        fig.colorbar(img_rgb, ax=ax[0])
        ```
        
        a. generate_rgb_view(): Menghasilkan tampilan RGB dari map, di mana warna-warna digunakan untuk merepresentasikan item seperti house, tree, road, dan rumput.
        b. imshow(): Menampilkan tampilan RGB di area plot pertama (ax[0]).
        c. colorbar(): Menambahkan legenda warna di samping tampilan untuk memperlihatkan rentang warna yang digunakan.

6. Plotting Thermal View
    ```python
    img_thermal = ax[1].imshow(thermal_view, cmap="hot", vmin=0, vmax=50)
    ax[1].set_title(f"Thermal View at Step {step + 1}")
    fig.colorbar(img_thermal, ax=ax[1])
    ```
    - ```thermal_view```: Menampilkan tampilan thermal (suhu) dari map.
    - ```imshow(..., cmap="hot")```: Menampilkan tampilan suhu dengan menggunakan palet warna "hot", yang menampilkan perbedaan suhu dengan warna merah/oranye.
    - ```vmin=0```, ```vmax=50```: Menetapkan skala warna untuk tampilan suhu dari 0°C hingga 50°C.
    - ```set_title()```: Memberikan judul untuk plot thermal, termasuk informasi langkah simulasi yang sedang ditampilkan.

7. Menyusun dan Menampilkan Plot
    ```python
    plt.tight_layout()
    plt.show()
    ```
    - ```tight_layout()```: Mengatur tata letak gambar agar rapi dan tidak ada elemen yang bertumpuk.
    - ```show()```: Menampilkan kedua plot secara bersamaan (RGB View dan Thermal View) pada layar

# Fungsi Main
```python
def main():
    blocksize = 120
    map_shape = (1, 1)

    map_obj = Map(map_shape, blocksize)

    # User input for number of items
    num_trees = int(input("Enter the number of trees to spawn: "))
    num_houses = int(input("Enter the number of houses to spawn: "))
    num_roads = int(input("Enter the number of roads to spawn: "))

    tree_coords = []
    house_coords = []
    road_coords = []

    # Input coordinates for trees, houses, and roads with validation
    for i in range(num_trees):
        x, y = map(int, input(f"Enter x, y coordinates for Tree {i + 1} (comma-separated): ").split(","))
        tree_coords.append((x, y))

    for i in range(num_houses):
        x, y = map(int, input(f"Enter x, y coordinates for House {i + 1} (comma-separated): ").split(","))
        house_coords.append((x, y))

    for i in range(num_roads):
        x, y = map(int, input(f"Enter x, y coordinates for Road {i + 1} (comma-separated): ").split(","))
        road_coords.append((x, y))

    # Add items to the map
    for block in map_obj.blocks:
        for coord in tree_coords:
            new_tree = Tree(coord)
            if not block.check_overlap(new_tree):  # Check for overlap
                block.add_item(new_tree)

        for coord in house_coords:
            new_house = House(coord)
            if not block.check_overlap(new_house):  # Check for overlap
                block.add_item(new_house)

        for coord in road_coords:
            new_road = Road(coord, blocksize)
            if not block.check_overlap(new_road):  # Check for overlap
                block.add_item(new_road)

    # Run the simulation loop
    simulation_loop(map_obj)

if __name__ == "__main__":
    main()

```
Fungsi ```main()```  adalah pusat dari program yang mengatur alur simulasi pembuatan map. Pengguna diminta untuk memasukkan jumlah dan posisi item (tree, house, road), lalu item tersebut ditempatkan di map jika tidak ada tumpang tindih (overlap) antar item. Setelah itu, program menroadkan simulasi suhu dan menampilkan map secara visual

## Penjelasan bagian-bagian fungsi Main()
1. Inisialisasi Variabel blocksize dan map_shape:
    ```python
    blocksize = 120
    map_shape = (1, 1)
    ```
    - ```blocksize = 120```: Mengatur ukuran block atau grid di dalam map. Setiap block akan memiliki ukuran 120x120 piksel.
    - ```map_shape = (1, 1)```: Mengatur bentuk map yang berupa matriks 2D. Dalam hal ini, map terdiri dari 1 baris dan 1 kolom, sehingga hanya ada 1 block pada map.
2. Membuat Objek Map:
    ```python
    map_obj = Map(map_shape, blocksize)
    ```
    Membuat sebuah objek dari class Map dengan bentuk map (map_shape) dan ukuran block (blocksize). Objek Map ini akan menampung block-block dan item (seperti tree, house, dan road) yang akan digambar di map.
3. Menerima Input dari Pengguna:
    ```python
    num_trees = int(input("Enter the number of trees to spawn: "))
    num_houses = int(input("Enter the number of houses to spawn: "))
    num_roads = int(input("Enter the number of roads to spawn: "))
    ```
    - ```num_trees```: Jumlah tree yang akan ditambahkan di map.
    - ```num_houses```: Jumlah house yang akan ditambahkan di map.
    - ```num_roads```: Jumlah road yang akan ditambahkan di map.
4. Mendefinisikan Koordinat untuk Tree, House, dan Road:
    ```python
    tree_coords = []
    house_coords = []
    road_coords = []
    ```
    ```tree_coords```, ```house_coords```, dan ```road_coords```: List untuk menyimpan koordinat yang akan diberikan oleh pengguna, di mana item-item tersebut akan ditempatkan di map.
5. Menerima Input Koordinat dari Pengguna:
    Pengguna akan memberikan koordinat ```(x, y)``` untuk setiap tree, house, dan road yang akan digambar pada map.
    - Koordinat untuk tree:
        ```python
        for i in range(num_trees):
        x, y = map(int, input(f"Enter x, y coordinates for Tree {i + 1} (comma-separated): ").split(","))
        tree_coords.append((x, y))
        ```
    - Koordinat untuk House:
        ```python
        for i in range(num_houses):
        x, y = map(int, input(f"Enter x, y coordinates for House {i + 1} (comma-separated): ").split(","))
        house_coords.append((x, y))
        ```
        Pengguna memasukkan koordinat (x, y) untuk setiap house, dan koordinatnya disimpan dalam ```house_coords```.
    - Koordinat untuk Road:
        ```python
        for i in range(num_roads):
        x, y = map(int, input(f"Enter x, y coordinates for Road {i + 1} (comma-separated): ").split(","))
        road_coords.append((x, y))
        ```
        Pengguna memasukkan koordinat ```(x, y)``` untuk setiap road, dan disimpan dalam ```road_coords```.


6. Menambahkan Item ke dalam Block di Map:
    Tree, house, dan road ditambahkan ke dalam block map dengan memeriksa apakah ada overlap (tumpang tindih) antar item atau tidak.
    - Menambahkan Tree
        ```python
            for block in map_obj.blocks:
                for coord in tree_coords:
                    new_tree = Tree(coord)
                    if not block.check_overlap(new_tree):  # Check for overlap
                        block.add_item(new_tree)
        ```
        Membuat objek Tree untuk setiap koordinat yang diberikan pengguna. Fungsi ```check_overlap()``` digunakan untuk memeriksa apakah item tree bertumpang tindih dengan item lain di block. Jika tidak bertumpang tindih, item ditambahkan ke block dengan ```add_item()```.
        
    - Menambahkan House:
        ```python
            for coord in house_coords:
                new_house = House(coord)
                if not block.check_overlap(new_house):  # Check for overlap
                    block.add_item(new_house)
        ```
        Sama seperti tree, house juga ditambahkan ke block jika tidak tumpang tindih.

7. Menroadkan Simulasi:
    ```python
    simulation_loop(map_obj, steps=24)
    ```
    Setelah semua item ditambahkan, ```simulation_loop()``` diroadkan. Fungsi ini akan menampilkan simulasi map dalam 24 langkah waktu (24 jam), dengan menunjukkan bagaimana suhu dasar (base temperature) berubah sepanjang hari.
8. Memastikan Fungsi main() Diroadkan:
    ```python
    if __name__ == "__main__":
        main()
    ```
    Bagian ini memastikan bahwa fungsi ```main()``` diroadkan ketika file diroadkan sebagai script, menginisialisasi proses input pengguna dan menroadkan simulasi map.


List error:
1. Bug Pertama
jam tidak dibatasi
klarifikasi:
simulasinya hanya untuk dibawah 24 jam
2. Bug kedua
kondisi untuk mengecek koordinat tidak berroad sehingga program tetap berroad
3.
