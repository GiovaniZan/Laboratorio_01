# Laboratorio_01
 
## Exercício 1
- MOV R0, #0 
    - Foi colocado no PC 0x40
    - Coloca o valor 0 no registrador R0, sem afetar o registrador APSR
    - Gerou instrução de 32 bits (4 bytes)

- MOVS R1, #0
    - Instrução localizada no PC 0x44 (avançado 4 bytes em relação à intrução anterior)
    - Coloca o valor 0 no registrador R1, afetando o registrador APSR. O bit Z passa ao valor 1
    - Gerou instrução de 16 bits (2 bytes)

- MOV R2, #-1
    - Instrução localizada no PC 0x46 (avançado 2 bytes em relação à intrução anterior)
    - Coloca o valor 0xffffffff (correspondente a -1 na notação complemento de dois, em 32 bits) no registrador R3. Não modifica o estado do registrador APSR (permanece 1, modificado na operação anterior)
    - Gerou instrução de 32 bits (4 bytes)

- MOVS R3, #-2
    - Instrução localizada no PC 0x4a (avançado 4 bytes em relação à intrução anterior)
    - Coloca o valor0xfffffffe (correspondente a -2 na notação complemento de dois, em 32 bits) no registrador R3. Modifica o estado do registrador APSR, o Bit Z passa a 0 pois o valor envolvido não é mais nulo, e o Bit N passa a 1, pois o valor é um número negativo.
    - Gerou instrução de 32 bits (4 bytes)

> Questão: Como o compilador decide se o valor é negativo e não um positivo próximo do limiar de 32bits?


- MVN R4, #-1
    - Instrução localizada no PC 0x4e (avançado 4 bytes em relação à intrução anterior)
    - Coloca o valor negado de 0xffffffff (correspondente a 0x00000000) no registrador R4, sem afetar o registrador APSR
    - Gerou instrução de 32 bits (4 bytes)

- MVNS R5, #-2
    - Instrução localizada no PC 0x52 (avançado 4 bytes em relação à intrução anterior)
   - Coloca o valor negado de 0xfffffffe (correspondente a 0x00000001) no registrador R5. Afeta o registrador APSR que agora tem seu bit N zerado, pois o valor final de R5 é positivo
    - Gerou instrução de 16 bits (2 bytes)


- MVN R6, #0
   - Instrução localizada no PC 0x54 (avançado 2 bytes em relação à intrução anterior)
   - Coloca o valor negado de 0x00000000 (correspondente a 0xffffffff) no registrador R6. Não afeta o registrador APSR, que mantém a sua indicação de número positivo (Bit N = 0) 
    - Gerou instrução de 32 bits

- MVNS R7, #0
  - Instrução localizada no PC 0x58 (avançado 4 bytes em relação à intrução anterior)
  - Coloca o valor negado de 0x00000000 (correspondente a 0xffffffff) no registrador R7. Afeta o registrador APSR, que altera a sua indicação de número negativo (Bit N passa para 1) 
    - Gerou instrução de 32 bits

> Os mnemônicos do disassembly não são sempre coincidentes com os utilizados no assembly pois o montador resolve ambiguidades como o tamanho adequado de instrução em função dos argumentos.

--------------------------------------------------
## Exercício 2

- MOV R0, #-0x56
    - Instrução no PC 0x40
    - Coloca em R0 o complemento de 2 de 0x56 = NOT(0x56) + 1 = 0xffff ffa9 + 1 = 0xfff ffaa
    - Instrução de 32 bits (4 bytes)
- MOV R1, #0x04
    - Instrução no PC 0x44
    - Coloca 0x0000 0004 no registrador R1
    - Instrução de 32 bits (4 bytes)
- MOV R2, R0, LSL R1
    - Instrução no PC 0x48
    - Coloca  no registrador R2, o registrador R0, deslocado de 4 bits (conteúdo do registrador R1) para a esquerda, resultando em 0xffff faa0. Os 4 bits mais significativos foram perdidos no processo. 
    - Esta operação não afetou o registrador APSR
    - Instrução de 32 bits (4 bytes)
