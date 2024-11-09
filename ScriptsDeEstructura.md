Este minijuego se enfoca en una plataforma, donde se encuentra el jugador batallando a enemigos, evitando la lluvia y tratando de no disparar las paredes. Si una bala le da a una pared, se cae o elimina uno de los 16 pisos que posee la arena. Por otro lado, si la bala choca con una esquina de la plataforma, se desparece todo el piso y el jugador muere. En esta sección se muestra el código trabajado para que se remuevan diferentes secciones del piso cuando las balas le dan a las paredes.

# Floor Manager
Para poder manipular el suelo, se crearon dos scripts: el FloorManager y Floor. Este último, se colocó en cada uno de los pisos de la estructura y posee dos funciones, Start y OnDestroy. En Start, se añaden los game objects de clase Floor a una lista en FloorManager, mientras que en OnDestroy se remueven de ella cuando son destruidos.

<p align="center">
  <img src="https://github.com/user-attachments/assets/4f794490-8874-47dc-a667-03ee497ec331" height="700" width="800" />
  <img src="https://github.com/user-attachments/assets/88043e5a-e6cc-4461-a92b-6dc0647a0df7" height="700" width="800" />
</p>
  
  Por otra parte, el FloorManager se añadió a un objeto vacío. En este script se inicializó una lista llamada floors, la cual se compone de los objetos de clase Floor. Además, se definió una variable de tipo FloorManager llamada instance y un UnityEvent. La variable instance se utiliza en la función Awake para verificar que solamente exista una sola instancia del FloorManager. Esto se conoce como un Singleton, un componente que solamente debe estar inicializado una vez. Por otra parte, se definió la función AddFloor y RemoveFloor para, respectivamente, añadir y quitar game objects de tipo Floor en la lista floors.

# Eliminando diferentes locetas
Se creó un script vacío llamado TriggerWall y éste se colocó como componente en todas las paredes que conforman la estructura. El propósito de esto es que las paredes sean instancias de la clase TriggerWall y que se pueda detectar cuando una bala colisone solamente con paredes.

<p align="center">
  <img src="https://github.com/user-attachments/assets/2bdd4abd-6153-4bdb-8208-06da173d8333" height="600" width="600" />
</p>

Para trabajar con la colisión, se desarrolló un script llamado BulletWallHit en el prefab de la bala. Dentro de este, se creó una función llamada OnTriggerEnter para que se pueda detectar la colisión entre una bala y la pared. Dentro de la función se definió una variable de tipo TriggerWall, la cual guarda el game object, la pared, que fue impactada. Además, se obtuvo el tamaño de la lista floors en el FloorManager para saber cúantos pisos quedan por eliminar.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a375426d-a0bb-4633-8bfd-fe5dd682c6ac" height="700" width="800" />
</p>

Lo que hace este código es que verifica si wall existe o, en otras palabras, si la bala chocó con alguna pared. Si el objeto de tipo TriggerWall existe y todavía hay suelos para remover, entonces se genera un número entero al azar, desde el cero hasta el largo de la lista, para obtener un game object de tipo Floor de la lista floors de manera aleatorea. Luego de obtener un suelo random, este se destruye en la plataforma y se elimina de la lista. 

# Eliminando todo el suelo
Para que se cumpla este caso, la bala tuvo que haber chocado con una de las cuatro esquinas de la arena. Se creó un script vacío llamado TriggerCorner y se colocó en cada una de las esquinas para que ellas sean game objects de la clase TriggerCorner. Al igual que con las paredes, se trabajó con la colisión en el script de BulletWallHit de la bala. En la misma función de OnTriggerEnter, se definió un variable de tipo TriggerCorner, la cual guarda el game object o esquina que se impactó. Si corner existe, si la bala tuvo contacto con una esquina, se entra a un bloque de código donde se itera por la lista de game objects de clase Floor y se eliminan todos los pisos. Esto resulta en que todo el suelo de la arena desaparezca.  

<p align="center">
  <img src="https://github.com/user-attachments/assets/7616ace9-5cfd-4b91-bfa9-d2a169191db4" height="600" width="600" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/a0ae115c-7b5a-4a29-92dd-223fb8ab6b9b" height="400" width="800" />
</p>

# Videos probando floor y corner scripts
![GIFMaker_me(2)](https://github.com/user-attachments/assets/c4212287-09a7-461c-9a33-a8dbd4d526cb)

![GIFMaker_me(3)](https://github.com/user-attachments/assets/bef74e9d-d752-4fe1-8239-2c7fcfcf0552)

[Volver al Readme](README.md)
