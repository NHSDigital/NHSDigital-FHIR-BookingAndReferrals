## {{page-title}}


## Introduction

The BaRS API and supplier solution will be secured by HTTPS/TLS, for both inbound and outbound connections. All certificates used are published on this website for your convenience. 

In order to establish a connection to and from any environment, a chain of trust must be set up using the certificates detailed below. 

For information on obtaining certificates as a Receiver see the {{pagelink:onboarding}} section.

## Inbound

All inbound connections to the BaRS API will be presented with environment specific certificate, provided by Digicert. This is inline with all NHS APIs on the platform. The details for the certificate and chain used are described in the table below. 

| Certificate CN                   | Thumbprint                               | Parent CN                        | Parent Thumbprint                        | Environment |
|----------------------------------|------------------------------------------|----------------------------------|------------------------------------------|-------------|
| dev.api.service.nhs.uk           | 8c41b2d0080ff4f83ef4164078d17bab5ed53cbb | DigiCert TLS RSA SHA256 2020 CA1 | 1c58a3a8518e8759bf075b76b750d4f2df264fcd | Sandbox     |
| int.api.service.nhs.uk           | 634680dfafcf3a6e229741ae7ad5b98dbe70d822 | DigiCert TLS RSA SHA256 2020 CA1 | 1c58a3a8518e8759bf075b76b750d4f2df264fcd | INT         |
| api.service.nhs.uk               | 2673f9045ba6f8ff8b7b82a9046f9b599af27cab | DigiCert TLS RSA SHA256 2020 CA1 | 1c58a3a8518e8759bf075b76b750d4f2df264fcd | Prod        |
| DigiCert TLS RSA SHA256 2020 CA1 | 1c58a3a8518e8759bf075b76b750d4f2df264fcd | DigiCert Global Root CA          | a8985d3a65e5e5c4b2d7d66d40c6dd2fb19c5436 | All         |
| DigiCert Global Root CA          | a8985d3a65e5e5c4b2d7d66d40c6dd2fb19c5436 | N/A                              | N/A                                      | All         |

### dev.api.service.nhs.uk (Digicert) 

