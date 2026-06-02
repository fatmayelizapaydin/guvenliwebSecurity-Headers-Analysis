# Örnek Web Sunucusu Güvenlik Konfigürasyonu

Analiz ettiğimiz sitelerdeki eksiklikleri gidermek için bir Nginx veya Apache sunucusunda kullanılması gereken örnek `HTTP Security Headers` konfigürasyonu aşağıdadır:

```nginx
# Nginx için örnek güvenlik başlıkları yapılandırması
add_header X-Content-Type-Options nosniff;
add_header X-Frame-Options "SAMEORIGIN";
add_header X-XSS-Protection "1; mode=block";
add_header Content-Security-Policy "default-src 'self'; script-src 'self' [https://trusted.cdn.com](https://trusted.cdn.com);";
add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";
