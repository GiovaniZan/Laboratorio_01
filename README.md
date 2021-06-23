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

> Os mnemônicos do disassemblynão são sempre coincidentes com os utilizados no assembly pois o montador resolve ambiguidades como o tamanho adequado de instrução em função dos argumentos.


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
    - Coloca  no registrador R4, o registrador R0, deslocado de 4 bits (conteúdo do registrador R1) para a direita, resultando em 0x0fff fffa. Os 4 bits menos significativos foram perdidos no processo. 
    - Esta operação não afetou o registrador APSR
    - Instrução de 32 bits (4 bytes)
- MOV R5, R0, ROR R1
    - Instrução no PC 0x54
    - Coloca  no registrador R4, o registrador R0, rolando 4 bits (conteúdo do registrador R1) para a direita, resultando em 0xafff fffa.
    - Esta operação não afetou o registrador APSR
    - Instrução de 32 bits (4 bytes)

### Substituindo MOV por MOVS no exercício:
Os conteúdos dos registradores não se alteraram, mas houve uma influência  

- MOVS R0, #-0x56
- MOVS R1, #0x04
- MOVS R2, R0, LSL R1
- MOVS R3, R0, LSR R1
- MOVS R4, R0, ASR R1
- MOVS R5, R0, ROR R1