```
-----BEGIN CERTIFICATE-----
MIIH7zCCBtegAwIBAgIQCd1RZTdgwjlx2LOoB8pNHTANBgkqhkiG9w0BAQsFADBP
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMSkwJwYDVQQDEyBE
aWdpQ2VydCBUTFMgUlNBIFNIQTI1NiAyMDIwIENBMTAeFw0yMjA2MjkwMDAwMDBa
Fw0yMzA2MjkyMzU5NTlaMFQxCzAJBgNVBAYTAkdCMQ4wDAYDVQQHEwVMZWVkczEU
MBIGA1UEChMLTkhTIERpZ2l0YWwxHzAdBgNVBAMTFmRldi5hcGkuc2VydmljZS5u
aHMudWswggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQChdhQee1KNW6C/
qUzRfgwLzxdXcLMusYrCR+dkiJiyVTy2JAP9iDwOqsJWeaxzXzXoPM+3ahq2m7c6
CgAhuk8XHo3vhRfJzLehbQtzAgnz5YDevpI74gj2V/Wd7/QGu8Cgh9AoCtO5gfh8
byju/V9eJArHxCE6huduBTp59y8Dth/VGWiDaOgYDauBOkSKdxVmPl1qZOv7cN/p
wD4TyZxs0CrqUrkRT4WfvABrOaG7jLbeKKhVfMYXSJhPs1g7STJaOzvrRAwt1O83
q4Objc3/oPnbbN1AyXlVyHI2exkxmNllYHRMogQMSFOpdj/g+zibw7tPpKDE49Xx
YFtfGOUHusb2Fj7kYh7bevdOibrmzG+zT1l29VNzaYp0sFMSrHaCBVZ6Rw/q3BHV
vRXfb+zpiSpmUG67FULKWQRCSKEBw7pfD1+cg8050PT+JnnhONjwzbwJMZjiibV7
f0JGP0G2JX1sRSad+EBHPYd1is0SESFhfrkSm5pQxgTkxGFKhBC0fm3LSP6qhelz
z1YIKupi66wC74dnV/YJkxOQ38r3uH0WTiZ8SL2Zd3Gd+1DPWXydvjfH94yQpOHj
ihRhHlkn+uRynOBqcCTsZ+9xyOjAQ3AicSLAsK9V+YxK+mO1IatgnmafLGNWYAsK
YpGS+BsOnS6Znecv9lFPcWWdTQsUpwIDAQABo4IDwDCCA7wwHwYDVR0jBBgwFoAU
t2ui6qiqhIx56rTaD5iyxZV2ufQwHQYDVR0OBBYEFMa79aKSfMUaT2POYUTKkpfF
mocAMG0GA1UdEQRmMGSCFmRldi5hcGkuc2VydmljZS5uaHMudWuCFnJlZi5hcGku
c2VydmljZS5uaHMudWuCGnNhbmRib3guYXBpLnNlcnZpY2UubmhzLnVrghZkZXAu
YXBpLnNlcnZpY2UubmhzLnVrMA4GA1UdDwEB/wQEAwIFoDAdBgNVHSUEFjAUBggr
BgEFBQcDAQYIKwYBBQUHAwIwgY8GA1UdHwSBhzCBhDBAoD6gPIY6aHR0cDovL2Ny
bDMuZGlnaWNlcnQuY29tL0RpZ2lDZXJ0VExTUlNBU0hBMjU2MjAyMENBMS00LmNy
bDBAoD6gPIY6aHR0cDovL2NybDQuZGlnaWNlcnQuY29tL0RpZ2lDZXJ0VExTUlNB
U0hBMjU2MjAyMENBMS00LmNybDA+BgNVHSAENzA1MDMGBmeBDAECAjApMCcGCCsG
AQUFBwIBFhtodHRwOi8vd3d3LmRpZ2ljZXJ0LmNvbS9DUFMwfwYIKwYBBQUHAQEE
czBxMCQGCCsGAQUFBzABhhhodHRwOi8vb2NzcC5kaWdpY2VydC5jb20wSQYIKwYB
BQUHMAKGPWh0dHA6Ly9jYWNlcnRzLmRpZ2ljZXJ0LmNvbS9EaWdpQ2VydFRMU1JT
QVNIQTI1NjIwMjBDQTEtMS5jcnQwCQYDVR0TBAIwADCCAXwGCisGAQQB1nkCBAIE
ggFsBIIBaAFmAHYArfe++nz/EMiLnT2cHj4YarRnKV3PsQwkyoWGNOvcgooAAAGB
r8Mt1gAABAMARzBFAiEA3y5VxP+JXtBoJdaQUf+DvWzfq7hfm7tSrKpDxLzr3LsC
ID8AtMzjnVttILxLmAZFmr/Xq2tEM7ubqJprZjqmZtxBAHUANc8ZG7+xbFe/D61M
bULLu7YnICZR6j/hKu+oA8M71kwAAAGBr8MtNwAABAMARjBEAiAhvkbK+nr8p1+s
fTqfrslKaI0K5prTdt65yHRdhJdtdAIgKlEWGUSlCH7AwfQJ04Xxo1o+rJ1nyl8Y
bD17Fmee4I0AdQCzc3cH4YRQ+GOG1gWp3BEJSnktsWcMC4fc8AMOeTalmgAAAYGv
wy1YAAAEAwBGMEQCIBoJtWDLt+0gBNbbW+73bJtYnD2/eLGF+ASZO9NjrgdcAiBx
UChWKBEH5ndm9j2MfiDfhb8CIkMDxYwl7cNU+owJhDANBgkqhkiG9w0BAQsFAAOC
AQEAm/i6ZvIf03/3YgF9dWoSygDDuziv5u5CQu6Vn9ojHPN6y+zzF8V6fyrgjo2q
+BILKe5AkhCak/YmBEKN4PcoLerCFmBS5F2GaJ0fYx4+BevaeauewMmXq3WrduAp
QwmVtvBfY4MdvFTZ1afLxPbBoMduwjI/7F8Vsq9yPWdwSlkEXCb5v8mCcWqIOr6F
mntXmZoNig+cWTWebyX3B/dVnYezQqcd2clM5yb3Tz/C4YPa/pHrXP4Uekskh9wm
LrKCzc961OVITemj0KA6xkbeVNnXjRjyKiZS//iDRugZJf3yh5oTON9fqoVgV+bd
9UWHkyVsonT2QQWayu4R2mb30g==
-----END CERTIFICATE-----
```

