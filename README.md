# Learning tcpdump

## 1 启动 tcpdump 抓包

```sh
$ docker run -it --net=host corfr/tcpdump -XvvennSs 0 host info.cern.ch
tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
```

## 2 请求 info.cern.ch

```sh
docker exec -it 349e309e7468 /bin/sh
/ # wget http://info.cern.ch
Connecting to info.cern.ch (188.184.21.108:80)
index.html           100% |*********************************************************************************************************************************|   646   0:00:00 ETA
/ #
```

## 查看 tcpdump 输出

```sh
02:43:32.879660 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 74: (tos 0x0, ttl 64, id 11612, offset 0, flags [DF], proto TCP (6), length 60)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [S], cksum 0x9cfc (correct), seq 3356944636, win 64240, options [mss 1460,sackOK,TS val 3099954794 ecr 0,nop,wscale 7], length 0
	0x0000:  4500 003c 2d5c 4000 4006 3990 c0a8 4103  E..<-\@.@.9...A.
	0x0010:  bcb8 156c e3ae 0050 c816 e8fc 0000 0000  ...l...P........
	0x0020:  a002 faf0 9cfc 0000 0204 05b4 0402 080a  ................
	0x0030:  b8c5 8e6a 0000 0000 0103 0307            ...j........
02:43:32.889446 f6:16:36:bc:f9:c6 > 02:50:00:00:00:01, ethertype IPv4 (0x0800), length 62: (tos 0x0, ttl 38, id 40194, offset 0, flags [none], proto TCP (6), length 48)
    188.184.21.108.80 > 192.168.65.3.58286: Flags [S.], cksum 0xc396 (correct), seq 452869015, ack 3356944637, win 65535, options [mss 1460,wscale 2,eol], length 0
	0x0000:  4500 0030 9d02 0000 2606 23f6 bcb8 156c  E..0....&.#....l
	0x0010:  c0a8 4103 0050 e3ae 1afe 3b97 c816 e8fd  ..A..P....;.....
	0x0020:  7012 ffff c396 0000 0204 05b4 0303 0200  p...............
02:43:32.889801 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 64, id 11613, offset 0, flags [DF], proto TCP (6), length 40)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [.], cksum 0xee64 (correct), seq 3356944637, ack 452869016, win 502, length 0
	0x0000:  4500 0028 2d5d 4000 4006 39a3 c0a8 4103  E..(-]@.@.9...A.
	0x0010:  bcb8 156c e3ae 0050 c816 e8fd 1afe 3b98  ...l...P......;.
	0x0020:  5010 01f6 ee64 0000                      P....d..
02:43:32.891310 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 129: (tos 0x0, ttl 64, id 11614, offset 0, flags [DF], proto TCP (6), length 115)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [P.], cksum 0xa0e8 (correct), seq 3356944637:3356944712, ack 452869016, win 502, length 75: HTTP, length: 75
	GET / HTTP/1.1
	Host: info.cern.ch
	User-Agent: Wget
	Connection: close

	0x0000:  4500 0073 2d5e 4000 4006 3957 c0a8 4103  E..s-^@.@.9W..A.
	0x0010:  bcb8 156c e3ae 0050 c816 e8fd 1afe 3b98  ...l...P......;.
	0x0020:  5018 01f6 a0e8 0000 4745 5420 2f20 4854  P.......GET./.HT
	0x0030:  5450 2f31 2e31 0d0a 486f 7374 3a20 696e  TP/1.1..Host:.in
	0x0040:  666f 2e63 6572 6e2e 6368 0d0a 5573 6572  fo.cern.ch..User
	0x0050:  2d41 6765 6e74 3a20 5767 6574 0d0a 436f  -Agent:.Wget..Co
	0x0060:  6e6e 6563 7469 6f6e 3a20 636c 6f73 650d  nnection:.close.
	0x0070:  0a0d 0a                                  ...
02:43:32.892389 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 64, id 11615, offset 0, flags [DF], proto TCP (6), length 40)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [F.], cksum 0xee18 (correct), seq 3356944712, ack 452869016, win 502, length 0
	0x0000:  4500 0028 2d5f 4000 4006 39a1 c0a8 4103  E..(-_@.@.9...A.
	0x0010:  bcb8 156c e3ae 0050 c816 e948 1afe 3b98  ...l...P...H..;.
	0x0020:  5011 01f6 ee18 0000                      P.......
02:43:32.902487 f6:16:36:bc:f9:c6 > 02:50:00:00:00:01, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 38, id 16111, offset 0, flags [none], proto TCP (6), length 40)
    188.184.21.108.80 > 192.168.65.3.58286: Flags [.], cksum 0xf00f (correct), seq 452869016, ack 3356944712, win 65535, length 0
	0x0000:  4500 0028 3eef 0000 2606 8211 bcb8 156c  E..(>...&......l
	0x0010:  c0a8 4103 0050 e3ae 1afe 3b98 c816 e948  ..A..P....;....H
	0x0020:  5010 ffff f00f 0000                      P.......
02:43:32.902572 f6:16:36:bc:f9:c6 > 02:50:00:00:00:01, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 38, id 4222, offset 0, flags [none], proto TCP (6), length 40)
    188.184.21.108.80 > 192.168.65.3.58286: Flags [.], cksum 0xf00e (correct), seq 452869016, ack 3356944713, win 65535, length 0
	0x0000:  4500 0028 107e 0000 2606 b082 bcb8 156c  E..(.~..&......l
	0x0010:  c0a8 4103 0050 e3ae 1afe 3b98 c816 e949  ..A..P....;....I
	0x0020:  5010 ffff f00e 0000                      P.......
02:43:33.871007 f6:16:36:bc:f9:c6 > 02:50:00:00:00:01, ethertype IPv4 (0x0800), length 71: (tos 0x0, ttl 38, id 9103, offset 0, flags [none], proto TCP (6), length 57)
    188.184.21.108.80 > 192.168.65.3.58286: Flags [P.], cksum 0x3030 (correct), seq 452869016:452869033, ack 3356944713, win 65535, length 17: HTTP, length: 17
	HTTP/1.1 200 OK
	0x0000:  4500 0039 238f 0000 2606 9d60 bcb8 156c  E..9#...&..`...l
	0x0010:  c0a8 4103 0050 e3ae 1afe 3b98 c816 e949  ..A..P....;....I
	0x0020:  5018 ffff 3030 0000 4854 5450 2f31 2e31  P...00..HTTP/1.1
	0x0030:  2032 3030 204f 4b0d 0a                   .200.OK..
