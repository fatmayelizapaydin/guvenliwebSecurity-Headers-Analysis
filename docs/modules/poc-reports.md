# 🧪 Proof of Concept (PoC) ve Güvenlik Denetim Notları

Bu doküman, analiz edilen web sitelerindeki güvenlik zafiyetlerinin pratik ispatlarını ve bu açıkların nasıl manipüle edilebildiğini teknik detaylarıyla açıklar.

## 1. Clickjacking İspatı (X-Frame-Options Eksikliği)
`X-Frame-Options` başlığı bulunmayan bir site, saldırgan tarafından oluşturulan bir web sayfası içine gizlice gömülebilir.

* **İspat Adımları:**
  1. Kendi yerel sunucunuzda basit bir HTML dosyası oluşturun.
  2. İçine şu satırı ekleyin: `<iframe src="https://hedef-site-url.com" style="width:100%; height:100%;"></iframe>`.
  3. Sayfayı tarayıcıda açtığınızda sitenin iframe içinde yüklendiğini (ve dolayısıyla saldırıya açık olduğunu) göreceksiniz.
* **Sonuç:** `DENY` başlığının olmaması, kullanıcının haberi olmadan butonlara tıklamasına (örneğin: "Satın al", "Şifremi Değiştir") olanak tanır.

## 2. XSS ve CSP İspatı (Content Security Policy)
CSP bulunmayan sitelerde tarayıcı, site dışından gelen veya site içine enjekte edilen (injected) JavaScript dosyalarını ayırt edemez.

* **İspat Adımları:**
  1. Tarayıcıda (Chrome/Edge/Firefox) `F12` ile Geliştirici Araçlarını açın.
  2. **Console** sekmesine gelin.
  3. `alert('XSS Başarılı!');` komutunu çalıştırın.
* **Analiz:** Eğer site modern bir CSP (Content Security Policy) kullanıyor olsaydı, tarayıcı bu komutu "inline script" olarak engelleyecekti. Ancak CSP eksikliği olan sitelerde komut doğrudan çalıştırılır.

## 3. Protokol İhlali (SSL Stripping Riski - HSTS Eksikliği)
* **İspat:** `SecurityHeaders.com` üzerinden yapılan taramada "Strict-Transport-Security" kısmının kırmızı olması, sitenin saldırganlar tarafından "SSL Strip" saldırılarına açık olduğunu ispatlar.
* **Gözlem:** Kullanıcı tarayıcısına doğrudan `http://` protokolü ile yazsa bile, HSTS başlığı tarayıcıyı `https://` ile bağlanmaya zorlamaz; bu da aradaki saldırganın trafiği okumasına (MITM) yol açar.

---

*Yukarıdaki diyagram, şeffaf bir katmanın kullanıcının tıklama verisini nasıl çaldığını özetler.*

## 4. Denetim Sonuç Notları
Bu PoC çalışmaları göstermiştir ki; modern web güvenliği sadece veritabanını korumak değil, istemci (tarayıcı) ile sunucu arasındaki **trafiği ve içeriği** güvenlik başlıklarıyla ("Defense in Depth") koruma altına almaktır.
