GDScript.md

# GDScript: A Linguagem Nativa da Godot Engine (Godot 4.5.1)


Este documento serve como um guia abrangente e aprofundado sobre o GDScript, a linguagem de script nativa da Godot Engine, com foco nas funcionalidades e melhores práticas da versão Godot 4.5.1. Ele é projetado para ser um recurso completo para desenvolvedores que desejam dominar o GDScript, desde os fundamentos da linguagem até a integração avançada com o motor, otimização de performance e interoperabilidade com outras tecnologias como GDExtension e C++.

## 1. Introdução ao GDScript

### 1.1. O que é GDScript?

GDScript é uma linguagem de script de alto nível, dinamicamente tipada (com tipagem estática opcional), projetada especificamente para a Godot Engine. Sua sintaxe é inspirada em Python, o que a torna extremamente legível, concisa e fácil de aprender, especialmente para desenvolvedores que já possuem familiaridade com Python ou outras linguagens de script.

Desenvolvido desde o início para se integrar perfeitamente com a arquitetura baseada em nós e cenas da Godot, o GDScript oferece acesso direto e sem atritos a todas as classes, métodos, propriedades e sistemas do motor. Isso significa que a experiência de codificação é fluida e intuitiva, permitindo que os desenvolvedores se concentrem na lógica do jogo e na criatividade, em vez de se preocuparem com complexidades de integração ou de baixo nível.

**Características Principais:**

*   **Sintaxe Python-like:** Facilita a leitura e escrita do código.
*   **Integração Nativa:** Acesso direto e otimizado à API da Godot.
*   **Tipagem Estática Opcional:** Permite um equilíbrio entre flexibilidade e robustez, com verificação de erros em tempo de desenvolvimento.
*   **Orientado a Objetos:** Suporta herança, polimorfismo e encapsulamento, alinhando-se com a arquitetura da Godot.
*   **Leve e Eficiente:** Projetado para ser performático dentro do ecossistema Godot.

### 1.2. Por que usar GDScript?

A escolha do GDScript como a linguagem principal para o desenvolvimento de jogos na Godot Engine oferece uma série de vantagens significativas:

*   **Curva de Aprendizado Suave:** Para iniciantes em programação ou para aqueles que vêm de linguagens como Python, o GDScript é incrivelmente acessível. Sua sintaxe limpa e intuitiva permite que você comece a criar jogos rapidamente, focando na lógica e na criatividade.
*   **Produtividade Elevada:** A concisão da sintaxe, a integração nativa com o editor da Godot e os ciclos de iteração rápidos (sem a necessidade de compilação demorada) resultam em um fluxo de trabalho altamente produtivo. Você pode prototipar ideias, testar mecânicas e iterar sobre o design do jogo de forma ágil.
*   **Integração Perfeita com a Godot Engine:** O GDScript foi construído para a Godot. Isso significa que ele se encaixa perfeitamente na arquitetura de nós e cenas do motor. Acessar e manipular elementos da cena, conectar sinais e utilizar as funcionalidades do motor é natural e direto.
*   **Ferramentas de Editor Robustas:** O editor da Godot oferece um suporte excepcional para GDScript, incluindo autocompletar inteligente, depurador integrado, realce de sintaxe, refatoração e documentação contextual. Isso melhora a experiência do desenvolvedor e acelera o processo de codificação.
*   **Comunidade Ativa e Recursos:** Embora seja uma linguagem específica da Godot, a comunidade em torno do GDScript é vibrante e crescente. Há uma vasta quantidade de tutoriais, exemplos, plugins e suporte disponível, facilitando a resolução de problemas e o aprendizado contínuo.
*   **Equilíbrio entre Performance e Facilidade de Uso:** Para a maioria das lógicas de jogo, a performance do GDScript é mais do que suficiente. Quando gargalos de performance são identificados em partes críticas, a Godot oferece a flexibilidade de estender o motor com C++ via GDExtension, permitindo que você otimize apenas o que é estritamente necessário, mantendo a produtividade do GDScript para o restante do projeto.
*   **Scripts de Ferramenta e Plugins de Editor:** O GDScript não se limita à lógica de jogo em tempo de execução. Ele pode ser usado para criar scripts de ferramenta que rodam no editor, automatizando tarefas, e para desenvolver plugins de editor completos, estendendo a funcionalidade da Godot para atender às suas necessidades específicas.

### 1.3. Comparação com outras linguagens (Blueprints, C++, C#, Rust, Java, GML, Python)

A Godot Engine oferece flexibilidade na escolha da linguagem de script, embora o GDScript seja a opção nativa e mais integrada. Comparar o GDScript com outras linguagens populares no desenvolvimento de jogos ajuda a entender seus pontos fortes e fracos, e a determinar a melhor ferramenta para cada cenário.

#### 1.3.1. GDScript vs. Blueprints (Unreal Engine)

| Característica          | GDScript (Godot Engine)                               | Blueprints (Unreal Engine)                                  |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de script visual baseada em nós                   |
| **Público-alvo**        | Programadores, desenvolvedores de jogos               | Designers, artistas, não-programadores, programadores       |
| **Facilidade de Uso**   | Alta para quem conhece Python; boa para iniciantes    | Alta para não-programadores; visualmente intuitivo          |
| **Performance**         | Boa; pode ser estendida com C++ (GDExtension)         | Excelente; compilado para C++                               |
| **Integração**          | Nativa e profunda com a API da Godot                  | Nativa e profunda com a API da Unreal                       |
| **Prototipagem**        | Rápida, especialmente para lógica de jogo             | Muito rápida, ideal para testar mecânicas                   |
| **Manutenção/Escala**   | Geralmente mais fácil de ler e manter em larga escala | Pode se tornar complexo e difícil de navegar em larga escala |
| **Controle de Versão**  | Fácil (arquivos de texto)                             | Desafiador (arquivos binários)                              |
| **Extensibilidade**     | C++ via GDExtension                                   | C++ (para criar novos nós ou lógica de base)                |
| **Depuração**           | Debugger textual padrão                               | Debugger visual com fluxo de execução                       |

**Conclusão:** GDScript oferece controle preciso e facilidade de manutenção para programadores, enquanto Blueprints capacitam não-programadores com uma abordagem visual e performance quase nativa. A escolha depende da preferência da equipe e da complexidade do projeto.

#### 1.3.2. GDScript vs. C++

| Característica          | GDScript (Godot Engine)                               | C++ (via GDExtension)                                       |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de programação compilada de baixo nível           |
| **Curva de Aprendizado**| Suave, ideal para iniciantes                          | Íngreme, exige conhecimento de gerenciamento de memória     |
| **Produtividade**       | Alta, ciclos de iteração rápidos                      | Menor para lógica geral, compilação mais lenta              |
| **Performance**         | Boa para a maioria dos casos, interpretada            | Máxima, compilada para código de máquina                    |
| **Controle de Baixo Nível**| Limitado                                            | Total, acesso direto a hardware e memória                   |
| **Integração com Godot**| Nativa e profunda                                     | Nativa e profunda (via GDExtension)                         |
| **Ecossistema**         | Específico da Godot                                   | Vasto, muitas bibliotecas C/C++ de terceiros                |
| **Gerenciamento de Memória**| Automático (coletor de lixo)                        | Manual (com ferramentas Godot como `Ref<T>`)                |
| **Uso Recomendado**     | Lógica de jogo geral, UI, prototipagem                | Gargalos de performance, integração de bibliotecas externas |

**Conclusão:** GDScript é a escolha padrão para produtividade e facilidade de uso na Godot. C++ via GDExtension é reservado para otimizações críticas de performance e integração de baixo nível, sendo a abordagem híbrida a mais eficaz.

#### 1.3.3. GDScript vs. C#

| Característica          | GDScript (Godot Engine)                               | C# (Godot Engine com Mono)                                  |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de programação compilada (JIT)                    |
| **Curva de Aprendizado**| Suave, concisa                                        | Moderada, familiar para devs Unity                          |
| **Produtividade**       | Alta, ciclos de iteração rápidos                      | Boa, mas com passo de compilação                            |
| **Performance**         | Boa, interpretada                                     | Superior para tarefas CPU-bound, compilada JIT              |
| **Ecossistema**         | Específico da Godot                                   | Vasto ecossistema .NET                                      |
| **Tipagem**             | Dinâmica com estática opcional                        | Forte e estática                                            |
| **Tamanho do Executável**| Leve                                                  | Maior (inclui runtime .NET)                                 |
| **Uso Recomendado**     | Lógica de jogo geral, UI, prototipagem                | Lógica complexa, alta performance, acesso a libs .NET       |

**Conclusão:** GDScript é ideal para agilidade e integração nativa. C# oferece performance superior para tarefas CPU-bound e acesso a um ecossistema robusto, sendo uma boa opção para desenvolvedores familiarizados com .NET ou projetos que exigem mais poder computacional.

#### 1.3.4. GDScript vs. Rust

| Característica          | GDScript (Godot Engine)                               | Rust (via GDExtension)                                      |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de programação de sistema compilada               |
| **Curva de Aprendizado**| Suave                                                 | Muito íngreme (ownership, borrowing)                        |
| **Produtividade**       | Alta, prototipagem rápida                             | Menor inicialmente, mas alta segurança e performance        |
| **Performance**         | Boa, interpretada                                     | Inigualável, compilada para código de máquina               |
| **Segurança**           | Boa, com tipagem opcional                             | Excepcional (garantias de memória em tempo de compilação)   |
| **Controle de Baixo Nível**| Limitado                                            | Total, sem garbage collector                                |
| **Uso Recomendado**     | Lógica de jogo geral, UI                              | Partes críticas de performance, segurança, plugins          |

**Conclusão:** GDScript é para a maior parte da lógica de jogo, priorizando a produtividade. Rust, via GDExtension, é para cenários onde performance máxima e segurança de memória são absolutas prioridades, como em sistemas complexos ou plugins de motor.

#### 1.3.5. GDScript vs. Java

| Característica          | GDScript (Godot Engine)                               | Java (Geral, com frameworks de jogo)                        |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de programação compilada (JIT)                    |
| **Curva de Aprendizado**| Suave, concisa                                        | Moderada, verbosa                                           |
| **Produtividade**       | Alta, integração nativa Godot                         | Boa, mas com overhead da JVM e verbosidade                  |
| **Performance**         | Boa, interpretada                                     | Alta (com JIT), mas com pausas do GC                        |
| **Ecossistema**         | Específico da Godot                                   | Vasto e maduro (propósito geral)                            |
| **Portabilidade**       | Excelente (Godot exporta para várias plataformas)     | Excelente (JVM - "Write Once, Run Anywhere")                |
| **Gerenciamento de Memória**| Automático (coletor de lixo)                        | Automático (coletor de lixo, com potenciais pausas)         |
| **Uso Recomendado**     | Lógica de jogo geral, UI, prototipagem                | Desenvolvimento Android, frameworks como LibGDX             |

**Conclusão:** GDScript é a escolha mais integrada e produtiva para a Godot. Java é uma linguagem de propósito geral com um ecossistema enorme e boa performance, mas sua integração com motores de jogo visuais como a Godot não é nativa, exigindo frameworks externos.

#### 1.3.6. GDScript vs. GML (GameMaker Language)

| Característica          | GDScript (Godot Engine)                               | GML (GameMaker Studio)                                      |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de script textual (C/JS-like)                     |
| **Filosofia do Motor**  | Arquitetura de Nós e Cenas (Composição)               | Arquitetura de Objetos e Eventos (Mais Procedural)          |
| **Curva de Aprendizado**| Suave, legível                                        | Suave, direta para 2D                                       |
| **Produtividade**       | Alta, integração Godot                                | Alta, especialmente para 2D                                 |
| **Extensibilidade**     | C++ via GDExtension                                   | DLLs/Bibliotecas Nativas (menos transparente)               |
| **Orientação a Objetos**| Forte, explícita                                      | Mais procedural, com herança de objetos                     |
| **Foco Principal**      | Jogos 2D e 3D                                         | Principalmente jogos 2D                                     |
| **Open Source**         | Sim (Godot Engine)                                    | Não (GameMaker Studio é comercial)                          |

