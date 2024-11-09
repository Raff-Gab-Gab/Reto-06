# Modelos

Comenzamos importando un prefab para el jugador y el enemigo. 

![Screenshot 2024-11-07 180329](https://github.com/user-attachments/assets/98d59a23-2f87-4667-8542-8ef99f722979)

A cada prefab se le asignó un material único para diferenciarlos visualmente. 

![Screenshot 2024-11-07 180525](https://github.com/user-attachments/assets/20070fea-226a-4a38-917e-4d4304685792)
![Screenshot 2024-11-07 180537](https://github.com/user-attachments/assets/e35a2ccc-41bb-4704-9e58-d6a1e45e4ff8)

# Jugador
Se agregaron varios scripts y componentes al jugador para manejar sus acciones:

![image](https://github.com/user-attachments/assets/60b23fd7-256b-4d4f-a0e3-a861c850ff75)
![Screenshot 2024-11-07 180823](https://github.com/user-attachments/assets/19d18f13-bc8e-4132-8735-c874848304d1)

PlayerMovement: Controla el movimiento del jugador en el espacio de juego. Gestiona la mecánica de disparo del jugador.
![Captura de pantalla 2024-11-08 204654](https://github.com/user-attachments/assets/51fa1a5c-341a-4489-a2f3-01c9e0266816)
![Captura de pantalla 2024-11-08 204848](https://github.com/user-attachments/assets/3132cd71-4a0f-43c9-8485-1d3098b90731)

Life: Controla la vida del jugador.
![Captura de pantalla 2024-11-08 205435](https://github.com/user-attachments/assets/3aa60074-9af1-4fde-b8dc-d8d54f54f461)

Player Input Component y Actions: Utilizamos el componente Player Input y configuramos las acciones para capturar las entradas del usuario, como movimiento y disparo.

![Screenshot 2024-11-07 181540](https://github.com/user-attachments/assets/1ac4be0c-730e-4b50-bedf-aa79475f14cc)

![Screenshot 2024-11-07 181549](https://github.com/user-attachments/assets/5dbae123-301f-4acc-89cf-2b0d35cefa1e)

![Screenshot 2024-11-07 181557](https://github.com/user-attachments/assets/d299e817-1a58-4ee1-bc2f-da68711f89ba)

Se creó un "shootpoint" en el jugador, que sirve como punto de origen para las balas cuando se disparan. 

![Screenshot 2024-11-07 181832](https://github.com/user-attachments/assets/edb81631-d84a-48a1-b6ad-382502a70fbf)

Importamos un prefab para la bala, el cual representa el proyectil que dispara el jugador. 

![Screenshot 2024-11-07 181914](https://github.com/user-attachments/assets/465369ad-8247-4737-99de-8565033677e8)

Este prefab contiene un script llamado ContactDamage, que elimina la bala al entrar en contacto con algún objeto y le quite vida al objeto, simulando el impacto.
![image](https://github.com/user-attachments/assets/a7ff73ea-f6d9-46a2-8ae7-4af32ba83254)

![GIFMaker_me(1)](https://github.com/user-attachments/assets/a630b77a-d111-4513-88cc-9cdccf8295d6)

# Enemigo

Se agregaron varios scripts a los enemigos para manejar su comportamiento:

![Screenshot 2024-11-07 182301](https://github.com/user-attachments/assets/ddbe64e9-0660-49b9-a81e-455e350ee2a1)

Enemy: Añade y elimina las instancias de enemigos en la lista del EnemiesManager mientras se crean y se van destruyendo, respectivamente.
![image](https://github.com/user-attachments/assets/eaa80dd3-72f9-4f34-8201-1484f5058cdf)

Enemy forward: Mueve el enemigo hacia adelante.
![Captura de pantalla 2024-11-08 213417](https://github.com/user-attachments/assets/a836e825-73ad-4a50-b977-ec8348652773)

Life: Asigna una cantidad de vida a los enemigos.

![image](https://github.com/user-attachments/assets/3a37757f-979c-447c-98ce-6fb1f218460f)

Se crearon cuatro spawners ubicados en las esquinas del mapa, que sirven como puntos de aparición para los enemigos. 
Estos spawners traen la generación constante de enemigos en diferentes lugares.

![Screenshot 2024-11-02 192629](https://github.com/user-attachments/assets/11d34e06-002a-4336-850a-aa83b22d2b41)

![Screenshot 2024-11-02 192637](https://github.com/user-attachments/assets/8ac57832-ccb1-4a11-97bb-b50fd38ff221)

![Screenshot 2024-11-02 192643](https://github.com/user-attachments/assets/690c9a4d-25f3-4a9d-85d0-7e9b8f2b232b)

![Screenshot 2024-11-02 192649](https://github.com/user-attachments/assets/f158c6ef-959b-4a1e-a7a1-39a093e7fdf6)

Se desarrolló un script spawner que controla la aparición de enemigos en el escenario. 
Se encarga de generar enemigos en los puntos designados en intervalos definidos.

![image](https://github.com/user-attachments/assets/73fd7e3e-8a5d-482f-aac1-e7884548cca5)

Se creo un script de WaveManager para agregar todos los waves de enemigos a una lista.

![image](https://github.com/user-attachments/assets/374ef4a1-3911-4c17-8f5c-6f2fe12ef1a9)

Se creó un script de EnemyManager que agrega cada enemigo a una lista cuando aparece y lo elimina cuando es destruido. 

![image](https://github.com/user-attachments/assets/0fe86ed2-cf88-4203-a440-ee00a7fd405a)

![GIFMaker_me](https://github.com/user-attachments/assets/047b4fb1-51dc-4652-b2ae-7c6ea479fe59)



# Game mode

Se asignó a cada enemigo un script de ScoreOnDeath que otorga puntos al jugador cuando el enemigo es destruido.

![image](https://github.com/user-attachments/assets/6b9a87b9-d019-4157-a7d0-d7c42490ff9d)

Este script maneja y actualiza la puntuación total del jugador en el juego, reflejando los puntos ganados al eliminar enemigos.

![image](https://github.com/user-attachments/assets/52153a1c-190b-4a25-ba1e-6b3c89ca0dcc)

Se creó un script llamado GameModeManager que cambia la escena del juego a una de victoria o derrota según el resultado. 
Este script monitorea el estado del juego y define el fin de la partida en función del éxito o fracaso del jugador.


# Win y Lose screen

Lose
![image](https://github.com/user-attachments/assets/c443f5f4-aa61-47ef-b1d0-a76014e932f0)

Win
![image](https://github.com/user-attachments/assets/6001f6a1-d808-4e35-9114-fdf5bbc7479d)






[Volver al Readme](README.md)
