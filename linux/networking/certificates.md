# certificates


**trust** - Tool for operating on the trust policy store on linux

## TLS

**quick commands:**

Generate a new private key and Certificate Signing Request:

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key
```

Generate a self-signed certificate:

```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```

Generate a certificate signing request (CSR) for an existing private key:

```
openssl req -out CSR.csr -key privateKey.key -new
```

Generate a certificate signing request based on an existing certificate:

```
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key
```

Remove a passphrase from a private key:

```
openssl rsa -in privateKey.pem -out newPrivateKey.pem
```

## Debugging Using OpenSSL

Check an MD5 hash of the public key to ensure that it matches with what is in a CSR or private key:

```
openssl x509 -noout -modulus -in certificate.crt | openssl md5
openssl rsa -noout -modulus -in privateKey.key | openssl md5
openssl req -noout -modulus -in CSR.csr | openssl md5
```
inspect certificate:

```
openssl x509 -in <cert_file> -text
```

Check an SSL connection. All the certificates (including Intermediates) should be displayed:

```
openssl s_client -connect www.github.com:443
```

## Converting Using OpenSSL
Convert PEM to DER:

```
openssl x509 -in domain.crt -outform der -out domain.der 
```

Convert DER to PEM:

```
openssl x509 -inform der -in domain.der -out domain.crt
```

Convert PEM to PKCS7:

```
openssl crl2pkcs7 -nocrl -certfile domain.crt -certfile ca-chain.crt -out domain.p7b 
```

Convert PKCS7 to PEM:

```
openssl pkcs7 -in domain.p7b -print_certs -out domain.crt
```

Convert PEM to PKCS12:

```
openssl pkcs12 -inkey domain.key -in domain.crt -export -out domain.pfx
```

Convert PKCS12 to PEM:

```
openssl pkcs12 -in domain.pfx -nodes -out domain.combined.crt
```

Convert a DER file (.crt .cer .der) to PEM:

```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```

Convert a PEM file to DER:

```
openssl x509 -outform der -in certificate.pem -out certificate.der
```

Convert a PKCS#12 file (.pfx .p12) containing a private key and certificates to PEM:

```
openssl pkcs12 -in keyStore.pfx -out keyStore.pem -nodes
```

Convert a PEM certificate file and a private key to PKCS#12 (.pfx .p12):

```
openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt
```


## Generating CSRs

Generate a Private Key and a CSR:

```
openssl req -newkey rsa:2048 -nodes -keyout domain.key -out domain.csr 
```

Generate a CSR from an Existing Private Key:

```
openssl req -key domain.key -new -out domain.csr 
```

Generate a CSR from an Existing Certificate and Private Key:

```
openssl x509 -in domain.crt -signkey domain.key -x509toreq -out domain.csr
```

## Generating SSL Certificates

Generate a Self-Signed Certificate:

```
openssl req -newkey rsa:2048 -nodes -keyout domain.key -x509 -days 365 -out domain.crt 
```

Generate a Self-Signed Certificate from an Existing Private Key:

```
openssl req -key domain.key -new -x509 -days 365 -out domain.crt 
```

Generate a Self-Signed Certificate from an Existing Private Key and CSR:

```
openssl x509 -signkey domain.key -in domain.csr -req -days 365 -out domain.crt
```

## View Certificates

View CSR Entries:

```
openssl req -text -noout -verify -in domain.csr
```

View Certificate Entries:

```
openssl x509 -text -noout -in domain.crt
```

Verify a Certificate was Signed by a CA:

```
openssl verify -verbose -CAFile ca.crt domain.crt
```

## Private Keys

Create a Private Key:

```
openssl genrsa -des3 -out domain.key 2048
```

Verify a Private Key:

```
openssl rsa -check -in domain.key
```

Verify a Private Key Matches a Certificate and CSR:

```
openssl rsa -noout -modulus -in domain.key | openssl md5 openssl x509 -noout -modulus -in domain.crt | openssl md5 openssl req -noout -modulus -in domain.csr | openssl md5
```

Encrypt a Private Key:

```
openssl rsa -des3 -in unencrypted.key -out encrypted.key
```

Decrypt a Private Key:

```
openssl rsa -in encrypted.key -out decrypted.key
```
