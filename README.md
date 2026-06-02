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

* 📄 **`user-stories.pdf`**: Contém o mapeamento completo das User Stories, regras de negócio e critérios de aceite estruturados no Confluence.
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

## 🗺️ Fluxograma do Projeto e Ciclo de Vida do Bug

O diagrama abaixo representa o fluxo de trabalho ponta a ponta adotado no projeto, integrando o mapeamento de requisitos, a gestão de testes no Jira/Zephyr e o fluxo de tratamento de defeitos (Bugs).

```mermaid
graph TD
    %% Estilos de Cores
    classDef inicio e fim fill:#F39C12,stroke:#333,stroke-width:2px,color:#fff;
    classDef processo fill:#3498DB,stroke:#2980B9,stroke-width:1px,color:#fff;
    classDef decisao fill:#F1C40F,stroke:#D68910,stroke-width:1px,color:#333;
    classDef bug fill:#E74C3C,stroke:#C0392B,stroke-width:2px,color:#fff;
    classDef sucesso fill:#2ECC71,stroke:#27AE60,stroke-width:2px,color:#fff;

    %% Fluxo Principal (Ciclo do Projeto)
    Start([Início: Requisitos da Telemedicina]) --> Passo1[Passo 1: Escrita de User Stories & Critérios de Aceite no Confluence]
    Passo1 --> Passo2[Passo 2: Planejamento no Jira - Criação do Backlog da Sprint]
    Passo2 --> Passo3[Passo 3: Modelagem de Testes no Zephyr Scale]
    
    subgraph Zephyr_Design [Abordagens de Teste Criadas]
        Passo3 --> CT_Manual[Testes Passo a Passo / Step-by-Step]
        Passo3 --> CT_BDD[Testes em Gherkin / BDD]
    end

    CT_Manual & CT_BDD --> Execucao{Execução dos Testes}

    %% Condicional de Sucesso ou Bug
    Execucao -- Teste Passou (Pass) --> Evidencia[Anexar Evidências e Fechar CT]
    Execucao -- Teste Falhou (Fail) --> CicloBug

    %% Sub-fluxo: Ciclo de Vida do Bug
    subgraph CicloBug [Fluxo de Gerenciamento de Defeitos]
        B1[1. Identificar Falha] --> B2[2. Abrir Card de Bug no Jira]
        B2 --> B3[3. Priorizar e Atribuir ao Desenvolvedor]
        B3 --> B4[4. Correção do Código pelo Dev]
        B4 --> B5{5.