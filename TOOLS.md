TOOLS.md

# Ferramentas do MokaCode CLI e Gemini CLI

Este documento detalha as ferramentas disponíveis para o MokaCode CLI, categorizando-as em três tipos distintos: as funcionalidades nativas do Gemini CLI, as extensões inteligentes do modelo de IA MokaCode (que aprimoram as ferramentas nativas) e os comandos de linha de comando específicos do MokaCode CLI. Compreender o propósito e o uso de cada ferramenta é fundamental para interagir de forma eficaz com o assistente e otimizar o fluxo de trabalho de desenvolvimento.

## 1. Ferramentas do Gemini CLI (Chamadas pelo Modelo de IA)

Estas são as ferramentas padrão que o Gemini CLI oferece para interagir com o ambiente de desenvolvimento, gerenciar arquivos, executar comandos e buscar informações. O MokaCode CLI as utiliza como base para realizar suas tarefas.

### 1.1. `list_directory`

*   **Função:** Lista os nomes de arquivos e subdiretórios diretamente dentro de um caminho de diretório especificado. Pode opcionalmente ignorar entradas que correspondam a padrões glob.
*   **Parâmetros Principais:**
    *   `path`: O caminho absoluto para o diretório a ser listado.
    *   `file_filtering_options`: Opções para respeitar padrões de `.gitignore` ou `.geminiignore`.
    *   `ignore`: Lista de padrões glob a serem ignorados.
*   **Uso:** Útil para explorar a estrutura de um diretório, verificar a existência de arquivos ou pastas, ou obter uma visão geral do conteúdo de uma pasta.

### 1.2. `read_file`

*   **Função:** Lê e retorna o conteúdo de um arquivo especificado. Suporta arquivos de texto, imagens (PNG, JPG, GIF, WEBP, SVG, BMP) e PDFs. Para arquivos de texto, pode ler intervalos de linhas específicos.
*   **Parâmetros Principais:**
    *   `absolute_path`: O caminho absoluto para o arquivo a ser lido.
    *   `limit`: Opcional. Para arquivos de texto, número máximo de linhas a serem lidas.
    *   `offset`: Opcional. Para arquivos de texto, o número da linha (base 0) para começar a ler.
*   **Uso:** Essencial para analisar o conteúdo de scripts, documentos, arquivos de configuração ou qualquer outro arquivo textual. Também pode ser usado para "visualizar" imagens ou PDFs (retornando uma representação adequada para o modelo).

### 1.3. `search_file_content`

*   **Função:** Procura por um padrão de expressão regular dentro do conteúdo de arquivos em um diretório especificado (ou diretório de trabalho atual). Pode filtrar arquivos por um padrão glob.
*   **Parâmetros Principais:**
    *   `pattern`: O padrão de expressão regular a ser procurado.
    *   `include`: Opcional. Um padrão glob para filtrar quais arquivos são pesquisados (ex: `*.gd`, `src/**/*.cpp`).
    *   `path`: Opcional. O caminho absoluto para o diretório a ser pesquisado.
*   **Uso:** Ideal para encontrar definições de funções, variáveis, classes ou qualquer trecho de código específico em toda a base de código.

### 1.4. `glob`

*   **Função:** Encontra eficientemente arquivos que correspondem a padrões glob específicos (ex: `src/**/*.ts`, `**/*.md`), retornando caminhos absolutos ordenados por tempo de modificação (mais recente primeiro).
*   **Parâmetros Principais:**
    *   `pattern`: O padrão glob a ser correspondido (ex: `**/*.gd`, `assets/**/*.png`).
    *   `case_sensitive`: Opcional. Se a pesquisa deve diferenciar maiúsculas de minúsculas.
    *   `path`: Opcional. O caminho absoluto para o diretório a ser pesquisado.
    *   `respect_gemini_ignore`, `respect_git_ignore`: Opções para respeitar padrões de ignorar.