### int.api.service.nhs.uk (Digicert) 

```
-----BEGIN CERTIFICATE-----
MIIHpjCCBo6gAwIBAgIQCbufxB/0/HfjHDnytP71fTANBgkqhkiG9w0BAQsFADBP
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMSkwJwYDVQQDEyBE
aWdpQ2VydCBUTFMgUlNBIFNIQTI1NiAyMDIwIENBMTAeFw0yMjAzMDcwMDAwMDBa
Fw0yMzA0MDcyMzU5NTlaMFQxCzAJBgNVBAYTAkdCMQ4wDAYDVQQHEwVMZWVkczEU
MBIGA1UEChMLTkhTIERpZ2l0YWwxHzAdBgNVBAMTFmludC5hcGkuc2VydmljZS5u
aHMudWswggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQC4JPKFpz/Rl8QC
tMERVDSLXehOKlzBg7V5tsFerUwMAvKSZwfd9gRDWnH+QarjypoKM6VkH+hv6NsU
ApWHngeO6BOstltMaIVXZ4GRfKD3iaJCA3WO2qaixjXjZDhWTCLrCnmUYnkpf3Sp
f8aIzLS9LMfLn84Xa0VvOtGTYN9/Cf6zPdfhI6Qy3qRJote8w73lWxs4SZ8ObFya
9c+OEb7gnZfhg0kgQFM6qwYPAqAuNHt47Sd/TLySQ186j2ItoFfRih2pMfEDw1a9
2HQTpYZDCrUCqkMyKacZAlf66LEOKnqAaqn+VxKGJa9wZghJP/ZrkSJ11jfnBBzN
IhUV5KGyTC2xjaHj3jXD8rzwRyNafHfQX1YYM4572+0LbXs+ZKrX0HXj34W765o7
PAUjJk4Ih52r7fFpch4hYkpyGfoN+riMxbBmSRelAbLXHOdi6LvsXGdxPtRQwlYa
zsjOD1+lhOFLtLXZplViNyKEGh1J5UVeL0OZuMW9b9x8Ug6/DPBVcoZ0UmnyUVr/
pgjRKF/zU67LWR0Vqzq9OUdTNLImEfMLsfKx2ytO/kSk9PB8Ifp0E5tz6j17kNeh
Q3TjR++e1AUrOq2DrqwzpH8QIfIIiEfsd/Y267YfWmPPwo6A6h7HqSH9BQuJihme
GO/aVQLpUUzZn/tbtuIFffvE8EovEwIDAQABo4IDdzCCA3MwHwYDVR0jBBgwFoAU
t2ui6qiqhIx56rTaD5iyxZV2ufQwHQYDVR0OBBYEFMxc1yJdMXn5cMQY/y/eYQIp
7zm+MCEGA1UdEQQaMBiCFmludC5hcGkuc2VydmljZS5uaHMudWswDgYDVR0PAQH/
BAQDAgWgMB0GA1UdJQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjCBjwYDVR0fBIGH
MIGEMECgPqA8hjpodHRwOi8vY3JsMy5kaWdpY2VydC5jb20vRGlnaUNlcnRUTFNS
U0FTSEEyNTYyMDIwQ0ExLTQuY3JsMECgPqA8hjpodHRwOi8vY3JsNC5kaWdpY2Vy
dC5jb20vRGlnaUNlcnRUTFNSU0FTSEEyNTYyMDIwQ0ExLTQuY3JsMD4GA1UdIAQ3
MDUwMwYGZ4EMAQICMCkwJwYIKwYBBQUHAgEWG2h0dHA6Ly93d3cuZGlnaWNlcnQu
Y29tL0NQUzB/BggrBgEFBQcBAQRzMHEwJAYIKwYBBQUHMAGGGGh0dHA6Ly9vY3Nw
LmRpZ2ljZXJ0LmNvbTBJBggrBgEFBQcwAoY9aHR0cDovL2NhY2VydHMuZGlnaWNl
cnQuY29tL0RpZ2lDZXJ0VExTUlNBU0hBMjU2MjAyMENBMS0xLmNydDAJBgNVHRME
AjAAMIIBfwYKKwYBBAHWeQIEAgSCAW8EggFrAWkAdgDoPtDaPvUGNTLnVyi8iWvJ
A9PL0RFr7Otp4Xd9bQa9bgAAAX9kHjD2AAAEAwBHMEUCIGtBH7mnWeRxvFLZN2E5
Q/9lrFm4Xhjcj9Zi9L9ThlzRAiEAulA+1XiMw6M5M23M/FB55fcvbIosAkQUAkuy
1yeaPv0AdgA1zxkbv7FsV78PrUxtQsu7ticgJlHqP+Eq76gDwzvWTAAAAX9kHjEd
AAAEAwBHMEUCIQDgRdzMBcsF6fI25ieut74nDBF0CMeI/3aXZKppdT6sdwIgU3Sy
90+7k1dyBUCGXqTJgodgkYLDaYNEvAQ+NmnA4nEAdwCzc3cH4YRQ+GOG1gWp3BEJ
SnktsWcMC4fc8AMOeTalmgAAAX9kHjFDAAAEAwBIMEYCIQC9aCfRJ6cPGwty3FP1
BAw3RRXQYr2Su4Xk+boJyNGe6gIhAIwV8BftA2Ee6dvSAhhtfOz5eddHy/am+lfJ
UYrw9j3jMA0GCSqGSIb3DQEBCwUAA4IBAQAMOtj25/qQDCzg1ceaZnWiORgyYpbh
ZGlR2jI9ujWPzbl/7SmUpFS6SnXaOh6L45NAR7Ld7Fhuqf34rgSobc5/cVaLMq5v
QduAlYq9aO5xG32TNsWQRXMFG9WFFg7HD00p8DMkF/cxXFACsCAwt1dGNbwbgAEj
+qn/TDymJ85HzQfcpTkQXvB7571DpDBvxPkYMxkzQtgb5Wz+VVyi2LL5J3AqOSWV
KKigsYqVwEiNTzgInknUmDHJN2igFUfpsPqVB41Xy8dc5SNTStbWsWLXA/0aHleK
D1TONGVLMXdZh3uFto9Q/E1kXw6LYKO9MUYnGweyFm7ipWERPzjE/w3N
-----END CERTIFICATE-----
```

