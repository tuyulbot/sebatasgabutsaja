
# Dokumentasi API Mutasi Orkut
**Deskripsi:** Tidak ada data yang di simpan sama sekali!!!!

> **Base URL:** `https://api.hidepulsa.com`

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
curl -X POST https://api.hidepulsa.com/minta-otp \
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
curl -X POST https://api.hidepulsa.com/valid-otp \
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

### Contoh Curl

```bash
curl -X POST https://api.hidepulsa.com/mutasi \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "merchant_id": "merchant code tnpa OK",
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login"
  }'
```

---

## 🧾 Endpoint: `/kasir/orkut/generate`

**Deskripsi:** Generate QRIS dan dapatkan URL gambar QR.

- **Method:** POST

### Payload

| Field         | Tipe   | Keterangan              |
|---------------|--------|--------------------------|
| auth_username | string | Username akun            |
| auth_token    | string | Token hasil login        |
| merchant      | string | Kode merchant (e.g. OK1234567) |
| nominal       | string | Nominal dalam satuan rupiah |

### Contoh Curl

```bash
curl -X POST https://api.hidepulsa.com/kasir/orkut/generate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login",
    "merchant": "merchant code",
    "nominal": "1000"
  }'
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
| merchant      | string | Kode merchant        |
| nominal       | string | Nominal transaksi    |

### Contoh Curl

```bash
curl -X POST https://api.hidepulsa.com/kasir/orkut/status-pembayaran \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login",
    "merchant": "merchant code",
    "nominal": "1000"
  }'
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
| merchant      | string | Kode merchant      |

### Contoh Curl

```bash
curl -X POST https://api.hidepulsa.com/kasir/orkut/mutasi \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "auth_username": "username",
    "auth_token": "token yang di dapat saat login",
    "merchant": "merchant code"
  }'
```

---


