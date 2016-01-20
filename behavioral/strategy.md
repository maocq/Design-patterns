## Strategy

```java
public interface Algoritmo{
  public void moverse();
}
```

```java
public class EnTierra implements Algoritmo{
  @Override
  public void moverse(){
    System.out.println("Moviendose sobre ruedas");
  }
}
```

```java
public class EnAire implements Algoritmo{
  @Override
  public void moverse(){
    System.out.println("Volando en los aires");
  }
}
```

```java
public class EnAireVeloz implements Algoritmo{
  @Override
  public void moverse(){
    System.out.println("Volando muy rapido!!!");
  }
}
```

```java
public abstract class Avion{
  private Algoritmo miAlgoritmo;

  public void setAlgoritmo(Algoritmo a){
    this.miAlgoritmo = a;
  }

  public void mover(){
    this.miAlgoritmo.moverse();
  }
}
```

```java
public class AvionComercial extends Avion{
  public AvionComercial(){}
}
```

```java
public class AvionRapido extends Avion{
  public AvionRapido(){}
}
```

```java
public class PruebaEstrategia{
  public static void main(String[] args){
    AvionComercial avionComercial = new AvionComercial();
    AvionRapido avionRapido = new AvionRapido();

    System.out.println("Primero el avion comercial...");
    avionComercial.setAlgoritmo(new EnTierra());
    avionComercial.mover();
    avionComercial.setAlgoritmo(new EnAire());
    avionComercial.mover();
    System.out.println();

    System.out.println("Ahora el avion rapido...");
    avionRapido.setAlgoritmo(new EnTierra());
    avionRapido.mover();
    avionRapido.setAlgoritmo(new EnAireVeloz());
    avionRapido.mover();
    System.out.println();

    System.out.println("El avion comercial veloz...");
    avionComercial.setAlgoritmo(new EnAireVeloz());
    avionComercial.mover();
  }
}
```