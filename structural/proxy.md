## Proxy

```java
package proxy;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class PersonaRemota implements Runnable{
  private Thread thread;
  ServerSocket socket;
  PrintWriter salida;
  Socket comunicationSocket;

  public PersonaRemota() {
    try {
      socket = new ServerSocket(45454);
      comunicationSocket = socket.accept();
      salida = new PrintWriter(comunicationSocket.getOutputStream(), true);
      thread = new Thread(this);
      thread.start();
    } catch (Exception e) {
      System.out.println("Ha ocurrido un error: "+e.getMessage());
    }
  }

  @Override
  public void run() {
    String textoEntrada;
    try {
      BufferedReader in = new BufferedReader(new InputStreamReader(
        comunicationSocket.getInputStream()));
      while ( ( textoEntrada = in.readLine() ) != null  ) {
        if (textoEntrada.equals("saludar")) {
          saludar();
        } else if(textoEntrada.equals("decirEstado")){
          decirEstado();
        } else if(textoEntrada.equals("despedirse")) {
          despedirse();
        }
      }
    } catch (Exception e) {
      System.out.println("Error general: "+e.getMessage());
    }
  }

  public void saludar() {
    salida.println("Hola!!!");
  }

  public void decirEstado() {
    salida.println("Estoy contento");
  }

  public void despedirse() {
    salida.println("Chao!!!");
  }

  public static void main(String[] args) {
    PruebaProxy pp = new PruebaProxy();
  }

}
```

```java
package proxy;

import java.io.IOException;
import java.io.InputStream;
import java.io.PrintWriter;
import java.net.Socket;

public class PersonaProxy implements Runnable {
  private Thread thread;
  Socket socket;
  InputStream in;
  PrintWriter salida;
  int character;

  public PersonaProxy() {
    try {
      socket = new Socket("127.0.0.1", 45454);
      System.out.println("Conectando...");
      in = socket.getInputStream();
      salida = new PrintWriter(socket.getOutputStream(), true);
      thread = new Thread(this);
      thread.start();
    } catch (IOException ioe) {
      System.err.println("Error al conectarse: "+ioe.getMessage());
    } catch (Exception e) {
      System.err.println("Error general: "+e.getMessage());
    }

    if (socket != null && socket.isConnected()) {
      System.out.println("Conectado!!!");
    }

  }

  @Override
  public void run() {
    try {
      while ( (character = in.read()) != -1 ) {
        System.out.println( (char) character );
      }

    } catch (Exception e) {
      System.out.println("Error general: "+e.getMessage());
    }
  }

  public void saludar() {
    salida.println("saludar");
  }

  public void decirEstado() {
    salida.println("decirEstado");
  }

  public void despedirse() {
    salida.println("despedirse");
  }

}
```

```java
package proxy;

public class PruebaProxy {
  PersonaProxy persona;

  public PruebaProxy() {
    persona = new PersonaProxy();
    persona.saludar();
    persona.decirEstado();
    persona.despedirse();
  }

  public static void main(String[] args) {
    PruebaProxy pp = new PruebaProxy();
  }
}
```