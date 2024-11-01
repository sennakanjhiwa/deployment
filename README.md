# Deployment Laravel

Berikut langkah-langkah untuk menyesuaikan izin saat kamu akan melakukan deployment proyek Laravel ke server produksi. Langkah-langkah ini memastikan keamanan tanpa mengurangi aksesibilitas bagi server web:

Sesuaikan Pemilik dan Grup Direktori Proyek
Ubah kepemilikan folder proyek agar hanya web server (misalnya, www-data) yang memiliki akses penuh di lingkungan produksi:

sudo chown -R www-data:www-data /path/to/your/laravel-project

Atur Izin untuk File dan Folder Secara Rekursif
Sesuaikan izin file dan folder proyek untuk meningkatkan keamanan:

# Izin 644 untuk semua file
sudo find /path/to/your/laravel-project -type f -exec chmod 644 {} \;

# Izin 755 untuk semua folder
sudo find /path/to/your/laravel-project -type d -exec chmod 755 {} \;

Atur Izin Khusus untuk Direktori storage dan bootstrap/cache
Folder storage dan bootstrap/cache membutuhkan akses tulis agar Laravel bisa menyimpan cache, sesi, dan file log. Berikan izin yang lebih longgar hanya pada folder ini:

sudo chmod -R 775 /path/to/your/laravel-project/storage
sudo chmod -R 775 /path/to/your/laravel-project/bootstrap/cache

Amankan File .env
File .env berisi konfigurasi penting dan rahasia. Ubah izin file ini agar hanya dapat dibaca oleh user www-data:

sudo chmod 600 /path/to/your/laravel-project/.env

Perbarui Izin saat Perubahan Baru
Saat melakukan pembaruan pada proyek, misalnya dengan git pull, periksa kembali izin file dan folder karena beberapa perubahan bisa mengubahnya. Kamu bisa menjalankan perintah-perintah di atas sebagai langkah akhir setelah update.

Optimalkan Laravel untuk Produksi
Setelah hak akses diatur, jalankan beberapa perintah optimasi berikut untuk memastikan aplikasi Laravel berjalan optimal di produksi:

php artisan config:cache
php artisan route:cache
php artisan view:cache

Langkah-langkah ini memastikan aplikasi Laravel tetap aman dan optimal di lingkungan produksi.
