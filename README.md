# Demonstração de Perda de Precisão de Números Reais em Java

## Descrição

Este programa demonstra uma característica dos números de ponto flutuante em Java: a perda de precisão ao representar números inteiros muito grandes utilizando o tipo `double`.

O exemplo utiliza o valor `9007199254740992.0`, correspondente a \(2^{53}\). A partir desse valor, o tipo `double` não consegue representar todos os números inteiros consecutivos.

Por isso, ao somar `1` ao número armazenado, o resultado pode permanecer igual ao valor anterior, mesmo que a operação tenha sido executada.

## Objetivos

- Compreender os limites de precisão do tipo `double`.
- Demonstrar que a representação de números em ponto flutuante possui precisão finita.
- Observar por que somar `1` nem sempre altera o valor armazenado.
- Relacionar o comportamento ao padrão IEEE 754.
- Diferenciar a faixa de valores representáveis da precisão numérica.

## Funcionamento do programa

O programa realiza três etapas:

1. **Exibe o valor inicial:** a variável `numero` recebe `9007199254740992.0`, equivalente a \(2^{53}\).
2. **Soma 1 ao valor:** o programa executa `numero = numero + 1`. O resultado exibido permanece igual ao valor inicial, pois o `double` não consegue representar o inteiro seguinte de forma distinta nessa magnitude.
3. **Soma mais 2 ao valor armazenado:** o programa executa `numero = numero + 2`. O resultado passa para o próximo valor representável nessa região, que é `9007199254740994.0`.

## Código-fonte

O arquivo `Principal.java` contém a implementação do programa.

## Como executar

É necessário ter o Java Development Kit (JDK) instalado.

**1. Compile o programa:**

```bash
javac Principal.java
```

**2. Execute o programa:**

```bash
java Principal
```

## Saída esperada

```text
Numero            = 9.007199254740992E15
Numero + 1        = 9.007199254740992E15
Depois de somar 2 = 9.007199254740994E15
```

O Java utiliza notação científica para exibir números muito grandes. Por exemplo, `9.007199254740992E15` representa \(9{,}007199254740992 \times 10^{15}\).

## Conceito fundamental: precisão do double

O tipo `double` utiliza 64 bits conforme o padrão IEEE 754:

- 1 bit para o sinal;
- 11 bits para o expoente;
- 52 bits armazenados para a parte fracionária do significando, com um bit implícito nos números normalizados.

Esse formato oferece aproximadamente 15 a 17 algarismos decimais significativos.

Embora o `double` consiga representar números de magnitude muito elevada, ele não consegue representar todos os inteiros consecutivos nessa faixa.

A partir de \(2^{53}\), o espaçamento entre valores consecutivos representáveis passa a ser de 2. Por isso, o número \(2^{53}+1\) não possui uma representação distinta em `double` e é arredondado para um dos valores vizinhos representáveis.

Neste exemplo, somar `1` não altera o valor armazenado. Somar `2` permite alcançar o próximo valor representável.

## Precisão não é o mesmo que overflow

É importante diferenciar dois conceitos:

- **Perda de precisão:** ocorre quando o tipo não consegue distinguir ou representar exatamente determinados valores.
- **Overflow:** ocorre quando o resultado ultrapassa a faixa de valores finitos que o tipo consegue representar.

Neste programa, ocorre perda de precisão, não overflow. O resultado continua dentro da faixa finita do tipo `double`.

## Conclusão

O exemplo demonstra que o tipo `double` possui uma faixa de representação muito ampla, mas sua precisão é limitada.

Em aplicações que exigem cálculos exatos com números inteiros muito grandes, pode ser mais apropriado utilizar `long`, desde que os valores estejam dentro de sua faixa, ou `BigInteger` quando for necessário trabalhar com inteiros arbitrariamente grandes.

Compreender essa diferença ajuda a evitar erros em cálculos científicos, financeiros e em sistemas que manipulam grandes quantidades numéricas.