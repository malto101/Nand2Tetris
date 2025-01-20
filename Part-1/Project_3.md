---
layout: default
title: Project 3
parent: Part 1
nav_order: 4
description: "Project 3 of Nand2Tetris."
permalink: /Part1/Project_3
has_children: false
includes:
  - head_custom.html
---

# Building Memory units in Nand2Tetris

Below are the gates we will be implementing.

1. **Bit**
2. **Register**
3. **RAM8**
4. **RAM64**
5. **RAM512**
6. **RAM4K**
7. **RAM16K**
8. **(Program Counter)PC**

---

## 1. Bit

```
CHIP Bit {
    IN in, load;
    OUT out;

    PARTS:
    //// Replace this comment with your code.
    Mux(a=tempout , b=in,   sel=load , out=tempin);
    DFF(in=tempin , out=out, out=tempout );
    
}
```

## 2. Register

```
CHIP Register {
    IN in[16], load;
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.
    Bit(in=in[0] , load=load , out=out[0] );
    Bit(in=in[1] , load=load , out=out[1] );    
    Bit(in=in[2] , load=load , out=out[2] );    
    Bit(in=in[3] , load=load , out=out[3] );    
    Bit(in=in[4] , load=load , out=out[4] );    
    Bit(in=in[5] , load=load , out=out[5] );    
    Bit(in=in[6] , load=load , out=out[6] );    
    Bit(in=in[7] , load=load , out=out[7] );    
    Bit(in=in[8] , load=load , out=out[8] );    
    Bit(in=in[9] , load=load , out=out[9] );    
    Bit(in=in[10] , load=load , out=out[10] );    
    Bit(in=in[11] , load=load , out=out[11] );    
    Bit(in=in[12] , load=load , out=out[12] );    
    Bit(in=in[13] , load=load , out=out[13] );    
    Bit(in=in[14] , load=load , out=out[14] );    
    Bit(in=in[15] , load=load , out=out[15] );    
    
}
```

## 3. RAM8

