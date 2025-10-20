Classes.md

# Classes.md: O Guia de Referência Essencial da Godot Engine

Bem-vindo ao `Classes.md`, um documento abrangente e detalhado, no estilo de um "ebook", projetado para servir como seu guia de referência definitivo para as classes mais importantes e diretamente utilizáveis da Godot Engine. Este documento foi criado pelo MokaCode CLI para fornecer a você, Machi, um conhecimento profundo e prático sobre os blocos de construção fundamentais do motor.

Diferente da documentação oficial, que é uma referência técnica, este guia foca em:
- **Contexto Prático:** Como e por que usar cada classe em cenários reais de desenvolvimento de jogos.
- **Melhores Práticas:** Dicas de performance, organização e padrões de design para escrever um código limpo e eficiente.
- **Exemplos Detalhados:** Trechos de código em GDScript que ilustram o uso das principais propriedades, métodos e sinais.
- **Relações e Interconexões:** Como as diferentes classes se comunicam e se encaixam na arquitetura geral da Godot.

Este é um documento vivo, destinado a crescer e evoluir. Vamos começar nossa jornada pelo coração da Godot Engine.

---

## Seção I: Fundamentos da Arquitetura Godot

Esta seção aborda as classes mais abstratas e fundamentais da Godot. Compreender estes conceitos é o primeiro e mais crucial passo para dominar o motor, pois tudo o mais é construído sobre esta base.

### 1. Object: A Origem de Tudo

A classe `Object` é a matriarca de quase todas as classes na Godot Engine. De `Node` a `Resource`, passando por `Control` e `RefCounted`, todas herdam, direta ou indiretamente, de `Object`. Ela fornece a infraestrutura essencial que permite que as entidades da Godot sejam gerenciadas pelo motor, oferecendo um sistema de sinais, metaprogramação e gerenciamento de memória de baixo nível. Compreender `Object` é fundamental para entender como a Godot funciona em sua essência.

#### O que é?
`Object` é a classe base mais fundamental na Godot. Ela não possui uma representação visual ou espacial no mundo do jogo, mas fornece funcionalidades cruciais de "meta-programação" (introspecção e reflexão) e gerenciamento de ciclo de vida. É o ancestral comum que garante que qualquer classe na Godot possa ser inspecionada em tempo de execução, possa emitir e conectar sinais, e possa ser gerenciada pelo motor, formando a base de um sistema de script coeso e dinâmico. Em essência, `Object` define o que significa ser um "objeto Godot".

#### Principais Funcionalidades e Métodos

-   **Identificação Única e Comparação:**
    -   `get_instance_id() -> int`: Retorna um ID numérico único para cada instância de `Object`. Este ID é garantido como único durante a sessão do jogo e é extremamente útil para:
        *   Usar objetos como chaves em um `Dictionary` ou `HashMap` de forma eficiente.
        *   Comparações rápidas de identidade, pois comparar dois inteiros é mais rápido do que comparar referências de objetos complexos.
        *   Rastrear objetos em sistemas de depuração ou log.
    -   `is_instance_valid(object: Object) -> bool`: Uma função estática (disponível globalmente) que verifica se uma instância de `Object` ainda é válida (não foi liberada da memória). Essencial para evitar "ponteiros pendurados" (dangling pointers) ao lidar com objetos que podem ser liberados assincronamente.

-   **Metaprogramação (Introspecção e Reflexão):** A capacidade de inspecionar e manipular objetos em tempo de execução, sem conhecer seus tipos concretos em tempo de compilação. Isso é a base da flexibilidade da Godot.
    -   `get_class() -> String`: Retorna o nome da classe do objeto como uma `String` (ex: "Node", "Sprite2D", "MyCustomClass"). Útil para lógica baseada em tipo em tempo de execução.
    -   `is_class(class_name: String) -> bool`: Verifica se o objeto é uma instância da classe especificada ou de qualquer classe que herde dela. É o equivalente ao operador `is` do GDScript, mas pode ser usado com nomes de classe em `String`.
    -   `has_method(method_name: String) -> bool`: Verifica se o objeto possui um método com o nome fornecido. Essencial antes de usar `call()` para evitar erros de tempo de execução.
    -   `call(method_name: String, ...)`: Chama um método do objeto pelo seu nome (string), passando argumentos variáveis. Poderoso para programação genérica, sistemas de plugins, ou quando o nome do método é determinado em tempo de execução.
    -   `get(property_name: String) -> Variant`: Obtém o valor de uma propriedade pelo seu nome. Permite acessar propriedades dinamicamente.
    -   `set(property_name: String, value: Variant)`: Define o valor de uma propriedade pelo seu nome. Isso acionará o método `setter` da propriedade, se houver. Permite modificar propriedades dinamicamente.
    -   `get_property_list() -> Array`: Retorna uma lista de dicionários, onde cada dicionário descreve uma propriedade do objeto (nome, tipo, hints, etc.). Usado por ferramentas de editor e sistemas de serialização.

-   **Gerenciamento de Memória (Manual e Assistido):**
    -   `free()`: Libera o objeto da memória **imediatamente**. Esta ação é perigosa se outras partes do código ainda tiverem uma referência forte a este objeto, podendo causar um crash (uso de "ponteiro pendurado"). Deve ser usado com extrema cautela e apenas quando você tem certeza de que nenhuma outra parte do sistema precisa do objeto. Geralmente, é preferível usar `queue_free()` para `Node`s.
    -   `is_queued_for_deletion() -> bool`: (Disponível em `Node` e classes que herdam dele) Verifica se o nó foi marcado para exclusão com `queue_free()`. A classe `Object` base não possui `queue_free()` diretamente, pois a liberação de `Object`s puros é mais manual ou via contagem de referências (`RefCounted`). Para mais detalhes sobre gerenciamento de memória em C++ com GDExtension, consulte o documento `C++.md`.

-   **Sinais (Comunicação Desacoplada - Padrão Observer):** O sistema de sinais da Godot é uma implementação do padrão Observer, permitindo que objetos se comuniquem sem ter conhecimento direto uns dos outros.
    -   `connect(signal: String, callable: Callable, flags: int = 0)`: Conecta um sinal do objeto a um método (`Callable`). `flags` podem ser usados para conexões especiais, como `CONNECT_ONE_SHOT` (desconecta automaticamente após a primeira emissão) ou `CONNECT_DEFERRED` (emite o sinal no próximo frame, útil para evitar reentrância).
    -   `disconnect(signal: String, callable: Callable)`: Desconecta um sinal. É uma boa prática desconectar sinais quando os objetos envolvidos não são mais necessários para evitar vazamentos de memória ou chamadas indesejadas.
    -   `emit_signal(signal: String, ...)`: Emite um sinal, notificando todos os ouvintes conectados. Os argumentos passados para `emit_signal` serão recebidos pelos métodos conectados.
    -   `add_user_signal(signal_name: String, arguments: Array = [])`: Permite adicionar um sinal personalizado a um objeto em tempo de execução. Útil para sistemas dinâmicos ou ferramentas de editor.

#### Casos de Uso Avançados
-   **Sistemas de Plugins e Modding:** Um sistema de plugins pode usar `call()` e `has_method()` para interagir com diferentes plugins de forma genérica, sem precisar conhecer a implementação exata de cada um. Isso permite que mods adicionem novas funcionalidades que o jogo base pode invocar dinamicamente.
-   **Ferramentas de Editor e Serialização:** Ferramentas que inspecionam e modificam cenas usam `get()`, `set()` e `get_class()` para exibir e alterar propriedades de qualquer `Node` ou `Resource` selecionado. O sistema de serialização da Godot também se baseia fortemente na introspecção de `Object` para salvar e carregar o estado dos objetos.
-   **Estruturas de Dados Customizadas Reativas:** Criar uma classe que herda de `Object` para uma estrutura de dados complexa que precisa emitir sinais quando seus dados mudam. Por exemplo, um `InventoryData` que emite um sinal `item_added` ou `item_removed`.

#### Exemplo de Código (GDScript - Expandido)
```gdscript
# data_model.gd
class_name DataModel
extends Object

signal data_changed(new_data: Dictionary)
signal value_exceeded_limit(key: String, current_value: Variant, limit: Variant)

var _internal_data: Dictionary
var _max_score_limit: int = 200

func _init(initial_data: Dictionary = {}):
    _internal_data = initial_data
    print("DataModel (ID: ", get_instance_id(), ") inicializado com: ", _internal_data)

func update_entry(key: String, value: Variant):
    var old_value = _internal_data.get(key)
    _internal_data[key] = value
    data_changed.emit(_internal_data) # Emite o sinal com os dados atualizados
    print("Entrada atualizada: ", key, " de ", old_value, " para ", value)

    if key == "score" and value is int and value > _max_score_limit:
        value_exceeded_limit.emit(key, value, _max_score_limit)

func get_entry(key: String) -> Variant:
    return _internal_data.get(key)

func has_entry(key: String) -> bool:
    return _internal_data.has(key)

# --- Em outro script ---
# main.gd
extends Node

var player_data_model: DataModel

func _ready():
    player_data_model = DataModel.new({"score": 100, "player_name": "Machi", "level": 1})
    
    # Conectando ao sinal de forma dinâmica e segura
    if player_data_model.has_signal("data_changed"):
        player_data_model.data_changed.connect(Callable(self, "_on_player_data_changed"))
    
    # Conectando um sinal com flag CONNECT_ONE_SHOT
    player_data_model.value_exceeded_limit.connect(Callable(self, "_on_score_limit_exceeded"), CONNECT_ONE_SHOT)

    # Usando metaprogramação para interagir com o modelo
    if player_data_model.has_method("update_entry"):
        player_data_model.call("update_entry", "score", 150)
        player_data_model.call("update_entry", "level", 2)
        player_data_model.set("player_name", "Machiato") # Usando set para propriedade

    # Testando is_class e get_class
    print("player_data_model é da classe DataModel? ", player_data_model.is_class("DataModel"))
    print("Classe de player_data_model: ", player_data_model.get_class())

    # Testando o limite do score
    player_data_model.call("update_entry", "score", 250)

func _on_player_data_changed(new_data: Dictionary):
    print("O modelo de dados do jogador foi atualizado! Novos dados: ", new_data)
    # Saída: O modelo de dados foi atualizado! Novos dados: {score: 150, player_name: Machi, level: 2}

func _on_score_limit_exceeded(key: String, current_value: Variant, limit: Variant):
    print("ALERTA: O valor de '", key, "' (", current_value, ") excedeu o limite de ", limit, "!")
    # Este sinal será desconectado automaticamente após esta primeira emissão

func _exit_tree():
    # Exemplo de desconexão manual (boa prática para evitar vazamentos)
    if player_data_model and player_data_model.data_changed.is_connected(Callable(self, "_on_player_data_changed")):
        player_data_model.data_changed.disconnect(Callable(self, "_on_player_data_changed"))
    if is_instance_valid(player_data_model):
        player_data_model.free() # Libera o objeto Object puro se não for mais necessário
```