**Conclusão:** GDScript, com a Godot, oferece uma abordagem mais moderna e orientada a objetos para jogos 2D e 3D, com alta extensibilidade. GML, com GameMaker, é excelente para simplicidade e rapidez no desenvolvimento de jogos 2D, sendo uma ótima porta de entrada.

#### 1.3.7. GDScript vs. Python

| Característica          | GDScript (Godot Engine)                               | Python (Geral, com bibliotecas de jogo)                     |
| :---------------------- | :---------------------------------------------------- | :---------------------------------------------------------- |
| **Tipo**                | Linguagem de script textual (Python-like)             | Linguagem de programação de propósito geral                 |
| **Integração com Motor**| Nativa e profunda com Godot                           | Não nativa com Godot (requer bindings de terceiros)         |
| **Curva de Aprendizado**| Suave, familiar para usuários Python                  | Suave, muito popular                                        |
| **Ecossistema**         | Específico da Godot                                   | Vasto e maduro (propósito geral, Pygame, Panda3D)           |
| **Performance**         | Otimizada para Godot, interpretada                    | Interpretada, GIL pode limitar paralelismo                  |
| **Ferramentas de Editor**| Integradas na Godot                                   | Ferramentas externas (IDEs Python)                          |
| **Distribuição de Jogos**| Otimizada pela Godot                                  | Mais complexa (empacotamento de Python)                     |
| **Uso Recomendado**     | Lógica de jogo geral na Godot                         | Ferramentas de pipeline, backend, jogos com Pygame/Arcade   |

**Conclusão:** GDScript é a escolha superior para lógica de jogo *dentro* da Godot Engine devido à sua integração nativa e otimização. Python é uma linguagem de propósito geral poderosa para ferramentas auxiliares, backend ou jogos desenvolvidos com bibliotecas Python dedicadas, mas não se integra diretamente com a Godot de forma nativa.

### 1.4. Histórico e Evolução do GDScript (GDScript 1.x vs GDScript 2.x)

O GDScript passou por uma evolução significativa entre as versões 1.x (utilizada na Godot 3.x) e 2.x (introduzida na Godot 4.x). Embora "GDScript 2" seja um termo informal, ele encapsula as melhorias e mudanças que tornaram a linguagem mais robusta, flexível e alinhada com a arquitetura renovada da Godot 4.

#### 1.4.1. GDScript 1.x (Godot 3.x)

Na Godot 3.x, o GDScript já era uma linguagem poderosa e fácil de usar, com sintaxe Python-like e forte integração com o motor. Suas principais características incluíam:

*   **Sintaxe Simples:** Foco na legibilidade e facilidade de aprendizado.
*   **Tipagem Dinâmica:** Flexibilidade para não declarar tipos explicitamente.
*   **Sistema de Sinais e `yield`:** Utilização de strings para conectar sinais e a palavra-chave `yield` para operações assíncronas.
*   **`export` Keyword:** Para expor variáveis no Inspector.
*   **Herança de Funções de Ciclo de Vida Implícita:** Funções como `_ready()` e `_process()` eram chamadas automaticamente na superclasse.

#### 1.4.2. GDScript 2.x (Godot 4.x)

O GDScript 2.x representa uma modernização da linguagem, introduzindo recursos que melhoram a segurança de tipo, a expressividade e a performance, ao mesmo tempo em que mantém a familiaridade e a facilidade de uso. As mudanças mais notáveis incluem:

*   **Tipagem Estática Opcional Aprimorada:** Embora já presente em GDScript 1.x, a tipagem estática foi significativamente aprimorada no GDScript 2.x, tornando-a mais robusta e incentivando seu uso para melhor detecção de erros, autocompletar e otimizações de performance.
*   **Anotações (`@`) para Exportação e Propriedades:** A palavra-chave `export` foi substituída por anotações como `@export`, `@export_range`, `@export_file`, etc. Isso torna a declaração mais clara e permite hints mais específicos no Inspector.
    *   **Exemplo:**
        ```gdscript
        # GDScript 1.x
        export var speed = 100.0

        # GDScript 2.x
        @export var speed: float = 100.0
        @export_range(0, 100, 1, "suffix:HP") var health: int = 50
        ```
*   **`Callable`s e Funções de Primeira Classe:** A conexão de sinais e operações assíncronas foi modernizada com a introdução de `Callable`s. Agora, funções podem ser tratadas como objetos, passadas como argumentos e armazenadas em variáveis.
    *   **Conexão de Sinais:**
        ```gdscript
        # GDScript 1.x
        connect("signal_name", self, "function_name", [arg1, arg2])

        # GDScript 2.x
        signal_name.connect(my_object.my_function.bind(arg1, arg2))
        ```
    *   **`await` (Substituindo `yield`):** A palavra-chave `yield` foi substituída por `await`, que é mais intuitiva e alinhada com padrões de programação assíncrona modernos.
        ```gdscript
        # GDScript 1.x
        yield(get_tree().create_timer(1.0), "timeout")

        # GDScript 2.x
        await get_tree().create_timer(1.0).timeout
        ```
*   **Funções Lambda (Funções Anônimas):** Permite a criação de funções pequenas e concisas diretamente onde são usadas, melhorando a expressividade do código.
    *   **Exemplo:**
        ```gdscript
        button.pressed.connect(func(): print("Botão pressionado!"))
        ```
*   **Palavra-chave `super`:** Para chamar métodos da classe pai, a sintaxe `.` foi substituída por `super`. Isso torna a intenção mais clara e evita ambiguidades.
    *   **Exemplo:**
        ```gdscript
        # GDScript 1.x
        func _ready():
            . _ready() # Chama o _ready da classe pai

        # GDScript 2.x
        func _ready():
            super._ready() # Chama o _ready da classe pai
        ```
*   **Herança de Funções de Ciclo de Vida Explícita:** No GDScript 2.x, as funções de ciclo de vida (`_ready`, `_process`, etc.) na classe pai não são mais chamadas implicitamente. É necessário usar `super._ready()` (ou similar) para garantir que a lógica da superclasse seja executada.
*   **Sintaxe de Propriedades (Setters e Getters):** A sintaxe para definir setters e getters foi simplificada, permitindo que a lógica seja definida diretamente ao lado da declaração da variável.
    *   **Exemplo:**
        ```gdscript
        var _health: int = 100:
            set(value):
                _health = value
                print("Vida alterada para: ", _health)
            get:
                return _health
        ```
*   **Arrays Tipados:** Possibilidade de declarar arrays que só podem conter elementos de um tipo específico, aumentando a segurança de tipo.
    *   **Exemplo:**
        ```gdscript
        var enemies: Array[CharacterBody2D] = []
        ```
*   **Comentários de Documentação (`##`):** Uma nova sintaxe para gerar documentação automaticamente, visível no editor e com suporte a BBCode.
*   **Novo Sistema de Tween:** O sistema de `Tween` foi reescrito, tornando-o mais flexível e poderoso.
*   **Y-sorting Integrado:** A funcionalidade de ordenação Y foi integrada diretamente na classe `CanvasItem`, eliminando a necessidade do nó `YSort` dedicado.

Essas mudanças no GDScript 2.x visam tornar a linguagem mais moderna, segura, performática e agradável de usar, alinhando-a com as capacidades e a arquitetura avançada da Godot 4.x.

---

## 2. Fundamentos da Linguagem

### 2.1. Sintaxe Básica e Convenções

A sintaxe do GDScript é projetada para ser limpa, legível e concisa, inspirada fortemente no Python. Isso facilita o aprendizado e a manutenção do código.

#### 2.1.1. Indentação e Blocos de Código

Assim como no Python, o GDScript utiliza a **indentação** para definir blocos de código, em vez de chaves `{}` ou palavras-chave `end`. Uma indentação consistente é crucial para a estrutura e a execução correta do código. Recomenda-se usar **quatro espaços** para cada nível de indentação.

**Exemplo:**

```gdscript
func my_function():
    # Este é um bloco de código indentado
    if true:
        # Este é outro bloco de código indentado
        print("Bloco interno")
    print("Bloco externo")
```

#### 2.1.2. Comentários

Comentários são essenciais para explicar a lógica do código, a intenção por trás de certas decisões e para tornar o código mais compreensível para outros desenvolvedores (e para você mesmo no futuro).

*   **Comentários de Linha Única:** Começam com `#`.
    ```gdscript
    # Este é um comentário de linha única
    var health = 100 # A vida inicial do jogador
    ```
*   **Comentários de Múltiplas Linhas:** Não há um bloco de comentário dedicado como `/* ... */` em C++. Para comentários de múltiplas linhas, você pode usar múltiplas linhas com `#` ou strings de múltiplas linhas (docstrings) para documentação de funções/classes.
    ```gdscript
    # Este é um comentário
    # que ocupa
    # múltiplas linhas.
    ```
*   **Comentários de Documentação (`##` - GDScript 2.x):** Introduzidos no GDScript 2.x, permitem gerar documentação automaticamente para classes, funções e variáveis. Suportam formatação BBCode.

    **Exemplo:**
    ```gdscript
    ## Esta é uma classe de exemplo para demonstrar comentários de documentação.
    ## Pode conter [b]formatação BBCode[/b] e múltiplas linhas.
    class_name MyDocumentedClass extends Node

    ## A vida atual do jogador.
    ## [code]var health: int = 100[/code]
    @export var health: int = 100

    ## Calcula o dano recebido pelo jogador.
    ## @param amount: A quantidade de dano a ser aplicada.
    ## @returns: A nova vida do jogador após o dano.
    func take_damage(amount: int) -> int:
        health -= amount
        return health
    ```

#### 2.1.3. Variáveis e Constantes

*   **Variáveis:** Usadas para armazenar dados que podem mudar durante a execução do programa. Declaradas com a palavra-chave `var`.
    ```gdscript
    var player_name = "Hero"
    var score = 0
    var is_game_over = false
    ```
*   **Constantes:** Usadas para armazenar dados que não devem mudar após a inicialização. Declaradas com a palavra-chave `const`. Por convenção, nomes de constantes são geralmente em `SCREAMING_SNAKE_CASE`.
    ```gdscript
    const MAX_SPEED = 200
    const GRAVITY = 9.8
    const PI = 3.14159
    ```

#### 2.1.4. Tipos de Dados (Built-in Types)

O GDScript possui uma variedade de tipos de dados embutidos para lidar com diferentes tipos de informações.

##### 2.1.4.1. Números (`int`, `float`)

*   **`int` (Inteiro):** Números inteiros (sem casas decimais).
    ```gdscript
    var enemy_count: int = 10
    var player_level: int = 1
    ```
*   **`float` (Ponto Flutuante):** Números com casas decimais.
    ```gdscript
    var player_speed: float = 150.5
    var game_time: float = 0.0
    ```

##### 2.1.4.2. Booleanos (`bool`)

Representam valores verdadeiros ou falsos. `true` ou `false`.

```gdscript
var is_player_alive: bool = true
var has_key: bool = false
```

##### 2.1.4.3. Strings (`String`)

Sequências de caracteres. Podem ser declaradas com aspas simples (`'`) ou duplas (`"`).

```gdscript
var greeting: String = "Olá, mundo!"
var item_name: String = 'Espada Longa'
```

*   **Concatenação:**
    ```gdscript
    var full_message = "Seu nome é " + player_name
    ```
*   **Formatação (f-strings - GDScript 2.x):** Similar às f-strings do Python, permite incorporar expressões diretamente em strings.
    ```gdscript
    var player_name = "Machi"
    var score = 1230
    var message = "Jogador: {player_name}, Pontuação: {score}".format({"player_name": player_name, "score": score})
    print(message) # Saída: Jogador: Machi, Pontuação: 1230

    # Ou usando o atalho % (mais antigo, mas ainda funcional)
    var message_old = "Jogador: %s, Pontuação: %d" % [player_name, score]
    print(message_old)
    ```

