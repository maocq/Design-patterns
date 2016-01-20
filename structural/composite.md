## Composite

```java
public class Responsable{

  private String nombre;
  private String telefono;

  public Responsable(String n, String t){
    this.nombre = n;
    this.telefono = t;
  }

  public String getNombre(){
    return this.nombre;
  }

  public String getTelefono(){
    return this.telefono;
  }
}
```

```java
public interface ItemProyecto{

  public int getTiempo();
  public void imprimir();

}
```

```java
import java.util.ArrayList;

public class Proyecto implements ItemProyecto{

  private String nombre;
  private Responsable responsable;
  private ArrayList<ItemProyecto> itemsProyecto = new ArrayList<ItemProyecto>();

  public Proyecto(String n, Responsable r){
    this.nombre = n;
    this.responsable = r;
  }

  public String getNombre(){
    return this.nombre;
  }

  public void agregarItemProyecto(ItemProyecto ipr){
    if(!itemsProyecto.contains(ipr)){
      itemsProyecto.add(ipr);
    }
  }

  @Override
  public int getTiempo(){
    int tiempoTotal = 0;
    for(ItemProyecto item:itemsProyecto){
      tiempoTotal += item.getTiempo();
    }
    return tiempoTotal;
  }

  @Override
  public void imprimir(){
    System.out.println(getNombre()+" Horas: "+getTiempo());
    for(ItemProyecto item:itemsProyecto){
      System.out.print("\t");
      item.imprimir();
    }
  }
}
```

```java
public class Entregable implements ItemProyecto{

  private String nombre;

  public Entregable(String n){
    this.nombre = n;
  }

  @Override
  public int getTiempo(){
    return 0;
  }

  @Override
  public void imprimir(){
    System.out.println("\tEntregable: "+this.nombre);
  }
}
```

```java
import java.util.ArrayList;

public class Tarea implements ItemProyecto{

  private String nombre;
  private Responsable responsable;
  private int tiempoRequerido;
  private ArrayList<ItemProyecto> itemsTarea = new ArrayList<ItemProyecto>();

  public Tarea(String n, Responsable r, int t){
    this.nombre = n;
    this.responsable = r;
    this.tiempoRequerido = t;
  }

  public void agregarItemTarea(ItemProyecto ipr){
    if(!itemsTarea.contains(ipr)){
      itemsTarea.add(ipr);
    }
  }

  @Override
  public int getTiempo(){
    int tiempoTotal = tiempoRequerido;
    for(ItemProyecto item:itemsTarea){
      tiempoTotal += item.getTiempo();
    }
    return tiempoTotal;
  }

  @Override
  public void imprimir(){
    System.out.println("\t"+this.nombre+" Horas: "+getTiempo());
    for(ItemProyecto item:itemsTarea){
      System.out.print("\t\t");
      item.imprimir();
    }
  }
}
```

