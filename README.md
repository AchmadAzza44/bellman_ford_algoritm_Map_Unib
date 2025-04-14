# 🏫 UNIB Navigator: Sistem Pencari Jalur Kampus Berbasis AI

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Sistem cerdas untuk menemukan rute optimal di lingkungan kampus Universitas Bengkulu menggunakan algoritma Bellman-Ford dengan adaptasi waktu nyata.

![Demo Aplikasi](demo.gif) *(Contoh tampilan aplikasi)*

## 🌟 Fitur Utama

- **Pencarian Jalur Optimal** berdasarkan waktu tempuh atau jarak
- **Adaptasi Waktu Nyata**:
  - Penutupan gerbang setelah jam operasional
  - Perbedaan rute weekday vs weekend
- **Multi-Mode Transportasi**:
  - 🚗 Mobil
  - 🏍 Motor
  - 🚶 Jalan Kaki
- **Visualisasi Interaktif** dengan peta Folium
- **Integrasi OpenRouteService** untuk akurasi tinggi

## 🛠 Teknologi

| Komponen           | Teknologi               |
|--------------------|-------------------------|
| Algoritma          | Bellman-Ford            |
| GUI                | Tkinter                 |
| Visualisasi Peta   | Folium + OpenStreetMap  |
| Geolokasi          | OpenRouteService API    |
| Bahasa Pemrograman | Python 3.8+             |

## 📥 Instalasi

1. Clone repository:
   ```bash
   git clone https://github.com/username/unib-navigator.git
   cd unib-navigator
 Install dependencies:
pip install -r requirements.txt
Dapatkan API Key dari OpenRouteService dan simpan di ORS_API_KEY (baris 10)
🚀 Penggunaan
Jalankan aplikasi:
python unib_navigator.py

Alur Penggunaan:

Pilih titik awal dari dropdown

Pilih tujuan

Tentukan jenis kendaraan

Klik "Cari Jalur"

Lihat hasil di peta dan detail rute

🗺 Struktur Data
Contoh Representasi Graf
"Gedung A": [
    ("Gedung B", {"jarak": 400, "waktu": 240}),
    ("Masjid", {"jarak": 200, "waktu": 120, "kendaraan": ["Jalan Kaki"]})
]

Atribut Edge:
jarak: Meter

waktu: Detik

kendaraan (opsional): Daftar kendaraan yang diperbolehkan

⏱ Algoritma
Bellman-Ford dipilih karena:

Dapat menangani bobot negatif (fleksibel untuk pengembangan)

Sederhana namun powerful untuk graf ukuran medium

Mudah diimplementasikan dengan Python dasar
def bellman_ford(graph, start, goal, weight_type="waktu"):
    # Inisialisasi
    distance = {node: float('inf') for node in graph}
    predecessor = {node: None for node in graph}
    distance[start] = 0
    
    # Relaksasi edge
    for _ in range(len(graph) - 1):
        for node in graph:
            for neighbor, attr in graph[node]:
                if distance[node] + attr[weight_type] < distance[neighbor]:
                    distance[neighbor] = distance[node] + attr[weight_type]
                    predecessor[neighbor] = node
    ...
    📊 Studi Kasus
Kasus 1: Rute Cepat ke Kelas
Input:

Asal: Gerbang Depan

Tujuan: Gedung F

Waktu: Senin, 07.45

Kendaraan: Motor

Output Sistem:
Rute: Gerbang Depan → MAKSI → Gedung B → Gedung F
Estimasi: 6 menit
Kasus 2: Akses Malam Hari
Input:

Asal: Rektorat

Tujuan: Gerbang Belakang

Waktu: Sabtu, 20.30

Kendaraan: Jalan Kaki

Adaptasi Sistem:

Menutup gerbang depan

Mengarahkan melalui GSG → Dekanat Teknik

🛠 Pengembangan
Todo List:
Tambahkan data bangunan baru

Implementasikan A* untuk performa lebih baik

Sistem caching untuk rute populer

Tambahkan mode wheelchair-friendly
