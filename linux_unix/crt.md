Installing a root/CA Certificate

Given a CA certificate file foo.crt, follow these steps to install it on Ubuntu:

1. Create a directory for extra CA certificates in /usr/local/share/ca-certificates:
````bash
sudo mkdir /usr/local/share/ca-certificates/extra
````
2. Copy the CA .crt file to this directory:
````bash
sudo cp foo.crt /usr/local/share/ca-certificates/extra/foo.crt
````
3. Let Ubuntu add the .crt file's path relative to /usr/local/share/ca-certificates to /etc/ca-certificates.conf:
````bash
sudo dpkg-reconfigure ca-certificates
````
4. To do this non-interactively, run:
````bash
sudo update-ca-certificates
````
In case of a .pem file on Ubuntu, it must first be converted to a .crt file:
````bash
openssl x509 -in foo.pem -inform PEM -out foo.crt
````
Or a .cer file can be converted to a .crt file:
````bash
openssl x509 -inform DER -in foo.cer -out foo.crt
````