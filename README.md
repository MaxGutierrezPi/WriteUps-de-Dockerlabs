# Write up de la maquina "Extraviado"

Maquina gratuita proporcionada por Dockerlabs<br>
Dificultad: Muy Facil

Descargamos la maquina del sitio oficial de Dockerlabs<br>
https://dockerlabs.es/

Descomprimimos el contenedor donde se aloja

```
unzip extraviado.zip
```

Cargamos el contenedor para poder interactuar con la maquina.

```
bash auto_deploy.sh extraviado.tar
```
Despliegue correcto del contenedor que contiene la maquina
<br><br>
![image_Alt](https://github.com/NETD3VIL/Write-up_Extraviado/blob/851bd738bbac8a4065e61fe9d817ec185aaf0f48/1.png)
<br><br>
Realizamos un escaneo con nmap y guardamos el resultado en un archivo de texto<br>
```
nmap -p- -sC -sV -sS --open -n -Pn -vvv 172.17.0.3 > scan.txt
```
Leemos el archivo generado por nmap utilizando cat
```
cat scan.txt
```
En el analisis encontramos dos puertos, el puerto 80 que normalmente esta relacionado con el protocolo HTTP donde podemos encontrar un servidor web Apache y el puerto 22 que esta relacionado con SSH donde encontramos OpenSSH
<br><br>
![image_Alt](https://github.com/MaxGutierrezPi/WriteUps-de-Dockerlabs/blob/1236114a536f9d7788bcb15e0442765b2dad95a3/2.png)
<br><br>
Nos dirigimos al navegador y escribimos la direccion IP de la maquina desplegada, nos vamos al codigo del sitio web y hasta la parte de abajo podemos encontrar dos cadenas de texto cifradas con el metodo Base64 y podemos saberlo porque terminan con un signo de "igual".<br><vr>
```
ZGFuaWVsYQ== : Zm9jYXJvamE=
```
<br>
Deciframos las dos cadenas utilizando este comando en la consola<br><br>

```echo "ZGFuaWVsYQ==" | base64 -d```
<br><br>
```echo "Zm9jYXJvamE=" | base64 -d```
<br><br>
Una vez decifrado nos entregara estas credenciales<br><br>

```daniela | focaroja```<br><br>
Usamos las credenciales obtenidas para conectarnos por SSH a la dirección ip a traves del puerto 22<br><br>
![image_Alt](https://github.com/MaxGutierrezPi/WriteUps-de-Dockerlabs/blob/8a80438daec1a83e074d50093690eab48c8c61fd/3.png)<br><br>
Una vez dentro comenzamos con la busqueda de información, nos encontramos una carpeta oculta llamada .secreto y leemos el archivo  passdiego.txt con el comando cat y encontramos una cadena de texto cifrada tambien en base64, deciframos la cadena y nos arroja el texto "ballenanegra" por lo que vamos a usarla como contraseña para entrar al usuario Diego<br><br>
![image_Alt](https://github.com/MaxGutierrezPi/WriteUps-de-Dockerlabs/blob/96a8b385caace4ca1fcf69b9b7dea9ca592656a6/4.png)<br><br>



