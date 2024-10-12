# PatronSingleton

# Índice

1. [¿Qué es el patrón Singleton?](#1-¿qué-es-el-patrón-singleton)
2. [Ventajas del patrón Singleton](#2-ventajas-del-patrón-singleton)
3. [Ejemplo del Patrón Singleton: Control de Instancia Única](#3-ejemplo-del-patrón-singleton-control-de-instancia-única)
   - [Código en Java](#código-en-java)
   - [Resultado en consola](#resultado-en-consola)
4. [Explicación](#explicación)
5. [Conclusión](#conclusión)

---

# Patrón Singleton

## 1. ¿Qué es el patrón Singleton?

El patrón **Singleton** es un patrón de diseño creacional que restringe la creación de objetos de una clase a una única instancia. Esto significa que solo puede existir una instancia de la clase, y proporciona un punto de acceso global para dicha instancia. Se utiliza en situaciones donde se necesita tener exactamente una instancia de un objeto, como cuando se gestiona una conexión a la base de datos o un registro de configuración en una aplicación.

El propósito principal del patrón Singleton es controlar la creación de objetos para evitar que se creen múltiples instancias de una misma clase, asegurando que todos los consumidores utilicen la misma instancia.

## 2. Ventajas del patrón Singleton

- **Control de instancias**: Garantiza que solo exista una instancia de una clase, lo que puede ser útil para gestionar recursos compartidos, como bases de datos o archivos de configuración.
- **Acceso global**: Proporciona un punto de acceso global a la única instancia, lo que facilita su uso en diferentes partes de una aplicación.
- **Eficiencia**: Evita la sobrecarga de crear múltiples instancias y controla el ciclo de vida de la instancia.
  
## 3. Ejemplo del Patrón Singleton: Control de Instancia Única

En este ejemplo, creamos una clase `ConexionBaseDatos` para representar una conexión a la base de datos que debe ser única en todo el sistema.

### Código en Java

```java
// Clase Singleton: Gestiona la conexión a la base de datos
class ConexionBaseDatos {
    // Variable estática que contiene la única instancia de la clase
    private static ConexionBaseDatos instanciaUnica;

    // Constructor privado para evitar instanciación desde fuera de la clase
    private ConexionBaseDatos() {
        System.out.println("Conexión establecida.");
    }

    // Método estático para obtener la única instancia de la clase
    public static ConexionBaseDatos obtenerInstancia() {
        if (instanciaUnica == null) {
            instanciaUnica = new ConexionBaseDatos();
        }
        return instanciaUnica;
    }

    // Método simulado para realizar operaciones en la base de datos
    public void ejecutarConsulta(String consulta) {
        System.out.println("Ejecutando consulta: " + consulta);
    }
}

// Clase principal para probar el Singleton
public class Main {
    public static void main(String[] args) {
        // Intentamos obtener varias veces la instancia del Singleton
        ConexionBaseDatos conexion1 = ConexionBaseDatos.obtenerInstancia();
        ConexionBaseDatos conexion2 = ConexionBaseDatos.obtenerInstancia();

        // Verificamos que ambas referencias apuntan al mismo objeto
        if (conexion1 == conexion2) {
            System.out.println("Ambas conexiones son iguales.");
        }

        // Usamos la conexión para ejecutar una consulta
        conexion1.ejecutarConsulta("SELECT * FROM estudiantes");
    }
}
```
### Resultado en consola

```bash
Conexión establecida.
Ambas conexiones son iguales.
Ejecutando consulta: SELECT * FROM estudiantes

```

## 4. Explicación

- **`ConexionBaseDatos`**: Es la clase Singleton que gestiona una única conexión a la base de datos.
    - El constructor de la clase es privado, lo que impide que se creen nuevas instancias directamente desde otras clases.
    - El método `obtenerInstancia` devuelve la única instancia de la clase, y si no ha sido creada aún, la crea.
- **Uso del Singleton**: En el método `main`, cuando se llaman a `obtenerInstancia()` varias veces, siempre devuelve la misma instancia, lo que garantiza que no haya múltiples conexiones a la base de datos.
- **Control de instancias**: Al comparar `conexion1` y `conexion2`, se confirma que ambas referencias apuntan al mismo objeto en memoria, validando el comportamiento del Singleton.

## 5. Conclusión

El patrón **Singleton** es una solución ideal para garantizar que una clase tenga solo una única instancia a lo largo de toda la aplicación. En este ejemplo, aseguramos que solo haya una conexión a la base de datos, lo que puede prevenir errores y optimizar el uso de recursos. El patrón proporciona un punto de acceso global a esta instancia y controla su ciclo de vida de manera eficiente, permitiendo centralizar la gestión de recursos compartidos.


