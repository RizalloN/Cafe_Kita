# Cafe Kita POS

Aplikasi kasir Flutter untuk Android, dengan katalog, stok, biaya operasional,
laporan, pencetakan struk, dan penambahan beberapa item sekaligus.

## Konfigurasi lokal

Repositori publik ini tidak menyertakan konfigurasi Firebase, data pengguna,
gambar QR pembayaran, keystore, atau password operasional. Kode integrasi
Firebase tetap disertakan. Untuk mengaktifkannya, tempatkan file konfigurasi
Firebase milik Anda di `android/app/google-services.json`; file tersebut diabaikan
Git. Firebase dan aturan akses harus dikonfigurasi secara terpisah.

Gambar QRIS diganti dengan placeholder kosong. Sebelum menerima pembayaran QRIS,
ganti referensi `assets/images/qris_placeholder.png` dengan gambar QR pembayaran
milik Anda dan simpan gambar pribadi di luar Git.

Source publik tidak menyertakan kredensial awal atau pepper instalasi asal.
Pengembang perlu mengisi `CAFE_KASIR_PASSWORD`, `CAFE_ADMIN_PASSWORD`,
`CAFE_OWNER_PASSWORD` (masing-masing minimal 12 karakter), dan
`CAFE_LEGACY_PEPPER` melalui `--dart-define` saat menjalankan build maupun tes.
Nilai `--dart-define` dapat diekstrak dari APK: gunakan hanya kredensial bootstrap
sementara, segera ganti saat login pertama, dan jangan gunakan ulang password
operasional atau pepper instalasi lain. Menyimpan file tersebut di Git dilarang.
Salinan publik ini memerlukan pengaturan sendiri sebelum dapat digunakan.

Contoh pengujian lokal dengan nilai khusus pengujian:

```powershell
flutter pub get
flutter test --dart-define=CAFE_KASIR_PASSWORD=Fixture-Kasir-2026! --dart-define=CAFE_ADMIN_PASSWORD=Fixture-Admin-2026! --dart-define=CAFE_OWNER_PASSWORD=Fixture-Owner-2026! --dart-define=CAFE_LEGACY_PEPPER=fixture-pepper
```

Untuk build Android, gunakan nilai bootstrap milik Anda dan jalankan
`flutter build apk --release` dengan keempat opsi `--dart-define` tersebut.
APK tersedia di `build/app/outputs/flutter-apk/app-release.apk`. File Firebase
harus dikonfigurasi terlebih dahulu. Release proyek masih memakai debug signing;
siapkan keystore produksi sendiri sebelum distribusi.

