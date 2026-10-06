# Sade IPA

Türkçe, sade bir iPhone arayüzü: IPA dosyası seçme, yükleme, imzayı yenileme ve gerçek profil bitiş tarihinden kalan süreyi gösterme. Ücretsiz Apple hesabı ve ücretli Apple Developer hesabı aynı uygulamada desteklenir. Kişisel kullanım için SideStore üzerine hazırlanmış bir uyarlamadır.

6 Ekim 2026 tarihinde [ilerleme göstergesi düzeltmesini içeren iOS derlemesi başarıyla tamamlandı](https://github.com/CS3cgin/sade-ipa/actions/runs/37520280948): Xcode 26.4.1, 13 sayaç testi, 0 hata; toplam süre 9 dakika 46 saniye. **Artifacts → SadeIPA** paketinde kişisel hesabınla imzalanacak `SadeIPA.ipa` bulunur. IPA'nın SHA-256 değeri `4b3cbaa66e9842fbed10160d6914a8dc4372b4a7a0cf67e8050af54a25f4baf8`; boyutu 27.828.000 bayt.

Görünen ilerleme yüzdesi artık 0–100 aralığında tutulur; son aşamada “Kurulum tamamlanıyor” yazısı çıkar. Sade IPA kendi imzasını yenilerken son aşamada beklerse Ana Ekran'a dönüp 30 saniye bekleyerek yeniden açma açıklaması gösterilir. Düğmeler gerçek işlem tamamlanınca açılır.

Önceki paket iPhone 16 / iOS 27.0.1 üzerinde açıldı; kullanıcı ücretsiz Apple hesabıyla giriş ve eşleştirmeyi tamamladı. Kendi imzasını yenilerken Ana Ekran'da 30 saniye bekleyip yeniden açınca işlem çubuğunun kaybolduğunu ve düğmelerin açıldığını doğruladı. Yeni paketin cihaz testi, USB çıkarılmış yenileme, başka IPA yükleme, ücretli hesap ve arka plan yenileme henüz doğrulanmadı.

## IPA üret

**Actions → Sade IPA derle → Run workflow → main → Run workflow** yolunu kullan. Derleme başarıyla tamamlandığında çalıştırma sayfasının **Artifacts → SadeIPA** bölümünden paketi indir ve ZIP'i aç. `SadeIPA.ipa`, Windows'ta iloader ile kendi Apple hesabın kullanılarak imzalanıp kurulmalıdır.

**Kaynak paketi bir IPA değildir.** Yukarıdaki cihaz gözlemleri tam uyumluluk testi yerine geçmez; kalan kontroller gerçek cihazda yapılmalıdır.

## Kaynak düzeni

`SadeIPA-Cloud.zip` kaynak ve derleme betiklerini içerir. Akış SHA-256 kontrolünden sonra ZIP'i açar, SideStore 0.7.0-alpha'nın sabit commit'ini ve alt modüllerini indirir, arayüz değişikliklerini uygular, sayaç testlerini çalıştırır ve iOS paketini üretir.

ZIP'i açarak `upstream.json`, `upstream.patch`, `overlay/`, `scripts/`, `Package.swift` ve testleri inceleyebilirsin. Tam kaynağı yeniden oluşturmak için ayıklanan klasörde `python3 scripts/fetch-upstream.py` çalıştır. Mac ve Xcode ile `bash scripts/build-macos.sh` derlemeyi yapar. Özel arayüz `SideStore/AltStore/My Apps/SadeUI/` içine eklenir.

Apple hesabı, parola, sertifika ve cihaz eşleştirme dosyaları bulut derlemesine verilmez. Bunlar ilk telefon kurulumunda iloader ve uygulamanın mevcut SideStore ayarları üzerinden yönetilir.

## İlk telefon kurulumu

1. Windows'a [resmî iloader](https://iloader.app/) ve [gerekli Apple USB sürücülerini](https://docs.sidestore.io/docs/installation/prerequisites) kur.
2. Telefonu USB ile bağla ve bilgisayara güven. iloader'da kendi IPA dosyanı yükleme akışıyla **SadeIPA.ipa** seç.
3. iPhone'da geliştirici hesabına güven ve istenirse Geliştirici Modu'nu aç.
4. iloader **Manage Pairing File → Export** ile dosyayı kaydet. `pairingFile.plist` adıyla kaydedildiyse iTunes **Dosya Paylaşımı → Sade IPA → Dosya Ekle** üzerinden aktar; telefonda uygulamayı yeniden açıp eşleştirme dosyası seçicisinden bu dosyayı seç. Alternatif olarak `ALTPairingFile.mobiledevicepairing` adıyla aktarılabilir. Uygulamanın adı değiştiği için iloader'ın otomatik SideStore listesinde görünmeyebilir.
5. App Store'dan LocalDevVPN kur. Wi-Fi ve VPN açıkken **Ayarlar → Hesap ve kurulum** üzerinden aynı Apple hesabıyla giriş yap.
6. Önce yükleyicinin kendi imzasını yenile. Son aşamada beklerse uygulamayı zorla kapatmadan Ana Ekran'a dön, 30 saniye bekle ve tekrar aç. Bilgisayar bağlantısını çıkardıktan sonra telefondan yenilemeyi doğrula.

Adım adım [iPhone kurulum rehberi](IPHONE-KURULUM.md).

## Ücretsiz ve ücretli hesaplar

Hesap türü, imzalama motorunun seçili Apple geliştirici takımından okunur. Giriş, çıkış ve takım değişiminde iki sekmedeki bilgi güncellenir. Bilinmeyen hesap ücretli sayılmaz; henüz giriş yapılmadıysa hesap sınırları varsayılmaz.

| Hesap | Profil süresi | Aktif uygulama sınırı |
| --- | --- | --- |
| Ücretsiz Apple hesabı | 7 gün | Sade IPA dahil toplam 3 |
| Apple Developer Program hesabı | 365 güne kadar | Ücretsiz hesaptaki 3 uygulama sınırı uygulanmaz |

Sayaç ve son gün hatırlatması her uygulamanın **gerçek profil bitiş tarihini** kullanır. Üyeliği yükseltmek veya hesabı değiştirmek mevcut imzayı uzatmaz. **Ayarlar → Hesap ve kurulum** üzerinden yeni hesap/takımla giriş yaptıktan sonra uygulamaları o hesapla yenile. Takım değişimi yeni imzalama kimliği gerektirebilir; hata varsa süre ilerlemez. Ücretsiz hesaba dönerken motorun uygulama sınırı yeniden geçerlidir.

İmzalama ve kurulum motoru SideStore'dan gelir; ücretsiz ve ücretli hesapla gerçek cihaz doğrulaması ayrıca gereklidir. Hesap sınırlarının kaynağı: [Apple](https://developer.apple.com/help/account/basics/about-your-developer-account), [SideStore](https://docs.sidestore.io/docs/faq).

Süre dolmadan yenile. iOS arka plan çalışmasını planladığı için belirli bir gün veya saatte otomatik yenileme garantisi yoktur. iOS güncellemesi, eşleştirme sorunu veya yükleyicinin imzasının dolması tekrar bilgisayar kullanımını gerektirebilir.

## Lisans

Altyapı: [SideStore 0.7.0-alpha](https://github.com/SideStore/SideStore/releases/tag/0.7.0-alpha), commit `6032424a0e56c1c319762e786099bdd9186a238b`. Bu sürüm, Apple tarafındaki değişiklik sonrası 0.6.4 ve önceki sürümlerde oluşan giriş sorununu düzeltir.

Özgün telif bildirimleri korunur. Uyarlama **AGPL-3.0** kapsamındadır; tam metin `LICENSE` dosyasında ve kaynak paketindedir. Bu proje resmî SideStore dağıtımı değildir. SideStore'un bundle kimliği korunur; mevcut SideStore'u değiştirebilir. Upstream uygulama güncellemesi özel arayüzü geri getirebilir.