##### 2.1.4.4. Coleções (`Array`, `Dictionary`)

*   **`Array` (Lista):** Coleção ordenada de elementos. Pode conter elementos de diferentes tipos (ou ser tipado no GDScript 2.x).
    ```gdscript
    var inventory: Array = ["Espada", "Escudo", "Poção"]
    var positions: Array[Vector2] = [Vector2(0,0), Vector2(10,10)] # Array tipado (GDScript 2.x)
    ```
*   **`Dictionary` (Dicionário):** Coleção não ordenada de pares chave-valor. As chaves devem ser únicas.
    ```gdscript
    var player_stats: Dictionary = {
        "strength": 10,
        "dexterity": 8,
        "intelligence": 12
    }
    var item_properties: Dictionary = {
        "name": "Anel de Poder",
        "effect": "Aumenta Força",
        "value": 50
    }
    ```

##### 2.1.4.5. Vetores e Transformações (`Vector2`, `Vector3`, `Transform2D`, `Transform3D`)

Tipos essenciais para matemática de jogos, representando posições, direções, escalas e rotações.

*   **`Vector2`:** Vetor 2D (x, y).
    ```gdscript
    var player_position: Vector2 = Vector2(100, 200)
    var direction: Vector2 = Vector2(1, 0).normalized() # Vetor normalizado
    ```
*   **`Vector3`:** Vetor 3D (x, y, z).
    ```gdscript
    var camera_target: Vector3 = Vector3(0, 5, -10)
    var up_vector: Vector3 = Vector3.UP # Constante embutida
    ```
*   **`Transform2D`:** Representa uma transformação 2D (posição, rotação, escala).
*   **`Transform3D`:** Representa uma transformação 3D (posição, rotação, escala).

##### 2.1.4.6. Cores (`Color`)

Representa cores no formato RGBA (Vermelho, Verde, Azul, Alpha).

```gdscript
var red_color: Color = Color(1, 0, 0) # Vermelho puro
var transparent_blue: Color = Color(0, 0, 1, 0.5) # Azul com 50% de transparência
var default_text_color: Color = Color.WHITE # Constante embutida
```

##### 2.1.4.7. Outros tipos úteis (`NodePath`, `RID`, `Callable`, `Signal`)

*   **`NodePath`:** Um caminho para um nó na árvore de cenas. Usado para referenciar nós de forma eficiente.
    ```gdscript
    var player_path: NodePath = "Player"
    var ui_label_path: NodePath = "CanvasLayer/UI/ScoreLabel"
    ```
*   **`RID` (Resource ID):** Identificador de recurso de baixo nível, usado internamente pelo motor para gerenciar recursos. Raramente manipulado diretamente pelo desenvolvedor.
*   **`Callable` (GDScript 2.x):** Um objeto que pode ser chamado, representando uma função ou método. Essencial para o novo sistema de sinais e `await`.
    ```gdscript
    var my_callable: Callable = Callable(self, "my_function")
    my_callable.call()
    ```
*   **`Signal` (GDScript 2.x):** Um objeto que representa um sinal. Usado para conectar e emitir sinais de forma mais robusta.
    ```gdscript
    signal health_changed(new_health: int)
    health_changed.emit(80)
    ```

### 2.2. Operadores

Operadores são símbolos que realizam operações em valores e variáveis.

#### 2.2.1. Aritméticos

| Operador | Descrição        | Exemplo         | Resultado |
| :------- | :--------------- | :-------------- | :-------- |
| `+`      | Adição           | `5 + 3`         | `8`       |
| `-`      | Subtração        | `10 - 4`        | `6`       |
| `*`      | Multiplicação    | `2 * 6`         | `12`      |
| `/`      | Divisão          | `15 / 3`        | `5.0`     |
| `%`      | Módulo (resto)   | `10 % 3`        | `1`       |
| `**`     | Exponenciação    | `2 ** 3`        | `8`       |

#### 2.2.2. Comparação

Retornam um valor booleano (`true` ou `false`).

| Operador | Descrição                | Exemplo         | Resultado |
| :------- | :----------------------- | :-------------- | :-------- |
| `==`     | Igual a                  | `5 == 5`        | `true`    |
| `!=`     | Diferente de             | `10 != 5`       | `true`    |
| `<`      | Menor que                | `7 < 10`        | `true`    |
| `>`      | Maior que                | `12 > 8`        | `true`    |
| `<=`     | Menor ou igual a         | `5 <= 5`        | `true`    |
| `>=`     | Maior ou igual a         | `20 >= 15`      | `true`    |

#### 2.2.3. Lógicos

Usados para combinar expressões booleanas.

| Operador | Descrição | Exemplo                               | Resultado |
| :------- | :-------- | :------------------------------------ | :-------- |
| `and`    | E lógico  | `true and false`                      | `false`   |
| `or`     | Ou lógico | `true or false`                       | `true`    |
| `not`    | Não lógico| `not true`                            | `false`   |

#### 2.2.4. Atribuição

Usados para atribuir valores a variáveis.

| Operador | Descrição                | Exemplo         | Equivalente a |
| :------- | :----------------------- | :-------------- | :------------ |
| `=`      | Atribuição simples       | `x = 10`        | `x = 10`      |
| `+=`     | Adição e atribuição      | `x += 5`        | `x = x + 5`   |
| `-=`     | Subtração e atribuição   | `x -= 2`        | `x = x - 2`   |
| `*=`     | Multiplicação e atribuição| `x *= 3`        | `x = x * 3`   |
| `/=`     | Divisão e atribuição     | `x /= 4`        | `x = x / 4`   |
| `%=`     | Módulo e atribuição      | `x %= 3`        | `x = x % 3`   |
| `**=`    | Exponenciação e atribuição| `x **= 2`       | `x = x ** 2`  |

#### 2.2.5. Bitwise

Operam nos bits individuais de números inteiros.

| Operador | Descrição             | Exemplo         |
| :------- | :-------------------- | :-------------- |
| `&`      | E bit a bit           | `5 & 3` (`0101 & 0011` = `0001` = `1`) |
| `|`      | Ou bit a bit          | `5 | 3` (`0101 | 0011` = `0111` = `7`) |
| `^`      | Ou exclusivo bit a bit| `5 ^ 3` (`0101 ^ 0011` = `0110` = `6`) |
| `~`      | Negação bit a bit     | `~5`            |
| `<<`     | Deslocamento à esquerda| `5 << 1` (`0101 << 1` = `1010` = `10`) |
| `>>`     | Deslocamento à direita | `5 >> 1` (`0101 >> 1` = `0010` = `2`) |

### 2.3. Estruturas de Controle de Fluxo

As estruturas de controle de fluxo determinam a ordem em que as instruções são executadas.

#### 2.3.1. Condicionais (`if`, `elif`, `else`)

Usadas para executar blocos de código com base em condições.

```gdscript
var score = 150

if score >= 1000:
    print("Você é um mestre!")
elif score >= 500:
    print("Você é um veterano!")
elif score >= 100:
    print("Você está indo bem!")
else:
    print("Continue praticando!")
```

#### 2.3.2. Laços de Repetição (`for`, `while`)

Usados para executar um bloco de código repetidamente.

*   **`for` Loop:** Itera sobre uma sequência (Array, String, Range, Dictionary).
    ```gdscript
    var items = ["Espada", "Escudo", "Poção"]
    for item in items:
        print("Item no inventário: ", item)

    for i in range(5): # Itera de 0 a 4
        print("Contagem: ", i)

    var player_stats = {"strength": 10, "dexterity": 8}
    for stat_name in player_stats:
        print("Atributo: %s, Valor: %d" % [stat_name, player_stats[stat_name]])
    ```
*   **`while` Loop:** Repete um bloco de código enquanto uma condição for verdadeira.
    ```gdscript
    var count = 0
    while count < 5:
        print("Contador: ", count)
        count += 1
    ```

#### 2.3.3. Controle de Laço (`break`, `continue`)

*   **`break`:** Termina o laço de repetição imediatamente.
    ```gdscript
    for i in range(10):
        if i == 5:
            break # Sai do loop quando i for 5
        print(i) # Imprime 0, 1, 2, 3, 4
    ```
*   **`continue`:** Pula a iteração atual e vai para a próxima.
    ```gdscript
    for i in range(5):
        if i == 2:
            continue # Pula a iteração quando i for 2
        print(i) # Imprime 0, 1, 3, 4
    ```

#### 2.3.4. Match Statement (GDScript 2.x)

Similar ao `switch` de outras linguagens, mas mais poderoso. Permite comparar um valor com múltiplos padrões.

```gdscript
var player_action = "attack"

match player_action:
    "attack":
        print("Jogador atacou!")
    "defend":
        print("Jogador defendeu!")
    "run":
        print("Jogador correu!")
    _: # Padrão curinga (default)
        print("Ação desconhecida.")

var item_type = "potion"
var item_rarity = "rare"

match [item_type, item_rarity]:
    ["potion", "common"]:
        print("Poção comum encontrada.")
    ["potion", "rare"]:
        print("Poção rara encontrada!")
    ["sword", _]: # Qualquer raridade para espada
        print("Espada encontrada.")
    _:
        print("Item desconhecido.")
```

### 2.4. Funções

Funções são blocos de código reutilizáveis que realizam uma tarefa específica.

#### 2.4.1. Definição e Chamada

*   **Definição:** Usando a palavra-chave `func`.
    ```gdscript
    func greet_player():
        print("Bem-vindo ao jogo!")

    func calculate_damage(base_damage, multiplier):
        return base_damage * multiplier
    ```
*   **Chamada:**
    ```gdscript
    greet_player()
    var final_damage = calculate_damage(10, 1.5)
    print("Dano final: ", final_damage)
    ```

#### 2.4.2. Parâmetros e Valores de Retorno

*   **Parâmetros:** Valores passados para a função.
*   **Valores de Retorno:** Valores que a função retorna usando a palavra-chave `return`.
    ```gdscript
    func add_numbers(a: int, b: int) -> int: # Com tipagem estática
        return a + b

    var sum = add_numbers(5, 7)
    print("Soma: ", sum)
    ```

#### 2.4.3. Funções Anônimas (Lambdas - GDScript 2.x)

Funções sem nome que podem ser definidas e usadas inline. Úteis para callbacks curtos ou para passar como argumentos.

```gdscript
# Conectando um sinal a uma função lambda
button.pressed.connect(func():
    print("Botão pressionado!")
    get_tree().quit()
)

# Usando lambda em um Array.map
var numbers = [1, 2, 3]
var squared_numbers = numbers.map(func(n): return n * n)
print(squared_numbers) # Saída: [1, 4, 9]
```

### 2.5. Classes e Orientação a Objetos

GDScript é uma linguagem orientada a objetos e se integra perfeitamente com o modelo de classes da Godot.

#### 2.5.1. `class_name`

A palavra-chave `class_name` permite registrar um script como uma classe globalmente acessível no editor e no código, sem a necessidade de carregar o arquivo explicitamente. Isso é fundamental para criar tipos personalizados que aparecem no editor.

```gdscript
# player.gd
class_name Player
extends CharacterBody2D

var player_name: String = "Machi"

func _ready():
    print("Player ", player_name, " está pronto!")
```
Agora, em qualquer outro script, você pode instanciar `Player` diretamente:
```gdscript
var new_player = Player.new()
new_player.player_name = "Novo Jogador"
```

#### 2.5.2. Herança (`extends`)

Scripts GDScript podem herdar de classes nativas da Godot (como `Node`, `Sprite2D`, `Resource`) ou de outras classes GDScript.

