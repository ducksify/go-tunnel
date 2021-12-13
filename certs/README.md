# Selfsign Certificats creation
### CA
openssl genrsa 2048 > ca.key
openssl req -new -x509 -nodes -days 1000 -key ca.key > ca.pem
### Server Certificat requests 
openssl req -newkey rsa:2048 -days 1000 -nodes -keyout server.key  -config server.cnf   > server-req.csr
### Sign certificat
openssl x509 -req -in server-req.csr -days 1000 -CA ca.crt -CAkey ca.key -set_serial 01 -extfile server.ext  -extensions v3_req > server.crt

### Client Certificat requests 
openssl req -newkey rsa:2048 -days 1000 -nodes -keyout server.key  -subj "/C=CH/ST=VD/O=Ducksify/OU=IT/CN=gotunclient.ducksify.com" > client-req.csr
### Sign certificat
openssl x509 -req -in client-req.csr -days 1000 -CA ca.crt -CAkey ca.key -set_serial 01 > u0.crt