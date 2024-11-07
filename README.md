# Генерация самоподписанного SSL сертификата для socket соединения python

> ## Предвапительно нужно создать файл конфигурации
>
> ```
> [req]
> default_bits = 2048
> default_md = sha256
> distinguished_name = req_distinguished_name
> x509_extensions = v3_req
> prompt = no
> [req_distinguished_name]
> C = RU
> ST = MO
> L = Moscow
> O = Test LLC
> OU = Test LLC
> CN = 192.168.1.1
> [v3_req]
> keyUsage = keyEncipherment, dataEncipherment
> extendedKeyUsage = serverAuth
> subjectAltName = @alt_names
> [alt_names]
> IP.1 = 192.168.1.1
> ```

*1) Генерируем закрытый ключ для CA (Certificate authority) сертификата.*

   `openssl genrsa -out rootCA.key 2048`

*2) Подписываем его*

   `openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 365 -out rootCA.pem -config cert.conf`
