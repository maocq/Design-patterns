## Chain of responsibility

```java
public interface InterfaceAyuda{
  public void getAyuda(int tipoAyuda);
}
```

```java
public class FrontEnd implements InterfaceAyuda{
  private final int TIPO_AYUDA = 1;
  private InterfaceAyuda susesor;

  public FrontEnd(InterfaceAyuda s){
    this.susesor = s;
  }

  @Override
  public void getAyuda(int tipo){
    if(tipo == TIPO_AYUDA){
      System.out.println("\t== Ayuda desde el FrontEnd.");
    } else {
      susesor.getAyuda(tipo);
    }
  }
}
```

```java
public class Middle implements InterfaceAyuda{
  private final int TIPO_AYUDA = 2;
  private InterfaceAyuda susesor;

  public Middle(InterfaceAyuda s){
    this.susesor = s;
  }

  @Override
  public void getAyuda(int tipo){
    if(tipo == TIPO_AYUDA){
      System.out.println("\t++ Ayuda desde el Middle.");
    } else {
      susesor.getAyuda(tipo);
    }
  }
}
```

```java
public class Aplicacion implements InterfaceAyuda{
  private final int TIPO_AYUDA = 3;

  public Aplicacion(){}

  @Override
  public void getAyuda(int tipo){
    System.out.println("\t-- Ayuda BASE DE LA APLICACION.");
  }
}
```

```java
import java.util.Scanner;

public class PruebaCadena{
  public static void main(String... args){
    Scanner sc = new Scanner(System.in);
    int opcion = 0;

    Aplicacion aplicacion = new Aplicacion();
    Middle intermediario  = new Middle(aplicacion);
    FrontEnd presentacion = new FrontEnd(intermediario);

    do{
      System.out.println("**************************************");
      System.out.println("* SELECCIONE LA AYUDA QUE DESEA VER  *");
      System.out.println("* 1 = Presentacion                   *");
      System.out.println("* 2 = Logica                         *");
      System.out.println("* 3 = Aplicacion                     *");
      System.out.println("* 0 = Salir del programa de ayuda    *");
      System.out.println("**************************************");

      opcion = sc.nextInt();
      if(opcion!=0){
        presentacion.getAyuda(opcion);
      }
    } while(opcion!=0);
  }
}
```