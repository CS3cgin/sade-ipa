# Sade IPA · iPhone'a ilk kurulum

Bu bilgisayarda iLoader 2.3.6, iTunes ve Apple USB sürücüleri mevcut. İlk kurulum ücretsiz veya ücretli Apple hesabıyla Windows üzerinden yapılır. Derlenen paket kişisel hesabınla imzalanmadan iPhone'a kurulamaz.

## 1. IPA'yı yükle

1. iPhone'u USB ile bağla, kilidini aç ve **Bu bilgisayara güven** isteğini onayla.
2. Başlat menüsünden **iloader** aç. Apple hesabına iloader içinde giriş yap; doğrulama kodunu da burada gir.
3. Telefonunu seç. **IPA yükle / Import IPA** seçeneğinde `build/SadeIPA.ipa` dosyasını seç.
4. **Install SideStore (Stable)** düğmesi farklı bir paket indirir. Özel arayüz için kendi IPA dosyanı seç.
5. Kurulum tamamlanınca iPhone'da **Ayarlar → Genel → VPN ve Aygıt Yönetimi → geliştirici hesabın** bölümünü açıp güven işlemini tamamla. iOS yeniden başlatmanı isteyebilir.
6. **Ayarlar → Gizlilik ve Güvenlik → Geliştirici Modu** seçeneğini etkinleştir; yeniden başlatma ve sonraki onayları tamamla.

## 2. Eşleştirme dosyasını aktar

Bu uyarlamanın adı “Sade IPA” olduğu için iloader'ın SideStore adına göre oluşturduğu otomatik eşleştirme listesinde görünmeyebilir. Dosyayı USB ile aktarabilirsin:

1. iloader'da **Eşleştirme dosyasını yönet / Manage Pairing File** bölümünü aç.
2. **Dışa aktar / Export** ile dosyayı bilgisayarına `ALTPairingFile.mobiledevicepairing` adıyla kaydet. Dosya adı uzantısıyla birlikte böyle olmalı; sonunda `.plist` veya `.txt` kalmamalı.
3. iTunes'ta iPhone simgesine tıkla → **Dosya Paylaşımı / File Sharing** → **Sade IPA** → **Dosya Ekle / Add**. Kaydettiğin dosyayı seç.
4. Apple Devices uygulaması cihazı yönetiyorsa aynı aktarımı o uygulamanın **Dosyalar / Files** bölümünden yap.
5. Sade IPA'yı kapatıp yeniden aç. Dosya seçme isteği çıkarsa **Dosyalar → iPhone'umda → Sade IPA** içindeki eşleştirme dosyasını seç.

Alternatif olarak dosyayı iloader'ın varsayılan `pairingFile.plist` adıyla kaydedip aynı yoldan aktarabilirsin. Sade IPA'yı tamamen kapatıp yeniden aç; **Select File / Dosya Seç** ile bu dosyayı seç. Uygulama dosyayı kendi beklediği adla kaydeder.

Eşleştirme dosyası yalnız senin cihazında kullanılmalıdır; GitHub'a yükleme.

## 3. Telefondan ilk yenilemeyi doğrula

1. App Store'dan **LocalDevVPN** kur. Wi-Fi'ye bağlan; LocalDevVPN'de **Connect** seç.
2. Sade IPA'da **Ayarlar → Hesap ve kurulum** aç; iloader'da kullandığın Apple hesabıyla giriş yap.
3. **Uygulamalar → Tümünü yenile** seç. Yükleyicinin kendi yenilemesi uygulamayı geçici olarak kapatabilir. Son aşamada beklerse Ana Ekran'a dön, 30 saniye bekle ve tekrar aç. İşlem sırasında uygulamayı uygulama değiştiriciden zorla kapatma.
4. Hata olmadığını ve gerçek imza bitiş tarihinin güncellendiğini kontrol et.
5. USB bağlantısını çıkar; Wi-Fi ve LocalDevVPN açıkken bir yenilemeyi daha dene. Böylece bilgisayarsız kullanım cihaz üzerinde doğrulanmış olur.

Ücretsiz hesapta imza 7 gün sürer. Süre dolmadan yenile; **Son gün hatırlatması** ve **Arka planda yenileme** seçeneklerini Ayarlar'dan açabilirsin. iOS arka plan çalışma zamanını seçtiği için otomatik yenileme kesin saatinde garanti değildir. Yükleyici dahil 3 aktif uygulama sınırı vardır.

## 4. Hesap türünü kontrol et veya değiştir

**Ayarlar** ekranında seçili takımın hesap türü görünür. Ücretsiz hesapta 7 gün / 3 aktif uygulama; Apple Developer hesabında 365 güne kadar / 3 uygulama sınırı yok bilgisi gösterilir. Sayaç her zaman kurulu uygulamanın gerçek profil tarihini kullanır.

Ücretli üyeliğin etkinleşince **Hesap ve kurulum** bölümünden hesabından çıkıp tekrar giriş yap; birden fazla takım sunulursa ücretli geliştirici takımını seç. Ardından **Tümünü yenile** ile yeni hesabınla imzala. Eski 7 günlük imza, yalnız üyeliği satın almakla uzamaz. Başarılı yenileme sonrasında listedeki bitiş tarihini kontrol et. Ücretsiz hesaba geri dönersen 3 aktif uygulama sınırı tekrar uygulanır.

Hesap/takım değişimi yeni imzalama kimliği gerektirebilir; her uygulamanın verisinin korunacağı garanti değildir. İki hesap türünde giriş, kurulum ve kendini yenileme gerçek cihazda ayrıca doğrulanmalıdır. Sınırlar için [Apple](https://developer.apple.com/help/account/basics/about-your-developer-account) ve [SideStore](https://docs.sidestore.io/docs/faq) açıklamalarını inceleyebilirsin.

Bir iOS güncellemesi veya eşleştirme kaydının bozulması yeniden Windows bağlantısı gerektirebilir. Kullanıcının iPhone 16 / iOS 27.0.1 cihazında kurulum, eşleştirme sonrası Hazır durumu ve kendini yenilemenin ardından Ana Ekran'a geçip yeniden açınca işlem çubuğunun kapanması gözlendi. USB olmadan yenileme, başka IPA yükleme, arka plan yenileme ve ücretli hesap testleri ayrıca yapılmalıdır.

Kaynaklar: [SideStore kurulum rehberi](https://docs.sidestore.io/docs/installation/install), [iloader](https://iloader.app/), [iloader eşleştirme uygulaması](https://github.com/nab138/iloader/blob/v2.3.6/src-tauri/src/pairing.rs), [Apple USB dosya paylaşımı](https://support.apple.com/en-ca/guide/itunes/itns32636/windows).
