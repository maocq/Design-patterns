## Abstract Factory

```java
package abstract_factory;

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
package abstract_factory;

public class OracleConexion extends Conexion{

  public OracleConexion(){}

  @Override
  public String descripcion() {
    return "Conexión oracle";
  }

}
```

```java
package abstract_factory;

public class SqlServerConexion extends Conexion {

  public SqlServerConexion(){}

  @Override
  public String descripcion() {
    return "Conexión SqlServer";
  }


}
```

```java
package abstract_factory;

public class MySqlConexion extends Conexion {

  public MySqlConexion(){}

  @Override
  public String descripcion() {
    return "Conexión MySql";
  }

}
```

---

```java
package abstract_factory;

public abstract class FabricaAbstracta {

  public FabricaAbstracta() {}

  protected abstract Conexion creaConexion (String tipo);
}
```

```java
package abstract_factory;

public class FabricaHeredada extends FabricaAbstracta{

  @Override
  protected Conexion creaConexion(String tipo) {

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
package abstract_factory;

import java.util.Scanner;

public class Pagos {

  public static void main(String[] args) {

    Scanner sc = new Scanner(System.in);
    FabricaHeredada miFabrica;
    Conexion miConexion;

    System.out.println("Digite la BD: ");
    String tipo = sc.nextLine();

    miFabrica = new FabricaHeredada();
    miConexion = miFabrica.creaConexion(tipo);

    String salida = "Esta conectado con: " +
            miConexion.descripcion();
    System.out.println(salida);

  }

}
```