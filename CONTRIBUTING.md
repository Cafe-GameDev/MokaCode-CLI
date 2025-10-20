CONTRIBUTING.md

# Como Contribuir para o Projeto GDExtension Godot

Agradecemos imensamente o seu interesse em contribuir para este projeto! Sua ajuda é fundamental para o crescimento e aprimoramento dos plugins da Godot Engine. Este documento fornece um guia abrangente para você começar a contribuir, garantindo um processo suave e eficiente.

## Sumário

1.  [Como Contribuir](#1-como-contribuir)
2.  [Relatando Bugs](#2-relatando-bugs)
3.  [Sugestão de Recursos/Melhorias](#3-sugestão-de-recursosmelhorias)
4.  [Desenvolvimento Local](#4-desenvolvimento-local)
    *   [Configuração do Ambiente](#41-configuração-do-ambiente)
    *   [Configuração do IDE](#42-configuração-do-ide)
    *   [Build e Execução](#43-build-e-execução)
    *   [Debugging](#44-debugging)
5.  [Estilo de Código](#5-estilo-de-código)
6.  [Processo de Pull Request](#6-processo-de-pull-request)
7.  [Checklists de Qualidade](#7-checklists-de-qualidade)
8.  [Licença](#8-licença)

---

## 1. Como Contribuir

Existem várias maneiras valiosas de contribuir para este projeto:

*   **Relatando Bugs:** Ajude-nos a identificar e corrigir problemas, fornecendo relatórios claros e reproduzíveis.
*   **Sugestão de Recursos/Melhorias:** Compartilhe suas ideias para novas funcionalidades ou aprimoramentos, ajudando a moldar o futuro do projeto.
*   **Escrevendo Código:** Contribua com código para corrigir bugs, implementar novos recursos, refatorar código existente ou melhorar a documentação.
*   **Melhorando a Documentação:** Ajude a manter a documentação clara, precisa, atualizada e abrangente, tornando o projeto mais acessível a todos.

## 2. Relatando Bugs

Se você encontrar um bug, por favor, siga estas diretrizes para relatá-lo de forma eficaz:

*   Verifique se o bug já foi relatado nas [Issues do GitHub](https://github.com/cafegamedev/GDExtension/issues). Se sim, adicione seus comentários e informações adicionais.
*   Abra uma nova Issue e forneça o máximo de detalhes possível:
    *   **Título:** Descrição concisa e clara do problema (ex: "[BUG] Crash ao carregar plugin X no Windows").
    *   **Passos para Reproduzir:** Instruções claras e numeradas para reproduzir o bug. Seja o mais específico possível.
        1.  Passo 1
        2.  Passo 2
        3.  ...
    *   **Comportamento Esperado:** O que você esperava que acontecesse.
    *   **Comportamento Atual:** O que realmente aconteceu (o bug).
    *   **Versão da Godot Engine:** (Ex: Godot 4.2.1 Stable)
    *   **Sistema Operacional:** (Ex: Windows 10, macOS Sonoma, Ubuntu 22.04)
    *   **Informações Adicionais:** Logs de erro, capturas de tela, vídeos, trechos de código relevantes, ou qualquer outra informação que possa ajudar a diagnosticar o problema.

## 3. Sugestão de Recursos/Melhorias

Se você tem uma ideia para um novo recurso ou uma melhoria, por favor, siga estas diretrizes:

*   Verifique se a sugestão já foi discutida nas [Issues do GitHub](https://github.com/cafegamedev/GDExtension/issues). Se sim, participe da discussão existente.
*   Abra uma nova Issue e descreva sua sugestão:
    *   **Título:** Descrição concisa da sugestão (ex: "[FEATURE] Adicionar sistema de inventário modular").
    *   **Problema que Resolve:** Qual problema a sua sugestão resolve ou qual necessidade ela atende.
    *   **Solução Proposta:** Como você imagina que o recurso ou melhoria funcionaria. Inclua detalhes sobre a API, integração com o editor, etc.
    *   **Casos de Uso:** Exemplos de como o recurso seria utilizado por desenvolvedores ou jogadores.
    *   **Alternativas Consideradas:** Se houver, discuta outras abordagens que você pensou e por que a sua proposta é a melhor.

## 4. Desenvolvimento Local

Para configurar seu ambiente de desenvolvimento local e começar a contribuir com código, siga estas etapas:

### 4.1. Configuração do Ambiente

1.  **Clone o Repositório:**
    ```bash
    git clone https://github.com/cafegamedev/GDExtension.git
    cd GDExtension
    ```
2.  **Instale a Godot Engine:** Certifique-se de ter a versão correta da Godot Engine instalada (verifique o `project.godot` para a versão alvo, geralmente a versão mais recente estável).
3.  **Configure o Ambiente C++ (para GDExtension):**
    *   **Compilador C++:** Instale um compilador C++ moderno (ex: MSVC no Windows, GCC/Clang no Linux/macOS). Consulte `C++.md` para mais detalhes.
    *   **Python:** Python 3.x é necessário para o SCons.
    *   **SCons:** Instale o SCons via pip: `pip install scons`.
    *   **`godot-cpp`:** Clone o repositório `godot-cpp` (a biblioteca de bindings C++ para GDExtension) na raiz do projeto, ou como um submódulo git.
        ```bash
        git submodule update --init --recursive
        # ou
        git clone https://github.com/godotengine/godot-cpp.git
        ```
        Certifique-se de que a versão do `godot-cpp` seja compatível com a versão da Godot Engine que você está usando.

### 4.2. Configuração do IDE

Recomendamos o uso de um IDE com bom suporte a C++ e GDScript:

*   **VS Code:** Com extensões como C/C++ (Microsoft), Python, GDScript (Godot Tools).
*   **Visual Studio (Windows):** Para desenvolvimento C++.
*   **CLion:** Excelente suporte a C++ e integração com sistemas de build.

Configure seu IDE para incluir os cabeçalhos do `godot-cpp` e do seu projeto GDExtension para autocompletar e navegação de código.

### 4.3. Build e Execução

1.  **Build da Biblioteca GDExtension:** Navegue até a raiz do seu projeto GDExtension e execute o SCons para compilar sua biblioteca C++.
    ```bash
    scons platform=<your_platform> target=<debug/release>
    # Exemplo: scons platform=windows target=debug
    ```
    Consulte `C++.md` e `GDExtension.md` para instruções de build mais detalhadas para diferentes plataformas.
2.  **Executar o Projeto Godot:** Abra o projeto Godot no editor e execute-o. Certifique-se de que seu plugin GDExtension esteja habilitado em `Project -> Project Settings -> Plugins`.

### 4.4. Debugging

*   **Debugging C++:** Configure seu IDE para anexar ao processo da Godot Engine. Isso permitirá definir breakpoints no seu código C++, inspecionar variáveis e percorrer a execução. Consulte `C++.md` para mais detalhes.
*   **Debugging GDScript:** Utilize o debugger embutido do Godot para scripts GDScript. Você pode definir breakpoints, inspecionar variáveis e controlar o fluxo de execução.

## 5. Estilo de Código

Para manter a consistência e a legibilidade do código, por favor, siga as seguintes diretrizes:

*   **GDScript:** Adira rigorosamente ao [Guia de Estilo do GDScript da Godot Engine](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_style_guide.html).
*   **C++:** Siga as convenções de estilo do Godot para C++ (geralmente baseadas em K&R com algumas adaptações). Utilize ferramentas de formatação como `clang-format` para garantir a consistência automática.
*   **Nomenclatura:** Utilize nomes descritivos e consistentes para variáveis, funções, classes e arquivos. Siga as convenções da Godot (PascalCase para classes, snake_case para métodos e variáveis).
*   **Comentários:** Adicione comentários claros e concisos onde a lógica não for autoexplicativa, explicando a intenção, algoritmos complexos ou decisões de design.

## 6. Processo de Pull Request

1.  **Crie um Fork:** Faça um fork do repositório principal para sua conta GitHub.
2.  **Crie uma Branch:** Crie uma nova branch a partir da branch `main` (ou da branch de desenvolvimento apropriada) para suas alterações. Use nomes descritivos para a branch (ex: `feature/nome-da-feature`, `bugfix/correcao-do-bug`).
    ```bash
    git checkout main
    git pull origin main
    git checkout -b feature/minha-nova-feature
    ```
3.  **Faça Suas Alterações:** Implemente suas alterações, seguindo o estilo de código e as melhores práticas do projeto.
4.  **Teste Suas Alterações:** Certifique-se de que suas alterações não introduzem novos bugs e que todos os testes existentes (unitários e de integração) continuam passando. Adicione novos testes se for o caso.
5.  **Commit Suas Alterações:** Escreva mensagens de commit claras, concisas e descritivas. Siga a convenção [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) (ex: `feat: Adiciona nova funcionalidade X`, `fix: Corrige bug Y`).
    ```bash
    git commit -m "feat: Adiciona nova funcionalidade X"
    # ou
    git commit -m "fix: Corrige bug Y"
    ```
6.  **Envie para o Seu Fork:**
    ```bash
    git push origin feature/minha-nova-feature
    ```
7.  **Abra um Pull Request (PR):** Vá para o repositório original no GitHub e abra um Pull Request da sua branch para a branch `main` (ou a branch de desenvolvimento apropriada).
    *   Forneça uma descrição detalhada das suas alterações, explicando o *porquê* e o *o quê* da mudança.
    *   Referencie quaisquer Issues relacionadas (ex: `Closes #123`, `Fixes #456`).
    *   Inclua capturas de tela ou GIFs se as alterações forem visuais.
    *   Preencha o template de PR, se houver.
8.  **Revisão de Código:** Participe ativamente do processo de revisão de código, respondendo a comentários e fazendo as alterações solicitadas.

## 7. Checklists de Qualidade

Antes de abrir um Pull Request, revise suas alterações com os seguintes checklists:

### 7.1. Checklist de Código

*   [ ] O código segue as diretrizes de estilo (GDScript, C++).
*   [ ] O código está bem comentado onde necessário.
*   [ ] Não há código morto ou comentado desnecessariamente.
*   [ ] As variáveis e funções têm nomes descritivos.
*   [ ] Não há warnings de compilador ou linter.
*   [ ] O código é eficiente e não introduz gargalos de performance.
*   [ ] O gerenciamento de memória em C++ está correto (uso de `Ref<T>`, `memnew`/`memdelete`).

### 7.2. Checklist de Testes

*   [ ] Todos os testes existentes passam.
*   [ ] Novos testes unitários foram adicionados para cobrir as novas funcionalidades ou correções de bugs.
*   [ ] Testes de integração foram realizados para verificar a interação entre componentes.
*   [ ] O plugin foi testado no editor Godot e em tempo de execução.
*   [ ] O plugin foi testado em diferentes plataformas (se aplicável).

### 7.3. Checklist de Documentação

*   [ ] A documentação interna (comentários de código) foi atualizada.
*   [ ] A documentação externa (README, PDD, etc.) foi atualizada para refletir as mudanças.
*   [ ] Novos exemplos ou tutoriais foram adicionados, se relevantes.

## 8. Licença

Ao contribuir para este projeto, você concorda que suas contribuições serão licenciadas sob a [Licença MIT](https://opensource.org/licenses/MIT). Consulte o arquivo `LICENSE` para mais detalhes.

Copyright (c) 2025 MokaCode by Machi