
# 🌾 Gelişmiş Tarım Drone'u Simülasyonu

Bu proje, **pekiştirmeli öğrenme (Q-learning)** algoritmasıyla çalışan bir tarım drone'unun simülasyonudur. Amaç, **hastalıklı bitkileri tespit etmek**, **batarya yönetimi sağlamak** ve **görev sonunda şarj istasyonuna dönmektir**.

---

## 🚀 Özellikler

- 6x6 grid tabanlı tarım alanı
- 3 tür hücre:  
  - `0`: Boş alan  
  - `1`: Sağlıklı bitki  
  - `2`: Hastalıklı bitki
- Batarya yönetimi (%2.5 tüketim, %8 şarj)
- Yerel 3x3 görüş alanı
- Gelişmiş ödül ve ceza sistemi
- Q-learning tabanlı akıllı ajan
- Gerçekçi görselleştirme (OpenCV)
- Eğitim ve test modları

---

## 🧠 Öğrenme Bileşenleri

### 📦 Durum (State)
```python
{
  "pozisyon": [y, x],
  "ziyaret_edilen": 6x6 matris,
  "yerel_gorunum": 3x3 matris,
  "batarya": [0-100],
  "sarjdan_beri_adim": int,
  "hastalikli_tespit": [0-1]
}
```

---

### 🎯 Aksiyonlar

| Kod | Aksiyon |
|-----|---------|
| 0   | Yukarı  |
| 1   | Aşağı   |
| 2   | Sol     |
| 3   | Sağ     |
| 4   | Şarj    |

---

### 🏆 Ödül Sistemi

| Durum                     | Ödül     |
|--------------------------|----------|
| Hastalıklı bitki tespiti | +300     |
| Şarj istasyonuna dönüş   | +200     |
| Boş alan keşfi           | +20      |
| Sağlıklı bitki           | +10      |
| Şarj etme                | +10~15   |
| Batarya bitmesi          | -150     |
| Tekrar ziyaret           | -15      |

---

## ⚙️ Kurulum

Gerekli kütüphaneleri yüklemek için:

```bash
pip install numpy matplotlib opencv-python gym
```

---


## 📂 Dosya Yapısı

```
.
├── images/
│   ├── tarla.png
│   ├── bos.png
│   ├── hastalikli.png
│   ├── drone.png
│   └── sarj.png
├── model/
│   └── q_table.pkl
├── TarimDroneSimulasyonu.ipynb
└── README.md
```

---

## 🔧 Hiperparametreler

| Parametre         | Değer       |
|-------------------|-------------|
| α (öğrenme oranı) | 0.15        |
| γ (indirim oranı) | 0.92        |
| ε (keşif oranı)   | 1.0 → 0.01  |
| Batarya tüketimi  | %2.5/adım   |
| Şarj hızı         | %8/adım     |

---

## 📊 Performans Metrikleri

**Başarı Puanı** hesaplaması:

```text
Başarı Puanı = %70 * Tespit Oranı + %30 * Eve Dönüş Oranı
```

- **Tespit Oranı** = Bulunan hastalıklı bitki sayısı / Toplam hastalıklı bitki sayısı  
- **Eve Dönüş Oranı** = Görev sonunda şarj istasyonuna güvenli dönüş yüzdesi

---

## 📸 Görselleştirme

Drone’un hareketleri ve çevresi her adımda **OpenCV** ile güncellenerek görselleştirilir.

- Drone’un anlık konumu  
- Batarya durumu  
- Tespit edilen hastalıklı bitkiler  
- Grid haritası  

görsel olarak izlenebilir.

---

## 👤 Geliştirici

**Ayşenur Yıldız**

- [LinkedIn](https://www.linkedin.com/in/aysenuryildizz/)
- [GitHub](https://github.com/AysenurYldz)
