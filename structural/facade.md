## Facade

```java
package facade;

public class Cpu {

  private boolean voltajeOk, energiaDispositivos, listoOk;

  public Cpu() {}

  public boolean enviarVoltaje(int voltaje) {
    if( voltaje >= 100  &&  voltaje <= 120) {
      voltajeOk = true;
    }
    return voltajeOk;
  }

  public boolean enviaEnergiaADispositivos() {
    if(voltajeOk) {
      energiaDispositivos = true;
    }
    return energiaDispositivos;
  }

  //...

  public boolean cpuLista() {
    if(energiaDispositivos) {
      listoOk = true;
    }
    return listoOk;
  }

}
```

```java
package facade;

public class ClienteSinFachada {
  private Cpu miCPU;

  public ClienteSinFachada() {
    miCPU = new Cpu();
  }

  public void encenderCPU() {
    miCPU.enviarVoltaje(110);
    miCPU.enviaEnergiaADispositivos();
    //...
    if(miCPU.cpuLista()) {
      System.out.println("CPU Encendida y lista!!!");
    }
  }

  public void trabajar() {
    System.out.println("Comienzo a trabajar!!!");
  }

  public static void main(String[] args) {
    ClienteSinFachada csf = new ClienteSinFachada();
    csf.encenderCPU();
    csf.trabajar();
  }
}
```
---

```java
package facade;

public class Fachada {
  private Cpu miCPU;

  public Fachada() {
    miCPU = new Cpu();
  }

  public void encenderCPU() {
    miCPU.enviarVoltaje(110);
    miCPU.enviaEnergiaADispositivos();
    //...
    if(miCPU.cpuLista()) {
      System.out.println("CPU Encendida y lista!!!");
    }
  }

}
```

```java
package facade;

public class ClienteConFachada {
  public Fachada miFachada;

  public ClienteConFachada() {
    miFachada = new Fachada();
  }

  public void encenderCPU() {
    miFachada.encenderCPU();
    System.out.println("COMIENZO A TRABAJAR");
  }

  public static void main(String[] args) {
    ClienteConFachada ccf = new ClienteConFachada();
    ccf.encenderCPU();
  }

}
```