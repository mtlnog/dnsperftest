# DNS Performance test

Shell script to test the performance of the most popular DNS resolvers from your location.

Includes by default:
 * Cisco OpenDNS - 208.67.222.123
 * CIRA Canadian Shield - 149.112.121.10
 * Cloudflare - 1.1.1.1
 * Comodo Secure - 8.20.247.20
 * Google - 8.8.8.8
 * Quad9 - 9.9.9.9

# Required 

You need to install bc and dig. 

For Ubuntu:

```
 $ sudo apt-get install bc dnsutils
```

For macOS using homebrew:

```
 $ brew install bc bind
```

# Utilization

``` 
 $ git clone --depth=1 https://github.com/mtlnog/dnsperftest/
 $ cd dnsperftest
 $ bash ./dnstest.sh
                     test1   test2   test3   test4   test5   test6   test7   test8   test9   Average 
127.0.0.53           1 ms    12 ms   1 ms    1 ms    1 ms    1 ms    1 ms    12 ms   1 ms      3.44
CloudflareDNS        4 ms    4 ms    4 ms    1 ms    4 ms    1 ms    1 ms    4 ms    1 ms      2.66
GooglePublicDNS      1 ms    8 ms    1 ms    4 ms    1 ms    1 ms    1 ms    16 ms   44 ms     8.55
ComodoSecureDNS      8 ms    16 ms   8 ms    12 ms   8 ms    8 ms    8 ms    8 ms    8 ms      9.33
Quad9                4 ms    8 ms    8 ms    4 ms    4 ms    4 ms    1 ms    4 ms    4 ms      4.55
CIRA-CanadianShield  8 ms    8 ms    4 ms    8 ms    8 ms    8 ms    8 ms    8 ms    8 ms      7.55
Cisco-OpenDNS        8 ms    20 ms   16 ms   32 ms   28 ms   4 ms    8 ms    44 ms   36 ms     21.77
```

To sort with the fastest first, add `sort -k 20 -n` at the end of the command:

```
  $ bash ./dnstest.sh | sort -k 20 -n
                     test1   test2   test3   test4   test5   test6   test7   test8   test9   Average 
CloudflareDNS        1 ms    1 ms    1 ms    4 ms    1 ms    4 ms    4 ms    4 ms    4 ms      2.66
127.0.0.53           12 ms   12 ms   1 ms    1 ms    1 ms    1 ms    4 ms    8 ms    1 ms      4.55
CIRA-CA_Shield       8 ms    8 ms    8 ms    8 ms    4 ms    4 ms    8 ms    8 ms    8 ms      7.11
GooglePublicDNS      16 ms   12 ms   4 ms    16 ms   4 ms    1 ms    1 ms    12 ms   1 ms      7.44
Quad9                12 ms   28 ms   4 ms    4 ms    20 ms   1 ms    1 ms    40 ms   1 ms      12.33
ComodoSecureDNS      8 ms    20 ms   8 ms    8 ms    32 ms   8 ms    8 ms    132 ms  8 ms      25.77
Cisco-OpenDNS        56 ms   92 ms   8 ms    36 ms   40 ms   4 ms    8 ms    36 ms   8 ms      32.00
```

To test using the IPv6 addresses, add the "ipv6" option:

```
  $ bash ./dnstest.sh ipv6 | sort -k 20 -n
                     test1   test2   test3   test4   test5   test6   test7   test8   test9   Average 
CIRA-CA_Shield_v6    1 ms    1 ms    1 ms    1 ms    4 ms    1 ms    1 ms    4 ms    1 ms      1.66
CloudflareDNS_v6     4 ms    4 ms    8 ms    4 ms    4 ms    1 ms    4 ms    4 ms    1 ms      3.77
127.0.0.53           12 ms   12 ms   1 ms    1 ms    8 ms    1 ms    1 ms    12 ms   1 ms      5.44
GooglePublicDNS_v6   20 ms   12 ms   4 ms    16 ms   4 ms    4 ms    1 ms    12 ms   4 ms      8.55
Quad9_v6             1 ms    4 ms    16 ms   1 ms    44 ms   4 ms    1 ms    28 ms   4 ms      11.44
Cisco-OpenDNS_v6     92 ms   24 ms   8 ms    32 ms   44 ms   8 ms    8 ms    36 ms   8 ms      28.88
```

To test both IPv6 and IPv4, add the "all" option:
```
  $ bash ./dnstest.sh all | sort -k 20 -n
                     test1   test2   test3   test4   test5   test6   test7   test8   test9   Average 
CIRA-CA_Shield_v6    1 ms    1 ms    4 ms    1 ms    1 ms    4 ms    1 ms    4 ms    1 ms      2.00
Quad9                1 ms    1 ms    4 ms    1 ms    1 ms    1 ms    1 ms    4 ms    4 ms      2.00
CloudflareDNS_v6     1 ms    4 ms    16 ms   4 ms    1 ms    1 ms    1 ms    1 ms    4 ms      3.66
CIRA-CA_Shield       8 ms    8 ms    8 ms    8 ms    4 ms    8 ms    8 ms    4 ms    8 ms      7.11
GooglePublicDNS      4 ms    12 ms   1 ms    20 ms   12 ms   4 ms    1 ms    12 ms   1 ms      7.44
ComodoSecureDNS      8 ms    8 ms    8 ms    8 ms    8 ms    8 ms    8 ms    8 ms    8 ms      8.00
GooglePublicDNS_v6   1 ms    4 ms    12 ms   20 ms   4 ms    4 ms    1 ms    16 ms   16 ms     8.66
127.0.0.53           4 ms    12 ms   4 ms    1 ms    1 ms    1 ms    4 ms    80 ms   1 ms      12.00
Quad9_v6             4 ms    164 ms  1 ms    1 ms    4 ms    8 ms    1 ms    1 ms    1 ms      20.55
Cisco-OpenDNS_v6     36 ms   128 ms  20 ms   8 ms    24 ms   8 ms    8 ms    36 ms   8 ms      30.66
CloudflareDNS        260 ms  1 ms    8 ms    4 ms    4 ms    4 ms    1 ms    1 ms    1 ms      31.55
Cisco-OpenDNS        40 ms   92 ms   8 ms    28 ms   28 ms   8 ms    8 ms    40 ms   40 ms     32.44
```
