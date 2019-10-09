API Data Wilayah Indonesia
==========================

Repository ini berisi source code untuk generate (REST) API statis berisi data wilayah Indonesia
serta perintah untuk mendeploynya ke _static hosting_ [Github Page](https://pages.github.com/).

#### Apa yang dimaksud API statis? 

API statis adalah API yang _endpoint_-nya terdiri dari file statis.

#### Keuntungan API statis?

* Dapat dihosting pada _static file hosting_ seperti Github Page, Netlify, dsb.
* Proses lebih cepat karena tidak membutuhkan server-side scripting.

#### Bagaimana cara kerjanya?

* Daftar provinsi, kab/kota, kecamatan, kelurahan/desa disimpan pada folder data berupa file `csv`, agar mudah diedit.
* Kemudian script `generate.php` dijalankan. Script ini akan men-generate ribuan endpoint (file) kedalam folder `static/api`.
* API siap 'dihidangkan'.

#### Saya mau hosting di Github saya sendiri, bagaimana caranya?

* Fork repository ini. 
* Buka cmd/terminal.
* `git clone https://github.com/usernamekamu/api-wilayah-indonesia.git`.
* `echo "" > hello.txt`.
* `git add hello.txt`.
* `git push origin master`.
* Tunggu beberapa saat sampai _Github_ build _Github Page_ kamu.
* Buka URL `https://usernamekamu.github.io/api-wilayah-indonesia`.

## ENDPOINTS

#### Mengambil Daftar Provinsi

```
GET /api/provinces.json
```

Contoh Response:

```json
[
  {
    "id": "11",
    "name": "ACEH"
  },
  {
    "id": "12",
    "name": "SUMATERA UTARA"
  },
  {
    "id": "13",
    "name": "SUMATERA BARAT"
  },
  ...
]
```

#### Mengambil Daftar Kab/Kota pada Provinsi Tertentu

```
GET /api/regencies/{provinceId}.json
```

Contoh untuk mengambil daftar kab/kota di provinsi Aceh (ID = 11):

```
GET /api/regencies/11.json
```

Contoh Response:

```json
[
  {
    "id": "1101",
    "province_id": "11",
    "name": "KABUPATEN SIMEULUE"
  },
  {
    "id": "1102",
    "province_id": "11",
    "name": "KABUPATEN ACEH SINGKIL"
  },
  {
    "id": "1103",
    "province_id": "11",
    "name": "KABUPATEN ACEH SELATAN"
  },
  ...
]
```

#### Mengambil Daftar Kecamatan pada Kab/Kota Tertentu

```
GET /api/districts/{regencyId}.json
```

Contoh untuk mengambil daftar kecamatan di Aceh Selatan (ID = 1103):

```
GET /api/districts/1103.json
```

Contoh Response:

```json
[
  {
    "id": "1103010",
    "regency_id": "1103",
    "name": "TRUMON"
  },
  {
    "id": "1103011",
    "regency_id": "1103",
    "name": "TRUMON TIMUR"
  },
  {
    "id": "1103012",
    "regency_id": "1103",
    "name": "TRUMON TENGAH"
  },
  ...
]
```

#### Mengambil Daftar Kelurahan pada Kecamatan Tertentu

```
GET /api/villages/{districtId}.json
```

Contoh untuk mengambil daftar kelurahan di Trumon (ID = 1103010):

```
GET /api/villages/1103010.json
```

Contoh Response:

```json
[
  {
    "id": "1103010001",
    "district_id": "1103010",
    "name": "KUTA PADANG"
  },
  {
    "id": "1103010002",
    "district_id": "1103010",
    "name": "RAKET"
  },
  {
    "id": "1103010003",
    "district_id": "1103010",
    "name": "GAMPONG TENGAH"
  },
  ...
]
```

#### Mengambil Data Provinsi berdasarkan ID Provinsi

```
GET /api/province/{provinceId}.json
```

Contoh untuk mengambil data provinsi Aceh (ID = 11):

```
GET /api/province/11.json
```

Contoh Response:

```json
{
  "id": "11",
  "name": "ACEH"
}
```

#### Mengambil Data Kab/Kota berdasarkan ID Kab/Kota

```
GET /api/regency/{regencyId}.json
```

Contoh untuk mengambil data kabupaten Aceh Selatan (ID = 1103):

```
GET /api/regency/1103.json
```

Contoh Response:

```json
{
  "id": "1103",
  "province_id": "11",
  "name": "KABUPATEN ACEH SELATAN"
}
```

#### Mengambil Data Kecamatan berdasarkan ID Kecamatan

```
GET /api/district/{districtId}.json
```

Contoh untuk mengambil data kecamatan Trumon Timur (ID = 1103011):

```
GET /api/district/1103011.json
```

Contoh Response:

```json
{
  "id": "1103011",
  "regency_id": "1103",
  "name": "TRUMON TIMUR"
}
```

#### Mengambil Data Kelurahan berdasarkan ID Kelurahan

```
GET /api/village/{villageId}.json
```

Contoh untuk mengambil data kelurahan Jambo Dalem (ID = 1103011010):

```
GET /api/village/1103011010.json
```

Contoh Response:

```json
{
  "id": "1103011010",
  "district_id": "1103011",
  "name": "JAMBO DALEM"
}
```
