# 📌 Recommender System: Word2Vec + ALS

## 🇮🇩 Deskripsi (Bahasa Indonesia)
Proyek ini adalah sistem rekomendasi yang menggabungkan dua pendekatan utama:
1. **Content-Based Filtering** menggunakan **Word2Vec** untuk merepresentasikan teks deskripsi produk sebagai vektor.
2. **Collaborative Filtering** menggunakan **Alternating Least Squares (ALS)** dari pustaka `implicit` untuk menemukan pola interaksi pengguna-produk.

Tujuan utama adalah memberikan rekomendasi produk yang relevan berdasarkan kesamaan konten dan perilaku pengguna lain.

---

## 🇬🇧 Description (English)
This project is a recommendation system that combines two main approaches:
1. **Content-Based Filtering** using **Word2Vec** to represent product description text as vectors.
2. **Collaborative Filtering** using **Alternating Least Squares (ALS)** from the `implicit` library to capture user-item interaction patterns.

The main goal is to provide relevant product recommendations based on both content similarity and collaborative behavior.

---

## 🚀 Fitur Utama / Main Features

### 🇮🇩 Bahasa Indonesia
- Tokenisasi deskripsi produk menjadi vektor dengan **Word2Vec**
- Rekomendasi berbasis kesamaan konten (cosine similarity)
- Collaborative Filtering menggunakan **ALS**
- Visualisasi distribusi rating dan evaluasi produk terbaik/terburuk

### 🇬🇧 English
- Tokenize product descriptions into vectors using **Word2Vec**
- Content-based recommendations via **cosine similarity**
- Collaborative Filtering using **ALS**
- Visualization of rating distribution and evaluation of top/bottom products

---

## ⚙️ Instalasi / Installation

### 🇮🇩 Bahasa Indonesia
Pastikan Anda memiliki Python 3.10+ dan jalankan perintah berikut:

```bash
pip install numpy pandas gensim implicit seaborn matplotlib scikit-learn
```

### 🇬🇧 English
Make sure you have Python 3.10+ and run the following:

```bash
pip install numpy pandas gensim implicit seaborn matplotlib scikit-learn
```

---

## ▶️ Cara Menjalankan / How to Run

### 🇮🇩 Bahasa Indonesia
1. Clone repository ini ke komputer Anda.
2. Letakkan dataset `amazon.csv` di folder proyek atau Google Drive (untuk Colab).
3. Jalankan notebook atau file Python (`Word2vec&ALS.ipynb`).
4. Sistem akan:
   - Melatih Word2Vec pada deskripsi produk
   - Melatih model ALS pada matriks interaksi
   - Memberikan rekomendasi produk

### 🇬🇧 English
1. Clone this repository to your computer.
2. Place the `amazon.csv` dataset inside the project folder or Google Drive (for Colab).
3. Run the notebook or Python file (`Word2vec&ALS.ipynb`).
4. The system will:
   - Train Word2Vec on product descriptions
   - Train ALS on interaction matrix
   - Generate product recommendations

---

## 📂 Struktur Proyek / Project Structure

```bash
.
├── Word2vec&ALS.ipynb   # Notebook utama / Main notebook
├── amazon.csv           # Dataset produk / Product dataset
├── README.md            # Dokumentasi bilingual / Bilingual documentation
```

---

## 📜 Lisensi / License
MIT License – silakan gunakan dan modifikasi untuk keperluan riset atau proyek Anda.  
MIT License – feel free to use and modify for your research or projects.
