# Projeto: Semáforo com Programação Orientada a Objetos (POO)
## Drive das Fotos: [# Sema-oro-inteligente](https://drive.google.com/drive/u/1/folders/1Nmn5LsAPqJI6xFHJ_UC1l1caeklS3qKI)
##  Objetivo da atividade

Desenvolver um sistema de semáforo funcional utilizando três LEDs (verde, amarelo e vermelho) controlados por um Arduino Uno, aplicando conceitos de Programação Orientada a Objetos (POO) em C++.
O objetivo principal é compreender o uso de classes, objetos e ponteiros, além de controlar a sequência de acendimento dos LEDs de forma automatizada.

##  Materiais utilizados

1 × Arduino Uno

1 × LED vermelho (porta digital 8)

1 × LED amarelo (porta digital 7)

1 × LED verde (porta digital 6)

3 × Resistores de 220 Ω (um para cada LED)

9 × Jumpers macho-macho

6 x Jumpers macho-femea

1 × Protoboard

1 × Cabo USB para alimentação e programação

##  Descrição resumida do funcionamento

O código utiliza classes para representar cada LED e o conjunto de LEDs como um semáforo.
Através de ponteiros e máquina de estados, o programa alterna automaticamente entre os estados verde → amarelo → vermelho, com tempos configuráveis, sem travar o Arduino com delay().

## Dificuldades encontradas

Tive dificuldade para conectar corretamente os jumpers, garantindo que cada fio estivesse na linha certa da protoboard.

Também tive dificuldade para posicionar os resistores no lugar correto e escolher a resistência ideal (valor de voltagem adequado para não queimar os LEDs).
