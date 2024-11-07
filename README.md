# ssl4socket
Генерация самоподписанного SSL сертификата для socket соединения python

1) Генерируем сертификат CA (Certificate authority).

   openssl genrsa -out rootCA.key 2048

2) Подписываем его

   openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 365 -out rootCA.pem -config cert.conf
