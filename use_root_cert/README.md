# Using root certificate

## Create certificate ([source](https://hackcatml.tistory.com/m/37))

```
$ sudo apt install openssl

$ openssl req -x509 -days 730 -nodes -newkey rsa:2048 -outform der -keyout server.key -out ca.der -extensions v3_ca

$ openssl rsa -in server.key -inform pem -out server.key.der -outform der

$ openssl pkcs8 -topk8 -in server.key.der -inform der -out server.key.pkcs8.der -outform der -nocrypt

$ openssl x509 -inform DER -in ca.der -out ca.pem

for android >= 7.0
$ cp ca.pem `openssl x509 -inform PEM -subject_hash_old -in ca.pem | head -1 | awk '{print $1}'`.0  --> will create file "{hash}.0"

for OWASP_ZAP
$ cat server.key ca.pem > owasp_zap.pem
```

## Install certificate on devices

-   android >= 7.0

    ```
    $ adb push {hash}.0 /data/local/tmp
    $ adb shell

    adb $ su - root
    adb $ mount -o rw,remount /system
    adb $ mv /data/local/tmp/{hash}.0 /system/etc/security/
    adb $ chmod 644 /system/etc/security/{hash}.0

    reboot device
    ```

-   [android < 7.0](https://www.youtube.com/watch?v=Aff-XIkNsso) (use ca.pem)
-   [ios](https://support.citrix.com/article/CTX228877) (use ca.pem)

## [See set proxy](../set_proxy)
