# apresenta-o-git--parte-2

//Leitura de distância com o sensor HC-SR04
#include <Ultrasonic.h>
#include <Servo.h>
#define SERVO 6 // Porta Digital 6 PWM

 Ultrasonic ultrassom(8,9); // define o nome do sensor(ultrassom)
//e onde esta ligado o trig(8) e o echo(7) respectivamente

Servo s; // Variável Servo
boolean mexeu = false;
int tempopraencher = 5000;
int tempodeespera = 120000;
 
long distancia;
// Esta função "setup" roda uma vez quando a placa e ligada ou resetada
 void setup() {
 Serial.begin(9600); //Habilita Comunicação Serial a uma taxa de 9600 bauds.
 s.attach(SERVO);
 s.write(90); // Inicia motor posição zero
 }
 
// Função que se repete infinitamente quando a placa é ligada
 void loop()
 {
   distancia = ultrassom.Ranging(CM);// ultrassom.Ranging(CM) retorna a distancia em
                                     // centímetros(CM) ou polegadas(INC)
   Serial.print(distancia); //imprime o valor da variável distancia
   Serial.println("cm");
   delay(100);
   if(distancia<=10 && mexeu == false){
      mexeu = true;
      s.write(85);
      delay(1000);
      s.write(90);
      delay(tempopraencher);
      s.write(95);
      delay(1000);
      s.write(90);
      }
   delay(tempodeespera);
   mexeu = false;
 }
