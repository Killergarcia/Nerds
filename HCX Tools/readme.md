# HCX Tools

## hcxdumptool

```
hcxdumptool -o capture.pcapng -i [interface] --enable_status=1
```

Hcxdumptool uses PMKID stuff to avoid needing the 4 way handshake for capturing PWs

https://hashcat.net/forum/thread-7717.html

## hcxpcapngtool

```
hcxpcapngtool -o capture_hash.txt [capture file]
```

```
hashcat -m 22000 [captured hash] -a3 ?l?l?l?l?l?l?l?l
```