```gdscript
# enemy.gd
class_name Enemy
extends CharacterBody2D

@export var damage: int = 10

func attack():
    print("Inimigo atacou causando ", damage, " de dano.")

# goblin.gd
class_name Goblin
extends Enemy # Goblin herda de Enemy

func _ready():
    damage = 5 # Goblins causam menos dano
    print("Um Goblin apareceu!")

func attack():
    super.attack() # Chama o método attack da classe pai
    print("Goblin usou um ataque fraco!")
```

#### 2.5.3. Encapsulamento (private, public)

GDScript não possui modificadores de acesso `public` ou `private` explícitos como C++ ou C#. Por convenção, variáveis e funções que começam com um underscore (`_`) são consideradas internas ou "privadas", indicando que não devem ser acessadas diretamente de fora da classe.

```gdscript
class_name MyClass

var public_variable = 10
var _private_variable = 20 # Convenção para variável privada

func public_method():
    print("Método público")

func _private_method(): # Convenção para método privado
    print("Método privado")
```

#### 2.5.4. Polimorfismo

Polimorfismo permite que objetos de diferentes classes respondam ao mesmo método de maneiras diferentes, desde que compartilhem uma interface comum (através de herança).

```gdscript
# weapon.gd
class_name Weapon
extends Resource

func use():
    push_error("Método 'use' não implementado para Weapon base.")

# sword.gd
class_name Sword extends Weapon

@export var attack_power: int = 10

func use():
    print("Espada usada! Causa ", attack_power, " de dano.")

# bow.gd
class_name Bow extends Weapon

@export var arrow_count: int = 20

func use():
    if arrow_count > 0:
        arrow_count -= 1
        print("Arco usado! Flechas restantes: ", arrow_count)
    else:
        print("Sem flechas!")

# player.gd
class_name Player extends CharacterBody2D

@export var equipped_weapon: Weapon

func _input(event):
    if event.is_action_pressed("attack") and equipped_weapon:
        equipped_weapon.use() # Chama o 'use' específico da arma equipada
```

#### 2.5.5. Construtores e Destrutores (`_init`, `_exit_tree`)

*   **`_init()` (Construtor):** É o método chamado quando uma nova instância da classe é criada. Usado para inicializar variáveis e configurar o objeto.
    ```gdscript
    class_name MyObject

    var name: String
    var id: int

    func _init(p_name: String = "Objeto Genérico", p_id: int = 0):
        name = p_name
        id = p_id
        print("Objeto ", name, " (ID: ", id, ") criado.")
    ```
*   **`_exit_tree()` (Destrutor/Limpeza):** É um método de callback do `Node` (e classes que herdam dele) que é chamado quando o nó está prestes a ser removido da árvore de cenas. Não é um destrutor no sentido estrito de C++, mas é o local ideal para realizar limpezas, desconectar sinais ou liberar recursos.
    ```gdscript
    extends Node

    func _exit_tree():
        print("Nó ", name, " saindo da árvore. Realizando limpeza...")
        # Desconectar sinais, liberar recursos, etc.
    ```

### 2.6. Tipagem Estática (Opcional)

GDScript 2.x aprimorou significativamente o suporte à tipagem estática, tornando-a uma ferramenta poderosa para melhorar a qualidade e a manutenibilidade do código.

#### 2.6.1. Benefícios da Tipagem Estática

*   **Detecção Antecipada de Erros:** O editor e o compilador podem identificar erros de tipo antes mesmo de o jogo ser executado, reduzindo bugs em tempo de execução.
*   **Melhor Autocompletar:** O editor pode fornecer sugestões de código mais precisas e contextuais, acelerando o desenvolvimento.
*   **Código Mais Legível e Compreensível:** A declaração explícita de tipos torna a intenção do código mais clara, facilitando a leitura e a compreensão por outros desenvolvedores.
*   **Refatoração Mais Segura:** Alterações no código se tornam mais seguras, pois o sistema de tipos ajuda a garantir que as interfaces entre as partes do código permaneçam consistentes.
*   **Potenciais Otimizações de Performance:** Embora o GDScript seja interpretado, a tipagem estática pode permitir que o compilador realize algumas otimizações, resultando em um código ligeiramente mais rápido em certos cenários.

#### 2.6.2. Sintaxe e Uso

A tipagem estática é aplicada usando dois pontos `:` após o nome da variável, parâmetro ou retorno, seguido pelo tipo.

```gdscript
var health: int = 100
var player_name: String = "Machi"
var speed: float = 150.0
var is_alive: bool = true
var inventory: Array[String] = ["Espada", "Escudo"] # Array tipado
var stats: Dictionary = {"str": 10, "dex": 8}
var player_node: CharacterBody2D = null # Pode ser inicializado como null
```

#### 2.6.3. Tipagem de Variáveis, Parâmetros e Retornos

*   **Variáveis:**
    ```gdscript
    var max_health: int = 100
    var current_target: Node2D
    ```
*   **Parâmetros de Função:**
    ```gdscript
    func take_damage(amount: int, source: Node) -> void:
        # ...
    ```
*   **Valores de Retorno de Função:**
    ```gdscript
    func get_player_position() -> Vector2:
        return global_position

    func is_enemy_dead(enemy_health: int) -> bool:
        return enemy_health <= 0
    ```

#### 2.6.4. `as` Keyword para Casting

A palavra-chave `as` é usada para realizar um *cast* seguro de um tipo para outro. Se o cast falhar (o objeto não for do tipo especificado), ele retornará `null`.

```gdscript
var node = get_node("Player")
var player: CharacterBody2D = node as CharacterBody2D

if player:
    player.move()
else:
    print("Nó 'Player' não é um CharacterBody2D ou não foi encontrado.")
```

### 2.7. Enums e Constantes

#### 2.7.1. Definição e Uso de Enums

Enums (enumerações) permitem definir um conjunto de constantes nomeadas, tornando o código mais legível e menos propenso a erros do que usar "números mágicos".

```gdscript
# Definindo um enum
enum PlayerState { IDLE, WALKING, RUNNING, JUMPING, ATTACKING }

var current_state: PlayerState = PlayerState.IDLE

func _process(delta):
    match current_state:
        PlayerState.IDLE:
            print("Jogador está parado.")
        PlayerState.WALKING:
            print("Jogador está andando.")
        # ...

# Enums com valores personalizados (GDScript 2.x)
enum ItemType { WEAPON = 0, ARMOR = 1, POTION = 2 }
var item: ItemType = ItemType.POTION
```

#### 2.7.2. Constantes Globais e Locais

*   **Constantes Locais:** Declaradas dentro de um script ou função, visíveis apenas naquele escopo.
    ```gdscript
    const MAX_HEALTH = 100

    func _ready():
        const INITIAL_AMMO = 30
        print(INITIAL_AMMO)
    ```
*   **Constantes Globais (Singletons/AutoLoad):** Para constantes que precisam ser acessíveis em todo o projeto, a melhor prática é defini-las em um script AutoLoad (Singleton).
    ```gdscript
    # global_constants.gd (como um AutoLoad)
    extends Node

    const GAME_VERSION = "1.0.0"
    const DEBUG_MODE = true
    const GRAVITY_STRENGTH = 9.8

    # Em qualquer outro script:
    print(GlobalConstants.GAME_VERSION)
    ```

---

## 3. Integração com a Godot Engine

### 3.1. O Sistema de Nós e Cenas

A Godot Engine é construída em torno do conceito de nós (Nodes) e cenas (Scenes). Um nó é o bloco de construção mais básico, e uma cena é uma coleção de nós organizados em uma árvore. O GDScript interage profundamente com essa estrutura.

#### 3.1.1. `Node` e `NodePath`

*   **`Node`:** É a classe base para todos os elementos da árvore de cenas. Tudo o que você vê ou interage no Godot é um `Node` ou herda de `Node` (ex: `Sprite2D`, `Camera3D`, `Button`).
*   **`NodePath`:** É um tipo de dado que representa o caminho para um nó na árvore de cenas. É uma forma eficiente de referenciar nós, especialmente quando eles não são filhos diretos.

    **Exemplo:**
    ```gdscript
    # Caminho relativo
    var player_path: NodePath = "Player"
    var score_label_path: NodePath = "CanvasLayer/UI/ScoreLabel"

    # Caminho absoluto (começa com /root/)
    var root_node_path: NodePath = "/root/Game"
    ```

#### 3.1.2. A Árvore de Cenas

A árvore de cenas é a estrutura hierárquica de nós que compõe o seu jogo. O nó raiz é o ponto de entrada da cena atual.

**Exemplo de Estrutura de Árvore:**

```
- Root (Node)
  - Player (CharacterBody2D)
    - Sprite (Sprite2D)
    - CollisionShape (CollisionShape2D)
  - Enemies (Node2D)
    - Goblin (CharacterBody2D)
    - Orc (CharacterBody2D)
  - CanvasLayer (CanvasLayer)
    - UI (Control)
      - ScoreLabel (Label)
      - HealthBar (TextureProgressBar)
```

#### 3.1.3. Acessando Nós (`$`, `get_node`)

Existem várias maneiras de acessar nós a partir de um script GDScript.

*   **Atalho `$` (NodePath Literal):** A forma mais comum e concisa para acessar filhos diretos ou nós com caminhos relativos curtos.
    ```gdscript
    # Acessando um filho direto
    var player_sprite = $Sprite

    # Acessando um nó com caminho relativo
    var score_label = $CanvasLayer/UI/ScoreLabel
    ```
*   **`get_node(path: NodePath)`:** Um método mais flexível que aceita um `NodePath` (String ou NodePath literal). Útil quando o caminho é dinâmico ou complexo.
    ```gdscript
    var player_node = get_node("Player")
    var enemy_manager = get_node(NodePath("../EnemyManager")) # Caminho relativo
    ```
*   **`@onready` (GDScript 2.x):** Uma anotação para inicializar variáveis com referências a nós *após* o nó atual e seus filhos estarem prontos na árvore de cenas. Isso garante que o nó referenciado já exista.

    **Exemplo:**
    ```gdscript
    extends Node2D

    @onready var player: CharacterBody2D = $Player
    @onready var score_label: Label = $UI/ScoreLabel

    func _ready():
        if player:
            print("Player encontrado: ", player.name)
        if score_label:
            print("Score Label encontrado: ", score_label.text)
    ```

#### 3.1.4. Instanciando Cenas (`PackedScene`)

Cenas são recursos (`PackedScene`) que podem ser carregados e instanciados em tempo de execução. Isso é fundamental para criar novos inimigos, projéteis, itens, etc.

*   **Carregando uma Cena:**
    ```gdscript
    const ENEMY_SCENE = preload("res://scenes/enemy.tscn") # Carrega a cena uma vez
    # ou
    var enemy_scene = load("res://scenes/enemy.tscn") # Carrega a cena sob demanda
    ```
*   **Instanciando uma Cena:**
    ```gdscript
    func spawn_enemy():
        var new_enemy = ENEMY_SCENE.instantiate() as Enemy # Instancia a cena
        add_child(new_enemy) # Adiciona o novo nó à árvore de cenas
        new_enemy.position = Vector2(randf_range(0, 1000), randf_range(0, 600))
    ```

### 3.2. Funções de Callback do Motor (`_ready`, `_process`, `_physics_process`, `_input`, etc.)

A Godot Engine chama automaticamente certas funções em seus scripts em momentos específicos do ciclo de vida de um nó. Essas são as "funções de callback" ou "métodos virtuais" que você sobrescreve para adicionar lógica ao seu jogo.

#### 3.2.1. `_ready()`

Chamado uma vez quando o nó e todos os seus filhos estão prontos na árvore de cenas. É o local ideal para inicializações que dependem de outros nós.

```gdscript
extends Node2D

func _ready():
    # GDScript 2.x: Chamar o _ready da classe pai explicitamente
    super._ready()
    print("Nó ", name, " está pronto!")
    # Inicializar variáveis, conectar sinais, obter referências a outros nós
    # (especialmente se não usar @onready)
```

#### 3.2.2. `_process(delta)`

