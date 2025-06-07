# ExamenElectr-nica


## Descripción del proyecto
El pensamiento se enreda, se tensiona, se relaja. 

El pensamiento continúa, en bucle. 

El pensamiento es un diálogo
     entre motores. 

##
La obra se compone de dos motores paso a paso, dos arduinos y una madeja de lana negra. Los motores están anclados a la muralla, cuyo soporte es una lámina de madera. Entre estos dos motores hay 60 cm de distancia donde la lana cuelga a merced del comportamiento de los motores. 

~~~ // MOTOR PASO A PASO

// Pines del motor
int out1 = 2;
int out2 = 3;
int out3 = 4;
int out4 = 5;

// Variables para azar
int velocidadGiro = 20; // velocidad de paso (ms)

unsigned long tiempoInicioDireccion = 0; // marca cuando empezó la dirección actual
unsigned long duracionDireccion = 0; // duración que mantendremos la dirección

int direccion = 1;

void setup() {
  pinMode(out1, OUTPUT);
  pinMode(out2, OUTPUT);
  pinMode(out3, OUTPUT);
  pinMode(out4, OUTPUT);

  Serial.begin(9600);

  // Inicializamos duración dirección y tiempo inicio
  duracionDireccion = random(15000, 30000); // entre 15 y 30 segundos por dirección
  tiempoInicioDireccion = millis();
}

void loop() {
  unsigned long tiempoActual = millis();

  // Cambiar dirección solo si ha pasado el tiempo mínimo para mantenerla
  if (tiempoActual - tiempoInicioDireccion >= duracionDireccion) {
    // Cambiar dirección aleatoriamente (menos probable que cambie)
    if (random(0, 100) < 30) { // 30% de probabilidad de cambiar dirección
      direccion = -direccion;
      Serial.println("Cambio de direccion!");
    }
    // Reiniciamos contadores
    duracionDireccion = random(15000, 30000); // nueva duración entre 15-30 seg
    tiempoInicioDireccion = tiempoActual;
  }

  // Definimos velocidadGiro para cada loop (puede ser un poco variable)
  velocidadGiro = random(10, 60);

  // Determinar cantidad de pasos a dar en este ciclo corto
  int pasosPorCiclo = 10; // controlamos la cantidad de pasos por loop para hacer movimiento fluido

  for (int i = 0; i < pasosPorCiclo; i++) {
    // Movimiento errático aleatorio con 10% de probabilidad:
    if (random(0, 100) < 10) {
      // Movimiento errático: pasos reversa rápidos
      pasoErratico();
      delay(velocidadGiro / 3);
    } else {
      // Movimiento normal según dirección
      if (direccion == 1) {
        paso1(); delay(velocidadGiro);
        paso2(); delay(velocidadGiro);
        paso3(); delay(velocidadGiro);
        paso4(); delay(velocidadGiro);
      } else {
        paso4(); delay(velocidadGiro);
        paso3(); delay(velocidadGiro);
        paso2(); delay(velocidadGiro);
        paso1(); delay(velocidadGiro);
      }
    }
  }
  
  // Pausa pequeña antes del siguiente ciclo para evitar bloqueos y permitir cambios de dirección
  delay(50);
}

// Función para movimiento errático: pasos cortos rápidos hacia atrás y adelante
void pasoErratico() {
  // Un pequeño movimiento rápido adelante y atrás para simular erraticidad
  paso1(); delay(5);
  paso2(); delay(5);
  paso3(); delay(5);
  paso4(); delay(5);
  paso4(); delay(5);
  paso3(); delay(5);
  paso2(); delay(5);
  paso1(); delay(5);
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

