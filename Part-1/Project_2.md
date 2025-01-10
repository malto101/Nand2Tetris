---
layout: default
title: Project 2
parent: Part 1
nav_order: 4
description: "Project 2 of Nand2Tetris."
permalink: /Part1/Project_2
has_children: false
includes:
  - head_custom.html
---

# Building Boolean Arthematics in Nand2Tetris

Here are the gates we'll be implementing:

1. **Half Adder**
2. **Full Adder**
3. **Add16**
4. **Inc16**
5. **ALU**

---

## 1. Half Adder

```
CHIP HalfAdder {
    IN a, b;    // 1-bit inputs
    OUT sum,    // Right bit of a + b 
        carry;  // Left bit of a + b

    PARTS:
    //// Replace this comment with your code.
    And(a=a , b=b , out=carry );
    Xor(a =a , b =b , out =sum );
}
```

## 2. Full Adder

```
CHIP FullAdder {
    IN a, b, c;  // 1-bit inputs
    OUT sum,     // Right bit of a + b + c
        carry;   // Left bit of a + b + c

    PARTS:
    //// Replace this comment with your code.
    HalfAdder(a=a , b=b , sum=halfsum , carry=halfcarry );
    HalfAdder(a=c , b=halfsum , sum=sum , carry=fullcarry);
    Or(a=halfcarry , b=fullcarry , out=carry );
}
```

## 3. Add16

On the LSB side, we will use Half adder as we have only 2 operands. And for the rest
we will use Hull Adder due to having 3 operands(carry).

```
CHIP Add16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.
    HalfAdder(a=a[0] , b=b[0] , sum=out[0] , carry=carry1 );
    FullAdder(a=a[1] , b=b[1] , c=carry1 , sum=out[1] , carry=carry2 );
    FullAdder(a=a[2] , b=b[2] , c=carry2 , sum=out[2] , carry=carry3 );
    FullAdder(a=a[3] , b=b[3] , c=carry3 , sum=out[3] , carry=carry4 );
    FullAdder(a=a[4] , b=b[4] , c=carry4 , sum=out[4] , carry=carry5 );
    FullAdder(a=a[5] , b=b[5] , c=carry5 , sum=out[5] , carry=carry6 );
    FullAdder(a=a[6] , b=b[6] , c=carry6 , sum=out[6] , carry=carry7 );
    FullAdder(a=a[7] , b=b[7] , c=carry7 , sum=out[7] , carry=carry8 );
    FullAdder(a=a[8] , b=b[8] , c=carry8 , sum=out[8] , carry=carry9 );
    FullAdder(a=a[9] , b=b[9] , c=carry9 , sum=out[9] , carry=carry10 );
    FullAdder(a=a[10] , b=b[10] , c=carry10 , sum=out[10] , carry=carry11 );
    FullAdder(a=a[11] , b=b[11] , c=carry11 , sum=out[11] , carry=carry12 );
    FullAdder(a=a[12] , b=b[12] , c=carry12 , sum=out[12] , carry=carry13 );
    FullAdder(a=a[13] , b=b[13] , c=carry13, sum=out[13] , carry=carry14 );
    FullAdder(a=a[14] , b=b[14] , c=carry14, sum=out[14] , carry=carry15 );
    FullAdder(a=a[15] , b=b[15] , c=carry15, sum=out[15] , carry=carry16 );
}
```

## 4. Inc16

We will use half adder between LSB(a[0]) and 1 and whatever gets carried, we will use
half adder between the carried component and next bit.

```
CHIP Inc16 {
    IN in[16];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.
    HalfAdder(a=in[0] , b=true , sum=out[0] , carry=carry0 );
    HalfAdder(a=in[1] , b=carry0 , sum=out[1] , carry=carry1 );
    HalfAdder(a=in[2] , b=carry1 , sum=out[2] , carry=carry2 );
    HalfAdder(a=in[3] , b=carry2 , sum=out[3] , carry=carry3 );
    HalfAdder(a=in[4] , b=carry3 , sum=out[4] , carry=carry4 );
    HalfAdder(a=in[5] , b=carry4 , sum=out[5] , carry=carry5 );
    HalfAdder(a=in[6] , b=carry5 , sum=out[6] , carry=carry6 );
    HalfAdder(a=in[7] , b=carry6 , sum=out[7] , carry=carry7 );
    HalfAdder(a=in[8] , b=carry7 , sum=out[8] , carry=carry8 );
    HalfAdder(a=in[9] , b=carry8 , sum=out[9] , carry=carry9 );
    HalfAdder(a=in[10] , b=carry9 , sum=out[10] , carry=carry10 );
    HalfAdder(a=in[11] , b=carry10 , sum=out[11] , carry=carry11 );
    HalfAdder(a=in[12] , b=carry11 , sum=out[12] , carry=carry12 );
    HalfAdder(a=in[13] , b=carry12 , sum=out[13] , carry=carry13 );
    HalfAdder(a=in[14] , b=carry13 , sum=out[14] , carry=carry14 );
    HalfAdder(a=in[15] , b=carry14 , sum=out[15] , carry=carry15 );

}
```

## 5. ALU

We can design the ALU by incorporating the previously designed components (like the  Add16 and Module 1 components) and adding logic gates to perform various operations based on control signals. The ALU typically takes two 16-bit inputs and performs operations based on 6 control signals:
	•	zx: Zero the first input.
	•	nx: Negate the first input.
	•	zy: Zero the second input.
	•	ny: Negate the second input.
	•	f: Choose between addition and AND operation.
	•	n: Negate the output.

```

CHIP ALU {
    IN  
        x[16], y[16],  // 16-bit inputs        
        zx, // zero the x input?
        nx, // negate the x input?
        zy, // zero the y input?
        ny, // negate the y input?
        f,  // compute (out = x + y) or (out = x & y)?
        no; // negate the out output?
    OUT 
        out[16], // 16-bit output
        zr,      // if (out == 0) equals 1, else 0
        ng;      // if (out < 0)  equals 1, else 0


    PARTS:
    //// Replace this comment with your code.
    //zx imlpementation
    Mux16(a=x , b=false , sel=zx , out=outzx);
    //nx implementation
    Not16(in=outzx , out=notoutzx );
    Mux16(a=outzx , b=notoutzx , sel=nx , out=outnx );
    //zy implementation
    Mux16(a=y , b=false , sel=zy , out=outzy);
    //ny implementation
    Not16(in=outzy , out=notoutzy );
    Mux16(a=outzy , b=notoutzy , sel=ny , out=outny);
    //f implementation
    Add16(a =outnx , b =outny , out =outadd );
    And16(a =outnx , b =outny , out =outand );
    Mux16(a=outand , b=outadd , sel=f , out=outf);
    //no implementation
    Not16(in=outf , out=notoutf );
    Mux16(a=outf , b=notoutf , sel=no , out=out, out[15]=signedbit, out[0..7]=left8, out[8..15]=right8 );
    //zr implementation
    Or8Way(in=left8, out=zr1);
    Or8Way(in=right8, out=zr2);
    Or(a=zr1, b=zr2, out=notzr);
    Not(in=notzr, out=zr);
    //ng implementation
    And(a=signedbit, b=true, out=ng);
}

```