Chamado a cada frame, ideal para lógica de jogo que não depende da física, como movimento de personagens não-físicos, animações, lógica de UI, etc. `delta` é o tempo decorrido desde o último frame.

```gdscript
extends Node2D

var speed: float = 100.0

func _process(delta: float):
    # Mover o nó a cada frame
    position.x += speed * delta
    # Atualizar UI, verificar entrada do jogador (não física)
```

#### 3.2.3. `_physics_process(delta)`

Chamado a cada passo de física fixo (geralmente 60 vezes por segundo por padrão), ideal para lógica de física, como movimento de `CharacterBody2D`/`3D`, `RigidBody2D`/`3D`, detecção de colisões, etc. `delta` é o tempo fixo do passo de física.

```gdscript
extends CharacterBody2D

var move_speed: float = 200.0
var jump_force: float = -400.0
var gravity: float = 9.8

func _physics_process(delta: float):
    velocity.y += gravity # Aplicar gravidade
    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_force
    
    # Mover o personagem usando a API de física
    move_and_slide()
```

#### 3.2.4. `_input(event)`

Chamado quando um evento de entrada (teclado, mouse, gamepad, touch) ocorre.

```gdscript
extends Node

func _input(event: InputEvent):
    if event.is_action_pressed("ui_accept"):
        print("Botão 'Aceitar' pressionado!")
    if event is InputEventMouseButton and event.pressed:
        print("Clique do mouse em: ", event.position)
```

#### 3.2.5. Outras Funções de Callback

Existem muitas outras funções de callback para diferentes tipos de nós e eventos, como:

*   `_unhandled_input(event)`: Para eventos de entrada que não foram consumidos por outros nós.
*   `_draw()`: Para desenho personalizado em nós `CanvasItem`.
*   `_gui_input(event)`: Para eventos de entrada em nós `Control`.
*   `_notification(what)`: Para receber notificações gerais do motor.

### 3.3. Sinais e Slots

O sistema de sinais e slots da Godot é um mecanismo poderoso para comunicação desacoplada entre objetos. Ele permite que um objeto "emita" um sinal quando algo acontece, e outros objetos podem "conectar" a esse sinal para "receber" a notificação e executar uma função (slot).

#### 3.3.1. Definição de Sinais (`signal`)

Sinais são declarados usando a palavra-chave `signal`, seguida pelo nome do sinal e, opcionalmente, pelos nomes e tipos dos argumentos (GDScript 2.x).

```gdscript
extends Node

signal health_changed(new_health: int)
signal game_over()
signal item_collected(item_name: String, quantity: int)
```

#### 3.3.2. Emissão de Sinais (`emit`)

Sinais são emitidos usando o método `emit()` do sinal, passando os argumentos definidos.

```gdscript
var _health: int = 100:
    set(value):
        _health = value
        health_changed.emit(_health) # Emite o sinal com o novo valor de vida

func take_damage(amount: int):
    _health = max(0, _health - amount)
    if _health <= 0:
        game_over.emit() # Emite o sinal de game over
```

#### 3.3.3. Conexão de Sinais (`connect`)

Conectar um sinal significa que uma função (slot) será chamada quando o sinal for emitido. No GDScript 2.x, isso é feito usando `Callable`s.

```gdscript
extends Node

@onready var player: Player = $Player
@onready var ui_manager: UIManager = $CanvasLayer/UIManager

func _ready():
    # Conectando um sinal do player ao UIManager
    player.health_changed.connect(ui_manager._on_player_health_changed)
    player.game_over.connect(Callable(self, "_handle_game_over").bind("Player morreu!")) # Com argumento extra

func _handle_game_over(message: String):
    print("Fim de jogo! Mensagem: ", message)
    get_tree().paused = true
```

*   **`Callable.bind(...)`:** Permite passar argumentos adicionais para o slot quando o sinal é emitido.

#### 3.3.4. Desconexão de Sinais (`disconnect`)

É importante desconectar sinais quando eles não são mais necessários para evitar vazamentos de memória ou chamadas indesejadas.

```gdscript
func _exit_tree():
    # Desconectar o sinal quando o nó sai da árvore
    if player.health_changed.is_connected(ui_manager._on_player_health_changed):
        player.health_changed.disconnect(ui_manager._on_player_health_changed)
```

#### 3.3.5. Sinais Built-in da Godot

Muitos nós da Godot emitem seus próprios sinais embutidos, que você pode conectar diretamente no editor ou via código.

**Exemplos:**

*   `Button.pressed`: Emitido quando o botão é pressionado.
*   `Area2D.body_entered(body: Node2D)`: Emitido quando um corpo entra na área.
*   `Timer.timeout`: Emitido quando o temporizador termina.

### 3.4. Exportando Variáveis (`@export`)

A anotação `@export` (GDScript 2.x, substituindo a palavra-chave `export` do GDScript 1.x) permite que você exponha variáveis de um script no Inspector do editor Godot. Isso permite que designers e artistas configurem valores diretamente no editor sem precisar modificar o código.

#### 3.4.1. Tipos de Exportação

O `@export` pode ser usado com a maioria dos tipos de dados embutidos e recursos. O editor Godot inferirá o tipo de controle a ser exibido no Inspector.

```gdscript
extends Node2D

@export var player_name: String = "Herói"
@export var max_health: int = 100
@export var move_speed: float = 150.0
@export var is_active: bool = true
@export var inventory_items: Array[String] = ["Espada", "Escudo"]
@export var player_stats: Dictionary = {"str": 10, "dex": 8}
@export var start_position: Vector2 = Vector2(0, 0)
@export var enemy_scene: PackedScene # Exporta um recurso de cena
@export var player_texture: Texture2D # Exporta um recurso de textura
```

#### 3.4.2. Hints de Exportação

Você pode adicionar "hints" (dicas) ao `@export` para fornecer ao editor Godot informações adicionais sobre como exibir e validar a variável no Inspector. Isso cria uma experiência de usuário mais rica e evita erros de configuração.

*   **`@export_range(min, max, step, "suffix:unit")`:** Para números, define um slider com um intervalo.
    ```gdscript
    @export_range(0, 100, 1, "suffix:HP") var current_health: int = 50
    @export_range(0.0, 1.0, 0.01, "suffix:%") var volume: float = 0.75
    ```
*   **`@export_enum("Opção A", "Opção B", "Opção C")`:** Para strings ou inteiros, cria um menu dropdown com opções predefinidas.
    ```gdscript
    @export_enum("Fogo", "Água", "Terra", "Ar") var element_type: String = "Fogo"
    ```
*   **`@export_file("*.tscn,*.scn")`:** Para strings, permite selecionar um arquivo do sistema de arquivos do projeto.
    ```gdscript
    @export_file("*.tscn") var level_scene_path: String
    ```
*   **`@export_dir`:** Para strings, permite selecionar um diretório.
    ```gdscript
    @export_dir var assets_folder: String
    ```
*   **`@export_multiline`:** Para strings, cria uma caixa de texto de múltiplas linhas.
    ```gdscript
    @export_multiline var dialogue_text: String
    ```
*   **`@export_color`:** Para `Color`, exibe um seletor de cores.
    ```gdscript
    @export_color var tint_color: Color = Color.WHITE
    ```
*   **`@export_node_path("Node2D")`:** Para `NodePath`, permite arrastar e soltar um nó do tipo especificado.
    ```gdscript
    @export_node_path("CharacterBody2D") var target_node_path: NodePath
    ```

#### 3.4.3. `_set` e `_get` para Propriedades Customizadas

Para um controle mais granular sobre como uma propriedade é lida ou escrita, você pode usar a sintaxe de `set` e `get` (GDScript 2.x). Isso é útil para validar valores, emitir sinais ou realizar outras ações quando uma propriedade é modificada.

```gdscript
extends Node2D

var _internal_mana: int = 100

@export var mana: int = 100:
    set(value):
        # Lógica de validação ou efeitos colaterais ao definir mana
        if value < 0:
            _internal_mana = 0
            print("Mana não pode ser negativa!")
        elif value > 200:
            _internal_mana = 200
            print("Mana máxima atingida!")
        else:
            _internal_mana = value
        print("Mana atual: ", _internal_mana)
    get:
        # Lógica ao obter mana
        return _internal_mana

func _ready():
    mana = 50 # Chama o setter
    print(mana) # Chama o getter
    mana = -10 # Chama o setter com validação
```

### 3.5. Singletons (AutoLoad)

Singletons, ou "AutoLoad" na Godot, são nós que são carregados automaticamente no início do jogo e estão sempre disponíveis globalmente. Eles são ideais para gerenciar estados de jogo, configurações globais, áudio, sistemas de salvamento/carregamento, ou qualquer funcionalidade que precise ser acessível de qualquer parte do seu projeto.

#### 3.5.1. Criação e Uso

1.  **Crie um Script:** Crie um novo script GDScript (ex: `global_game_manager.gd`).
2.  **Adicione à Lista de AutoLoad:** Vá em `Project -> Project Settings -> AutoLoad`.
3.  **Adicione o Caminho:** Clique no botão "Add Node Path", selecione seu script e dê um nome para o Singleton (ex: `GlobalGameManager`). Certifique-se de que "Enable" esteja marcado.

**Exemplo de Script Singleton (`global_game_manager.gd`):**

```gdscript
extends Node

var current_score: int = 0
var game_state: String = "playing"

func add_score(amount: int):
    current_score += amount
    print("Pontuação atual: ", current_score)

func set_game_state(state: String):
    game_state = state
    print("Estado do jogo: ", game_state)
```

**Uso em qualquer outro script:**

```gdscript
extends Node2D

func _ready():
    GlobalGameManager.add_score(100)
    GlobalGameManager.set_game_state("paused")
    print("Pontuação global: ", GlobalGameManager.current_score)
```

#### 3.5.2. Vantagens e Desvantagens

*   **Vantagens:**
    *   **Acesso Global:** Facilmente acessível de qualquer script sem a necessidade de `get_node()` ou referências complexas.
    *   **Gerenciamento Centralizado:** Ideal para lógica de jogo que precisa ser centralizada e persistente entre cenas.
    *   **Inicialização Automática:** Carregado automaticamente no início do jogo.
*   **Desvantagens:**
    *   **Acoplamento Forte:** O uso excessivo de Singletons pode levar a um acoplamento forte entre as partes do seu código, tornando-o mais difícil de testar e refatorar.
    *   **Dificuldade de Teste:** Singletons podem dificultar testes unitários, pois seu estado global pode afetar o comportamento de outros testes.
    *   **Violação do Princípio da Responsabilidade Única:** Um Singleton pode acumular muitas responsabilidades se não for bem projetado.

**Melhor Prática:** Use Singletons com moderação e para propósitos bem definidos. Considere alternativas como injeção de dependência ou passagem de referências para reduzir o acoplamento quando possível.

### 3.6. Resources

Resources são blocos de dados reutilizáveis que podem ser salvos em arquivos (`.tres`, `.res`) e carregados em tempo de execução. Eles são fundamentais para a Programação Orientada a Resources (ROP) na Godot, permitindo a separação de dados e lógica, e a configuração de elementos do jogo diretamente no editor.

#### 3.6.1. O que são Resources?

Um `Resource` é uma instância de `RefCounted` que pode ser serializada. Isso significa que ele pode conter dados (variáveis exportadas) e lógica (funções), e pode ser salvo e carregado do disco. Exemplos de Resources embutidos na Godot incluem `Texture2D`, `PackedScene`, `Shader`, `Material`, `Animation`.

#### 3.6.2. Criando Resources Customizados (`class_name extends Resource`)

Você pode criar seus próprios tipos de Resources estendendo a classe `Resource` em um script GDScript e usando `class_name`. Isso permite definir estruturas de dados e comportamentos personalizados que podem ser configurados no editor.

**Exemplo de `ItemData.gd` (um Resource customizado):**