- MOV R3, R0, LSR R1
    - Instrução no PC 0x4c
    - Coloca  no registrador R3, o registrador R0, deslocado de 4 bits (conteúdo do registrador R1) para a direita, resultando em 0x0fff fffa. Os 4 bits menos significativos foram perdidos no processo. 
    - Esta operação não afetou o registrador APSR
    - Instrução de 32 bits (4 bytes)
- MOV R4, R0, ASR R1
    - Instrução no PC 0x50
    - Coloca  no registrador R4, o registrador R0, deslocado de 4 bits (conteúdo do registrador R1) para a direita, resultando em 0xffff fffa. Os 4 bits menos significativos foram perdidos no processo. Como o valor original é negativo, os bits mais significativos são preenchidos com 1´s.
    - Esta operação não afetou o registrador APSR
    - Instrução de 32 bits (4 bytes)
- MOV R5, R0, ROR R1
    - Instrução no PC 0x54
    - Coloca  no registrador R4, o registrador R0, rolando 4 bits (conteúdo do registrador R1) para a direita, resultando em 0xafff fffa.
    - Esta operação não afetou o registrador APSR
    - Instrução de 32 bits (4 bytes)

### Substituindo MOV por MOVS no exercício 2 :
Os conteúdos dos registradores R0 a R5 não se alteraram em relação ao observado com as instruções MOV, mas houve uma influência no registrador de Status e no tamanho de algumas instruçoes. Como os valor nod registradores foram idênticos, não o atualizarei na lista de observações que segue.

- MOVS R0, #-0x56
    - Instrução de 32 bits no PC 0x40
    - APSR alterou o bit N para 1 (indicando a passagem de número negativo)
- MOVS R1, #0x04
   - Instrução de 16 bits no PC 0x44
   - APSR alterou o bit N para 0 (indicando a passagem de número não-negativo)
- MOVS R2, R0, LSL R1
   - Instrução de 32 bits no PC 0x46
    - APSR alterou os bits
        - N para 1 (indicando a passagem de número negativo)
        - C para 1 (indicando que a operação "perdeu" um bit para a esquerda)
- MOVS R3, R0, LSR R1
    - Instrução de 32 bits no PC 0x4a
    - APSR alterou os bits
        - N = 0
        - C permaneceu 1 !!!
            -  indica que houve a perda de um bit 1 para a direita? - O C tanto indica um carry com o um borrow?
- MOVS R4, R0, ASR R1
    - Instrução de 32 bits no PC 0x4e
    - APSR alterado para
        - N = 1
        - C permanece 1
- MOVS R5, R0, ROR R1
    - Instrução de 32 bits no PC 0x52
    - APSR alterado para
        - N = 1 (o valor resultante ainda é negativo (msb = 1))
        - C = 1 (o último valor rotacionado de lsb para msb foi um 1)

### Substituindo MOV por MVN no exercício 2 :
 
>  Neste caso as instruções : 

    - MVN R2, R0, LSL R1
    - MVN R3, R0, LSR R1
    - MVN R4, R0, ASR R1
    - MVN R5, R0, ROR R1

> apresentam erro de sintaxe.

------------------------------
## Exercício 3
Na montagem desta sequência de instruções, todas foram implementadas em 32 bits. 

- MOV R0, #0X55
    - instrução no PC 0x40
    - Colocou a constante 0x0000 0055 em R0
- MOV R1, R0, LSL #16
    - Instrução no PC 0x44
    - Colocou em R1 o valor de R0 com um deslocamento para a esquerda de 16 bits, resultando em R1 = 0x0055 0000
    (LSL = Logical Shift Left)
- MOV R2, R1, LSR #8
    - Instrução no PC 0x48
    - Colocou em R2 o valor de R1 com um deslocamento para a direita de 8 bits, resultando em R1 = 0x0000 5500
    (LSR = Logical Shift Right)
- MOV R3, R2, ASR #4
    - Instrução no PC 0x4c
    - Coloca em R3 o valor de R2 com um deslocamento aritmnético para a direita de 4 bits, resultando em  R3 = 0x0000 0550
