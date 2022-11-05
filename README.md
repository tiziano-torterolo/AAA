
# --------------

La idea es que utilicen estos codigos como API / biblioteca.

La idea es ayudar a los que recien estan empezando a trabajar en python

Si a alguien le interesa ( https://readme.so/es/editor ) 





## Primeros Pasos (Conectar Arduino)

Para establecer comunicacion con el arduino utilicen la siguiente clase


```python
from Comunicadores.ComunicacionArduino import ComunicacionArduino

comunicador = ComunicacionArduino()

#comunicador = ComunicacionArduino("Serial")
#comunicador = ComunicacionArduino("Blue")
#comunicador = ComunicacionArduino("Wifi")
```

Si quieres establecer comunciacion Serial:

```python
comunicador = ComunicacionArduino("Serial")

comunicador = ComunicacionArduino("Serial",baudRate = 9600)

comunicador = ComunicacionArduino("Serial",SerialPort="COM6")
```
Si quieres establecer comunciacion Bluetooth:

```python
comunicador = ComunicacionArduino("Blue")
#actualmente no disponible :(
```

De forma predeterminda se inicia en comunicacion Wifi

```python
ComunicacionArduino() = ComunicacionArduino("Wifi")

comunicador = ComunicacionArduino("Wifi", wifiaddr = "localhost")

comunicador = ComunicacionArduino("Wifi", wifiport=8050)

comunicador = ComunicacionArduino("Wifi", wifiaddr = "localhost" , wifiport=8050)
```

## Enviar y Recibir Arduino

Si ya tiene conectado el arduino puede Enviar y Recibir texto con los siguientes 
metodos

```python
comunicador.SendToArduino("ping")

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
controladorsilla = ControladorSillaRobotica(comunicador)
```

El controlador cuenta con los siguientes metodos
```python
controladorsilla.Forward() 

controladorsilla.BackWard()

controladorsilla.Rigth()

controladorsilla.Left()

controladorsilla.RotateLeft()

controladorsilla.RotateRigth()

```
Si quiere hacer que rote una cantidad arbitraria de grados tiene:
```python
controladorsilla.RotateFreeleft(angle)

controladorsilla.RotateFreeRigth(angle)
```

## Controlador Brazo
La creacion del controlador es igual que la anterior
```python
from Controladores.ControladorBrazoRobotico import ControladorBrazoRobotico
```

```python
controladorsilla = ControladorBrazoRobotico(comunicador)
```

Recordemos que los brazos roboticos cuentan con distintos ejes, el brazo
del laboratorio de logistica cuenta con 6 ejes.

Para guardar la posicion utilicen un marcador de posicion:
```python
from Controladores.PositionMarker import PositionMarker

position1 = PositionMarker([0,180,360,0,180,90])
#imaginen que es una posicion real :3

PositionMarker() = PositionMarker([0,0,0,0,0,0])
#No escribir nada es lo mismo que escribir [0,0,0,0,0,0]
```
Para mover el brazo a una posición ya guardada utilicen:

```python
controladorbrazo.MoveTo(position1)

controladorbrazo.MoveToRestPosition()
#Envia el brazo a posicion de descanso

position3 = controladorbrazo.GetPosition()
#Obtiene la posicion actual del brazo
#No funciona 
```
## Terminando IMPORTANTE!!
es muy importante que una vez finalizado el codigo Cierren el comunicador
```python
#end
comunicador.Terminar()
```