# Modul Praktikum Pertemuan 6: Working with Foundation Model (Part 2)

Topik: Pengaplikasian Foundation Model pada Studi Kasus Analisis Sentimen dan Komparasi Performa Model pada Deteksi Spam

---

## 1. Nama Praktikum
Pengaplikasian Foundation Model pada Kasus Analisis Sentimen Ulasan Produk dan Komparasi Performa Model (Qwen vs Gamma)

## 2. Target Kompetensi
1. Mahasiswa mampu mengaplikasikan Foundation Model (Qwen) untuk menyelesaikan kasus analisis sentimen pada ulasan produk di Google Colab.
2. Mahasiswa mampu menguji kepatuhan format keluaran pada Foundation Model, yaitu melihat apakah model memberikan jawaban singkat (positif/negatif/netral saja) atau memberikan jawaban satu paragraf.
3. Mahasiswa mampu melakukan komparasi performa antara model Qwen dan Gamma (Google Gemma) pada kasus deteksi spam berdasarkan 5 parameter: akurasi, patuh format, rata-rata waktu per jawaban, pemakaian memori (VRAM) per jawaban, dan kualitas bahasa (skala 1 sampai 5).

## 3. Alat/Tools yang Digunakan
1. Google Colaboratory (https://colab.research.google.com) dengan akselerator T4 GPU.
2. Akun dan Access Token Hugging Face (https://huggingface.co/settings/tokens).
3. Framework/Library Python: `torch`, `transformers`, `accelerate`, dan `huggingface_hub`.
4. Foundation Model:
   - Model 1 (Praktikum & Komparasi): `Qwen/Qwen2.5-1.5B-Instruct` (https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct)
   - Model 2 (Tugas Komparasi): `google/gemma-2-2b-it` (https://huggingface.co/google/gemma-2-2b-it) atau repositori alternatif `unsloth/gemma-2-2b-it` (https://huggingface.co/unsloth/gemma-2-2b-it)

---

## 4. Daftar File pada Repository Ini
1. `Praktikum_4_Menjalankan_Foundation_Model_Qwen.ipynb` : Notebook panduan praktikum di kelas menggunakan model Qwen beserta pencatatan waktu eksekusi dan VRAM.
2. `Tugas_4_Menjalankan_Foundation_Model_Gamma.ipynb` : Template notebook kosong untuk mengerjakan tugas mandiri menggunakan model Gamma (Gemma) dan komparasi performa deteksi spam.

---

## 5. Langkah-Langkah Praktikum

### Tahap A: Persiapan Lingkungan GPU & Autentikasi Hugging Face
1. Unduh file `Praktikum_4_Menjalankan_Foundation_Model_Qwen.ipynb` dari repositori ini, lalu buka di Google Colab (https://colab.research.google.com).
2. Aktifkan GPU melalui menu Runtime -> Change runtime type -> pilih T4 GPU -> Save.
3. Jalankan sel Tahap 1 untuk memastikan status `Is GPU Available? : True` dan menginstal library `transformers`, `accelerate`, serta `huggingface_hub`.
4. Jalankan sel Tahap 2 (`login()`) dan masukkan Access Token (`hf_...`) Hugging Face Anda.

### Tahap B: Pengaplikasian Model pada Analisis Sentimen Ulasan Produk
1. Jalankan sel Langkah 1 untuk memuat Tokenizer dan Model `Qwen/Qwen2.5-1.5B-Instruct` ke dalam memori GPU (VRAM).
2. Jalankan sel Langkah 2 untuk membuat function `jalankan_qwen()` yang sekaligus mencatat waktu eksekusi (`Execution Time`) dan pemakaian memori (`Peak VRAM`) per jawaban.
3. Jalankan sel Langkah 3 untuk melihat hasil pengujian model pada kasus analisis sentimen ulasan produk (baik dengan instruksi jawaban singkat satu kata maupun jawaban satu paragraf) serta contoh pengantar kasus deteksi spam.

---

## 6. Tugas Praktikum (Tugas 4)
Pada tugas ini, mahasiswa diminta melakukan komparasi performa antara model Qwen dan Gamma (Gemma) untuk kasus deteksi spam dengan langkah berikut:

1. Unduh file template `Tugas_4_Menjalankan_Foundation_Model_Gamma.ipynb` dari repositori ini dan buka di Google Colab.
2. Lengkapi kode untuk memuat model Gamma (`google/gemma-2-2b-it` atau `unsloth/gemma-2-2b-it`) beserta function `jalankan_gamma()` dengan mengikuti contoh pada notebook praktikum Qwen.
3. Buat dan jalankan pengujian prompt untuk kasus deteksi spam (Anda dapat memodifikasi dari contoh prompt pada praktikum Qwen, termasuk menguji instruksi jawaban singkat saja vs jawaban satu paragraf) pada model Qwen dan Gamma.
4. Catat hasilnya dan lengkapi Tabel Komparasi Performa antara Qwen dan Gamma pada bagian akhir notebook berdasarkan 5 kriteria berikut:
   - Akurasi: ketepatan model dalam menebak pesan spam atau bukan spam.
   - Patuh Format: apakah model memberikan jawaban singkat saja (sesuai yang diminta pada prompt) atau memberikan jawaban satu paragraf.
   - Rata-rata waktu per jawaban: rata-rata nilai `Execution Time` (dalam detik).
   - Pemakaian memori per jawaban: nilai `Peak VRAM` (dalam MB) per jawaban.
   - Kualitas bahasa yang digunakan: dinilai dalam rentang skala 1 (tidak mudah dimengerti dan tidak baku) sampai dengan 5 (sangat mudah dimengerti dan sangat baku).

---

## 7. Format Laporan dan Pengumpulan
Mahasiswa mengumpulkan 2 file ke LMS Layar sebelum batas waktu berakhir:

1. File Notebook Tugas (`.ipynb`):
   - Pastikan semua sel kode sudah dijalankan (Run) sehingga output jawaban, waktu eksekusi, dan pemakaian VRAM tampil di bawah sel.
   - Unduh melalui menu File -> Download -> Download .ipynb.
   - Format nama file: `Tugas_4_[NPM]_[NamaLengkap].ipynb`
2. File Laporan Praktikum (`.pdf`):
   - Berisi identitas mahasiswa (Nama dan NPM), screenshot bukti eksekusi praktikum (Qwen) dan tugas (Gamma), tabel komparasi performa kedua model, serta kesimpulan singkat.
   - Format nama file: `Laporan_Tugas_4_[NPM]_[NamaLengkap].pdf`

---

## 8. Rubrik Penilaian (Total: 100 Poin)

| No | Komponen Penilaian | Bobot Maksimal | Poin Penuh (Selesai & Tepat) | Setengah Poin (Kurang Lengkap / Error Sebagian) | 0 Poin (Tidak Dikerjakan / Gagal) |
| :-: | :--- | :---: | :--- | :--- | :--- |
| 1 | Load Tokenizer & Model Gamma | 30 Poin | 30 Poin: Berhasil memuat tokenizer dan model Gamma ke GPU T4 tanpa error serta menampilkan waktu muat dan pemakaian VRAM. | 15 Poin: Kode pemanggilan model sudah ditulis tetapi masih menghasilkan error saat dijalankan. | 0 Poin: Sel kode dibiarkan kosong. |
| 2 | Function Inference & Eksekusi Prompt Deteksi Spam | 25 Poin | 25 Poin: Function `jalankan_gamma()` dan pengujian prompt deteksi spam berjalan lancar dengan output teks yang tampil lengkap. | 12 Poin: Kode berjalan sebagian atau output belum di-run saat file diunduh. | 0 Poin: Function dan pengujian prompt tidak dikerjakan. |
| 3 | Pencatatan Waktu & Pemakaian Memori per Jawaban | 25 Poin | 25 Poin: Berhasil menampilkan `Execution Time` (detik) dan `Peak VRAM` (MB) per jawaban serta menghitung rata-ratanya di tabel. | 13 Poin: Menampilkan waktu dan VRAM di output kode tetapi tidak dimasukkan ke dalam tabel pengamatan. | 0 Poin: Tidak mencatat waktu eksekusi maupun pemakaian memori. |
| 4 | Tabel Komparasi 5 Parameter, Laporan PDF & Format File | 20 Poin | 20 Poin: Tabel komparasi Qwen vs Gamma (akurasi, patuh format, rata-rata waktu, memori, dan kualitas bahasa 1-5) serta kesimpulan terisi lengkap, dan mengumpulkan file `.ipynb` serta `.pdf` sesuai format nama. | 10 Poin: Tabel komparasi kurang lengkap atau hanya mengumpulkan salah satu dari dua file yang diminta. | 0 Poin: Tidak melampirkan tabel komparasi dan laporan PDF. |
