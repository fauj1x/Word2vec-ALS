
# Word2Vec & ALS Recommendation System


[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1NSxqB5L9jfhpD_Li3IvhwAuaj_0gEHPA?usp=sharing)


## Deskripsi Singkat
Proyek ini membangun sistem rekomendasi produk menggunakan dua pendekatan utama:
1. **Content-Based Filtering (CBF) dengan Word2Vec** → merekomendasikan produk berdasarkan kemiripan deskripsi teks produk.
2. **Collaborative Filtering (CF) dengan ALS (Alternating Least Squares)** → merekomendasikan produk berdasarkan pola interaksi user–produk.
3. **Hybrid Recommendation** → menggabungkan kedua pendekatan dengan bobot tertentu (alpha).

Proyek juga dilengkapi dengan visualisasi bar chart untuk setiap metode.

---

## Alur Kerja Sistem

### 1. Persiapan & Import Library
- Menginstal dan memuat library: `numpy`, `pandas`, `gensim`, `implicit`, `matplotlib`, `sklearn`, dll.
- Memastikan dataset tersedia (`amazon.csv`) dengan kolom utama: `user_id`, `product_name`, `about_product`, dan `rating`.

### 2. Preprocessing Data
- Membersihkan kolom `about_product`. Jika tidak ada, digunakan fallback (`description`, dll.) atau `product_name`.
- Membersihkan kolom `rating` → hanya angka (contoh: "4.0 out of 5" → 4.0).
- Menghapus baris yang memiliki nilai kosong pada kolom penting.

### 3. Content-Based Filtering (Word2Vec)
- **Tokenisasi**: deskripsi produk diubah menjadi daftar kata (lowercase, hanya huruf/angka).
- **Training Word2Vec**: menghasilkan embedding (vektor representasi) untuk setiap kata.
- **Representasi Produk**: vektor produk = rata-rata vektor kata deskripsi produk.
- **Rekomendasi**: dihitung **cosine similarity** antar produk → pilih `top_k` produk paling mirip (default 5).
- **Visualisasi**: bar chart vertikal dengan nilai rating produk hasil rekomendasi.

### 4. Collaborative Filtering (ALS)
- Encode `user_id` dan `product_name` menjadi kode numerik (`user_code`, `item_code`).
- Membentuk **matrix user–item** berbentuk sparse.
- Melatih model ALS untuk mempelajari pola interaksi user–produk.
- Fungsi `als_recommend(user_id, top_k)` → menghasilkan produk rekomendasi berdasarkan prediksi skor preferensi.
- **Visualisasi**: bar chart vertikal skor rekomendasi ALS untuk user tertentu.

### 5. Hybrid Recommendation
- Menggabungkan skor **similarity (CBF)** dan **prediksi ALS (CF)** dengan formula:
  ```
  hybrid_score = alpha * cbf_score + (1 - alpha) * cf_score
  ```
  - `alpha = 0.5` → kontribusi CBF dan CF seimbang.
  - `alpha = 1.0` → hanya CBF.
  - `alpha = 0.0` → hanya CF.
- Menghasilkan rekomendasi `top_k` produk teratas.
- **Visualisasi**: bar chart vertikal skor hybrid.

### 6. Evaluasi Produk
- Menampilkan **Top 5** dan **Bottom 5** produk berdasarkan rata-rata rating dari dataset.
- Visualisasi bar chart produk dengan rating tertinggi dan terendah.

---

