## Data Analysis for E-Commerce Challenge

----

#### Sample of Dataset project

<details>
<summary markdown="span">users</summary>

| user_id | nama_user                | kodepos | email                       |
|---------|--------------------------|---------|-----------------------------|
|       1 | Ir. Paris Siregar, S.Sos | 20412   | dadapsamosir@hotmail.com    |
|       2 | Oliva Zulkarnain         | 37034   | permadiputri@pt.mil.id      |
|       3 | Latika Mustofa           | 02728   | caturanggriawan@pd.go.id    |
|       4 | Elvina Rahmawati         | 00470   | varyani@pd.ac.id            |
|       5 | Tedi Irawan              | 39756   | latuponodaliono@hotmail.com |

</details>

<details>
<summary markdown="span">products</summary>

| product_id | desc_product               | category       | base_price |
|------------|----------------------------|----------------|------------|
|          1 | OLIVIA KULOT OLV03         | Pakaian Wanita |     110000 |
|          2 | BLANIK BLOUSE BL304        | Pakaian Wanita |     100000 |
|          3 | NEW DAY BY RIX DRESS ND01  | Pakaian Wanita |      85000 |
|          4 | BLANIK BLOUSE BL023        | Pakaian Wanita |      85000 |
|          5 | BLANIK BLAZER BL031        | Pakaian Wanita |      99000 |

</details>

<details>
<summary markdown="span">orders</summary>

| order_id | seller_id | buyer_id | kodepos | subtotal | discount | total   | created_at          | paid_at    | delivery_at |
|----------|-----------|----------|---------|----------|----------|---------|---------------------|------------|-------------|
|        3 |         5 |     4769 | 32610   |   900000 |        0 |  900000 | 2019-06-01 00:00:00 | 2019-06-04 | 2019-06-12  |
|        5 |        23 |     4276 | 2674    |   220000 |        0 |  220000 | 2019-04-02 00:00:00 | 2019-04-05 | 2019-04-09  |
|        8 |         4 |    14110 | 48577   |  1248000 |        0 | 1248000 | 2019-08-02 00:00:00 | 2019-08-13 | 2019-08-20  |
|       19 |         5 |     3831 | 91235   |  1074000 |        0 | 1074000 | 2020-05-16 00:00:00 | NA         | NA          |
|       31 |        46 |     5318 | 96740   |   253000 |        0 |  253000 | 2019-03-12 00:00:00 | 2019-03-17 | 2019-03-20  |

</details>

<details>
<summary markdown="span">order_details</summary>

| order_detail_id | order_id | product_id | price | quantity |
|-----------------|----------|------------|-------|----------|
|               5 |        3 |        907 | 25000 |       36 |
|               9 |        5 |        562 | 10000 |       22 |
|              15 |        8 |        645 | 39000 |       32 |
|              48 |       19 |        287 | 22000 |       12 |
|              49 |       19 |        201 | 26000 |       27 |

</details>

----

#### 10 Transaksi terbesar user 12476
Lengkapi kode SQL berikut ini agar menampilkan 10 transaksi dari pembelian dari pengguna dengan user_id 12476, urutkan dari nilai transaksi paling besar. Tampilkan variabel seller_id, buyer_id, nilai_transaksi, dan tanggal_transaksi.

```sql
SELECT
  seller_id, 
  buyer_id, 
  total AS nilai_transaksi, 
  created_at AS tanggal_transaksi
FROM 
  orders
WHERE 
  buyer_id = 12476
ORDER BY 
  3 
  DESC
LIMIT 
  10;
```

<details>
<summary markdown="span">OUTPUT :</summary>

| seller_id | buyer_id | nilai_transaksi | tanggal_transaksi   |
|-----------|----------|-----------------|---------------------|
|        61 |    12476 |        12014000 | 2019-12-23 00:00:00 |
|        53 |    12476 |         9436000 | 2019-12-05 00:00:00 |
|        64 |    12476 |         4951000 | 2019-12-19 00:00:00 |
|        57 |    12476 |         4854000 | 2019-12-01 00:00:00 |
|        22 |    12476 |         4010000 | 2019-11-29 00:00:00 |
|        48 |    12476 |         1440000 | 2020-02-27 00:00:00 |
|        61 |    12476 |         1053000 | 2019-10-17 00:00:00 |
|        35 |    12476 |          816000 | 2020-05-12 00:00:00 |
|        60 |    12476 |          740000 | 2019-09-26 00:00:00 |
|         3 |    12476 |          399000 | 2019-09-26 00:00:00 |

</details>

----

#### Transaksi per bulan
Lengkapi kode SQL berikut ini agar menampilkan summary transaksi per bulan di tahun 2020.  

```sql
SELECT 
  EXTRACT(YEAR_MONTH FROM created_at) AS tahun_bulan, 
  count(1) AS jumlah_transaksi, 
  SUM(total) AS total_nilai_transaksi
FROM 
  orders
WHERE 
  created_at>='2020-01-01'
GROUP BY 1
ORDER BY 1;
```

