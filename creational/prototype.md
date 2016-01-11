## Prototype

```java
package prototype;

public interface Figura {
  public void setNombre(String n);
  public String getNombre();
  public void mover(int x,int y);
  public void getPosicion();
  public Figura clonar();
}
```

```java
package prototype;

public class Circulo implements Figura{
  private String nombre;
  private int posicionX, posicionY;

  public Circulo() {}

  @Override
  public void setNombre(String n) {
    this.nombre = n;
  }

  @Override
  public String getNombre() {
    return nombre;
  }

  @Override
  public void mover(int x, int y) {
    this.posicionX = x;
    this.posicionY = y;
  }

  @Override
  public void getPosicion() {
    System.out.println("Circulo en x "+ this.posicionX);
    System.out.println("Circulo en y "+ this.posicionY);
  }

  @Override
  public Figura clonar() {
    Figura figura = new Circulo();
    figura.setNombre(this.nombre);
    figura.mover(this.posicionX, this.posicionY);
    return figura;
  }

}
```

```java
package prototype;

public class Cuadrado implements Figura{
  private String nombre;
  private int posicionX, posicionY;

  public Cuadrado() {}

  @Override
  public void setNombre(String n) {
    this.nombre = n;
  }

  @Override
  public String getNombre() {
    return nombre;
  }

  @Override
  public void mover(int x, int y) {
    this.posicionX = x;
    this.posicionY = y;
  }

  @Override
  public void getPosicion() {
    System.out.println("Cuadrado en x "+ this.posicionX);
    System.out.println("Cuadrado en y "+ this.posicionY);
  }

  @Override
  public Figura clonar() {
    Figura figura = new Cuadrado();
    figura.setNombre(this.nombre);
    figura.mover(this.posicionX, this.posicionY);
    return figura;
  }

}
```
---

```java
package prototype;

import java.util.Scanner;

public class PruebaFiguras {

  public static void main(String[] args) {

    Scanner sc = new Scanner(System.in);
    int opcion, posX, posY;

    Circulo circulo = new Circulo();
    Cuadrado cuadrado = new Cuadrado();
    Figura figura;

    circulo.setNombre("Mi circulo");
    circulo.mover(12, 34);

    cuadrado.setNombre("Mi cuadrado");
    cuadrado.mover(200, 200);

    System.out.println("Estas son las figuras originales");
    System.out.println("Circulo: "+circulo.getNombre());
    System.out.println("Cuadrado: "+cuadrado.getNombre());
    System.out.println("Estas son las posiciones originales");
    circulo.getPosicion();
    cuadrado.getPosicion();

    System.out.println("Digite la opción que desea clonar: ");
    System.out.println("1 = Circulo, 2 = Cuadrado");
    opcion = sc.nextInt();

    if (opcion == 1) {
      figura = circulo.clonar();
    } else {
      figura = cuadrado.clonar();
    }

    figura.setNombre(figura.getNombre() + " clonado");
    System.out.println("Digite la nueva posicion en X:");
    posX = sc.nextInt();
    System.out.println("Digite la nueva posicion en Y:");
    posY = sc.nextInt();
    figura.mover(posX, posY);

    System.out.println("Esta es la figura clonada");
    System.out.println(figura.getNombre());
    System.out.println("Esta es la posicion del clon");
    figura.getPosicion();

    System.out.println("Estas son las figuras originales");
    System.out.println("Circulo: "+circulo.getNombre());
    System.out.println("Cuadrado: "+cuadrado.getNombre());
    System.out.println("Estas son las posiciones originales");
    circulo.getPosicion();
    cuadrado.getPosicion();

  }

}
```