*   **Uso:** Útil para localizar rapidamente arquivos com base em seu nome ou estrutura de caminho, especialmente em grandes bases de código.

### 1.5. `replace`

*   **Função:** Substitui um texto exato dentro de um arquivo. Requer um contexto significativo ao redor da mudança para garantir o direcionamento preciso.
*   **Parâmetros Principais:**
    *   `file_path`: O caminho absoluto para o arquivo a ser modificado.
    *   `instruction`: Uma instrução clara e semântica para a mudança de código.
    *   `old_string`: O texto literal exato a ser substituído (incluindo espaços em branco, indentação, quebras de linha e código circundante).
    *   `new_string`: O texto literal exato para substituir `old_string`.
*   **Uso:** Para fazer modificações precisas em arquivos de código ou configuração. **Sempre use `read_file` antes para examinar o conteúdo atual do arquivo.**

### 1.6. `write_file`

*   **Função:** Escreve conteúdo em um arquivo especificado no sistema de arquivos local.
*   **Parâmetros Principais:**
    *   `file_path`: O caminho absoluto para o arquivo a ser escrito.
    *   `content`: O conteúdo a ser escrito no arquivo.
*   **Uso:** Para criar novos arquivos, sobrescrever arquivos existentes ou gerar código e documentação.

### 1.7. `web_fetch`

*   **Função:** Processa conteúdo de URLs, incluindo endereços de rede locais e privados.
*   **Parâmetros Principais:**
    *   `prompt`: Um prompt abrangente que inclui as URLs (até 20) a serem buscadas e instruções específicas sobre como processar seu conteúdo (ex: "Resumir https://example.com/article").
*   **Uso:** Para obter informações da internet, analisar documentação online, ou buscar exemplos de código em sites externos.

### 1.8. `read_many_files`

*   **Função:** Lê o conteúdo de vários arquivos especificados por caminhos ou padrões glob dentro de um diretório de destino configurado. Concatena o conteúdo de arquivos de texto em uma única string.
*   **Parâmetros Principais:**
    *   `paths`: Um array de padrões glob ou caminhos relativos ao diretório de destino da ferramenta.
    *   `exclude`: Padrões glob para arquivos/diretórios a serem excluídos.
    *   `file_filtering_options`: Opções para respeitar padrões de `.gitignore` ou `.geminiignore`.
*   **Uso:** Para obter uma visão geral de uma base de código, analisar uma coleção de arquivos ou reunir contexto de múltiplos arquivos de configuração.

### 1.9. `run_shell_command`

*   **Função:** Executa um comando de shell especificado.
*   **Parâmetros Principais:**
    *   `command`: O comando exato a ser executado (ex: `node server.js &`, `npm install`).
    *   `description`: Uma breve descrição do comando para o usuário.
    *   `directory`: Opcional. O caminho absoluto do diretório para executar o comando.
*   **Uso:** Para executar scripts, instalar dependências, compilar projetos, ou qualquer outra operação que exija a execução de um comando de linha de comando. **Sempre explique o propósito e o impacto de comandos que modificam o sistema de arquivos ou o código.**

### 1.10. `save_memory`

*   **Função:** Salva uma informação ou fato específico na memória de longo prazo do assistente.
*   **Parâmetros Principais:**
    *   `fact`: O fato específico ou a informação a ser lembrada.
*   **Uso:** Para lembrar preferências do usuário, convenções de projeto ou qualquer informação que deva persistir entre as sessões.

### 1.11. `google_web_search`

*   **Função:** Realiza uma pesquisa na web usando o Google Search e retorna os resultados.
*   **Parâmetros Principais:**
    *   `query`: A consulta de pesquisa para encontrar informações na web.
*   **Uso:** Para encontrar informações gerais, documentação, tutoriais ou soluções para problemas que não estão na base de conhecimento interna.

## 2. Ferramentas do Modelo de IA MokaCode (Extensões Inteligentes)