### api.service.nhs.uk (Digicert) 

```
-----BEGIN CERTIFICATE-----
MIIHtDCCBpygAwIBAgIQCo1zwR1XPV9LCf6wELDvIzANBgkqhkiG9w0BAQsFADBP
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMSkwJwYDVQQDEyBE
aWdpQ2VydCBUTFMgUlNBIFNIQTI1NiAyMDIwIENBMTAeFw0yMjAzMDcwMDAwMDBa
Fw0yMzA0MDcyMzU5NTlaMFAxCzAJBgNVBAYTAkdCMQ4wDAYDVQQHEwVMZWVkczEU
MBIGA1UEChMLTkhTIERpZ2l0YWwxGzAZBgNVBAMTEmFwaS5zZXJ2aWNlLm5ocy51
azCCAiIwDQYJKoZIhvcNAQEBBQADggIPADCCAgoCggIBAL5Giwu+wLvQlcWJGZnV
5sswmYiknViv84orFv38P+9GLNXC48wMgJPu3rtuZsTe5JdtaVRPflXK4rxfuIUd
ybfbDmW4zeUn5Yj2ZdkoZMqLlLX7D9H04wl2Aw/C0OP+pMq3Ear6KuCA8Y9kF+zF
KcR1foUvc4Fw2LxkWal10S2lzPLTbN4f2pZjT3JT1HMobRDQKt4kG/XDGbpkox/9
xQSNHdLYemenKVFQLGt+EVc51NTfMHFg8KXR/T0gvs0e0r/IOZZxl1+NEXkIvnQQ
fYJQB+LeMgpuMK1dj8xBnHnmsO3B8vvwJDycrSq50BfvXZpARUDhAiy2n+WWoM+s
hKmuojkDmnBEVtq78eDDF40vMahzpDhgSHhzM5pdpIvnofXGO4IkzLrNKTGlIXl8
2PERRM7zScuAWl5P6OWX7ygN8uoUh+NdDoiWsbQxZrTTO7kFgIbiheEMzMH28Myi
BWN9/LvRYpqWSSW7R4/NNfd8M62ER36xWetYk/IHdSXfBbfg1hJQMK+QZrA+Io8T
QABhTc0eBxlctOYCsKeXkhOBNTokED8DwQSG8f+LN2tA48cX+HrSRZ0gYA4X6vbl
TpdlmxbqXjQeTCrG65qmh3gffPNzZc+Ck2qL4SVlHBLw2LowagmjVvyWnfP8o0dH
LIic/3Tbx5hzUGsX4OHiM55ZAgMBAAGjggOJMIIDhTAfBgNVHSMEGDAWgBS3a6Lq
qKqEjHnqtNoPmLLFlXa59DAdBgNVHQ4EFgQU6lxJ78pLAnSpbhbSmCSt+zZgPvow
NgYDVR0RBC8wLYISYXBpLnNlcnZpY2UubmhzLnVrghdwb3J0YWwuZGV2ZWxvcGVy
Lm5ocy51azAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsG
AQUFBwMCMIGPBgNVHR8EgYcwgYQwQKA+oDyGOmh0dHA6Ly9jcmwzLmRpZ2ljZXJ0
LmNvbS9EaWdpQ2VydFRMU1JTQVNIQTI1NjIwMjBDQTEtNC5jcmwwQKA+oDyGOmh0
dHA6Ly9jcmw0LmRpZ2ljZXJ0LmNvbS9EaWdpQ2VydFRMU1JTQVNIQTI1NjIwMjBD
QTEtNC5jcmwwPgYDVR0gBDcwNTAzBgZngQwBAgIwKTAnBggrBgEFBQcCARYbaHR0
cDovL3d3dy5kaWdpY2VydC5jb20vQ1BTMH8GCCsGAQUFBwEBBHMwcTAkBggrBgEF
BQcwAYYYaHR0cDovL29jc3AuZGlnaWNlcnQuY29tMEkGCCsGAQUFBzAChj1odHRw
Oi8vY2FjZXJ0cy5kaWdpY2VydC5jb20vRGlnaUNlcnRUTFNSU0FTSEEyNTYyMDIw
Q0ExLTEuY3J0MAkGA1UdEwQCMAAwggF8BgorBgEEAdZ5AgQCBIIBbASCAWgBZgB1
AOg+0No+9QY1MudXKLyJa8kD08vREWvs62nhd31tBr1uAAABf2QbUbgAAAQDAEYw
RAIgQ8/ac+so1XceqvA6MPcVg1uN4XobN1UKdhkbtPyCUCMCIFkXRGBI+H7pjyHR
qiRQjt2EUusUs5U+L9TqK807fkivAHUANc8ZG7+xbFe/D61MbULLu7YnICZR6j/h
Ku+oA8M71kwAAAF/ZBtRrQAABAMARjBEAiB2Efj+Xq7BsWTU6E+FfMQ0CXis2aSt
CpTqcpnnc5+GlgIgXJxSXIQ9N2dhiqcAtDEQmZzZUZLh+nK/JjHAq2MShVsAdgCz
c3cH4YRQ+GOG1gWp3BEJSnktsWcMC4fc8AMOeTalmgAAAX9kG1HcAAAEAwBHMEUC
IBLnTvDSHa4jE24pDTqMpvemVyA5n6+7laNwI4DKN128AiEA1UyzaSEpGulrYeJ0
0ht+Y6PxJSDbqOAGQdHQfSKwJo4wDQYJKoZIhvcNAQELBQADggEBAFlPTQfhMH/i
xhBxX6MqEo/LaRWsbJWeP1ncKph3M/UvFXJdHeTHoZlUWTyispY+81DRwzC0pFhr
UL0OxspiPcW3MI4hMzaFOOzEYr6n2Cpqm36e+Z3hM78a8AO3rMtSjnYStkl9jNfU
6aGHiuUxPkl95BxMkIO156UQpyVrRuVQ/WCQrJgo3R+C9QK+VTh91JUyyGf6NluM
iRWLy2pTVHUX+7nBWVFR7ACgdwij2utwIDtzyOjynR3KmLE8UWVIu0I1NLwpMnRc
47nIWuRFvU/obcmfqZk8LiQMwoOKoG6GEfF2/32i9o6ucmvhJwnpNbqOlne8kv4D
ysWdIG7hl3g=
-----END CERTIFICATE-----

```