```
CHIP RAM8 {
    IN in[16], load, address[3];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.


    DMux8Way(in=in[0] , sel=address , a=a0 , b=b0, c=c0 , d=d0 , e=e0 , f=f0 , g=g0 , h=h0 );
    DMux8Way(in=in[1] , sel=address , a=a1 , b=b1, c=c1 , d=d1 , e=e1 , f=f1 , g=g1 , h=h1 );
    DMux8Way(in=in[2] , sel=address , a=a2 , b=b2, c=c2 , d=d2 , e=e2 , f=f2 , g=g2 , h=h2 );
    DMux8Way(in=in[3] , sel=address , a=a3 , b=b3, c=c3 , d=d3 , e=e3 , f=f3 , g=g3 , h=h3 );
    DMux8Way(in=in[4] , sel=address , a=a4 , b=b4, c=c4 , d=d4 , e=e4 , f=f4 , g=g4 , h=h4 );
    DMux8Way(in=in[5] , sel=address , a=a5 , b=b5, c=c5 , d=d5 , e=e5 , f=f5 , g=g5 , h=h5 );
    DMux8Way(in=in[6] , sel=address , a=a6 , b=b6, c=c6 , d=d6 , e=e6 , f=f6 , g=g6 , h=h6 );
    DMux8Way(in=in[7] , sel=address , a=a7 , b=b7, c=c7 , d=d7 , e=e7 , f=f7 , g=g7 , h=h7 );
    DMux8Way(in=in[8] , sel=address , a=a8 , b=b8, c=c8 , d=d8 , e=e8 , f=f8 , g=g8 , h=h8 );
    DMux8Way(in=in[9] , sel=address , a=a9 , b=b9, c=c9 , d=d9 , e=e9 , f=f9 , g=g9 , h=h9 );
    DMux8Way(in=in[10] , sel=address , a=a10 , b=b10, c=c10 , d=d10 , e=e10 , f=f10 , g=g10 , h=h10 );
    DMux8Way(in=in[11] , sel=address , a=a11 , b=b11, c=c11 , d=d11 , e=e11 , f=f11 , g=g11 , h=h11 );
    DMux8Way(in=in[12] , sel=address , a=a12 , b=b12, c=c12 , d=d12 , e=e12 , f=f12 , g=g12 , h=h12 );
    DMux8Way(in=in[13] , sel=address , a=a13 , b=b13, c=c13 , d=d13 , e=e13 , f=f13 , g=g13 , h=h13 );
    DMux8Way(in=in[14] , sel=address , a=a14 , b=b14, c=c14 , d=d14 , e=e14 , f=f14 , g=g14 , h=h14 );
    DMux8Way(in=in[15] , sel=address , a=a15 , b=b15, c=c15 , d=d15 , e=e15 , f=f15 , g=g15 , h=h15 );

    DMux8Way(in=load , sel=address , a=loada , b=loadb , c=loadc , d=loadd , e=loade , f=loadf , g=loadg , h=loadh );

    Register(in[0]=a0, in[1] =a1, in[2]=a2 ,in[3]=a3, in[4]=a4, in[5]=a5, in[6]=a6, in[7]=a7,in[8]= a8, in[9]=a9, in[10]=a10, in[11]=a11, in[12]=a12, in[13]=a13, in[14]=a14, in[15]=a15 , load=loada , out=a );
    Register(in[0]=b0, in[1] =b1, in[2]=b2 ,in[3]=b3, in[4]=b4, in[5]=b5, in[6]=b6, in[7]=b7,in[8]= b8, in[9]=b9, in[10]=b10, in[11]=b11, in[12]=b12, in[13]=b13, in[14]=b14, in[15]=b15 , load=loadb , out=b );
    Register(in[0]=c0, in[1] =c1, in[2]=c2 ,in[3]=c3, in[4]=c4, in[5]=c5, in[6]=c6, in[7]=c7,in[8]= c8, in[9]=c9, in[10]=c10, in[11]=c11, in[12]=c12, in[13]=c13, in[14]=c14, in[15]=c15 , load=loadc , out=c );
    Register(in[0]=d0, in[1] =d1, in[2]=d2 ,in[3]=d3, in[4]=d4, in[5]=d5, in[6]=d6, in[7]=d7,in[8]= d8, in[9]=d9, in[10]=d10, in[11]=d11, in[12]=d12, in[13]=d13, in[14]=d14, in[15]=d15 , load=loadd , out=d );
    Register(in[0]=e0, in[1] =e1, in[2]=e2 ,in[3]=e3, in[4]=e4, in[5]=e5, in[6]=e6, in[7]=e7,in[8]= e8, in[9]=e9, in[10]=e10, in[11]=e11, in[12]=e12, in[13]=e13, in[14]=e14, in[15]=e15 , load=loade , out=e );
    Register(in[0]=f0, in[1] =f1, in[2]=f2 ,in[3]=f3, in[4]=f4, in[5]=f5, in[6]=f6, in[7]=f7,in[8]= f8, in[9]=f9, in[10]=f10, in[11]=f11, in[12]=f12, in[13]=f13, in[14]=f14, in[15]=f15 , load=loadf , out=f );
    Register(in[0]=g0, in[1] =g1, in[2]=g2 ,in[3]=g3, in[4]=g4, in[5]=g5, in[6]=g6, in[7]=g7,in[8]= g8, in[9]=g9, in[10]=g10, in[11]=g11, in[12]=g12, in[13]=g13, in[14]=g14, in[15]=g15 , load=loadg , out=g );
    Register(in[0]=h0, in[1] =h1, in[2]=h2 ,in[3]=h3, in[4]=h4, in[5]=h5, in[6]=h6, in[7]=h7,in[8]= h8, in[9]=h9, in[10]=h10, in[11]=h11, in[12]=h12, in[13]=h13, in[14]=h14, in[15]=h15 , load=loadh , out=h );

    Mux8Way16(a=a , b=b , c=c , d=d , e=e , f=f , g=g , h=h , sel=address , out=out );

}
```

## 4. RAM64

