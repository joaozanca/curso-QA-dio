# 🏥 Projeto de Gerenciamento de Testes - Plataforma de Telemedicina

Desafio de projeto focado no mapeamento de requisitos, garantia de qualidade (QA) e estruturação de testes para um ecossistema de saúde, simulando o cenário real de desenvolvimento de uma plataforma de Telemedicina.

---

## 🛠️ Ferramentas e Metodologia

* **Jira:** Gerenciamento do projeto utilizando a metodologia ágil **Scrum** (Organização do Backlog e acompanhamento de itens através de Sprints).
* **Confluence:** Centralização da documentação e escrita das User Stories.
* **Zephyr Scale:** Criação, organização em pastas e estruturação dos Casos de Teste (CTs).

---

## 📂 Estrutura do Repositório e Artefatos

Os documentos oficiais gerados durante as etapas do desafio estão organizados na pasta raiz deste repositório:

* 📄 **`documentacao-de-requisitos-dio.pdf`**: Contém o mapeamento completo das User Stories, regras de negócio e critérios de aceite estruturados no Confluence.
* 📄 **`plano-de-testes-zephyr.pdf`**: Relatório contendo todos os Casos de Teste detalhados, cobrindo os formatos *Step-by-Step* (Passo a Passo) e cenários escritos em *BDD (Gherkin)*.
* 📸 **`print_quadro_sprint_jira.png`**: Captura de tela do quadro da Sprint Ativa no Jira, demonstrando o fluxo de trabalho dos cards.

---

## 📝 Escopo dos Testes Mapeados

### 🧪 Casos de Teste: Passo a Passo (Step-by-Step)
1. **Validar bloqueio de conta após 5 tentativas inválidas consecutivas**: Garante a segurança de acesso dos profissionais de saúde bloqueando o login suspeito.
2. **Validar encerramento de sessão após 5 minutos de ociosidade**: Garante o sigilo médico desconectando sessões inativas automaticamente.

### 🥒 Casos de Teste: BDD (Gherkin)
1. **Validar restrição de login com e-mail pessoal**: Cenário híbrido (palavras-chave em inglês e texto em português) validando o bloqueio de e-mails corporativos inválidos.
2. **Cancelamento de consulta antes de 24 horas de antecedência**: Validação de regra de negócio para cancelamento autônomo por parte do paciente sem cobrança de taxas.

---

## 🚀 Como Visualizar os Resultados

1. Acesse os arquivos PDF listados no repositório para conferir a formatação oficial exportada do ecossistema Atlassian.
2. Os critérios de aceite em BDD foram validados seguindo as restrições de sintaxe do interpretador nativo do Zephyr Scale (omitindo as tags de cabeçalho `Feature` e `Scenario` conforme especificação técnica da ferramenta).

---

## 🗺️ Fluxograma de Engenharia: Fluxos e Status de Trabalho (Workflow)

O diagrama abaixo mapeia a esteira técnica de estados de uma tarefa dentro de um ciclo de desenvolvimento ágil, detalhando o comportamento padrão de um item de Backlog e as ramificações de transição de um defeito (Bug/Defect Life Cycle).

```mermaid
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

💻 Autor
👋 Desenvolvido por joaozanca durante a Formação de Automação de Testes.