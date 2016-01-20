## Template method

```java
public abstract class CuentaBancaria{
  private String cuenta;
  private int saldo = 0;

  private void setCuenta(String c){
    this.cuenta = c;
  }

  private void consignar(int i){
    System.out.println("Consignando...");
    this.saldo += i;
  }

  private void retirar(int i){
    System.out.println("Retirando...");
    if(i<=this.saldo-10){
      this.saldo -= i;
    } else {
      System.out.println("No se puede retirar ese monto.");
    }
  }

  private void consultarSaldo(){
    System.out.println("El saldo es: "+this.saldo);
  }

  protected void auditoria(){
    System.out.println("Se ha procesado la cuenta: "+this.cuenta);
  }

  public abstract void saludar();

  public void procesar(String c, int i, int t){
    saludar();
    setCuenta(c);
    switch(t){
      case 1:
        consignar(i);
        break;
      case 2:
        retirar(i);
        break;
      default:
        System.out.println("Opcion no valida");
    }
    consultarSaldo();
    auditoria();
  }
}
```

```java
public class CajeroAutomatico extends CuentaBancaria{

  public CajeroAutomatico(String c, int i, int t){
    procesar(c,i,t);
  }

  @Override
  public void saludar(){
    System.out.println("Por favor ingrese los datos...");
  }
}
```

```java
public class Cajero extends CuentaBancaria{
  public Cajero(String c, int i, int t){
    procesar(c,i,t);
  }

  @Override
  public void auditoria(){
    super.auditoria();
    System.out.println("Con mucho gusto, vuelva pronto.");
  }

  @Override
  public void saludar(){
    System.out.println("Bienvenido a su banco, en que le puedo ayudar?");
  }
}
```

```java
public class PruebaPlantilla{
  public static void main(String... args){

    CajeroAutomatico ca = new CajeroAutomatico("F678AB", 30, 1);
    ca.procesar("F678AB",10,2);

    System.out.println();

    Cajero c = new Cajero("1234AB", 50, 1);
    c.procesar("1234AB",10,2);
  }
}
```