
# 🌾 Tarım Drone'u Simülasyonu / *Agricultural Drone Simulation*

Bu proje, **pekiştirmeli öğrenme (Q-learning)** algoritmasıyla çalışan bir tarım drone'unun simülasyonudur. Amaç, **hastalıklı bitkileri tespit etmek**, **batarya yönetimi sağlamak** ve **görev sonunda şarj istasyonuna dönmektir.**

*This project is a simulation of an agricultural drone powered by reinforcement learning (Q-learning) algorithm. The goal is to detect diseased plants, manage battery usage, and return to the charging station at the end of the mission.*
---

## 🚀 Özellikler / *Features*

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


- *6x6 grid-based farming area*
- *3 cell types:*  
  - *`0`:Empty space*  
  - *`1`: S Healthy plant*  
  - *`2`:  Diseased plant*
- *Battery management (2.5% consumption, 8% charge)*
- *Local 3x3 vision area*
- *Advanced reward and penalty system*
- *Q-learning based intelligent agent*
- *Realistic visualization (OpenCV)*
- *Training and testing modes**

---

## 🧠 Öğrenme Bileşenleri /*Learning Components*

### 📦 Durum (*State*)
```python
{
  "pozisyon": [y, x],           # Drone position
  "ziyaret_edilen": 6x6 matris, # Visited cells matrix
  "yerel_gorunum": 3x3 matris,  # Local view matrix
  "batarya": [0-100],           # Battery percentage
  "sarjdan_beri_adim": int,     # Steps since last charge
  "hastalikli_tespit": [0-1]    # Disease detection ratio
}
```

---

### 🎯 Aksiyonlar/ *Actions*

| Kod/*code* | Aksiyon/ *Action* |
|-----|---------|
| 0   | Yukarı /*Up* |
| 1   | Aşağı /*Down*   |
| 2   | Sol / *Left*   |
| 3   | Sağ / *Right*   |
| 4   | Şarj /*Charge*   |

---

### 🏆 Ödül Sistemi / *Reward System*

| Durum / *Condition*                    | Ödül   / *Reward*  |
|--------------------------|----------|
| Hastalıklı bitki tespiti / *Diseased plant detection*	 | +300     |
| Şarj istasyonuna dönüş / *Return to charging station*	   | +200     |
| Boş alan keşfi /*Empty space discovery*         | +20      |
| Sağlıklı bitki /*Healthy plant*         | +10      |
| Şarj etme /*Charging*           | +10~15   |
| Batarya bitmesi / *Battery depletion*        | -150     |
| Tekrar ziyaret /*Revisit*       | -15      |

---

## ⚙️ Kurulum/ *Installation*

Gerekli kütüphaneleri yüklemek için: / *To install required libraries:*

```bash
pip install numpy matplotlib opencv-python gym
```

---


## 📂 Dosya Yapısı/ *File Structure*

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

## 🔧 Hiperparametreler /*Hyperparameters*

| Parametre   /* Parameter   *    | Değer   /*Value*   |
|-------------------|-------------|
| α (öğrenme oranı / *learning rate*)	 | 0.15        |
| γ (indirim oranı / *discount factor)*	 | 0.92        |
| ε (keşif oranı / *exploration rate)*  | 1.0 → 0.01  |
| Batarya tüketimi / *Battery consumption* | %2.5/adım / *per move* |
| Şarj hızı / *Charging rate*     | %8/adım / *per step*   |

---

## 📊 Performans Metrikleri / *Performance Metrics*

**Başarı Puanı** hesaplaması:/ ***Success Score** calculation:*

```text
Başarı Puanı = %70 * Tespit Oranı + %30 * Eve Dönüş Oranı

*Success Score = 70% * Detection Rate + 30% * Return-to-Base Rate*

```

- **Tespit Oranı** = Bulunan hastalıklı bitki sayısı / Toplam hastalıklı bitki sayısı
- ***Detection Rate** = Detected diseased plants / Total diseased plants*
- **Eve Dönüş Oranı** = Görev sonunda şarj istasyonuna güvenli dönüş yüzdesi
- ***Return-to-Base Rate** = Percentage of safe returns to charging station at mission end*
  
---

## 📸 Görselleştirme/ *Visualization*

Drone’un hareketleri ve çevresi her adımda **OpenCV** ile güncellenerek görselleştirilir.

- Drone’un anlık konumu  
- Batarya durumu  
- Tespit edilen hastalıklı bitkiler  
- Grid haritası  

görsel olarak izlenebilir.


*Drone movements and environment are visualized in real-time using **OpenCV** at each step.*

- *Drone's current position*
- *Battery status*
- *Detected diseased plants*
- *Grid map*

---

## 👤 Geliştirici/ *Developer*

**Ayşenur Yıldız**