```gdscript
# item_data.gd
class_name ItemData
extends Resource

@export var item_name: String = "Novo Item"
@export var description: String = "Uma descrição genérica."
@export var icon: Texture2D
@export var stackable: bool = true
@export_range(1, 999) var max_stack_size: int = 1

func use(target_node: Node) -> void:
    print("Usando item: ", item_name, " no alvo: ", target_node.name)
    # Lógica de uso específica para este item
```

Para criar uma instância deste Resource no editor:
1.  Clique com o botão direito em uma pasta no FileSystem.
2.  Selecione `New Resource...`.
3.  Procure por `ItemData` e crie-o.
Agora você pode configurar as propriedades do seu `ItemData` diretamente no Inspector.

#### 3.6.3. Carregando e Salvando Resources

*   **Carregando:**
    *   `preload("res://path/to/my_resource.tres")`: Carrega o recurso no momento da compilação do script. Ideal para recursos que são sempre necessários.
    *   `load("res://path/to/my_resource.tres")`: Carrega o recurso sob demanda, quando a função é chamada.
    ```gdscript
    const MY_ITEM_DATA = preload("res://resources/my_sword_data.tres")

    func _ready():
        var item_instance: ItemData = MY_ITEM_DATA.duplicate() # Duplicar para evitar modificar o original
        print(item_instance.item_name)
    ```
*   **Salvando:** Resources podem ser salvos programaticamente.
    ```gdscript
    func save_item_data(item_data: ItemData, path: String):
        ResourceSaver.save(item_data, path)
        print("ItemData salvo em: ", path)
    ```

#### 3.6.4. ROP (Programação Orientada a Resources) com GDScript

A Programação Orientada a Resources (ROP) é uma filosofia de design que utiliza `Resources` como entidades ativas e modulares para encapsular dados e comportamentos. Com GDScript, a ROP permite:

*   **Modularidade e Reutilização:** Crie `Resources` para itens, habilidades, estados de IA, configurações de jogo, etc. Eles podem ser reutilizados em múltiplas cenas e personagens.
*   **Configuração no Editor:** Designers podem configurar o comportamento e os dados dos `Resources` diretamente no Inspector, sem escrever código.
*   **Separação de Dados e Lógica:** Mantenha a lógica de comportamento nos `Resources` e os dados configuráveis nas variáveis exportadas, promovendo um design mais limpo.
*   **Polimorfismo:** Utilize herança de `Resources` para criar hierarquias complexas de dados e comportamentos, onde diferentes tipos de `Resources` respondem a métodos comuns de maneiras específicas.

**Exemplo de ROP com GDScript:**

```gdscript
# skill_data.gd (Resource base para habilidades)
class_name SkillData
extends Resource

@export var skill_name: String = "Habilidade Base"
@export var cooldown: float = 1.0

func activate(caster: Node, target: Node) -> void:
    push_error("Método 'activate' não implementado para SkillData base.")

# fireball_skill.gd (Habilidade específica)
class_name FireballSkill
extends SkillData

@export var damage: int = 20
@export var particle_effect: PackedScene

func activate(caster: Node, target: Node) -> void:
    print(skill_name, " ativada! Causando ", damage, " de dano em ", target.name)
    if particle_effect:
        var particles = particle_effect.instantiate()
        target.add_child(particles)
        particles.global_position = target.global_position
        # Lógica para iniciar e destruir partículas

# player.gd
class_name Player extends CharacterBody2D

@export var skills: Array[SkillData] # Array de Resources de habilidades

func _input(event):
    if event.is_action_pressed("use_skill_1") and skills.size() > 0:
        skills[0].activate(self, $TargetEnemy) # Ativa a primeira habilidade
```

---

## 4. Boas Práticas e Padrões de Design

Aderir a boas práticas e padrões de design é fundamental para escrever código GDScript limpo, manutenível, escalável e performático.

### 4.1. Guia de Estilo do GDScript (Godot Official)

A Godot Engine possui um guia de estilo oficial para GDScript que deve ser seguido rigorosamente. Ele garante consistência em todo o projeto e facilita a colaboração.

**Principais Pontos do Guia de Estilo:**

*   **Indentação:** 4 espaços.
*   **Nomenclatura:**
    *   `PascalCase` para `class_name` e nomes de classes.
    *   `snake_case` para variáveis, funções, argumentos e sinais.
    *   `SCREAMING_SNAKE_CASE` para constantes.
    *   `_` prefixo para variáveis/funções "privadas" (convenção).
*   **Tipagem Estática:** Use tipagem estática sempre que possível para variáveis, parâmetros e retornos.
*   **Comentários:** Use `#` para comentários de linha única e `##` para comentários de documentação.
*   **Espaçamento:** Use espaços em branco para melhorar a legibilidade (ex: `if condition:`, `var x = 10`).
*   **Linhas em Branco:** Use linhas em branco para separar blocos lógicos de código.
*   **Tamanho da Linha:** Mantenha as linhas de código com um comprimento razoável (geralmente até 100-120 caracteres).

**Referência:** [GDScript style guide](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_style_guide.html)

### 4.2. Organização de Código e Estrutura de Pastas

Uma estrutura de pastas bem organizada é crucial para a escalabilidade do projeto.

*   **`res://`:** O diretório raiz do seu projeto.
*   **`addons/`:** Para plugins e extensões.
*   **`scenes/`:** Para arquivos `.tscn` (cenas).
*   **`scripts/`:** Para scripts GDScript que não estão anexados a uma cena específica ou que são Singletons.
*   **`assets/`:** Para recursos como imagens, áudio, modelos 3D.
    *   `assets/textures/`
    *   `assets/audio/`
    *   `assets/models/`
*   **`resources/`:** Para `Resources` customizados (`.tres`).
*   **`ui/`:** Para cenas e scripts relacionados à interface do usuário.
*   **`shaders/`:** Para arquivos `.gdshader`.

**Exemplo de Estrutura:**

```
res://
├── addons/
│   └── my_plugin/
│       ├── plugin.cfg
│       └── script.gd
├── scenes/
│   ├── main_menu.tscn
│   ├── game_level_1.tscn
│   └── player.tscn
├── scripts/
│   ├── global_game_manager.gd
│   └── utilities.gd
├── assets/
│   ├── textures/
│   │   ├── player_sprite.png
│   │   └── background.png
│   ├── audio/
│   │   ├── music.ogg
│   │   └── jump_sound.wav
│   └── models/
│       └── character.glb
├── resources/
│   ├── item_data/
│   │   ├── sword_data.tres
│   │   └── potion_data.tres
│   └── skill_data/
│       └── fireball_skill.tres
└── ui/
    ├── main_hud.tscn
    └── hud_script.gd
```

### 4.3. Padrões de Design Comuns

Padrões de design são soluções reutilizáveis para problemas comuns de design de software. Aplicá-los em GDScript ajuda a criar código mais flexível, modular e fácil de manter.

#### 4.3.1. State Machine (Máquina de Estados)

Gerencia o comportamento de um objeto através de estados discretos. Ideal para IA de inimigos, estados de jogador, estados de UI.

**Conceito:** Um objeto pode estar em um de vários estados, e cada estado define um conjunto de comportamentos e transições para outros estados.

**Implementação com GDScript e Resources (conforme ROP):**

```gdscript
# player_state.gd (Resource base)
class_name PlayerState
extends Resource

var player: CharacterBody2D
var state_machine: StateMachine

func enter():
    pass # Lógica ao entrar no estado

func exit():
    pass # Lógica ao sair do estado

func update(delta: float):
    pass # Lógica de atualização do estado (em _process)

func physics_update(delta: float):
    pass # Lógica de atualização do estado (em _physics_process)

# idle_state.gd (Estado específico)
class_name IdleState extends PlayerState

func enter():
    print("Entrando em Idle")
    player.play_animation("idle")

func physics_update(delta: float):
    if Input.is_action_pressed("move_left") or Input.is_action_pressed("move_right"):
        state_machine.transition_to("RunningState")
    if Input.is_action_just_pressed("jump"):
        state_machine.transition_to("JumpingState")

# running_state.gd (Estado específico)
class_name RunningState extends PlayerState

func enter():
    print("Entrando em Running")
    player.play_animation("run")

func physics_update(delta: float):
    var direction = Input.get_vector("move_left", "move_right", "move_up", "move_down")
    player.velocity.x = direction.x * player.speed
    if direction.x == 0:
        state_machine.transition_to("IdleState")

# state_machine.gd (Gerenciador de estados)
class_name StateMachine
extends Node

@export var initial_state_data: PlayerState # Resource do estado inicial
var current_state: PlayerState

func _ready():
    if initial_state_data:
        current_state = initial_state_data.duplicate()
        current_state.player = get_parent() as CharacterBody2D # Assumindo que o StateMachine é filho do Player
        current_state.state_machine = self
        current_state.enter()

func _process(delta: float):
    if current_state:
        current_state.update(delta)

func _physics_process(delta: float):
    if current_state:
        current_state.physics_update(delta)

func transition_to(state_name: String):
    if current_state:
        current_state.exit()
    
    var new_state_data = load("res://resources/states/" + state_name + ".tres") as PlayerState # Carrega o Resource do novo estado
    if new_state_data:
        current_state = new_state_data.duplicate()
        current_state.player = get_parent() as CharacterBody2D
        current_state.state_machine = self
        current_state.enter()
    else:
        push_error("Estado não encontrado: ", state_name)

# player.gd (Anexa o StateMachine)
class_name Player extends CharacterBody2D

@export var speed: float = 150.0
@onready var state_machine: StateMachine = $StateMachine

func _ready():
    state_machine.player = self # Garante que o player seja passado para a máquina de estados
    # ...
```

#### 4.3.2. Singleton (Gerenciadores Globais)

Conforme discutido na seção 3.5, Singletons (AutoLoad) fornecem acesso global a instâncias únicas de classes.

**Uso:** Gerenciadores de áudio, salvamento/carregamento, configurações de jogo, gerenciadores de nível.

**Exemplo:** `GlobalGameManager` (ver seção 3.5.1).

#### 4.3.3. Observer (Sinais e Eventos)

O sistema de sinais e slots da Godot é uma implementação direta do padrão Observer.

**Conceito:** Um objeto (o "assunto") notifica seus dependentes (os "observadores") automaticamente quando seu estado muda, sem que os observadores precisem conhecer o assunto diretamente.

**Uso:** Notificar a UI sobre mudanças na vida do jogador, notificar inimigos sobre a morte do jogador, sistemas de eventos gerais.

**Exemplo:** `Player.health_changed` conectado a `UIManager._on_player_health_changed` (ver seção 3.3.3).

#### 4.3.4. Command (Comandos de Ação)

Encapsula uma solicitação como um objeto, permitindo parametrizar clientes com diferentes solicitações, enfileirar ou registrar solicitações e suportar operações desfazíveis.

**Conceito:** Cada ação (mover, atacar, usar item) é um objeto de comando.

**Implementação:**

```gdscript
# command.gd (Resource base)
class_name Command
extends Resource

func execute(target: Node) -> void:
    push_error("Método 'execute' não implementado para Command base.")

func undo(target: Node) -> void:
    push_error("Método 'undo' não implementado para Command base.")

# move_command.gd
class_name MoveCommand
extends Command

@export var direction: Vector2
@export var speed: float

func execute(target: Node) -> void:
    if target is CharacterBody2D:
        target.velocity = direction.normalized() * speed
        target.move_and_slide()
        print("Movendo ", target.name, " na direção ", direction)

func undo(target: Node) -> void:
    if target is CharacterBody2D:
        target.velocity = Vector2.ZERO
        target.move_and_slide()
        print("Desfazendo movimento de ", target.name)

# player.gd
class_name Player extends CharacterBody2D

@export var move_command: MoveCommand # Resource de comando

func _physics_process(delta):
    var input_direction = Input.get_vector("move_left", "move_right", "move_up", "move_down")
    if input_direction != Vector2.ZERO:
        move_command.direction = input_direction
        move_command.speed = 100 # Exemplo
        move_command.execute(self)
```