#### Dicas e Melhores Práticas
-   **Hierarquia é Chave:** Entenda de qual classe base você deve herdar. Se precisa de gerenciamento automático de memória, `RefCounted` é a escolha. Se precisa estar na árvore de cenas, `Node` é a escolha. `Object` puro é raro para lógica de jogo diretamente, sendo mais comum para classes de dados ou utilitários que não precisam de contagem de referências ou de estar na árvore de cenas.
-   **Metaprogramação vs. Tipagem Estática:** Embora `call()`, `get()` e `set()` sejam flexíveis e poderosos para sistemas dinâmicos (como plugins ou ferramentas de editor), eles são mais lentos que chamadas diretas e anulam as vantagens de segurança da tipagem estática. Prefira o acesso direto (`objeto.metodo()`, `objeto.propriedade`) sempre que possível para performance e segurança em lógica de jogo central.
-   **`is_instance_valid()`:** Sempre use `is_instance_valid()` antes de acessar um `Object` que pode ter sido liberado, especialmente se você não tem controle total sobre seu ciclo de vida. Isso previne crashes por acesso a memória inválida.
-   **`free()` vs `queue_free()`:** Lembre-se que `free()` é imediato e perigoso. Para `Node`s, `queue_free()` é quase sempre a escolha correta. Para `Object`s puros que você gerencia manualmente, `free()` é apropriado quando você tem certeza de que o objeto não é mais referenciado.

---

### 2. RefCounted: Gerenciamento Automático de Memória

`RefCounted` (Reference-Counted) herda de `Object` e adiciona uma funcionalidade crucial e elegante: **gerenciamento automático de memória por contagem de referências**. Esta classe é a base para todos os `Resource`s e muitos outros objetos internos da Godot que precisam de um ciclo de vida gerenciado sem a necessidade de estar na árvore de cenas.

#### O que é?
`RefCounted` é a classe base para objetos cujo ciclo de vida deve ser gerenciado automaticamente através de um mecanismo de contagem de referências. A ideia é simples: o objeto mantém um contador interno de quantas variáveis ou outros objetos estão "apontando" para ele. Quando esse contador chega a zero, o objeto se libera automaticamente da memória. Isso elimina a necessidade de chamar `free()` manualmente, prevenindo uma classe inteira de bugs de gerenciamento de memória, como vazamentos e acessos a memória já liberada.

#### Principais Funcionalidades e Métodos
-   `init_ref() -> bool`: Inicializa a contagem de referências. Raramente chamado manualmente, pois a criação de um `Ref<T>` ou a atribuição a um `Variant` geralmente faz isso.
-   `reference() -> bool`: Incrementa o contador de referências. Chamado automaticamente quando uma nova referência forte é criada (ex: atribuir a um `Ref<T>` ou `Variant`). Raramente chamado manualmente.
-   `unreference() -> bool`: Decrementa o contador de referências. Se o contador chegar a zero, o objeto é liberado. Chamado automaticamente quando uma referência forte é destruída ou sai do escopo. Raramente chamado manualmente.
-   `get_reference_count() -> int`: Retorna o número atual de referências ao objeto. Útil para depuração e para entender o ciclo de vida do objeto.

#### A Armadilha: Referências Cíclicas
O principal problema da contagem de referências são as **referências cíclicas**. Se o `ObjetoA` (um `RefCounted`) contém uma referência forte ao `ObjetoB` (outro `RefCounted`), e o `ObjetoB` contém uma referência forte de volta ao `ObjetoA`, a contagem de referências de ambos nunca chegará a zero, mesmo que nenhuma outra parte do código os esteja usando. Isso cria um vazamento de memória.

**Solução:** Use referências fracas com `weakref()` em GDScript ou `std::weak_ptr` em C++ (para objetos C++ puros, não Godot `RefCounted`). Uma referência fraca permite acessar o objeto, mas não incrementa seu contador de referências, quebrando o ciclo.

```gdscript
# Exemplo de Referência Cíclica e Solução com weakref()
class_name ObjectA extends RefCounted
var b_ref: ObjectB

class_name ObjectB extends RefCounted
var a_weak_ref: WeakRef

func _init():
    print("Objeto criado: ", get_class())

func _notification(what):
    if what == NOTIFICATION_PREDELETE:
        print("Objeto prestes a ser destruído: ", get_class())

func test_circular_reference():
    var a = ObjectA.new()
    var b = ObjectB.new()

    a.b_ref = b # A tem uma referência forte a B
    b.a_weak_ref = weakref(a) # B tem uma referência FRACA a A

    # Se ambos tivessem referências fortes, nenhum seria liberado.
    # Com weakref, A pode ser liberado quando não houver mais referências fortes a ele.

    # Para acessar a referência fraca, você precisa chamar get_ref()
    var ref_para_a = b.a_weak_ref.get_ref()
    if ref_para_a:
        print("Objeto A ainda existe via weakref.")
    else:
        print("Objeto A foi liberado via weakref.")

    # Quando 'a' e 'b' saem do escopo, suas referências fortes são liberadas.
    # A contagem de referências de B chega a 0, B é liberado.
    # A contagem de referências de A chega a 0, A é liberado.

# Em um script principal para testar
extends Node
func _ready():
    var test_obj = ObjectA.new() # Apenas para acessar o método estático
    test_obj.test_circular_reference()
    test_obj.free() # Libera o objeto temporário
```

#### Relação com Outras Classes
-   **`Resource` é um `RefCounted`:** Esta é a principal razão pela qual `RefCounted` é tão importante. Todos os recursos (texturas, scripts, cenas, materiais, etc.) são gerenciados por contagem de referências. Isso permite que múltiplos nós ou scripts compartilhem o mesmo recurso sem se preocupar com sua liberação manual.
-   **`Variant`:** Quando um `RefCounted` é armazenado em um `Variant` (o tipo universal da Godot), a contagem de referências é automaticamente incrementada. Quando o `Variant` é destruído ou sobrescrito, a contagem é decrementada.

#### Dicas e Melhores Práticas
-   Use `RefCounted` (ou `Resource`) para objetos de dados que precisam ser compartilhados entre múltiplos nós ou sistemas, e cujo ciclo de vida não está diretamente ligado à árvore de cenas.
-   Em C++ com GDExtension, **sempre** use o smart pointer `godot::Ref<T>` para gerenciar instâncias de classes que herdam de `RefCounted`. Ele gerencia a contagem de referências automaticamente e previne muitos erros de memória. Consulte o documento `C++.md` para mais detalhes.
-   Fique atento a possíveis referências cíclicas, especialmente em estruturas de dados complexas como grafos, árvores duplamente ligadas ou sistemas de eventos. Use `weakref()` em GDScript ou projete suas classes C++ para evitar ciclos fortes.
-   Para depuração, `get_reference_count()` pode ser útil para entender por que um objeto `RefCounted` não está sendo liberado.

---

### 3. Resource: Os Blocos de Construção de Dados

A classe `Resource` é uma das mais poderosas e centrais da Godot. Ela herda de `RefCounted` e representa qualquer tipo de dado que pode ser salvo no disco e carregado pela engine. `Resources` são a espinha dorsal da filosofia de **Programação Orientada a Resources (ROP)** da Godot, que o MokaCode CLI segue e incentiva.

#### O que é?
Um `Resource` é um bloco de dados reutilizável e serializável. Pense em texturas (`Texture2D`), modelos 3D (`Mesh`), clipes de áudio (`AudioStream`), animações (`Animation`), scripts (`GDScript`) e até cenas inteiras (`PackedScene`). Todos são `Resource`s. A ROP incentiva o uso de `Resource`s customizados para encapsular dados e até mesmo lógica de comportamento, tornando-os componentes poderosos e reutilizáveis que podem ser configurados diretamente no editor.

#### Principais Propriedades e Métodos
-   `resource_path: String`: O caminho do arquivo no disco (`res://...`) de onde o recurso foi carregado. É útil para identificar a origem de um recurso ou para carregá-lo dinamicamente.
-   `resource_name: String`: Um nome opcional para o recurso, que pode ser definido no editor ou via código. Útil para organização.
-   `take_over_path(path: String)`: Define o `resource_path` para o recurso. Geralmente usado quando você cria um recurso em tempo de execução e deseja salvá-lo em um arquivo específico.
-   `duplicate(subresources: bool = false) -> Resource`: Cria uma cópia profunda ou rasa do recurso. Se `subresources` for `true`, os sub-recursos dentro dele (outros `Resources` referenciados) também são duplicados. É crucial usar `duplicate()` se você pretende modificar um recurso em tempo de execução sem afetar todas as outras instâncias que o utilizam. Por exemplo, se você tem um `ItemData` para uma poção e o jogador usa uma, você duplica o `ItemData` para modificar a quantidade da poção no inventário sem alterar o `ItemData` original.

#### Criando Resources Customizados (ROP)
Este é o superpoder da ROP. Você pode criar seus próprios tipos de `Resource` para modelar os dados do seu jogo, tornando-os configuráveis por designers e artistas diretamente no editor.

```gdscript
# item_data.gd
class_name ItemData
extends Resource

@export var id: String = "item_default" # ID único para referência
@export var display_name: String = "Novo Item"
@export_multiline var description: String = "Uma descrição genérica para o item."
@export var icon: Texture2D # Ícone visual do item
@export var stackable: bool = true # Se o item pode ser empilhado
@export_range(1, 999) var max_stack_size: int = 1 # Quantidade máxima por pilha
@export var rarity: Enums.ItemRarity = Enums.ItemRarity.COMMON # Exemplo de enum customizado

# Método de comportamento que pode ser sobrescrito por subclasses
func use(user_node: Node, target_node: Node) -> void:
    print("Usando '", display_name, "' por ", user_node.name, " em ", target_node.name)
    # Adicione a lógica de uso padrão do item aqui
    # Ex: tocar som, aplicar efeito visual

func get_tooltip_text() -> String:
    return "[b]" + display_name + "[/b]\n" + description + "\n[color=gray]Raridade: " + str(rarity) + "[/color]"

# Exemplo de subclasse de Resource
# potion_data.gd
class_name PotionData
extends ItemData

@export var heal_amount: int = 20

func use(user_node: Node, target_node: Node) -> void:
    super.use(user_node, target_node) # Chama o método use da classe base
    if target_node.has_method("heal"):
        target_node.call("heal", heal_amount)
        print(user_node.name, " usou ", display_name, " e curou ", heal_amount, " em ", target_node.name)
```

**Como usar no Editor:**
1.  No painel `FileSystem`, clique com o botão direito em uma pasta (ex: `res://resources/items/`).
2.  Selecione `New Resource...`.
3.  Na janela de criação de recurso, procure por `ItemData` ou `PotionData` (se você criou a subclasse).
4.  Salve o arquivo (ex: `health_potion.tres`).
5.  No `Inspector`, preencha as propriedades exportadas (nome, descrição, ícone, `heal_amount`, etc.).
6.  Em um script de `Node` (ex: `player.gd`), você pode exportar uma variável do tipo `ItemData` ou `PotionData` e arrastar seu arquivo `.tres` para ela no Inspector.

