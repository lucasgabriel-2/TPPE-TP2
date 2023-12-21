# Trabalho prático 2

## Boas Interfaces

### Descrição
Os módulos nos ajudam a separar preocupações e dividir o problema. Cada módulo define uma interface, a fachada pública por trás da qual ele esconde uma implementação interna.
Uma boa interface é clara, bem definida e oferece acesso controlado às funcionalidades internas do módulo. Da mesma forma que um módulo bem projetado utiliza interfaces para expor sua funcionalidade, boas interfaces garantem uma interação eficiente e sem problemas entre diferentes partes de um sistema, promovendo a modularidade, legibilidade e facilidade de manutenção


### Relação da característica com os maus-cheiros de código definidos por Fowler

**Longa lista de parâmetros**: Interfaces eficientes são cruciais no design de software, atuando como fronteiras claras entre diferentes módulos, para isso longas listas de parâmetros em métodos são desaconselhadas, pois tornam o código difícil de entender e manter. Isso vai de encontro ao princípio de "compression" nas interfaces, que busca representar operações extensas de forma mais simples. Simplificar interfaces, substituindo parâmetros por métodos, Preservar o objeto inteiro ou introduzindo objetos, melhora a legibilidade e a estabilidade do código.

### Operação de Refatoração

**Introduzir objeto-parâmetro:**  substituir um
conjunto de dados que não estão logicamente
relacionados por um objeto de dados

``` JAVA
public interface ProductService {

    double calculateTotalPrice(String name, double price, int quantity, String category, String manufacturer, String description);

    void applyDiscount(String name, double price, int quantity, double discountPercentage, String category, String manufacturer, String description);

}
```

### Após a refatoração:

```java
public class ProductData {

    private String name;
    private double price;
    private int quantity;
    private String category;
    private String manufacturer;
    private String description;

    public ProductData(String name, double price, int quantity, String category, String manufacturer, String description) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
        this.category = category;
        this.manufacturer = manufacturer;
        this.description = description;
    }

    
}

public interface ProductService {

    double calculateTotalPrice(ProductData productData);

    void applyDiscount(ProductData productData, double discountPercentage);

    
}
```


## Outro exemplo (na linguagem typescript)


### Aplicação que recebe várias propriedades que podem ser passadas para uma interface

```typescript
const Card = (
 sign: boolean,
 ticker: string,
 price: number,
 porcentage: number,
 imgUrl?: string
) => {
 const urlImg =
   imgUrl === "https://brapi.dev/favicon.svg"
     ? "https://s3-symbol-logo.tradingview.com/itausa--big.svg"
     : imgUrl;


 return (
   <CardWrapper>
     <TitleWrapper sign={sign}>
       <p>
         <strong>{ticker}</strong>
       </p>
       <img src={urlImg} alt="{ticker}" />
     </TitleWrapper>


     <StockDataSection sign={sign}>
       <StockPrice price={price}></StockPrice>
       <Pill sign={porcentage > 0} porcentage={porcentage}></Pill>
     </StockDataSection>
   </CardWrapper>
 );
};

export { Card };
```


### Aplicando a interface que representa um card de uma ação.

```typescript
export interface ITicker {
  sign: boolean;
  ticker: string;
  price: number;
  porcentage: number;
  imgUrl?: string;
}

const Card = ({ ...props }: ITicker) => {
  const urlImg =
    props.imgUrl === "https://brapi.dev/favicon.svg"
      ? "https://s3-symbol-logo.tradingview.com/itausa--big.svg"
      : imgUrl;

  return (
    <CardWrapper>
      <TitleWrapper sign={props.sign}>
        <p>
          <strong>{props.ticker}</strong>
        </p>
        <img src={urlImg} alt="{ticker}" />
      </TitleWrapper>

      <StockDataSection sign={props.sign}>
        <StockPrice price={props.price}></StockPrice>
        <Pill sign={props.porcentage > 0} porcentage={props.porcentage}></Pill>
      </StockDataSection>
    </CardWrapper>
  );
};

export { Card };
```

## Referências

[1] GOODLIFFE, P. Code Craft the practice of writing excellent code. ch. 1. Hanbit Media Inc, p. 3-22, 2007.