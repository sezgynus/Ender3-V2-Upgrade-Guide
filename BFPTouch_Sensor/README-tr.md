# BFPTouch Sensör Kurulumu — Ender 3 V2

[English](README.md) | [Türkçe](README-tr.md) | [← Ana Kılavuz](../README-tr.md)

![BFPTouch demonstrasyonu](Photos/2.gif)

Bu kılavuz, Ender 3 V2 üzerinde uygulanmış BFPTouch kurulumunu belgeler. Modifikasyon; **3D baskılı montaj parçası**, **SG90 servo motor** ve **optik endstop** kullanarak BLTouch benzeri prob işlevi sağlar; aynı zamanda kontrolcüsüz BFPTouch tasarımının donanım ve firmware farklarını dikkate alır.

## Hızlı Bakış

| Alan | Uygulama |
|---|---|
| Hedef yazıcı | Creality Ender 3 V2 |
| Prob yaklaşımı | BFPTouch / BLTouch benzeri tabla probu |
| Hareket elemanı | SG90 servo |
| Algılama | Optik endstop |
| Montaj | 3D baskılı, sıkı geçme |
| Anakart bağlantıları | V, G, IN, OUT |
| Firmware seçenekleri | Önceden yapılandırılmış firmware veya manuel Marlin yapılandırması |

## BFPTouch ile BLTouch Arasındaki Fark

BLTouch kendi kontrol elektroniğine sahiptir. Yazıcıdan gönderilen servo açı komutları sensör tarafından belirli işlemlere karşılık gelen komutlar olarak yorumlanır.

Bu projede kullanılan BFPTouch üzerinde bir kontrolcü bulunmaz. Bu nedenle anakarttan gelen servo sinyali **SG90 açısını doğrudan** kontrol eder. BLTouch için komut anlamına gelen açılar BFPTouch mekanizmasını istenmeyen konumlara götürebilir veya mekanik çarpışmaya neden olabilir.

<img src="Photos/6.png" width="800" />

Bu nedenle BFPTouch, standart BLTouch komut-açı davranışının doğrudan varsayılması yerine doğrudan servo hareketine uygun firmware davranışı gerektirir.

## Gerekli Donanım

- **3D baskılı BFPTouch montaj parçası**
  - Model: [Thingiverse 6918868](https://www.thingiverse.com/thing:6918868)
  - PLA veya PETG kullanılabilir.
- **1 × SG90 servo motor**
- **1 × optik endstop**
- Gerektiğinde havya, lehim ve flux
- Tornavida, pense ve kablo bağı

## Donanım Kurulumu

### 1. Montaj Parçasını Basın

Referans verilen BFPTouch montaj parçasını; servo, optik endstop ve yazıcıya sıkı geçme bağlantısı için yeterli ölçü kalitesinde basın.

### 2. Probu Monte Edin

SG90 servo ve optik endstopu ilgili yuvalarına yerleştirin. Kabloları yazıcının hareketine müdahale etmeyecek şekilde yönlendirin.

### 3. Yazıcıya Takın

Toplanan BFPTouch'u montaj parçasının sıkı geçme tasarımıyla Ender 3 V2'ye takın ve mekanik olarak sağlam olduğunu doğrulayın.

<p>
  <img src="Photos/4.jpg" width="200" />
  <img src="Photos/2.jpg" width="200" />
  <img src="Photos/3.gif" width="266" />
</p>

### 4. Anakart Bağlantılarını Yapın

| Anakart pini | BFPTouch bağlantısı |
|---|---|
| V | SG90 VCC + optik endstop VCC |
| G | SG90 GND + optik endstop GND |
| IN | SG90 PWM sinyali |
| OUT | Optik endstop çıkışı |

Enerji vermeden önce bağlantıları ve izolasyonu doğrulayın.

## Firmware Yapılandırması

Bu modifikasyon için iki firmware yolu belgelenmiştir.

### Seçenek 1 — Önceden Yapılandırılmış Firmware

Önceden yapılandırılmış firmware uygulaması ayrı [Ender3V2S1 deposunda](https://github.com/sezgynus/Ender3V2S1) bulunmaktadır.

Bu seçenek firmware değişikliklerini manuel olarak tekrar etmeyi gerektirmez.

### Seçenek 2 — Manuel Marlin Yapılandırması

BFPTouch, yukarıda açıklanan doğrudan SG90 hareketine uygun Marlin yapılandırması gerektirir. Bu depo donanım gereksinimlerini ve standart BLTouch servo-açı varsayımlarının neden değiştirilmeden kullanılamayacağını belgeler.

Ayrıntılı manuel Marlin parametre seti **bu depoda bulunmadığından**, belgelenmemiş değerler özellikle türetilmemiştir.

## Doğrulama Materyalleri

Depoda uygulanmış proba ait çeşitli fotoğraf ve GIF demonstrasyonları bulunmaktadır:

| Materyal | Amaç |
|---|---|
| `Photos/1.gif` | BFPTouch demonstrasyonu |
| `Photos/2.gif` | Kılavuzun üst kısmında kullanılan ana demonstrasyon |
| `Photos/1.jpg`–`Photos/5.jpg` | Fiziksel kurulum referansları |
| `Photos/3.gif` | Yakın montaj/mekanik referansı |
| `Photos/6.png` | Kontrol farkını açıklamak için kullanılan BLTouch komut/açı referansı |

## Güvenlik ve Mekanik Kontroller

Homing veya probing işleminden önce:

- probun herhangi bir parçaya çarpmadan açılıp kapanabildiğini doğrulayın;
- optik endstop durumunun doğru değiştiğini kontrol edin;
- kabloların hareket alanına girmediğinden emin olun;
- otomatik Z hareketine güvenmeden önce servo hareketini kontrollü biçimde test edin.

Doğrudan servo kontrol farkı önemlidir: başka bir prob mekanizmasına ait firmware ayarlarının mekanik olarak güvenli olduğu doğrulama yapılmadan varsayılmamalıdır.

## Proje Kapsamı

Bu alt kılavuz, depoda şu anda bulunan materyalle desteklenen BFPTouch donanım uygulamasını ve firmware yaklaşımını belgeler. Belgelenmemiş kalibrasyon değerleri veya Marlin parametreleri eklenmemiştir.

[← Ana yükseltme kılavuzuna dön](../README-tr.md)
