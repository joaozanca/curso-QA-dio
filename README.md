graph TD
    Start([Item Criado no Backlog]) --> Passo1[TO DO: Escrita de User Stories & Critérios de Aceite]
    Passo1 --> Passo2[IN PROGRESS: Planejamento da Sprint no Jira]
    Passo2 --> Passo3[READY FOR QA: Modelagem de Testes no Zephyr]
    
    Passo3 --> CT_Manual[Testes Passo a Passo]
    Passo3 --> CT_BDD[Testes em Gherkin / BDD]

    CT_Manual --> Execucao{IN TEST: Execução dos Testes}
    CT_BDD --> Execucao

    Execucao -- Teste Passou --> Evidencia[DONE: Anexar Evidências e Fechar Item]
    Execucao -- Teste Falhou --> NewBug[NEW: Bug Identificado]

    subgraph Ciclo_de_Vida_do_Bug [Fluxo de Tratamento de Defeitos]
        NewBug --> Assigned[ASSIGNED: Atribuído ao Dev]
        Assigned --> OpenBug[OPEN: Em Correção pelo Dev]
        
        OpenBug --> Fixed[FIXED: Correção do Código Concluída]
        Fixed --> PendingRetest[PENDING RETEST: Aguardando Re-teste]
        PendingRetest --> ReTest{RE-TEST: Executando Reteste}
        
        ReTest -- Falha Persiste --> ReOpened[REOPENED: Bug Reaberto]
        ReOpened --> OpenBug
        
        ReTest -- Correção Validada --> Verified[VERIFIED: Correção Verificada]
        Verified --> ClosedBug[CLOSED: Bug Fechado]
    end

    Evidencia --> PDF_Export[Passo 4: Exportação de Relatórios em PDF]
    ClosedBug --> PDF_Export
    PDF_Export --> End([Fim: Entrega do Repositório no GitHub])