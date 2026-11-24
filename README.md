# Studi komparatif model generatif

Buka [notebooks/studi_generatif.ipynb](notebooks/studi_generatif.ipynb) di VS Code. Pilih kernel **Deep Learning (Python 3.11)**, lalu jalankan **Restart Kernel and Run All**. Jika perlu menyiapkan kernel baru, pasang dependensi dengan `python -m pip install -r requirements.txt`, lalu pilih interpreter tersebut di VS Code. Untuk pelatihan CUDA, gunakan build PyTorch dan torchvision yang sesuai dengan driver.

- [Draf laporan 11 halaman](report/draf_laporan.pdf) memuat metode, metrik, lima figur, dan catatan Q1–Q6.
- Mode default memuat delapan checkpoint terpilih dari eksperimen referensi lokal. Ia menghitung ulang metrik rekonstruksi dan akurasi test, lalu membuat lima figur dan CSV di `results/review/`.
- `REPLAY_FID=True` menghitung ulang FID test untuk VAE, Vanilla GAN, DCGAN, dan DDPM. [Verifikasi FID tersimpan](results/review/fid-replay.csv) mencatat selisih absolut kurang dari 0,002 terhadap nilai referensi.
- `TRAIN=True` melatih dari inisialisasi baru, memilih model dengan validation, menghitung metrik test, dan menyimpan hasil di `results/training/`. Latihan penuh dan FID lebih praktis dengan GPU.
- `results/checkpoints/` dan `results/metrics/` menyimpan bobot, histori, split, dan angka dari run referensi. `data/` menyimpan cache Fashion-MNIST dan bobot Inception lokal. Notebook mengambil cache yang diperlukan pada pemakaian pertama jika cache lokal kosong.

Eksperimen ini menggunakan split yang sama untuk semua model, seed 42, dan batch 128. Bobot dan histori berasal dari salinan lokal `Tuges AE_GAN/DL-Generative-Models`. Mode review mempertahankan angka latensi dari RTX 4060 Laptop GPU. Jika melatih ulang, hasil dapat berubah karena urutan inisialisasi, urutan batch, dan perangkat. Kode pelatihan ringkas diuji satu epoch dengan subset data untuk setiap model dan decoder.

PDF tugas meminta PDF 10–12 halaman, tautan repositori GitHub publik, dan riwayat pengerjaan. PDF juga membatasi bantuan AI pada referensi sintaks serta dokumentasi. Repositori ini berisi materi referensi yang dikerjakan dengan bantuan AI dan mempertahankan sumber hasil lama.
