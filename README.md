# ExamTrace

ExamTrace adalah proyek deteksi kecurangan saat ujian dari rekaman peserta. Model menentukan apakah tiap cuplikan termasuk `normal` atau `cheat`.

## 🎯 Tujuan

- Membangun model yang bisa mengenali pola perilaku pada peserta yang belum dilihat saat pelatihan.
- Mengukur apakah urutan gerakan membantu membedakan aktivitas yang mirip, seperti mengecek dan menggunakan smartwatch.
- Menghasilkan satu prediksi untuk setiap ID test sesuai format submission.

## 📊 Dataset

| Bagian | Isi |
| --- | --- |
| `data/train/normal/` | 208 video MOV. Contohnya menulis jawaban, berpikir, melihat sekitar, dan mengecek smartwatch. |
| `data/train/cheat/` | 208 video MOV. Contohnya melirik berulang, membaca catatan tersembunyi, melihat ke bawah meja, dan menggunakan smartwatch. |
| `data/test/` | 1.515 sekuens dengan total 45.450 frame JPG. |
| `data/sample_submission.csv` | Contoh submission dengan 1.515 baris dan kolom `id` serta `label`. |

Video train dikelompokkan berdasarkan subjek dan direkam dari sudut depan (`front`) serta samping (`side`). Folder `data/` disimpan secara lokal dan diabaikan Git. Rujuk `Jawaban FAQ.docx` untuk aturan kompetisi, termasuk metrik dan pemetaan label.

## ⏳ Alur pengerjaan

- [ ] **Eksplorasi data.** Catat label, ID subjek, aktivitas, sudut kamera, durasi, FPS, dan resolusi video. Cek apakah video serta frame bisa dibaca dan apakah ID test cocok dengan contoh submission.
- [ ] **Split train dan validasi berdasarkan subjek.** Tempatkan semua rekaman satu subjek, termasuk kedua sudut kamera, di split yang sama supaya orang yang sama tidak muncul di train dan validasi.
- [ ] **Preprocessing.** Ambil frame dari video train dan urutkan frame test berdasarkan nomor file. Gunakan ukuran input dan normalisasi yang konsisten.
- [ ] **Latih baseline.** Klasifikasikan frame dengan model citra, lalu rata-ratakan probabilitas frame untuk menghasilkan satu prediksi per sekuens.
- [ ] **Evaluasi dan analisis kesalahan.** Gunakan metrik resmi kompetisi. Cek confusion matrix dan bandingkan kesalahan berdasarkan aktivitas dan sudut kamera. Catat skor pada split validasi yang sama agar eksperimen bisa dibandingkan.
- [ ] **Uji model temporal.** Bandingkan baseline dengan model yang mempertimbangkan urutan frame. Pilih model berdasarkan hasil validasi.
- [ ] **Prediksi dan submit.** Buat `submission.csv` dengan satu prediksi per ID, urutan ID sesuai template, dan label sesuai aturan panitia.

## 💻 Mulai dari notebook

Buka [code.ipynb](code.ipynb) dari root proyek. Mulai dari eksplorasi data dan audit file sebelum menambahkan preprocessing dan training. Catat temuan EDA, pilihan model, dan skor validasi di notebook saat hasilnya sudah tersedia.
