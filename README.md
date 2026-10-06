# Sade IPA

Türkçe, sade bir iPhone arayüzü: IPA dosyası seçme, yükleme, imzayı yenileme ve gerçek profil bitiş tarihinden kalan süreyi gösterme. Kişisel kullanım için SideStore üzerine hazırlanmış bir uyarlamadır.

## IPA üret

**Actions → Sade IPA derle → Run workflow → main → Run workflow** yolunu kullan. Derleme başarıyla tamamlandığında çalıştırma sayfasının **Artifacts → SadeIPA** bölümünden paketi indir ve ZIP'i aç. `SadeIPA.ipa`, Windows'ta iloader ile kendi ücretsiz Apple hesabın kullanılarak imzalanıp kurulmalıdır.

**Kaynak paketi bir IPA değildir.** iOS derlemesi, hesap girişi, yükleme, kendini yenileme ve iPhone 16 / iOS 27.0.1 uyumluluğu gerçek cihazda ayrıca doğrulanmalıdır.

## Kaynak düzeni

`SadeIPA-Cloud.zip` kaynak ve derleme betiklerini içerir. Akış SHA-256 kontrolünden sonra ZIP'i açar, SideStore 0.7.0-alpha'nın sabit commit'ini ve alt modüllerini indirir, arayüz değişikliklerini uygular, sayaç testlerini çalıştırır ve iOS paketini üretir.

ZIP'i açarak `upstream.json`, `upstream.patch`, `overlay/`, `scripts/`, `Package.swift` ve testleri inceleyebilirsin. Tam kaynağı yeniden oluşturmak için ayıklanan klasörde `python3 scripts/fetch-upstream.py` çalıştır. Mac ve Xcode ile `bash scripts/build-macos.sh` derlemeyi yapar. Özel arayüz `SideStore/AltStore/My Apps/SadeUI/` içine eklenir.

Apple hesabı, parola, sertifika ve cihaz eşleştirme dosyaları bulut derlemesine verilmez. Bunlar ilk telefon kurulumunda iloader ve uygulamanın mevcut SideStore ayarları üzerinden yönetilir.

## İlk telefon kurulumu

1. Windows'a [resmî iloader](https://iloader.app/) ve [gerekli Apple USB sürücülerini](https://docs.sidestore.io/docs/installation/prerequisites) kur.
2. Telefonu USB ile bağla ve bilgisayara güven. iloader'da kendi IPA dosyanı yükleme akışıyla **SadeIPA.ipa** seç.
3. iPhone'da geliştirici hesabına güven ve istenirse Geliştirici Modu'nu aç.
4. iloader **Manage Pairing File → Export** ile dosyayı `ALTPairingFile.mobiledevicepairing` adıyla kaydet. iTunes **Dosya Paylaşımı → Sade IPA → Dosya Ekle** üzerinden aktar. Uygulamanın adı değiştiği için iloader'ın otomatik SideStore listesinde görünmeyebilir.
5. App Store'dan LocalDevVPN kur. Wi-Fi ve VPN açıkken **Ayarlar → Hesap ve kurulum** üzerinden aynı Apple hesabıyla giriş yap.
6. Önce yükleyicinin kendi imzasını yenile ve başarıyı kontrol et. Bilgisayar bağlantısını çıkardıktan sonra telefondan yenilemeyi doğrula.

Adım adım [iPhone kurulum rehberi](IPHONE-KURULUM.md).

Ücretsiz hesapta imza 7 gün sürer ve yükleyici dahil 3 aktif uygulama sınırı vardır. Süre dolmadan yenile. iOS arka plan çalışmasını planladığı için belirli bir gün veya saatte otomatik yenileme garantisi yoktur. iOS güncellemesi, eşleştirme sorunu veya yükleyicinin imzasının dolması tekrar bilgisayar kullanımını gerektirebilir.

## Lisans

Altyapı: [SideStore 0.7.0-alpha](https://github.com/SideStore/SideStore/releases/tag/0.7.0-alpha), commit `6032424a0e56c1c319762e786099bdd9186a238b`. Bu sürüm, Apple tarafındaki değişiklik sonrası 0.6.4 ve önceki sürümlerde oluşan giriş sorununu düzeltir.

Özgün telif bildirimleri korunur. Uyarlama **AGPL-3.0** kapsamındadır; tam metin `LICENSE` dosyasında ve kaynak paketindedir. Bu proje resmî SideStore dağıtımı değildir. SideStore'un bundle kimliği korunur; mevcut SideStore'u değiştirebilir. Upstream uygulama güncellemesi özel arayüzü geri getirebilir.
