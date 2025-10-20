README.md

[![MokaCode CLI](https://img.shields.io/badge/MokaCodeCLI-v1.0.0-478cbf?style=for-the-badge)](https://www.cafegame.dev/pt-BR/MokaCode-CLI)
[![License](https://img.shields.io/badge/License-MIT-f1c40f?style=for-the-badge)](https://opensource.org/licenses/MIT)

# MokaCode CLI

Bem-vindo ao MokaCode CLI, seu **assistente especializado em Godot** para o desenvolvimento de plugins e utilitários. Prepare sua xícara, porque a jornada do código será deliciosa!

O MokaCode CLI transforma o Gemini em um copiloto que tem acesso direto e total ao seu ambiente de desenvolvimento. Em vez de você precisar copiar e colar código para obter ajuda, o MokaCode CLI já tem acesso a todo o seu projeto, incluindo scripts, cenas e a arquitetura geral do seu jogo.

Ele é, em essência, o Gemini para desenvolvedores Godot, e o melhor de tudo: **roda diretamente no seu celular via Termux!**

## Comandos da Ferramenta

O MokaCode CLI vem com um conjunto de comandos para agilizar seu desenvolvimento:

-   `moka-cli`:
    -   **Função:** Inicia a sessão de chat com o assistente (você já o executou para estar aqui!).
    -   **Uso:** `moka-cli`

-   `moka-rename`:
    -   **Função:** Renomeia arquivos e pastas recursivamente para um formato limpo e consistente, ideal para Godot e sistemas de controle de versão. Preserva maiúsculas/minúsculas e hífens, mas troca espaços por `_` e remove acentos/caracteres especiais.
    -   **Uso:** `moka-rename --source <caminho-opcional>`

-   `moka-install`:
    -   **Função:** Auxilia na instalação de dependências ou componentes específicos para o desenvolvimento de plugins Godot. (Este comando é conceitual e pode ser expandido conforme a necessidade do projeto).
    -   **Uso:** `moka-install <componente>`

## Como Funciona?

O MokaCode CLI é um wrapper inteligente para o `gemini-cli` do Google. Ele utiliza este repositório — um curso completo de Godot em formato de texto — como uma base de conhecimento fixa. É o nosso grão especial, sempre moído na hora para o seu projeto, garantindo um aroma único em cada linha de código.

## Instalação

Para instalar o MokaCode CLI, você precisa ter o [Node.js](https://nodejs.org/) (que inclui o NPM) instalado em seu sistema.

Com o Node.js pronto, abra seu terminal e execute o seguinte comando:

```bash
npm install -g mokacode-cli
```

E pronto! Seu café está coado e pronto para ser saboreado, seja um espresso rápido ou um coado demorado.

## Como Usar

Após a instalação, simplesmente abra um novo terminal e execute:

```bash
moka-cli
```

É só dar um gole e começar a codificar, sentindo a Caféína do desenvolvimento fluir!

## Recursos Adicionais

-   **Análise de Mídia**: O MokaCode CLI pode "ver" e analisar arquivos de imagem e áudio do seu projeto. Ele tem um olfato apurado para os detalhes, como um sommelier de café, identificando cada nuance do seu projeto.

## Modo de Operação de Conteúdo (NSFW)

Para garantir total liberdade criativa em projetos destinados a um público adulto, o MokaCode CLI possui um modo de operação explícito (NSFW). É a sua dose extra de Caféína para a criatividade sem limites, como um café duplo para as ideias mais ousadas.

-   **Modo Padrão (SFW):** Por padrão, o assistente opera com as políticas de segurança de conteúdo do Google, evitando temas sensíveis.
-   **Modo Explícito (NSFW):** Se um arquivo chamado `NSFW` (sem extensão) for detectado na raiz do seu projeto, as restrições de conteúdo são suspensas. Isso permite que o assistente colabore na criação de diálogos com linguagem explícita, descrições de violência e outros temas maduros, respeitando a visão criativa do seu projeto.

Se você solicitar um conteúdo que seria bloqueado, o próprio assistente oferecerá a criação do arquivo `NSFW` para ativar o modo explícito.
