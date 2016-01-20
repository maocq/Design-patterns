## State

```java
public interface Estado{
  public void ejecutarAccion();
}
```

```java
public class Activa implements Estado{
  @Override
  public void ejecutarAccion(){
    System.out.println("Estado Activo: Atento");
  }
}
```

```java
public class Mantenimiento implements Estado{
  @Override
  public void ejecutarAccion(){
    System.out.println("Estado en mantenimiento: No atento");
    System.out.println("Enviar correo para informar el estado");
  }
}
```

```java
public class Alarma{
  private Estado miEstado;

  public void setEstado(Estado e){
    this.miEstado = e;
  }

  public void ejecutarAccion(){
    miEstado.ejecutarAccion();
  }
}
```

```java
import java.util.Scanner;

public class PruebaEstado{
  public static void main(String... args){
    Alarma alarma = new Alarma();
    Activa activa = new Activa();
    Mantenimiento mantenimiento = new Mantenimiento();
    int opcion = 0;
    Scanner sc = new Scanner(System.in);

    do{
      muestraMenu();
      opcion = sc.nextInt();
      switch(opcion){
        case 1:
          alarma.setEstado(activa);
          break;
        case 2:
          alarma.setEstado(mantenimiento);
          break;
        case 0:
          System.exit(0);
        default:
          System.out.println("Opcion errada");
      }
      alarma.ejecutarAccion();
    } while(opcion!=0);
  }

  private static void muestraMenu(){
    StringBuffer menu = new StringBuffer();
    menu.append("****************************************\n");
    menu.append("* SELECCIONE EL ESTADO DE LA ALARMA    *\n");
    menu.append("* 1- ACTIVA. 2- MANTENIMIENTO 0- SALIR *\n");
    menu.append("****************************************\n");
    System.out.println(menu.toString());
  }
}
```