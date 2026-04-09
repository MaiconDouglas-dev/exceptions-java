Resumo

Solução 1: Lógica de validação no programa principal.
    Lógica de validação não delegada.
Solução 2: Método retornando string.
    Semântica da operação prejudicada.
        Retornar string não tem nada a ver com atualização de reserva.
        E se a operação tivesse que retornar, string ?
    Não é possível tratar exceções em construtores.
    Não há auxílio do complilador: o programa deve "lembrar" de verificar se houve erro.
    Lógica fica estruturada em condicionais aninhadas.
Solução 3: Tratamento de exceções.