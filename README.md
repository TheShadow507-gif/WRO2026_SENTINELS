# Nuestra experiencia en WRO Future Engineers 2026

Este documento habla sobre nuestra experiencia en la competencia de **World Robot Olympiad (WRO) 2026**, en la categoría *Future Engineers*. Somos un equipo conformado por **David Garibaldy**, **Makenzie** y **Cesar**, y aquí contamos todo el trabajo que realizamos durante varias semanas para poder llegar a estos días de competencia: cómo lo hicimos, qué hicimos, y las pruebas que fuimos haciendo en el camino.

## Quiénes somos

Somos un equipo de tres integrantes que decidimos meternos de lleno al reto de construir, programar y afinar un vehículo autónomo capaz de recorrer la pista de Future Engineers sin intervención humana: mantenerse dentro del carril, tomar las esquinas correctamente, contar las vueltas, detenerse en la meta, y esquivar los obstáculos (pilares) que aparecen en el camino.

## El proceso de trabajo

Durante varias semanas nos dividimos el trabajo entre la parte mecánica/electrónica y la parte de programación, e íbamos probando y ajustando ambas en paralelo conforme el vehículo tomaba forma.

### Primeras pruebas: hacer que el robot se mueva y "vea"

Lo primero que resolvimos fue la parte más básica: que el vehículo pudiera avanzar en línea recta usando el motor DC controlado por un driver (con los pines ENA/IN3/IN4) y un servomotor para la dirección de las llantas delanteras. En paralelo, integramos dos sensores ultrasónicos, uno apuntando en diagonal hacia la derecha y otro hacia la izquierda, para que el robot pudiera "sentir" qué tan cerca estaban las paredes de la pista a cada lado.

### Lógica de manejo en el pasillo y detección de esquinas

Con los sensores funcionando, programamos la lógica central del recorrido: si un lado detecta que la pared se abre (una lectura de distancia mayor a un umbral configurado), el robot interpreta que ahí está la esquina y gira el servo hacia ese lado; si ambos lados están despejados, gira hacia el que esté más abierto; si ninguno se abre, sigue recto.

Después de varias pruebas notamos un problema: en algunos tramos, el sensor del lado contrario detectaba una apertura falsa y el robot dudaba o giraba hacia el lado equivocado. Para resolverlo, agregamos una mejora importante: el robot **define el sentido de la pista (horario o antihorario) una sola vez**, apenas detecta la primera apertura clara, y a partir de ahí solo le hace caso al sensor de ese lado durante el resto de la carrera. Esto hizo que el manejo fuera mucho más consistente.

### Conteo de vueltas

Para saber cuándo detenerse, agregamos un contador que registra cada vez que el robot entra en un giro (no en cada ciclo, sino solo al inicio de cada giro nuevo). Configuramos cuántos giros equivalen a una vuelta completa de la pista y cuántas vueltas se necesitan para terminar la carrera; al llegar a esa meta, el robot se detiene automáticamente.

### Esquive de obstáculos (pilares)

Uno de los retos más grandes fue el manejo de los pilares de colores de la pista, que en la competencia oficial indican hacia qué lado debe pasar el vehículo (rojo a la derecha, verde a la izquierda). Como no contamos con una cámara ni con un sensor de color dedicado, adaptamos nuestra solución: usamos los mismos dos sensores ultrasónicos para detectar cuándo un pilar está muy cerca en el camino (una lectura mucho más cercana de lo normal), y en ese caso el robot ejecuta una maniobra de esquive en dos fases —primero se desvía hacia un lado para rodear el pilar, luego corrige hacia el lado contrario para enderezarse— alternando el lado de esquive cada vez que aparece un nuevo pilar, para evitar quedarse pegado siempre del mismo lado.

## Pruebas y calibración

Gran parte de las semanas de trabajo se fueron en pruebas sobre la pista real, ajustando valores como:

- La velocidad del motor en tramos rectos y en curvas.
- Los ángulos del servo para giro recto, izquierda y derecha.
- El umbral de distancia que define cuándo "se abrió" un lado (esquina).
- El umbral de distancia que define cuándo hay un pilar muy cerca (obstáculo).
- Los tiempos de cada fase del esquive de pilares.

Cada uno de estos valores lo fuimos afinando a partir de la observación directa del comportamiento del vehículo en la pista, corrigiendo poco a poco los casos en los que se salía del carril, giraba antes o después de tiempo, o no completaba bien el esquive de un pilar.

## Reflexión final

Este proyecto nos permitió aprender no solo sobre programación y electrónica, sino también sobre el proceso real de ingeniería: probar, fallar, medir, ajustar, y volver a probar. Cada mejora que hicimos —desde fijar el sentido de la pista hasta el esquive alternado de pilares— surgió de un problema concreto que detectamos en pruebas reales, y eso fue, para nosotros, la parte más valiosa de toda la experiencia.
