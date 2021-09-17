```
$ cat objdump.txt

memory.o:     file format elf32-littlearm

Contents of section .text:
 0000 04b02de5 00b08de2 14d04de2 0130a0e3  ..-.......M..0..
 0010 08300be5 0230a0e3 0c300be5 08201be5  .0...0...0... ..
 0020 0c301be5 033082e0 10300be5 10301be5  .0...0...0...0..
 0030 0300a0e1 00d08be2 04b09de4 1eff2fe1  ............../.
Contents of section .debug_info:
 0000 67000000 04000000 00000401 14000000  g...............
 0010 0c6c0000 00000000 00000000 00400000  .l...........@..
 0020 00000000 00020f00 00000101 63000000  ............c...
 0030 00000000 40000000 019c6300 00000361  ....@.....c....a
 0040 00010263 00000002 91740362 00010363  ...c.....t.b...c
 0050 00000002 91700363 00010463 00000002  .....p.c...c....
 0060 916c0004 0405696e 740000             .l....int..
Contents of section .debug_abbrev:
 0000 01110125 0e130b03 0e1b0e11 01120610  ...%............
 0010 17000002 2e013f19 030e3a0b 3b0b2719  ......?...:.;.'.
 0020 49131101 12064018 97421901 13000003  I.....@..B......
 0030 34000308 3a0b3b0b 49130218 00000424  4...:.;.I......$
 0040 000b0b3e 0b030800 0000               ...>......
Contents of section .debug_aranges:
 0000 1c000000 02000000 00000400 00000000  ................
 0010 00000000 40000000 00000000 00000000  ....@...........
Contents of section .debug_line:
 0000 37000000 02001f00 00000201 fb0e0d00  7...............
 0010 01010101 00000001 00000100 6d656d6f  ............memo
 0020 72792e63 00000000 00000502 00000000  ry.c............
 0030 01674b4b 842f0208 000101             .gKK./.....
Contents of section .debug_str:
 0000 2f686f6d 652f7069 2f334269 6e66006d  /home/pi/3Binf.m
 0010 61696e00 474e5520 43313120 362e332e  ain.GNU C11 6.3.
 0020 30203230 31373035 3136202d 6d617263  0 20170516 -marc
 0030 683d6172 6d763620 2d6d666c 6f61742d  h=armv6 -mfloat-
 0040 6162693d 68617264 202d6d66 70753d76  abi=hard -mfpu=v
 0050 6670202d 6d746c73 2d646961 6c656374  fp -mtls-dialect
 0060 3d676e75 202d6720 2d4f3000 6d656d6f  =gnu -g -O0.memo
 0070 72792e63 00                          ry.c.
Contents of section .comment:
 0000 00474343 3a202852 61737062 69616e20  .GCC: (Raspbian
 0010 362e332e 302d3138 2b727069 312b6465  6.3.0-18+rpi1+de
 0020 62397531 2920362e 332e3020 32303137  b9u1) 6.3.0 2017
 0030 30353136 00                          0516.
Contents of section .debug_frame:
 0000 0c000000 ffffffff 0100027c 0e0c0d00  ...........|....
 0010 1c000000 00000000 00000000 40000000  ............@...
 0020 420e048b 01420d0b 580d0d42 cb0e0000  B....B..X..B....
Contents of section .ARM.attributes:
 0000 412e0000 00616561 62690001 24000000  A....aeabi..$...
 0010 05360006 06080109 010a0212 04140115  .6..............
 0020 01170318 0119011a 021c011e 062201    .............".

Disassembly of section .text:

00000000 <main>:
#include <stdio.h>
   0:	e52db004 	push	{fp}		; (str fp, [sp, #-4]!)
   4:	e28db000 	add	fp, sp, #0
   8:	e24dd014 	sub	sp, sp, #20
int main(void) {
   c:	e3a03001 	mov	r3, #1
  10:	e50b3008 	str	r3, [fp, #-8]
	int a = 1;
  14:	e3a03002 	mov	r3, #2
  18:	e50b300c 	str	r3, [fp, #-12]
	int b = 2;
  1c:	e51b2008 	ldr	r2, [fp, #-8]
  20:	e51b300c 	ldr	r3, [fp, #-12]
  24:	e0823003 	add	r3, r2, r3
  28:	e50b3010 	str	r3, [fp, #-16]
	int c = a+b;
	printf("posizione in memoria di a: 0x%08llx\n",(long int)&a);
  2c:	e51b3010 	ldr	r3, [fp, #-16]
	printf("posizione in memoria di b: 0x%08llx\n",(long int)&b);
  30:	e1a00003 	mov	r0, r3
  34:	e28bd000 	add	sp, fp, #0
  38:	e49db004 	pop	{fp}		; (ldr fp, [sp], #4)
  3c:	e12fff1e 	bx	lr
  ```
