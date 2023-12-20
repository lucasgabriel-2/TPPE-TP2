# Trabalho prático 2

## Extensibilidade

### Descrição
   A extensibilidade refere-se à capacidade de adicionar funcionalidades de maneira eficiente sem comprometer a estrutura existente. A extensibilidade geralmente busca reduzir o acoplamento entre diferentes partes do sistema.

### Relação da característica com os maus-cheiros de código definidos por Fowler

**Classe grande:** A extensibilidade no desenvolvimento de software refere-se à capacidade de adicionar novas funcionalidades de maneira eficiente, sem comprometer a estrutura existente. Essa característica está intimamente ligada aos maus-cheiros de código identificados por Martin Fowler, especialmente no caso de classes grandes. Classes extensíveis evitam a armadilha de over-engineering e coesão baixa, promovendo um design que permite fácil adaptação e manutenção. Ao projetar para extensibilidade facilita-se a manutenção. Operações de refatoração sugeridas por Fowler, como extrair classe ou extrair subclasse, podem solucionar esse tipo de problema e ajudar na manutenção de um código mais limpo e modular.

### Operação de Refatoração

 **Extrair subclasse:** agrupar um número de variáveis
que fazem sentido como uma subclasse da classe em
que estão.

``` JAVA
public class ItemPedido {
    private String descricao;
    private double preco;
    private int quantidade;
    private boolean promocional;

    public ItemPedido(String descricao, double preco, int quantidade) {
        this.descricao = descricao;
        this.preco = preco;
        this.quantidade = quantidade;
        this.promocional = false;
    }

    public void calcularTotal() {
        
    }

    public void aplicarDesconto() {
        this.promocional = true;
    }


}

```

Após a refatoração:
```java
public class ItemPedido {
    private String descricao;
    private double preco;
    private int quantidade;

    public ItemPedido(String descricao, double preco, int quantidade) {
        this.descricao = descricao;
        this.preco = preco;
        this.quantidade = quantidade;
    }

    public void calcularTotal() {
        
    }
}

public class ItemPromocional extends ItemPedido {
    private boolean promocional;

    public ItemPromocional(String descricao, double preco, int quantidade) {
        super(descricao, preco, quantidade);
        this.promocional = false;
    }

    public void aplicarDesconto() {
        this.promocional = true;
    }
}

```

## Referências

[1] GOODLIFFE, P. Code Craft the practice of writing excellent code. ch. 1. Hanbit Media Inc, p. 3-22, 2007.