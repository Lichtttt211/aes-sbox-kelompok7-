# Konstruksi S-box AES Berbasis SAGA (Versi 2 Model ML) untuk Enkripsi Citra

**Proyek Akhir Mata Kuliah Kriptografi — Kelompok 7**

## Anggota Kelompok 7

| No | Nama | NIM | Pembagian Tugas Utama |
|---|---|---|---|
| 1 | **Cahya Din Ramadhan** | `2404130018` | Eksplorasi 30 polinomial irreducible $\text{GF}(2^8)$, dataset bit-plane Mandrill, & perbandingan **2 model ML** (`KNN` baseline vs `Ridge Komposit Row+Pairwise-XOR`) |
| 2 | **Muhammad Nabil Fikri** | `2404130167` | Optimasi multi-objektif *Surrogate-Assisted Genetic Algorithm* (SAGA), optimasi konstanta $C$, konstruksi `S-box K7`, & uji dasar (Balance, Bijective, NL, SAC) |
| 3 | **Fathan Nabil Rahman** | `2404130140` | Uji lanjutan (BIC-NL, BIC-SAC, LAP, DAP, FP/OFP, Siklus) & komparasi terhadap AES, Alamsyah (2023), & Alamsyah (2025) `S-box₄₄` |
| 4 | **Rashya Farellyndo Revanza** | `2404130132` | Implementasi AES-128 T-table (FIPS-197), mode CBC dua arah (*domain-separated IV*), enkripsi citra, Histogram ($\chi^2$), Entropy, Korelasi H/V/D, NPCR, & UACI |

## 2 Model Machine Learning yang Dibandingkan

1. **KNN Regressor (64-bit mentah) — *Baseline***: melatih KNN langsung pada 64 bit matriks affine ($R^2 \approx 0{,}075$ di SAC, $-0{,}049$ di BIC-SAC).
2. **Ridge Regression Komposit (`Row + Pairwise-XOR`) — *Usulan***: memanfaatkan representasi baris tunggal (untuk SAC) dan 28 pasangan XOR antar-baris (untuk BIC-SAC) sehingga mencapai $R^2 = 1{,}00000$ dan digunakan sebagai *surrogate fitness* cepat di Algoritma Genetik (SAGA).

## Ringkasan Hasil `S-box K7`

- **Polinomial:** `0x17B` ($x^8+x^6+x^5+x^4+x^3+x+1$, peringkat #1 dari 30 polinomial irreducible)
- **Konstanta $C$:** `0xEE` (`238`)
- **Metrik:** Balance = Ya · Bijective = Ya · NL = `112` · SAC = `0.50000` (dev `0.01562`) · BIC-NL = `112` · BIC-SAC = `0.50000` (dev `0.00446`) · LAP (bias) = `0.0625` · DAP = `0.015625` · Skor $S = 0.00000$ · Skor $SV = 16.00000$ · FP = `0` · OFP = `0` · Siklus = `1 (256)`

