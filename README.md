graph TD
    %% Estilos de Cores para Status do Jira
    classDef inicial fill:#7F8C8D,stroke:#333,stroke-width:2px,color:#fff;
    classDef todo fill:#2980B9,stroke:#1F618D,stroke-width:1px,color:#fff;
    classDef inprogress fill:#F39C12,stroke:#B9770E,stroke-width:1px,color:#fff;
    classDef qa fill:#9B59B6,stroke:#6C3483,stroke-width:1px,color:#fff;
    classDef bug fill:#E74C3C,stroke:#C0392B,stroke-width:1px,color:#fff;
    classDef concluido fill:#2ECC71,stroke:#1D8348,stroke-width:2px,color:#fff;

    %% Fluxo de Trabalho Principal (User Story / Task)
    Start([Item Criado no Backlog]) --> ToDo[TO DO / A FAZER]
    
    ToDo --> InProgress[IN PROGRESS / EM DESENVOLVIMENTO]
    
    %% Condição de Bloqueio no Desenvolvimento
    InProgress -- Impedimento Identificado --> Blocked[BLOCKED / BLOQUEADO]
    Blocked -- Impedimento Resolvido --> InProgress
    
    InProgress --> ReadyQA[READY FOR QA / PRONTO PARA TESTE]

    %% Transição para a Esteira de Testes
    ReadyQA --> InTest{IN TEST / EM TESTE}

    %% Ramificação de Resultados do Teste
    InTest -- Teste Passou --> Done[DONE / CONCLUÍDO]
    InTest -- Defeito Encontrado (Bug) --> NewBug[NEW / BUG IDENTIFICADO]

    %% Sub-fluxo: Ciclo de Vida do Bug (Bug/Defect Lifecycle)
    subgraph Ciclo_de_Vida_do_Bug [Fluxo de Tratamento de Defeitos]
        NewBug --> Assigned[ASSIGNED / ATRIBUÍDO AO DEV]
        Assigned --> OpenBug[OPEN / EM CORREÇÃO]
        
        %% Validações de descarte de Bug
        OpenBug -- Invalido / Duplicado / Nao Reprodutivel --> ClosedBug[CLOSED / FECHADO]
        
        OpenBug --> Fixed[FIXED / CORRIGIDO]
        Fixed --> PendingRetest[PENDING RETEST / AGUARDANDO RE-TESTE]
        PendingRetest --> ReTest{RE-TEST / EXECUTANDO RETESTE}
        
        %% Decisões do Re-teste
        ReTest -- Falha Persiste --> ReOpened[REOPENED / REABERTO]
        ReOpened --> OpenBug
        
        ReTest -- Correção Validada --> Verified[VERIFIED / VERIFICADO]
        Verified --> ClosedBug
    end

    %% Retorno do Bug Fechado para o Fluxo Principal
    ClosedBug --> ToDo

    %% Aplicação de Classes aos Elementos
    class Start inicial;
    class ToDo,ReOpened todo;
    class InProgress,OpenBug,Assigned,Fixed inprogress;
    class ReadyQA,InTest,PendingRetest,ReTest,Verified qa;
    class Blocked,NewBug bug;
    class Done,ClosedBug concluido;