```gdscript
# player.gd
extends CharacterBody2D

@export var equipped_item: ItemData # Pode ser um ItemData ou qualquer subclasse (PotionData, WeaponData)

func _input(event: InputEvent):
    if event.is_action_pressed("use_item"):
        if equipped_item:
            equipped_item.use(self, self) # Passa o próprio jogador como usuário e alvo

func heal(amount: int):
    print(name, " foi curado em ", amount, " pontos.")
    # Lógica de cura real
```

#### Dicas e Melhores Práticas
-   **Separe Dados da Lógica de Cena:** Use `Resource`s para armazenar dados de personagens, inimigos, itens, habilidades, configurações de jogo, etc. Os `Node`s na cena (a parte visual e interativa) devem ler os dados desses `Resource`s e implementar a lógica de interação. Isso torna seu jogo mais fácil de balancear, manter e permite que designers trabalhem com dados sem tocar no código.
-   **`preload()` vs `load()`:**
    -   `preload("path/to/resource.tres")`: Carrega o recurso em tempo de compilação (quando o script é carregado). Causa um erro se o arquivo não for encontrado. É mais rápido em tempo de execução, pois o recurso já está na memória. Use para recursos que você sabe que sempre precisará e que são essáticos (ex: `PackedScene` de um projétil, `ItemData` de um item base).
    -   `load("path/to/resource.tres")`: Carrega o recurso sob demanda, quando a função `load()` é chamada. Retorna `null` se o arquivo não for encontrado. É mais flexível e útil para carregamento dinâmico de recursos (ex: níveis, assets que dependem da escolha do jogador) ou para evitar carregar tudo na memória de uma vez.
-   **Sempre use `duplicate()` para Resources modificáveis:** Se você pretende modificar um `Resource` em tempo de execução (ex: diminuir a quantidade de uma poção no inventário, alterar a durabilidade de uma arma), **sempre** chame `.duplicate()` ao instanciá-lo ou ao atribuí-lo a uma variável. Caso contrário, você modificará o arquivo base compartilhado, afetando todas as outras instâncias que o utilizam e até mesmo o arquivo salvo em disco. Se o `Resource` for apenas para leitura (ex: `EnemyData` com stats fixos), não há necessidade de duplicar.
-   **ROP com GDExtension/C++:** Para `Resources` que encapsulam lógica complexa ou computacionalmente intensiva, considere implementá-los em C++ via GDExtension. Isso combina a flexibilidade de configuração no editor com a performance nativa do C++. Consulte o documento `ROP.md` para uma exploração aprofundada da Programação Orientada a Resources.

---

### 4. Node: Os Átomos da Árvore de Cenas

Se `Object` é a origem de tudo, `Node` é a origem de tudo que **vive na árvore de cenas**. É a classe base para todos os elementos que compõem seu jogo, desde sprites e modelos 3D até timers e gerenciadores de UI. A arquitetura baseada em nós da Godot é uma das suas características mais distintivas e poderosas.

#### O que é?
Um `Node` é um bloco de construção fundamental que pode ser adicionado à `SceneTree` (Árvore de Cenas). Ele herda de `Object`, então possui todas as suas funcionalidades (sinais, metaprogramação, gerenciamento de memória básico), mas adiciona conceitos cruciais para a construção de jogos:
-   **Hierarquia:** Nós são organizados em uma estrutura de árvore (pai-filho), onde as transformações (posição, rotação, escala) e a visibilidade são herdadas dos pais.
-   **Processamento de Ciclo de Vida:** Nós possuem métodos de callback (`_ready`, `_process`, `_physics_process`, etc.) que são chamados pela engine em momentos específicos.
-   **Grupos:** Nós podem ser adicionados a grupos, permitindo o gerenciamento e a comunicação de coleções de nós de forma desacoplada.
-   **Acesso à `SceneTree`:** Nós têm acesso ao `SceneTree` global, que gerencia o fluxo do jogo.

#### Principais Propriedades e Métodos

-   **Gerenciamento da Árvore de Cenas:**
    -   `get_parent() -> Node`: Retorna o nó pai. Útil para navegar na hierarquia.
    -   `get_child(idx: int) -> Node`: Retorna um filho pelo seu índice (0-based).
    -   `get_children() -> Array[Node]`: Retorna um array com todos os filhos diretos do nó.
    -   `get_node(path: NodePath) -> Node`: Encontra um nó na árvore usando seu caminho. O atalho `$` (ex: `$Sprite2D`) é uma forma mais concisa e recomendada de usar `get_node()` para caminhos literais.
    -   `add_child(node: Node, force_readable_name: bool = false)`: Adiciona um nó como filho deste. O nó filho será processado e renderizado como parte da subárvore.
    -   `remove_child(node: Node)`: Remove um nó filho da árvore. O nó não é liberado da memória automaticamente; você deve chamar `queue_free()` nele se não for mais necessário.
    -   `queue_free()`: Remove o nó da árvore e o libera da memória de forma segura no final do frame atual. Esta é a maneira preferida de destruir nós em tempo de execução, pois evita problemas de reentrância e acesso a nós já liberados.
    -   `reparent(new_parent: Node, keep_global_transform: bool = true)`: Move o nó para um novo pai na árvore de cenas. Se `keep_global_transform` for `true`, a posição global do nó é mantida.

-   **Ciclo de Vida (Callbacks - Métodos Virtuais):** Estes métodos são chamados automaticamente pela Godot e são onde você implementa a lógica do seu jogo.
    -   `_enter_tree()`: Chamado quando o nó entra na `SceneTree`. O nó e seus filhos ainda não estão "prontos" (ou seja, `_ready()` ainda não foi chamado).
    -   `_ready()`: Chamado uma vez quando o nó e todos os seus filhos estão prontos na árvore de cenas. É o local ideal para inicializações que dependem de outros nós ou para obter referências a eles (usando `@onready`).
    -   `_process(delta: float)`: Chamado a cada frame. Use para lógica de jogo geral, animações, UI, entrada do jogador (não física). `delta` é o tempo decorrido desde o último frame, essencial para um movimento independente de framerate.
    -   `_physics_process(delta: float)`: Chamado em intervalos fixos (geralmente 60 vezes por segundo por padrão). Use para lógica de física, movimento de `CharacterBody2D`/`3D`, `RigidBody2D`/`3D`, detecção de colisões. `delta` é o tempo fixo do passo de física.
    -   `_input(event: InputEvent)`: Chamado para cada evento de entrada (teclado, mouse, gamepad, touch). Permite processar inputs diretamente no nó.
    -   `_unhandled_input(event: InputEvent)`: Chamado para eventos de entrada que não foram consumidos por outros nós na árvore (ex: nós de UI).
    -   `_exit_tree()`: Chamado quando o nó está prestes a sair da `SceneTree`. Ideal para limpeza, desconectar sinais ou liberar recursos que foram alocados manualmente.

-   **Outros Propriedades e Métodos Úteis:**
    -   `name: String`: O nome do nó. É importante que seja único entre irmãos para facilitar o acesso via `$` ou `get_node()`.
    -   `owner: Node`: O nó que "possui" este nó (geralmente o nó raiz da cena à qual este nó pertence). Útil para saber a qual cena um nó instanciado pertence.
    -   `get_tree() -> SceneTree`: Retorna a `SceneTree` global à qual o nó pertence. Essencial para acessar funcionalidades globais do jogo.
    -   `is_in_group(group: String) -> bool`: Verifica se o nó pertence a um grupo específico.
    -   `add_to_group(group: String)`: Adiciona o nó a um grupo. Grupos são uma forma poderosa de gerenciar coleções de nós de forma desacoplada.
    -   `remove_from_group(group: String)`: Remove o nó de um grupo.

#### Relação com `SceneTree`
Um `Node` só se torna "ativo" (ou seja, seus métodos de ciclo de vida são chamados) quando ele é adicionado à `SceneTree`. A `SceneTree` é a responsável por orquestrar a execução de todos os nós, propagando os callbacks de processo, física e entrada.

#### Exemplo de Código (GDScript - Expandido)
```gdscript
# player.gd
extends CharacterBody2D # Herda de CharacterBody2D, que por sua vez herda de Node2D e Node

@export var speed: float = 150.0
@export var jump_velocity: float = -400.0

@onready var animated_sprite: AnimatedSprite2D = $AnimatedSprite2D # Referência segura ao filho
@onready var collision_shape: CollisionShape2D = $CollisionShape2D

func _ready():
    print("O nó '", name, "' (ID: ", get_instance_id(), ") está pronto!")
    print("Seu pai é: ", get_parent().name)
    add_to_group("players") # Adiciona o jogador ao grupo "players"

    # Exemplo de adição dinâmica de um nó filho
    var timer = Timer.new()
    timer.name = "AttackCooldownTimer"
    timer.wait_time = 0.5
    timer.one_shot = true
    add_child(timer)
    timer.timeout.connect(Callable(self, "_on_attack_cooldown_timeout"))

    # Acessar o filho recém-adicionado usando $
    var attack_timer = $AttackCooldownTimer as Timer
    if attack_timer:
        print("Timer de ataque adicionado: ", attack_timer.name)

func _physics_process(delta: float):
    # Lógica de movimento e física
    var direction = Input.get_vector("move_left", "move_right", "move_up", "move_down")
    velocity.x = direction.x * speed

    if not is_on_floor():
        velocity.y += ProjectSettings.get_setting("physics/2d/default_gravity") * delta

    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_velocity

    move_and_slide()

    update_animation(direction)

func _input(event: InputEvent):
    if event.is_action_just_pressed("attack"):
        perform_attack()

func update_animation(direction: Vector2):
    if direction.x != 0:
        animated_sprite.animation = "run"
        animated_sprite.flip_h = direction.x < 0
    else:
        animated_sprite.animation = "idle"

func perform_attack():
    var attack_timer = $AttackCooldownTimer as Timer
    if attack_timer and not attack_timer.is_stopped():
        print("Ataque em cooldown!")
        return

    print("Jogador atacou!")
    animated_sprite.animation = "attack"
    animated_sprite.play()
    attack_timer.start()
    # Lógica para criar hitbox, causar dano, etc.

func _on_attack_cooldown_timeout():
    print("Cooldown de ataque finalizado.")
    animated_sprite.animation = "idle" # Retorna à animação idle

func _exit_tree():
    print("Nó '", name, "' saindo da árvore. Realizando limpeza...")
    # Desconectar sinais, liberar recursos alocados manualmente, etc.
    # Exemplo: se o timer foi criado dinamicamente e não é filho de outro nó gerenciado
    # if is_instance_valid(timer): timer.free()
```

