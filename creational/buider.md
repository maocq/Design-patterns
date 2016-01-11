## Builder

```java
package builder;

import java.util.List;

public interface Robot {

  public void trabajar();

  public void cargaAcciones(List<Integer> accion);
}
```

```java
package builder;

import java.util.List;

public class RobotHamburguesa implements Robot {

  List<Integer> acciones;

  public RobotHamburguesa() {}

  private void iniciar() {
    System.out.println("Iniciando la Hamburguesa");
  }

  private void getIngredientes() {
    System.out.println("Buscando: Pan, Hambuerguesa, Salsas");
  }

  private void armar() {
    System.out.println("Armando la Hamburguesa");
  }

  private void revisar() {
    System.out.println("Revisando el proceso");
  }

  private void terminar() {
    System.out.println("Proceso terminado");
  }

  @Override
  public void cargaAcciones(List<Integer> accion) {
    this.acciones = accion;
  }

  @Override
  public void trabajar() {
    iniciar();
    for(Integer i:acciones) {
      switch (i) {
      case 1:
        getIngredientes();
        break;
      case 2:
        armar();
        break;
      case 3:
        revisar();
        break;
      default:
        System.out.println("Esa acción no la puedo hacer");
        break;
      }
    }
    terminar();
  }

}
```

```java
package builder;

import java.util.List;

public class RobotHotDog implements Robot {

    List<Integer> acciones;

    public RobotHotDog() {}

    private void start() {
      System.out.println("Iniciando el HotDog");
    }

    private void getParts() {
      System.out.println("Buscando: Pan, Salchicha, Salsas");
    }

    private void build() {
      System.out.println("Armando el HotDog");
    }

    private void check() {
      System.out.println("Revisando el proceso");
    }

    private void finish() {
      System.out.println("Proceso terminado");
    }

    @Override
    public void cargaAcciones(List<Integer> accion) {
      this.acciones = accion;
    }

    @Override
    public void trabajar() {
      start();
      for(Integer i:acciones) {
        switch (i) {
        case 1:
          getParts();
          break;
        case 2:
          build();
          break;
        case 3:
          check();
          break;
        default:
          System.out.println("Esa acción no la puedo hacer");
          break;
        }
      }
      finish();
    }

}
```

```java
package builder;

import java.util.ArrayList;
import java.util.List;

public class Builder {

  Robot robot;

  List<Integer> acciones;

  public Builder() {
    acciones = new ArrayList<Integer>();
  }

  public void setRobot(int i) {
    if(i == 1) {
      robot = new RobotHamburguesa();
    } else {
      robot = new RobotHotDog();
    }
  }

  public void addGetIngredientes() {
    acciones.add(1);
  }

  public void addArmar() {
    acciones.add(2);
  }

  public void addRevisar() {
    acciones.add(3);
  }

  public void addImposible() {
    acciones.add(100);
  }



  public Robot getRobot() {
    robot.cargaAcciones(acciones);
    return robot;
  }

}
```

```java
package builder;

import java.util.Scanner;

public class Cliente {

  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    Builder constructor = new Builder();
    Robot robot;
    int tipoRobot;

    System.out.println("Digite el tipo de robot que desea: ");
    tipoRobot = sc.nextInt();

    constructor.setRobot(tipoRobot);
    constructor.addRevisar();
    constructor.addImposible();
    constructor.addGetIngredientes();
    constructor.addArmar();
    constructor.addRevisar();

    robot = constructor.getRobot();
    robot.trabajar();
  }

}
```