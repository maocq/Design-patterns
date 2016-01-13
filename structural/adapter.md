## Adapter

```java
package adapter;

public class Nombre {

  private String nombreCompuesto;

  public String getNombreCompuesto() {
    return nombreCompuesto;
  }

  public void setNombreCompuesto(String nombreCompuesto) {
    this.nombreCompuesto = nombreCompuesto;
  }

}
```

```java
package adapter;

public class Adaptador {

  private Nombre objetoNombre;
  private String nombre;
  private String apellido;

  public Adaptador(Nombre n) {
    this.objetoNombre = n;
    setNombre(objetoNombre.getNombreCompuesto().split(" ")[0]);
    setApellido(objetoNombre.getNombreCompuesto().split(" ")[1]);
  }

  public Nombre getObjetoNombre() {
    return objetoNombre;
  }
  public void setObjetoNombre(Nombre objetoNombre) {
    this.objetoNombre = objetoNombre;
  }
  public String getNombre() {
    return nombre;
  }
  public void setNombre(String nombre) {
    this.nombre = nombre;
  }
  public String getApellido() {
    return apellido;
  }
  public void setApellido(String apellido) {
    this.apellido = apellido;
  }

}
```

```java
package adapter;

import java.util.Scanner;

public class PruebaNombre {

  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    Nombre objetoNombre = new Nombre();

    System.out.println("Digite su nombre y apellido");
    objetoNombre.setNombreCompuesto(sc.nextLine());

    Adaptador adaptador = new Adaptador(objetoNombre);

    System.out.println("Tu nombre es: "+ adaptador.getNombre());
    System.out.println("Tu apellido es: "+ adaptador.getApellido());
  }

}
```