
# Dil Seçimi
[English](README.md) | [Türkçe](README-tr.md)

# Ender 3 V2 Yükseltme Kılavuzu

**Ender 3 V2 Yükseltme Kılavuzu**'na hoş geldiniz! Bu depo, Ender 3 V2 3D yazıcınızı harika yükseltmelerle geliştirmek için ayrıntılı talimatlar ve kaynaklar sunar. Her yükseltme, donanım kurulumu, yazılım yapılandırması ve sorunsuz bir deneyim için faydalı ipuçları içerir.

---

## 🚀 Mevcut Yükseltmeler

### [1. **BFPTouch Sensör Kurulumu**](./BFPTouch_Sensor)
3D yazıcınızı daha iyi baskı kalitesi ve kullanım kolaylığı için otomatik tabla hizalama özelliği ile geliştirin.

- **Özellikler**: Daha tutarlı ilk katman, zahmetsiz tabla hizalama.
- **Kaynaklar**: 
  - Kurulum kılavuzu
  - Donanım yapılandırması
  - Kablolama diyagramları
  - Referans için fotoğraflar

### [2. **Kasa Işığı Aktivasyonu ve LED Çıkışı Modifikasyonu**](./Case_Light)
Çalışma alanınızı aydınlatın ve ana kartı LED kontrolü için modifiye edin.

- **Özellikler**: Daha iyi baskı görünürlüğü için entegre aydınlatma.
  - **G-kodu kontrolü**: Kasa ışığını G-kodu ile `M355` komutu ile kontrol edin:
    - **Kullanım**: `M355 [P<byte>] [S<bool>]`
    - **Parametreler**:
      - `[P<byte>]`: Parlaklık faktörünü 0 ile 255 arasında ayarlayın.
      - `[S<bool>]`: Kasa ışığını açın veya kapatın.
    - Detaylı dokümantasyon için [Marlin M355 G-kodu sayfasını](https://marlinfw.org/docs/gcode/M355.html) ziyaret edin.
  - **Esnek kontrol seçenekleri**:
    - Slicer tarafından oluşturulan G-koduna `M355` makroları ekleyerek baskılar sırasında ışık kontrolünü otomatikleştirin.
    - OctoPrint özel kontrol seçeneklerini kullanarak makroyu tetikleyin ve kullanıcı arayüzü üzerinden ışığı ayarlayarak daha fazla esneklik sağlayın.
- **Kaynaklar**:
  - Kablolama modifikasyonları
  - Devre şemaları
  - Kurulum fotoğrafları

### [3. **Filament Sensörü Kurulumu**](./Filament_Sensor)
Filament bittiğinde veya kırıldığında bunu algılayan bir filament sensörü kurarak başarısız baskılardan kaçının.

- **Özellikler**: Gerçek zamanlı filament izleme.
- **Kaynaklar**:
  - Kurulum talimatları
  - Donanım güncellemeleri
  - Devre bağlantıları

---

## 🛠️ Bu Depoda Neler Bulacaksınız?
Bu depo şunları içerir:

1. **Ayrıntılı Talimatlar**: Her yükseltme için adım adım kurulum kılavuzları.
2. **Donanım Kaynakları**: Özelleştirme için önceden derlenmiş donanım ve kaynak kodu.
3. **Devre Diyagramları**: Kablolama ve bağlantılar için net diyagramlar.
4. **Fotoğraflar**: Kurulum sırasında referans için yüksek çözünürlüklü görüntüler.
5. **Sorun Giderme İpuçları**: Yaygın sorunlar ve çözümleri.

---

## 📂 Depo Yapısı
```
📁 Ender3V2_Upgrade_Guide
├── BFPTouch_Sensor
│   ├── README.md
│   ├── README-tr.md
│   ├── Diagrams
│   └── Photos
├── Case_Light
│   ├── README.md
│   ├── README-tr.md
│   ├── HW_Modifications
│   ├── Diagrams
│   └── Photos
├── Filament_Sensor
│   ├── README.md
│   ├── README-tr.md
│   ├── Diagrams
│   └── Photos
├── README.md
└── README-tr.md
```

---

## 📜 Lisans
Bu proje [MIT Lisansı](LICENSE) altında lisanslanmıştır.

---

## 🙌 Katkılar
Katkılar memnuniyetle karşılanır! Yeni yükseltme, iyileştirme veya düzeltme fikirleriniz varsa, bir konu açmaktan veya bir pull request göndermekten çekinmeyin.

---

İyi baskılar! 🎉
