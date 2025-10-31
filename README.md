Deteksi Penyakit Tanaman dengan Deep Learning

Proyek ini adalah eksplorasi dan perbandingan model deep learning untuk klasifikasi gambar, dengan studi kasus mendeteksi 38 jenis penyakit tanaman yang berbeda dari citra daun.Tujuan utama dari repositori ini adalah untuk membandingkan performa dari beberapa arsitektur Convolutional Neural Network (CNN) modern yang populer (MobileNetV2, ResNet50, DenseNet121) menggunakan metode Transfer Learning dan Fine-Tuning.

Tentang Proyek
Deteksi dini penyakit pada tanaman sangat penting untuk ketahanan pangan dan manajemen pertanian. Proyek ini mencoba mengotomatisasi proses tersebut menggunakan computer vision.Daripada hanya membangun satu model, riset ini berfokus pada:Efektivitas Transfer Learning: Seberapa baik model yang sudah dilatih (di ImageNet) beradaptasi dengan tugas baru?Perbandingan Arsitektur: Model mana (feature extractor) yang paling cocok untuk dataset ini?Manfaat Fine-Tuning: Seberapa besar peningkatan akurasi yang bisa didapat setelah kita "mencairkan" sebagian layer dan melatihnya ulang dengan learning rate rendah?

DatasetProyek ini menggunakan New Plant Diseases Dataset (Augmented) yang tersedia di Kaggle.Sumber: Isi: Lebih dari 87.000 gambar RGB.Kelas: 38 kelas yang berbeda (contoh: Apple___Apple_scab, Corn_(maize)___healthy, Tomato___Bacterial_spot).Struktur: Dataset sudah dibagi menjadi folder train dan valid untuk kemudahan penggunaan.

Metodologi RisetAlur kerja (pipeline) machine learning yang digunakan dalam proyek ini adalah sebagai berikut:Preprocessing DataMenggunakan ImageDataGenerator dari Keras.Normalisasi: Gambar di-rescale dari rentang [0, 255] menjadi [0, 1].Resizing: Semua gambar diubah ukurannya menjadi $128 \times 128$ piksel.Data Augmentation: Diterapkan pada data training (rotasi, zoom, shear, horizontal flip) untuk mencegah overfitting dan membuat model lebih kokoh.Perbandingan Model (Eksperimen)Kami membandingkan tiga model pre-trained yang diakui:MobileNetV2ResNet50DenseNet121Proses Training Dua TahapSetiap model dilatih menggunakan strategi dua tahap untuk performa maksimal:Tahap 

1: Transfer Learning (Melatih Head)Seluruh layer feature extractor (misalnya MobileNetV2) dibekukan (trainable = False).Hanya layer klasifikasi baru (head) yang kita tambahkan di atasnya yang dilatih.Dilatih selama 5 Epoch dengan optimizer Adam.Tahap 
2: Fine-Tuning (Melatih Sebagian Base)Sebagian layer teratas dari feature extractor "dicairkan" (trainable = True).Model di-compile ulang dengan learning rate yang sangat rendah ($1e-5$) agar tidak merusak weights yang sudah ada.Model dilatih kembali selama 10 Epoch tambahan.

Cara Menjalankan Proyek
Anda dapat mereproduksi hasil riset ini dengan mengikuti langkah-langkah berikut:
Clone RepositoriInstalasi LibraryPastikan Anda memiliki Python 3. 

Proyek ini membutuhkan library berikut:
Setup DatasetDownload dataset dari https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset?resource=download.
Ekstrak file zip.
Pastikan struktur folder Anda sesuai dengan yang digunakan dalam notebook, yaitu:
Ubah variabel base_dir di dalam notebook agar sesuai dengan path di komputer Anda.Jalankan NotebookBuka file .ipynb (misalnya Plant_Disease_Riset.ipynb) menggunakan Jupyter Notebook atau Google Colab dan jalankan sel-selnya secara berurutan.

Teknologi yang Digunakan
Python 3
TensorFlow & Keras: Untuk membangun dan melatih model deep learning.
NumPy: Untuk operasi numerik.
Matplotlib: Untuk membuat plot dan visualisasi hasil.
Jupyter Notebook: Untuk lingkungan riset interaktif.
