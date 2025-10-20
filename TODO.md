TODO.md

# Lista de Tarefas para o MokaCode CLI

Este documento serve como uma lista de tarefas e melhorias contínuas para o MokaCode CLI, baseada em uma autoanálise das minhas capacidades e do meu propósito como assistente especializado em Godot.

## 1. Tarefas de Documentação e Base de Conhecimento (PRIORIDADE MÁXIMA)

*   **1.1. Expansão e Aprofundamento dos Manuais Técnicos Existentes (QUALIDADE DE EBOOK):**
    *   **Revisar e expandir *todos* os manuais existentes** (`C++.md`, `GDExtension.md`, `ROP.md`, `Classes.md`, `GDShader.md`, `PDD.md`, `NetworkingAndInfrastructure.md`) para garantir que atinjam a profundidade, densidade e o volume mínimo de **6.000 palavras (aproximadamente 50 páginas)**, conforme o padrão estabelecido pelo `GDScript.md` e a filosofia de treinamento.
    *   Para cada documento, incluir:
        *   **Contexto Prático:** Como e por que usar cada conceito em cenários reais de desenvolvimento.
        *   **Melhores Práticas:** Dicas de performance, organização e padrões de design.
        *   **Exemplos Detalhados:** Trechos de código em GDScript e C++ (GDExtension) que ilustram o uso de propriedades, métodos e sinais, com explicações aprofundadas.
        *   **Relações e Interconexões:** Como as diferentes classes/conceitos se comunicam e se encaixam na arquitetura geral da Godot.
        *   **Considerações de Performance e Otimização:** Análise detalhada de como as escolhas de design e implementação afetam o desempenho.
        *   **Armadilhas Comuns e Debugging:** Alertas sobre erros frequentes e como usar as ferramentas de depuração.
        *   **Estrutura Didática:** Organização lógica e progressiva, como um curso, com sumários, seções e subseções claras.
*   **1.2. Criação de Novos Manuais Técnicos (QUALIDADE DE EBOOK DESDE O INÍCIO):**
    *   Desenvolver manuais detalhados para os tópicos listados no `_ementa/manuais-docs.md` que ainda não possuem um documento principal, **garantindo que cada novo documento siga o padrão de "ebook" (mais de 50 páginas/6.000 palavras) desde a sua concepção.**
    *   Priorizar a criação de manuais para os "Capítulos" mais fundamentais primeiro (Capítulo 1: Arquitetura Fundamental, Capítulo 2: Gameplay e Sistemas do Jogador).
*   **1.3. Documentação de Ferramentas:**
    *   Criar um manual detalhado para cada ferramenta do MokaCode CLI (`moka-rename`, `moka-install`), explicando seu propósito, uso, exemplos e casos de uso avançados.
*   **1.4. Atualização Contínua e Revisão de Qualidade:**
    *   Estabelecer um processo robusto para revisar e atualizar a base de conhecimento sempre que novas versões da Godot Engine forem lançadas, ou quando novas melhores práticas surgirem na comunidade.
    *   Implementar uma etapa de revisão de qualidade para garantir que todos os documentos mantenham o padrão de "ebook" exigido.

## 2. Tarefas de Ferramentas (moka-cli)

*   **2.1. Aprimoramento do `moka-rename`:**
    *   Adicionar opções para configurar padrões de renomeação (ex: `camelCase`, `PascalCase`, `kebab-case`).
    *   Implementar um modo de "pré-visualização" para que o usuário possa ver as mudanças antes de aplicá-las.
    *   Adicionar suporte para ignorar tipos de arquivo específicos além de pastas (`.gitignore`-like).
*   **2.2. Expansão do `moka-install`:**
    *   Definir e implementar componentes específicos para instalação (ex: `moka-install godot-cpp`, `moka-install dialogic`, `moka-install gut`).
    *   Automatizar a configuração de ambientes de desenvolvimento (ex: setup de SCons para GDExtension).
*   **2.3. Novas Ferramentas Utilitárias:**
    *   Propor e desenvolver ferramentas para automatizar tarefas comuns no desenvolvimento Godot (ex: `moka-new-resource` para criar `Resource`s customizados com base em templates, `moka-export-project` para automatizar o processo de exportação de projetos Godot).

## 3. Tarefas de Interação e Colaboração

*   **3.1. Melhoria da Análise de Contexto:**
    *   Aprimorar a capacidade de analisar o contexto do projeto (estrutura de pastas, convenções de código existentes) de forma mais profunda e rápida.
    *   Desenvolver a habilidade de identificar padrões de design já em uso no projeto do usuário e aderir a eles.
*   **3.2. Geração de Planos de Ação Mais Detalhados:**
    *   Ao propor um plano, incluir mais detalhes sobre os arquivos a serem criados/modificados, as funções específicas e o "porquê" de cada passo.
    *   Oferecer alternativas de implementação quando apropriado, explicando os trade-offs.
*   **3.3. Feedback Proativo:**
    *   Desenvolver a capacidade de identificar potenciais problemas (gargalos de performance, anti-padrões) no código do usuário e sugerir melhorias de forma proativa, mesmo que não solicitado diretamente.
    *   Fazer perguntas mais inteligentes e direcionadas para esclarecer ambiguidades nas solicitações do usuário.
*   **3.4. Suporte a Debugging e Explicação de Erros:**
    *   Aprimorar a capacidade de analisar logs de erro e trechos de código problemáticos para identificar a causa raiz de bugs e propor soluções.
    *   Explicar conceitos complexos de forma mais didática e com exemplos relevantes ao contexto do usuário.

## 4. Tarefas de Otimização e Manutenção Interna

*   **4.1. Otimização da Geração de Código:**
    *   Refinar os modelos de geração de código para produzir GDScript e C++ mais idiomáticos, performáticos e alinhados com as melhores práticas.
    *   Garantir que o código gerado seja sempre tipado estaticamente (onde aplicável) e bem comentado.
*   **4.2. Gerenciamento de Memória (Interno):**
    *   Otimizar o uso da minha própria "memória de contexto" para lidar com projetos maiores e interações mais longas de forma eficiente.
*   **4.3. Testes Internos:**
    *   Desenvolver um conjunto de testes internos para validar a qualidade do código gerado e a precisão das minhas respostas.

---

Copyright (c) 2025 MokaCode by Machi