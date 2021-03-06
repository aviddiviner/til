# Fingerprint SSH keys

Quick refresher course on working with SSH keys.

- Create new SSH key:

```
ssh-keygen -t rsa -f private_key.pem
```

- Generate public key from private key:

```
ssh-keygen -yf private_key.pem > public_key.pub
```

- Get SHA256 or MD5 fingerprints from a public key:

```
% ssh-keygen -lf public_key.pub
2048 SHA256:KNY8iVR40c8v6Ahm0gWjUhtwJo8Fbbgu2obGMuihW1U dave@macbook (RSA)
% ssh-keygen -E md5 -lf public_key.pub
2048 MD5:8e:56:e6:01:e0:ec:29:cf:29:60:fb:66:5f:5a:89:a1 dave@macbook (RSA)
```

## EC2 keys

#### EC2 generated key

If the key is generated by EC2 (40 byte fingerprint), it's computed by taking the SHA1 of the _private_ key part in PKCS#8 format:

```
openssl pkcs8 -in private_key.pem -inform PEM -outform DER -topk8 -nocrypt | openssl sha1 -c
```

Note that you're creating a digest of the private key (the first command just converts the private key from PEM (text) to DER (binary) format). The consequence of this is that you can't verify the fingerprint of such keys unless you have the private key.

#### Imported key

If the key is imported into EC2 (32 byte fingerprint), it's the MD5 of the _public_ key part. Here we extract the public key from the private key and checksum that:

```
openssl rsa -in private_key.pem -pubout -outform DER | openssl md5 -c
```

#### Advanced EC2 key high jinks

You may need a more recent version of openssl to use the `openssl pkey` public/private key processing tool:

```
brew install openssl
alias openssl='/usr/local/opt/openssl/bin/openssl'
```

- Generate PEM-format public key from private key (these commands are equivalent):

```
ssh-keygen -ef private_key.pem -m pkcs8
openssl rsa -in private_key.pem -pubout -outform PEM
openssl pkey -in private_key.pem -pubout -outform PEM
```

- Get 32 byte MD5 fingerprint using only the public key (as PEM file):

```
openssl pkey -in public_key.pem -pubin -pubout -outform DER | openssl md5 -c
```
