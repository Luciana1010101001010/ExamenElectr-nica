# ExamenElectronica

El pensamiento se enrreda, se tensiona, se relaja. 

El pensamiento continúa, en bucle. 

El pensamiento es un diálogo
     entre motores. 

## Descripción del proyecto

Dos motores en movimiento circular, están conectados por medio de una lana que, debido a la rotación de los motores, se tensiona o distensiona. 
[![montaje](https://i.postimg.cc/ydRByyS2/1000057439.jpg)](https://postimg.cc/bDqKzbgR)

##
La obra se compone de dos motores paso a paso, dos arduinos y una madeja de lana negra. El soporte de cada mòdulo està compuesto por una lámina de madera, anclada a la muralla, el cual tiene un soporte de cortina hecho del mismo material, donde la lana se enrolla y cuelga a merced del comportamiento de los motores. Recomiendo que los elementos utilizados para construir dichos módulos, sean con materiales y objetos encontrados.


[![1000057427.jpg](https://i.postimg.cc/kX1ZDt2S/1000057427.jpg)](https://postimg.cc/KRTQHjrc)

## Diagramas 
[![Diagrama-Tinkercad.png](https://i.postimg.cc/1Rnt2gd1/Diagrama-Tinkercad.png)](https://postimg.cc/F1vNJKmT)
[![Diagrama.png](https://i.postimg.cc/QdkZvss3/Diagrama.png)](https://postimg.cc/K1zWg6Rq)




~~~ // MOTOR PASO A PASO

// Pines del motor
int out1 = 2;
int out2 = 3;
int out3 = 4;
int out4 = 5;

// Velocidad de giro (ms por paso)
int velocidadGiro = 5;  // entre más bajo, más rápido gira el motor
int velMax = 5;
int velMin = 20;


int randomDireccion = 0; //Para que varíe el movimiento 

int contador  = 0;
int limiteContador = 500;

void setup() {
  // Configuramos los pines del motor como salidas
  pinMode(out1, OUTPUT);
  pinMode(out2, OUTPUT);
  pinMode(out3, OUTPUT);
  pinMode(out4, OUTPUT);

  randomSeed(analogRead(0));

  Serial.begin(9600);
}

void loop() {
  contador = contador + 1;
  // Gira el motor en una dirección de forma continua
  if (randomDireccion == 0) {
    paso1();
    delay(velocidadGiro);

    paso2();
    delay(velocidadGiro);

    paso3();
    delay(velocidadGiro);

    paso4();
    delay(velocidadGiro);
  }

  if (randomDireccion == 1) {
    paso4();
    delay(velocidadGiro);

    paso3();
    delay(velocidadGiro);

    paso2();
    delay(velocidadGiro);

    paso1();
    delay(velocidadGiro);
  }

  

  if (contador > limiteContador)
  {
    velocidadGiro = random (velMax, velMin);

    contador = 0;

    randomDireccion = random(0,2);

  }

 Serial.print(velocidadGiro);
  Serial.print(" - ");
  Serial.print(contador);
  Serial.print(" - ");
  Serial.print(randomDireccion);
  Serial.println();

}

// FUNCIONES PARA CADA PASO

void paso1() {
  digitalWrite(out1, HIGH);
  digitalWrite(out2, LOW);
  digitalWrite(out3, LOW);
  digitalWrite(out4, LOW);
}

void paso2() {
  digitalWrite(out1, LOW);
  digitalWrite(out2, HIGH);
  digitalWrite(out3, LOW);
  digitalWrite(out4, LOW);
}

void paso3() {
  digitalWrite(out1, LOW);
  digitalWrite(out2, LOW);
  digitalWrite(out3, HIGH);
  digitalWrite(out4, LOW);
}

void paso4() {
  digitalWrite(out1, LOW);
  digitalWrite(out2, LOW);
  digitalWrite(out3, LOW);
  digitalWrite(out4, HIGH);
} ~~~

