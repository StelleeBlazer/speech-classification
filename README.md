### 🐾 Animal Sound Classification using CNN

# Klasifikasi Suara Tiruan Hewan menggunakan CNN 🐾

Project Notebook ini merupakan modifikasi dari proyek klasifikasi huruf vokal. Tujuannya adalah untuk melatih sebuah model Convolutional Neural Network (CNN) yang mampu mengklasifikasikan lima jenis suara tiruan hewan:

- Sapi (moo)
- Kucing (meow)
- Anjing (woof)
- Kambing (mbee)
- Burung (tweet)

Prosesnya meliputi persiapan dataset, pra-pemrosesan audio untuk mengekstrak fitur MFCC, pelatihan model CNN, hingga evaluasi dan pengujian.

### Langkah 1: Persiapan Dataset

Untuk membuat notebook ini dapat langsung dijalankan tanpa perlu merekam 75 sampel suara secara manual (15 sampel x 5 kelas), kita akan **mensimulasikan pembuatan dataset**.

Fungsi di bawah ini akan membuat struktur direktori yang benar (`./data/Cow`, `./data/Cat`, dll.) dan mengisinya dengan file `.wav` tiruan (berisi noise putih). Ini memastikan seluruh alur kerja—mulai dari pra-pemrosesan hingga pelatihan—dapat berjalan tanpa error.

**Untuk Penggunaan Nyata**: Anda dapat menghapus atau melewati sel simulasi data dan menggantinya dengan rekaman suara Anda sendiri dengan struktur folder yang sama.

### Langkah 2: Pra-pemrosesan Audio & Ekstraksi Fitur

Tahap ini mengubah data audio mentah menjadi bentuk yang siap diolah oleh model. Prosesnya adalah sebagai berikut:

- **Pra-pemrosesan Audio**:
  - **Voice Activity Detection (VAD)**: Menggunakan `librosa.effects.split` untuk membuang bagian hening (silent) dari audio.
  - **Padding/Cropping**: Menyamakan panjang semua sampel audio menjadi 2 detik. Sampel yang lebih pendek akan diberi *padding* (tambahan hening), dan yang lebih panjang akan dipotong.
  - **Normalisasi Amplitudo**: Menyesuaikan volume suara agar berada dalam rentang yang konsisten.

- **Ekstraksi Fitur MFCC**:
  - **MFCC (Mel-Frequency Cepstral Coefficients)** adalah representasi suara yang meniru persepsi pendengaran manusia. Fitur ini sangat efektif untuk tugas pengenalan suara.
  - Kita akan mengekstrak **40 koefisien MFCC** dari setiap sampel audio yang telah diproses.

### Langkah 3: Visualisasi Data

Untuk mendapatkan pemahaman yang lebih baik tentang data yang kita gunakan, mari kita visualisasikan:
1.  **Bentuk Gelombang (Waveform)**: Menunjukkan bagaimana amplitudo suara berubah seiring waktu, baik sebelum maupun sesudah pra-pemrosesan.
2.  **Spektogram MFCC**: Menampilkan representasi fitur MFCC dari setiap kelas suara. Pola yang berbeda pada spektogram inilah yang akan dipelajari oleh model CNN.

### Langkah 4: Arsitektur Model CNN

Model yang digunakan adalah Convolutional Neural Network (CNN) sederhana yang dirancang untuk input gambar 2D seperti MFCC.

- **Input**: Spektogram MFCC berukuran `(1, 40, 126)`.
- **Lapisan Konvolusi (`conv`)**:
  1.  **Conv2d #1**: Menggunakan 16 filter untuk mendeteksi pola-pola dasar.
  2.  **ReLU**: Fungsi aktivasi untuk memperkenalkan non-linearitas.
  3.  **MaxPool2d**: Mengurangi ukuran fitur (downsampling) untuk efisiensi.
  4.  **Conv2d #2**: Menggunakan 32 filter untuk mendeteksi pola yang lebih kompleks.
  5.  **ReLU & MaxPool2d**.
- **Lapisan Fully Connected (`fc`)**:
  - Fitur yang telah diekstrak kemudian diratakan (*flattened*) dan dihubungkan ke lapisan linear yang menghasilkan output probabilitas untuk 5 kelas suara hewan.

### Langkah 5: Pelatihan Model

Sekarang kita akan melatih model CNN.

- **Device**: Menggunakan GPU (`cuda`) jika tersedia, jika tidak, CPU akan digunakan.
- **Loss Function**: `CrossEntropyLoss`, standar untuk masalah klasifikasi multi-kelas.
- **Optimizer**: `Adam`, sebuah optimizer yang efisien.
- **Epochs**: 100. Jumlah iterasi pelatihan pada keseluruhan dataset.

Selama pelatihan, kita akan memantau loss dan akurasi pada data latihing dan data testing untuk setiap epoch.

### Langkah 6: Evaluasi Kinerja Model

Setelah pelatihan, kita akan mengevaluasi performa akhir model pada data testing menggunakan metrik yang lebih detail:
- **Accuracy**: Persentase prediksi yang benar secara keseluruhan.
- **Classification Report**: Laporan yang berisi:
  - **Precision**: Kemampuan model untuk tidak salah melabeli sampel.
  - **Recall**: Kemampuan model untuk menemukan semua sampel yang relevan.
  - **F1-Score**: Rata-rata harmonik dari precision dan recall.

**Kesimpulan**:
Berdasarkan hasil evaluasi pada dataset simulasi, model menunjukkan performa yang sangat baik, seringkali mencapai akurasi 100%. Namun, penting untuk diingat bahwa dataset ini kecil dan tidak bervariasi. Pengujian lebih lanjut dengan dataset yang lebih besar dan beragam sangat disarankan untuk mengukur performa model yang sesungguhnya.

### Langkah 7: Uji Coba Klasifikasi Langsung

Sel di bawah ini memungkinkan Anda untuk menguji model secara langsung dengan merekam suara menggunakan mikrofon.

**Catatan**: Sel ini hanya akan berfungsi di lingkungan lokal (seperti Jupyter di komputer Anda) dan memerlukan mikrofon yang terpasang. Ini mungkin tidak akan berjalan di Google Colab tanpa konfigurasi tambahan.

#### 🎙️ Record imitated suara hewan tiruan

#### 🔍 Preprocessing & Feature Extraction

#### 🧠 CNN Model

#### 🚀 Training Model

#### ✅ Evaluation