#### Dicas e Melhores Práticas
-   **Composição sobre Herança:** A Godot incentiva fortemente a construção de objetos complexos compondo `Node`s simples, em vez de criar hierarquias de herança de scripts muito profundas. Por exemplo, um `Player` é um `CharacterBody2D` que *tem* um `Sprite2D`, uma `CollisionShape2D` e um `AnimationPlayer` como filhos, em vez de herdar de uma classe `PlayerBase` que herda de `CharacterBody2D` e contém toda a lógica visual.
-   **`@onready` para Referências a Filhos:** Use a anotação `@onready var meu_no = $Caminho/Para/O/No` para inicializar variáveis com referências a outros nós. Isso garante que a referência seja obtida somente quando a árvore estiver pronta (`_ready()` foi chamado), evitando erros de acesso a nós que ainda não existem.
-   **Grupos para Desacoplamento:** Use grupos para desacoplar o código. Em vez de um inimigo procurar pelo nó "Player" diretamente, ele pode procurar por todos os nós no grupo "players". Isso permite ter múltiplos jogadores, testar cenas de inimigos de forma isolada, e facilita a adição/remoção de entidades sem quebrar referências diretas.
-   **`queue_free()` para Liberação Segura:** Sempre use `queue_free()` para remover nós da árvore de cenas em tempo de execução. Nunca use `free()` diretamente em nós da árvore, pois isso pode causar problemas de reentrância e crashes se o nó ainda estiver sendo processado ou referenciado por outros nós no mesmo frame.
-   **`get_node()` vs `$`:** O atalho `$` é mais conciso para caminhos literais. Para caminhos dinâmicos ou complexos, `get_node()` com um `NodePath` construído programaticamente é mais apropriado.

---

### 5. SceneTree: O Coração Pulsante do Jogo

A `SceneTree` é a classe que gerencia a hierarquia de nós e o fluxo principal do jogo. Embora você raramente instancie uma `SceneTree` manualmente (ela é um singleton global), você a acessa constantemente a partir de qualquer `Node` usando `get_tree()`. Ela é o orquestrador de tudo que acontece no seu jogo.

#### O que é?
É um singleton de fato que atua como o `MainLoop` (loop principal) do seu jogo. Ela contém a cena atualmente ativa, gerencia o estado global do jogo (pausa, quit, etc.), e propaga os callbacks (`_process`, `_physics_process`, `_input`, etc.) para todos os nós na árvore. A `SceneTree` é a representação em tempo de execução da sua hierarquia de cenas e nós.

#### Principais Propriedades e Métodos
-   **Gerenciamento de Cenas:**
    -   `current_scene: Node`: O nó raiz da cena atualmente ativa. Permite acesso direto à cena principal carregada.
    -   `change_scene_to_file(path: String) -> Error`: Muda a cena atual para uma nova cena a partir de um arquivo (`.tscn`). A cena antiga é liberada da memória. Retorna `OK` em caso de sucesso, ou um código de erro.
    -   `change_scene_to_packed(packed_scene: PackedScene) -> Error`: O mesmo que `change_scene_to_file`, mas usando um recurso `PackedScene` já carregado na memória. Mais eficiente se a cena já foi pré-carregada.
    -   `reload_current_scene() -> Error`: Recarrega a cena atual. Útil para reiniciar um nível ou um estado de jogo.
    -   `set_auto_accept_quit(enabled: bool)`: Controla se o jogo deve sair automaticamente quando o sistema operacional solicita (ex: fechar janela).

-   **Gerenciamento de Estado Global:**
    -   `paused: bool`: Se `true`, o jogo é pausado. Quando `paused` é `true`, `_process` não será chamado na maioria dos nós, mas `_physics_process` ainda será (a menos que o `process_mode` do nó seja alterado para `PROCESS_MODE_PAUSABLE`). Nós de UI (Control) geralmente têm `PROCESS_MODE_ALWAYS` para que possam funcionar mesmo com o jogo pausado.
    -   `quit(exit_code: int = 0)`: Encerra o jogo. `exit_code` pode ser usado para indicar o status de saída.
    -   `set_quit_on_go_back(enabled: bool)`: Em plataformas móveis, se `true`, o botão "voltar" do sistema operacional encerra o jogo.

-   **Gerenciamento de Nós e Grupos (Global):**
    -   `get_nodes_in_group(group: String) -> Array[Node]`: Retorna um array com todos os nós que pertencem a um grupo específico em toda a árvore de cenas. Extremamente útil para comunicação global e gerenciamento de coleções de objetos.
    -   `call_group(group: String, method: String, ...)`: Chama um método em todos os nós de um grupo. Permite enviar comandos para múltiplos objetos de uma vez.
    -   `set_group(group: String, property: String, value: Variant)`: Define uma propriedade em todos os nós de um grupo.
    -   `get_first_node_in_group(group: String) -> Node`: Retorna o primeiro nó encontrado em um grupo. Útil quando você espera apenas um nó em um grupo (ex: o jogador).

#### Exemplo de Código (GDScript - Expandido)
```gdscript
# game_manager.gd (um AutoLoad/Singleton)
extends Node

signal game_paused(is_paused: bool)
signal game_over_signal

func _ready():
    # Conecta o sinal de quit do sistema operacional
    get_tree().root.set_auto_accept_quit(false) # Desabilita quit automático
    get_tree().root.set_quit_on_go_back(false) # Desabilita quit no botão voltar (mobile)
    get_tree().notification(NOTIFICATION_WM_CLOSE_REQUEST)
    get_tree().root.connect("tree_exiting", Callable(self, "_on_tree_exiting"))

func _unhandled_input(event: InputEvent):
    # Pausar/despausar o jogo com a tecla 'P'
    if event.is_action_pressed("pause_toggle"):
        toggle_pause()

func toggle_pause():
    get_tree().paused = not get_tree().paused
    game_paused.emit(get_tree().paused)
    print("Jogo pausado: ", get_tree().paused)
    # Exibir/esconder menu de pausa aqui

func game_over():
    print("Fim de jogo!")
    game_over_signal.emit()
    # Notificar todos os inimigos para pararem
    get_tree().call_group("enemies", "stop_ai") # Chama o método stop_ai em todos os nós do grupo "enemies"
    # Recarregar a cena após 3 segundos
    await get_tree().create_timer(3.0).timeout
    get_tree().reload_current_scene()

func go_to_main_menu():
    print("Voltando ao menu principal...")
    get_tree().change_scene_to_file("res://scenes/main_menu.tscn")

func _on_tree_exiting():
    print("O jogo está sendo encerrado. Salvando dados...")
    # Chamar SaveManager.save_game() aqui
    get_tree().quit() # Confirma o encerramento
```

#### Dicas e Melhores Práticas
-   **Singletons (Autoloads):** A `SceneTree` é o local ideal para registrar Singletons (Autoloads) que precisam de acesso global e persistência entre cenas. Use-os para gerenciar o estado do jogo, áudio, configurações, etc.
-   **Transições de Cena:** Para transições de cena mais suaves e com efeitos visuais (fade-out/fade-in), crie um `SceneTransitionManager` (Autoload) que gerencie o `change_scene_to_file` ou `change_scene_to_packed` e adicione animações.
-   **Gerenciamento de Pausa:** Ao pausar o jogo, lembre-se de que nós de UI (Control) geralmente precisam ter seu `process_mode` definido como `PROCESS_MODE_ALWAYS` para continuar funcionando e permitir a interação com o menu de pausa.
-   **Comunicação Global com Grupos:** `get_nodes_in_group()` e `call_group()` são ferramentas poderosas para comunicação global e gerenciamento de coleções de nós sem a necessidade de referências diretas, promovendo o desacoplamento.

---

### 6. PackedScene: O Molde da Cena

Uma `PackedScene` é um `Resource` que contém uma cena serializada. É o "molde" ou "blueprint" que você usa para criar novas instâncias de cenas em tempo de execução. `PackedScene`s são fundamentais para a modularidade e reutilização de componentes em jogos Godot.

#### O que é?
Quando você salva uma cena no editor (um arquivo `.tscn`), você está, na verdade, criando um `PackedScene`. Este recurso armazena a estrutura da árvore de nós, suas propriedades, scripts anexados e conexões de sinais. Ele é um "modelo" que pode ser instanciado múltiplas vezes para criar cópias idênticas da cena original, cada uma com seu próprio estado independente.

#### Principal Método
-   `instantiate() -> Node`: Este é o método chave. Ele cria uma nova instância da árvore de nós que a `PackedScene` representa e retorna o nó raiz dessa nova instância. A nova instância é uma cópia exata da cena original, mas é independente e pode ser modificada sem afetar o `PackedScene` original ou outras instâncias.

#### Casos de Uso Comuns
-   **Inimigos e Personagens:** Crie uma cena para seu inimigo (`inimigo.tscn`) ou personagem (`player.tscn`) e a instancie sempre que um novo inimigo precisar aparecer ou um novo jogador entrar no jogo.
-   **Projéteis e Efeitos:** Crie cenas para projéteis (`bala.tscn`), explosões (`explosao.tscn`) ou outros efeitos visuais/sonoros e instancie-os dinamicamente quando necessário.
-   **Itens Coletáveis:** Moedas, poções, power-ups, etc., podem ser cenas que são instanciadas quando um inimigo é derrotado ou um baú é aberto.
-   **Componentes Reutilizáveis:** Elementos de UI complexos, partes de níveis (ex: salas de dungeon), ou qualquer conjunto de nós que você deseja reutilizar como uma unidade.

#### Exemplo de Código (GDScript - Expandido)
```gdscript
# weapon.gd
extends Node2D

# Carrega a cena da bala uma vez para otimização (preload)
const BULLET_SCENE: PackedScene = preload("res://scenes/bullet.tscn")

@export var fire_rate: float = 0.2 # Tiros por segundo
var can_shoot: bool = true

func _ready():
    # Adiciona um timer para controlar a taxa de tiro
    var shoot_timer = Timer.new()
    shoot_timer.wait_time = fire_rate
    shoot_timer.one_shot = true
    add_child(shoot_timer)
    shoot_timer.timeout.connect(Callable(self, "_on_shoot_timer_timeout"))

func _process(delta: float):
    if Input.is_action_pressed("shoot") and can_shoot:
        shoot()
        can_shoot = false
        ($ShootCooldownTimer as Timer).start() # Inicia o cooldown

func shoot():
    if not BULLET_SCENE:
        push_error("Cena da bala não carregada!")
        return

    # 1. Instancia a cena da bala
    var new_bullet = BULLET_SCENE.instantiate() as Area2D
    if not new_bullet:
        push_error("Falha ao instanciar a bala!")
        return

    # 2. Adiciona a nova instância à árvore de cenas
    # get_tree().current_scene é uma forma segura de adicionar à cena principal
    get_tree().current_scene.add_child(new_bullet)

    # 3. Configura a posição e rotação da bala para corresponder à arma
    new_bullet.global_transform = global_transform
    # Se a bala tiver um script, você pode passar parâmetros para ela aqui
    if new_bullet.has_method("set_direction"):
        new_bullet.call("set_direction", Vector2.RIGHT.rotated(global_rotation))

    print("Bala disparada!")

func _on_shoot_timer_timeout():
    can_shoot = true
```

