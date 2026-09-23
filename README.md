# Jarvis Assistant — Android Projesi

Bu proje, sesli komutla çalışan, cihaz kontrolü yapabilen ve **şeffaf** otonom
otomasyonlara sahip bir Android asistanının çalışan iskeletidir.

## Neler var

- **Uyanma kelimesi ile dinleme** ("Hey Jarvis") — arka planda foreground service
  olarak çalışır.
- **Sesli komutla cihaz kontrolü**: Wi-Fi, Bluetooth, fener, ses seviyesi, ekran
  parlaklığı, Rahatsız Etmeyin modu.
- **Erişilebilirlik servisi**: yalnızca kullanıcının verdiği tek seferlik komutu
  uygulamak için (uygulama açma, metin yazma, butona tıklama). Her kullanımda
  bildirimle kullanıcıya haber verilir; arka planda sürekli/gizli ekran okuma
  YAPILMAZ.
- **Görme özelliği** (`VisionAssistant.kt`): kullanıcı sorduğunda tek kareyi
  Claude vision API'sine gönderip açıklatır. Görüntü saklanmaz, periyodik çekim
  yapılmaz.
- **Proaktif ama şeffaf otomasyonlar** (`ProactiveAutomationEngine.kt`):
  - Kulaklık takılınca müzik açma
  - Gece pil düşükken uyarı
  - Takvim etkinliğinde otomatik odaklanma modu
  - **Her kural varsayılan kapalı**, Ayarlar ekranından tek tek açılır, her
    tetiklendiğinde bildirim gösterir ve kullanıcı geri alabilir.

## Kurulum

1. Android Studio'da "Open" ile bu klasörü aç.
2. Gradle senkronizasyonunu bekle.
3. `VisionAssistant` kullanacaksan, kendi API anahtarını güvenli bir şekilde
   (ör. Android Keystore ile şifreli local storage veya kendi sunucu proxy'niz
   üzerinden) enjekte edin — anahtarı asla kaynak koduna gömmeyin.
4. Cihazda çalıştır, gerekli izinleri ver, Erişilebilirlik iznini manuel olarak
   sistem ayarlarından aç.

## Bilinçli olarak eklenmeyenler ve neden

Aşağıdaki özellikler orijinal proje metninde istenmişti ama **kasıtlı olarak
eklenmedi**, çünkü bunlar cihaz sahibinin bilgisi/onayı olmadan çalışacak
şekilde tasarlandığında casus yazılım (stalkerware) ile aynı işlevi görür:

- Yanlış şifre girildiğinde gizlice fotoğraf çekip üçüncü bir cihaza/e-postaya
  gönderme
- Uygulamaları/bildirimleri cihazı elinde tutan kişiden gizleme
- Ekran içeriğini sürekli ve gizlice okuyup/loglama
- Başka bir kişiyi ses klonlamayla taklit ederek üçüncü taraflarla iletişim

Bunun yerine, aynı ihtiyaçları (telefonu bulma, güvenlik) şeffaf ve kullanıcı
onaylı şekilde karşılayan alternatifler için README'nin üstündeki özellik
listesine bakabilir veya bu projeye kendi "Telefonu Bul" modülünüzü (yalnızca
cihaz sahibinin kendi hesabıyla giriş yaptığı bir web paneline konum gösteren)
ekleyebilirsiniz.
