## Factory

```java
package factory;

public abstract class Conexion {

  //Constructor vacio
  public Conexion(){}


  //Método descripción
  public String descripcion() {
    return "Conexión generica";
  }

}
```

```java
package factory;

public class MySqlConexion extends Conexion {

  public MySqlConexion(){}

  @Override
  public String descripcion() {
    return "Conexión MySql";
  }


}
```

```java
package factory;

public class OracleConexion extends Conexion{

  public OracleConexion(){}

  @Override
  public String descripcion() {
    return "Conexión oracle";
  }

}
```

```java
package factory;

public class SqlServerConexion extends Conexion {

  public SqlServerConexion(){}

  @Override
  public String descripcion() {
    return "Conexión SqlServer";
  }


}
```



```java
package factory;

public class Fabrica {

  protected String tipo;

  // Constructor que recibe el nombre
  // del tipo de conexión

  public Fabrica(String t) {
    tipo = t;
  }

  // Método que retorna el objeto
  // conexión especifico
  public Conexion creaConexion() {
    if (tipo.equalsIgnoreCase("Oracle")) {
      return new OracleConexion();
    } else if (tipo.equalsIgnoreCase("SqlServer")) {
      return new SqlServerConexion();
    } else {
      return new MySqlConexion();
    }
  }

}
```

```java
package factory;

import java.util.Scanner;

public class Contabilidad {

  public static void main(String[] args) {
    // TODO Auto-generated method stub

    Scanner sc = new Scanner(System.in);
    Fabrica miFabrica;
    Conexion miConexion;

    System.out.println("Digite la BD:");
    String tipo = sc.nextLine();

    miFabrica = new Fabrica(tipo);
    miConexion = miFabrica.creaConexion();

    String salida = "Esta conectado con "+ miConexion.descripcion();
    System.out.println(salida);

  }

}
```