- MOV R4, R3, ROR #2
    - Instrução no PC 0x50
    - Coloca em R4 o valor de R3 rotacionado para a direita de 2 bits. Como o padrão 0x0550 = 0b0000 0101 0101 0000 a rotação deste padrão por dois bits resulta em 0b0000 0001 0101 0100 = 0x0154. Como os dois bits menos significativos de R3 são nulos, o resultado final de R4 é 0x0000 0154 
- MOV R5, R4, RRX
    - Instrução no PC 0x54
    - Coloca em R5 o valor de R4, rotacionado a direita com o uso do bit C (do APSR, atualmente zerado). O padrão de R3 é 0x0000 0154 = 0b0000 0000 0000 0000 0000 0001 0101 0100, que rotacionado com uso do Carry (C=0), resulta no padrão 0b0000 0000 0000 0000 0000 0000 1010 1010 = 0x0000 00aa, colocado no registrador R5

Nenhuma das instruções alterou o conteúdo do registrador APSR.


### Substituindo MOV por MVN no exercício 3 :
- MVN R0, #0X55
    - Instrução no PC 0x40
    - Coloca #0x55 negado no registrador R0. !(0b0000 0000 0000 0000 0000 0000 0101 0101) = 0b1111 1111 1111 1111 1111 1111 1010 1010 = R0 = 0xffff ffaa 
- MVN R1, R0, LSL #16
    - Instrução no PC 0x44
    - Coloca em R1 o valor negado de R0 deslocado para a esquerda de 16 bits. R1 = !(0xffaa 0000) = 0x0055 ffff 
- MVN R2, R1, LSR #8
   - Instrução no PC 0x48
   - Coloca em R2 o valor negado do registrador R1 deslocado para direita de forma lógica em 8 bits. R2 = !(0x0000 55ff)  = 0xffff aa00 
- MVN R3, R2, ASR #4
   - Instrução no PC 0x4c
   - Coloca em R3 o valor negado do registrador R2 deslocado para direita de forma aritmética em 4 bits. R2 = !(0xffff faa0) = 0x0000 055f  
- MVN R4, R3, ROR #2
    - Instrução no PC 0x50
    - Coloca em R4 o valor negado de R3 rodado para a direita em 2 bits.
        - R3        =    0b0000 0000 0000 0000 0000 0101 0101 1111
        - R3 ROR #2 =    0b1100 0000 0000 0000 0000 0001 0101 0111
        - !(R3 ROR #2) = 0b0011 1111 1111 1111 1111 1110 1010 1000
        - R4 = 0x3fff fea8
- MVN R5, R4, RRX
    - Instrução no PC 0x54
    - Coloca em R5 o valor negado do registrador R4 Rodado para a Direita com uso do C. RRX = Rotate Right eXtended
        - R4       = 0b0011 1111 1111 1111 1111 1110 1010 1000 , C = 0 -> valor atual no APSR
        - R4 RRX   = 0b0001 1111 1111 1111 1111 1111 0101 0100
        - !(R4 RRX)= 0b1110 0000 0000 0000 0000 0000 1010 1011
        - R5 = 0xe000 00ab



## Exercício 4

- MOV R0, #0x5678
    - Coloca o valor  #0x5678 no registrador  R0
- MOVT R0, #0x1234
     - Coloca o valor  #0x1234 nos 16 bits superiores do registrador R0
- MOVT R1, #0x1234
    - Coloca o valor  #0x1234 nos 16 bits superiores do registrador R1
- MOV R1, #0x5678
    - Coloca o valor  #0x5678 no registrador  R1, apagando o conteúdo dos 16 bits superiores do registrador R1!
> Existe direfença. A ordem é fundamental para a movimentação de valores de mais de 16 bits. O valor dos bits menos significativos devem ser atribuídos antes dos bits mais significativos.



## Exercício 5
Forma mais eficiente de atribuição.
- R0 = 0
    - MOVS R0, #0x00
- R1 = 200
    - MOVS R1, #200
- R2 = 0x1234
    - MOV R2, #0x1234
- R3 = 0xffff ff00
    - MVN R3, #0xff
- R4 = 0xabcd ef00
    - MOV R4 #0xef00
    - MOVT R4, #0xabcd


