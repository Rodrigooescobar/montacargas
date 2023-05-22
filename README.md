# Primer parcial de SPD
![imagen de arduino y tinkercad](tinkercad-arduino.png "arduino en tinkercad")
<!-- UL-->
## Alumno:
---
* Rodrigo Omar Escobar

## Proyecto Montacargas de 9 pisos
---
![imagen del proyecyo](proyecto.png "proyecto hecho en tinkercad")
![diagrama del proyecyo](diagrama.png "diagrama hecho en tinkercad")
## Descripcion
---
Proyecto de montacargas de 9 pisos con 3 botones, uno para subir de piso, uno para bajar y otro para denerlo, se puede parar cuando el usuario lo desee, ya sea en movimiento o en estado de reposo, contiene 2 led indicadores, uno verde que enciende cuando el montacargas esta en marcha y otro led rojo que indica cuando esta detenido
## Funciones principales
---
Funciones para subir de piso, para bajar y otro detener, estas funciones usan un contador el movimiento, que indican el numero del piso del montacargas, a traves de un  switch se da las instrucciones al display de 7 segmentos que numero debe mostrar.
<!-- Bloque de codigos -->
```c++
void subir_piso()//Funcion para subir de piso
{
  nro_piso++;//Sube un piso
  
  for (int tiempo_actual = 0; tiempo_actual < 3000; tiempo_actual += 10)//Recorre por 3000ms
  {
    encender_led(LED_MARCHA, HIGH, LED_PARADA, LOW);//Enciende led marcha y apaga el de parada
    if (digitalRead (PULSADOR_PARADA) == 0 && digitalRead (PULSADOR_PARADA) != pulsador_anterior)// Boton de para durante la marcha
    {
      detener_montacargas();//Funcion para dentener la marcha que esta en proceso 
    }
      else if (digitalRead (PULSADOR_PARADA) == 1)
  	{
    	pulsador_anterior = 1;
  	}
    Serial.println("SUBIENDO");//Dentro del for
  }//Fuera del for
  encender_led(LED_PARADA, HIGH, LED_MARCHA, LOW);//Completa el piso y enciede el led que esta en parada
}
  
void bajar_piso()//Funcion para bajar de piso
{
  nro_piso--; //Le resta 1 al contador de piso
  
  for (int tiempo_actual = 0; tiempo_actual < 3000; tiempo_actual += 10)
  {
    encender_led(LED_MARCHA, HIGH, LED_PARADA, LOW);//Enciende led marcha y apaga el de parada
    if (digitalRead (PULSADOR_PARADA) == 0 && digitalRead (PULSADOR_PARADA) != pulsador_anterior)// Boton de para durante la marcha
    {
      detener_montacargas();//Funcion para dentener la marcha que esta en proceso 
    }
      else if (digitalRead (PULSADOR_PARADA) == 1)
  	{
    	pulsador_anterior = 1;
  	}
    Serial.println("BAJANDO");
  }//fuera del for
  encender_led(LED_PARADA, HIGH, LED_MARCHA, LOW);//Enciende el led de parada al completar la marcha
}

void detener_montacargas()//Funcion para dentener el montacargas
{
  while (digitalRead (PULSADOR_PARADA) == 0)// Entra al primer while hasta que el boton vuelva a su estado de reposo
  {
    Serial.println("PARADA");
  }
    while (digitalRead (PULSADOR_PARADA) == 1) // Sale de la funcion al precionar el boton
  {
    Serial.println("PARADA");
    encender_led(LED_PARADA, HIGH, LED_MARCHA, LOW);
  }
  pulsador_anterior = digitalRead (PULSADOR_PARADA);
}
```
Funcion del display donde es comandado a traves del swtich como se explico antes.

```c++
void mostrar_numero_por_display ()// Funcion que muestra el nro del piso por el display
{  
  digitalWrite (A, LOW);
  digitalWrite (B, LOW);
  digitalWrite (C, LOW);
  digitalWrite (D, LOW);
  digitalWrite (E, LOW);
  digitalWrite (F, LOW);
  digitalWrite (G, LOW);
  
  switch (nro_piso)
    {
    case 0:
      	digitalWrite (A, HIGH);
        digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (D, HIGH);
        digitalWrite (E, HIGH);
        digitalWrite (F, HIGH);
        break;
    case 1:
        digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
        break;
    case 2:
        digitalWrite (A, HIGH);
        digitalWrite (B, HIGH);
        digitalWrite (D, HIGH);
        digitalWrite (E, HIGH);
        digitalWrite (G, HIGH);
        break;
    case 3:
        digitalWrite (A, HIGH);
        digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (D, HIGH);
        digitalWrite (G, HIGH);
    	break;
    case 4:
    	digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (F, HIGH);
        digitalWrite (G, HIGH);
        break;
    case 5:
        digitalWrite (A, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (D, HIGH);
        digitalWrite (F, HIGH);
        digitalWrite (G, HIGH);
    	break;
    case 6:
        digitalWrite (A, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (D, HIGH);
    	digitalWrite (E, HIGH);
        digitalWrite (F, HIGH);
        digitalWrite (G, HIGH);
    	break;
    case 7:
        digitalWrite (A, HIGH);
        digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
    	break;
    case 8:
        digitalWrite (A, HIGH);
    	digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (D, HIGH);
    	digitalWrite (E, HIGH);
        digitalWrite (F, HIGH);
        digitalWrite (G, HIGH);
    	break;
    case 9:
        digitalWrite (A, HIGH);
        digitalWrite (B, HIGH);
        digitalWrite (C, HIGH);
        digitalWrite (F, HIGH);
        digitalWrite (G, HIGH);
    	break;
    }
}

```
## Link del proyecto
---
* [Proyecto](https://www.tinkercad.com/things/bNp2QRHDYhh?sharecode=J8ogw9SX7kTXkO-vtW1mXZV4U9Q0fco6h8rYiuCzcc0)
## Link del video funcionando
* [Video](https://youtu.be/UXNEi_hCEUc)


