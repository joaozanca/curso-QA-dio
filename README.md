```mermaid
graph TD %% Estilos de Cores
    classDef inicio e fim fill:#F39C12,stroke:#333,stroke-width:2px,color:#fff;
    classDef processo fill:#3498DB,stroke:#2980B9,stroke-width:1px,color:#fff;
    classDef decisao fill:#F1C40F,stroke:#D68910,stroke-width:1px,color:#333;
    classDef bug fill:#E74C3C,stroke:#C0392B,stroke-width:2px,color:#fff;
    classDef sucesso fill:#2ECC71,stroke:#27AE60,stroke-width:2px,color:#fff;

    Start([Item Criado no Backlog]) --> Passo1[TO DO: Escrita de User Stories & Critérios de Aceite]
    Passo1 --> Passo2[IN PROGRESS: Planejamento da Sprint no Jira]
    Passo2 --> Passo3[READY FOR QA: Modelagem de Testes no Zephyr]
    
    subgraph Zephyr_Design [Abordagens de Teste Criadas]
        Passo3 --> CT_Manual[Testes Passo a Passo]
        Passo3 --> CT_BDD[Testes em Gherkin / BDD]
    end

    CT_Manual & CT_BDD --> Execucao{IN TEST: Execução dos Testes}

    Execucao -- Teste Passou --> Evidencia[DONE: Anexar Evidências e Fechar Item]
    Execucao -- Teste Falhou --> NewBug[NEW: Bug Identificado]

    subgraph Ciclo_de_Vida_do_Bug [Fluxo de Tratamento de Defeitos]
        NewBug --> Assigned[ASSIGNED: Atribuído ao Dev]
        Assigned --> OpenBug[OPEN: Em Correção pelo Dev]
        
        OpenBug -- Invalido / Duplicado --> ClosedBug[CLOSED: Bug Fechado]
        
        OpenBug --> Fixed[FIXED: Correção do Código Concluída]
        Fixed --> PendingRetest[PENDING RETEST: Aguardando Re-teste]
        PendingRetest --> ReTest{RE-TEST: Executando Reteste}
        
        ReTest -- Falha Persiste --> ReOpened[REOPENED: Bug Reaberto]
        ReOpened --> OpenBug
        
        ReTest -- Correção Validada --> Verified[VERIFIED: Correção Verificada]
        Verified --> ClosedBug
    end

    Evidencia --> PDF_Export[Passo 4: Exportação de Relatórios em PDF]
    ClosedBug --> PDF_Export
    PDF_Export --> End([Fim: Entrega do Repositório no GitHub])

    class Start,End inicio;
    class Passo1,ReOpened,NewBug,ClosedBug bug;
    class Passo2,OpenBug,Assigned,Fixed processo;
    class Passo3,CT_Manual,CT_BDD,PendingRetest,Verified sucesso;
    class Execucao,ReTest decisao;