graph TD
    Start([Item Criado no Backlog]) --> ToDo[TO DO / A FAZER]
    
    ToDo --> InProgress[IN PROGRESS / EM DESENVOLVIMENTO]
    
    InProgress -- Impedimento Identificado --> Blocked[BLOCKED / BLOQUEADO]
    Blocked -- Impedimento Resolvido --> InProgress
    
    InProgress --> ReadyQA[READY FOR QA / PRONTO PARA TESTE]
    ReadyQA --> InTest{IN TEST / EM TESTE}

    InTest -- Teste Passou --> Done[DONE / CONCLUÍDO]
    InTest -- Defeito Encontrado --> NewBug[NEW / BUG IDENTIFICADO]

    subgraph Ciclo_de_Vida_do_Bug [Fluxo de Tratamento de Defeitos]
        NewBug --> Assigned[ASSIGNED / ATRIBUÍDO AO DEV]
        Assigned --> OpenBug[OPEN / EM CORREÇÃO]
        
        OpenBug -- Invalido / Duplicado --> ClosedBug[CLOSED / FECHADO]
        
        OpenBug --> Fixed[FIXED / CORRIGIDO]
        Fixed --> PendingRetest[PENDING RETEST / AGUARDANDO RE-TESTE]
        PendingRetest --> ReTest{RE-TEST / EXECUTANDO RETESTE}
        
        ReTest -- Falha Persiste --> ReOpened[REOPENED / REABERTO]
        ReOpened --> OpenBug
        
        ReTest -- Correção Validada --> Verified[VERIFIED / VERIFICADO]
        Verified --> ClosedBug
    end

    ClosedBug --> ToDo