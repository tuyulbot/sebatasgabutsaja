
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