#### Dicas e Melhores Práticas
-   **`preload()` vs `load()`:** Use `preload()` para `PackedScene`s que são sempre necessárias e que você sabe que estarão presentes. Isso carrega o recurso em tempo de compilação, tornando a instanciação mais rápida. Use `load()` para cenas que são carregadas sob demanda (ex: níveis diferentes, cenas que dependem de escolhas do jogador) para otimizar o tempo de inicialização e o uso de memória.
-   **Adicionar à Árvore de Cenas:** Lembre-se que `instantiate()` apenas cria o nó na memória. Você precisa adicioná-lo à árvore de cenas com `add_child()` (geralmente no nó pai apropriado ou na cena atual via `get_tree().current_scene.add_child()`) para que ele se torne ativo, seja processado e renderizado.
-   **Tipagem Segura:** Ao instanciar, use `as Type` (ex: `as Area2D`) para garantir a tipagem correta. Isso melhora a segurança do código, permite o autocompletar e ajuda na detecção de erros.
-   **Otimização com `Object Pool`:** Para objetos que são instanciados e liberados com muita frequência (ex: projéteis, partículas), considere implementar um padrão `Object Pool`. Em vez de `instantiate()` e `queue_free()`, você "empresta" objetos de um pool e os "devolve" quando não são mais necessários. Isso reduz o overhead de alocação/desalocação de memória e pode melhorar significativamente a performance. (Consulte o documento `C++.md` para um exemplo de `Object Pool` em C++).

---

### 7. CanvasItem, Node2D e Control: A Base do 2D

Essas três classes formam a hierarquia fundamental para toda a renderização 2D e interação na Godot Engine. Compreender suas diferenças e propósitos é crucial para construir interfaces de usuário e elementos de jogo 2D eficientes e bem estruturados.

#### 7.1. `CanvasItem`: O Elemento Desenhável Base

*   **O que é?** `CanvasItem` é a classe base abstrata para tudo que é desenhado em 2D na Godot. Ela não pode ser instanciada diretamente, mas fornece as funcionalidades básicas para renderização 2D. Pense nela como o contrato mínimo para um objeto que pode ser "desenhado" em uma tela 2D.
*   **Funcionalidades Chave:**
    *   **Visibilidade:** Propriedades como `visible` (para o nó e seus filhos) e `self_modulate` (para o nó sem afetar os filhos).
    *   **Cor e Modulação:** `modulate` (multiplica a cor do item e seus filhos) e `self_modulate` (apenas o item).
    *   **Materiais:** `material` para aplicar shaders ou outros efeitos de renderização.
    *   **Ordem de Desenho:** `z_index` (controla a ordem de sobreposição, maior valor desenha por cima) e `y_sort_enabled` (ordena filhos com base na sua posição Y, útil para perspectiva falsa 3D).
    *   **Desenho Personalizado:** O método virtual `_draw()` permite que você desenhe formas, linhas, texturas e polígonos personalizados usando a API de desenho da Godot.
*   **Casos de Uso:** Raramente usado diretamente, mas suas propriedades e métodos são herdados por `Node2D` e `Control`.

#### 7.2. `Node2D`: Objetos no Mundo 2D

*   **O que é?** `Node2D` herda de `CanvasItem` e é a classe base para todos os nós 2D que possuem uma **transformação espacial** (posição, rotação, escala) no mundo do jogo. Ele representa um objeto com uma localização e orientação no espaço 2D.
*   **Funcionalidades Chave:**
    *   **Transformação Local:** `position`, `rotation` (em radianos), `rotation_degrees` (em graus), `scale`. Estas são relativas ao nó pai.
    *   **Transformação Global:** `global_position`, `global_rotation`, `global_scale`. Estas são absolutas em relação à viewport.
    *   **`transform: Transform2D`:** Uma matriz que encapsula a posição, rotação e escala. É a forma mais robusta e eficiente de manipular a transformação de um nó.
    *   **Métodos de Movimento:** `look_at(point: Vector2)` (gira o nó para apontar para um ponto), `translate(offset: Vector2)` (move o nó por um vetor), `rotate(angle: float)` (gira o nó por um ângulo).
    *   **Conversão de Coordenadas:** `to_global(local_point: Vector2)` e `to_local(global_point: Vector2)` para converter entre sistemas de coordenadas.
*   **Casos de Uso:** Personagens, inimigos, projéteis, elementos de cenário, câmeras, colisores. Qualquer coisa que precise de uma posição e orientação no seu mundo 2D.

#### 7.3. `Control`: Elementos de Interface do Usuário (UI)

*   **O que é?** `Control` também herda de `CanvasItem`, mas é a classe base para todos os **nós de UI**. Além das propriedades de `CanvasItem`, `Control` adiciona conceitos de **retângulos, âncoras, margens e foco** para criar interfaces de usuário responsivas e interativas.
*   **Funcionalidades Chave:**
    *   **Layout:** `layout_mode` (controla como o nó se comporta dentro de contêineres), `anchor_left`, `anchor_top`, `anchor_right`, `anchor_bottom` (âncoras para posicionamento responsivo), `offset_left`, `offset_top`, `offset_right`, `offset_bottom` (margens em relação às âncoras).
    *   **Tamanho e Posição:** `size`, `position` (relativos ao pai `Control`).
    *   **Interação:** `mouse_filter` (como o nó interage com eventos do mouse), `focus_mode` (como o nó pode receber foco para entrada de teclado/gamepad).
    *   **Temas:** `theme` para aplicar estilos visuais consistentes.
    *   **Métodos de Layout:** `get_rect()` (retorna o retângulo de layout), `set_anchors_preset(preset: int)` (define presets de âncoras, ex: `PRESET_FULL_RECT` para preencher o pai).
    *   **Callbacks de UI:** `_gui_input(event: InputEvent)` para lidar com eventos de entrada específicos da UI.
*   **Casos de Uso:** Botões, rótulos, barras de progresso, menus, inventários, painéis, contêineres de layout. Qualquer elemento da sua interface de usuário.

#### A Diferença Crucial
-   Use `Node2D` para elementos do *mundo do jogo* (personagens, cenários, projéteis, etc.). Eles interagem com a física e a lógica do jogo.
-   Use `Control` para elementos da *interface do usuário* (HUD, menus, inventário, etc.). Eles são otimizados para layout responsivo e interação com o usuário.

Embora ambos sejam visuais e herdem de `CanvasItem`, eles são otimizados para propósitos diferentes e possuem conjuntos de propriedades e métodos distintos que refletem suas funções. Misturar os dois sem um bom motivo pode levar a problemas de layout e interação.

---

### 8. Node3D: A Base do 3D

Análogo ao `Node2D`, o `Node3D` (anteriormente `Spatial` na Godot 3.x) é a classe base para todos os nós que existem no espaço 3D. Ele fornece a fundação para a construção de mundos e objetos tridimensionais na Godot Engine.

#### O que é?
`Node3D` fornece a transformação 3D fundamental (posição, rotação, escala) para objetos no mundo 3D. Ele é o ponto de partida para qualquer objeto que precise ter uma localização e orientação no espaço tridimensional. `MeshInstance3D`, `CharacterBody3D`, `Camera3D`, `Light3D`, etc., todos herdam de `Node3D`.

#### Principais Propriedades e Métodos
-   **Transformação Local:**
    -   `position: Vector3`: Posição local do nó em relação ao seu pai.
    -   `rotation: Vector3`: Rotação local do nó em ângulos de Euler (em radianos).
    -   `rotation_degrees: Vector3`: Rotação local do nó em ângulos de Euler (em graus). Mais intuitivo para muitos desenvolvedores.
    -   `scale: Vector3`: Escala local do nó.
    -   `quaternion: Quaternion`: Rotação local como um Quatérnio. Quatérnios são mais robustos para interpolação de rotações e evitam o problema de "gimbal lock" que pode ocorrer com ângulos de Euler.
-   **Transformação Global:**
    -   `global_position: Vector3`: Posição global do nó no mundo.
    -   `global_rotation: Vector3`: Rotação global do nó em ângulos de Euler.
    -   `global_scale: Vector3`: Escala global do nó.
    -   `global_transform: Transform3D`: A matriz de transformação 3D completa (posição, rotação e escala global). É a forma mais robusta e eficiente de manipular a transformação global de um nó.
-   **`transform: Transform3D`:** A matriz de transformação 3D completa (posição, rotação e escala local). Manipular o `transform` diretamente é frequentemente mais eficiente e preciso do que manipular `position`, `rotation` e `scale` separadamente, especialmente para operações complexas.
-   **Métodos de Movimento e Orientação:**
    -   `look_at(target: Vector3, up: Vector3 = Vector3.UP)`: Rotaciona o nó para "olhar" para um ponto no espaço 3D. O vetor `up` define qual direção é "para cima" para o nó.
    -   `translate(offset: Vector3)`: Move o nó por um vetor de offset em seu espaço local.
    -   `rotate_x(angle: float)`, `rotate_y(angle: float)`, `rotate_z(angle: float)`: Gira o nó em torno de seus eixos locais X, Y ou Z, respectivamente.
    -   `to_global(local_point: Vector3)`: Converte uma coordenada local para global.
    -   `to_local(global_point: Vector3)`: Converte uma coordenada global para local.

#### Exemplo de Código (GDScript - Expandido)
```gdscript
# player_3d.gd
extends CharacterBody3D

@export var speed: float = 5.0
@export var rotation_speed: float = 2.0 # Radianos por segundo
@export var jump_velocity: float = 5.0

var target_look_at_position: Vector3 = Vector3.ZERO

func _physics_process(delta: float):
    var input_dir = Input.get_vector("move_left", "move_right", "move_forward", "move_backward")
    var direction = (transform.basis * Vector3(input_dir.x, 0, input_dir.y)).normalized()

    if is_on_floor():
        if Input.is_action_just_pressed("jump"):
            velocity.y = jump_velocity
    else:
        velocity.y -= ProjectSettings.get_setting("physics/3d/default_gravity") * delta

    if direction:
        velocity.x = direction.x * speed
        velocity.z = direction.z * speed
    else:
        velocity.x = move_toward(velocity.x, 0, speed)
        velocity.z = move_toward(velocity.z, 0, speed)

    move_and_slide()

    # Exemplo de rotação para olhar para um alvo
    if target_look_at_position != Vector3.ZERO:
        look_at(target_look_at_position, Vector3.UP)

func set_target_to_look_at(target_pos: Vector3):
    target_look_at_position = target_pos

func _ready():
    print("Player 3D pronto!")
```

#### Dicas e Melhores Práticas
-   **Transformações 3D:** Entenda os conceitos de posição, rotação (ângulos de Euler vs. Quatérnios) e escala em 3D. Para rotações complexas ou interpolação suave, prefira `Quaternion` para evitar "gimbal lock".
-   **Eixos:** Lembre-se de que no Godot 3D, o eixo Y geralmente aponta para cima, o X para a direita e o Z para frente (em um sistema de coordenadas destro).
-   **`look_at()`:** Muito útil para câmeras, inimigos ou qualquer objeto que precise "encarar" um alvo. Pode ser combinado com interpolação para um movimento de câmera ou rotação mais suave.
-   **`Transform3D`:** Manipular o `transform` diretamente é a forma mais eficiente e robusta de aplicar múltiplas transformações (translação, rotação, escala) de uma vez, pois evita recálculos intermediários.
-   **Composição:** Assim como no 2D, a composição de `Node3D`s é a abordagem preferida. Um `Player` pode ser um `CharacterBody3D` que *tem* um `MeshInstance3D` (para o modelo), uma `Camera3D` e outros nós como filhos.

