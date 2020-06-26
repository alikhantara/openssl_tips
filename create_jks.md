# How to create keystore with full key chain for connect from java to self-signed https server.
I write this after non-pleasant meeting with IBM Integration Bus 
Ok. 
You need client certificate(cert.crt), key(key.key), ca (ca.crt) and intermediate certificate (int.crt) from server side.  
First make the full key chain .p12 (or .pfx):

```sh
cat cert.crt ca.crt int.crt >> fullchain.cer
openssl pkcs12 -export -in fullchain.cer -inkey key.key -out fullchain.p12
```

Export all certificates from .p12 to keystore:
```sh
keytool -importkeystore -srckeystore fullchain.p12 -srcstoretype PKCS12 -destkeystore fullchain.jks
Importing keystore fullchain.p12 to fullchain.jks...
Enter destination keystore password:
Re-enter new password:
Enter source keystore password:
Entry for alias 1 successfully imported.
Import command completed: 1 entries successfully imported, 0 entries failed or cancelled
```

After, export rootCA and Intermediate certificate to truststore:
```sh
keytool -import -trustcacerts -alias rootca -file ca.crt.pem -keystore cacerts.jks
keytool -import -trustcacerts -alias inetrmediate -file int.crt -keystore cacerts.jks
```