```java
import java.util.ArrayList;

public class ProgramarProyecto{

  private Proyecto miProyecto;
  private Responsable responsable1, responsable2, responsable3, responsable4, responsable5, responsable6,
            responsable7, responsable8, responsable9, responsable10, responsable11, responsable12,
            responsable13, responsable14, responsable15, responsable16;

  public ProgramarProyecto(){
    creaResponsables();
    creaProyectoPrincipal();
    creaSubProAnalisis();
    creaSubProDiseno();
    creaSubProDesarrollo();
    creaSubProPruebas();
    creaSubProImplementacion();
    miProyecto.imprimir();
  }

  public void creaResponsables(){
    responsable1 = new Responsable("ALEXYS LOZADA", "7898989");
    responsable2 = new Responsable("DANIEL LOZADA", "8767676");
    responsable3 = new Responsable("JENIFFER GONZALEZ", "4353535");
    responsable4 = new Responsable("JORGE PEREZ", "2131313");
    responsable5 = new Responsable("CARLOS RODRIGUEZ", "2232323");
    responsable6 = new Responsable("ARMANDO GOMEZ", "2343434");
    responsable7 = new Responsable("DEIBIS JIMENEZ", "2454545");
    responsable8 = new Responsable("CRISTIAN BANNOY", "2565656");
    responsable9 = new Responsable("LICETH GÃœIZA", "2676767");
    responsable10 = new Responsable("EDWIN JIMENEZ","2787878");
    responsable11 = new Responsable("LORENA GIRALDO","2898989");
    responsable12 = new Responsable("CAROL MARTINEZ","2909090");
    responsable13 = new Responsable("LEIDY PEREZ","3202020");
    responsable14 = new Responsable("JUAN PABLO SANCHEZ","3455667");
    responsable15 = new Responsable("DIANA LANCHEROS", "4322121");
    responsable16 = new Responsable("JEISSON LENNIS","6543232");
  }

  public void creaProyectoPrincipal(){
    miProyecto = new Proyecto("CREAR UN SOFTWARE",responsable1);
  }

  public void creaSubProAnalisis(){

    Proyecto subProyecto = new Proyecto("ANALISIS", responsable2);
    Entregable entregable = new Entregable("DOCUMENTO DE ANALISIS");

      Tarea tarea1 = new Tarea("IDENTIFICACION DE INTERESADOS", responsable3, 0);
        Tarea subTarea11 = new Tarea("IDENTIFICAR USUARIOS", responsable4, 36);
        Tarea subTarea12 = new Tarea("IDENTIFICAR TECNICOS", responsable5, 12);
      tarea1.agregarItemTarea(subTarea11);
      tarea1.agregarItemTarea(subTarea12);

      Tarea tarea2 = new Tarea("LEVANTAMIENTO DE REQUERIMIENTOS",responsable6,0);
        Tarea subTarea21 = new Tarea("REQUERIMIENTOS FUNCIONALES", responsable6, 72);
        Tarea subTarea22 = new Tarea("REQUERIMIENTOS NO FUNCIONALES", responsable6, 24);
      tarea2.agregarItemTarea(subTarea21);
      tarea2.agregarItemTarea(subTarea22);

      Tarea tarea3 = new Tarea("ANALISIS DE REQUERIMIENTOS", responsable7, 72);

    subProyecto.agregarItemProyecto(entregable);
    subProyecto.agregarItemProyecto(tarea1);
    subProyecto.agregarItemProyecto(tarea2);
    subProyecto.agregarItemProyecto(tarea3);

    miProyecto.agregarItemProyecto(subProyecto);
  }

  public void creaSubProDiseno(){

    Proyecto subProyecto = new Proyecto("DISENO", responsable2);
    Entregable entregable = new Entregable("DOCUMENTO DISENO");

      Tarea tarea1 = new Tarea("DISENO DE CASOS DE USO", responsable8, 34);
      Tarea tarea2 = new Tarea("DISENO DE SECUENCIAS", responsable8, 24);
      Tarea tarea3 = new Tarea("DIAGRAMAS DE UML", responsable8, 30);

    subProyecto.agregarItemProyecto(entregable);
    subProyecto.agregarItemProyecto(tarea1);
    subProyecto.agregarItemProyecto(tarea2);
    subProyecto.agregarItemProyecto(tarea3);

    miProyecto.agregarItemProyecto(subProyecto);
  }

  public void creaSubProDesarrollo(){

    Proyecto subProyecto = new Proyecto("DESARROLLO", responsable2);
    Entregable entregable = new Entregable("CODIGO FUENTE");

      Tarea tarea1 = new Tarea("DEFINICION DEL LENGUAJE A USAR", responsable9, 12);
      Tarea tarea2 = new Tarea("DESARROLLAR CODIGO", responsable10, 0);
        Tarea subTarea21 = new Tarea("CODIGO DE CAPA DE DATOS", responsable11, 120);
        Tarea subTarea22 = new Tarea("CODIGO DE CAPA LOGICA", responsable12, 180);
        Tarea subTarea23 = new Tarea("CODIGO DE CAPA PRESENTACION", responsable13, 120);
      tarea2.agregarItemTarea(subTarea21);
      tarea2.agregarItemTarea(subTarea22);
      tarea2.agregarItemTarea(subTarea23);

    subProyecto.agregarItemProyecto(entregable);
    subProyecto.agregarItemProyecto(tarea1);
    subProyecto.agregarItemProyecto(tarea2);

    miProyecto.agregarItemProyecto(subProyecto);
  }

  public void creaSubProPruebas(){

    Proyecto subProyecto = new Proyecto("PRUEBAS", responsable2);
    Entregable entregable = new Entregable("DOCUMENTO DE ACEPTACION");

      Tarea tarea1 = new Tarea("REALIZACION DE PRUEBAS TECNICAS", responsable14, 24);
      Tarea tarea2 = new Tarea("REALIZACION DE PRUEBAS DE USUARIO", responsable15, 36);

    subProyecto.agregarItemProyecto(entregable);
    subProyecto.agregarItemProyecto(tarea1);
    subProyecto.agregarItemProyecto(tarea2);

    miProyecto.agregarItemProyecto(subProyecto);
  }

  public void creaSubProImplementacion(){

    Proyecto subProyecto = new Proyecto("IMPLEMENTACION", responsable2);
    Entregable entregable = new Entregable("SOFTWARE FUNCIONANDO");

      Tarea tarea1 = new Tarea("CONFIGURACION DEL SERVIDOR", responsable16, 24);
      Tarea tarea2 = new Tarea("IMPLEMENTACION DEL SOFTWARE", responsable2, 24);

    subProyecto.agregarItemProyecto(entregable);
    subProyecto.agregarItemProyecto(tarea1);
    subProyecto.agregarItemProyecto(tarea2);

    miProyecto.agregarItemProyecto(subProyecto);
  }
}
```

```java
public class PruebaCompuesto{
  public static void main(String... args){
    System.out.println();
    ProgramarProyecto pp = new ProgramarProyecto();
  }
}
```