---

### 9. Variant, Callable e Signal: A Santíssima Trindade da Comunicação

Estas três classes/tipos são fundamentais para a flexibilidade, comunicação e interoperabilidade na Godot Engine, especialmente entre GDScript e C++ (via GDExtension).

#### 9.1. `Variant`: O Tipo Universal

*   **O que é?** `Variant` é um tipo de dado universal que pode armazenar qualquer outro tipo da Godot (int, float, String, Vector2, Object, Node, Resource, Array, Dictionary, etc.). Ele é a "cola" que permite a comunicação flexível entre GDScript e C++, e é o que possibilita a tipagem dinâmica do GDScript. Em C++, `Variant` é uma classe que encapsula e gerencia a memória de forma segura para o tipo de dado que contém.
*   **Funcionalidades Chave:**
    *   **Flexibilidade:** Pode assumir qualquer tipo de dado Godot.
    *   **Interoperabilidade:** Usado para passar dados entre GDScript e C++ de forma transparente.
    *   **Gerenciamento de Memória:** Para tipos `RefCounted` e `Object`s, o `Variant` gerencia a contagem de referências ou a vida útil, garantindo a segurança da memória.
    *   **Introspecção:** Possui métodos como `get_type()` para verificar o tipo de dado que ele contém em tempo de execução.
*   **Casos de Uso:** Argumentos e retornos de funções `call()`, parâmetros de sinais, armazenamento em `Array`s e `Dictionary`s, comunicação entre linguagens.

#### 9.2. `Callable`: A Referência a Funções

*   **O que é?** `Callable` é um `Object` que representa uma referência a uma função ou método. Ele "chama" uma função em um objeto específico. É a evolução do `FuncRef` da Godot 3 e é uma parte central do novo sistema de sinais e `await` na Godot 4. `Callable`s permitem tratar funções como objetos de primeira classe.
*   **Funcionalidades Chave:**
    *   **Conexão de Sinais:** Usado para conectar sinais a métodos de forma segura e tipada.
    *   **Passagem de Funções:** Pode ser passado como argumento para outras funções, permitindo callbacks flexíveis.
    *   **Operações Assíncronas:** Usado com `await` para esperar a conclusão de operações assíncronas.
    *   **`bind(...)`:** Permite "pré-vincular" argumentos a um `Callable`, que serão passados para a função quando ela for chamada.
*   **Casos de Uso:** Conectar sinais, implementar padrões de design como Command ou Strategy, callbacks para timers ou animações, agendamento de tarefas.

#### 9.3. `Signal`: O Padrão Observer em Objeto

*   **O que é?** `Signal` é um `Object` que representa um sinal. Na Godot 4, os sinais são tratados como objetos de primeira classe, o que torna a conexão e desconexão mais robustas e explícitas. O sistema de sinais é a implementação nativa da Godot do padrão de design **Observer (Publish/Subscribe)**.
*   **Funcionalidades Chave:**
    *   **Desacoplamento:** Permite que objetos se comuniquem sem ter conhecimento direto uns dos outros.
    *   **Event-Driven:** Facilita a criação de arquiteturas orientadas a eventos.
    *   **Conexão/Desconexão:** Métodos `connect()` e `disconnect()` para gerenciar ouvintes.
    *   **Emissão:** Método `emit()` para disparar o sinal e notificar os ouvintes.
*   **Casos de Uso:** Notificar a UI sobre mudanças no estado do jogador, comunicar eventos entre sistemas, implementar sistemas de eventos globais.

#### Exemplo de Código (GDScript - Expandido)
```gdscript
# player.gd
extends CharacterBody2D

signal health_changed(new_health: int) # Sinal com argumento tipado
signal player_died() # Sinal sem argumentos

var current_health: int = 100

func take_damage(amount: int):
    current_health -= amount
    current_health = max(0, current_health)
    health_changed.emit(current_health) # Emite o sinal com o novo valor de vida
    print("Jogador recebeu ", amount, " de dano. Vida atual: ", current_health)
    if current_health <= 0:
        player_died.emit() # Emite o sinal de morte

# ui_health_bar.gd
extends TextureProgressBar

func _ready():
    # Encontra o jogador (assumindo que é um nó irmão ou em um caminho conhecido)
    var player_node = get_node("../Player") as Player
    if player_node:
        # Conectando o sinal 'health_changed' do player a um método 'update_health_bar' neste script.
        # Usando Callable para conexão segura.
        player_node.health_changed.connect(Callable(self, "update_health_bar"))
        player_node.player_died.connect(Callable(self, "_on_player_died"))
        max_value = player_node.current_health # Inicializa a barra de vida
        value = player_node.current_health
    else:
        push_error("Player não encontrado para conectar o sinal de vida!")

func update_health_bar(new_health: int):
    value = new_health
    print("Barra de vida atualizada para: ", new_health)

func _on_player_died():
    print("Jogador morreu! Exibindo tela de Game Over.")
    # Lógica para exibir tela de Game Over

# game_manager.gd (Autoload)
extends Node

@onready var player_node: Player = $"/root/Game/Player" # Acessa o jogador globalmente

func _ready():
    if player_node:
        # Conectando um sinal com Callable.bind() para passar argumentos adicionais
        player_node.player_died.connect(Callable(self, "_handle_game_over").bind("O jogador foi derrotado!"))

func _handle_game_over(message: String):
    print("GAME OVER! Mensagem: ", message)
    get_tree().paused = true
    # Lógica para reiniciar o jogo ou ir para o menu principal
```

#### Dicas e Melhores Práticas
-   **`Variant` para Flexibilidade:** Use `Variant` quando precisar de flexibilidade para lidar com diferentes tipos de dados, especialmente em APIs genéricas ou ao interagir com GDScript de C++.
-   **`Callable` para Conexões Seguras:** Prefira usar `Callable` para conectar sinais, pois é mais robusto e tipado do que usar strings (como na Godot 3.x). Use `Callable.bind()` para passar argumentos adicionais.
-   **Sinais para Desacoplamento:** Utilize sinais extensivamente para comunicação entre objetos. Isso reduz o acoplamento, tornando seu código mais modular, fácil de testar e manter. Em vez de um objeto chamar diretamente um método em outro, ele emite um sinal, e o outro objeto (se interessado) se conecta a ele.
-   **Sinais Customizados:** Defina seus próprios sinais (`signal my_signal(...)`) para eventos importantes em suas classes, tornando-as mais reutilizáveis e extensíveis.
-   **`await` com `Callable`:** Use `await` com `Callable` para esperar a conclusão de operações assíncronas de forma limpa e sequencial, evitando "callback hell".

---

### 10. ClassDB: O Registro de Classes (GDExtension)

`ClassDB` não é uma classe que você instancia, mas um singleton global usado internamente pela Godot Engine. Ele é crucial para o desenvolvimento com **GDExtension**, pois é o mecanismo pelo qual suas classes C++ customizadas são registradas e expostas ao motor, tornando-as acessíveis em GDScript e no editor.

#### O que é?
`ClassDB` é o banco de dados de classes da Godot. Ele mantém um registro de todas as classes disponíveis no motor, suas propriedades, métodos, sinais e constantes. Quando você cria uma classe em C++ via GDExtension e quer que a Godot a reconheça e a trate como uma classe nativa (permitindo que ela apareça no "Create New Node" ou seja instanciada em GDScript), você a registra no `ClassDB`.

#### Principais Métodos (C++ - GDExtension)
-   **`ClassDB::register_class<T>()`:** Registra uma classe C++ no motor. Isso a torna visível para o sistema de tipos da Godot.
    ```cpp
    // No seu _gdextension_initialize
    ClassDB::register_class<MyCustomNode>();
    ClassDB::register_class<MyCustomResource>();
    ```
-   **`ClassDB::bind_method(D_METHOD(...), &MyClass::my_method)`:** Expõe um método C++ para ser chamado pelo GDScript e pelo editor. `D_METHOD` é uma macro que cria um `MethodInfo` com o nome do método e os nomes dos argumentos, que são usados para reflexão.
    ```cpp
    // No _bind_methods de MyCustomNode
    ClassDB::bind_method(D_METHOD("my_cpp_function", "value"), &MyCustomNode::my_cpp_function);
    ```
-   **`ClassDB::add_property("MyClass", PropertyInfo(...), "setter", "getter")`:** Expõe uma propriedade C++ para o Inspector e GDScript. Requer métodos `setter` e `getter` correspondentes na sua classe C++.
    ```cpp
    // No _bind_methods de MyCustomNode
    ADD_PROPERTY(PropertyInfo(Variant::FLOAT, "speed", PROPERTY_HINT_RANGE, "0,1000,0.1"), "set_speed", "get_speed");
    ```
-   **`ClassDB::add_signal("MyClass", MethodInfo(...))`:** Expõe um sinal C++ para ser conectado no GDScript e no editor. `MethodInfo` define o nome do sinal e seus argumentos.
    ```cpp
    // No _bind_methods de MyCustomNode
    ADD_SIGNAL(MethodInfo("custom_cpp_signal", PropertyInfo(Variant::INT, "data")));
    ```
-   **`BIND_ENUM_CONSTANT(ENUM_VALUE)`:** Para expor valores de enumerações C++ à Godot, tornando-os acessíveis em GDScript e no editor.
    ```cpp
    // No _bind_methods de MyCustomNode
    BIND_ENUM_CONSTANT(MyCustomNode::MY_ENUM_VALUE_ONE);
    ```

#### Casos de Uso e Importância
O uso do `ClassDB` é o coração da interoperabilidade entre C++ e o resto do motor. Ele permite que suas extensões nativas se comportem como se fossem parte integrante da Godot, com todos os benefícios de reflexão, serialização e integração com o editor. Sem o `ClassDB`, suas classes C++ seriam invisíveis para a Godot e não poderiam ser usadas de forma integrada.

#### Dicas e Melhores Práticas
-   **Consistência:** Mantenha a consistência na nomenclatura de métodos e propriedades expostas para GDScript. Siga as convenções da Godot (snake_case para métodos, PascalCase para classes).
-   **Hints de Propriedade:** Use `PROPERTY_HINT`s em `PropertyInfo` para fornecer uma melhor experiência de edição no Inspector da Godot (ex: sliders para ranges, dropdowns para enums, seletores de arquivo).
-   **Documentação:** Comente seus métodos e propriedades no C++ para que a documentação apareça no editor da Godot ao usar o autocompletar ou a ajuda contextual.

---

### 11. Outras Classes Fundamentais (Breve Visão Geral)

Embora as classes acima sejam a espinha dorsal, muitas outras são cruciais para o desenvolvimento de jogos. Esta seção oferece uma breve visão geral de algumas delas, com a intenção de aprofundar em documentos específicos.