#### 4.3.5. Strategy (Comportamentos Intercambiáveis)

Define uma família de algoritmos, encapsula cada um deles e os torna intercambiáveis. `Resources` são ideais para encapsular esses algoritmos.

**Conceito:** Um objeto pode mudar seu comportamento em tempo de execução, delegando a lógica a um objeto "estratégia" diferente.

**Implementação com GDScript e Resources:**

```gdscript
# attack_strategy.gd (Resource base)
class_name AttackStrategy
extends Resource

func perform_attack(attacker: Node, target: Node) -> void:
    push_error("Método 'perform_attack' não implementado para AttackStrategy base.")

# melee_attack_strategy.gd
class_name MeleeAttackStrategy
extends AttackStrategy

@export var damage: int = 10

func perform_attack(attacker: Node, target: Node) -> void:
    print(attacker.name, " realizou um ataque corpo a corpo em ", target.name, " causando ", damage, " de dano.")
    if target.has_method("take_damage"):
        target.take_damage(damage)

# ranged_attack_strategy.gd
class_name RangedAttackStrategy
extends AttackStrategy

@export var projectile_scene: PackedScene
@export var projectile_speed: float = 300.0

func perform_attack(attacker: Node, target: Node) -> void:
    print(attacker.name, " realizou um ataque à distância em ", target.name)
    if projectile_scene:
        var projectile = projectile_scene.instantiate()
        attacker.get_parent().add_child(projectile) # Adiciona o projétil na cena
        projectile.global_position = attacker.global_position
        var direction = (target.global_position - attacker.global_position).normalized()
        projectile.velocity = direction * projectile_speed
        # Lógica para o projétil se mover e causar dano

# enemy.gd
class_name Enemy extends CharacterBody2D

@export var current_attack_strategy: AttackStrategy

func _ready():
    if current_attack_strategy:
        current_attack_strategy = current_attack_strategy.duplicate() # Duplicar para não modificar o Resource original
        # ...

func attack_target(target: Node):
    if current_attack_strategy:
        current_attack_strategy.perform_attack(self, target)
```

#### 4.3.6. Object Pool (Pool de Objetos)

Reutiliza objetos em vez de criá-los e destruí-los constantemente, o que pode ser caro em termos de performance (especialmente para projéteis, partículas, inimigos).

**Conceito:** Mantém uma coleção de objetos "inativos" que podem ser ativados e desativados conforme a necessidade.

**Implementação:**

```gdscript
# object_pool.gd
class_name ObjectPool
extends Node

@export var object_scene: PackedScene
@export var pool_size: int = 10

var _pool: Array[Node] = []

func _ready():
    for i in range(pool_size):
        var new_object = object_scene.instantiate()
        add_child(new_object)
        new_object.hide() # Esconde o objeto inicialmente
        new_object.set_process_mode(Node.PROCESS_MODE_DISABLED) # Desabilita processamento
        _pool.append(new_object)

func get_object() -> Node:
    for obj in _pool:
        if obj.is_hidden():
            obj.show()
            obj.set_process_mode(Node.PROCESS_MODE_INHERIT) # Habilita processamento
            return obj
    
    # Se não houver objetos disponíveis, cria um novo (opcional)
    var new_object = object_scene.instantiate()
    add_child(new_object)
    _pool.append(new_object)
    print("Pool expandido! Novo tamanho: ", _pool.size())
    return new_object

func return_object(obj: Node):
    obj.hide()
    obj.set_process_mode(Node.PROCESS_MODE_DISABLED)
    # Resetar estado do objeto, se necessário
    if obj.has_method("reset"):
        obj.reset()
```

### 4.4. Modularização e Reusabilidade

*   **Scripts Separados:** Mantenha a lógica em scripts separados e bem definidos, cada um com uma responsabilidade única.
*   **`class_name`:** Use `class_name` para tornar seus scripts reutilizáveis e acessíveis globalmente.
*   **Resources:** Utilize `Resources` para encapsular dados e comportamentos que podem ser compartilhados e configurados.
*   **Sinais:** Use sinais para comunicação desacoplada, reduzindo dependências diretas entre nós.
*   **Funções Utilitárias:** Crie scripts com funções estáticas ou Singletons para utilitários comuns (ex: matemática, manipulação de strings).

### 4.5. Comentários e Documentação de Código

*   **Comentários Claros:** Explique a lógica complexa, a intenção por trás das decisões e os algoritmos não triviais.
*   **Comentários de Documentação (`##`):** Use-os para gerar documentação interna que pode ser visualizada no editor.
*   **READMEs:** Para plugins e módulos maiores, mantenha um `README.md` atualizado.
*   **PDDs:** Para funcionalidades complexas, considere criar um Product Design Document (PDD) para planejar e documentar a arquitetura.

---

## 5. Performance e Otimização

Embora o GDScript seja uma linguagem interpretada, a Godot Engine é altamente otimizada, e muitas técnicas podem ser aplicadas para garantir que seu código GDScript seja performático.

### 5.1. Tipagem Estática para Performance

A tipagem estática opcional no GDScript 2.x não apenas melhora a detecção de erros, mas também pode levar a pequenas otimizações de performance. Quando o compilador sabe o tipo de uma variável, ele pode gerar bytecode mais eficiente.

**Exemplo:**

```gdscript
# Menos performático (tipo inferido em tempo de execução)
var my_number = 10

# Mais performático (tipo conhecido em tempo de compilação)
var my_number: int = 10
```

### 5.2. Cache de Referências a Nós

Evite chamadas repetidas a `get_node()` ou `$NodePath` dentro de funções que são chamadas frequentemente (como `_process` ou `_physics_process`). Em vez disso, obtenha a referência uma vez e armazene-a em uma variável.

**Ruim:**

```gdscript
func _process(delta):
    $Player.move()
    $UI/ScoreLabel.text = str(GlobalGameManager.current_score)
```

**Bom (usando `@onready`):**

```gdscript
@onready var player: CharacterBody2D = $Player
@onready var score_label: Label = $UI/ScoreLabel

func _process(delta):
    player.move()
    score_label.text = str(GlobalGameManager.current_score)
```

### 5.3. Evitando Loops Intensivos em GDScript

Para cálculos que envolvem muitos itens ou iterações (ex: algoritmos de pathfinding em grandes mapas, processamento de grandes arrays de dados), o GDScript pode ser mais lento. Nesses casos, considere:

*   **Mover a Lógica para C++ via GDExtension:** Para gargalos de performance críticos, reescrever a lógica em C++ e expô-la via GDExtension pode oferecer ganhos significativos.
*   **Otimizar o Algoritmo:** Escolha algoritmos com melhor complexidade de tempo.
*   **Processamento em Batch:** Se possível, processe dados em blocos em vez de item por item.

### 5.4. `_process` vs `_physics_process`

*   **`_process(delta)`:** Chamado a cada frame. Use para lógica de jogo geral, animações, UI, entrada do jogador (não física). A taxa de quadros pode variar.
*   **`_physics_process(delta)`:** Chamado a cada passo de física fixo (padrão 60 vezes por segundo). Use para lógica de física, movimento de corpos físicos, detecção de colisões. Garante consistência independentemente da taxa de quadros.

**Não misture lógica de física em `_process` e vice-versa.** Isso pode levar a comportamentos inconsistentes ou bugs.

### 5.5. `call_deferred` e `set_process_mode`

*   **`call_deferred(method_name, ...)`:** Agenda a chamada de um método para o próximo frame, após o processamento atual. Útil para evitar problemas de reentrada ou para realizar operações que modificam a árvore de cenas de forma segura.
    ```gdscript
    func _on_body_entered(body):
        # Não remova o corpo diretamente aqui, pode causar problemas
        call_deferred("remove_body", body)

    func remove_body(body):
        body.queue_free()
    ```
*   **`set_process_mode(mode: int)`:** Controla quando um nó é processado.
    *   `Node.PROCESS_MODE_INHERIT`: Processa normalmente (padrão).
    *   `Node.PROCESS_MODE_PAUSABLE`: Processa apenas se o nó não estiver pausado.
    *   `Node.PROCESS_MODE_ALWAYS`: Processa mesmo se o nó ou a árvore estiver pausada.
    *   `Node.PROCESS_MODE_DISABLED`: Não processa.
    Use `PROCESS_MODE_DISABLED` para desativar temporariamente a lógica de um nó, economizando recursos.

### 5.6. Otimização de Coleções (`Array`, `Dictionary`)

*   **Arrays:**
    *   **`append()` vs. `push_back()`:** `push_back()` é ligeiramente mais rápido que `append()` para adicionar elementos ao final de um array.
    *   **`erase()`:** Remover elementos do meio de um array é caro, pois todos os elementos subsequentes precisam ser deslocados. Se você precisar remover muitos elementos, considere usar um `Dictionary` ou marcar elementos para remoção e limpar o array de uma vez.
    *   **Arrays Tipados (GDScript 2.x):** Use arrays tipados para melhor segurança e potenciais otimizações.
*   **Dictionaries:**
    *   Acesso por chave é geralmente muito rápido.
    *   Iterar sobre dicionários pode ser mais lento que iterar sobre arrays.

### 5.7. Considerações sobre Garbage Collection (Godot 4.x)

GDScript utiliza um sistema de contagem de referência para gerenciamento de memória, similar a um coletor de lixo. Objetos que herdam de `RefCounted` (como `Resource`) são liberados automaticamente quando não há mais referências a eles. Nós (`Node`) são liberados quando chamam `queue_free()` ou quando sua cena é descarregada.

*   **Evite Referências Circulares Fortes:** Tenha cuidado com referências circulares fortes entre objetos `RefCounted`, pois isso pode impedir que sejam liberados. Use `weakref()` para criar referências fracas quando necessário.
*   **`queue_free()`:** Sempre use `queue_free()` para remover nós da árvore de cenas. Isso garante que o nó seja liberado de forma segura no final do frame, evitando problemas.
*   **Liberar Recursos Manuais:** Se você carregar recursos manualmente (ex: `Image.load()`), certifique-se de liberá-los quando não forem mais necessários para evitar vazamentos de memória.

---

## 6. Debugging e Ferramentas

Depurar é uma parte essencial do desenvolvimento de jogos. A Godot Engine oferece um conjunto robusto de ferramentas para depurar código GDScript.

### 6.1. `print()`, `push_error()`, `push_warning()`

*   **`print(...)`:** A função mais básica para exibir mensagens no console de saída. Útil para rastrear valores de variáveis, o fluxo de execução e mensagens informativas.
    ```gdscript
    print("Vida do jogador: ", player_health)
    print("Posição X: ", position.x, " Y: ", position.y)
    ```
*   **`push_error(...)`:** Exibe uma mensagem de erro no console de saída, geralmente em vermelho, indicando um problema grave.
    ```gdscript
    if target == null:
        push_error("Alvo é nulo! Não é possível atacar.")
        return
    ```
*   **`push_warning(...)`:** Exibe uma mensagem de aviso no console de saída, geralmente em amarelo, indicando um problema potencial que não é crítico, mas deve ser investigado.
    ```gdscript
    if ammo <= 0:
        push_warning("Sem munição! Recarregue.")
    ```

### 6.2. Debugger Integrado da Godot

O editor Godot possui um depurador GDScript completo que permite inspecionar o estado do seu jogo em tempo de execução.

#### 6.2.1. Breakpoints

*   **Definição:** Clique na margem esquerda do editor de código ao lado de uma linha para definir um breakpoint. A execução do jogo pausará nessa linha.
*   **Condicionais:** Você pode definir condições para breakpoints, fazendo com que eles pausem apenas quando uma expressão for verdadeira (ex: `health <= 0`).

#### 6.2.2. Inspeção de Variáveis

Quando o jogo está pausado em um breakpoint, você pode inspecionar os valores de todas as variáveis no escopo atual, incluindo variáveis locais, membros da classe e variáveis globais.

#### 6.2.3. Controle de Execução

