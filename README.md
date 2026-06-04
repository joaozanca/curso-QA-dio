```mermaid
graph TD
    Start([Item Criado no Backlog]) --> Passo1[TO DO:<br>Escrita de User Stories &<br>Critérios de Aceite]
    Passo1 --> Passo2[IN PROGRESS:<br>Planejamento da Sprint no Jira]
    Passo2 --> Passo3[READY FOR QA:<br>Modelagem de Testes no Zephyr]
    
    subgraph Zephyr_Design [Abordagens de Teste Criadas]
        Passo3 --> CT_Manual[Testes Passo a Passo]
        Passo3 --> CT_BDD[Testes em Gherkin / BDD]
    end

    CT_Manual --> Execucao{IN TEST:<br>Execução dos Testes}
    CT_BDD --> Execucao

    Execucao -- Teste Passou --> Evidencia[DONE:<br>Anexar Evidências e Fechar Item]
    Execucao -- Teste Falhou --> NewBug[NEW:<br>Bug Identificado]

    subgraph Ciclo_de_Vida_do_Bug [Fluxo de Tratamento de Defeitos]
        NewBug --> Assigned[ASSIGNED:<br>Atribuído ao Dev]
        Assigned --> OpenBug[OPEN:<br>Em Correção pelo Dev]
        
        OpenBug -- Invalido / Duplicado --> ClosedBug[CLOSED:<br>Bug Fechado]
        
        OpenBug --> Fixed[FIXED:<br>Correção do Código Concluída]
        Fixed --> PendingRetest[PENDING RETEST:<br>Aguardando Re-teste]
        PendingRetest --> ReTest{RE-TEST:<br>Executando Reteste}
        
        ReTest -- Falha Persiste --> ReOpened[REOPENED:<br>Bug Reaberto]
        ReOpened --> OpenBug
        
        ReTest -- Correção Validada --> Verified[VERIFIED:<br>Correção Verificada]
        Verified --> ClosedBug
    end

    Evidencia --> Deploy[Deploy em Produção:<br>Liberação da Feature]
    ClosedBug --> Deploy
    Deploy --> End([Fim: Funcionalidade Online<br>& Monitorada])