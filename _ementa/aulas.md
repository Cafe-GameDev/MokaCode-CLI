# Estrutura de Aulas do Curso (Índice Detalhado e Expandido)

Este documento delineia a trilha de aprendizagem completa do curso. A estrutura foi projetada para ser uma formação de nível universitário, levando o aluno do zero absoluto ao nível profissional.

# Sumário

- [Estrutura de Aulas do Curso (Índice Detalhado e Expandido)](#estrutura-de-aulas-do-curso-índice-detalhado-e-expandido)
- [Sumário](#sumário)
  - [**Módulo 00: Fundamentos Universais da Lógica de Programação**](#módulo-00-fundamentos-universais-da-lógica-de-programação)
  - [**Módulo 01: Godot Engine: Conceitos Essenciais**](#módulo-01-godot-engine-conceitos-essenciais)
  - [**Módulo 02: O Laboratório de Mecânicas: Construindo seu Primeiro Jogo**](#módulo-02-o-laboratório-de-mecânicas-construindo-seu-primeiro-jogo)
  - [**Módulo 03: Desafio: Faça seu Jogo**](#módulo-03-desafio-faça-seu-jogo)
  - [\*\*Módulo 04: \*\*](#módulo-04-)
  - [**Módulo 05: Dome Keeper**](#módulo-05-dome-keeper)
  - [**Módulo 06: Desafio: Faça seu Jogo**](#módulo-06-desafio-faça-seu-jogo)
  - [**Módulo 07:**](#módulo-07)
  - [**Módulo 08: Overwath 2D**](#módulo-08-overwath-2d)
  - [\*_Módulo 09: ARPG_](#módulo-09-arpg)

---

## **Módulo 00: Fundamentos Universais da Lógica de Programação**

- **Objetivo:** Estabelecer uma base conceitual robusta e agnóstica de linguagem sobre os pilares da programação. Este módulo serve como o alicerce teórico para qualquer área de desenvolvimento de software, utilizando exemplos em GDScript, Python, JavaScript e C++ para ilustrar a universalidade dos conceitos.

- **Aulas:**

  - **Aula 0.1: O que é Programação? Algoritmos e Modelos Lógicos**

    - **Conceito Central:** Apresentar a programação como a disciplina de criar modelos lógicos formais (algoritmos) para resolver problemas e automatizar processos. O foco é a tradução de um requisito abstrato em uma sequência de instruções precisas, determinísticas e não-ambíguas que um sistema computacional pode executar.
    - **Tópicos a Cobrir:**
      - Definição formal de Algoritmo: uma sequência finita de ações executáveis para resolver um problema.
      - Abstração e Decomposição: como quebrar problemas complexos em subproblemas menores e gerenciáveis.
      - Linguagens de Programação como ferramentas formais para a expressão de algoritmos.
      - Diferença entre código-fonte (abstração humana) e código de máquina (execução nativa).
      - Introdução ao Pseudocódigo como ferramenta de design de algoritmos.
    - **Objetivo de Aprendizagem:** Ao final da aula, o aluno deve ser capaz de definir o que é um algoritmo e de projetar uma solução para um problema simples em pseudocódigo, demonstrando pensamento lógico e estruturado.
    - **Exercício Prático Sugerido:** Escrever um pseudocódigo para um algoritmo que determina o maior de três números. O pseudocódigo deve ser claro o suficiente para que possa ser implementado em qualquer linguagem sem ambiguidades.

  - **Aula 0.2: Variáveis, Constantes e Gerenciamento de Estado**

    - **Conceito Central:** Introduzir variáveis como referências nomeadas a espaços na memória que armazenam o **estado** da aplicação. Uma variável é uma abstração que permite ao programador manipular dados sem gerenciar endereços de memória físicos. Constantes são referências a dados imutáveis, essenciais para a legibilidade e para garantir a integridade de valores críticos para a lógica do programa (ex: configurações, constantes matemáticas).
    - **Tópicos a Cobrir:**
      - Declaração, inicialização e atribuição.
      - Escopo de variáveis (introdução ao conceito de onde uma variável é acessível).
      - Convenções de nomenclatura (`snake_case`, `camelCase`, `PascalCase`).
      - O papel das constantes na prevenção de "números mágicos" e na refatoração de código.
    - **Objetivo de Aprendizagem:** O aluno deve entender o papel das variáveis na gestão do estado de uma aplicação e ser capaz de declarar variáveis e constantes de forma apropriada em múltiplas linguagens.
    - **Exemplos de Código (Declaração de variável `player_score` e constante `MAX_CONNECTIONS`):**
      - **GDScript:**
        ```gdscript
        var player_score = 100
        const MAX_CONNECTIONS = 8
        ```
      - **Python:**
        ```python
        player_score = 100
        MAX_CONNECTIONS = 8 # Por convenção
        ```
      - **JavaScript:**
        ```javascript
        let playerScore = 100;
        const MAX_CONNECTIONS = 8;
        ```
      - **C++:**
        ```cpp
        int playerScore = 100;
        const int MAX_CONNECTIONS = 8;
        ```
    - **Exercício Prático Sugerido:** Em quatro arquivos separados (um para cada linguagem), declarar variáveis que definem o estado inicial de um personagem (ex: `health`, `stamina`, `ammo_count`) e constantes para seus atributos base (ex: `MAX_HEALTH`, `BASE_SPEED`).

  - **Aula 0.3: Tipos de Dados Primitivos: O Contrato de Dados**

    - **Conceito Central:** Explicar os tipos de dados como um **contrato** que define a natureza dos dados que uma variável pode conter. Este contrato informa ao compilador/interpretador como alocar memória, quais operações são válidas e como os dados devem ser representados binariamente. A aula abordará a diferença entre sistemas de tipagem estática (verificação em tempo de compilação, como C++) e dinâmica (verificação em tempo de execução, como Python/JS), e a abordagem híbrida do GDScript.
    - **Tópicos a Cobrir:**
      - Inteiros (`int`), Ponto Flutuante (`float`, `double`), Booleanos (`bool`), Caracteres (`char`) e Strings (`String`).
      - Implicações de performance e segurança da tipagem estática vs. flexibilidade da tipagem dinâmica.
      - Inferência de tipo.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de selecionar o tipo de dado primitivo apropriado para representar diferentes informações, entendendo as implicações de sua escolha em diferentes sistemas de tipagem.
    - **Exemplos de Código (Declaração de `health` com tipagem explícita):**
      - **GDScript:** `var health: int = 100`
      - **Python:** `health: int = 100` (Type Hint)
      - **JavaScript (com JSDoc):**
        ```javascript
        /** @type {number} */
        let health = 100;
        ```
      - **C++:** `int health = 100;`
    - **Exercício Prático Sugerido:** Refatorar o exercício anterior para usar a sintaxe de tipagem explícita de cada linguagem. Discutir em comentários por que `health` não deveria ser um `String` e quais seriam as consequências de usar um `float` em vez de um `int`.

  - **Aula 0.4: Operadores e Expressões: Manipulando o Estado**

    - **Conceito Central:** Apresentar operadores como símbolos que representam computações sobre operandos (variáveis e literais). Uma combinação de operadores e operandos forma uma expressão, que é avaliada para produzir um novo valor. Esta é a forma fundamental de manipular o estado da aplicação.
    - **Tópicos a Cobrir:**
      - Operadores Aritméticos (`+`, `-`, `*`, `/`, `%`).
      - Operadores de Atribuição (`=`, `+=`, `-=`).
      - Operadores de Comparação (`==`, `!=`, `>`, `<`, `>=`, `<=`).
      - Operadores Lógicos (`&&`/`and`, `||`/`or`, `!`/`not`).
      - Precedência de operadores.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de construir expressões complexas para realizar cálculos e avaliações lógicas, entendendo como essas expressões são avaliadas.
    - **Exemplos de Código (Verificar se o jogador está vivo E tem mana):**
      - **GDScript:** `if health > 0 and mana >= 10:`
      - **Python:** `if health > 0 and mana >= 10:`
      - **JavaScript:** `if (health > 0 && mana >= 10) { ... }`
      - **C++:** `if (health > 0 && mana >= 10) { ... }`
    - **Exercício Prático Sugerido:** Escrever uma expressão que calcula o dano final de um ataque, aplicando um modificador de crítico. Ex: `final_damage = base_damage * damage_multiplier; if is_critical_hit: final_damage *= 2;`. Implementar em duas linguagens diferentes.

  - **Aula 0.5: Estruturas de Controle de Fluxo: Decisão e Iteração**

    - **Conceito Central:** Unificar condicionais e loops como as estruturas que permitem a execução não-linear de um algoritmo. **Decisão (Branching)** com `if/elif/else` permite que o programa execute diferentes caminhos de código com base em expressões booleanas. **Iteração (Looping)** com `for/while` permite a execução repetida de um bloco de código, seja por um número definido de vezes ou enquanto uma condição for verdadeira.
    - **Tópicos a Cobrir:**
      - Estruturas `if`, `elif`/`else if`, `else`.
      - Estruturas `switch`/`match` como alternativa a `if`s aninhados.
      - Loops `while` (condição no início) e `do-while` (condição no final).
      - Loops `for` (iteração sobre coleções) e `for` tradicional (baseado em contador).
      - Controle de loop: `break` e `continue`.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de utilizar estruturas de controle de fluxo para criar algoritmos complexos com múltiplos caminhos de execução e lógica repetitiva.
    - **Exemplos de Código (Iterar sobre um inventário e imprimir cada item):**
      - **GDScript:**
        ```gdscript
        for item in inventory:
            print(item)
        ```
      - **Python:**
        ```python
        for item in inventory:
            print(item)
        ```
      - **JavaScript:**
        ```javascript
        for (const item of inventory) {
          console.log(item);
        }
        ```
      - **C++:**
        ```cpp
        for (const auto& item : inventory) {
            std::cout << item << std::endl;
        }
        ```
    - **Exercício Prático Sugerido:** Escrever um programa que itera de 1 a 100. Para cada número, ele deve verificar: se for múltiplo de 3, imprime "Fizz"; se for múltiplo de 5, imprime "Buzz"; se for múltiplo de ambos, imprime "FizzBuzz"; caso contrário, imprime o próprio número. Este é o clássico problema "FizzBuzz".

  - **Aula 0.6: Funções: Abstração e Reutilização de Lógica**

    - **Conceito Central:** Apresentar funções como a primeira e mais fundamental ferramenta de **abstração** em programação. Funções permitem encapsular uma sequência de instruções em uma unidade lógica nomeada, que pode ser parametrizada (via argumentos) e pode produzir um resultado (via valor de retorno). Elas são a espinha dorsal do princípio DRY (Don't Repeat Yourself) e da decomposição de problemas.
    - **Tópicos a Cobrir:**
      - Definição vs. Chamada de função.
      - Parâmetros/Argumentos e Assinatura da Função.
      - Valores de Retorno.
      - Funções `void` / Procedimentos (que não retornam valor).
      - Passagem de argumentos por valor vs. por referência (introdução conceitual).
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de identificar blocos de código repetidos e refatorá-los em funções reutilizáveis, melhorando a legibilidade, manutenibilidade e organização do código.
    - **Exemplos de Código (Função que calcula dano com base na força e defesa):**
      - **GDScript:**
        ```gdscript
        func calculate_damage(attack_power: int, defense: int) -> int:
            var damage = attack_power - defense
            return max(0, damage)
        ```
      - **Python:**
        ```python
        def calculate_damage(attack_power: int, defense: int) -> int:
            damage = attack_power - defense
            return max(0, damage)
        ```
      - **JavaScript:**
        ```javascript
        /** @param {number} attackPower @param {number} defense @returns {number} */
        function calculateDamage(attackPower, defense) {
          const damage = attackPower - defense;
          return Math.max(0, damage);
        }
        ```
      - **C++:**
        ```cpp
        int calculateDamage(int attackPower, int defense) {
            int damage = attackPower - defense;
            return std::max(0, damage);
        }
        ```
    - **Exercício Prático Sugerido:** Criar uma função `is_player_alive(health)` que recebe um valor de vida e retorna `true` se a vida for maior que 0, e `false` caso contrário. Chamar esta função dentro de uma estrutura `if`.

  - **Aula 0.7: Estruturas de Dados: Organizando Coleções de Informações**

    - **Conceito Central:** Introduzir as duas principais estruturas de dados para coleções: **Arrays/Listas** (coleções ordenadas, contíguas ou não, acessadas por um índice numérico) e **Dicionários/Mapas/Hashes** (coleções de pares chave-valor, não ordenadas, acessadas por uma chave única). Discutir os trade-offs de performance (busca, inserção, remoção) e os casos de uso ideais para cada uma.
    - **Tópicos a Cobrir:**
      - Arrays/Listas: Acesso por índice, iteração, métodos comuns (`append`, `pop`, `size`).
      - Dicionários/Mapas: Acesso por chave, iteração sobre chaves/valores, verificação de existência de chave.
      - A importância de escolher a estrutura de dados correta para a performance do algoritmo.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de modelar dados complexos (como um inventário ou uma lista de stats) usando a estrutura de dados apropriada.
    - **Exemplos de Código (Definir um inventário e os stats de um jogador):**
      - **GDScript:**
        ```gdscript
        var inventory: Array = ["Sword", "Shield"]
        var stats: Dictionary = {"str": 10, "dex": 8}
        ```
      - **Python:**
        ```python
        inventory: list = ["Sword", "Shield"]
        stats: dict = {"str": 10, "dex": 8}
        ```
      - **JavaScript:**
        ```javascript
        const inventory = ["Sword", "Shield"];
        const stats = { str: 10, dex: 8 };
        ```
      - **C++:**
        ```cpp
        #include <vector>
        #include <string>
        #include <map>
        std::vector<std::string> inventory = {"Sword", "Shield"};
        std::map<std::string, int> stats = {{"str", 10}, {"dex", 8}};
        ```
    - **Exercício Prático Sugerido:** Modelar um "bestiário". Criar uma lista de dicionários, onde cada dicionário representa um monstro e contém suas estatísticas (nome, hp, fraquezas - que pode ser outra lista).

  - **Aula 0.8: Paradigmas: Introdução à Orientação a Objetos (OOP)**

    - **Conceito Central:** Apresentar a Orientação a Objetos como um paradigma para modelar sistemas complexos, baseando-se na interação de entidades autocontidas (objetos). Definir **Classe** como um "blueprint" que define a estrutura (propriedades) e o comportamento (métodos) de uma categoria de objetos. Um **Objeto** é uma instância concreta de uma classe, com seu próprio estado. O princípio chave é o **encapsulamento**: agrupar dados e as funções que operam nesses dados.
    - **Tópicos a Cobrir:**
      - Classe vs. Objeto (Instância).
      - Propriedades/Atributos (o estado do objeto).
      - Métodos (o comportamento do objeto).
      - O conceito de `self` ou `this` como uma referência ao próprio objeto dentro de seus métodos.
      - Construtores (`_init`, `__init__`, `constructor`).
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de criar classes simples para modelar entidades de um jogo, encapsulando seus dados e comportamentos em uma única unidade lógica.
    - **Exemplos de Código (Classe `Player` simples):**
      - **GDScript:**
        ```gdscript
        class_name Player
        var health: int
        func _init(start_health: int):
            self.health = start_health
        func take_damage(amount: int):
            self.health -= amount
        ```
      - **Python:**
        ```python
        class Player:
            def __init__(self, start_health: int):
                self.health = start_health
            def take_damage(self, amount: int):
                self.health -= amount
        ```
      - **JavaScript:**
        ```javascript
        class Player {
          constructor(startHealth) {
            this.health = startHealth;
          }
          takeDamage(amount) {
            this.health -= amount;
          }
        }
        ```
      - **C++:**
        ```cpp
        class Player {
        public:
            int health;
            Player(int startHealth) {
                this->health = startHealth;
            }
            void takeDamage(int amount) {
                this->health -= amount;
            }
        };
        ```
    - **Exercício Prático Sugerido:** Criar uma classe `Item` com propriedades `name` e `value`. Criar duas instâncias (objetos) dessa classe, uma para uma "Poção" e outra para uma "Espada", cada uma com valores diferentes.

  - **Aula 0.9: Serialização de Dados: Persistência de Estado**
    - **Conceito Central:** Introduzir o conceito de **serialização**: o processo de converter uma estrutura de dados ou estado de um objeto em um formato que pode ser armazenado (ex: em um arquivo) ou transmitido e, posteriormente, reconstruído (desserialização). Foco no **JSON (JavaScript Object Notation)** como um formato de serialização universal, legível por humanos e facilmente mapeável para Dicionários/Mapas/Objetos. Apresentar o formato **TRES** do Godot como uma forma de serialização de `Resource`s integrada à engine, otimizada para o editor.
    - **Tópicos a Cobrir:**
      - O problema da persistência: dados em memória são voláteis.
      - O que é um formato de serialização de dados?
      - Estrutura e sintaxe do JSON.
      - Mapeamento 1:1 entre um Dicionário/Objeto em código e sua representação JSON.
      - Visão geral de como as linguagens fornecem bibliotecas para parsear (ler) e gerar JSON.
    - **Objetivo de Aprendizagem:** O aluno deve entender o que é serialização, por que ela é necessária para salvar o progresso de um jogo, e ser capaz de ler e escrever uma estrutura de dados simples no formato JSON.
    - **Exemplo de Código (Representação de um objeto `player_data` em JSON):**
      - **Código (Python/JS/GDScript):**
        ```
        player_data = {
            "name": "Bruno",
            "level": 5,
            "inventory": ["Sword", "Shield"],
            "is_active": true
        }
        ```
      - **JSON (Arquivo `save.json`):**
        ```json
        {
          "name": "Bruno",
          "level": 5,
          "inventory": ["Sword", "Shield"],
          "is_active": true
        }
        ```
    - **Exercício Prático Sugerido:** Pegar a estrutura de dados do "bestiário" do exercício 0.7 e escrevê-la manualmente em um arquivo de texto com a sintaxe JSON correta. Verificar se a sintaxe está válida usando um validador online.

---

## **Módulo 01: Godot Engine: Conceitos Essenciais**

- **Objetivo:** Conectar os conceitos universais do Módulo 00 com a implementação e filosofia específicas da Godot. Este módulo trata a engine como um framework de software com decisões de design e arquitetura que podem ser analisadas e compreendidas.

- **Aulas:**

  - **1.1: A Filosofia Godot: Composição de Cenas e a Estrutura de Árvore**

    - **Conceito Central:** Analisar a arquitetura de Cenas e Nós da Godot sob a ótica de padrões de design de software. A Árvore de Cenas é uma implementação do padrão **Composite**, onde tanto um Nó individual quanto uma Cena inteira (uma árvore de Nós) podem ser tratados de forma uniforme. A aula enfatiza como a Godot favorece a **Composição sobre a Herança**, um princípio fundamental de design de software que promove a reutilização e a modularidade.
    - **Tópicos a Cobrir:**
      - O Nó como a unidade atômica de funcionalidade.
      - A Cena como um "blueprint" de Nós reutilizável.
      - Instanciação de Cenas como a principal forma de construir o mundo do jogo.
      - Comparação teórica: Herança (`extends CharacterBody2D`) vs. Composição (um Nó `Player` que _tem_ um Nó `Sprite2D` e um Nó `CollisionShape2D` como filhos).
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de explicar por que a abordagem de composição da Godot é poderosa e como ela se traduz na estrutura de Cenas e Nós.
    - **Exercício Prático Sugerido:** Criar uma cena `Bullet.tscn` (`Area2D` + `Sprite2D`). Criar uma cena `Player.tscn`. No script do `Player`, instanciar a cena `Bullet` como filha do nó raiz do jogo, demonstrando como Cenas podem criar outras Cenas.

  - **1.2: Tour pela Interface: Anatomia de um Ambiente de Desenvolvimento Integrado (IDE)**

    - **Conceito Central:** Apresentar o editor da Godot como um IDE especializado para desenvolvimento de jogos. Cada painel é uma ferramenta para uma tarefa específica: o **Viewport** para manipulação espacial, o **Inspetor** como uma interface de reflexão para as propriedades de um objeto, o **Sistema de Arquivos** para gerenciamento de ativos, e o **Painel Inferior** para depuração e automação de animação.
    - **Tópicos a Cobrir:**
      - Fluxo de trabalho: da importação de um asset no FileSystem, para a sua utilização em uma Cena no Viewport, à configuração de suas propriedades no Inspetor.
      - O conceito de "contexto": como as ferramentas e opções mudam dependendo do Nó selecionado.
      - Uso do Debugger para inspecionar o estado do jogo em tempo de execução.
    - **Objetivo de Aprendizagem:** O aluno deve se familiarizar com o fluxo de trabalho profissional dentro do editor, entendendo o propósito de cada ferramenta e como elas se interconectam.
    - **Exercício Prático Sugerido:** Importar uma imagem. Criar um `Sprite2D` e arrastar a imagem para sua propriedade `Texture` no Inspetor. Adicionar um script ao sprite, colocar um `breakpoint` na função `_process` e rodar o jogo em modo de depuração para inspecionar suas variáveis.

  - **1.3: GDScript na Prática: O Ciclo de Vida de um Objeto e a Serialização de Propriedades**

    - **Conceito Central:** Conectar as funções de ciclo de vida (`_ready`, `_process`, `_physics_process`) ao conceito de **Game Loop** e **programação orientada a eventos**. São métodos "callback" que a engine invoca em pontos específicos da execução de um objeto. A anotação `@export` é apresentada como um mecanismo de **serialização e reflexão** que expõe uma propriedade do script para o editor, permitindo a sua manipulação e persistência no arquivo de cena (`.tscn`).
    - **Tópicos a Cobrir:**
      - A ordem de execução: `_init`, `_enter_tree`, `_ready`.
      - A diferença entre `_process` (taxa de quadros variável) e `_physics_process` (taxa de quadros fixa) e as implicações para a lógica de jogo.
      - O parâmetro `delta` como o tempo decorrido, essencial para um movimento independente de framerate.
      - Como `@export` transforma uma variável de script em uma propriedade serializável do Nó.
    - **Objetivo de Aprendizagem:** O aluno deve compreender como dar comportamento a um Nó (Objeto) e como expor seus atributos (Propriedades) para o editor de forma controlada, entendendo o fluxo de execução de um script Godot.
    - **Exercício Prático Sugerido:** Criar um script com uma variável `@export var speed: float = 100.0`. Na função `_physics_process`, mover o nó horizontalmente usando `position.x += speed * delta`. Observar como alterar o valor de `speed` no Inspetor afeta o comportamento em tempo real.

  - **1.4: Gerenciamento de Input: Abstração e Polling de Estado**

    - **Conceito Central:** Apresentar o `InputMap` como uma **camada de abstração** que desacopla a ação lógica do jogo (ex: "pular") do evento de hardware (ex: "tecla de espaço pressionada"). A classe `Input` é um Singleton global que serve como API para consultar (**polling**) o estado deste sistema de eventos em cada frame, uma abordagem comum em game loops.
    - **Tópicos a Cobrir:**
      - Configurando ações e mapeando múltiplos inputs (teclado, controle) para a mesma ação.
      - Polling de estado (`is_action_pressed`) vs. detecção de evento (`is_action_just_pressed`).
      - Uso de `Input.get_vector` para simplificar o código de movimento 2D.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de implementar um sistema de input robusto e remapeável, uma prática padrão em jogos comerciais.
    - **Exercício Prático Sugerido:** Criar um `InputMap` para um personagem de plataforma com ações "move_left", "move_right" e "jump". Implementar a lógica de movimento em `_physics_process` usando `Input.get_axis` e a lógica de pulo em `_physics_process` usando `Input.is_action_just_pressed`.

  - **1.5 & 1.6: O Motor de Física: Abstrações de Corpos e Filtragem de Colisão**

    - **Conceito Central:** Discutir os diferentes Nós de corpo de física (`CharacterBody`, `RigidBody`, `StaticBody`, `Area`) como diferentes **abstrações de simulação física**, cada uma com um trade-off entre controle do programador e controle da engine. As Camadas e Máscaras de Colisão são explicadas como um **sistema de filtragem espacial eficiente**, frequentemente implementado com operações bitwise, para otimizar a detecção de colisões e definir regras de interação.
    - **Tópicos a Cobrir:**
      - `CharacterBody2D`: Movimento controlado por script com resolução de colisão (`move_and_slide`).
      - `RigidBody2D`: Movimento controlado pela simulação física (forças, impulsos).
      - `Area2D`: Detecção de sobreposição, não colisão sólida.
      - `StaticBody2D`: Colisor imóvel e otimizado.
      - Configuração de Layers (em qual grupo eu estou?) e Masks (quais grupos eu detecto?).
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de escolher o corpo de física apropriado para cada entidade e configurar suas interações de forma precisa e otimizada.
    - **Exercício Prático Sugerido:** Criar um projétil (`Area2D`) na camada "player_bullet" que só detecta a máscara "enemies". Criar um inimigo (`CharacterBody2D`) na camada "enemies" que só detecta a máscara "player_bullet" e "world".

  - **1.7: Sinais: O Padrão Observer em Prática**

    - **Conceito Central:** Apresentar o sistema de Sinais da Godot como uma implementação nativa do padrão de design **Observer (Publish/Subscribe)**. Este mecanismo promove o **baixo acoplamento** entre objetos, permitindo que um objeto (o "Publisher") emita um evento sem precisar conhecer a identidade ou a implementação dos objetos (os "Subscribers") que reagirão a ele.
    - **Tópicos a Cobrir:**
      - Conectando sinais pelo editor (aba Nó) e por código (`connect`).
      - Criando sinais customizados (`signal my_signal(param1, param2)`).
      - Emitindo sinais (`my_signal.emit(value1, value2)`).
      - Vantagens: código mais modular, Cenas que funcionam de forma independente.
    - **Objetivo de Aprendizagem:** O aluno deve entender as vantagens de uma arquitetura orientada a eventos e ser capaz de usar sinais para criar código modular e de fácil manutenção.
    - **Exercício Prático Sugerido:** Criar um `Button` que, ao ter seu sinal `pressed` emitido, chama uma função em um script pai. Este script pai, por sua vez, emite um sinal customizado `game_started`. Um terceiro nó (ex: um `AudioManager`) conecta-se a `game_started` para tocar uma música.

  - **1.8: Arquitetura com `Resource`: Serialização e Design Orientado a Dados**

    - **Conceito Central:** Aprofundar no conceito de serialização do Módulo 00, apresentando `Resource` como o objeto de dados serializável fundamental da Godot. Esta aula introduz o paradigma de **Design Orientado a Dados**, onde separamos explicitamente os **dados** (o que um objeto _é_, ex: `WeaponData.tres`) do **comportamento** (o que um objeto _faz_, ex: o script no Nó do jogador que usa a arma).
    - **Tópicos a Cobrir:**
      - Criar um script que herda de `Resource` e usa `class_name`.
      - Adicionar propriedades com `@export` ao Recurso.
      - Criar múltiplos arquivos `.tres` a partir do mesmo script de Recurso.
      - Exportar uma variável em um Nó que espera um tipo de Recurso customizado.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de modelar os dados de seu jogo usando `Resource`s customizados, criando uma arquitetura mais flexível e escalável.
    - **Exercício Prático Sugerido:** Criar um `EnemyData.gd` que herda de `Resource` com stats como `health`, `speed`, `damage`. Criar dois arquivos: `slime.tres` e `goblin.tres`, com valores diferentes. Criar uma cena de inimigo cujo script tem `@export var data: EnemyData` e usa esses valores na sua lógica.

  - **1.9: Construção de UI: O Sistema de Layout Retido**

    - **Conceito Central:** Explicar os Nós `Control` como os componentes de um **sistema de GUI de modo retido (retained mode)**. O foco será nos Nós `Container`, que são controladores de layout que executam algoritmos específicos (box layout, grid layout) para organizar seus filhos automaticamente, permitindo a criação de interfaces responsivas que se adaptam a diferentes resoluções e aspect ratios.
    - **Tópicos a Cobrir:**
      - Âncoras e Margens: como os `Control`s se posicionam em relação ao seu pai.
      - `VBoxContainer`, `HBoxContainer`, `GridContainer`, `CenterContainer`.
      - `Size Flags`: como um `Control` se comporta dentro de um `Container` (Fill, Expand, Shrink).
      - O nó `CanvasLayer` para garantir que a UI seja desenhada sobre o jogo.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de construir interfaces de usuário que se adaptam a diferentes tamanhos de tela, utilizando os algoritmos de layout dos containers.
    - **Exercício Prático Sugerido:** Criar um HUD para um jogo. Usar um `MarginContainer` para as bordas, um `HBoxContainer` no topo para informações como Vidas e Pontos, e um `VBoxContainer` no canto para um minimapa ou lista de quests.

  - **1.10: Sistemas de Animação: Keyframing e Máquinas de Estado**

    - **Conceito Central:** Apresentar o `AnimatedSprite2D` como uma simples máquina de estados para animações de sprite. O `AnimationPlayer` será introduzido como um poderoso **motor de tweening e keyframing genérico**, capaz de interpolar qualquer propriedade de qualquer Nó ao longo do tempo. Ele é uma ferramenta de automação de sequências, não apenas de animação visual, podendo chamar métodos, emitir sinais e até animar shaders.
    - **Tópicos a Cobrir:**
      - Criando `SpriteFrames` para o `AnimatedSprite2D`.
      - A timeline do `AnimationPlayer`: adicionando tracks e keyframes.
      - Animando propriedades (`position`, `scale`, `modulate`).
      - Usando a "Call Method Track" para sincronizar código com animações.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de usar ambas as ferramentas para criar animações de personagem e de interface, e sincronizar eventos de gameplay com as animações.
    - **Exercício Prático Sugerido:** Criar uma animação de ataque em um `AnimationPlayer` que move um `Sprite2D` para frente e para trás. Adicionar uma "Call Method Track" que chama uma função `deal_damage` no meio da animação.

  - **1.11: Timers e Áudio: Agendamento de Eventos e Espacialização**

    - **Conceito Central:** Apresentar o `Timer` como uma abstração para o **agendamento de eventos assíncronos**, utilizando o padrão Observer (sinal `timeout`) para notificar a conclusão. Os nós de áudio serão diferenciados pelo conceito de **espacialização**: `AudioStreamPlayer` para áudio global (não-posicional, como música de fundo) e `AudioStreamPlayer2D/3D` para áudio diegético (posicional, como o som de um passo), cuja percepção depende da sua posição no espaço do jogo.
    - **Tópicos a Cobrir:**
      - Configurando `Timer` para `one_shot` (cooldowns) ou repetido (spawners).
      - `Audio Buses`: como rotear e aplicar efeitos a diferentes categorias de som (SFX, Música, Voz).
      - Diferença entre áudio diegético e não-diegético no design de som.
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de usar timers para lógicas baseadas em tempo e implementarmos áudio de forma eficaz, compreendendo os diferentes nós de áudio e seus casos de uso.
    - **Exercício Prático Sugerido:** Criar um spawner de inimigos que usa um `Timer` repetitivo. A cada `timeout`, ele instancia uma cena de inimigo. Adicionar um `AudioStreamPlayer2D` na cena do inimigo para que ele emita um som que pode ser ouvido de perto.

  - **Aula 1.12: A `SceneTree` e Sistemas Globais (Autoloads e Grupos)**

    - **Conceito Central:** Apresentar a `SceneTree` como a classe que gerencia a hierarquia de nós em tempo de execução e o fluxo principal do jogo. Introduzir o padrão de design **Singleton** e sua implementação em Godot, o **Autoload**, como a solução padrão para gerenciar estado e sistemas globais (ex: `GameManager`, `AudioManager`). Apresentar o sistema de **Grupos** como uma ferramenta de desacoplamento para comunicação e gerenciamento de coleções de nós.
    - **Tópicos a Cobrir:**
      - A `SceneTree`: o que é e seu papel no loop do jogo (`get_tree()`).
      - Pausar o jogo (`get_tree().paused`).
      - O padrão Singleton: por que precisamos de acesso global a certos sistemas?
      - Configurando um Autoload no editor de projeto.
      - O sistema de Grupos: adicionando nós a grupos via código (`add_to_group`) e pelo editor.
      - Chamando métodos em todos os nós de um grupo (`get_tree().call_group()`).
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de estruturar a arquitetura de gerenciamento do seu jogo, sabendo quando e por que usar um Autoload e como utilizar Grupos para gerenciar coleções de objetos.
    - **Exercício Prático Sugerido:** Criar um Autoload `Global.gd` que mantém uma variável `score`. Criar uma cena de "moeda" que, ao ser coletada, adiciona-se ao grupo "coins" e chama `Global.add_score()`. Criar um botão na UI que, ao ser pressionado, chama `get_tree().call_group("coins", "queue_free")` para remover todas as moedas da tela.

  - **Aula 1.13: Construção de Mundos com `TileMap`**

    - **Conceito Central:** Apresentar o sistema de `TileMap` como a principal ferramenta para o design de níveis 2D, permitindo a construção rápida e eficiente de layouts complexos a partir de um `TileSet`.
    - **Tópicos a Cobrir:**
      - O que é um `TileMap` e um `TileSet`.
      - Criando um `TileSet` a partir de uma imagem (atlas).
      - Adicionando colisão a tiles individuais (Camada de Física).
      - Usando o "pintor" de `TileMap` para construir um nível.
      - Camadas de `TileMap` para organizar elementos (chão, paredes, decoração).
    - **Objetivo de Aprendizagem:** O aluno será capaz de criar um `TileSet` funcional a partir de uma folha de sprites e usar o `TileMap` para construir um nível 2D com colisões físicas.
    - **Exercício Prático Sugerido:** Usando um asset de tileset simples (um quadrado para parede e um para chão), criar um `TileSet`, configurar a colisão para a parede, e construir uma pequena sala fechada com um `TileMap`. Colocar um `CharacterBody2D` dentro para testar as colisões.

  - **Aula 1.14: Câmeras 2D e Viewports**

    - **Conceito Central:** Detalhar o funcionamento da `Camera2D` como a janela do jogador para o mundo do jogo. Explicar suas propriedades essenciais para criar uma experiência visual profissional e polida. Introduzir o `SubViewport` como uma técnica para renderizar uma parte do jogo em uma textura (ex: para um minimapa).
    - **Tópicos a Cobrir:**
      - O papel da `Camera2D` e a propriedade `current`.
      - Movimento suave: `smoothing_enabled` e `smoothing_speed`.
      - Limites da câmera: `limit_left`, `limit_top`, etc., para confinar a visão ao nível.
      - Arrasto (Drag): como fazer a câmera seguir o jogador com uma "folga".
      - Zoom.
      - Introdução ao `SubViewport` e `SubViewportContainer` para a criação de um minimapa básico.
    - **Objetivo de Aprendizagem:** O aluno saberá como configurar uma `Camera2D` para seguir o jogador de forma profissional e entenderá a base para a criação de um minimapa.
    - **Exercício Prático Sugerido:** Adicionar uma `Camera2D` a um `CharacterBody2D` em um nível de `TileMap` grande. Configurar os `limits` da câmera para as bordas do mapa. Experimentar diferentes valores de `smoothing_speed` para ver o efeito no seguimento do jogador.

  - **Aula 1.15: Arquitetura de Comportamento com Máquinas de Estado (FSM)**

    - **Conceito Central:** Apresentar o padrão de design **Máquina de Estados Finitos (FSM)** como a principal arquitetura para gerenciar comportamentos complexos e excludentes em entidades de jogo (jogador, IA). Diferenciar de uma FSM visual (como `AnimationPlayer`) para uma FSM implementada em código para máxima flexibilidade.
    - **Tópicos a Cobrir:**
      - O problema: por que `if/elif/else` aninhados se tornam insustentáveis para gerenciar estados (ex: `is_jumping`, `is_attacking`, `is_dashing`).
      - A solução: o padrão FSM com Estados e Transições.
      - Implementação em Godot: a classe `State.gd` base (com funções virtuais `enter`, `exit`, `process`).
      - O nó `StateMachine.gd` que gerencia o estado atual e as transições.
      - Exemplo teórico de uma FSM para um personagem simples (Idle, Walk, Jump).
    - **Objetivo de Aprendizagem:** O aluno deve ser capaz de explicar o que é uma FSM, por que ela é usada, e entender a estrutura de código para implementar uma em GDScript.
    - **Exercício Prático Sugerido:** Criar os scripts `State.gd` e `StateMachine.gd`. Criar dois estados simples (`LightOnState.gd`, `LightOffState.gd`) que apenas imprimem mensagens no console. Criar uma cena com um `StateMachine` e os dois estados, e um `Button` que chama `state_machine.transition_to()` para alternar entre os estados.

  - **Aula 1.16: Efeitos Visuais com Sistemas de Partículas**

    - **Conceito Central:** Introduzir o nó `GPUParticles2D` como a ferramenta de alta performance da Godot para criar "juice" e feedback visual através de efeitos de partículas (fogo, fumaça, explosões, brilhos mágicos).
    - **Tópicos a Cobrir:**
      - O que são partículas e por que usar a GPU para processá-las.
      - Configurando um `GPUParticles2D`: `amount`, `lifetime`, `one_shot`.
      - O `Process Material`: definindo o comportamento das partículas (direção, velocidade, gravidade).
      - Modificando a aparência ao longo do tempo: `Color Ramp`, `Scale Curve`.
    - **Objetivo de Aprendizagem:** O aluno será capaz de configurar um `GPUParticles2D` para criar efeitos visuais simples e estilizados.
    - **Exercício Prático Sugerido:** Criar três cenas de efeitos de partículas: uma explosão simples que é `one_shot`, um rastro de fumaça contínuo, e um efeito de "power-up" com partículas que sobem lentamente.

  - **Aula 1.17: Animação Avançada com `AnimationTree`**

    - **Conceito Central:** Apresentar a `AnimationTree` como a ferramenta de nível profissional para gerenciar animações complexas de personagens, permitindo transições suaves e lógicas entre diferentes clipes de animação do `AnimationPlayer`.
    - **Tópicos a Cobrir:**
      - Por que o `AnimationPlayer` sozinho não é suficiente para personagens complexos.
      - A `AnimationTree` como um controlador para o `AnimationPlayer`.
      - O `AnimationNodeStateMachine`: criando uma FSM visual para transições de animação (ex: Idle -> Walk -> Attack).
      - Condições de transição (ex: `travel()` se `speed > 0`).
      - Introdução ao `AnimationNodeBlendSpace2D` para animações direcionais (misturar walk_up, walk_down, walk_left, walk_right com base no input).
    - **Objetivo de Aprendizagem:** O aluno entenderá como e por que usar uma `AnimationTree` para criar um controlador de animação robusto e escalável para um personagem.
    - **Exercício Prático Sugerido:** Pegar um `AnimationPlayer` com animações de "Idle" e "Walk". Criar uma `AnimationTree` e uma `AnimationNodeStateMachine` para fazer a transição entre as duas animações com base em uma variável `is_moving`.

  - **Aula 1.18: Sistemas de Inventário Orientado a Dados**

    - **Conceito Central:** Apresentar a arquitetura de um sistema de inventário simples, onde os itens são `Resource`s e a lógica de gerenciamento é centralizada. Focar na separação entre os dados do item (`ItemResource`) e os dados do inventário (a lista de itens que o jogador possui).
    - **Tópicos a Cobrir:**
      - Revisão do `ItemResource`: `id`, `name`, `texture`, `stackable`.
      - Estrutura de dados do inventário: Um Array de Dicionários `[{"item": ItemResource, "quantity": int}]`.
      - Lógica do `InventoryManager`: Funções teóricas para `add_item`, `remove_item`, `find_stack`, `find_empty_slot`.
      - A importância do sinal `inventory_changed` para desacoplar a lógica da UI.
    - **Objetivo de Aprendizagem:** O aluno entenderá a arquitetura de dados e a lógica por trás de um sistema de inventário modular.
    - **Exercício Prático Sugerido:** Criar um `ItemResource` para "Poção" e "Moeda". Criar um script `Inventory.gd` (não um Autoload ainda) com um array e funções `add_item`/`remove_item`. Usar botões na UI para chamar essas funções e imprimir o conteúdo do array no console para verificar a lógica.

  - **Aula 1.19: UI de Inventário e a Hotbar**
    - **Conceito Central:** Ensinar como criar uma interface de usuário (UI) que representa visualmente os dados de um sistema de inventário. Introduzir o conceito de **Hotbar** como um componente de UI comum para acesso rápido a itens.
    - **Tópicos a Cobrir:**
      - Usando um `GridContainer` para criar a grade do inventário.
      - Criando uma cena de "Slot" reutilizável (`InventorySlot.tscn`).
      - Conectando a UI ao sinal `inventory_changed` do `InventoryManager` para se atualizar automaticamente.
      - A Hotbar: Uma grade menor na HUD principal.
      - Vinculando a Hotbar ao `InputMap`: Associando as ações "hotbar_1", "hotbar_2", etc., às teclas numéricas.
      - Lógica para "selecionar" um slot na hotbar e usar o item correspondente.
    - **Objetivo de Aprendizagem:** O aluno será capaz de construir uma UI de inventário reativa e implementar uma hotbar funcional para acesso rápido a itens.
    - **Exercício Prático Sugerido:** Criar uma cena `InventoryGrid.tscn` que gera `Button`s em um `GridContainer`. Criar uma cena `Hotbar.tscn` com 5 `Button`s em um `HBoxContainer`. Fazer com que pressionar a tecla "1" imprima "Selecionado Slot 1".

---

## **Módulo 02: O Laboratório de Mecânicas: Construindo seu Primeiro Jogo**

- **Filosofia do Módulo:** Em vez de criar um jogo específico, vamos construir um "Laboratório de Testes". Esta é a nossa sandbox, onde cada aula adiciona uma nova mecânica interativa. Essa abordagem espelha o processo real de desenvolvimento: prototipar, testar e refinar sistemas de forma isolada antes de integrá-los em um jogo completo.

- **Aulas:**

  - **Aula 2.1: Setup do Ambiente com TileMaps**

    - **Conceito Central:** Estruturação de um nível 2D usando o sistema de TileMap da Godot.
    - **Projeto:** Criar a cena "Laboratorio.tscn". Desenvolver um `TileSet` com texturas de chão e parede, definindo suas propriedades de colisão. "Pintar" a arena do laboratório.
    - **Objetivo de Aprendizagem:** O aluno será capaz de criar e configurar um `TileSet` para construir níveis 2D de forma eficiente.

  - **Aula 2.2: O Player e o Input Básico**

    - **Conceito Central:** Implementar um personagem controlável, traduzindo input do teclado em movimento e dando feedback visual com animações simples.
    - **Projeto:** Criar a cena `Player.tscn` (`CharacterBody2D`). Configurar o `InputMap` para movimento. Implementar o movimento top-down com `move_and_slide()`. Usar um `AnimatedSprite2D` para animações de "Idle" e "Walk".
    - **Objetivo de Aprendizagem:** O aluno dominará o padrão de código para um `CharacterBody2D` e saberá como gerenciar estados de animação simples.

  - **Aula 2.3: Câmera 2D Suave e com Limites**

    - **Conceito Central:** Configurar uma câmera que segue o jogador de forma profissional, com movimento suave e restrita aos limites do nível.
    - **Projeto:** Adicionar uma `Camera2D` à cena do Player. Habilitar o `smoothing` para um seguimento fluido e definir os `limits` da câmera com base no tamanho do `TileMap`.
    - **Objetivo de Aprendizagem:** O aluno saberá como usar e configurar uma `Camera2D` para criar uma experiência de jogo polida.

  - **Aula 2.4: O Alvo Estático (Dummy) e Feedback de Dano com `FloatingTextManager`**

    - **Conceito Central:** Criar a primeira entidade interativa e fornecer feedback visual imediato para as ações do jogador usando um sistema de texto flutuante gerenciado globalmente.
    - **Projeto:** Criar a cena `Dummy.tscn` (`StaticBody2D`). Criar a cena `FloatingText.tscn` e o Autoload `FloatingTextManager.gd`. O Dummy, ao ser atingido, chamará `FloatingTextManager.show_damage_text()` para instanciar o texto no local do dano.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a instanciar cenas para efeitos visuais, a usar `Tween` para animações procedurais e a criar um sistema de feedback reutilizável.

  - **Aula 2.5: Arquitetura de Armas com `Resource`**

    - **Conceito Central:** Introduzir o Design Orientado a Dados, separando os dados da arma (dano, velocidade do projétil) de sua lógica.
    - **Projeto:** Criar um script `WeaponData.gd` que herda de `Resource`. Criar os arquivos `pistol.tres` e `rifle.tres` com stats diferentes. O Player terá uma variável `@export var weapon: WeaponData`.
    - **Objetivo de Aprendizagem:** O aluno entenderá o conceito e a vantagem de usar `Resource`s para definir e gerenciar os dados do jogo.

  - **Aula 2.6: Sistema de Tiro e Filtragem de Colisão**

    - **Conceito Central:** Instanciar projéteis e usar o sistema de camadas de física para controlar precisamente o que pode atingir o quê.
    - **Projeto:** Criar a cena `Bullet.tscn` (`Area2D`). O Player, ao atirar, instancia a bala usando os dados da `WeaponData` atual. Configurar `CollisionLayer` e `CollisionMask` para que a bala do jogador só interaja com inimigos.
    - **Objetivo de Aprendizagem:** O aluno dominará a instanciação de cenas e a configuração do sistema de física para criar interações de combate robustas.

  - **Aula 2.7: Setup dos Sistemas Globais (Autoloads)**

    - **Conceito Central:** Estruturar a arquitetura de Autoloads para gerenciar o estado, cenas, áudio e configurações de forma global e desacoplada.
    - **Projeto:** Configurar os Autoloads essenciais: `GameManager.gd` (para estado e flags de progresso), `AudioManager.gd`, `SceneManager.gd` (para transições de cena) e `SettingsManager.gd` (para configurações futuras).
    - **Objetivo de Aprendizagem:** O aluno aprenderá a estruturar um projeto com singletons para gerenciar sistemas globais, formando a espinha dorsal da arquitetura do jogo.

  - **Aula 2.8: Coletáveis e o `InventoryManager`**

    - **Conceito Central:** Criar um objeto que pode ser coletado e um sistema de inventário para armazená-lo.
    - **Projeto:** Criar o Autoload `InventoryManager.gd`. Criar a cena `HealthPack.tscn` (`Area2D`). Ao ser coletado pelo Player, o item chama `InventoryManager.add_item()` e desaparece. O item pode ter um cooldown de respawn usando um `Timer`.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a criar um sistema de inventário baseado em dados e a gerenciar o ciclo de vida de objetos coletáveis.

  - **Aula 2.9: Construindo a HUD: Barra de Vida e Hotbar**

    - **Conceito Central:** Construir a interface principal do jogo e conectá-la aos sistemas globais para exibir dados em tempo real.
    - **Projeto:** Criar a cena `HUD.tscn` (`CanvasLayer`). Adicionar uma barra de vida que se atualiza com sinais do `GameManager`. Criar uma `HotbarUI` que se conecta ao `InventoryManager.inventory_changed` para exibir os itens coletados.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a criar uma interface de usuário reativa que reflete o estado do jogo, conectando a UI a diferentes gerenciadores.

  - **Aula 2.10: Sistema de Loot com `LootSystem`**

    - **Conceito Central:** Fazer um inimigo "dropar" itens colecionáveis de forma organizada e baseada em dados, usando uma tabela de loot.
    - **Projeto:** Criar os `Resource`s `LootTable.gd` e `LootItem.gd`. Criar o Autoload `LootSystem.gd`. Ao ser destruído, o Dummy usará o `LootSystem` para processar sua `LootTable` e instanciar os drops (ex: `Coin.tscn`).
    - **Objetivo de Aprendizagem:** O aluno aprenderá a criar um sistema de loot ponderado, orientado a dados, para gerenciar as recompensas do jogo.

  - **Aula 2.11: Desbloqueio de Itens com Flags no `GameManager`**

    - **Conceito Central:** Criar um item no mundo que desbloqueia permanentemente uma nova opção para o jogador, salvando esse progresso em um gerenciador de estado global.
    - **Projeto:** Criar a cena `WeaponPickup.tscn` que exporta uma `WeaponData`. Colocar uma instância no laboratório com o `rifle.tres`. Ao coletar, o `GameManager` define uma flag de progresso (ex: `game_progress["rifle_unlocked"] = true`).
    - **Objetivo de Aprendizagem:** O aluno aprenderá a usar um gerenciador de estado central para rastrear e persistir o progresso e os desbloqueios do jogador.

  - **Aula 2.12: Troca de Armas e Hotbar Funcional**

    - **Conceito Central:** Implementar a lógica de troca entre as armas desbloqueadas, usando a Hotbar como interface visual e funcional.
    - **Projeto:** Implementar a troca de armas no Player (ex: com a roda do mouse ou teclas numéricas). O Player emite um sinal `weapon_switched`. A HUD ouve este sinal para destacar o slot ativo na Hotbar e exibir o nome da arma.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a criar uma UI interativa e a usar sinais para manter múltiplos sistemas (Player, HUD, GameManager) sincronizados.

  - **Aula 2.13: O Inimigo Móvel (A Abordagem Direta)**

    - **Conceito Central:** Criar um adversário com comportamento autônomo, implementando a lógica de movimento e ataque diretamente no script.
    - **Projeto:** Criar a cena `MobileEnemy.tscn` (`CharacterBody2D`) e seu script. A lógica de patrulha e tiro é codificada diretamente no script, misturando dados e comportamento.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a criar uma IA funcional de forma rápida, servindo como contraponto para a refatoração seguinte.

  - **Aula 2.14: Unificação e Refatoração (A Arquitetura com `Resource`)**

    - **Conceito Central:** Refatorar os inimigos `Dummy` e `MobileEnemy` em uma única cena `Enemy.tscn`, usando `Resource`s para diferenciar os comportamentos.
    - **Projeto:** Criar `Enemy.tscn` e `Enemy.gd`. Criar `EnemyData.gd` com stats e flags (`can_move`, `can_shoot`). Criar `dummy_data.tres` e `patrol_bot_data.tres`. O script `Enemy.gd` usará o `Resource` para definir seu comportamento.
    - **Objetivo de Aprendizagem:** O aluno entenderá o "porquê" do Design Orientado a Dados, vendo na prática como ele leva a um código mais limpo e reutilizável.

  - **Aula 2.15: Adicionando Inteligência (A Máquina de Estados - FSM)**

    - **Conceito Central:** Evoluir a arquitetura unificada, adicionando uma FSM para criar um comportamento de IA dinâmico (patrulha, perseguição, ataque).
    - **Projeto:** Adicionar a flag `use_fsm` ao `EnemyData.gd` e criar o `hunter_data.tres`. Adicionar um `StateMachine` e os `State`s à cena `Enemy.tscn`. A FSM só será ativada se `data.use_fsm` for verdadeiro.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a implementar uma FSM para gerenciar estados de IA e a usar `Resource`s para ativar sistemas inteiros.

  - **Aula 2.16: Spawner de Alvos e Gerenciamento por Grupos**

    - **Conceito Central:** Criar um sistema que instancia inimigos em intervalos e gerenciá-los como uma coleção usando o sistema de Grupos.
    - **Projeto:** Criar um `Spawner.tscn` que usa um `Timer` para instanciar `Enemy.tscn`. Adicionar cada inimigo ao grupo "alvos". Criar um botão na UI que chama `get_tree().call_group("alvos", "queue_free")` para limpar a arena.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a usar `Timer`s para spawning e o sistema de Grupos para gerenciamento de múltiplos objetos.

  - **Aula 2.17: Gerenciando a Vida do Player e a HUD Completa**

    - **Conceito Central:** Fechar o loop de combate, permitindo que o jogador também receba dano.
    - **Projeto:** Adicionar o sinal `health_changed` ao `GameManager`. Criar uma "Bala de Inimigo" em uma layer diferente. Ajustar as máscaras de colisão para que o Player seja atingido. A HUD se conecta ao `health_changed` para exibir a vida do jogador.
    - **Objetivo de Aprendizagem:** O aluno será capaz de gerenciar o estado completo do jogador e criar uma HUD reativa.

  - **Aula 2.18: O Sistema de Save/Load com `SaveManager`**

    - **Conceito Central:** Persistir o estado do jogo em um arquivo para que o progresso do jogador não seja perdido, usando um gerenciador dedicado.
    - **Projeto:** Implementar o Autoload `SaveManager.gd`. Suas funções `save_game()` e `load_game()` irão orquestrar a coleta de dados de outros sistemas (ex: `GameManager.get_save_data()`, `InventoryManager.get_save_data()`), convertê-los para JSON e usar `FileAccess` para salvar/ler o arquivo.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a criar um sistema de salvamento robusto que interage com múltiplos gerenciadores para persistir o estado completo do jogo.

  - **Aula 2.19: O Sistema de Pause**

    - **Conceito Central:** Implementar uma funcionalidade de pause que congela a ação e exibe um menu.
    - **Projeto:** Criar um `PauseMenu.tscn`. Ao pressionar "Esc", o jogo é pausado (`get_tree().paused = true`) e o menu de pause se torna visível. O menu deve ter seu `process_mode` definido como "When Paused" para continuar funcionando.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a usar a árvore de cenas para pausar o jogo e a gerenciar o processamento de nós individuais durante a pausa.

  - **Aula 2.20: Polimento e "Juice": Feedback Sensorial com Áudio Espacial**

    - **Conceito Central:** Adicionar uma camada de polimento sobre as mecânicas existentes, com foco em feedback audiovisual avançado, incluindo áudio espacial.
    - **Projeto:** Adicionar um `AudioListener2D` à `Camera2D` para que o áudio seja percebido da perspectiva do jogador. No `AudioManager`, usar um `AudioStreamPlayer` para tocar uma música de fundo de baixo volume. Para os efeitos (tiro, impacto), usar `AudioStreamPlayer2D` nas cenas relevantes para que o som seja posicional. Implementar uma função de `camera_shake`. Criar uma cena `HitEffect.tscn` com `GPUParticles2D` e seu próprio som de impacto espacial.
    - **Objetivo de Aprendizagem:** O aluno entenderá a importância do "Game Feel", aprendendo a implementar áudio global (música) e áudio espacial (SFX com `AudioStreamPlayer2D` e `AudioListener2D`), além de efeitos de câmera e partículas.

  - **Aula 2.21: Polimento Final com `AnimationTree`**
    - **Conceito Central:** Elevar a qualidade da animação do personagem, substituindo a lógica manual do `AnimatedSprite2D` por uma `AnimationTree` para gerenciar as transições.
    - **Projeto:** Adicionar um `AnimationPlayer` e uma `AnimationTree` ao Player. Criar uma `AnimationNodeStateMachine` dentro da `AnimationTree` para controlar as transições entre as animações de "Idle" e "Walk" com base na velocidade do jogador.
    - **Objetivo de Aprendizagem:** O aluno aprenderá a usar a ferramenta de animação mais poderosa e escalável da Godot para criar personagens mais vivos e reativos.

---

## **Módulo 03: Desafio: Faça seu Jogo**

---

## **Módulo 04: **

---

## **Módulo 05: Dome Keeper**

---

## **Módulo 06: Desafio: Faça seu Jogo**

---

## **Módulo 07:**

---

## **Módulo 08: Overwath 2D**

---

## \*_Módulo 09: ARPG_

---
