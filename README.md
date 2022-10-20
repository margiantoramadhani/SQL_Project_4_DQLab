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

####












































