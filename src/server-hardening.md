# 🛡️ Güvenli Web Sunucu Yapılandırması (Hardening Guide)

Bu doküman, analiz edilen web uygulamalarındaki güvenlik açıklarını (CSP, HSTS, X-Frame-Options eksiklikleri) gidermek için gerekli olan **"Sıkılaştırılmış" (Hardened)** sunucu ve uygulama konfigürasyonlarını içerir.

## 1. Nginx Sunucusu İçin Güvenlik Başlıkları
Modern bir web sunucusunda güvenlik, merkezi bir konfigürasyon ile yönetilmelidir. Aşağıdaki yapılandırma, sitenizi en yüksek güvenlik seviyesine taşır:

```nginx
# /etc/nginx/conf.d/security_headers.conf

# 1. HSTS: Tarayıcıyı HTTPS'e zorlar ve saldırganın HTTP'ye düşürmesini engeller (SSL Stripping koruması)
add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;

# 2. CSP: Sadece güvenilir kaynaklardan script ve içerik çalıştırılmasını sağlar (XSS koruması)
add_header Content-Security-Policy "default-src 'self'; script-src 'self' [https://trusted-cdn.com](https://trusted-cdn.com); object-src 'none'; frame-ancestors 'none';" always;

# 3. Clickjacking Koruması: Sitenin başka bir sayfa içerisinde iframe ile açılmasını tamamen engeller
add_header X-Frame-Options "DENY" always;

# 4. MIME Sniffing Engelleme: Tarayıcının içerik tipini tahmin etmesini engeller (XSS koruması)
add_header X-Content-Type-Options "nosniff" always;

# 5. Referrer Politikası: Gizli bilgilerin sızmasını engeller
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
