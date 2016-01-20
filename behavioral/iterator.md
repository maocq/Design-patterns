## Iterator

```java
public class ListaNumeros{
  private int numeros[];
  private int posicion;

  public ListaNumeros(){
    numeros = new int[10];
    posicion = 0;
  }

  public void agregar(int i){
    numeros[posicion++] = i;
  }

  public ListaNumerosIterador iterador(){
    return new ListaNumerosIterador(numeros);
  }
}
```

```java
public class ListaPalabras{
  private String palabra1, palabra2, palabra3, palabra4, palabra5;
  private int posicion;

  public ListaPalabras(){
    posicion = 0;
  }

  public void agregar(String p){
    switch(posicion){
      case 0:
        palabra1 = p;
        break;
      case 1:
        palabra2 = p;
        break;
      case 2:
        palabra3 = p;
        break;
      case 3:
        palabra4 = p;
        break;
      case 4:
        palabra5 = p;
        break;
    }
    posicion++;
  }

  public ListaPalabrasIterador iterador(){
    return new ListaPalabrasIterador(palabra1, palabra2, palabra3, palabra4, palabra5);
  }
}
```

```java
public interface Iterador{
  public Object siguiente();
  public boolean tieneSiguiente();
}
```

```java
public class ListaNumerosIterador implements Iterador{
  private int numeros[];
  private int posicion;

  public ListaNumerosIterador(int num[]){
    this.numeros = num;
    this.posicion = 0;
  }

  @Override
  public Object siguiente(){
    return numeros[posicion++];
  }

  @Override
  public boolean tieneSiguiente(){
    if(posicion < numeros.length && numeros[posicion] != 0){
      return true;
    } else {
      return false;
    }
  }
}
```

```java
public class ListaPalabrasIterador implements Iterador{
  private String palabra1, palabra2, palabra3, palabra4, palabra5;
  private int posicion;

  public ListaPalabrasIterador(String p1, String p2,
                 String p3, String p4,
                 String p5)
  {
    this.palabra1 = p1;
    this.palabra2 = p2;
    this.palabra3 = p3;
    this.palabra4 = p4;
    this.palabra5 = p5;
    this.posicion = 0;
  }

  @Override
  public Object siguiente(){
    switch(posicion++){
      case 0:
        return palabra1;
      case 1:
        return palabra2;
      case 2:
        return palabra3;
      case 3:
        return palabra4;
      case 4:
        return palabra5;
    }
    return null;
  }

  @Override
  public boolean tieneSiguiente(){
    if(posicion < 5){
      return true;
    } else {
      return false;
    }
  }
}
```

```java
public class PruebaIterador{
  public static void main(String... args){
    ListaNumeros ln = new ListaNumeros();
    ListaPalabras lp = new ListaPalabras();
    Iterador iterador;

    ln.agregar(5);
    ln.agregar(3);
    ln.agregar(1);
    ln.agregar(9);
    ln.agregar(2);
    ln.agregar(8);

    lp.agregar("OCHO");
    lp.agregar("CINCO");
    lp.agregar("DOS");
    lp.agregar("UNO");
    lp.agregar("TRES");
    lp.agregar("NUEVE");

    iterador = ln.iterador();
    while(iterador.tieneSiguiente()){
      // Acceder al elemento
      int numero = (int) iterador.siguiente();
      // Hacer algo con el elemento
      System.out.println(numero);
    }

    System.out.println();

    iterador = lp.iterador();
    while(iterador.tieneSiguiente()){
      String palabra = (String) iterador.siguiente();
      System.out.println(palabra);
    }

  }
}
```