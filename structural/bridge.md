## Bridge

```java
package bridge;

public interface I_ImpLista {
  public void addItem(String item);
  public void remItem(String item);
  public int getCantidadDeItems();
  public String getItem(int index);
  public boolean soportaRepetidos();
}
```

```java
package bridge;

import java.util.ArrayList;

public class ImpListaRepetidos implements I_ImpLista{

  private ArrayList<String> listaItems = new ArrayList<String>();

  @Override
  public void addItem(String item) {
    listaItems.add(item);
  }

  @Override
  public void remItem(String item) {
    if (listaItems.contains(item)) {
      listaItems.remove(listaItems.indexOf(item));
    }
  }

  @Override
  public int getCantidadDeItems() {
    return listaItems.size();
  }

  @Override
  public String getItem(int index) {
    if (index < listaItems.size()) {
      return (String) listaItems.get(index);
    }
    return null;
  }

  @Override
  public boolean soportaRepetidos() {
    return true;
  }

}
```

```java
package bridge;

import java.util.ArrayList;

public class ImpListaUnicos implements I_ImpLista {

  private ArrayList<String> listaItems = new ArrayList<String>();

  @Override
  public void addItem(String item) {
    if (!listaItems.contains(item)) {
      listaItems.add(item);
    }
  }

  @Override
  public void remItem(String item) {
    if (listaItems.contains(item)) {
      listaItems.remove(listaItems.indexOf(item));
    }
  }

  @Override
  public int getCantidadDeItems() {
    return listaItems.size();
  }

  @Override
  public String getItem(int index) {
    if (index < listaItems.size()) {
      return (String) listaItems.get(index);
    }
    return null;
  }

  @Override
  public boolean soportaRepetidos() {
    return false;
  }

}
```

```java
package bridge;

public class ListaBase {

  protected I_ImpLista implementacion;

  public void setImplementacion(I_ImpLista impl) {
    this.implementacion = impl;
  }

  public void agregarItem(String item) {
    implementacion.addItem(item);
  }

  public void removerItem(String item) {
    implementacion.remItem(item);
  }

  public int cuentaItems() {
    return implementacion.getCantidadDeItems();
  }

  public String obtenerItem(int index) {
    return implementacion.getItem(index);
  }

}
```

```java
package bridge;

public class ListaEnumerada extends ListaBase {

  @Override
  public String obtenerItem(int index) {
    return (index + 1) + ". " + super.obtenerItem(index);
  }

}
```

```java
package bridge;

public class ListaVineta extends ListaBase {

  private char tipoVineta;

  public void setTipoItem(char nuevoTipo) {
    if (nuevoTipo > ' ') {
      tipoVineta = nuevoTipo;
    } else {
      tipoVineta = '+';
    }
  }

  @Override
  public String obtenerItem(int index) {
    return tipoVineta + " " + super.obtenerItem(index);
  }

}
```

```java
package bridge;

import java.util.Scanner;

public class PruebaBridge {

  public static void main(String[] args) {

    Scanner entrada = new Scanner(System.in);
    int opcion;

    I_ImpLista implementacion;

    System.out.println("\n Digite el tipo de lista que desea");
    System.out.println("1 = Items repetidos, 2 = Items unicos \n");

    opcion = entrada.nextInt();

    switch (opcion) {
    case 1:
      System.out.println("Creando lista. Permite repetidos");
      implementacion = new ImpListaRepetidos();
      break;
    case 2:
      System.out.println("Creando lista. Items unicos");
      implementacion = new ImpListaUnicos();
      break;
    default:
      System.out.println("Error, debe elegir entre 1 0 2");
      System.out.println("Saliendo del programa...");
      return;
    }

    System.out.println("Creando presentacion Base...");
    ListaBase listabase = new ListaBase();
    listabase.setImplementacion(implementacion);
    System.out.println("Lista base creada!!! \n");

    System.out.println("Por favor digite 3 elementos de la lista");
    for (int i = 0; i < 3; i++) {
      System.out.print("Item "+(i + 1)+": ");
      listabase.agregarItem(entrada.next());
    }

    System.out.println("Creando una lista enumerada...");
    ListaEnumerada listaEnumerada = new ListaEnumerada();
    listaEnumerada.setImplementacion(implementacion);

    System.out.println("Creando una lista con viñetas...");
    ListaVineta listaVineta = new ListaVineta();
    listaVineta.setImplementacion(implementacion);

    System.out.println("Digite un simbolo para la viñeta");
    listaVineta.setTipoItem( (char) entrada.next().charAt(0) );

    System.out.println("Imprimiendo las diferentes listas...");

    System.out.println("Lista base");
    for (int i = 0; i < listabase.cuentaItems(); i++) {
      System.out.println("\t"+listabase.obtenerItem(i));
    }

    System.out.println("Lista enumerada");
    for (int i = 0; i < listaEnumerada.cuentaItems(); i++) {
      System.out.println("\t"+listaEnumerada.obtenerItem(i));
    }

    System.out.println("Lista con viñetas");
    for (int i = 0; i < listaVineta.cuentaItems(); i++) {
      System.out.println("\t"+listaVineta.obtenerItem(i));
    }

  }

}
```