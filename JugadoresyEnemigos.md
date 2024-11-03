# Modelos

Comenzamos importando un prefab para el jugador y el enemigo. 

A cada prefab se le asignó un material único para diferenciarlos visualmente. 

# Jugador
Se agregaron varios scripts al jugador para manejar sus acciones:
PlayerMovement: Controla el movimiento del jugador en el espacio de juego.
PlayerShooter: Gestiona la mecánica de disparo del jugador.
Life: Controla la vida del jugador.
Player Input Component y Actions: Utilizamos el componente Player Input y configuramos las acciones para capturar las entradas del usuario, como movimiento y disparo.

Se creó un "shootpoint" en el jugador, que sirve como punto de origen para las balas cuando se disparan. 
Esto permite un control preciso de la dirección de disparo y la posición desde la cual se generan las balas.

Importamos un prefab para la bala, el cual representa el proyectil que dispara el jugador. 

Este prefab contiene un script llamado ContactDestroyer, que elimina la bala al entrar en contacto con algún objeto, simulando el impacto.

Configuración del Jugador

Scripts de Funcionalidad: Se agregaron varios scripts al jugador para manejar sus acciones:
PlayerMovement: Controla el movimiento del jugador en el espacio de juego.
PlayerShooter: Gestiona la mecánica de disparo del jugador.
Life: Controla la vida del jugador, registrando y aplicando daño recibido.
Player Input Component y Actions: Utilizamos el componente Player Input y configuramos las acciones necesarias para capturar las entradas del usuario, como movimiento y disparo.

Punto de Disparo (ShootPoint): Se creó un "shootpoint" en el jugador, que sirve como punto de origen para las balas cuando se disparan. Esto permite un control preciso de la dirección de disparo y la posición desde la cual se generan las balas.

Prefab de Bala: Importamos un prefab para la bala, el cual representa el proyectil que dispara el jugador. Este prefab contiene un script llamado ContactDestroyer, que elimina la bala al entrar en contacto con algún objeto, simulando el impacto.

# Enemigo

Se agregaron varios scripts a los enemigos para manejar su comportamiento:
Enemy: Controla las acciones y patrones de movimiento de los enemigos.
Life: Asigna una cantidad de vida a los enemigos.

Se crearon cuatro spawners ubicados en las esquinas del mapa, que sirven como puntos de aparición para los enemigos. 
Estos spawners traen la generación constante de enemigos en diferentes lugares.

Se desarrolló un script que controla la aparición de enemigos en el escenario. 
Se encarga de generar enemigos en los puntos designados en intervalos definidos.

Se creó un script de EnemyManager que agrega cada enemigo a una lista cuando aparece y lo elimina cuando es destruido. 

# Game mode

Se asignó a cada enemigo un script de ScoreOnDeath que otorga puntos al jugador cuando el enemigo es destruido.

Este script maneja y actualiza la puntuación total del jugador en el juego, reflejando los puntos ganados al eliminar enemigos.

Se creó un script llamado GameModeManager que cambia la escena del juego a una de victoria o derrota según el resultado. 
Este script monitorea el estado del juego y define el fin de la partida en función del éxito o fracaso del jugador.
