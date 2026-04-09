# Estudo de Caso: Evolução do Tratamento de Exceções em Java

Este repositório documenta a evolução da lógica de tratamento de erros em um sistema de reservas, comparando diferentes abordagens e destacando por que o uso de exceções é o padrão da indústria.

---

## 🏗️ Solução 1: Lógica de validação no programa principal
Nesta primeira abordagem, as verificações de data e disponibilidade são feitas diretamente na classe onde o programa é executado (`main`).

* **Problema central:** A lógica de validação **não é delegada**.
* A classe que deveria ser responsável pela regra de negócio (como a classe `Reserva`) fica "passiva", enquanto o programa principal fica sobrecarregado com decisões que não deveriam ser dele.

---

## ⚠️ Solução 2: Método retornando String
Aqui, tentamos delegar a lógica para o método, mas ele sinaliza erros retornando uma mensagem de texto em vez de lançar um erro real.

* **Semântica da operação prejudicada:** * Retornar uma `String` não tem relação direta com a ação de atualizar uma reserva.
    * **Dilema de retorno:** E se a operação já tivesse que retornar uma `String` por padrão (ex: um ID ou nome)? Fica impossível distinguir sucesso de erro.
* **Limitação Técnica:** Não é possível tratar exceções em **construtores** usando este método.
* **Fragilidade:** Não há auxílio do compilador. O desenvolvedor deve "lembrar" de verificar se o retorno foi um erro após cada chamada de método.
* **Código Sujo:** A lógica de execução fica estruturada em diversas **condicionais aninhadas** (`if` dentro de `if`), dificultando a manutenção.

---

## ✅ Solução 3: Tratamento de Exceções (Modelo Ideal)
A solução definitiva que utiliza os recursos nativos do Java para garantir a robustez do sistema.

* **Try-Catch:** Separa a lógica de sucesso (bloco `try`) da lógica de erro (bloco `catch`).
* **Resiliência:** Permite que o programa se recupere de falhas ou pare a execução de forma controlada.
* **Clareza:** A semântica do código é preservada, e as regras de negócio ficam centralizadas na classe correspondente.

---