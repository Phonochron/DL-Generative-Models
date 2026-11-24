# Hasil komparasi Fashion-MNIST

Buka [Notebook 07](../../notebooks/07_komparasi.ipynb) untuk membaca tabel dan kelima figur. Notebook ini memakai data evaluasi yang sudah diekspor dari checkpoint terpilih. Split 56.000/7.000/7.000 dan seed 42 sama untuk seluruh model.

- [Tabel enam model](comparison.csv) dan [skor pemilihan checkpoint](validation.csv).
- [Figur 1](figures/figure1.png) rekonstruksi delapan citra test.
- [Figur 2](figures/figure2.png) enam belas sampel acak per generator.
- [Figur 3](figures/figure3.png) transpos kelas dan fitur, decoder beku, Vanilla AE, serta sampling Gaussian MLP.
- [Figur 4](figures/figure4.png) interpolasi lima model pada enam nilai alpha.
- [Figur 5](figures/figure5.png) kurva loss enam model dan enam tahap reverse DDPM.

## Sumber dan pengukuran

- AE dan VAE memakai checkpoint di `custom_ae_vae`. Ketiganya dipilih berdasarkan MSE validasi. MSE, PSNR, dan SSIM dihitung dari 7.000 citra test.
- Vanilla GAN dan DCGAN memakai run `custom_vanilla_gan_v2` dan `custom_dcgan_v2`. Epoch 15, 30, dan 50 dievaluasi dengan CNN-FID validasi yang sama untuk kandidat dalam tiap run. Skor validasi dan FID test menggunakan extractor fitur yang berbeda.
- FID test memakai TorchMetrics Inception 2048, 2.048 citra test pertama sesuai indeks split dan 2.048 citra sintetis. FID yang tercatat ialah VAE 95.01, Vanilla GAN 117.97, DCGAN 43.40, DDPM 67.89. DDPM memakai checkpoint epoch 20, sampler clipped-x0, 200 langkah.
- Waktu GAN ialah rerata 50 epoch training v2. Waktu AE, VAE dan DDPM diukur dari satu epoch benchmark terpisah dengan seed 42 dan seluruh 56.000 citra training. Validation dan penyimpanan checkpoint berada di luar interval ukur. Benchmark memakai NVIDIA GeForce RTX 4060 Laptop GPU dan PyTorch 2.11.0+cu128. Latensi per batch 64 berasal dari notebook masing-masing untuk generasi dan benchmark terpisah untuk rekonstruksi.
- Figur 2 memakai sampel seed 42. Figur 4 memakai kelas T-shirt/top dan Ankle boot. Label endpoint GAN diestimasi oleh MLP dari 1.024 kandidat dengan seed 43. Prediksi kelas, indeks kandidat, dan konfigurasi benchmark tercatat di [benchmark.json](benchmark.json). Figur 5 memakai frame dari satu jalur reverse DDPM seed 45.
- MLP epoch 22 memprediksi benar 6,271 dari 7,000 citra test (89.59%). Decoder beku epoch 28 menghasilkan MSE 0.017384, PSNR 18.4067 dB, dan SSIM 0.6599. Uji prior pada CPU menghasilkan 178 dari 640 koordinat negatif, dengan 12 dimensi fitur bersimpangan baku nol. Lihat [hasil MLP](../metrics/custom_mlp_decoder/mlp_test_accuracy.json) dan [komparasi decoder](../metrics/custom_mlp_decoder/mlp_decoder_comparison.csv).

## Acuan untuk memperbarui laporan

| Halaman laporan saat ini | Bagian yang perlu dicocokkan |
| --- | --- |
| 1 | Ganti angka rangkuman dengan hasil tabel dan akurasi MLP terbaru. |
| 2 | Perbarui jumlah sampel FID menjadi 2.048 per distribusi, kriteria pemilihan VAE menjadi MSE validasi, dan sumber waktu training. |
| 4 | Catat bahwa statistik BatchNorm discriminator DCGAN dibekukan saat langkah generator. |
| 5 | Gunakan `comparison.csv` dan pisahkan penjelasan CNN-FID validasi dari Inception FID test. |
| 6–10 | Gunakan Figur 1–5 berurutan. Cocokkan angka decoder dan prior MLP pada halaman 8 serta endpoint interpolasi pada halaman 9. |
| 11 | Tinjau lagi jawaban Q6 dan keterbatasan berdasarkan hasil yang dipakai di laporan. |

Folder ini memuat artefak verifikasi teknis berbantuan AI. Laporan PDF lama menyimpan hasil referensi. Penulis perlu memeriksa artefak dan menyusun pembahasan Q1–Q6 sesuai ketentuan halaman 6 pada panduan tugas.