02:43:33.871231 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 64, id 11616, offset 0, flags [DF], proto TCP (6), length 40)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [.], cksum 0xee07 (correct), seq 3356944713, ack 452869033, win 502, length 0
	0x0000:  4500 0028 2d60 4000 4006 39a0 c0a8 4103  E..(-`@.@.9...A.
	0x0010:  bcb8 156c e3ae 0050 c816 e949 1afe 3ba9  ...l...P...I..;.
	0x0020:  5010 01f6 ee07 0000                      P.......
02:43:33.875293 f6:16:36:bc:f9:c6 > 02:50:00:00:00:01, ethertype IPv4 (0x0800), length 915: (tos 0x0, ttl 38, id 46873, offset 0, flags [none], proto TCP (6), length 901)
    188.184.21.108.80 > 192.168.65.3.58286: Flags [P.], cksum 0x1bb6 (correct), seq 452869033:452869894, ack 3356944713, win 65535, length 861: HTTP
	0x0000:  4500 0385 b719 0000 2606 068a bcb8 156c  E.......&......l
	0x0010:  c0a8 4103 0050 e3ae 1afe 3ba9 c816 e949  ..A..P....;....I
	0x0020:  5018 ffff 1bb6 0000 6163 6365 7074 2d72  P.......accept-r
	0x0030:  616e 6765 733a 2062 7974 6573 0d0a 636f  anges:.bytes..co
	0x0040:  6e6e 6563 7469 6f6e 3a20 636c 6f73 650d  nnection:.close.
	0x0050:  0a63 6f6e 7465 6e74 2d6c 656e 6774 683a  .content-length:
	0x0060:  2036 3436 0d0a 636f 6e74 656e 742d 7479  .646..content-ty
	0x0070:  7065 3a20 7465 7874 2f68 746d 6c0d 0a64  pe:.text/html..d
	0x0080:  6174 653a 2053 756e 2c20 3036 204a 756e  ate:.Sun,.06.Jun
	0x0090:  2032 3032 3120 3032 3a34 333a 3333 2047  .2021.02:43:33.G
	0x00a0:  4d54 0d0a 6574 6167 3a20 2232 3836 2d34  MT..etag:."286-4
	0x00b0:  6631 6161 6462 3331 3035 6330 220d 0a6c  f1aadb3105c0"..l
	0x00c0:  6173 742d 6d6f 6469 6669 6564 3a20 5765  ast-modified:.We
	0x00d0:  642c 2030 3520 4665 6220 3230 3134 2031  d,.05.Feb.2014.1
	0x00e0:  363a 3030 3a33 3120 474d 540d 0a73 6572  6:00:31.GMT..ser
	0x00f0:  7665 723a 2041 7061 6368 650d 0a0d 0a3c  ver:.Apache....<
	0x0100:  6874 6d6c 3e3c 6865 6164 3e3c 2f68 6561  html><head></hea
	0x0110:  643e 3c62 6f64 793e 3c68 6561 6465 723e  d><body><header>
	0x0120:  0a3c 7469 746c 653e 6874 7470 3a2f 2f69  .<title>http://i
	0x0130:  6e66 6f2e 6365 726e 2e63 683c 2f74 6974  nfo.cern.ch</tit
	0x0140:  6c65 3e0a 3c2f 6865 6164 6572 3e0a 0a3c  le>.</header>..<
	0x0150:  6831 3e68 7474 703a 2f2f 696e 666f 2e63  h1>http://info.c
	0x0160:  6572 6e2e 6368 202d 2068 6f6d 6520 6f66  ern.ch.-.home.of
	0x0170:  2074 6865 2066 6972 7374 2077 6562 7369  .the.first.websi
	0x0180:  7465 3c2f 6831 3e0a 3c70 3e46 726f 6d20  te</h1>.<p>From.
	0x0190:  6865 7265 2079 6f75 2063 616e 3a3c 2f70  here.you.can:</p
	0x01a0:  3e0a 3c75 6c3e 0a3c 6c69 3e3c 6120 6872  >.<ul>.<li><a.hr
	0x01b0:  6566 3d22 6874 7470 3a2f 2f69 6e66 6f2e  ef="http://info.
	0x01c0:  6365 726e 2e63 682f 6879 7065 7274 6578  cern.ch/hypertex
	0x01d0:  742f 5757 572f 5468 6550 726f 6a65 6374  t/WWW/TheProject
	0x01e0:  2e68 746d 6c22 3e42 726f 7773 6520 7468  .html">Browse.th
	0x01f0:  6520 6669 7273 7420 7765 6273 6974 653c  e.first.website<
	0x0200:  2f61 3e3c 2f6c 693e 0a3c 6c69 3e3c 6120  /a></li>.<li><a.
	0x0210:  6872 6566 3d22 6874 7470 3a2f 2f6c 696e  href="http://lin
	0x0220:  652d 6d6f 6465 2e63 6572 6e2e 6368 2f77  e-mode.cern.ch/w
	0x0230:  7777 2f68 7970 6572 7465 7874 2f57 5757  ww/hypertext/WWW
	0x0240:  2f54 6865 5072 6f6a 6563 742e 6874 6d6c  /TheProject.html
	0x0250:  223e 4272 6f77 7365 2074 6865 2066 6972  ">Browse.the.fir
	0x0260:  7374 2077 6562 7369 7465 2075 7369 6e67  st.website.using
	0x0270:  2074 6865 206c 696e 652d 6d6f 6465 2062  .the.line-mode.b
	0x0280:  726f 7773 6572 2073 696d 756c 6174 6f72  rowser.simulator
	0x0290:  3c2f 613e 3c2f 6c69 3e0a 3c6c 693e 3c61  </a></li>.<li><a
	0x02a0:  2068 7265 663d 2268 7474 703a 2f2f 686f  .href="http://ho
	0x02b0:  6d65 2e77 6562 2e63 6572 6e2e 6368 2f74  me.web.cern.ch/t
	0x02c0:  6f70 6963 732f 6269 7274 682d 7765 6222  opics/birth-web"
	0x02d0:  3e4c 6561 726e 2061 626f 7574 2074 6865  >Learn.about.the
	0x02e0:  2062 6972 7468 206f 6620 7468 6520 7765  .birth.of.the.we
	0x02f0:  623c 2f61 3e3c 2f6c 693e 0a3c 6c69 3e3c  b</a></li>.<li><
	0x0300:  6120 6872 6566 3d22 6874 7470 3a2f 2f68  a.href="http://h
	0x0310:  6f6d 652e 7765 622e 6365 726e 2e63 682f  ome.web.cern.ch/
	0x0320:  6162 6f75 7422 3e4c 6561 726e 2061 626f  about">Learn.abo
	0x0330:  7574 2043 4552 4e2c 2074 6865 2070 6879  ut.CERN,.the.phy
	0x0340:  7369 6373 206c 6162 6f72 6174 6f72 7920  sics.laboratory.
	0x0350:  7768 6572 6520 7468 6520 7765 6220 7761  where.the.web.wa
	0x0360:  7320 626f 726e 3c2f 613e 3c2f 6c69 3e0a  s.born</a></li>.
	0x0370:  3c2f 756c 3e0a 3c2f 626f 6479 3e3c 2f68  </ul>.</body></h
	0x0380:  746d 6c3e 0a                             tml>.
02:43:33.875332 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 64, id 11617, offset 0, flags [DF], proto TCP (6), length 40)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [.], cksum 0xeaab (correct), seq 3356944713, ack 452869894, win 501, length 0
	0x0000:  4500 0028 2d61 4000 4006 399f c0a8 4103  E..(-a@.@.9...A.
	0x0010:  bcb8 156c e3ae 0050 c816 e949 1afe 3f06  ...l...P...I..?.
	0x0020:  5010 01f5 eaab 0000                      P.......
02:43:33.875375 f6:16:36:bc:f9:c6 > 02:50:00:00:00:01, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 38, id 42104, offset 0, flags [none], proto TCP (6), length 40)
    188.184.21.108.80 > 192.168.65.3.58286: Flags [F.], cksum 0xec9f (correct), seq 452869894, ack 3356944713, win 65535, length 0
	0x0000:  4500 0028 a478 0000 2606 1c88 bcb8 156c  E..(.x..&......l
	0x0010:  c0a8 4103 0050 e3ae 1afe 3f06 c816 e949  ..A..P....?....I
	0x0020:  5011 ffff ec9f 0000                      P.......
02:43:33.875407 02:50:00:00:00:01 > f6:16:36:bc:f9:c6, ethertype IPv4 (0x0800), length 54: (tos 0x0, ttl 64, id 11618, offset 0, flags [DF], proto TCP (6), length 40)
    192.168.65.3.58286 > 188.184.21.108.80: Flags [.], cksum 0xeaaa (correct), seq 3356944713, ack 452869895, win 501, length 0
	0x0000:  4500 0028 2d62 4000 4006 399e c0a8 4103  E..(-b@.@.9...A.
	0x0010:  bcb8 156c e3ae 0050 c816 e949 1afe 3f07  ...l...P...I..?.
	0x0020:  5010 01f5 eaaa 0000                      P.......
^C
13 packets captured
17 packets received by filter
0 packets dropped by kernel
```

可以看到 `tcp` 三次握手和四次挥手，以及 GET 请求和 HTTP 200 OK 的响应。