## Outbound

All outbound connections from the BaRS API proxy to Receivers, with the exception of the Sandbox environment, will be secured using TLS-MA.

### PTL
The PTL environments will present a certificate issued by the NHS PTL Root Authority, as the RootCA. This does not include the Sandbox environment.

Details of the certificate chain described in the table below can be found in the [How to Connect Guidance](https://digital.nhs.uk/services/path-to-live-environments/integration-environment#rootca-and-subca-certificates).


| Certificate CN         | Thumbprint                               | Parent CN              | Parent Thumbprint                        | Environment |
|------------------------|------------------------------------------|------------------------|------------------------------------------|-------------|
| int.api.service.nhs.uk | ce7808839f72ea8ed4548b4de37546bed5d6dc9f | NHS INT Level 1C       | 5007daf3aeea1c1360ec0d1e9e5bedccc7182b79 | PTL         |
| NHS INT Level 1C       | 5007daf3aeea1c1360ec0d1e9e5bedccc7182b79 | NHS PTL Root Authority | 6287fa6e10a7dd90e62556f7c2814a6abf04590c | PTL         |
| NHS PTL Root Authority | 6287fa6e10a7dd90e62556f7c2814a6abf04590c | N/A                    | N/A                                      | PTL         |

###  int.api.service.nhs.uk (NHS PTL Root)

```
-----BEGIN CERTIFICATE-----
MIIE2jCCA8KgAwIBAgIEXcnbeTANBgkqhkiG9w0BAQsFADA2MQwwCgYDVQQKEwNu
aHMxCzAJBgNVBAsTAkNBMRkwFwYDVQQDExBOSFMgSU5UIExldmVsIDFDMB4XDTIx
MTAyMjA3MjUzNloXDTI0MTAyMjA3NTUzNlowQTEMMAoGA1UEChMDbmhzMRAwDgYD
VQQLEwdEZXZpY2VzMR8wHQYDVQQDExZpbnQuYXBpLnNlcnZpY2UubmhzLnVrMIIC
IjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwMXSm2iNiR4xxX1AYVDWkviT
rEjidc91Ypcg5BbK3hEIgx7tPsKleef87TCj/7Io6XxV95VyIVhv9mw0m2VYtd7+
o9aAXDxsagmGWI3WSPp4UnS99jrC1jKyoEw7yLlXK0spoJ8i7+nZDpcytmKEX5wb
O6I5+QW2fNA3/sCwUXbEfpZsyURa+plZGR9qWpTnLxFRkTb5zxasGS5MrBBsX3ZP
uEmU1qDcNQlwm59NXVQPfC07X/POd8/sHXFGdB0BhtSOTYeCAOa/IlE+sX1hdTyt
g1u8sRmOc2LPh5H5MN75A7oJuLbapWz+BvmUAAl3n+8pIUT2wpk/CjSUIQhWJRG0
W7RwnGiT3PF8ZTuY4xTT0EaZEDc/BEvo063xTY7Nnr770WaQAeDwVkdyDpMOkJh/
/aVN3uIjituTPhOzIbBYyXEFc59IJZAlWFMaFWMN5wo7JXhWhWLcxXU//bSMjU+K
e0yKHHpPdsVgwBV7mp4Pd6/PhrzCxhaGp5f3a0rn/+gmwuJCfjvcuV3twZBkmCdw
lpyjxQn/ZzJt2CuNAJRAW5J2FogpDxBxSk7NZnf255KaNUYEMF68Ff12RhuX7mmO
eIrpUwStZF8wfNv9suLPk9oWqt4DjAzdxgs5URRnkJbAGEv7je55A6mZxUJdfe1+
PKnqUy0tx7MuHUT/ZdsCAwEAAaOB5DCB4TALBgNVHQ8EBAMCBaAwHQYDVR0lBBYw
FAYIKwYBBQUHAwEGCCsGAQUFBwMCMBgGA1UdIAQRMA8wDQYLKoY6AIl7ZQADAQEw
MwYDVR0fBCwwKjAooCagJIYiaHR0cDovL2NybC5uaHMudWsvaW50LzFjL2NybGM3
LmNybDAfBgNVHSMEGDAWgBQABoJtq6YSQ+22DfTmPMQgwWGboDAdBgNVHQ4EFgQU
a1IdNWkENZuJ6oVZbX3tvyJUmX8wCQYDVR0TBAIwADAZBgkqhkiG9n0HQQAEDDAK
GwRWOC4zAwIEsDANBgkqhkiG9w0BAQsFAAOCAQEAM1vfrfUhzRfMsNprGI5qQE99
eRLGXsvWY45eWJKMcCvw4VBFbcABMxACfuO/arIQvYrkzpBpnF8fMu5tiwi+PgIQ
k7xIf2l7UsIM+f13gj+YDHsQaRF5MO3ywFC56/ybGEMI+pp6Co0pKvbXQtk14rRR
213tWOxoV9W/keEHiNZTOM54EbAzXwvsVjvIwyxxwDGNbhsLKfCYPLgHpExFMSFF
08fEKUAbPiLUUBIQpLtSGv/Sn/SAk1wh0nG2UXcjTGIX0ZNhT8DyYNonjg9kQ6J8
8g6Nu/awWRl7a6Kf9mWsxaspCGHYi5Q10tXSZdDuBzAkQJ0MZS3DZ7/mb+ISvQ==
-----END CERTIFICATE-----
```

### Prod

The production environment will present a certificate issued by the NHS Root Authority, as the RootCA.

Details of the certificate chain described in the table below can be found in the [How to Connect Guidance](https://digital.nhs.uk/services/path-to-live-environments/live-environment#rootca-and-subca-certificates)

| Certificate CN                  | Thumbprint                               | Parent CN          | Parent Thumbprint                        | Environment |
|---------------------------------|------------------------------------------|--------------------|------------------------------------------|-------------|
| bars-proxy.spineservices.nhs.uk | 57c911af253c2f8c362654f78f13e73051eeede3 | NHS Level 1C       | da3cf9d13a705704f2cba274c79794963c36ff94 | Prod        |
| NHS Level 1C                    | da3cf9d13a705704f2cba274c79794963c36ff94 | NHS Root Authority | ec7a3b3cb795ece956c5a7bec4204a298feb236c | Prod        |
| NHS Root Authority              | ec7a3b3cb795ece956c5a7bec4204a298feb236c | N/A                | N/A                                      | Prod        |

```
-----BEGIN CERTIFICATE-----
MIIEEjCCAvqgAwIBAgIEYQ6SIzANBgkqhkiG9w0BAQsFADAyMQwwCgYDVQQKDANu
aHMxCzAJBgNVBAsMAkNBMRUwEwYDVQQDDAxOSFMgTGV2ZWwgMUMwHhcNMjIxMjEy
MTU1NjI1WhcNMjQwNjA0MTEyODMxWjBKMQwwCgYDVQQKDANuaHMxEDAOBgNVBAsM
B0RldmljZXMxKDAmBgNVBAMMH2JhcnMtcHJveHkuc3BpbmVzZXJ2aWNlcy5uaHMu
dWswggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC+3ACj/4ijhnV9F4V9
Encu1ulski0sK36XX8etuwqRbpzW6dpRmACUE001zSp0Fg6kaW1OE13kfMNJzTgy
cjjL7FnQLG0UAuK7ghTKp/I7SvqwNkCCPVnMm+s1wfzBKQGbWRhsgiUy/jKizgTz
163BHoB8WzGPDwV0K+9nmf3tBiqi+dB1UWtBOZc9mUgqt9+Hy54pjX/aYVL//L04
24kSntJoP4pzeumTeHHKTLPv2FT3lfBW7cDh6cBZ62Dv15P1EopgZwirNrmZTFox
Hm0rmIh4WFQrtQ8TxNAKfBIq32hxL51bfJRctKgQGc/VDaQ2MoV2cSTZSF+6CQn8
E2wvAgMBAAGjggEWMIIBEjALBgNVHQ8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUH
AwEGCCsGAQUFBwMCMBgGA1UdIAQRMA8wDQYLKoY6AIl7ZQADAQEwNwYDVR0fBDAw
LjAsoCqgKIYmaHR0cDovL2NybC5uaHMudWsvbGl2ZS8xYy9jcmxjNDUxOS5jcmww
KwYDVR0QBCQwIoAPMjAyMjEyMTIxNTU2MjVagQ8yMDIzMTIyNTEyNTc1M1owHwYD
VR0jBBgwFoAUummj43rifD03V1Jv6fMTZEzhwLUwHQYDVR0OBBYEFNZdTAjy6Qt2
K/kPx7eoIPC6WnwRMAkGA1UdEwQCMAAwGQYJKoZIhvZ9B0EABAwwChsEVjguMwMC
BLAwDQYJKoZIhvcNAQELBQADggEBAEO5dJfCpEXu5PvYXvh0iHMLGeNd00ghyfMH
9F8rLw3LVTEWlrkOg1d76wEuHeBo2pM1A5YFvBkv+FpDxcKizqHXlryXZxIdkfMw
GEFIPBK+wdZAFDcKXlSZZUvUpvpC6MycJHN3i5sgE8jkugfmTZvc0orjg2pgh4y8
vsBI/yY8M4hqxF0fUd9msVo0tvCf8gNfMmRYN/3XfUrGtUjjBmXVj7GsKoijBqzS
ynbcbOis4iXQJz78K2lGMw0sGx44C7e+L+Bd/gr9B+locaEHXuDMYY/lH+ckcFGT
XOLsRJNdE3hyGSUwn7eCJA8La5XLrjo9EgfVo6GKX4sX1L+Ibtw=
-----END CERTIFICATE-----

```