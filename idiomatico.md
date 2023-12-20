# Trabalho prático 2

## "Idiomático" (idioma da linguagem)

### Descrição

 Um projeto bem estruturado adota as melhores práticas e se alinha às convenções e expressões idiomáticas da linguagem escolhida. Isso garante que outros desenvolvedores possam compreender a estrutura do código em pouco tempo, além de melhorar a coesão do código.

### Relação da característica com os maus-cheiros de código definidos por Fowler

**Código duplicado:** Eliminar código duplicado é essencial para desenvolver um código idiomático, alinhado às práticas e convenções específicas da linguagem escolhida. Isso não apenas aprimora a eficiência do código, mas também facilita a compreensão por parte de outros desenvolvedores. Ao adotar as expressões idiomáticas da linguagem, o código se torna mais coeso e alinhado às melhores práticas, contribuindo para a clareza e legibilidade do projeto.

### Operação de Refatoração

**Extrair método:** quando a mesma expressão encontra-se
em dois métodos na mesma classe

``` JAVA
import java.util.Arrays;
import java.util.List;

public class Principal {

    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Cálculo da soma dos números pares
        int somaPares = calcularSomaPares(numeros);
        System.out.println("Soma dos números pares: " + somaPares);

        // Cálculo da soma dos números ímpares
        int somaImpares = calcularSomaImpares(numeros);
        System.out.println("Soma dos números ímpares: " + somaImpares);
    }

    private static int calcularSomaPares(List<Integer> numeros) {
        int somaPares = 0;
        for (int numero : numeros) {
            if (numero % 2 == 0) {
                somaPares += numero;
            }
        }
        return somaPares;
    }

    private static int calcularSomaImpares(List<Integer> numeros) {
        int somaImpares = 0;
        for (int numero : numeros) {
            if (numero % 2 != 0) {
                somaImpares += numero;
            }
        }
        return somaImpares;
    }
}

```

Após a refatoração:
```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class Principal{

    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Cálculo da soma para pares e ímpares em um único Stream
        Map<Boolean, Integer> somaPorParidade = calcularSomaPorParidade(numeros);

        System.out.println("Soma dos números pares: " + somaPorParidade.get(true));
        System.out.println("Soma dos números ímpares: " + somaPorParidade.get(false));
    }

    private static Map<Boolean, Integer> calcularSomaPorParidade(List<Integer> numeros) {
        return numeros.stream()
                .collect(Collectors.partitioningBy(numero -> numero % 2 == 0,
                        Collectors.summingInt(Integer::intValue)));
    }
}

```

## Referências

[1] GOODLIFFE, P. Code Craft the practice of writing excellent code. ch. 1. Hanbit Media Inc, p. 3-22, 2007.

