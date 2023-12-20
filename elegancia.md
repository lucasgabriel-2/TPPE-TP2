# Trabalho prático 2

## Elegância

### Descrição
   A elegância no código é a busca por uma estrutura simples e clara que resulta em benefícios práticos. Códigos elegantes são mais fáceis de entender, têm baixa complexidade, promovem coesão entre partes, reduzem o acoplamento, facilitam a leitura e manutenção, permitem extensões eficientes, melhoram a legibilidade e aumentam a durabilidade do software. Essa abordagem não apenas torna o código esteticamente agradável, mas também contribui para sua eficiência e adaptabilidade ao longo do tempo, assim, facilitando também o trabalho dos desenvolvedores. 

### Relação da característica com os maus-cheiros de código definidos por Fowler

**Lista de parâmetros longa demais:**
Para se obter elegância no código é necessário simplicidade, porém longas listas de parâmetros tornam o código confuso. Substituir parâmetros por métodos, preservar objetos ou introduzir um objeto-parâmetro melhora a elegância, simplificando o código. Isso reduz a complexidade, promove coesão e facilita leitura e manutenção, contribuindo para adaptabilidade ao longo do tempo. Assim, a elegância torna o código claro e de fácil manutenção.


### Operação de Refatoração

**Introduzir um objeto-parâmetro:** para substituir um conjunto de dados que não estão logicamente relacionados por um objeto de dados.

``` JAVA
public class Calculadora {
   public double calcularPagamento(double valorHoras, double horasTrabalhadas, double taxaImposto, double descontos, double bonus) {
       double salarioBruto = valorHoras * horasTrabalhadas;
       double salarioLiquido = salarioBruto - (salarioBruto * taxaImposto) - descontos + bonus;
       return salarioLiquido;
   }


   public static void main(String[] args) {
       Calculadora calculadora = new Calculadora();
       double salarioFinal = calculadora.calcularPagamento(20, 160, 0.2, 50, 100);
       System.out.println("Salário Final: $" + salarioFinal);
   }
}
```

Após a refatoração:
```java
public class DadosPagamento {
   private double valorHoras;
   private double horasTrabalhadas;
   private double taxaImposto;
   private double descontos;
   private double bonus;


   public DadosPagamento(double valorHoras, double horasTrabalhadas, double taxaImposto, double descontos, double bonus) {
       this.valorHoras = valorHoras;
       this.horasTrabalhadas = horasTrabalhadas;
       this.taxaImposto = taxaImposto;
       this.descontos = descontos;
       this.bonus = bonus;
   }


  // métodos get e set
}


public class Calculadora {
   public double calcularPagamento(DadosPagamento dados) {
       double salarioBruto = dados.getValorHoras() * dados.getHorasTrabalhadas();
       double salarioLiquido = salarioBruto - (salarioBruto * dados.getTaxaImposto()) - dados.getDescontos() + dados.getBonus();
       return salarioLiquido;
   }


   public static void main(String[] args) {
       DadosPagamento dadosPagamento = new DadosPagamento(20, 160, 0.2, 50, 100);
       Calculadora calculadora = new Calculadora();
       double salarioFinal = calculadora.calcularPagamento(dadosPagamento);
       System.out.println("Salário Final: $" + salarioFinal);
   }
}
```

## Referências

[1] GOODLIFFE, P. Code Craft the practice of writing excellent code. ch. 1. Hanbit Media Inc, p. 3-22, 2007.