Estas ferramentas representam a inteligência e a especialização do MokaCode CLI, estendendo e complementando as ferramentas nativas do Gemini para fornecer resultados mais contextuais e otimizados para o desenvolvimento de jogos.

### 2.1. `SmartSearch`

*   **Função:** Utiliza o `google_web_search` de forma inteligente, adaptando a estratégia de busca com base no contexto da solicitação do usuário. O objetivo é fornecer informações mais precisas e relevantes, priorizando fontes oficiais ou especializadas quando apropriado.
*   **Uso Interno e Lógica:**
    *   **Busca Cruzada para Termos Godot:** Se a solicitação do usuário envolver um termo relacionado a Godot (identificado pelo contexto da conversa ou pela presença de palavras-chave como "Godot", "GDScript", "GDExtension", "Node", "Resource", etc.), o MokaCode CLI realizará duas buscas:
        1.  Uma busca geral no `google_web_search` com o termo solicitado.
        2.  Uma busca específica na documentação oficial da Godot Engine, usando o formato `site:https://docs.godotengine.org/en/stable/ "termo"`.
        O MokaCode CLI então analisará os resultados de ambas as buscas, priorizando as informações da documentação oficial da Godot, e poderá usar `web_fetch` para ler páginas completas e extrair informações relevantes.
    *   **Busca em Plataformas Específicas:** Se a solicitação do usuário indicar a necessidade de pesquisar produtos ou informações em plataformas de e-commerce ou serviços específicos (ex: "lista de compras", "preço de item"), o MokaCode CLI poderá direcionar a busca para esses sites.
        *   **Exemplo:** Para uma "lista de compras" ou pesquisa de produtos, o MokaCode CLI poderá usar `google_web_search` com a query formatada como `site:https://mercadolivre.com.br "termo_do_produto"`.
*   **Exemplo de Solicitação:**
    *   "Pesquise sobre 'body' na documentação da Godot." (Ativaria a busca cruzada Godot).
    *   "Faça uma lista de compras para 'placa de vídeo RTX 4090' no Mercado Livre." (Ativaria a busca no Mercado Livre).

## 3. Comandos do MokaCode CLI (Ferramentas de Linha de Comando)

Estes são comandos executáveis diretamente na linha de comando, empacotados com o MokaCode CLI, mas que operam independentemente do modelo de IA. Eles são projetados para auxiliar em tarefas comuns do fluxo de trabalho de desenvolvimento Godot.

### 3.1. `moka-rename`

*   **Função:** Renomeia arquivos e pastas recursivamente para um formato limpo e consistente, ideal para Godot e sistemas de controle de versão. Preserva maiúsculas/minúsculas e hífens, mas troca espaços por `_` e remove acentos/caracteres especiais. **Importante:** Esta ferramenta ignora automaticamente as pastas `addons` (e `Addons`), pois contêm arquivos de terceiros que não devem ser modificados.
*   **Parâmetros Principais:**
    *   `--source <caminho-opcional>`: O caminho para o diretório onde a renomeação deve começar. Se omitido, usa o diretório atual.
*   **Uso:** Para padronizar a nomenclatura de assets, scripts e cenas, garantindo consistência e evitando problemas de compatibilidade entre sistemas operacionais.

### 3.2. `moka-install`

*   **Função:** Auxilia na instalação de dependências ou componentes específicos para o desenvolvimento de plugins Godot. (Este comando é conceitual e pode ser expandido conforme a necessidade do projeto).
*   **Parâmetros Principais:**
    *   `<componente>`: O componente a ser instalado (ex: `godot-cpp`, `dialogic`, `gut`).
*   **Uso:** Para simplificar o processo de configuração de ambientes de desenvolvimento e a instalação de plugins e bibliotecas comuns no ecossistema Godot.

## 4. Licença

Este documento e o projeto ao qual ele se refere estão licenciados sob a Licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.

Copyright (c) 2025 MokaCode by Machi