<details>
<summary markdown="span">OUTPUT :</summary>

| tahun_bulan | jumlah_transaksi | total_nilai_transaksi |
|-------------|------------------|-----------------------|
|      202001 |             5062 |            9941756800 |
|      202002 |             5872 |           12665113550 |
|      202003 |             7323 |           17189378400 |
|      202004 |             7955 |           21219233750 |
|      202005 |            10026 |           31288823000 |

</details>

----

#### Pengguna dengan rata-rata transaksi terbesar di Januari 2020
Lengkapi kode SQL berikut ini agar menampilkan 10 pembeli dengan rata-rata nilai transaksi terbesar yang bertransaksi minimal 2 kali di Januari 2020. Tampilkan variabel buyer_id, jumlah_transaksi, dan avg_nilai_transaksi.

```sql
SELECT 
  buyer_id, 
  COUNT(1) AS jumlah_transaksi, 
  AVG(total) AS avg_nilai_transaksi
FROM 
  orders
WHERE 
  created_at>='2020-01-01' AND created_at<'2020-02-01'
GROUP BY 1
HAVING 
  COUNT(1)>=2
ORDER BY 3 DESC
LIMIT 10
```

<details>
<summary markdown="span">OUTPUT :</summary>

| buyer_id | jumlah_transaksi | avg_nilai_transaksi |
|----------|------------------|---------------------|
|    11140 |                2 |       11719500.0000 |
|     7905 |                2 |       10440000.0000 |
|    12935 |                2 |        8556500.0000 |
|    12916 |                2 |        7747000.0000 |
|    17282 |                2 |        6797500.0000 |
|     1418 |                2 |        6741000.0000 |
|     5418 |                2 |        5336000.0000 |
|    11906 |                2 |        5309500.0000 |
|    12533 |                2 |        5218500.0000 |
|      841 |                2 |        5052500.0000 |

</details>

----

#### Transaksi besar di Desember 2019

Lengkapi kode SQL berikut ini agar menampilkan semua nilai transaksi minimal 20,000,000 di bulan Desember 2019, tampilkan nama_pembeli, nilai transaksi dan tanggal_transaksi, urutkan sesuai abjad pembeli.

```sql
SELECT
  nama_user AS nama_pembeli, 
  total AS nilai_transaksi, 
  created_at AS tanggal_transaksi
FROM
  orders
INNER JOIN
  users ON buyer_id = user_id
WHERE 
  created_at>='2019-12-01' 
  AND created_at<'2020-01-01'
  AND total >=20000000
ORDER BY 1;
```

<details>
<summary markdown="span">OUTPUT :</summary>

| nama_pembeli                  | nilai_transaksi | tanggal_transaksi   |
|-------------------------------|-----------------|---------------------|
| Diah Mahendra                 |        21142000 | 2019-12-24 00:00:00 |
| Dian Winarsih                 |        22966000 | 2019-12-21 00:00:00 |
| dr. Yulia Waskita             |        29930000 | 2019-12-28 00:00:00 |
| drg. Kajen Siregar            |        27893500 | 2019-12-10 00:00:00 |
| Drs. Ayu Lailasari            |        22300000 | 2019-12-09 00:00:00 |
| Hendri Habibi                 |        21815000 | 2019-12-19 00:00:00 |
| Kartika Habibi                |        25760000 | 2019-12-22 00:00:00 |
| Lasmanto Natsir               |        22845000 | 2019-12-27 00:00:00 |
| R.A. Betania Suryono          |        20523000 | 2019-12-07 00:00:00 |
| Syahrini Tarihoran            |        29631000 | 2019-12-05 00:00:00 |
| Tgk. Hamima Sihombing, M.Kom. |        29351400 | 2019-12-25 00:00:00 |
| Tgk. Lidya Lazuardi, S.Pt     |        20447000 | 2019-12-16 00:00:00 |

</details>

----

#### Kategori Produk Terlaris di 2020

Lengkapi kode SQL berikut ini agar menampilkan 5 Kategori dengan total quantity terbanyak di tahun 2020, hanya untuk transaksi yang sudah terkirim ke pembeli. Tampilkan category, total_quantity, total_price.

```sql
SELECT
  category, 
  SUM(quantity) AS total_quantity, 
  SUM(price) AS total_price
FROM 
  orders
INNER JOIN order_details USING(order_id)
INNER JOIN products USING(product_id)
WHERE 
  created_at>='2020-01-01'
  AND delivery_at is not null
GROUP BY 1
ORDER BY 2 desc
LIMIT 5;
```

<details>
<summary markdown="span">OUTPUT :</summary>

| category        | total_quantity | total_price |
|-----------------|----------------|-------------|
| Kebersihan Diri |         944018 |  1333153000 |
| Fresh Food      |         298372 |   793756000 |
| Makanan Instan  |         280481 |    67868000 |
| Bahan Makanan   |         218151 |   120563000 |
| Minuman Ringan  |         212103 |    63017000 |

</details>

























