# CSigner

Türkçe, sade bir iPhone uygulaması: IPA dosyası seçme, yükleme, imzayı yenileme ve kalan süreyi gösterme. Ücretsiz Apple hesabı ve ücretli Apple Developer hesabı desteklenir. Yazılım & Teknoloji — CSecgin.

CSigner, önceki Sade IPA uygulamasının yeni adıdır. Yeni elma ikonu kırpılmadan gri zemine yerleştirilmiştir. Arayüz açık ve koyu moda uyumlu nötr gri kullanır. Ayarlar ekranındaki kurulum rehberi, altyapı bağlantısı ve hesap değiştirme açıklaması kaldırılmıştır.

**7 Ekim 2026 durumu:** [CSigner derlemesi başarılı](https://github.com/CS3cgin/sade-ipa/actions/runs/37588625691). Xcode 26.4.1 ile IPA üretildi; 15 test, 0 hata. İndirilen IPA'nın SHA-256 manifesti, adı, ana ikonu, arm64 dosyası ve ZIP bütünlüğü doğrulandı. Derlenmiş iPhone/iPad ikonları kaynak görsel boyutlarıyla piksel düzeyinde birebir eşleşti. Yeni görünümün iPhone testi, USB çıkarılmış yenileme, başka IPA yükleme, ücretli hesap ve arka plan yenileme kontrolleri ayrıca yapılmalıdır.

## IPA üret

**Actions → CSigner derle → Run workflow → main → Run workflow** yolunu kullan. Başarılı çalıştırmanın **Artifacts → CSigner** paketini indir ve ZIP'i aç. `CSigner.ipa`, Windows'ta iloader ile kendi Apple hesabın kullanılarak imzalanıp kurulmalıdır.

Mevcut uygulamanın üzerine aynı Apple hesabıyla kur. Uygulamayı önceden silmek gerekmez. Motorun kendi uygulamasını tanıması için bundle kimliği korunmuştur.

## Kaynak düzeni

Depodaki `CSigner-Cloud.part*.b64` dosyaları kaynak ZIP'inin Base64 parçalarıdır. Akış önce bunları `CSigner-Cloud.zip` olarak birleştirir, SHA-256 kontrolünden sonra ZIP'i açar, sabitlenmiş SideStore ve alt modüllerini indirir, değişiklikleri uygular, mevcut sayaç ve ilerleme testlerini çalıştırır ve iOS paketini üretir.

ZIP'i açarak `upstream.json`, `upstream.patch`, `overlay/`, `scripts/`, `Package.swift` ve testleri inceleyebilirsin. Tam kaynağı yeniden oluşturmak için ayıklanan klasörde `python3 scripts/fetch-upstream.py` çalıştır. Mac ve Xcode ile `bash scripts/build-macos.sh` derlemeyi yapar. Özel arayüz `SideStore/AltStore/My Apps/SadeUI/` içinde, ikonlar `SideStore/AltStore/Resources/Icons.xcassets/CSignerIcon.appiconset/` içindedir.

Apple hesabı, parola, sertifika ve cihaz eşleştirme dosyaları bulut derlemesine verilmez.

## Kullanım

İlk kurulum bilgisayardan iloader ile yapılır. Sonraki normal yükleme ve yenilemeler telefonda Wi-Fi ve LocalDevVPN üzerinden çalışır. Apple hesabı ve eşleştirme işlemleri **Ayarlar → Hesap ve kurulum** bölümündedir.

Ücretsiz hesapta CSigner dahil toplam 3 aktif uygulama sınırı ve 7 günlük profil süresi vardır. Ücretli hesabın profil süresi 365 güne kadar çıkabilir. Sayaç ve hatırlatmalar kurulu uygulamanın gerçek profil bitiş tarihini kullanır. Hesap değiştirmek önceki profili uzatmaz; yeni hesapla yenileme gerekir.

Süre dolmadan yenile. iOS arka plan çalışmasını planladığı için belirli bir gün veya saatte otomatik yenileme garantisi yoktur.

## Kaynak ve lisans

CSigner, [SideStore 0.7.0-alpha](https://github.com/SideStore/SideStore/releases/tag/0.7.0-alpha) üzerine hazırlanmış bir uyarlamadır; resmî SideStore dağıtımı değildir. Upstream commit: `6032424a0e56c1c319762e786099bdd9186a238b`.

Özgün telif bildirimleri korunur. Uyarlama **AGPL-3.0** kapsamındadır; tam metin `LICENSE` dosyasında ve kaynak paketindedir. Kaynak kodu bu depodan erişilebilir. İmzalama ve kurulum motoru SideStore'dan gelir. Bundle kimliği `com.SideStore.SideStore` olarak korunur; mevcut SideStore/Sade IPA kurulumunu değiştirebilir.
