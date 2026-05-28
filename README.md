# Implementasi Medallion Architecture pada Ekosistem Apache Spark dan Kafka untuk Inovasi Pemeliharaan Prediktif Industri 4.0 (Studi Kasus: NASA CMAPSS)

[![Spark Version](https://img.shields.io/badge/Apache%20Spark-3.5.5-orange?logo=apachespark)](https://spark.apache.org/)
[![Kafka Version](https://img.shields.io/badge/Apache%20Kafka-7.3.0-black?logo=apachekafka)](https://kafka.apache.org/)
[![MinIO](https://img.shields.io/badge/Object%20Storage-MinIO-blue?logo=minio)](https://min.io/)
[![Python Version](https://img.shields.io/badge/Python-3.9+-blue.svg?logo=python)](https://python.org)

Repositori ini berisi implementasi *data pipeline* end-to-end berbasis streaming real-time untuk **Predictive Maintenance (PdM)** menggunakan dataset **NASA C-MAPSS**. Proyek ini disusun untuk memenuhi Tugas Besar mata kuliah **Analisis Big Data** (Sains Data, Institut Teknologi Sumatera). Kami menerapkan **Medallion Architecture** (Bronze, Silver, dan Gold Layers) guna mengolah data telemetri sensor masif secara andal, hemat memori, dan terdistribusi.

---

## 👥 Identitas Kelompok 20 RB
| No | Nama Peran | NIM | Username GitHub |
|---|---|---|---|
| 1 | Reynaldi Rahmad | 122450088 | [@reyrhmdd](https://github.com/reyrhmdd) |
| 2 | Cindy Laura Manik | 123450112 | [@CindyLauraManik](https://github.com/CindyLauraManik) |
| 3 | Dharu Cahyoaji Sasongko | 123450023 | [@DaruCahyoaji](https://github.com/DaruCahyoaji) |
| 4 | Natasya Felisita Br Ginting | 123140017 | [@NatasyaFelisitaBrGinting17](https://github.com/NatasyaFelisitaBrGinting17) |

**Tema:** SDGs 9 - Industri, Inovasi, dan Infrastruktur  
**Paper Acuan:** *A Scalable Big Data Framework for Real-Time Predictive Maintenance in Industrial IoT* (Asad et al., 2026).

---

## 🏗️ Arsitektur Sistem
Proyek ini mengintegrasikan komponen data engineering modern untuk mensimulasikan lingkungan IoT Pabrik pintar:
1. **Data Ingestion Layer (Kafka):** Mengalirkan data sensor C-MAPSS baris demi baris menyerupai sensor fisik dengan delay teratur.
2. **Bronze Layer (MinIO):** Menyimpan data mentah dari Kafka apa adanya ke dalam format Parquet (Immutable Raw Data Storage).
3. **Silver Layer (MinIO):** Melakukan pembersihan data, eliminasi sensor redundan/konstan, penanganan missing values, dan normalisasi (Min-Max Scaling) terdistribusi via PySpark.
4. **Gold Layer (Prediction Engine):** Membentuk *sliding window/time-steps* sekuensial secara real-time dan mengumpankannya ke dalam model **Deep Learning LSTM (.h5)** menggunakan Spark UDF untuk memprediksi Remaining Useful Life (RUL) mesin.

---

## 📁 Struktur Direktori Proyek
```text
├── dataset_cmapss/          # Tempat menyimpan file train_FD001.txt s.d train_FD004.txt
├── models/                  # Direktori penyimpanan file model LSTM (.h5)
├── docker-compose.yml       # Konfigurasi orkestrasi Kafka, Zookeeper, dan MinIO
├── producer.py              # Script Kafka Producer (IoT Simulator)
├── spark_pipeline.py        # Script Utama PySpark Structured Streaming (Medallion Layers)
└── README.md                # Dokumentasi Proyek