```

CHIP RAM64 {
    IN in[16], load, address[6];
    OUT out[16];

    PARTS:

    //// Replace this comment with your code.

    DMux8Way(in=in[0] , sel=address[0..2] , a=a0 , b=b0, c=c0 , d=d0 , e=e0 , f=f0 , g=g0 , h=h0 );
    DMux8Way(in=in[1] , sel=address[0..2] , a=a1 , b=b1, c=c1 , d=d1 , e=e1 , f=f1 , g=g1 , h=h1 );
    DMux8Way(in=in[2] , sel=address[0..2] , a=a2 , b=b2, c=c2 , d=d2 , e=e2 , f=f2 , g=g2 , h=h2 );
    DMux8Way(in=in[3] , sel=address[0..2] , a=a3 , b=b3, c=c3 , d=d3 , e=e3 , f=f3 , g=g3 , h=h3 );
    DMux8Way(in=in[4] , sel=address[0..2] , a=a4 , b=b4, c=c4 , d=d4 , e=e4 , f=f4 , g=g4 , h=h4 );
    DMux8Way(in=in[5] , sel=address[0..2] , a=a5 , b=b5, c=c5 , d=d5 , e=e5 , f=f5 , g=g5 , h=h5 );
    DMux8Way(in=in[6] , sel=address[0..2] , a=a6 , b=b6, c=c6 , d=d6 , e=e6 , f=f6 , g=g6 , h=h6 );
    DMux8Way(in=in[7] , sel=address[0..2] , a=a7 , b=b7, c=c7 , d=d7 , e=e7 , f=f7 , g=g7 , h=h7 );
    DMux8Way(in=in[8] , sel=address[0..2] , a=a8 , b=b8, c=c8 , d=d8 , e=e8 , f=f8 , g=g8 , h=h8 );
    DMux8Way(in=in[9] , sel=address[0..2] , a=a9 , b=b9, c=c9 , d=d9 , e=e9 , f=f9 , g=g9 , h=h9 );
    DMux8Way(in=in[10] , sel=address[0..2] , a=a10 , b=b10, c=c10 , d=d10 , e=e10 , f=f10 , g=g10 , h=h10 );
    DMux8Way(in=in[11] , sel=address[0..2] , a=a11 , b=b11, c=c11 , d=d11 , e=e11 , f=f11 , g=g11 , h=h11 );
    DMux8Way(in=in[12] , sel=address[0..2] , a=a12 , b=b12, c=c12 , d=d12 , e=e12 , f=f12 , g=g12 , h=h12 );
    DMux8Way(in=in[13] , sel=address[0..2] , a=a13 , b=b13, c=c13 , d=d13 , e=e13 , f=f13 , g=g13 , h=h13 );
    DMux8Way(in=in[14] , sel=address[0..2] , a=a14 , b=b14, c=c14 , d=d14 , e=e14 , f=f14 , g=g14 , h=h14 );
    DMux8Way(in=in[15] , sel=address[0..2] , a=a15 , b=b15, c=c15 , d=d15 , e=e15 , f=f15 , g=g15 , h=h15 );

    DMux8Way(in=load , sel=address[0..2] , a=loada , b=loadb , c=loadc , d=loadd , e=loade , f=loadf , g=loadg , h=loadh );

    RAM8(in[0]=a0, in[1] =a1, in[2]=a2 ,in[3]=a3, in[4]=a4, in[5]=a5, in[6]=a6, in[7]=a7,in[8]= a8, in[9]=a9, in[10]=a10, in[11]=a11, in[12]=a12, in[13]=a13, in[14]=a14, in[15]=a15 , load=loada , address=address[3..5], out=out1 );
    RAM8(in[0]=b0, in[1] =b1, in[2]=b2 ,in[3]=b3, in[4]=b4, in[5]=b5, in[6]=b6, in[7]=b7,in[8]= b8, in[9]=b9, in[10]=b10, in[11]=b11, in[12]=b12, in[13]=b13, in[14]=b14, in[15]=b15 , load=loadb , address=address[3..5], out=out2 );
    RAM8(in[0]=c0, in[1] =c1, in[2]=c2 ,in[3]=c3, in[4]=c4, in[5]=c5, in[6]=c6, in[7]=c7,in[8]= c8, in[9]=c9, in[10]=c10, in[11]=c11, in[12]=c12, in[13]=c13, in[14]=c14, in[15]=c15 , load=loadc , address=address[3..5], out=out3 );
    RAM8(in[0]=d0, in[1] =d1, in[2]=d2 ,in[3]=d3, in[4]=d4, in[5]=d5, in[6]=d6, in[7]=d7,in[8]= d8, in[9]=d9, in[10]=d10, in[11]=d11, in[12]=d12, in[13]=d13, in[14]=d14, in[15]=d15 , load=loadd , address=address[3..5], out=out4 );
    RAM8(in[0]=e0, in[1] =e1, in[2]=e2 ,in[3]=e3, in[4]=e4, in[5]=e5, in[6]=e6, in[7]=e7,in[8]= e8, in[9]=e9, in[10]=e10, in[11]=e11, in[12]=e12, in[13]=e13, in[14]=e14, in[15]=e15 , load=loade , address=address[3..5], out=out5 );
    RAM8(in[0]=f0, in[1] =f1, in[2]=f2 ,in[3]=f3, in[4]=f4, in[5]=f5, in[6]=f6, in[7]=f7,in[8]= f8, in[9]=f9, in[10]=f10, in[11]=f11, in[12]=f12, in[13]=f13, in[14]=f14, in[15]=f15 , load=loadf , address=address[3..5], out=out6 );
    RAM8(in[0]=g0, in[1] =g1, in[2]=g2 ,in[3]=g3, in[4]=g4, in[5]=g5, in[6]=g6, in[7]=g7,in[8]= g8, in[9]=g9, in[10]=g10, in[11]=g11, in[12]=g12, in[13]=g13, in[14]=g14, in[15]=g15 , load=loadg , address=address[3..5], out=out7 );
    RAM8(in[0]=h0, in[1] =h1, in[2]=h2 ,in[3]=h3, in[4]=h4, in[5]=h5, in[6]=h6, in[7]=h7,in[8]= h8, in[9]=h9, in[10]=h10, in[11]=h11, in[12]=h12, in[13]=h13, in[14]=h14, in[15]=h15 , load=loadh , address=address[3..5], out=out8 );

    Mux8Way16(a=out1 , b=out2 , c=out3 , d=out4 , e=out5 , f=out6 , g=out7 , h=out8 , sel=address[0..2] , out=out );

}

```

