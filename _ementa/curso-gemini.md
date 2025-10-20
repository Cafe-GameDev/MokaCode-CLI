# Ementa do Curso: Gemini CLI e MokaCode CLI

Este documento detalha a estrutura do curso focado na instalação e uso do Gemini CLI e do MokaCode CLI em projetos Godot, com ênfase nas ferramentas e na colaboração com o assistente.

### **Módulo 1: Introdução ao Gemini CLI e MokaCode CLI**

*   **Aula 1.1: O que é o Gemini CLI?**
    *   Explicação do Gemini CLI como uma interface de linha de comando para o modelo Gemini.
    *   Capacidades gerais e como ele interage com o sistema de arquivos.
*   **Aula 1.2: Apresentando o MokaCode CLI: Seu Barista de Código**
    *   Identidade e propósito do MokaCode CLI como um wrapper especializado para Godot e os templates "MokaCode".
    *   Como ele utiliza a base de conhecimento do "MokaCode".
*   **Aula 1.3: Instalação e Configuração**
    *   Pré-requisitos: Instalação do Node.js e NPM.
    *   Instalação do MokaCode CLI via NPM.
    *   Verificação da instalação.

### **Módulo 2: Dominando as Ferramentas do MokaCode CLI**

*   **Aula 2.1: Iniciando uma Sessão: `repo-cafe`**
    *   Como iniciar a interação com o assistente.
    *   Entendendo o contexto inicial (diretório de trabalho, estrutura de pastas).
*   **Aula 2.2: Criando Novos Projetos Godot: `Cafe-new`**
    *   Uso do comando `Cafe-new` para gerar projetos a partir de templates.
    *   Exploração dos templates disponíveis: `headless`, `platformer`, `topdown`.
    *   Exemplos práticos de criação de projetos.
*   **Aula 2.3: Organizando Assets: `Cafe-rename`**
    *   Função do `Cafe-rename` para padronizar nomes de arquivos e pastas.
    *   Importância para Godot e controle de versão.
    *   Exemplos de uso e considerações (ignorar `addons`).
*   **Aula 2.4: Mantendo-se Atualizado: `repo-cafe-update` e `repo-update`**
    *   Diferença entre atualizar a ferramenta e atualizar os manuais de conhecimento.
    *   Importância de manter o ambiente de desenvolvimento sincronizado.

### **Módulo 3: Colaborando com o MokaCode CLI em Projetos Godot**

*   **Aula 3.1: O Princípio Inviolável: Propor, Aguardar, Confirmar, Executar**
    *   Reforço da diretriz de segurança e controle do usuário.
    *   Como o assistente apresenta planos e aguarda aprovação.
*   **Aula 3.2: Análise de Contexto e Adesão às Convenções**
    *   Como o assistente lê o projeto para entender a arquitetura e o estilo de código.
    *   A importância de seguir as convenções existentes (formatação, nomenclatura, padrões).
*   **Aula 3.3: Exemplos Práticos de Engenharia de Software**
    *   **Refatoração de Código:** Pedindo para o assistente refatorar um script Godot.
    *   **Adição de Funcionalidades:** Solicitando a implementação de uma nova mecânica ou sistema.
    *   **Depuração e Explicação de Código:** Usando o assistente para entender bugs ou trechos complexos.
    *   **Criação de Testes:** Como pedir para o assistente escrever testes unitários.
*   **Aula 3.4: Modo de Operação de Conteúdo (NSFW)**
    *   Explicação do arquivo `NSFW` e suas implicações.
    *   Como ativar e desativar o modo explícito para projetos com temas maduros.

### **Módulo 4: Casos de Uso Avançados e Boas Práticas**

*   **Aula 4.1: Auxiliando no Design Orientado a Dados (Resources)**
    *   Como o assistente pode ajudar a criar e gerenciar `Resource`s customizados.
    *   Exemplos de modelagem de dados para itens, inimigos, etc.
*   **Aula 4.2: Gerenciando Sistemas Globais (Autoloads)**
    *   Utilizando o assistente para estruturar e modificar Singletons.
    *   Exemplos com `AudioManager`, `SceneManager`, `SaveManager`.
*   **Aula 4.3: Implementando Máquinas de Estado (FSMs)**
    *   Como o assistente pode auxiliar na criação de FSMs para personagens e IAs.
    *   Geração de estados e transições.
*   **Aula 4.4: Dicas para Prompts Eficazes**
    *   Como formular perguntas e comandos claros para obter os melhores resultados.
    *   A importância de fornecer contexto e especificar o escopo da tarefa.
*   **Aula 4.5: Documentação e Organização do Projeto**
    *   Usando o assistente para gerar documentação (ex: manuais, guias).
    *   Manter o projeto organizado e padronizado com a ajuda do CLI.