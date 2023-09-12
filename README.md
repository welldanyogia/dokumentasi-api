
# API Daftar Harga

API Daftar Harga digunakan untuk mengambil informasi daftar harga dari Digiflazz dan menyimpannya ke dalam database.

## Daftar Isi

- [Endpoint](#endpoint)
- [Permintaan](#permintaan)
  - [Contoh Permintaan](#contoh-permintaan)
  - [Deskripsi Parameter Permintaan](#deskripsi-parameter-permintaan)
- [Respons Daftar Harga Pulsa Prepaid](#respons-daftar-harga-pulsa-prepaid)
  - [Contoh Respons](#contoh-respons)
  - [Deskripsi Parameter Respons](#deskripsi-parameter-respons)
- [Respons Daftar Harga Pasca](#respons-daftar-harga-pasca)
  - [Contoh Respons](#contoh-respons)
  - [Deskripsi Parameter Respons](#deskripsi-parameter-respons)
- [Perhatian](#perhatian)

## Endpoint

- **URL**: `https://api.digiflazz.com/v1/price-list`

## Permintaan

### Contoh Permintaan

Berikut adalah contoh struktur JSON yang harus disertakan dalam permintaan:

```json
{
  "cmd": "prepaid",
  "username": "username",
  "sign": "740b00a1b8784e028cc8078edf66d12b"
}
```

### Deskripsi Parameter Permintaan

- `cmd` (String, Wajib): Command, bisa berupa "prepaid" atau "pasca".
- `username` (String, Wajib): Nama pengguna yang telah diatur di pengaturan koneksi API.
- `sign` (String, Wajib): Tanda tangan dengan rumus md5(username + apiKey + "pricelist").

## Respons Daftar Harga Pulsa Prepaid

### Contoh Respons

Berikut adalah contoh JSON yang akan Anda terima setelah mengirim permintaan:

```json
{
  "data": [
    {
      "product_name": "Xl 100.000",
      "category": "Pulsa",
      "brand": "XL",
      "type": "Umum",
      "seller_name": "PT. ABC",
      "price": 98000,
      "buyer_sku_code": "X100",
      "buyer_product_status": true,
      "seller_product_status": true,
      "unlimited_stock": true,
      "stock": 0,
      "multi": true,
      "start_cut_off": "23:45",
      "end_cut_off": "00:15",
      "desc": "Pulsa Xl Rp 100.000"
    },
    {
      "product_name": "Telkomsel Pulsa Transfer 5.000",
      "category": "Pulsa",
      "brand": "TELKOMSEL",
      "type": "Pulsa Transfer",
      "seller_name": "PT. BCA",
      "price": 5100,
      "buyer_sku_code": "S5",
      "buyer_product_status": true,
      "seller_product_status": false,
      "unlimited_stock": false,
      "stock": 1200,
      "multi": false,
      "start_cut_off": "",
      "end_cut_off": "",
      "desc": "Pulsa Telkomsel Rp 5.000"
    }
  ]
}
```

### Deskripsi Parameter Respons

- `product_name` (String, Wajib): Nama produk.
- `category` (String, Wajib): Nama kategori.
- `brand` (String, Wajib): Nama brand.
- `type` (String, Wajib): Nama tipe.
- `seller_name` (String, Wajib): Nama seller.
- `price` (Int, Wajib): Harga produk yang ditentukan oleh seller.
- `buyer_sku_code` (String, Wajib): Kode produk yang disetting oleh Anda sebagai Buyer.
- `buyer_product_status` (Boolean, Wajib): Status produk Anda sebagai buyer.
- `seller_product_status` (Boolean, Wajib): Status produk Seller.
- `unlimited_stock` (Boolean, Wajib): Penentu apakah stok terbatas atau tidak.
- `stock` (Int, Wajib): Sisa stock seller (dapat diabaikan jika `unlimited_stock` bernilai true).
- `multi` (Boolean, Wajib): Transaksi dapat dilakukan lebih dari satu kali ke denom dan no tujuan yang sama dalam sehari.
- `start_cut_off` (String, Wajib): Jam mulai Cut Off (Format: hh:mm).
- `end_cut_off` (String, Wajib): Jam mulai Cut Off (Format: hh:mm).
- `desc` (String, Wajib): Deskripsi produk.

## Respons Daftar Harga Pasca

### Contoh Respons

Berikut adalah contoh JSON yang akan Anda terima setelah mengirim permintaan:

```json
{
  "data": [
    {
      "product_name": "Pln Postpaid",
      "category": "Pascabayar",
      "brand": "PLN",
      "seller_name": "PT. ABC",
      "admin": 2750,
      "commission": 1800,
      "buyer_sku_code": "pln",
      "buyer_product_status": true,
      "seller_product_status": true,
      "desc": "-"
    },
    {
      "product_name": "aetra",
      "category": "Pascabayar",
      "brand": "PDAM",
      "seller_name": "Mr. Ed",
      "admin": 2000,
      "commission": 550,
      "buyer_sku_code": "aetra",
      "buyer_product_status": true,
      "seller_product_status": true,
      "desc": "Provinsi Jakarta"
    }
  ]
}
```

### Deskripsi Parameter Respons

- `product_name` (String, Wajib): Nama produk.
- `category` (String, Wajib): Nama kategori.
- `brand` (String, Wajib): Nama brand.
- `seller_name` (String, Wajib): Nama seller.
- `admin` (Int, Wajib): Biaya admin.
- `commission` (Int, Wajib): Biaya komisi yang akan didapatkan Buyer.
- `buyer_sku_code` (String, Wajib): Kode produk yang disetting oleh Anda sebagai Buyer.
- `buyer_product_status` (Boolean, Wajib): Status produk Anda sebagai buyer.
- `seller_product_status` (Boolean, Wajib): Status produk Seller.
- `desc` (String, Wajib): Deskripsi produk.

## Perhatian

- Response JSON akan di bungkus oleh variabel `data`, pastikan Anda melakukan parsing
