
# Dokumentasi API Mutasi Orkut UNOFFICIAL
**NOTED!!! :** Tidak ada data yang di simpan sama sekali!!!!

> **Base URL:** `https://orkut.hidepulsa.com`

---

## 🔐 Autentikasi

Semua endpoint membutuhkan `Authorization` header dengan format:

```
Authorization: Bearer YOUR_API_KEY
```

---

## 📬 Endpoint: `/minta-otp`

**Deskripsi:** Meminta kode OTP untuk login.

- **Method:** POST

### Payload

| Field    | Tipe    | Keterangan         |
|----------|---------|--------------------|
| username | string  | Username akun      |
| password | string  | Password akun      |

### Contoh Curl

```bash
curl -X POST https://orkut.hidepulsa.com/minta-otp \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"username": "username", "password": "44421"}'
```

---

## ✅ Endpoint: `/valid-otp`

**Deskripsi:** Validasi OTP dan dapatkan token.

- **Method:** POST

### Payload

| Field    | Tipe   | Keterangan                     |
|----------|--------|--------------------------------|
| username | string | Username akun                  |
| otp      | string | Kode OTP (sebagai password)    |

### Contoh Curl

```bash
curl -X POST https://orkut.hidepulsa.com/valid-otp \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"username": "username", "otp": "123456"}'
```

---

## 🧾 Endpoint: `/kasir/orkut/generate`

**Deskripsi:** Generate QRIS nominal wajib kasih kode unik dan dapatkan URL gambar QR.

- **Method:** POST

### Payload

| Field         | Tipe   | Keterangan              |
|---------------|--------|--------------------------|
| auth_username | string | Username akun            |
| auth_token    | string | Token hasil login        |
| merchant      | string | Kode merchant (e.g. OK1234567) |
| nominal       | string | Nominal + kode unik |

### Contoh Request

```bash
curl -X POST https://orkut.hidepulsa.com/kasir/orkut/generate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login",
    "merchant": "merchant code",
    "nominal": "1000"
  }'
```
### Contoh Respon Sukses
```json
{
  "success": true,
  "nominal": "1000",
  "image_url": "https://orkut.hidepulsa.com/static/......",
  "qr_string": "000201010212......"
}
```
### Contoh Respon Gagal
```json
{
  "error": "Gagal generate QRIS"
}
```
---

## 🔎 Endpoint: `/kasir/orkut/status-pembayaran`

**Deskripsi:** Cek status pembayaran QRIS yang telah digenerate.

- **Method:** POST

### Payload

| Field         | Tipe   | Keterangan           |
|---------------|--------|----------------------|
| auth_username | string | Username akun        |
| auth_token    | string | Token hasil login    |
| merchant      | string | Kode merchant (e.g. OK1234567)      |
| nominal       | string | Nominal + kode unik proses sebelomnya di generate    |

### Contoh Request

```bash
curl -X POST https://orkut.hidepulsa.com/kasir/orkut/status-pembayaran \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login",
    "merchant": "merchant code",
    "nominal": "1000"
  }'
```
### Contoh Respon Ditemukan Pembayaran
```json
{
  "status": "success",
  "data": [
    {
      "date": "2025-07-25 18:02:06",
      "amount": "500",
      "type": "CR",
      "qris": "static",
      "brand_name": "DANA",
      "issuer_reff": "015916474193",
      "buyer_reff": "NOBU / SO**********",
      "balance": "77777"
    }
  ]
}
```
### Contoh Respon Belum Ditemukan Pembayaran
```json
{
  "status": "success",
  "message": "no data"
}
```
---

## 📋 Endpoint: `/kasir/orkut/mutasi`

**Deskripsi:** Ambil histori mutasi QRIS langsung dari digital app.

- **Method:** POST

### Payload

| Field         | Tipe   | Keterangan         |
|---------------|--------|--------------------|
| auth_username | string | Username akun      |
| auth_token    | string | Token hasil login  |
| merchant      | string | Kode merchant (e.g. OK1234567)     |

### Contoh Request

```bash
curl -X POST https://orkut.hidepulsa.com/kasir/orkut/mutasi \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login",
    "merchant": "merchant code"
  }'
```
### Contoh Respon Sukses
```json
{
  "status": "success",
  "message": null,
  "data": [
    {
      "date": "2025-07-25 17:10:26",
      "amount": "1000",
      "type": "CR",
      "qris": "static",
      "brand_name": "DANA",
      "issuer_reff": "015841279721",
      "buyer_reff": "NOBU / SO*******************",
      "balance": "77777"
    }
  ],
  "merchant": "12455",
  "key": "f1455e7dccd6c464b79"
}
```
### Contoh Respon Gagal
```json
{
  "status": "success",
  "message": "no data",
  "data": null,
  "merchant": "12345",
  "key": "9f01b8324a"
}
```
---
## 💸 Endpoint: `/mutasi`

**Deskripsi:** Cek mutasi QRIS berdasarkan token.

- **Method:** POST

### Payload

| Field         | Tipe    | Keterangan                |
|---------------|---------|---------------------------|
| merchant_id   | string  | ID merchant (contoh: 1192690) |
| auth_username | string  | Username akun             |
| auth_token    | string  | Token hasil validasi OTP  |

### Contoh Request

```bash
curl -X POST https://orkut.hidepulsa.com/mutasi \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "merchant_id": "merchant code tnpa OK",
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login"
  }'
```
### Contoh Respon Sukses
```json
{
    "success": true,
    "qris_history": {
        "success": true,
        "total": 1,
        "page": 1,
        "pages": 1,
        "results": [
            {
                "id": 160644687,
                "debet": "0",
                "kredit": "500",
                "saldo_akhir": "77.777",
                "keterangan": "NOBU / SO**********",
                "tanggal": "25/07/2025 18:02",
                "status": "IN",
                "fee": "",
                "brand": {
                    "name": "DANA",
                    "logo": "https://app.orderkuota.com/assets/qris/dana.png"
                }
            }
        ]
    },
    "account": {
        "success": true,
        "results": {
            "id": 12345,
            "username": "sonzaix",
            "name": "sonzaix",
            "email": "sonzaix@gmail.com",
            "phone": "08123456789",
            "balance": 999999,
            "balance_str": "Rp 999.999",
            "qris_balance": 999999,
            "qris_balance_str": "Rp 999,999",
            "qrcode": "https://app.orderkuota.com/assets/qrcode/a38462faffc6437af67.png",
            "qris": "https://qris.orderkuota.com/qrnobu/2381492-8c8d7dd14-QR.png",
            "qris_name": "SONZAIX"
        }
    }
}
```
### Contoh Respon Gagal
```json
{
  "success": false,
  "message": "Fields tidak benar!"
}
```
---


