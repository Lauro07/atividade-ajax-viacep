# Atividade sobre AJAX (Asynchronous JavaScript And Xml)

Este repositório contém diferentes implementações de uma consulta à API [ViaCEP](https://viacep.com.br/) para demonstrar e comparar métodos de chamadas assíncronas em JavaScript.

## 1. Pesquisa Comparativa: XMLHttpRequest, fetch, Promises e async/await

### XMLHttpRequest (XHR)

* **O que é?** É a API original, presente nos navegadores há muitos anos, que permite fazer requisições HTTP para um servidor.
* **Como funciona?** É baseada em eventos e *callbacks*. Você instancia um objeto (`new XMLHttpRequest()`), define uma função de *callback* (`onreadystatechange`) para ouvir as mudanças de estado da requisição e, finalmente, abre (`.open()`) e envia (`.send()`) a requisição.
* **Vantagens:** Compatibilidade com navegadores muito antigos.
* **Desvantagens:** Sintaxe verbosa e complexa. O gerenciamento de *callbacks* pode se tornar confuso, levando ao "callback hell" (aninhamento excessivo de funções).

### Fetch API

* **O que é?** É a interface moderna e substituta do `XMLHttpRequest` para fazer requisições de rede.
* **Como funciona?** É baseada em `Promises`, o que simplifica o tratamento de respostas assíncronas. Uma chamada `fetch()` retorna uma `Promise` que resolve para o objeto `Response` assim que o servidor responde (com cabeçalhos).
* **Vantagens:** Sintaxe muito mais limpa e legível. Gerenciamento de erros mais fácil através do `.catch()`. API mais flexível e poderosa (ex: lidar com cabeçalhos, cache, etc.).
* **Desvantagens:** Requer dois passos para obter o JSON (o primeiro `fetch()` retorna a resposta HTTP, e então é preciso chamar `.json()` que também retorna uma `Promise`). Além disso, o `fetch` não rejeita a *Promise* em caso de erros HTTP (como 404 ou 500); ele só rejeita em falhas de rede.

### Promises

* **O que é?** Não é um *método* de requisição, mas sim um *padrão* (e um objeto) para lidar com operações assíncronas. O `fetch` *usa* Promises.
* **Como funciona?** Uma `Promise` é um objeto que representa a eventual conclusão (ou falha) de uma operação assíncrona. Ela pode estar em um de três estados: *pending* (pendente), *fulfilled* (realizada/sucesso) ou *rejected* (rejeitada/falha).
* **Vantagens:** Permite encadear operações (`.then()`) de forma legível e centralizar o tratamento de erros (`.catch()`), evitando o "callback hell".
* **Desvantagens:** A sintaxe de encadeamento (`.then().then()...`) ainda pode se tornar verbosa em casos complexos.

### Async/Await

* **O que é?** É uma "açúcar sintático" (syntactic sugar) construído *em cima* das `Promises`. Não é uma tecnologia nova, mas sim uma nova forma de *escrever* código que usa `Promises`.
* **Como funciona?** Permite escrever código assíncrono que se parece e se comporta como código síncrono.
    * A palavra-chave `async` é usada para declarar uma função que lidará com operações assíncronas.
    * A palavra-chave `await` é usada *dentro* de uma função `async` para pausar a execução da função até que a `Promise` seja resolvida.
* **Vantagens:** Torna o código extremamente legível e fácil de manter. O tratamento de erros é feito com blocos `try...catch`, que são familiares para a maioria dos desenvolvedores.
* **Desvantagens:** Requer que a função seja declarada como `async`. É preciso ter cuidado para não usar `await` de forma que bloqueie operações que poderiam rodar em paralelo.

---

## 2. Comparação de Desempenho e Facilidade de Uso

### Facilidade de Uso (Do mais difícil ao mais fácil)

1.  **`XMLHttpRequest`:** É o mais difícil. A sintaxe é verbosa, exige configuração manual do `onreadystatechange` e o tratamento de estados (readyState 0 a 4) é complexo e propenso a erros.
2.  **`fetch` com `.then/.catch` (Promises):** Muito mais fácil que o XHR. A lógica de "faça isso, *então* faça aquilo" é intuitiva. O `.catch()` centraliza os erros.
3.  **`fetch` com `async/await`:** É considerado o mais fácil e legível. O código flui de cima para baixo, como um script síncrono, e o `try...catch` é um padrão de tratamento de erro muito conhecido.

### Desempenho

Em termos de *velocidade da requisição de rede*, não há diferença prática perceptível entre os métodos. O tempo de ida e vinda ao servidor (latência) será o mesmo.

A diferença está na *eficiência do código* e na *experiência do desenvolvedor*:
* **`async/await`** e **`fetch`** são implementações nativas modernas e otimizadas pelos navegadores.
* O principal ganho não é em milissegundos de rede, mas em **produtividade**, **manutenibilidade** e **redução de bugs**, onde `async/await` é o vencedor claro.

## 3. Códigos da Atividade

* [ajax-xhr.html](./ajax-xhr.html) - (Implementação original com XMLHttpRequest)
* [ajax-fetch-promise.html](./ajax-fetch-promise.html) - (Implementação com fetch e .then/.catch)
* [ajax-fetch-async-await.html](./ajax-fetch-async-await.html) - (Implementação com fetch e async/await)