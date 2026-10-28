# Modul Praktikum Pertemuan 6: Working with Foundation Model (Part 2)

**Topik:** Pengaplikasian Foundation Model pada Studi Kasus Analisis Sentimen & Komparasi Performa Model pada Deteksi Spam

---

## 1. Nama Praktikum
Pengaplikasian Foundation Model pada Kasus Analisis Sentimen Ulasan Produk dan Komparasi Performa Model (Qwen vs Gamma)

## 2. Target Kompetensi
1. Mahasiswa mampu mengaplikasikan *Foundation Model* (**Qwen**) untuk menyelesaikan kasus **Analisis Sentimen pada Ulasan Produk** (Positif, Negatif, dan Netral) di Google Colab.
2. Mahasiswa mampu menguji kepatuhan format keluaran (*format compliance*) pada *Foundation Model*, yaitu membandingkan instruksi jawaban singkat (satu kata label) dengan jawaban berbentuk paragraf.
3. Mahasiswa mampu melakukan komparasi performa antara model **Qwen** dan **Gamma (Google Gemma)** pada studi kasus **Deteksi SPAM** berdasarkan 5 parameter: **Akurasi**, **Patuh Format**, **Rata-rata Waktu per Jawaban**, **Pemakaian Memori (VRAM) per Jawaban**, dan **Kualitas Bahasa (Skala 1–5)**.