## 5. RAM512

```
CHIP RAM512 {
    IN in[16], load, address[9];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.

    DMux8Way(in=in[0] , sel=address[0..2] , a=a0 , b=b0, c=c0 , d=d0 , e=e0 , f=f0 , g=g0 , h=h0 );
    DMux8Way(in=in[1] , sel=address[0..2] , a=a1 , b=b1, c=c1 , d=d1 , e=e1 , f=f1 , g=g1 , h=h1 );
    DMux8Way(in=in[2] , sel=address[0..2] , a=a2 , b=b2, c=c2 , d=d2 , e=e2 , f=f2 , g=g2 , h=h2 );
    DMux8Way(in=in[3] , sel=address[0..2] , a=a3 , b=b3, c=c3 , d=d3 , e=e3 , f=f3 , g=g3 , h=h3 );
    DMux8Way(in=in[4] , sel=address[0..2] , a=a4 , b=b4, c=c4 , d=d4 , e=e4 , f=f4 , g=g4 , h=h4 );
    DMux8Way(in=in[5] , sel=address[0..2] , a=a5 , b=b5, c=c5 , d=d5 , e=e5 , f=f5 , g=g5 , h=h5 );
    DMux8Way(in=in[6] , sel=address[0..2] , a=a6 , b=b6, c=c6 , d=d6 , e=e6 , f=f6 , g=g6 , h=h6 );
    DMux8Way(in=in[7] , sel=address[0..2] , a=a7 , b=b7, c=c7 , d=d7 , e=e7 , f=f7 , g=g7 , h=h7 );
    DMux8Way(in=in[8] , sel=address[0..2] , a=a8 , b=b8, c=c8 , d=d8 , e=e8 , f=f8 , g=g8 , h=h8 );
    DMux8Way(in=in[9] , sel=address[0..2] , a=a9 , b=b9, c=c9 , d=d9 , e=e9 , f=f9 , g=g9 , h=h9 );
    DMux8Way(in=in[10] , sel=address[0..2] , a=a10 , b=b10, c=c10 , d=d10 , e=e10 , f=f10 , g=g10 , h=h10 );
    DMux8Way(in=in[11] , sel=address[0..2] , a=a11 , b=b11, c=c11 , d=d11 , e=e11 , f=f11 , g=g11 , h=h11 );
    DMux8Way(in=in[12] , sel=address[0..2] , a=a12 , b=b12, c=c12 , d=d12 , e=e12 , f=f12 , g=g12 , h=h12 );
    DMux8Way(in=in[13] , sel=address[0..2] , a=a13 , b=b13, c=c13 , d=d13 , e=e13 , f=f13 , g=g13 , h=h13 );
    DMux8Way(in=in[14] , sel=address[0..2] , a=a14 , b=b14, c=c14 , d=d14 , e=e14 , f=f14 , g=g14 , h=h14 );
    DMux8Way(in=in[15] , sel=address[0..2] , a=a15 , b=b15, c=c15 , d=d15 , e=e15 , f=f15 , g=g15 , h=h15 );

    DMux8Way(in=load , sel=address[0..2] , a=loada , b=loadb , c=loadc , d=loadd , e=loade , f=loadf , g=loadg , h=loadh );

    RAM64(in[0]=a0, in[1] =a1, in[2]=a2 ,in[3]=a3, in[4]=a4, in[5]=a5, in[6]=a6, in[7]=a7,in[8]= a8, in[9]=a9, in[10]=a10, in[11]=a11, in[12]=a12, in[13]=a13, in[14]=a14, in[15]=a15 , load=loada , address=address[3..8], out=out1 );
    RAM64(in[0]=b0, in[1] =b1, in[2]=b2 ,in[3]=b3, in[4]=b4, in[5]=b5, in[6]=b6, in[7]=b7,in[8]= b8, in[9]=b9, in[10]=b10, in[11]=b11, in[12]=b12, in[13]=b13, in[14]=b14, in[15]=b15 , load=loadb , address=address[3..8], out=out2 );
    RAM64(in[0]=c0, in[1] =c1, in[2]=c2 ,in[3]=c3, in[4]=c4, in[5]=c5, in[6]=c6, in[7]=c7,in[8]= c8, in[9]=c9, in[10]=c10, in[11]=c11, in[12]=c12, in[13]=c13, in[14]=c14, in[15]=c15 , load=loadc , address=address[3..8], out=out3 );
    RAM64(in[0]=d0, in[1] =d1, in[2]=d2 ,in[3]=d3, in[4]=d4, in[5]=d5, in[6]=d6, in[7]=d7,in[8]= d8, in[9]=d9, in[10]=d10, in[11]=d11, in[12]=d12, in[13]=d13, in[14]=d14, in[15]=d15 , load=loadd , address=address[3..8], out=out4 );
    RAM64(in[0]=e0, in[1] =e1, in[2]=e2 ,in[3]=e3, in[4]=e4, in[5]=e5, in[6]=e6, in[7]=e7,in[8]= e8, in[9]=e9, in[10]=e10, in[11]=e11, in[12]=e12, in[13]=e13, in[14]=e14, in[15]=e15 , load=loade , address=address[3..8], out=out5 );
    RAM64(in[0]=f0, in[1] =f1, in[2]=f2 ,in[3]=f3, in[4]=f4, in[5]=f5, in[6]=f6, in[7]=f7,in[8]= f8, in[9]=f9, in[10]=f10, in[11]=f11, in[12]=f12, in[13]=f13, in[14]=f14, in[15]=f15 , load=loadf , address=address[3..8], out=out6 );
    RAM64(in[0]=g0, in[1] =g1, in[2]=g2 ,in[3]=g3, in[4]=g4, in[5]=g5, in[6]=g6, in[7]=g7,in[8]= g8, in[9]=g9, in[10]=g10, in[11]=g11, in[12]=g12, in[13]=g13, in[14]=g14, in[15]=g15 , load=loadg , address=address[3..8], out=out7 );
    RAM64(in[0]=h0, in[1] =h1, in[2]=h2 ,in[3]=h3, in[4]=h4, in[5]=h5, in[6]=h6, in[7]=h7,in[8]= h8, in[9]=h9, in[10]=h10, in[11]=h11, in[12]=h12, in[13]=h13, in[14]=h14, in[15]=h15 , load=loadh , address=address[3..8], out=out8 );

    Mux8Way16(a=out1 , b=out2 , c=out3 , d=out4 , e=out5 , f=out6 , g=out7 , h=out8 , sel=address[0..2] , out=out );

}
```

