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

   `openssl genrsa -out CA.key 2048`

*2) Подписываем его*

   `openssl req -x509 -new -nodes -key CA.key -sha256 -days 365 -out CA.pem -config server.conf`

*3) openssl genrsa -out client1.key 2048

*4) openssl req -new -key client1.key -out client1.csr -config client1.conf

*5) openssl x509 -req -in client1.csr -CA CA.pem -CAkey CA.key -CAcreateserial -out client1.crt -days 364 -sha256
