graph TD
    %% Estilos de Cores para Status do Jira
    classDef inicial fill:#7F8C8D,stroke:#333,stroke-width:2px,color:#fff;
    classDef todo fill:#2980B9,stroke:#1F618D,stroke-width:1px,color:#fff;
    classDef inprogress fill:#F39C12,stroke:#B9770E,stroke-width:1px,color:#fff;
    classDef qa fill:#9B59B6,stroke:#6C3483,stroke-width:1px,color:#fff;
    classDef bug fill:#E74C3C,stroke:#C0392B,stroke-width:1px,color:#fff;
    classDef concluido fill:#2ECC71,stroke:#1D8348,stroke-width:2px,color:#fff;

    %% Fluxo Principal (Ciclo do Projeto com Status Técnicos)
    Start([Item Criado no Backlog]) --> Passo1[TO DO: Escrita de User Stories & Critérios de Aceite]
    Passo1 --> Passo2[IN PROGRESS: Planejamento da Sprint no Jira]
    Passo2 --> Passo3[READY FOR QA: Modelagem de Testes no Zephyr]
    
    subgraph Zephyr_Design [Abordagens de Teste Criadas]
        Passo3 --> CT_Manual[Testes Passo a Passo]
        Passo3 --> CT_BDD[Testes em Gherkin / BDD]
    end

    CT_Manual & CT_BDD --> Execucao{IN TEST: Execução dos Testes}

    %% Condicional de Sucesso ou Bug
    Execucao -- Teste Passou --> Evidencia[DONE: Anexar Evidências e Fechar Item]
    Execucao -- Teste Falhou --> NewBug[NEW: Bug Identificado]

    %% Sub-fluxo: Ciclo de Vida do Bug (Status Técnicos)
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

    %% Finalização
    Evidencia --> PDF_Export[Passo 4: Exportação de Relatórios em PDF]
    ClosedBug --> PDF_Export
    PDF_Export --> End([Fim: Entrega do Repositório no GitHub])

    %% Aplicação de Classes aos Elementos
    class Start,End inicial;
    class Passo1,ReOpened todo;
    class Passo2,OpenBug,Assigned,Fixed inprogress;
    class Passo3,CT_Manual,CT_BDD,Execucao,PendingRetest,ReTest,Verified qa;
    class NewBug bug;
    class Evidencia,PDF_Export,ClosedBug concluido;