## 6. RAM4K

```
CHIP RAM4K {
    IN in[16], load, address[12];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.

    DMux8Way(in=in[0] , sel=address[0..2] , a=a0 , b=b0, c=c0 , d=d0 , e=e0 , f=f0 , g=g0 , h=h0 );
    DMux8Way(in=in[1] , sel=address[0..2] , a=a1 , b=b1, c=c1 , d=d1 , e=e1 , f=f1 , g=g1 , h=h1 );
    DMux8Way(in=in[2] , sel=address[0..2] , a=a2 , b=b2, c=c2 , d=d2 , e=e2 , f=f2 , g=g2 , h=h2 );
    DMux8Way(in=in[3] , sel=address[0..2] , a=a3 , b=b3, c=c3 , d=d3 , e=e3 , f=f3 , g=g3 , h=h3 );
    DMux8Way(in=in[4] , sel=address[0..2] , a=a4 , b=b4, c=c4 , d=d4 , e=e4 , f=f4 , g=g4 , h=h4 );
    DMux8Way(in=in[5] , sel=address[0..2] , a=a5 , b=b5, c=c5 , d=d5 , e=e5 , f=f5 , g=g5 , h=h5 );
    DMux8Way(in=in[6] , sel=address[0..2] , a=a6 , b=b6, c=c6 , d=d6 , e=e6 , f=f6 , g=g6 , h=h6 );
    DMux8Way(in=in[7] , sel=address[0..2] , a=a7 , b=b7, c=c7 , d=d7 , e=e7 , f=f7 , g=g7 , h=h7 );
    DMux8Way(in=in[8] , sel=address[0..2] , a=a8 , b=b8, c=c8 , d=d8 , e=e8 , f=f8 , g=g8 , h=h8 );
    DMux8Way(in=in[9] , sel=address[0..2] , a=a9 , b=b9, c=c9 , d=d9 , e=e9 , f=f9 , g=g9 , h=h9 );
    DMux8Way(in=in[10] , sel=address[0..2] , a=a10 , b=b10, c=c10 , d=d10 , e=e10 , f=f10 , g=g10 , h=h10 );
    DMux8Way(in=in[11] , sel=address[0..2] , a=a11 , b=b11, c=c11 , d=d11 , e=e11 , f=f11 , g=g11 , h=h11 );
    DMux8Way(in=in[12] , sel=address[0..2] , a=a12 , b=b12, c=c12 , d=d12 , e=e12 , f=f12 , g=g12 , h=h12 );
    DMux8Way(in=in[13] , sel=address[0..2] , a=a13 , b=b13, c=c13 , d=d13 , e=e13 , f=f13 , g=g13 , h=h13 );
    DMux8Way(in=in[14] , sel=address[0..2] , a=a14 , b=b14, c=c14 , d=d14 , e=e14 , f=f14 , g=g14 , h=h14 );
    DMux8Way(in=in[15] , sel=address[0..2] , a=a15 , b=b15, c=c15 , d=d15 , e=e15 , f=f15 , g=g15 , h=h15 );

    DMux8Way(in=load , sel=address[0..2] , a=loada , b=loadb , c=loadc , d=loadd , e=loade , f=loadf , g=loadg , h=loadh );

    RAM512(in[0]=a0, in[1] =a1, in[2]=a2 ,in[3]=a3, in[4]=a4, in[5]=a5, in[6]=a6, in[7]=a7,in[8]= a8, in[9]=a9, in[10]=a10, in[11]=a11, in[12]=a12, in[13]=a13, in[14]=a14, in[15]=a15 , load=loada , address=address[3..11], out=out1 );
    RAM512(in[0]=b0, in[1] =b1, in[2]=b2 ,in[3]=b3, in[4]=b4, in[5]=b5, in[6]=b6, in[7]=b7,in[8]= b8, in[9]=b9, in[10]=b10, in[11]=b11, in[12]=b12, in[13]=b13, in[14]=b14, in[15]=b15 , load=loadb , address=address[3..11], out=out2 );
    RAM512(in[0]=c0, in[1] =c1, in[2]=c2 ,in[3]=c3, in[4]=c4, in[5]=c5, in[6]=c6, in[7]=c7,in[8]= c8, in[9]=c9, in[10]=c10, in[11]=c11, in[12]=c12, in[13]=c13, in[14]=c14, in[15]=c15 , load=loadc , address=address[3..11], out=out3 );
    RAM512(in[0]=d0, in[1] =d1, in[2]=d2 ,in[3]=d3, in[4]=d4, in[5]=d5, in[6]=d6, in[7]=d7,in[8]= d8, in[9]=d9, in[10]=d10, in[11]=d11, in[12]=d12, in[13]=d13, in[14]=d14, in[15]=d15 , load=loadd , address=address[3..11], out=out4 );
    RAM512(in[0]=e0, in[1] =e1, in[2]=e2 ,in[3]=e3, in[4]=e4, in[5]=e5, in[6]=e6, in[7]=e7,in[8]= e8, in[9]=e9, in[10]=e10, in[11]=e11, in[12]=e12, in[13]=e13, in[14]=e14, in[15]=e15 , load=loade , address=address[3..11], out=out5 );
    RAM512(in[0]=f0, in[1] =f1, in[2]=f2 ,in[3]=f3, in[4]=f4, in[5]=f5, in[6]=f6, in[7]=f7,in[8]= f8, in[9]=f9, in[10]=f10, in[11]=f11, in[12]=f12, in[13]=f13, in[14]=f14, in[15]=f15 , load=loadf , address=address[3..11], out=out6 );
    RAM512(in[0]=g0, in[1] =g1, in[2]=g2 ,in[3]=g3, in[4]=g4, in[5]=g5, in[6]=g6, in[7]=g7,in[8]= g8, in[9]=g9, in[10]=g10, in[11]=g11, in[12]=g12, in[13]=g13, in[14]=g14, in[15]=g15 , load=loadg , address=address[3..11], out=out7 );
    RAM512(in[0]=h0, in[1] =h1, in[2]=h2 ,in[3]=h3, in[4]=h4, in[5]=h5, in[6]=h6, in[7]=h7,in[8]= h8, in[9]=h9, in[10]=h10, in[11]=h11, in[12]=h12, in[13]=h13, in[14]=h14, in[15]=h15 , load=loadh , address=address[3..11], out=out8 );

    Mux8Way16(a=out1 , b=out2 , c=out3 , d=out4 , e=out5 , f=out6 , g=out7 , h=out8 , sel=address[0..2] , out=out );

}
```

