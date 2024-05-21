---
date: 2024-05-19 03:41:00
layout: post
title: HACK Assembler
subtitle: HACK Assembly to Machine Language Translator
description: A CLI application written in Dart that translates the HACK assembly
  language into binary machine code.
image: /assets/img/uploads/hack-assembler.png
category: portfolio
tags:
  - dart
  - cli
author: Dan
paginate: false
---
## T﻿ech Used

* D﻿art

## P﻿roject Details

F﻿ind the code on [GitHub](https://github.com/DanArcherOnline/hack_assembly_assembler).

S﻿upply a file named sum.asm with the contents below to the application.

```hack
// Computes sum=1+...+100.
@i // i=1
M=1
@sum // sum=0
M=0
(LOOP)
@i // if (i-100)=0 goto END
D=M
@100
D=D-A
@END
D;JGT
@i // sum+=i
D=M
@sum
M=D+M
@i // i++
M=M+1
@LOOP // goto LOOP
0;JMP
(END) // infinite loop
@END
0;JMP
```

T﻿he application will produce a file with the corresponding machine code.

```binary
0000000000010000
1110111111001000
0000000000010001
1110101010001000
0000000000010000
1111110000010000
0000000001100100
1110010011010000
0000000000010010
1110001100000001
0000000000010000
1111110000010000
0000000000010001
1111000010001000
0000000000010000
1111110111001000
0000000000000100
1110101010000111
```

L﻿earn more about this project at [Nand2Tetris](https://www.nand2tetris.org/project06).