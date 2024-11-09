# Win y Los Screens

## Dibujo

### Lose Screen

Por primera cosa se boceteó la configuración del la imagen, dónde iban todos los elementos

![DeathScreenInProcessMin01](https://github.com/user-attachments/assets/01f23f01-7e84-42f5-95cc-aac1358622ba)

![DeathScreenInProcessMin02](https://github.com/user-attachments/assets/f993f5a0-a709-424d-8b37-d2a7829e8e1b)

![DeathScreenInProcessMin03](https://github.com/user-attachments/assets/59ccd7d9-d1f3-459d-9517-af8bb04ed621)

De allí se sacó un boceto final

![DeathScreenInProcessMin04](https://github.com/user-attachments/assets/72c49e48-0051-4023-92bd-280869781448)

Del boceto final se sacó las formas simples de los enemigos, utilizando solo los colores normales

![DeathScreenInProcessMin05](https://github.com/user-attachments/assets/1c359fa6-2fab-4dc7-b0d5-d1b90e6e8532)

Luego se limpió un poco más

![DeathScreenInProcessMin06](https://github.com/user-attachments/assets/b33c886e-7f71-48d3-b20c-87c1afb81e28)

De allí se le cambió los colores para que reflejara los colores en el jeugo

![DeathScreenInProcessMin07](https://github.com/user-attachments/assets/760e1dfd-5444-4b48-b55b-e0972926a058)

De allí entonces se creó el fondo

![DeathScreenInProcessMin08](https://github.com/user-attachments/assets/640ec3cc-053a-49d9-8354-d417a9e5f6b4)

Luego se añadió la lluvia

![DeathScreenInProcessMin09](https://github.com/user-attachments/assets/25558a9f-41a4-49af-8188-4df2191ca327)

Par aque quedara mejor se alteró el color de las gotas para que vieran más verdes

![DeathScreenInProcessMin10](https://github.com/user-attachments/assets/0d661308-a9b9-4339-bc13-8df553945523)

### Win Screen

Se siguió un procedimiento similar

Se empezó con el boceto del personaje y luego se creó el dibujo con las formas simples

![WinScreenInProgressMin01](https://github.com/user-attachments/assets/df3e2779-cdbd-4d57-945b-48a6ac91b5d2)

![WinScreenInProgressMin02](https://github.com/user-attachments/assets/19db92eb-03f1-4c82-8e19-5b9b831a2a6b)

![WinScreenInProgressMin03](https://github.com/user-attachments/assets/9e2f5836-5032-4492-97ba-a936636164da)

Se colocó el fondo desde ahora para poder ayudar a colorear el resto del personaje

![WinScreenInProgressMin04](https://github.com/user-attachments/assets/c92ea3fd-d2e7-4ddc-b7e7-0bdabf4ae9cc)

![WinScreenInProgressMin05](https://github.com/user-attachments/assets/932df1cd-4453-4544-a073-ee4e5c550189)

Entonces se dubujaron als gotas de agua y se les ajustó el color y la opacidad, para que pareciera la bruma después de que llueve fuerte

![WinScreenInProgressMin06](https://github.com/user-attachments/assets/92e26555-9707-4a49-bbb2-b654ab5cacb8)

![WinScreenInProgressMin07](https://github.com/user-attachments/assets/40e7b241-0440-42c4-946e-88085254cd84)

![WinScreenInProgressMin08](https://github.com/user-attachments/assets/13be9b12-4fed-4dd4-b4bd-cc388e1029b7)

Las imágenes finales

![DeathScreen](https://github.com/user-attachments/assets/cc941b9c-9dd3-4881-b629-6bcfa85731a7)

![WinScreen](https://github.com/user-attachments/assets/5a214675-d86f-4a40-99a3-f87e43a67be7)

## Juego

Hace falta asegurarse que el jugador puede perder dentro del juego. Así como está el jugador puede ganar (simplemente mata a todos los enemigos) pero no tiene manera de perder.

### Perder

Se crea un cubo llamado Lava, el cual se coloca debajo del terreno. Servirá para matar al jugador cuando caiga de la plataforma.

![01](https://github.com/user-attachments/assets/4faeec65-6e12-47f0-af96-86ad20af6c71)

![015](https://github.com/user-attachments/assets/df6fd2e6-8c6b-45bb-8a29-1d0bedfc9425)

Se creó un material llamado `LavaMaterial` y se aplicó al cubo.

![02](https://github.com/user-attachments/assets/79777e97-eb8c-4063-acdd-01ed7df90819)

material

![03](https://github.com/user-attachments/assets/9a005a5a-7d2c-453e-a992-34ee90fc8094)

valores del material

![04](https://github.com/user-attachments/assets/b4dd1589-d04f-479b-82c5-0cd657de57f0)

lava con el material

Se aseguró que la lava fuera un `Trigger`, similar a las balas, y que tuviera un script para que hiciera daño al jugador.

![05](https://github.com/user-attachments/assets/08bf9231-8e2f-4c6e-8ed0-527499254442)

Box collider con trigger checkbox puesto

![06](https://github.com/user-attachments/assets/af076c47-6009-49b3-9e1f-e12fc873ea42)

contact damage script con 9999999 daño

## Game Mode

Se creó un objeto vacío llamado `GameMode` para guardar la lógica del juego, en particular para las transiciones de escenas.

![07](https://github.com/user-attachments/assets/b57de811-1d60-4417-8262-f3f59e095b65)


Se le añadió un script a GameMode que verifica dos cosas:

-   si el jugador murió, por cual cambia la escena a `LoseScreen`

-   si no hay enemigos ni oleadas de enemigos, por cual cambia la escena a `WinScreen`

#### GameMode.cs

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.InputSystem;
using UnityEngine.SceneManagement;

public class GameMode : MonoBehaviour
{
    [SerializeField] Life playerlife;   //  player

    void Start()
    {
        playerlife.onDeath.AddListener(PlayerDied);

        Enemiesmanager.instance.onChanged.AddListener(CheckWinCondition);
        WaveManager.instance.onChanged.AddListener(CheckWinCondition);
    }

    void PlayerDied()
    {
        SceneManager.LoadScene("LoseScreen");
    }

    void CheckWinCondition()
    {
        if (Enemiesmanager.instance.enemies.Count <= 0
            && WaveManager.instance.waves.Count <= 0)
        {
            SceneManager.LoadScene("WinScreen");
        }
    }
}
```

Una vez se le añadió el script al objeto GameMode se le configuró con el componente `Life` del jugador

![09](https://github.com/user-attachments/assets/28ff508c-ac9c-493b-ade3-e976c902c01f)

Script de GameMode

## Win Screen

Se creó un escena nueva llamada WinScreen

En la escena nueva se creó un objeto tipo Imagen (UI).

![10](https://github.com/user-attachments/assets/fdfba593-adfb-4d8f-9d80-76d352276c76)

Mientrastanto, al recurso WinScreen.png se le cambiarion las propiedades para que fuera un *Sprite (2D and UI)*

![11](https://github.com/user-attachments/assets/8f49f02c-17d3-44c2-80ea-0de832489dcb)

propiedades de Winscreen.png

Entonces a la imagen se le añadió el sprite WinScreen.png y se alteró los valores del ancho y alto para que pudieran caber en la pantalla apropiadamente.

![12](https://github.com/user-attachments/assets/1207b9bf-dd78-468e-91fe-f0532f0c7f32)

width y height

![13](https://github.com/user-attachments/assets/6440aac2-f58b-4aed-82ea-e80e9a2cbf46)

imagen final de cómo queda en la escena

Se repitió el mismo procedimiento para el `LoseScreen`

![14](https://github.com/user-attachments/assets/b40b2717-8fbc-4e85-a841-55214a742ded)

imagen LoseScreen final

Las escenas finales dentro del juego son `Terrain`, `LoseScreen`, y `WinScreen`.

![15](https://github.com/user-attachments/assets/75a2e85a-beea-49e5-bad0-4c34fd897d31)

todas las escenas en el juego final

## Implementación final

Lo último que faltó fua cambiar los *Build Settings* para que reconociera todas las escenas necesarias dentro del juego y los scripts pudieran funcionar

![16](https://github.com/user-attachments/assets/6c832807-a076-4322-9beb-474e8dfb9667)

screenshot de Build Settings. Todas las escenas están presentas, más una extra que no quité