## 7. RAM16K

```
CHIP RAM16K {
    IN in[16], load, address[14];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.
    DMux4Way(in=in[0] , sel=address[0..1] , a=a0 , b=b0 , c=c0 , d=d0 );
    DMux4Way(in=in[1] , sel=address[0..1] , a=a1 , b=b1 , c=c1 , d=d1 );
    DMux4Way(in=in[2] , sel=address[0..1] , a=a2 , b=b2 , c=c2 , d=d2 );
    DMux4Way(in=in[3] , sel=address[0..1] , a=a3 , b=b3 , c=c3 , d=d3 );
    DMux4Way(in=in[4] , sel=address[0..1] , a=a4 , b=b4 , c=c4 , d=d4 );
    DMux4Way(in=in[5] , sel=address[0..1] , a=a5 , b=b5 , c=c5 , d=d5 );
    DMux4Way(in=in[6] , sel=address[0..1] , a=a6 , b=b6 , c=c6 , d=d6 );
    DMux4Way(in=in[7] , sel=address[0..1] , a=a7 , b=b7 , c=c7 , d=d7 );
    DMux4Way(in=in[8] , sel=address[0..1] , a=a8 , b=b8 , c=c8 , d=d8 );
    DMux4Way(in=in[9] , sel=address[0..1] , a=a9 , b=b9 , c=c9 , d=d9 );
    DMux4Way(in=in[10] , sel=address[0..1] , a=a10 , b=b10 , c=c10 , d=d10 );
    DMux4Way(in=in[11] , sel=address[0..1] , a=a11 , b=b11 , c=c11 , d=d11 );
    DMux4Way(in=in[12] , sel=address[0..1] , a=a12 , b=b12 , c=c12 , d=d12 );
    DMux4Way(in=in[13] , sel=address[0..1] , a=a13 , b=b13 , c=c13 , d=d13 );
    DMux4Way(in=in[14] , sel=address[0..1] , a=a14 , b=b14 , c=c14 , d=d14 );
    DMux4Way(in=in[15] , sel=address[0..1] , a=a15 , b=b15 , c=c15 , d=d15 );

    DMux4Way(in=load , sel=address[0..1] , a=loada , b=loadb , c=loadc , d=loadd );

    RAM4K(in[0]=a0, in[1] =a1, in[2]=a2 ,in[3]=a3, in[4]=a4, in[5]=a5, in[6]=a6, in[7]=a7,in[8]= a8, in[9]=a9, in[10]=a10, in[11]=a11, in[12]=a12, in[13]=a13, in[14]=a14, in[15]=a15 , load=loada , address=address[2..13], out=out1 );
    RAM4K(in[0]=b0, in[1] =b1, in[2]=b2 ,in[3]=b3, in[4]=b4, in[5]=b5, in[6]=b6, in[7]=b7,in[8]= b8, in[9]=b9, in[10]=b10, in[11]=b11, in[12]=b12, in[13]=b13, in[14]=b14, in[15]=b15 , load=loadb , address=address[2..13], out=out2 );
    RAM4K(in[0]=c0, in[1] =c1, in[2]=c2 ,in[3]=c3, in[4]=c4, in[5]=c5, in[6]=c6, in[7]=c7,in[8]= c8, in[9]=c9, in[10]=c10, in[11]=c11, in[12]=c12, in[13]=c13, in[14]=c14, in[15]=c15 , load=loadc , address=address[2..13], out=out3 );
    RAM4K(in[0]=d0, in[1] =d1, in[2]=d2 ,in[3]=d3, in[4]=d4, in[5]=d5, in[6]=d6, in[7]=d7,in[8]= d8, in[9]=d9, in[10]=d10, in[11]=d11, in[12]=d12, in[13]=d13, in[14]=d14, in[15]=d15 , load=loadd , address=address[2..13], out=out4 );

    Mux4Way16(a=out1 , b=out2 , c=out3 , d=out4 ,sel=address[0..1] , out=out );

}
```

## 8. Program Counter(PC)

```
CHIP PC {
    IN in[16], reset, load, inc;
    OUT out[16];
    
    PARTS:
    //// Replace this comment with your code.
	Inc16(in=outin,out=incout);
	Mux16(a=outin,b=incout,sel=inc,out=out1);
	Mux16(a=out1,b=in,sel=load,out=out2);
	Mux16(a=out2,b=false,sel=reset,out=out3);
	Register(in=out3,load=true,out=out,out=outin);
}
```