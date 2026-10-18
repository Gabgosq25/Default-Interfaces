<h1 align="center">
  🚀 Java Default Methods: Cálculo de Juros
</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white" alt="Java"/>
  <img src="https://img.shields.io/badge/IntelliJ_IDEA-000000.svg?style=for-the-badge&logo=intellij-idea&logoColor=white" alt="IntelliJ IDEA"/>
  <img src="https://img.shields.io/badge/Clean_Code-222222?style=for-the-badge&logo=dev.to&logoColor=white" alt="Clean Code"/>
</p>

<p align="center">
  Um projeto prático demonstrando o uso de <b>Default Methods</b> em Interfaces Java, focado na reutilização de regras de negócio (cálculo de juros compostos) sem acoplamento.
</p>

<hr>

## 📋 Sobre o Projeto

Este repositório contém um sistema de cálculo de juros compostos que simula empréstimos ou financiamentos. O objetivo principal não é apenas a matemática financeira, mas sim a **arquitetura do código**. 

O projeto explora a funcionalidade de `default methods` (introduzida no Java 8), que permite que interfaces forneçam uma implementação padrão para métodos. Isso resolve um problema clássico da Orientação a Objetos: como compartilhar lógica comum entre classes que não devem ou não podem herdar da mesma superclasse.

---

## ✨ Funcionalidades em Destaque

- 🏛️ **Design Patterns:** Uso inteligente de Interfaces para estabelecer contratos de serviços financeiros.
- ♻️ **Reutilização de Código:** A fórmula de juros compostos é escrita apenas uma vez na interface, sendo herdada gratuitamente pelos serviços do Brasil e dos EUA.
- 🛡️ **Programação Defensiva:** Validação de dados de entrada lançando `InvalidParameterException` caso a quantidade de meses seja menor que 1.
- 🔀 **Polimorfismo:** A classe principal interage apenas com a interface `InterestService`, ignorando os detalhes de implementação das classes concretas.

---

## 🏗️ Estrutura do Código

```text
📦 src
 ┣ 📂 application
 ┃ ┗ 📜 Program.java                 # Ponto de entrada (Main), responsável pela interação com o utilizador.
 ┗ 📂 services
   ┣ 📜 InterestService.java         # Interface contendo o Default Method com a lógica financeira.
   ┣ 📜 BrazilInterestService.java   # Implementação específica para taxas do Brasil.
   ┗ 📜 UsaInterestService.java      # Implementação específica para taxas dos Estados Unidos.
```

---

## 🔍 Entendendo a Mágica (Default Methods)

Em versões mais antigas do Java, as interfaces só podiam conter assinaturas de métodos abstratos. Se a fórmula de juros fosse igual para o Brasil e para os EUA, teríamos de repetir o código em ambas as classes ou criar uma classe abstrata (o que limita a flexibilidade, pois o Java não suporta herança múltipla).

Com os **Default Methods**, resolvemos isso diretamente na interface:

```java
public interface InterestService {

    // Método abstrato: cada país define a sua própria taxa.
    double getInterestRate();

    // Default Method: a fórmula matemática é a mesma para todos, então já fica implementada aqui!
    default double payment(double amount, int months) {
        if (months < 1) {
            throw new InvalidParameterException("Months must be greater than zero");
        }
        return amount * Math.pow(1.0 + getInterestRate() / 100.0, months);
    }
}
```

Isso garante um código incrivelmente enxuto nas classes `BrazilInterestService` e `UsaInterestService`, aplicando na perfeição o princípio **DRY (Don't Repeat Yourself)** do Clean Code.

---

## 🚀 Como Executar na Sua Máquina

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/Gabgosq25/Default-Interfaces.git
   ```
2. **Abra o projeto:**
   Abra o projeto na sua IDE favorita (IntelliJ IDEA, Eclipse, etc).
3. **Rode a aplicação:**
   Navegue até `application/Program.java` e execute o método `main`.
4. **Interação:**
   O terminal pedirá o valor do empréstimo (`Amount`) e a duração em meses (`Months`). O programa processará o cálculo instanciando o serviço desejado e exibirá o montante final formatado.

---

<p align="center">
  <i>Projeto desenvolvido como exercício prático do curso de Java do professor Nélio Alves, estruturado e documentado para consolidar os conhecimentos em Arquitetura de Software e Boas Práticas. ☕</i>
</p>