*   **Continuar:** Retoma a execução normal do jogo.
*   **Step Over:** Executa a linha atual e avança para a próxima, sem entrar em chamadas de função.
*   **Step Into:** Entra em chamadas de função, permitindo depurar o código dentro da função.
*   **Step Out:** Sai da função atual e retorna para o ponto de chamada.

### 6.3. Remote Scene Tree

A aba "Remote" no painel "Scene" (Árvore de Cenas) do editor Godot permite inspecionar a árvore de cenas *em tempo de execução*. Você pode selecionar qualquer nó, ver suas propriedades, scripts anexados e até mesmo modificar valores em tempo real para testar diferentes cenários.

### 6.4. Profiler da Godot

O profiler (na aba "Monitor" do painel "Debugger") ajuda a identificar gargalos de performance em seu código GDScript e no motor. Ele mostra o tempo gasto em cada função, o uso de CPU, o uso de memória e outras métricas.

*   **Uso:** Ative o profiler antes de executar o jogo e analise os resultados para encontrar as funções que consomem mais tempo.

### 6.5. `assert()`

A função `assert()` verifica se uma condição é verdadeira. Se a condição for falsa, o jogo pausará no depurador (apenas em builds de depuração) e exibirá uma mensagem de erro. É útil para verificar pré-condições e invariantes.

```gdscript
func divide(a: float, b: float) -> float:
    assert(b != 0, "Erro: Divisão por zero!")
    return a / b
```

### 6.6. Ferramentas de Linting e Análise Estática

Embora o Godot tenha seu próprio sistema de verificação de erros, ferramentas externas de linting e análise estática podem ajudar a manter a qualidade do código, identificar problemas de estilo e potenciais bugs.

*   **GDScript Linter:** Existem linters de terceiros que podem ser integrados ao seu IDE (como VS Code) para fornecer feedback em tempo real sobre o estilo e a qualidade do seu código GDScript.

---

## 7. Interoperabilidade com GDExtension e C++

A Godot Engine é projetada para ser extensível. Embora o GDScript seja a linguagem principal, a interoperabilidade com GDExtension e C++ é crucial para otimizações de performance e integração de baixo nível.

### 7.1. Quando usar GDScript vs GDExtension/C++

A decisão de usar GDScript ou GDExtension/C++ deve ser estratégica:

*   **Use GDScript para:**
    *   **Lógica de Jogo Geral:** A maior parte da lógica de personagens, UI, gerenciamento de cenas, eventos de alto nível.
    *   **Prototipagem Rápida:** Testar novas ideias e mecânicas rapidamente.
    *   **Scripts de Editor:** Ferramentas personalizadas para o fluxo de trabalho.
    *   **Partes do Jogo Não Críticas para Performance:** Onde a velocidade de execução não é o fator mais limitante.
    *   **Facilidade de Manutenção:** Código textual é geralmente mais fácil de ler, refatorar e versionar.

*   **Use GDExtension/C++ para:**
    *   **Gargalos de Performance:** Partes do código que são computacionalmente intensivas e estão causando quedas na taxa de quadros (ex: simulações de partículas complexas, IA avançada, algoritmos de pathfinding em tempo real para muitos agentes).
    *   **Integração com Bibliotecas Externas:** Quando você precisa usar uma biblioteca C/C++ de terceiros (OpenCV, FMOD, etc.) que não tem um equivalente em GDScript ou que exige performance nativa.
    *   **Extensões de Baixo Nível:** Criar novos tipos de nós, recursos ou funcionalidades que exigem acesso direto à API interna da Godot ou controle de hardware.
    *   **Portabilidade de Código Existente:** Se você já tem uma base de código C++ que deseja reutilizar em seu projeto Godot.
    *   **Proteção de IP:** Distribuir partes do seu código como bibliotecas binárias.

### 7.2. Instanciando e Usando Classes C++ em GDScript

Classes C++ registradas via GDExtension aparecem no GDScript como classes nativas. Você pode instanciá-las e usá-las diretamente.

**Exemplo (assumindo `MyCustomCPPClass` é uma classe C++ GDExtension):**

```gdscript
extends Node

func _ready():
    var cpp_object = MyCustomCPPClass.new() # Instancia a classe C++
    add_child(cpp_object)
    cpp_object.set_property_from_gdscript("Olá do GDScript!")
    print("Propriedade C++: ", cpp_object.get_property_from_gdscript())
```

### 7.3. Chamando Métodos e Acessando Propriedades C++

Métodos e propriedades expostos de classes C++ (via `_bind_methods` na GDExtension) podem ser chamados e acessados diretamente do GDScript.

```gdscript
# Supondo que MyCustomCPPClass tenha um método 'do_something_cpp()'
cpp_object.do_something_cpp()

# Supondo que MyCustomCPPClass tenha uma propriedade 'cpp_value'
cpp_object.cpp_value = 123
print(cpp_object.cpp_value)
```

### 7.4. Conectando a Sinais C++

Sinais emitidos por classes C++ (registrados via `ADD_SIGNAL` na GDExtension) podem ser conectados a slots GDScript.

```gdscript
# Supondo que MyCustomCPPClass emita um sinal 'cpp_signal_emitted(value: int)'
func _ready():
    var cpp_object = MyCustomCPPClass.new()
    cpp_object.cpp_signal_emitted.connect(_on_cpp_signal)
    add_child(cpp_object)

func _on_cpp_signal(value: int):
    print("Sinal C++ recebido com valor: ", value)
```

### 7.5. Passagem de Dados entre GDScript e C++ (Variant)

A Godot usa o tipo `Variant` para passar dados entre GDScript e C++. A maioria dos tipos de dados embutidos do GDScript (int, float, String, Vector2, Array, Dictionary, etc.) são automaticamente convertidos para e de `Variant` quando interagem com o código C++.

Isso torna a comunicação entre as duas linguagens muito fluida e transparente.

### 7.6. Considerações de Threading e Concorrência

*   **Thread Principal:** A Godot Engine opera principalmente em um único thread (o thread principal). A maioria das operações da API da Godot (manipulação de nós, acesso a recursos, etc.) deve ser feita no thread principal.
*   **GDExtension e Threads:** Se você usar threads em seu código C++ GDExtension, tenha muito cuidado para não acessar a API da Godot diretamente de threads secundários. Use mecanismos como `call_deferred()` do GDScript ou `Callable.call_deferred()` do C++ para agendar operações na API da Godot para serem executadas no thread principal.
*   **Sincronização:** Use mutexes e semáforos (disponíveis em C++ e na API da Godot) para sincronizar o acesso a dados compartilhados entre threads.

---

## 8. GDScript no Editor Godot

O GDScript não é apenas para a lógica de jogo em tempo de execução; ele também é uma ferramenta poderosa para estender o próprio editor Godot, criando ferramentas personalizadas e melhorando o fluxo de trabalho.

### 8.1. Scripts de Ferramenta (`tool`)

Um script com a palavra-chave `tool` é executado tanto no editor quanto em tempo de execução. Isso permite que você visualize o comportamento do seu script diretamente no editor, crie ferramentas de design e automatize tarefas.

**Exemplo:**

```gdscript
# my_tool_script.gd
@tool
extends Node2D

@export var message: String = "Olá do Editor!"

func _ready():
    if Engine.is_editor_hint():
        # Código que roda apenas no editor
        print("Script de ferramenta pronto no editor!")
    else:
        # Código que roda apenas em tempo de execução
        print("Script de ferramenta pronto no jogo!")

func _process(delta):
    if Engine.is_editor_hint():
        # Atualizar visualização no editor
        queue_redraw() # Força o _draw() a ser chamado
    # ...

func _draw():
    if Engine.is_editor_hint():
        draw_string(get_theme_font("font", "Label"), Vector2(0, 0), message, get_theme_color("font_color", "Label"))
```

### 8.2. Plugins de Editor

Para funcionalidades mais complexas e integradas ao editor, você pode criar plugins de editor completos. Um plugin de editor é um script que estende `EditorPlugin` e permite adicionar novas funcionalidades à interface do editor Godot.

#### 8.2.1. `EditorPlugin`

A classe `EditorPlugin` fornece a API para interagir com o editor.

**Estrutura básica de um plugin de editor:**

```gdscript
# addons/my_custom_plugin/plugin.gd
@tool
extends EditorPlugin

func _enter_tree():
    # Adicionar funcionalidades ao editor
    add_control_to_bottom_panel(my_custom_dock) # Exemplo
    add_tool_menu_item("Minha Ferramenta Customizada", Callable(self, "_on_tool_menu_pressed"))

func _exit_tree():
    # Remover funcionalidades do editor
    remove_control_from_bottom_panel(my_custom_dock)
    remove_tool_menu_item("Minha Ferramenta Customizada")

func _on_tool_menu_pressed():
    print("Menu de ferramenta customizado pressionado!")
    # Abrir uma janela, executar uma ação, etc.
```

#### 8.2.2. Adicionando Controles Customizados

Você pode adicionar seus próprios controles (`Control` nodes) à interface do editor, como painéis, botões, sliders, etc.

```gdscript
# Exemplo de um painel customizado para o plugin
var my_custom_dock: Control

func _init():
    my_custom_dock = Control.new()
    my_custom_dock.name = "MyCustomDock"
    var label = Label.new()
    label.text = "Este é o meu painel customizado!"
    my_custom_dock.add_child(label)
```

#### 8.2.3. Criando Docks e Painéis

Plugins podem adicionar docks (painéis laterais ou inferiores) ao editor, fornecendo interfaces personalizadas para suas ferramentas.

*   `add_control_to_dock(dock_slot: int, control: Control)`
*   `add_control_to_bottom_panel(control: Control)`

### 8.3. Autocompletar e Documentação Integrada

O editor Godot oferece um excelente autocompletar para GDScript, incluindo classes nativas, métodos, propriedades, sinais e até mesmo suas próprias classes `class_name`. A documentação integrada (acessível pressionando F1 ou Ctrl+Clique em um elemento) fornece informações detalhadas sobre a API.

---

## 9. Recursos Adicionais e Comunidade

Para continuar aprimorando suas habilidades em GDScript e Godot, aproveite os vastos recursos disponíveis.

### 9.1. Documentação Oficial da Godot Engine (GDScript)

A documentação oficial da Godot é o recurso mais completo e atualizado para aprender GDScript e o motor.

*   **GDScript reference:** [https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/index.html](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/index.html)
*   **GDScript style guide:** [https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_style_guide.html](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_style_guide.html)
*   **Godot 4.x documentation:** [https://docs.godotengine.org/en/stable/](https://docs.godotengine.org/en/stable/)

### 9.2. Tutoriais e Cursos Online

*   **Godot Engine YouTube Channel:** Tutoriais oficiais e apresentações.
*   **GDQuest:** Cursos e tutoriais de alta qualidade sobre Godot e GDScript.
*   **HeartBeast:** Tutoriais populares para iniciantes.
*   **Udemy, Coursera, GameDev.tv:** Plataformas com diversos cursos sobre Godot.

### 9.3. Comunidade Godot (Fóruns, Discord, Reddit)

A comunidade Godot é muito ativa e acolhedora.

*   **Godot Engine Discord:** [https://discord.gg/godotengine](https://discord.gg/godotengine)
*   **Godot Forums:** [https://godotforums.org/](https://godotforums.org/)
*   **r/godot:** Subreddit oficial da Godot.
*   **Stack Overflow:** Para perguntas e respostas técnicas.

### 9.4. Projetos Open Source de Exemplo

Estudar projetos open source é uma excelente forma de aprender.

*   **Godot Demo Projects:** Projetos de demonstração oficiais da Godot.
*   **GitHub:** Procure por projetos Godot no GitHub para ver como outros desenvolvedores implementam funcionalidades.

---

## 10. Licença

Este documento e o projeto ao qual ele se refere estão licenciados sob a Licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.

Copyright (c) 2025 MokaCode by Machi
