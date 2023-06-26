# Segundo Parcial SPD

Documentación del desarrollo del segundo desafío evaluativo propuesto.

![LOGO TINKERCAD](https://github.com/iagovalverde/EjemploDocumentacion/blob/main/img/ArduinoTinkercad.jpg)

## Identidad.

Nombre: Lucas Gabriél Sigüenza<br/>
División: E<br/>

## ProyectO
### Imágen del circuito.<br/>
[![Circuito](https://i.im.ge/2023/06/26/0SnDyX.Circuito.th.png)](https://im.ge/i/0SnDyX)<br/>
### Imágen del esquema<br/>
[![Diagrama](https://i.im.ge/2023/06/26/0SnpGF.Diagrama.th.png)](https://im.ge/i/0SnpGF)<br/>
### Lista de componenetes.<br/>
[![Lista de componentes](https://i.im.ge/2023/06/26/0Sn6sp.Lista-de-componentes.th.png)](https://im.ge/i/0Sn6sp)<br/>

## Descripción.
Es un circuito cuya función principal es la lectura de temperatura y su impresión en un display LCD 16x2..<br/>
Se le anexa un servo, dos leds, un sensor de temperatura, control IR y un sistema de alarma de incendios con el fin de
presentar la estación y estado de incendio por el display.<br/>
## LINK AL PROYECTO
*[proyecto](https://www.tinkercad.com/things/hUusEf535Am-ingenious-bigery/editel?sharecode=u3A-DT86myqqBlq-uWGohQLHp7GHVnDPtIuS4bnAfEo)

## Funciones
```C++ 
float obtener_temperatura(int pin)
{
  int lectura = analogRead(pin);
  float temp = (lectura * 5.0 / 1023.0 - 0.5) * 100.0;
  return temp;
}

void escribir_estacion_lcd(String mensaje)
{
  if (estacion != estacion_actual.toInt())
  {
    limpiar_pantalla_lcd();
  }
  lcd.setCursor(0, 0);
  lcd.print("Estacion:");
  lcd.setCursor(0, 1);
  lcd.print(mensaje);
  estado_incendio = 0;
}
void limpiar_pantalla_lcd()
{
  lcd.setCursor(0, 0);
  lcd.print("                        ");
  lcd.setCursor(0, 1);
  lcd.print("                        ");
}

void titilar_led(int led)
{
  digitalWrite(led, 1);
  delay(500);
  digitalWrite(led, 0);
  delay(100);
}

void evaluar_control()
{
   if (controlIR.decode())
    {
      if (controlIR.decodedIRData.decodedRawData
          == tecla_encender && bandera_encendido == 0)
      {
        bandera_encendido = 1;
        Serial.println("Encendido");
        IrReceiver.resume();  
      }
      else if (controlIR.decodedIRData.decodedRawData
               == tecla_encender && bandera_encendido == 1)
      {
        bandera_encendido = 0;
        Serial.println("Apagado");
        IrReceiver.resume();  
      }
   }
}
```
