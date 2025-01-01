---
layout: default
title: Project 1
parent: Part 1
nav_order: 4
description: "Project 1 of Nand2Tetris."
permalink: /Part1/Project_1
has_children: false
includes:
  - head_custom.html
---

# Building Fundamental Gates in Nand2Tetris 

In this blog, we will implement the fundamental gates required for Nand2Tetris in **Hardware Description Language ()**. All gates are built from the **Nand** gate, which is the only primitive available in this system.

Here are the gates we'll be implementing:

1. **NOT**
2. **AND**
3. **OR**
4. **XOR**
5. **Mux**
6. **DMux**
7. **NOT16**
8. **AND16**
9. **OR16**
10. **Mux16**
11. **DMux16**
12. **Mux4Way16**
13. **Mux8Way16**
14. **DMux4Way**
15. **DMux8Way**

---

## 1. NOT Gate

```
CHIP Not {
    IN in;
    OUT out;

    PARTS:
    Nand(a=in, b=in, out=out);
}
```

## 2. AND Gate

```
CHIP And {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=na);
    Not(in=na, out=out);
}
```

## 3. OR Gate

```
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=nab);
    Or(a=a, b=b, out=ab);
    And(a=nab, b=ab, out=out);
}
```

## 4. XOR Gate

```
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=nab);
    Or(a=a, b=b, out=ab);
    And(a=nab, b=ab, out=out);
}
```

## 5. Mux Gate

```
CHIP Mux {
    IN a, b, sel;
    OUT out;

    PARTS:
    Not(in=sel, out=nsel);
    And(a=a, b=nsel, out=out1);
    And(a=b, b=sel, out=out2);
    Or(a=out1, b=out2, out=out);
}
```

## 6. DMux Gate

```
CHIP DMux {
    IN in, sel;
    OUT a, b;

    PARTS:
    Not(in=sel, out=nsel);
    And(a=in, b=nsel, out=a);
    And(a=in, b=sel, out=b);
}
```

## 7. NOT15 Gate

```
CHIP Not16 {
    IN in[16];
    OUT out[16];

    PARTS:
    Nand16(a=in, b=in, out=out);
}
```

## 8. AND16 Gate

```
CHIP And16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    Nand16(a=a, b=b, out=nandOut);
    Not16(in=nandOut, out=out);
}
```

## 9. OR16 Gate

```
CHIP Or16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    Not16(in=a, out=notA);
    Not16(in=b, out=notB);
    Nand16(a=notA, b=notB, out=out);
}
```

## 10. MUX16 Gate

```
CHIP Mux16 {
    IN a[16], b[16], sel;
    OUT out[16];

    PARTS:
    Not(in=sel, out=notSel);
    And16(a=a, b[0..15]=notSel, out=selA);
    And16(a=b, b[0..15]=sel, out=selB);
    Or16(a=selA, b=selB, out=out);
}
```

## 11. DMUX16 Gate

```
CHIP DMux8Way {
    IN in, sel[3];
    OUT a, b, c, d, e, f, g, h;

    PARTS:
    DMux(in=in, sel=sel[2], a=abcd, b=efgh);
    DMux4Way(in=abcd, sel=sel[0..1], a=a, b=b, c=c, d=d);
    DMux4Way(in=efgh, sel=sel[0..1], a=e, b=f, c=g, d=h);
}
```

## 12.MUX4Way16 Gate

```
CHIP Mux4Way16 {
    IN a[16], b[16], c[16], d[16], sel[2];
    OUT out[16];

    PARTS:
    Mux(a=a, b=b, sel=sel[0], out=ab[16]);
    Mux(a=c, b=d, sel=sel[0], out=cd[16]);
    Mux(a=ab, b=cd, sel=sel[1], out=out);
}
```

## 13. MUX8Way16 Gate

```
CHIP Mux8Way16 {
    IN a[16], b[16], c[16], d[16], e[16], f[16], g[16], h[16], sel[3];
    OUT out[16];

    PARTS:
    Mux4Way16(a=a, b=b, c=c, d=d, sel=sel[0..1], out=abcd[16]);
    Mux4Way16(a=e, b=f, c=g, d=h, sel=sel[0..1], out=efgh[16]);
    Mux(a=abcd, b=efgh, sel=sel[2], out=out);
}
```

## 14. DMUX4Way Gate

```
CHIP DMux8Way {
    IN in, sel[3];
    OUT a, b, c, d, e, f, g, h;

    PARTS:
    DMux(in=in, sel=sel[2], a=abcd, b=efgh);
    DMux4Way(in=abcd, sel=sel[0..1], a=a, b=b, c=c, d=d);
    DMux4Way(in=efgh, sel=sel[0..1], a=e, b=f, c=g, d=h);
}
```

## 15. DMUX8Way Gate

```
CHIP DMux8Way {
    IN in, sel[3];
    OUT a, b, c, d, e, f, g, h;

    PARTS:
    DMux(in=in, sel=sel[2], a=abcd, b=efgh);
    DMux4Way(in=abcd, sel=sel[0..1], a=a, b=b, c=c, d=d);
    DMux4Way(in=efgh, sel=sel[0..1], a=e, b=f, c=g, d=h);
}
```

## 16. OR8Way

```
CHIP Or8Way {
    IN in[8];
    OUT out;

    PARTS:
    Or(a=in[0], b=in[1], out=or1);
    Or(a=in[2], b=in[3], out=or2);
    Or(a=in[4], b=in[5], out=or3);
    Or(a=in[6], b=in[7], out=or4);
    Or(a=or1, b=or2, out=or5);
    Or(a=or3, b=or4, out=or6);
    Or(a=or5, b=or6, out=out);
}
```