## 3. Alat/Tools yang Digunakan
1. **Google Colaboratory** (https://colab.research.google.com) dengan akselerator *Hardware* **T4 GPU**.
2. **Akun & Access Token Hugging Face** (https://huggingface.co/settings/tokens).
3. **Framework/Library Python:** `torch`, `transformers`, `accelerate`, dan `huggingface_hub`.
4. **Foundation Model:**
   - **Model 1 (Praktikum & Komparasi):** `Qwen/Qwen2.5-1.5B-Instruct` (https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct)
   - **Model 2 (Tugas Komparasi):** `google/gemma-2-2b-it` (https://huggingface.co/google/gemma-2-2b-it) atau repositori alternatif `unsloth/gemma-2-2b-it` (https://huggingface.co/unsloth/gemma-2-2b-it)

---

## 4. Daftar File pada Repository Ini
1. `Praktikum_4_Menjalankan_Foundation_Model_Qwen.ipynb` : Notebook panduan praktikum di kelas untuk studi kasus **Analisis Sentimen Ulasan Produk** menggunakan model **Qwen** beserta pencatatan waktu eksekusi dan VRAM.
2. `Tugas_4_Menjalankan_Foundation_Model_Gamma.ipynb` : Template notebook tugas mandiri untuk menguji model **Gamma (Gemma)** dan melakukan **Komparasi Performa Qwen vs Gamma pada Kasus Deteksi Spam**.

---

## 5. Langkah-Langkah Praktikum

### Tahap A: Persiapan Lingkungan GPU & Autentikasi Hugging Face
1. Unduh file `Praktikum_4_Menjalankan_Foundation_Model_Qwen.ipynb` dari repositori ini, lalu buka di Google Colab (https://colab.research.google.com).
2. Aktifkan GPU melalui menu **Runtime -> Change runtime type -> pilih T4 GPU -> Save**.
3. Jalankan sel **Tahap 1** untuk memastikan status `Is GPU Available? : True` dan menginstal library `transformers`, `accelerate`, serta `huggingface_hub`.
4. Jalankan sel **Tahap 2 (`login()`)** dan masukkan **Access Token (`hf_...`)** Hugging Face Anda.

### Tahap B: Pembuatan Model Analisis Sentimen Ulasan Produk (Praktikum Kelas)
1. Jalankan sel **Langkah 1** untuk memuat *Tokenizer* dan *Model* `Qwen/Qwen2.5-1.5B-Instruct` ke dalam memori GPU (VRAM) serta mencatat waktu muat dan penggunaan memori awal.
2. Jalankan sel **Langkah 2** untuk mendefinisikan function `jalankan_qwen()`. Function ini telah dilengkapi dengan penghitung **Waktu Eksekusi (`Execution Time`)** dalam satuan detik dan **Puncak Pemakaian Memori GPU (`Peak VRAM`)** dalam satuan MB untuk setiap jawaban yang dihasilkan.
3. Jalankan sel **Langkah 3** untuk menguji model pada berbagai sampel **Ulasan Produk**:
   - Menguji ketepatan klasifikasi sentimen (**POSITIF**, **NEGATIF**, dan **NETRAL**).
   - Mengamati **Kepatuhan Format**, yaitu apakah model mampu mematuhi instruksi ketika diminta hanya menjawab label `POSITIF`/`NEGATIF`/`NETRAL` saja tanpa penjelasan tambahan, dibandingkan ketika diminta memberikan alasan dalam satu paragraf.

---

## 6. Tugas Praktikum (Asesmen Mandiri)
Pada tugas pertemuan ke-6 ini, mahasiswa diminta melakukan **Komparasi Performance antara Qwen dan Gamma (Gemma) untuk Kasus Deteksi SPAM** dengan langkah-langkah berikut:

1. Unduh file template `Tugas_4_Menjalankan_Foundation_Model_Gamma.ipynb` dari repositori ini dan buka di Google Colab.
2. Lengkapi kode untuk memuat model **Gamma** (`google/gemma-2-2b-it` atau `unsloth/gemma-2-2b-it`) beserta function `jalankan_gamma()` yang mencatat **Waktu Eksekusi (`Execution Time`)** dan **Pemakaian Memori (`Peak VRAM`)** per jawaban.
3. Uji kedua model (**Qwen** dan **Gamma**) menggunakan **3 sampel pesan uji Deteksi SPAM** yang telah disediakan di dalam notebook (mencakup pengujian instruksi format singkat satu kata `SPAM`/`BUKAN SPAM` maupun format penjelasan).
4. Hitung dan isi **Tabel Komparasi Performa Qwen vs Gamma** pada bagian akhir notebook yang mencakup **5 kriteria wajib**:
   - **Akurasi:** Persentase atau jumlah tebakan yang tepat dari seluruh sampel pesan uji (contoh: `3/3 (100%)` atau `2/3 (66.7%)`).
   - **Patuh Format:** Apakah model patuh hanya memberikan label jawaban saja ketika diminta, atau tetap memberikan penjelasan satu paragraf.
   - **Rata-rata Waktu per Jawaban (Detik):** Rata-rata nilai `Execution Time` dari ketiga pengujian prompt.
   - **Pemakaian Memori per Jawaban (MB):** Rata-rata atau nilai `Peak VRAM` yang dibutuhkan model saat menghasilkan jawaban.
   - **Kualitas Bahasa yang Digunakan (Range 1 s/d 5):**
     - `1` = Tidak mudah dimengerti dan tidak baku
     - `2` = Kurang mudah dimengerti dan kurang baku
     - `3` = Cukup mudah dimengerti dan cukup baku
     - `4` = Mudah dimengerti dan baku
     - `5` = Sangat mudah dimengerti dan sangat baku

---

## 7. Format Laporan dan Pengumpulan
Mahasiswa wajib mengumpulkan **2 (dua) file** secara langsung ke LMS Layar sebelum batas waktu berakhir:

1. **File Notebook Tugas (`.ipynb`):**
   - Pastikan seluruh sel kode telah dijalankan (*Run*) sehingga seluruh *output* teks, waktu eksekusi, dan pemakaian VRAM tampil lengkap di bawah setiap sel kode.
   - Unduh dari Google Colab melalui menu **File -> Download -> Download .ipynb**.
   - Format nama file: `Tugas_4_[NPM]_[NamaLengkap].ipynb`
2. **File Laporan Praktikum (`.pdf`):**
   - Berisi identitas mahasiswa (Nama dan NPM), *screenshot* bukti hasil eksekusi praktikum Analisis Sentimen (Qwen) dan tugas Deteksi Spam (Qwen & Gamma), **Tabel Komparasi 5 Parameter**, serta analisis kesimpulan model mana yang memiliki performa lebih baik.
   - Format nama file: `Laporan_Tugas_4_[NPM]_[NamaLengkap].pdf`

---

## 8. Rubrik Penilaian (Total: 100 Poin)

| No | Komponen Penilaian | Bobot Maksimal | Poin Penuh (Selesai & Tepat) | Setengah Poin (Kurang Lengkap / Error Sebagian) | 0 Poin (Tidak Dikerjakan / Gagal) |
| :-: | :--- | :---: | :--- | :--- | :--- |
| 1 | **Implementasi Model & Eksekusi Kasus Deteksi Spam** | **30 Poin** | **30 Poin:** Berhasil memuat model Gamma serta menjalankan pengujian ke-3 sampel pesan Deteksi Spam tanpa *error* dengan *output* tampil lengkap. | **15 Poin:** Model berhasil dimuat namun hanya menguji 1–2 sampel pesan atau terdapat *error* pada sebagian sel. | **0 Poin:** Kode tidak dikerjakan atau tidak dijalankan (*belum di-run*). |
| 2 | **Pengujian Akurasi & Kepatuhan Format** | **25 Poin** | **25 Poin:** Menguji dan mengevaluasi dengan benar apakah model menjawab tepat (Akurasi) serta apakah model mematuhi batasan format jawaban singkat vs satu paragraf. | **12 Poin:** Menjalankan *prompt* tetapi tidak mengevaluasi aspek kepatuhan format dan akurasi jawaban. | **0 Poin:** Tidak melakukan pengujian. |
| 3 | **Pencatatan Rata-rata Waktu & Pemakaian Memori (VRAM)** | **25 Poin** | **25 Poin:** Menampilkan `Execution Time` (detik) dan `Peak VRAM` (MB) pada setiap jawaban serta menghitung rata-ratanya dengan tepat. | **13 Poin:** Menampilkan waktu dan VRAM pada kode tetapi salah atau tidak menghitung nilai rata-ratanya di tabel. | **0 Poin:** Tidak mencatat waktu eksekusi maupun pemakaian memori. |
| 4 | **Tabel Komparasi 5 Parameter, Laporan PDF & Format File** | **20 Poin** | **20 Poin:** Tabel komparasi Qwen vs Gamma terisi lengkap untuk ke-5 parameter (termasuk skor Kualitas Bahasa 1–5), kesimpulan jelas, dan mengumpulkan file `.ipynb` serta `.pdf` sesuai format nama. | **10 Poin:** Tabel komparasi tidak mencantumkan salah satu parameter atau hanya mengumpulkan salah satu file (`.ipynb` atau `.pdf`). | **0 Poin:** Tidak melampirkan tabel komparasi dan laporan PDF. |
