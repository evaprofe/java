

---

### Ficha 1: Introducción a la Serialización
**Título:** ¿Qué es la serialización?
- **Definición:** Proceso de convertir un objeto en un flujo de bytes para almacenarlo en un archivo, transmitirlo a través de una red o mantener su estado en memoria.
- **Interfaz Serializable:** Las clases que se van a serializar deben implementar esta interfaz.

---

### Ficha 2: Clase `Serializable`
**Título:** Implementación de `Serializable`
- **Código Ejemplo:**
  ```java
  import java.io.Serializable;

  public class Persona implements Serializable {
      private static final long serialVersionUID = 1L;
      private String nombre;
      private int edad;

      public Persona(String nombre, int edad) {
          this.nombre = nombre;
          this.edad = edad;
      }

      // Getters y setters
  }
  ```
- **serialVersionUID:** Número de versión único para la clase. Ayuda a detectar cambios en la estructura de la clase.

---

### Ficha 3: Serializar un Objeto
**Título:** Cómo serializar un objeto
- **Código Ejemplo:**
  ```java
  import java.io.FileOutputStream;
  import java.io.ObjectOutputStream;

  public class SerializarEjemplo {
      public static void main(String[] args) {
          Persona persona = new Persona("Juan", 30);

          try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("persona.ser"))) {
              oos.writeObject(persona);
              System.out.println("Objeto serializado correctamente.");
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```
- **Pasos:**
  1. Crear un objeto de la clase `ObjectOutputStream`.
  2. Asociarlo a un flujo de salida (como un archivo).
  3. Llamar al método `writeObject()` para serializar el objeto.

---

### Ficha 4: Deserializar un Objeto
**Título:** Cómo deserializar un objeto
- **Código Ejemplo:**
  ```java
  import java.io.FileInputStream;
  import java.io.ObjectInputStream;

  public class DeserializarEjemplo {
      public static void main(String[] args) {
          Persona persona = null;

          try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("persona.ser"))) {
              persona = (Persona) ois.readObject();
              System.out.println("Nombre: " + persona.getNombre());
              System.out.println("Edad: " + persona.getEdad());
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```
- **Pasos:**
  1. Crear un objeto de la clase `ObjectInputStream`.
  2. Asociarlo a un flujo de entrada (como un archivo).
  3. Llamar al método `readObject()` para deserializar el objeto.

---

### Ficha 5: Campos Transitorios
**Título:** Campos transitorios
- **Definición:** Campos que no se serializan.
- **Código Ejemplo:**
  ```java
  private transient String password;
  ```
- **Uso:** Útil para campos que no deben ser almacenados o transmitidos, como contraseñas.

---

### Ficha 6: Personalización de la Serialización
**Título:** Métodos personalizados
- **Métodos:**
  - `private void writeObject(ObjectOutputStream oos)`
  - `private void readObject(ObjectInputStream ois)`
- **Uso:** Permiten controlar el proceso de serialización y deserialización.
- **Ejemplo:**
  ```java
  private void writeObject(ObjectOutputStream oos) throws IOException {
      oos.defaultWriteObject();
      oos.writeInt(edad);
  }

  private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
      ois.defaultReadObject();
      edad = ois.readInt();
  }
  ```

---

### Ficha 7: Uso Práctico
**Título:** Ejemplo completo
- **Clase Principal:**
  ```java
  public class EscribirYLeer {
      public static void main(String[] args) {
          EscribirYLeer eyl = new EscribirYLeer();
          eyl.escribeFichero("mascotas.dat");
          eyl.anhadeFichero("mascotas.dat");
          eyl.leeFichero("mascotas.dat");
      }
  }
  ```
- **Métodos:**
  - `escribeFichero(String fichero)`: Escribe objetos en un archivo.
  - `anhadeFichero(String fichero)`: Añade objetos al archivo sin sobrescribir.
  - `leeFichero(String fichero)`: Lee y muestra los objetos almacenados.

---

