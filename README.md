# Studi komparatif model generatif

Eksperimen Fashion-MNIST memakai split train, validation, dan test 80/10/10, seed 42, serta batch size 128.

## Menjalankan notebook

Pasang dependensi dengan `python -m pip install -r requirements.txt`. Buka proyek di VS Code dan pilih kernel Python 3.11. Untuk CUDA, gunakan build PyTorch dan torchvision yang sesuai dengan driver GPU.

1. [Data dan arsitektur](notebooks/01_data_dan_arsitektur.ipynb)
2. [Vanilla AE, Sparse AE, dan VAE](notebooks/02_autoencoder_dan_vae.ipynb)
3. [Vanilla GAN](notebooks/03_vanilla_gan.ipynb)
4. [DCGAN](notebooks/04_dcgan.ipynb)
5. [DDPM](notebooks/05_ddpm.ipynb)
6. [MLP dan decoder beku](notebooks/06_mlp_dan_decoder_beku.ipynb)
7. [Perbandingan hasil](notebooks/07_komparasi.ipynb)

Jalankan `02` sebelum `06` karena `06` memakai checkpoint Vanilla AE yang dibuat oleh `02`. Dengan `TRAIN=True`, notebook melatih model dan menulis checkpoint serta metrik ke folder `custom_*` di bawah `results/checkpoints/` dan `results/metrics/`. Pilih `TRAIN=False` setelah checkpoint tersedia untuk mengulang evaluasi. FID test menggunakan TorchMetrics dengan 2.048 sampel. Cache Fashion-MNIST dan bobot Inception memerlukan akses unduh pada pemakaian pertama.

Bobot dan hasil referensi yang sudah tercatat di Git berasal dari pengerjaan terdahulu berbantuan AI. Hasil pelatihan baru tersimpan di folder `custom_*` di atas.

Tabel, figur, dan catatan sumber eksperimen aktif tersedia di [results/final](results/final/README.md).
