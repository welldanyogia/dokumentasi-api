# Dokumentasi API Laravel

Dokumentasi ini menjelaskan API Laravel yang digunakan untuk mengambil daftar harga dari endpoint eksternal dan menyimpan respons produk ke dalam database.

## Endpoint

- Base URL: `https://example.com/api`

### Mengambil Daftar Harga

- **Endpoint**: `/fetch-price-list`
- **Metode**: POST
- **Deskripsi**: Mengambil daftar harga dari endpoint eksternal dan menyimpannya ke dalam database.

#### Permintaan (Request)

Contoh JSON permintaan:

```json
{
  "cmd": "prepaid",
  "username": "username",
  "sign": "740b00a1b8784e028cc8078edf66d12b"
}
```

| Parameter   | Deskripsi                              | Tipe Data | Wajib |
|-------------|----------------------------------------|-----------|-------|
| cmd         | Command: prepaid atau pasca           | String    | Ya    |
| username    | Username yang telah diatur di pengaturan koneksi API | String | Ya    |
| sign        | Signature dengan formula md5(username + apiKey + "pricelist") | String | Ya    |

#### Respons (Response)

Contoh JSON respons:

```json
{
  "message": "Data has been fetched and stored."
}
```

#### Kesalahan (Errors)

- `404 Not Found`: Endpoint tidak ditemukan.
- `500 Internal Server Error`: Kesalahan server saat mengambil atau menyimpan data.

## Model Data Produk

Model data produk yang disimpan dalam database:

- `product_name`: Nama produk
- `category`: Nama kategori
- `brand`: Nama brand
- `seller_name`: Nama seller
- `price`: Harga produk yang ditentukan oleh seller
- `buyer_sku_code`: Kode produk yang disetting oleh Anda sebagai Buyer
- `buyer_product_status`: Status produk Anda sebagai buyer
- `seller_product_status`: Status produk Seller
- `unlimited_stock`: Penentu apakah stok terbatas atau tidak
- `stock`: Sisa stock seller (dapat diabaikan jika `unlimited_stock` bernilai true)
- `multi`: Transaksi dapat dilakukan lebih dari satu kali ke denom dan no tujuan yang sama dalam sehari
- `start_cut_off`: Jam mulai Cut Off (Format: hh:mm)
- `end_cut_off`: Jam mulai Cut Off (Format: hh:mm)
- `desc`: Deskripsi produk

## Contoh Penggunaan

### Mengambil Daftar Harga

```bash
POST https://example.com/api/fetch-price-list
```

Contoh permintaan:

```json
{
  "cmd": "prepaid",
  "username": "username",
  "sign": "740b00a1b8784e028cc8078edf66d12b"
}
```

Contoh respons:

```json
{
  "message": "Data has been fetched and stored."
}
```

## Catatan

- Pastikan Anda telah mengganti nilai "username" dan "your-api-key" dengan nilai yang sesuai dengan akun Anda pada endpoint Digiflazz.
- Selalu tangani kesalahan dengan baik dalam kode Anda untuk mengatasi masalah seperti kesalahan jaringan atau validasi permintaan.
```

Dokumentasi ini hanya merupakan contoh. Anda harus menyesuaikan dokumen ini dengan rincian dan kebutuhan spesifik dari API Anda. Pastikan untuk menjelaskan dengan jelas cara menggunakan endpoint, parameter yang diperlukan, respons yang diharapkan, serta kemungkinan kesalahan yang dapat terjadi.
