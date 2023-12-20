# Trabalho prático 2

## Modularidade

### Descrição
   A Modularidade no design de software se baseia em duas características fundamentais: coesão e acoplamento. A coesão mede o quão bem as funcionalidades relacionadas estão agrupadas dentro de um módulo, formando uma unidade coesa. Módulos fortemente coesos mantêm uma funcionalidade clara e evitam tornar-se aglomerados de recursos não relacionados. 
   
   Por outro lado, o acoplamento refere-se à interdependência entre módulos. Projetos bem estruturados buscam alcançar um baixo acoplamento, reduzindo a dependência entre os módulos. Embora seja impossível ter módulos totalmente desacoplados, minimizar as ligações diretas e indiretas promove independência e facilita a manutenção.

### Relação da característica com os maus-cheiros de código definidos por Fowler

**Classe grande:** A Modularidade no design de software, baseada em coesão e acoplamento, está intrinsecamente ligada aos maus-cheiros de código descritos por Martin Fowler. Onde por exemplo uma "Classe Grande" indica baixa coesão e pode ser mitigada pela extração de classes ou subclasses, alinhando-se à busca por módulos coesos ao agrupar um número de variáveis
que juntas fazem mais sentido para o projeto.

### Operação de Refatoração

 **Extrair classe:** para agrupar um número de variáveis que juntas fazem algum sentido para o projeto.

``` JAVA
public class Pedido {
    private String clienteNome;
    private String clienteTelefone;
    private String enderecoRua;
    private String enderecoCidade;
    private String enderecoEstado;
    private String enderecoCEP;
    // ... outras variáveis relacionadas ao pedido

    public Pedido(String clienteNome, String clienteTelefone, String enderecoRua, String enderecoCidade,
                  String enderecoEstado, String enderecoCEP) {
        this.clienteNome = clienteNome;
        this.clienteTelefone = clienteTelefone;
        this.enderecoRua = enderecoRua;
        this.enderecoCidade = enderecoCidade;
        this.enderecoEstado = enderecoEstado;
        this.enderecoCEP = enderecoCEP;
        // ... inicialização de outras variáveis
    }

    // ... outros métodos relacionados ao pedido
}
```

Após a refatoração:
```java
public class Pedido {
    private String clienteNome;
    private String clienteTelefone;
    private Endereco endereco;
    // ... outras variáveis relacionadas ao pedido

    public Pedido(String clienteNome, String clienteTelefone, Endereco endereco) {
        this.clienteNome = clienteNome;
        this.clienteTelefone = clienteTelefone;
        this.endereco = endereco;
        // ... inicialização de outras variáveis
    }

    // ... outros métodos relacionados ao pedido
}

public class Endereco {
    private String rua;
    private String cidade;
    private String estado;
    private String cep;

    public Endereco(String rua, String cidade, String estado, String cep) {
        this.rua = rua;
        this.cidade = cidade;
        this.estado = estado;
        this.cep = cep;
    }

    // ... getters e setters
}
```

## Referências

[1] GOODLIFFE, P. Code Craft the practice of writing excellent code. ch. 1. Hanbit Media Inc, p. 3-22, 2007.