*   **`Input` (Singleton):** Gerencia todos os eventos de entrada (teclado, mouse, gamepad). Essencial para a interação do jogador.
*   **`Engine` (Singleton):** Fornece acesso a informações e funcionalidades globais do motor, como `Engine.get_frames_per_second()` ou `Engine.is_editor_hint()`.
*   **`ProjectSettings` (Singleton):** Permite acessar e modificar as configurações do projeto (`project.godot`) em tempo de execução.
*   **`Timer`:** Um nó para agendar chamadas de função ou eventos após um determinado tempo. Fundamental para cooldowns, atrasos e eventos temporizados.
*   **`Tween`:** Um nó poderoso para animar propriedades de qualquer objeto de forma suave e flexível. Ideal para animações de UI, movimento de objetos, etc.
*   **`FileAccess`:** Para ler e escrever arquivos no sistema de arquivos. Essencial para sistemas de salvamento/carregamento customizados.
*   **`ResourceLoader` / `ResourceSaver`:** Para carregar e salvar `Resources` programaticamente.

---

### 12. Conclusão: A Teia Interconectada de Classes da Godot

As classes da Godot Engine formam uma teia interconectada, onde cada componente desempenha um papel vital na construção de jogos. Desde a base abstrata de `Object` até os nós visuais especializados como `Node2D` e `Node3D`, e os mecanismos de comunicação como `Variant`, `Callable` e `Signal`, cada classe é projetada para ser modular, flexível e eficiente. Dominar essas classes é o caminho para desbloquear todo o potencial da Godot e criar experiências de jogo ricas e performáticas. A integração com C++ via GDExtension amplia ainda mais essas possibilidades, permitindo que você estenda o motor em seus próprios termos, com a performance e o controle que o C++ oferece.

## 13. Licença

Este documento e o projeto ao qual ele se refere estão licenciados sob a Licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.

Copyright (c) 2025 MokaCode by Machi

---

### 2. RefCounted: Gerenciamento Automático de Memória

`RefCounted` (Reference-Counted) herda de `Object` e adiciona uma funcionalidade crucial e elegante: **gerenciamento automático de memória por contagem de referências**.

#### O que é?
É a classe base para objetos que não estão na árvore de cenas, mas cujo ciclo de vida deve ser gerenciado automaticamente. A ideia é simples: o objeto mantém um contador interno de quantas variáveis ou outros objetos estão "apontando" para ele. Quando esse contador chega a zero, o objeto se libera automaticamente da memória. Isso elimina a necessidade de chamar `free()` manualmente, prevenindo uma classe inteira de bugs de gerenciamento de memória.

#### Principais Funcionalidades e Métodos
- `init_ref() -> bool`: Inicializa a contagem de referências. Raramente chamado manualmente.
- `reference() -> bool`: Incrementa o contador de referências. Raramente chamado manualmente.
- `unreference() -> bool`: Decrementa o contador de referências. Se o contador chegar a zero, o objeto é liberado. Raramente chamado manualmente.
- `get_reference_count() -> int`: Retorna o número atual de referências ao objeto. Útil para depuração.

#### A Armadilha: Referências Cíclicas
O principal problema da contagem de referências são as **referências cíclicas**. Se o `ObjetoA` (um `RefCounted`) contém uma referência forte ao `ObjetoB` (outro `RefCounted`), e o `ObjetoB` contém uma referência forte de volta ao `ObjetoA`, a contagem de referências de ambos nunca chegará a zero, mesmo que nenhuma outra parte do código os esteja usando. Isso cria um vazamento de memória.

**Solução:** Use referências fracas com `weakref()`. Uma referência fraca permite acessar o objeto, mas não incrementa seu contador de referências, quebrando o ciclo.

```gdscript
var obj_a = RefCounted.new()
var obj_b = RefCounted.new()

obj_a.parceiro = obj_b # Referência forte de A para B
obj_b.parceiro = weakref(obj_a) # Referência FRACA de B para A

# Para acessar a referência fraca, você precisa chamar get_ref()
var ref_para_a = obj_b.parceiro.get_ref()
if ref_para_a:
    print("Objeto A ainda existe.")
else:
    print("Objeto A foi liberado.")
```

#### Relação com Outras Classes
- **`Resource` é um `RefCounted`:** Esta é a principal razão pela qual `RefCounted` é tão importante. Todos os recursos (texturas, scripts, cenas, materiais) são gerenciados por contagem de referências.

#### Dicas e Melhores Práticas
- Use `RefCounted` (ou `Resource`) para objetos de dados que precisam ser compartilhados entre múltiplos nós.
- Em C++, sempre use o smart pointer `Ref<T>` para gerenciar instâncias de classes que herdam de `RefCounted`. Ex: `Ref<MyCustomResource>`. Ele gerencia a contagem de referências automaticamente.
- Fique atento a possíveis referências cíclicas, especialmente em estruturas de dados complexas como grafos ou árvores duplamente ligadas. Use `weakref()` para quebrá-las.

---

### 3. Resource: Os Blocos de Construção de Dados

A classe `Resource` é uma das mais poderosas e centrais da Godot. Ela herda de `RefCounted` e representa qualquer tipo de dado que pode ser salvo no disco e carregado pela engine.

#### O que é?
Um `Resource` é um bloco de dados reutilizável. Pense em texturas (`Texture2D`), modelos 3D (`Mesh`), clipes de áudio (`AudioStream`), animações (`Animation`), scripts (`GDScript`) e até cenas inteiras (`PackedScene`). Todos são `Resource`s. A filosofia da **Programação Orientada a Resources (ROP)**, que o MokaCode CLI segue, incentiva o uso de `Resource`s customizados para encapsular dados e até mesmo lógica.

#### Principais Propriedades e Métodos
- `resource_path: String`: O caminho do arquivo no disco (`res://...`) de onde o recurso foi carregado.
- `resource_name: String`: O nome do recurso.
- `take_over_path(path: String)`: Define o `resource_path`.
- `duplicate(subresources: bool = false) -> Resource`: Cria uma cópia do recurso. Se `subresources` for `true`, os sub-recursos dentro dele também são duplicados. É crucial usar `duplicate()` se você quiser modificar um recurso em tempo de execução sem afetar todas as outras instâncias que o utilizam.

#### Criando Resources Customizados
Este é o superpoder da ROP. Você pode criar seus próprios tipos de `Resource` para modelar os dados do seu jogo.

```gdscript
# item_data.gd
class_name ItemData
extends Resource

@export var nome: String = "Novo Item"
@export_multiline var descricao: String
@export var icone: Texture2D
@export var empilhavel: bool = true
@export_range(1, 99) var max_pilha: int = 1

func usar(alvo: Node):
    print("Usando '", nome, "' em '", alvo.name, "'")
    # Adicione a lógica de uso do item aqui
```

**Como usar:**
1. No FileSystem, clique com o botão direito -> `New Resource...` -> procure por `ItemData`.
2. Salve o arquivo (ex: `espada.tres`).
3. No Inspector, preencha as propriedades (nome, descrição, ícone, etc.).
4. Em um script, você pode exportar uma variável do tipo `ItemData` e arrastar seu arquivo `.tres` para ela.

```gdscript
# player.gd
extends CharacterBody2D

@export var item_equipado: ItemData

func _input(event):
    if event.is_action_pressed("usar_item"):
        if item_equipado:
            item_equipado.usar(self)
```

#### Dicas e Melhores Práticas
- **Separe Dados da Lógica de Cena:** Use `Resource`s para armazenar dados de personagens, inimigos, itens, habilidades, etc. Os `Node`s na cena (a parte visual) devem ler os dados desses `Resource`s. Isso torna seu jogo mais fácil de balancear e manter.
- **`preload()` vs `load()`:**
  - `preload("path/to/resource.tres")`: Carrega o recurso em tempo de compilação. Causa um erro se o arquivo não for encontrado. É mais rápido em tempo de execução. Use para recursos que você sabe que sempre precisará.
  - `load("path/to/resource.tres")`: Carrega o recurso em tempo de execução. Retorna `null` se o arquivo não for encontrado. É mais flexível e útil para carregamento dinâmico.
- **Sempre use `duplicate()`:** Se você pretende modificar um `Resource` em tempo de execução (ex: diminuir a quantidade de uma poção no inventário), sempre chame `.duplicate()` ao instanciá-lo. Caso contrário, você modificará o arquivo base compartilhado, afetando todos os outros lugares que o usam.

---

### 4. Node: Os Átomos da Árvore de Cenas

Se `Object` é a origem de tudo, `Node` é a origem de tudo que **vive na árvore de cenas**. É a classe base para todos os elementos que compõem seu jogo, desde sprites e modelos 3D até timers e gerenciadores de UI.

#### O que é?
Um `Node` é um bloco de construção que pode ser adicionado à `SceneTree` (Árvore de Cenas). Ele herda de `Object`, então possui todas as suas funcionalidades (sinais, metaprogramação), mas adiciona conceitos cruciais:
- Hierarquia (pais e filhos)
- Processamento de ciclo de vida (`_ready`, `_process`, etc.)
- Grupos
- Acesso à `SceneTree`

#### Principais Propriedades e Métodos

- **Gerenciamento da Árvore:**
  - `get_parent() -> Node`: Retorna o nó pai.
  - `get_child(idx: int) -> Node`: Retorna um filho pelo seu índice.
  - `get_children() -> Array[Node]`: Retorna um array com todos os filhos.
  - `get_node(path: NodePath) -> Node`: Encontra um nó na árvore usando seu caminho. O atalho `$` (ex: `$Sprite2D`) é uma forma mais concisa de usar `get_node()`.
  - `add_child(node: Node)`: Adiciona um nó como filho deste.
  - `remove_child(node: Node)`: Remove um nó filho.
  - `queue_free()`: Remove o nó da árvore e o libera da memória de forma segura.

- **Ciclo de Vida (Callbacks):**
  - `_enter_tree()`: Chamado quando o nó entra na `SceneTree`.
  - `_ready()`: Chamado uma vez quando o nó e todos os seus filhos estão prontos. Ideal para inicialização.
  - `_process(delta: float)`: Chamado a cada frame. Para lógica geral.
  - `_physics_process(delta: float)`: Chamado em intervalos fixos. Para lógica de física.
  - `_input(event: InputEvent)`: Chamado para cada evento de entrada.
  - `_exit_tree()`: Chamado quando o nó está prestes a sair da `SceneTree`. Ideal para limpeza.

- **Outros:**
  - `name: String`: O nome do nó.
  - `owner: Node`: O nó raiz da cena à qual este nó pertence.
  - `get_tree() -> SceneTree`: Retorna a `SceneTree` à qual o nó pertence.
  - `is_in_group(group: String) -> bool`: Verifica se o nó pertence a um grupo.
  - `add_to_group(group: String)`: Adiciona o nó a um grupo.

#### Relação com `SceneTree`
Um `Node` só se torna "ativo" (ou seja, seus métodos de ciclo de vida são chamados) quando ele é adicionado à `SceneTree`. A `SceneTree` é a responsável por orquestrar a execução de todos os nós.

