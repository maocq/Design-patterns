## Memento

```java
public class Registro{
  private String nombre;
  private int edad;
  private boolean esActivo;

  public Registro(String n, int e, boolean a){
    this.nombre = n;
    this.edad = e;
    this.esActivo = a;
  }

  public void getRegistro(){
    System.out.print("Nombre: "+this.nombre+", ");
    System.out.print("Edad: "+this.edad+", ");
    System.out.print("Activo: "+this.esActivo+".\n");
  }
}
```

```java
import java.util.ArrayList;

public class BaseDeDatos{
  private ArrayList<Registro> listado;
  private Memento memento;

  public BaseDeDatos(){
    listado = new ArrayList<Registro>();
    memento = new Memento();
  }

  public void agregarRegistro(String n, int e, boolean a){
    Registro temp = new Registro(n,e,a);
    listado.add(temp);
  }

  public void limpiarBD(){
    listado = null;
  }

  public void mostrarListado(){
    if(listado!=null){
      for(Registro temp: listado){
        temp.getRegistro();
      }
    } else {
      System.out.println("Base de datos vacia!!!");
    }
  }

  public void generarBackup(){
    memento.setBackup(listado);
  }

  public void getBackup(int i){
    listado = new ArrayList<Registro>();
    for(Registro temp: memento.getBackup(i)){
      listado.add(temp);
    }
  }

  public int getTamanioBackup(){
    return memento.getSize();
  }
}
```

```java
import java.util.ArrayList;

public class Memento{
  private ArrayList<ArrayList<Registro>> backup;

  public Memento(){
    backup = new ArrayList<ArrayList<Registro>>();
  }

  public void setBackup(ArrayList<Registro> bd){
    ArrayList<Registro> lista = new ArrayList<Registro>();
    for(Registro registro: bd){
      lista.add(registro);
    }
    backup.add(lista);
  }

  public ArrayList<Registro> getBackup(int i){
    return backup.get(i);
  }

  public int getSize(){
    return backup.size();
  }
}
```

```java
import java.util.Scanner;

public class PruebaMemento{
  public static void main(String args[]){

    Scanner sc = new Scanner(System.in);
    int opcion = 0;
    BaseDeDatos bd = new BaseDeDatos();

    bd.agregarRegistro("Alexys Lozada",33,true);
    bd.agregarRegistro("Ronald Lozada",32,true);
    bd.generarBackup();

    bd.agregarRegistro("Carol Lozada",18,true);
    bd.agregarRegistro("Leidy Gonzalez",10,true);
    bd.generarBackup();

    bd.agregarRegistro("Yamile Gamboa",33,false);
    bd.agregarRegistro("Jennifer Piedrahita",27,false);
    bd.generarBackup();

    do{
      mostrarMenu();
      opcion = sc.nextInt();
      switch(opcion){
        case 1:
          bd.mostrarListado();
          break;
        case 2:
          bd.limpiarBD();
          System.out.println("Base de datos borrada.");
          break;
        case 3:
          muestraBackup(bd.getTamanioBackup());
          bd.getBackup(sc.nextInt()-1);
          break;
        default:
          System.out.println("No ha digitado una opcion valida");
      }
    } while (opcion!=0);
  }

  public static void mostrarMenu(){
    System.out.println("*********************************************");
    System.out.println("* SELECCIONE LA OPCION DE LA BD             *");
    System.out.println("* 1- Listar 2- LimpiarBD 3- Restaura Backup *");
    System.out.println("*********************************************");
  }

  public static void muestraBackup(int t){
    System.out.format("Existen %s backups.", t);
    System.out.print("\nDigite el backup que desea restaurar: ");
  }
}
```