## Output yang Dihasilkan
1. **Content-Based Recommendations**: daftar produk mirip + rating.
```
=== Content-Based: Word2Vec ===
Product embeddings shape: (1464, 100)
Example content-based recommendations for: Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini (3 FT Pack of 1, Grey)
                                          product_name  rating
369  Wayona Nylon Braided USB to Lightning Fast Cha...     4.2
614  Wayona Nylon Braided USB to Lightning Fast Cha...     4.2
220  Wayona Nylon Braided Usb Syncing And Charging ...     4.2
80   Wayona Usb Nylon Braided Data Sync And Chargin...     4.2
430  USB Charger, Oraimo Elite Dual Port 5V/2.4A Wa...     4.0

```
2. **ALS Recommendations**: daftar produk untuk user tertentu + skor prediksi.
```
=== Collaborative Filtering: ALS (implicit) ===
Ratings matrix shape (users x items): (1193, 1336)

[Warning] OpenBLAS is configured to use 2 threads. 
It is highly recommended to disable its internal threadpool 
by setting the environment variable 'OPENBLAS_NUM_THREADS=1' 
or by calling 'threadpoolctl.threadpool_limits(1, "blas")'.
Having OpenBLAS use a threadpool can lead to severe performance issues.

[Warning] Method expects CSR input, and was passed coo_matrix instead. 
Converting to CSR took 0.0003369 seconds.

Training ALS model: 100% | 20/20 [00:00<00:00, 39.47it/s]

ALS recommendations (name, score):
1. Redmi Note 11T 5G (Stardust White, 6GB RAM, 128GB ROM) | Dimensity 810 5G | 33W Pro Fast Charging | Charger Included | Additional Exchange Offers | Get 2 Months of YouTube Premium Free!
   → 0.1219
2. MYVN LTG to USB for Fast Charging & Data Sync USB Cable Compatible for iPhone 5/5s/6/6S/7/7+/8/8+/10/11, iPad Air/Mini, iPod and iOS Devices (1 M)
   → 0.1113
3. Acer 80 cm (32 inches) N Series HD Ready TV AR32NSV53HD (Black)
   → 0.1098
4. BRUSTRO Copytinta Coloured Craft Paper A4 Size 80 GSM Mixed Bright Colour 40 Sheets Pack (10 cols X 4 Sheets) Double Side Color for Office Printing, Art and Craft.
   → 0.0849
5. Sujata Powermatic Plus, Juicer Mixer Grinder with Chutney Jar, 900 Watts, 3 Jars (White)
   → 0.0796


```
3. **Hybrid Recommendations**: daftar gabungan dengan skor hybrid.
```
=== Hybrid Recommendations ===

1. MYVN LTG to USB for Fast Charging & Data Sync USB Cable Compatible for iPhone 5/5s/6/6S/7/7+/8/8+/10/11, iPad Air/Mini, iPod and iOS Devices (1 M)
   → 0.5441

2. Acer 80 cm (32 inches) N Series HD Ready TV AR32NSV53HD (Black)
   → 0.5423

3. Brayden Chopro, Electric Vegetable Chopper for Kitchen with 500 ML Capacity, 
   400 Watts Copper Motor and 4 Bi-Level SS Blades (Black)
   → 0.5314

4. Amazon Basics USB 3.0 Cable - A Male to Micro B - 6 Feet (1.8 Meters), Black
   → 0.5305

5. VU 164 cm (65 inches) The GloLED Series 4K Smart LED Google TV 65GloLED (Grey)
   → 0.5251

```
4. **Top/Bottom Products**: daftar produk dengan rata-rata rating tertinggi dan terendah.
```
=== Evaluation & Summary ===

Top 5 Products by Mean Rating:
1. Amazon Basics Wireless Mouse | 2.4 GHz Connection, 1600 DPI | Type-C Adapter | 
   Up to 12 Months of Battery Life | Ambidextrous Design | Suitable for PC/Mac/Laptop
   → 5.0

2. Syncwire LTG to USB Cable for Fast Charging Compatible with Phone 5/5C/5S/6/6S/7/8/X/XR/XS Max/11/12/13 Series 
   and Pad Air/Mini, iPod & Other Devices (1.1 Meter, White)
   → 5.0

3. REDTECH USB-C to Lightning Cable 3.3FT, [Apple MFi Certified] Lightning to Type-C Fast Charging Cord 
   Compatible with iPhone 14/13/13 Pro/Max/12/11/X/XS/XR/8, Supports Power Delivery - White
   → 5.0

4. Instant Pot Air Fryer, Vortex 2QT, Touch Control Panel, 360° EvenCrisp™ Technology, Uses 95% Less Oil, 
   4-in-1 Appliance: Air Fry, Roast, Bake, Reheat (Vortex 1.97Litre, Black)
   → 4.8

5. Swiffer Instant Electric Water Heater Faucet Tap Home-Kitchen Instantaneous Water Heater Tankless for Tap, 
   LED Electric Head Water Heaters Tail Gallon Comfort (3000W) (Pack of 1)
   → 4.8


Bottom 5 Products by Mean Rating:
1. Khaitan ORFin Fan Heater for Home and Kitchen-K0 2215
   → 2.0

2. Personal Size Blender, Portable Blender, Battery Powered USB Blender, with Four Blades, 
   Mini Blender Travel Bottle for Juice, Shakes, and Smoothies (Pink)
   → 2.3

3. Green Tales Heat Seal Mini Food Sealer - Impulse Machine for Sealing Plastic Bags Packaging
   → 2.6

4. SHREENOVA ID116 Plus Bluetooth Fitness Smart Watch for Men, Women, and Kids Activity Tracker (Black)
   → 2.8

5. MR. BRAND Portable USB Juicer Electric USB Juice Maker Mixer Bottle Blender Grinder Mixer, 
   6 Blades Rechargeable Bottle (Multi Color) (MULTI MIXER 6 BLED)
   → 2.8

```
5. **Visualisasi**: bar chart untuk setiap hasil rekomendasi.
<img width="994" height="590" alt="image" src="https://github.com/user-attachments/assets/14dde5ef-4890-447e-9ae5-71c5693b6a34" />
<img width="996" height="590" alt="image" src="https://github.com/user-attachments/assets/a5f69071-bba3-4c8b-bf3a-a4fdb6d8fd1c" />
<img width="1346" height="590" alt="image" src="https://github.com/user-attachments/assets/d2918d57-3852-4c54-980d-cded1111e3b4" />
<img width="1346" height="590" alt="image" src="https://github.com/user-attachments/assets/d9b69af4-a267-49bf-a64d-2a8cb331104d" />
<img width="1560" height="1410" alt="image" src="https://github.com/user-attachments/assets/c7b5f682-2d4c-4dee-9009-bd13ade6dc63" />




---

## Cara Menjalankan
1. Siapkan dataset `amazon.csv` dengan kolom `user_id`, `product_name`, `about_product`, `rating`.
2. Jalankan file Python (`word2vec&als.py`) di Google Colab atau lokal dengan environment yang memiliki dependency.
3. Perhatikan hasil rekomendasi yang ditampilkan di console dan grafik bar chart.
4. Ubah parameter:
   - `top_k` → jumlah rekomendasi yang ingin ditampilkan (default 5).
   - `alpha` → bobot hybrid (0.0 – 1.0).

---

## Kesimpulan
- **Content-Based (Word2Vec)** bekerja baik jika deskripsi produk kaya teks, bisa merekomendasikan produk yang mirip secara konten.  
- **Collaborative Filtering (ALS)** lebih kuat jika data interaksi user–produk cukup besar, mampu menangkap pola preferensi user.  
- **Hybrid Method** menggabungkan kelebihan keduanya → hasil rekomendasi lebih relevan dan seimbang.

---
