# Lluvia

## Base

primer paso fue crear la gota de lluvia del tamaño de una bola de playa

![01](https://github.com/user-attachments/assets/8d312a15-1d70-4ca2-8849-fc09aaca2eb5)

Después se le añadió el componente Rigidbody para que cayera

![02](https://github.com/user-attachments/assets/b016c187-ff47-4368-8c50-d393b464f009)

Se creó un layer nuevo para que pudiera interactuar correctamente con los alrededores

![03](https://github.com/user-attachments/assets/aee3e22a-3e49-4829-a955-ca60d6321949)

## Apariencia

Se creó un material nuevo para la gota de agua, la cual se llamó `RainColor` y se añadió a la gota.

![04](https://github.com/user-attachments/assets/1f3a8776-28d6-4b60-84be-377a5cf4141a)

![05](https://github.com/user-attachments/assets/c834ff17-2d2b-40a9-a320-9650cd4b1782)

![06](https://github.com/user-attachments/assets/ec546b37-a6cf-47ab-8d65-c8653bfbcd6d)

## Funcionalidad

### Spawnear

Se creó un objeto vacío llamado RainSpawner para que manejara la generación de las gotas de agua.
Al objeto se le añadió un script para que creara las gotas de agua.

#### RainSpawner.cs versión 1

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class RainSpawner : MonoBehaviour
{
    public GameObject prefab;
    public float startTime;
    public float endTime;
    public float spawnRate;
    // Start is called before the first frame update
    void Start()
    {
        InvokeRepeating("Spawn", startTime, spawnRate);
        Invoke("EndSpawner", endTime);
    }

    void Spawn()
    {
        Instantiate(prefab, transform.position, transform.rotation);
    }

    void EndSpawner()
    {
        CancelInvoke();
    }
}

```

### Posiciones aleatorias

El siguiente código crea una cierta cantidad de objetos en el mismo lugar donde está el spawner. Pero para que sea lluvia hace falta que salgan muchas gotas de agua de muchas partes, así que para eso se introdujo unas variablas y comportamiento aleatorio


#### RainSpawner.cs versión 2

```
public class RainSpawner : MonoBehaviour
{

    ...

    public float rangeX;
    public float rangeZ;

    ...

        void Spawn()
    {
        Vector3 newPos = new Vector3(Random.Range(-rangeX + transform.position.x, rangeX + transform.position.x),
                                 transform.position.y,
                                 Random.Range(-rangeZ + transform.position.z, rangeZ + transform.position.z));
        Instantiate(prefab, newPos, transform.rotation);
    }

    ...

```

Las variables `rangeX` y `rangeY` determinan cuán lejos de el centro puede estar la gota de agua.
Cuando llega el momento de crear una gota nueva se genera una posición nueva con la función `Random.Range` para el componente `x` y `z` de la gota nueva.

Para visualizar mejor el campo de las gotas de agua se añadió un gizmo que lo muestra.

```
    void OnDrawGizmos() {
        Gizmos.color = Color.green;
        Gizmos.DrawWireCube(transform.position, new Vector3(2*rangeX, 0, 2*rangeZ));
    }
```

![10](https://github.com/user-attachments/assets/b43f2cd9-337a-4022-833f-9432b96e6d84)

![11](https://github.com/user-attachments/assets/3b2e1387-39ad-457a-94e3-e87dae9cc9d4)

imagen ortográfica del campo de lluvia, que se puede observar que ocupa el terreno entero.

## Campos de lluvia

Ya que un campo solo crea una gota a la vez se añadieron más campos.

![12](https://github.com/user-attachments/assets/765758fc-0f42-472e-8f2b-8e1f07ae4158)

## Gotas temporeras

Para limpiar el espacio y evitar que se llene de gotas se creó un script DestroySelf para las gotas

#### DestroySelf.cs

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DestroySelf : MonoBehaviour
{
    public float timeToDie;

    // Update is called once per frame
    void OnCollisionEnter(Collision collision)
    {
        Invoke("EndSelf", timeToDie);
    }

    void EndSelf()
    {
        Destroy(gameObject);
    }
}
```

# Vista final

https://github.com/user-attachments/assets/9c342b23-9fba-4615-b2dd-5947ac663b2e

#### RainSpawner.cs

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class RainSpawner : MonoBehaviour
{
    public GameObject prefab;
    public float startTime;
    public float endTime;
    public float spawnRate;

    public float rangeX;
    public float rangeZ;
    // Start is called before the first frame update
    void Start()
    {
        InvokeRepeating("Spawn", startTime, spawnRate);
        Invoke("EndSpawner", endTime);
    }

    void Spawn()
    {
        Vector3 newPos = new Vector3(Random.Range(-rangeX + transform.position.x, rangeX + transform.position.x),
                                 transform.position.y,
                                 Random.Range(-rangeZ + transform.position.z, rangeZ + transform.position.z));
        Instantiate(prefab, newPos, transform.rotation);
    }

    void EndSpawner()
    {
        CancelInvoke();
    }


    void OnDrawGizmos() {
        Gizmos.color = Color.green;
        Gizmos.DrawWireCube(transform.position, new Vector3(2*rangeX, 0, 2*rangeZ));
    }
}
```

#### DestroySelf.cs

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DestroySelf : MonoBehaviour
{
    public float timeToDie;

    // Update is called once per frame
    void OnCollisionEnter(Collision collision)
    {
        Invoke("EndSelf", timeToDie);
    }

    void EndSelf()
    {
        Destroy(gameObject);
    }
}
```
