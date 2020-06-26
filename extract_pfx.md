# How to extract private key and certificate from .pfx

This command extract the key:
```sh
openssl pkcs12 -in yourpfx.pfx -nocerts -out private_key.key -nodes
```

This command extract the certificate:
```sh
openssl pkcs12 -in yourpfx.pfx -nokeys -out certificate.pem
```

As a bonus:
This command remove passphrase from private key.
```sh
#openssl rsa -in private_key.pem -out private_key_without_pass.key
```