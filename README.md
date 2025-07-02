### 1. `users`
Digunakan untuk menyimpan data pelanggan yang mendaftar dan melakukan transaksi di toko online.

Kolom:
- `id_user`: ID unik untuk user (Primary Key)
- `nama`: Nama user
- `email`: Email user
- `password`: Password user (disarankan sudah dienkripsi)
- `alamat`: Alamat lengkap
- `no_hp`: Nomor handphone

### 2. `produk`
Menyimpan daftar produk yang dijual dalam toko online.

Kolom:
- `id_produk`: ID unik produk (Primary Key)
- `nama_produk`: Nama produk
- `deskripsi`: Deskripsi produk
- `harga`: Harga satuan
- `stok`: Jumlah stok tersedia
- `id_kategori`: Relasi ke tabel `kategori` (Foreign Key)

### 3. `kategori`
Menyimpan data kategori dari produk.

Kolom:
- `id_kategori`: ID unik kategori (Primary Key)
- `nama_kategori`: Nama kategori

### 4. `transaksi`
Mencatat setiap pembelian oleh user.

Kolom:
- `id_transaksi`: ID unik transaksi (Primary Key)
- `id_user`: Relasi ke user yang melakukan pembelian (Foreign Key)
- `tanggal_transaksi`: Tanggal pembelian
- `total`: Total harga keseluruhan
- `status_pembayaran`: Status pembayaran ('Belum Bayar' atau 'Sudah Bayar')

### 5. `detail_transaksi`
Berisi detail produk apa saja yang dibeli dalam satu transaksi.

Kolom:
- `id_detail`: ID unik detail transaksi (Primary Key)
- `id_transaksi`: Relasi ke `transaksi` (Foreign Key)
- `id_produk`: Relasi ke `produk` (Foreign Key)
- `jumlah`: Jumlah produk dibeli
- `harga_saat_transaksi`: Harga produk saat dibeli

### 6. `admin`
Menyimpan data admin yang mengelola sistem.

Kolom:
- `id_admin`: ID unik admin (Primary Key)
- `nama_admin`: Nama admin
- `email_admin`: Email admin
- `password_admin`: Password admin (disarankan sudah dienkripsi)


## Relasi dan Kardinalitas

1. **User – Transaksi**  
   One-to-Many: Satu user bisa melakukan banyak transaksi.  
   Relasi: `transaksi.id_user` → `users.id_user`

2. **Transaksi – Detail Transaksi**  
   One-to-Many: Satu transaksi memiliki banyak detail.  
   Relasi: `detail_transaksi.id_transaksi` → `transaksi.id_transaksi`

3. **Produk – Detail Transaksi**  
   One-to-Many: Satu produk bisa masuk ke banyak transaksi.  
   Relasi: `detail_transaksi.id_produk` → `produk.id_produk`

4. **Kategori – Produk**  
   One-to-Many: Satu kategori berisi banyak produk.  
   Relasi: `produk.id_kategori` → `kategori.id_kategori`


## Cara Import Database

**Menggunakan phpMyAdmin:**
1. Login ke phpMyAdmin.
2. Klik "New" lalu buat database dengan nama `toko_online`.
3. Pilih database tersebut, klik tab "Import".
4. Pilih file `database.sql`, lalu klik "Go".

**Menggunakan MySQL CLI:**
```bash
mysql -u root -p < database.sql

