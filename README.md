# Projeto: Semáforo com Programação Orientada a Objetos (POO)
## Drive: [# Sema-oro-inteligente](https://drive.google.com/drive/u/1/folders/1Nmn5LsAPqJI6xFHJ_UC1l1caeklS3qKI)

##  Objetivo da atividade

![IMG_8374](https://github.com/user-attachments/assets/c963579e-e91c-4eef-a4d3-2676dcac668d)


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

## Código com POO e Ponteios

```cpp

#include <Arduino.h>

/* ===== Classe led ===== */
class led {
  private:
    uint8_t pin;
  public:
    led(uint8_t p) : pin(p) {}
    void begin() { pinMode(pin, OUTPUT); off(); }
    void on()    { digitalWrite(pin, HIGH); }
    void off()   { digitalWrite(pin, LOW);  }
    void set(bool value) { digitalWrite(pin, value ? HIGH : LOW); }
};

/* ===== Classe trafficLight ===== */
class trafficLight {
  private:
    led* green;
    led* yellow;
    led* red;

    enum state { greenOn, yellowOn, redOn };
    state currentState;

    unsigned long greenTimeMs;
    unsigned long yellowTimeMs;
    unsigned long redTimeMs;

    unsigned long lastChangeMs;

    void switchTo(state next) {
      green->off();
      yellow->off();
      red->off();

      if (next == greenOn)  green->on();
      if (next == yellowOn) yellow->on();
      if (next == redOn)    red->on();

      currentState = next;
      lastChangeMs = millis();
    }

  public:
    trafficLight(led* g, led* y, led* r,
                 unsigned long greenTime=3000,
                 unsigned long yellowTime=800,
                 unsigned long redTime=3000)
      : green(g), yellow(y), red(r),
        greenTimeMs(greenTime), yellowTimeMs(yellowTime), redTimeMs(redTime),
        currentState(redOn), lastChangeMs(0) {}

    void begin() {
      green->begin();
      yellow->begin();
      red->begin();
      switchTo(greenOn);
    }

    void update() {
      unsigned long now = millis();
      switch (currentState) {
        case greenOn:
          if (now - lastChangeMs >= greenTimeMs) switchTo(yellowOn);
          break;
        case yellowOn:
          if (now - lastChangeMs >= yellowTimeMs) switchTo(redOn);
          break;
        case redOn:
          if (now - lastChangeMs >= redTimeMs) switchTo(greenOn);
          break;
      }
    }

    void setTimings(unsigned long g, unsigned long y, unsigned long r) {
      greenTimeMs = g;
      yellowTimeMs = y;
      redTimeMs = r;
    }
};

/* ===== Instâncias ===== */
led greenLed(6);
led yellowLed(7);
led redLed(8);

trafficLight* semaforo; // ponteiro para o semáforo

void setup() {
  // aloca o objeto dinamicamente
  semaforo = new trafficLight(&greenLed, &yellowLed, &redLed, 3000, 800, 3000);
  semaforo->begin();
}

void loop() {
  semaforo->update();
}

```

