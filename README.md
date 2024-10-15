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
1. self.pose:
    - Tipe: Tuple (x, y)-
    - Fungsi: Menyimpan posisi pohon dalam bentuk koordinat (x, y) pada map. Posisi ini ditentukan saat pohon dibuat. Koordinat ini adalah titik pusat pohon.
2. self.size:
    - Tipe: Integer
    - Fungsi: Menyimpan ukuran dari pohon. Ukuran ini sudah ditentukan sebelumnya oleh variabel TREE_SIZE, yang nilainya diatur sebagai 10. Ukuran ini merupakan dimensi pohon dalam piksel, yaitu 10x10 piksel.
3. self .name:
    - Tipe: String
    - Fungsi: Menyimpan nama dari objek pohon, yaitu "Tree". Nama ini bisa digunakan untuk membedakan objek ini dari objek lain seperti rumah atau jalan.
4. self.age:
    - Tipe: Integer
    - Fungsi: Menyimpan usia pohon, yang ditentukan secara acak menggunakan fungsi random.randint(1, 100). Setiap pohon akan memiliki usia yang berbeda-beda di antara 1 hingga 100 tahun

```python
def get_image(self):
        img = np.ones((self.size, self.size)) * TREE_COLOR
        return img
```
1. get_image(self):
    Metode ini digunakan untuk menghasilkan representasi visual dari pohon dalam bentuk matriks numpy. Pohon akan ditampilkan sebagai matriks berukuran 10x10 (sesuai dengan TREE_SIZE) yang diisi dengan nilai warna tertentu.
