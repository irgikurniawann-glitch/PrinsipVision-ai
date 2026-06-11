# PrinsipVision AI - Spatial OCR Extraction Tool

PrinsipVision AI adalah aplikasi berbasis web pintar yang dirancang untuk mengekstrak teks dari dokumen resmi, tanda terima, atau struk belanja dengan tingkat presisi tata letak yang tinggi (**Layout/Spatial Preservation**). 

Aplikasi ini memecahkan masalah umum pada OCR konvensional yang sering kali menggabungkan teks berkolom menjadi satu paragraf acak, sehingga merusak struktur pembacaan tabel atau data kanan-kiri.

---

##  Fitur Utama

- **Spatial Layout Preservation:** Menggunakan algoritma kalkulasi spasi dinamis berdasarkan rata-rata lebar karakter untuk mempertahankan format kolom dan baris asli dokumen.
- **Dynamic Vertical Reconstruction:** Menghitung jarak baris (`gap`) secara geometris untuk merekonstruksi spasi paragraf atau tabel kosong agar tidak saling dempet.
- **Interactive Visual Feedback:** Menampilkan bounding box interaktif di atas dokumen menggunakan `gr.AnnotatedImage` untuk menunjukkan teks yang berhasil dikenali oleh model AI.
- **Bilingual Core UI (i18n):** Pemilihan bahasa pengantar (Indonesia & English) yang langsung memperbarui seluruh komponen interface secara dinamis.
- **Modern & Responsive UI:** Tampilan antarmuka berbasis antarmuka kartu (*Card-based UI*) yang adaptif untuk perangkat desktop maupun mobile.

---

## Tech Stack & Model AI

- **Core Engine:** [EasyOCR](https://github.com/JaidedAI/EasyOCR) (Deep Learning-based OCR dengan arsitektur CRAFT untuk deteksi teks dan CRNN untuk pengenalan karakter).
- **Inference Accelerator:** PyTorch (Mendukung akselerasi GPU CUDA jika tersedia).
- **Image Processing:** OpenCV & NumPy (Untuk manipulasi koordinat spasial biner $X$ dan $Y$).
- **Web Framework:** Gradio (Sebagai *interface layer* aplikasi).

---

##  Analisis Algoritma Spasial

Aplikasi ini tidak sekadar mengekstrak string mentah, melainkan memproses array koordinat bounding box (`bbox`) dari EasyOCR dengan logika matematika berikut:

1. **Dynamic Grouping:** Mengelompokkan teks ke dalam satu baris yang sama berdasarkan toleransi tinggi huruf dinamis:  
   $$\text{Dynamic Tolerance} = \text{Average Height} \times 0.5$$
2. **Matrix Projection:** Memproyeksikan posisi koordinat horizontal $X_{min}$ gambar ke dalam representasi kolom string biner berdasarkan proporsi lebar maksimum karakter:  
   $$\text{Target Column} = \frac{X_{min}}{\text{Image Width}} \times \text{MAX\_COLUMNS}$$

---

## Cara Menjalankan di Lokal (Local Deployment)

### 1. Kloning Repositori
```bash
git clone [https://github.com/irgikurniawann-glitch/PrinsipVision-AI.git](https://github.com/irgikurniawann-glitch/PrinsipVision-AI.git)
cd PrinsipVision-AI
