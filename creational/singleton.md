## Singleton


```java
package singleton;

public final class Singleton {

  private static final Singleton singleton = new Singleton();
  private static int cantidad;

  private Singleton() {
    System.out.println("Hola he sido creado una sola vez!!");
  }

  public static Singleton obtenerSingleton() {
    cantidad++;
    return singleton;
  }

  public static void vecesLlamado() {
    System.out.println("Se ha llamado el metodo "+cantidad+" veces");
  }

}
```

```java
package singleton;

public class PruebaSingleton {

  public static void main(String[] args) {

    Singleton miSingleton = Singleton.obtenerSingleton();
    Singleton miSingleton2 = Singleton.obtenerSingleton();
    Singleton miSingleton3 = Singleton.obtenerSingleton();
    Singleton miSingleton4 = Singleton.obtenerSingleton();
    Singleton miSingleton5 = Singleton.obtenerSingleton();

    miSingleton3.vecesLlamado();

    System.out.println("He terminado");

  }

}
```


#### Ejemplo

```java
package singleton;

import sun.net.www.content.text.plain;

public final class Marcianos {
  private static final Marcianos marcianos = new Marcianos();
  private static int cantidad;

  private Marcianos() {
    cantidad = 10;
  }

  public static Marcianos getMarcianos() {
    return marcianos;
  }

  public static void derribaMarcianos() {
    System.out.println("Derribe un marciano");
    if(cantidad > 0)
      cantidad--;
  }

  public static void creaMarcianos() {
    if(cantidad > 0) {
      System.out.println("Cree un marciano");
      cantidad++;
    }
  }

  public static void cuantosQuedan() {
    if (cantidad > 0) {
      System.out.println("Quedam "+cantidad+" marcianos");
    } else {
      System.out.println("Has ganado!!!");
    }
  }
}
```

```java
package singleton;

public class Computadora {
  private Marcianos marcianos = Marcianos.getMarcianos();

  public Computadora(){}

  public void creaMarcianos() {
    marcianos.creaMarcianos();
  }
}
```

```java
package singleton;

public class Jugador {
  private Marcianos marcianos;

  public Jugador() {
    marcianos = Marcianos.getMarcianos();
  }

  public void destruirMarciano() {
    marcianos.derribaMarcianos();
  }
}
```

```java
package singleton;

import java.util.Scanner;

public class Juego {

  public static void main(String[] args) {

    Marcianos marcianos;
    Computadora computadora;
    Jugador jugador;
    Scanner sc;

    marcianos = Marcianos.getMarcianos();
    computadora = new Computadora();
    jugador = new Jugador();

    sc = new Scanner(System.in);

    int disparos;

    do {
      System.out.println("Digite los disparos: ");
      disparos = sc.nextInt();
      for (int i = 0; i < disparos; i++) {
        jugador.destruirMarciano();
      }
      computadora.creaMarcianos();
      marcianos.cuantosQuedan();
    } while (disparos != 0);

  }

}
```