Welcome to the ExpressPQDelivery Project
==============================
The epqd_server_lib is a library that implements ExpressPQDelivery handshake for server based on OpenSSL.

## How to start(Linux Ubuntu)
### Set compile option
```bash
./Configure
```
### Make
```bash
make depend && make
```
### Install
```bash
sudo make install
```
### Build OQS-provider
```bash
cd epqd_client_lib
```
```bash
git clone https://github.com/open-quantum-safe/oqs-provider.git  
cd oqs-provider  
```

```bash
git reset --hard 49bb2d271ec64f35f5a3905577f2dbc2c1b8d07d  
```
```bash
sudo su  
cmake -DOQS_KEM_ENCODERS=ON -S . -B _build && cmake --build _build && cmake --install _build  
```
### Setting openssl.cnf file
In the case of `oqs-provider` add these lines to achieve this:

```
[provider_sect]
default = default_sect
oqsprovider = oqsprovider_sect
[oqsprovider_sect]
activate = 1
```

### Checking OQS-Provider

If successfully done, running, e.g., `openssl list -providers`
should output something along these lines (version IDs variable of course):

```
providers:
  default
    name: OpenSSL Default Provider
    version: 3.3.0
    status: active
  oqsprovider
    name: OpenSSL OQS Provider
    version: 0.5.4-dev
    status: active
```

## TroubleShooting
```bash
OPENSSL_ROOT_DIR=~/epqd_server_lib/ OPENSSL_INSTALL=/usr/local/lib64 ./scripts/fullbuild.sh  
```

```bash
export OPENSSL_CONF=/etc/ssl/openssl.cnf
```


## Reference
https://www.lesstif.com/system-admin/openssl-compile-build-6291508.html
https://github.com/open-quantum-safe/oqs-provider/blob/main/USAGE.md?plain=1
