
# --------------

La idea es que utilicen estos codigos como API / biblioteca.

La idea es ayudar a los que recien estan empezando a trabajar en python

Si a alguien le interesa ( https://readme.so/es/editor ) 





## Primeros Pasos (Conectar Arduino)

Para establecer comunicacion con el arduino utilicen la siguiente clase


```python
from Comunicadores.ComunicacionArduino import ComunicacionArduino

com = ComunicacionArduino()

#com = ComunicacionArduino("Serial")
#com = ComunicacionArduino("Blue")
#com = ComunicacionArduino("Wifi")
```

Si quieres establecer comunciacion Serial:

```python
com = ComunicacionArduino("Serial")

com = ComunicacionArduino("Serial",baudRate = 9600)

com = ComunicacionArduino("Serial",SerialPort="COM6")
```
Si quieres establecer comunicacion Bluetooth:

```python
com = ComunicacionArduino("Blue")
#actualmente no disponible :(
```

De forma predeterminda se inicia en comunicacion Wifi

```python
ComunicacionArduino() = ComunicacionArduino("Wifi")

com = ComunicacionArduino("Wifi", wifiaddr = "localhost")

com = ComunicacionArduino("Wifi", wifiport=8050)

com = ComunicacionArduino("Wifi", wifiaddr = "localhost" , wifiport=8050)
```

## Enviar y Recibir Arduino

Si ya tiene conectado el arduino puede Enviar y Recibir texto con los siguientes 
metodos

```python
com.SendToArduino("ping")

msg = comunicador.GetFromArduino()
```

## Controlador Silla

En el caso de la silla:

```python
from Controladores.ControladorSillaRobotica import ControladorSillaRobotica

```
Debe crear el controlador y pasarle como parametro el comunicador
creado anteriormente
```python
silla = ControladorSillaRobotica(comunicador)
```

El controlador cuenta con los siguientes metodos
```python
silla.Forward() 

silla.BackWard()

silla.Rigth()

silla.Left()

silla.RotateLeft()

silla.RotateRigth()

```
Si quiere hacer que rote una cantidad arbitraria de grados tiene:
```python
silla.RotateFreeleft(angle)

silla.RotateFreeRigth(angle)
```

## Controlador Brazo
La creacion del controlador es igual que la anterior
```python
from Controladores.ControladorBrazoRobotico import ControladorBrazoRobotico
```

```python
brazo = ControladorBrazoRobotico(comunicador)
```

Recordemos que los brazos roboticos cuentan con distintos ejes, el brazo
del laboratorio de logistica cuenta con 6 ejes.

Para guardar la posicion utilicen un marcador de posicion:
```python
from Controladores.PositionMarker import PositionMarker

p1 = PositionMarker([0,180,360,0,180,90])
#imaginen que es una posicion real :3

PositionMarker() = PositionMarker([0,0,0,0,0,0])
#No escribir nada es lo mismo que escribir [0,0,0,0,0,0]
```
Para mover el brazo a una posición ya guardada utilicen:

```python
brazo.MoveTo(position1)

brazo.MoveToRestPosition()
#Envia el brazo a posicion de descanso

p3 = brazo.GetPosition()
#Obtiene la posicion actual del brazo
#No funciona 
```
## IMPORTANTE!!
es muy importante que una vez finalizado el codigo Cierren el comunicador
```python
#end
com.Terminar()
```