#### Exemplo de Código (GDScript)
```gdscript
# player.gd
extends Node2D

func _ready():
    print("O nó '", self.name, "' está pronto!")
    print("Seu pai é: ", get_parent().name)
    
    # Adicionar um novo nó como filho
    var timer = Timer.new()
    timer.name = "MeuTimer"
    add_child(timer)
    
    # Acessar o filho recém-adicionado
    var meu_timer_ref = $MeuTimer
    # ou
    var meu_timer_ref2 = get_node("MeuTimer")
    
    print("Filho adicionado: ", meu_timer_ref.name)

func _process(delta):
    # Este código será executado a cada frame
    pass
```

#### Dicas e Melhores Práticas
- **Composição sobre Herança:** A Godot incentiva a construção de objetos complexos compondo `Node`s simples, em vez de criar hierarquias de herança de scripts muito profundas. Um `Player` é um `CharacterBody2D` que *tem* um `Sprite2D`, uma `CollisionShape2D` e um `AnimationPlayer` como filhos.
- **`@onready`:** Use a anotação `@onready var meu_no = $Caminho/Para/O/No` para inicializar variáveis com referências a outros nós. Isso garante que a referência seja obtida somente quando a árvore estiver pronta, evitando erros.
- **Grupos:** Use grupos para desacoplar o código. Em vez de um inimigo procurar pelo nó "Player", ele pode procurar por todos os nós no grupo "players". Isso permite ter múltiplos jogadores ou testar cenas de inimigos de forma isolada.

---

### 5. SceneTree: O Coração Pulsante do Jogo

A `SceneTree` é a classe que gerencia a hierarquia de nós e o fluxo principal do jogo. Embora você raramente instancie uma `SceneTree` manualmente, você a acessa constantemente a partir de qualquer `Node` usando `get_tree()`.

#### O que é?
É um singleton de fato que atua como o `MainLoop` (loop principal) do seu jogo. Ela contém a cena atualmente ativa, gerencia o estado do jogo (pausa, etc.) e propaga os callbacks (`_process`, `_input`, etc.) para todos os nós na árvore.

#### Principais Propriedades e Métodos
- **Gerenciamento de Cenas:**
  - `current_scene: Node`: O nó raiz da cena atualmente ativa.
  - `change_scene_to_file(path: String) -> Error`: Muda a cena atual para uma nova cena a partir de um arquivo. A cena antiga é liberada.
  - `change_scene_to_packed(packed_scene: PackedScene) -> Error`: O mesmo, mas usando um recurso `PackedScene` já carregado.
  - `reload_current_scene() -> Error`: Recarrega a cena atual.

- **Gerenciamento de Estado:**
  - `paused: bool`: Se `true`, o jogo é pausado. `_process` não será chamado em nós normais, mas `_physics_process` ainda será (a menos que o modo de pausa do nó seja alterado).
  - `quit(exit_code: int = 0)`: Encerra o jogo.

- **Gerenciamento de Nós e Grupos:**
  - `get_nodes_in_group(group: String) -> Array[Node]`: Retorna um array com todos os nós em um grupo.
  - `call_group(group: String, method: String, ...)`: Chama um método em todos os nós de um grupo.
  - `get_first_node_in_group(group: String) -> Node`: Retorna o primeiro nó encontrado em um grupo.

#### Exemplo de Código (GDScript)
```gdscript
# game_manager.gd (um AutoLoad/Singleton)
extends Node

func _unhandled_input(event):
    # Pausar/despausar o jogo com a tecla 'P'
    if event.is_action_pressed("pause_toggle"):
        get_tree().paused = not get_tree().paused
        print("Jogo pausado: ", get_tree().paused)

func game_over():
    print("Fim de jogo!")
    # Notificar todos os inimigos para pararem
    get_tree().call_group("enemies", "stop_ai")
    # Recarregar a cena após 2 segundos
    await get_tree().create_timer(2.0).timeout
    get_tree().reload_current_scene()

func go_to_main_menu():
    get_tree().change_scene_to_file("res://scenes/main_menu.tscn")
```

---

### 6. PackedScene: O Molde da Cena

Uma `PackedScene` é um `Resource` que contém uma cena serializada. É o "molde" ou "blueprint" que você usa para criar novas instâncias de cenas em tempo de execução.

#### O que é?
Quando você salva uma cena no editor (um arquivo `.tscn`), você está, na verdade, criando um `PackedScene`. Este recurso armazena a estrutura da árvore de nós, suas propriedades, scripts anexados e conexões de sinais.

#### Principal Método
- `instantiate() -> Node`: Este é o método chave. Ele cria uma nova instância da árvore de nós que a `PackedScene` representa e retorna o nó raiz dessa nova instância.

#### Casos de Uso Comuns
- **Inimigos e Personagens:** Crie uma cena para seu inimigo (`inimigo.tscn`) e a instancie sempre que um novo inimigo precisar aparecer.
- **Projéteis:** Crie uma cena para sua bala (`bala.tscn`) e a instancie toda vez que o jogador atirar.
- **Efeitos Visuais:** Crie uma cena para uma explosão (`explosao.tscn`) e a instancie no local desejado.
- **Itens Coletáveis:** Moedas, poções, etc.

#### Exemplo de Código (GDScript)
```gdscript
# weapon.gd
extends Node2D

# Carrega a cena da bala uma vez para otimização
const BULLET_SCENE = preload("res://scenes/bullet.tscn")

func _process(delta):
    if Input.is_action_just_pressed("shoot"):
        shoot()

func shoot():
    # 1. Instancia a cena da bala
    var new_bullet = BULLET_SCENE.instantiate()

    # 2. Adiciona a nova instância à árvore de cenas
    # get_owner() é uma forma de garantir que a bala seja adicionada à cena principal
    get_owner().add_child(new_bullet)

    # 3. Configura a posição e rotação da bala
    new_bullet.global_transform = self.global_transform
```

---

### 7. CanvasItem, Node2D e Control: A Base do 2D

Essas três classes formam a hierarquia fundamental para toda a renderização 2D.

- **`CanvasItem`**: É a classe base para tudo que é desenhado em 2D. Ela fornece funcionalidades de visibilidade (`visible`), cor (`modulate`, `self_modulate`), materiais (`material`) e ordem de desenho (`z_index`). Ela não pode ser instanciada diretamente.

- **`Node2D`**: Herda de `CanvasItem`. É a classe base para todos os nós 2D que possuem uma **transformação espacial** (posição, rotação, escala). `Sprite2D`, `CharacterBody2D`, `Area2D`, `Camera2D`, etc., todos herdam de `Node2D`.
  - **Propriedades Chave:** `position`, `rotation`, `scale`, `global_position`, `global_rotation`, `global_scale`.
  - **Métodos Chave:** `look_at()`, `translate()`, `rotate()`, `to_local()`, `to_global()`.

- **`Control`**: Também herda de `CanvasItem`. É a classe base para todos os **nós de UI**. Além das propriedades de `CanvasItem`, `Control` adiciona conceitos de **retângulos, âncoras e margens** para criar interfaces de usuário responsivas. `Button`, `Label`, `Panel`, `HBoxContainer`, etc., todos herdam de `Control`.
  - **Propriedades Chave:** `layout_mode`, `anchor_left`, `anchor_top`, `anchor_right`, `anchor_bottom`, `offset_left`, `offset_top`, etc., `size`, `position`.
  - **Métodos Chave:** `get_rect()`, `set_anchors_preset()`.

**A Diferença Crucial:** Use `Node2D` para elementos do *mundo do jogo* (personagens, cenários, projéteis). Use `Control` para elementos da *interface do usuário* (HUD, menus, inventário). Embora ambos sejam visuais, eles são otimizados para propósitos diferentes.

---

### 8. Node3D: A Base do 3D

Análogo ao `Node2D`, o `Node3D` (anteriormente `Spatial` na Godot 3.x) é a classe base para todos os nós que existem no espaço 3D.

#### O que é?
`Node3D` fornece a transformação 3D fundamental (posição, rotação, escala) para objetos no mundo 3D. `MeshInstance3D`, `CharacterBody3D`, `Camera3D`, `Light3D`, etc., todos herdam de `Node3D`.

#### Principais Propriedades e Métodos
- **`position: Vector3`**: Posição local.
- **`rotation: Vector3`**: Rotação local (ângulos de Euler).
- **`rotation_degrees: Vector3`**: Rotação local em graus.
- **`scale: Vector3`**: Escala local.
- **`quaternion: Quaternion`**: Rotação local como um Quatérnio (melhor para interpolação).
- **`global_position: Vector3`**: Posição global.
- **`transform: Transform3D`**: A matriz de transformação 3D completa (posição, rotação e escala). É a forma mais robusta de manipular a transformação.
- **`look_at(target: Vector3, up: Vector3 = Vector3.UP)`**: Rotaciona o nó para "olhar" para um ponto no espaço.

---

### 9. Variant, Callable e Signal: A Santíssima Trindade da Comunicação

- **`Variant`**: É um tipo de dado universal que pode armazenar qualquer outro tipo da Godot (int, float, String, Vector2, Object, etc.). É a "cola" que permite a comunicação flexível entre GDScript e C++, e é o que possibilita a tipagem dinâmica do GDScript.

- **`Callable`**: É um `Object` que representa uma função. Ele "chama" uma função em um objeto. É a evolução do `FuncRef` da Godot 3. `Callable`s são usados para conectar sinais, passar funções como argumentos e para operações assíncronas com `await`.

- **`Signal`**: É um `Object` que representa um sinal. No GDScript 2.x, você pode tratar os próprios sinais como objetos de primeira classe, o que torna a conexão e desconexão mais robustas e explícitas.

```gdscript
# player.gd
signal health_changed(new_health: int)

func take_damage(amount: int):
    health -= amount
    health_changed.emit(health) # Emite o sinal

# ui.gd
func _ready():
    var player = get_node("../Player")
    # Conectando o sinal 'health_changed' do player a um método 'update_health_bar' neste script.
    player.health_changed.connect(update_health_bar)

func update_health_bar(new_health: int):
    $HealthBar.value = new_health
```

---

### 10. ClassDB: O Registro de Classes (GDExtension)

`ClassDB` não é uma classe que você instancia, mas um singleton global usado internamente, crucial para o desenvolvimento com **GDExtension**.

#### O que é?
É o banco de dados que a Godot usa para registrar todas as classes disponíveis no motor, incluindo as suas classes C++ customizadas. Quando você cria uma classe em C++ e quer que a Godot a reconheça, você a registra no `ClassDB`.

#### Principais Métodos (C++)
- `ClassDB::register_class<T>()`: Registra uma classe C++ no motor.
- `ClassDB::bind_method(D_METHOD(...), &MyClass::my_method)`: Expõe um método C++ para ser chamado pelo GDScript e pelo editor.
- `ClassDB::add_property("MyClass", PropertyInfo(...), "setter", "getter")`: Expõe uma propriedade C++ para o Inspector e GDScript.
- `ClassDB::add_signal("MyClass", MethodInfo(...))`: Expõe um sinal C++ para ser conectado no GDScript e no editor.

O uso do `ClassDB` é o coração da interoperabilidade entre C++ e o resto do motor, permitindo que suas extensões nativas se comportem como se fossem parte integrante da Godot.
