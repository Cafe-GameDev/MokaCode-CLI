Classes.md

# Classes Essenciais da Godot Engine: Um Guia Abrangente (Godot 4.5.1)


Este documento serve como um "ebook" detalhado sobre as classes mais utilizadas e fundamentais da Godot Engine, com foco na versão 4.5.1. Ele é projetado para ser um recurso completo para desenvolvedores que desejam aprofundar seu conhecimento sobre a arquitetura de nós e cenas da Godot, otimizando o desenvolvimento de jogos e plugins.

## 1. Introdução: A Filosofia de Classes da Godot Engine

A Godot Engine é construída sobre uma arquitetura flexível e modular, onde tudo é um "nó" (Node) ou um "recurso" (Resource). Compreender as classes fundamentais e como elas interagem é crucial para desenvolver jogos eficientes e escaláveis. Este guia explorará as classes mais relevantes, suas funcionalidades e melhores práticas de uso.

A Godot se destaca por sua abordagem baseada em nós, que permite a composição de funcionalidades complexas a partir de blocos de construção menores e reutilizáveis. Cada nó possui um propósito específico e pode ser combinado com outros para criar cenas interativas e dinâmicas. Além disso, o sistema de recursos (Resources) complementa essa filosofia, permitindo a criação de dados configuráveis e comportamentos que podem ser compartilhados e gerenciados de forma eficiente.

Este ebook não apenas descreverá as classes, mas também fornecerá exemplos práticos, dicas de otimização e insights sobre como integrar essas classes em seus projetos, seja você um desenvolvedor de jogos 2D, 3D ou um criador de plugins para o editor.

## 2. Conceitos Fundamentais

Nesta seção, exploraremos as classes que formam a base da Godot Engine, essenciais para entender como o motor funciona e como construir seus projetos de forma eficaz.

### 2.1. `Node`

O `Node` é a classe mais fundamental na Godot Engine. Ele serve como a base para todos os elementos que compõem uma cena. Tudo o que você adiciona à sua árvore de cenas, desde um personagem a um botão de UI, é um `Node` ou herda dele. Eles são os blocos de construção que permitem organizar a lógica do jogo, o comportamento e a estrutura visual.

#### 2.1.1. Descrição

Um `Node` é um objeto genérico que pode ter filhos, ser adicionado a uma árvore de cenas e ter scripts anexados para definir seu comportamento. Ele não possui representação visual ou física por si só, mas fornece a estrutura hierárquica e as funcionalidades básicas para que outros nós mais especializados possam operar.

#### 2.1.2. Uso Comum

*   **Organização da Cena:** Agrupar outros nós para manter a cena organizada (ex: um nó `Node` vazio chamado "Inimigos" para conter todos os inimigos).
*   **Lógica de Jogo Abstrata:** Implementar lógica de jogo que não está diretamente ligada a um elemento visual ou físico específico.
*   **Nó Raiz de Cenas:** Frequentemente, o nó raiz de uma cena é um `Node` simples, que serve como um contêiner para todos os outros elementos da cena.

#### 2.1.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `name`: O nome único do nó dentro de seu pai.
    *   `owner`: O nó que "possui" este nó (geralmente o nó raiz da cena).
    *   `parent`: O nó pai na árvore de cenas.
*   **Métodos:**
    *   `add_child(node: Node)`: Adiciona um nó como filho.
    *   `remove_child(node: Node)`: Remove um nó filho.
    *   `get_node(path: NodePath)`: Obtém uma referência a um nó usando seu caminho.
    *   `queue_free()`: Libera o nó da memória de forma segura no final do frame.
    *   `_ready()`: Callback chamado quando o nó e seus filhos estão prontos na árvore de cenas.
    *   `_process(delta: float)`: Callback chamado a cada frame para lógica de jogo geral.
    *   `_physics_process(delta: float)`: Callback chamado a cada passo de física fixo.
    *   `connect(signal: String, callable: Callable)`: Conecta um sinal a um método.
    *   `emit_signal(signal: String, ...)`: Emite um sinal.

#### 2.1.4. Exemplos de Código

```gdscript
# Exemplo: Organizando nós em uma cena
extends Node

func _ready():
    var player_node = Node2D.new()
    player_node.name = "Player"
    add_child(player_node)

    var enemy_container = Node.new()
    enemy_container.name = "Enemies"
    add_child(enemy_container)

    var goblin = CharacterBody2D.new()
    goblin.name = "Goblin1"
    enemy_container.add_child(goblin)

    # Acessando um nó
    var player = get_node("Player")
    if player:
        print("Player encontrado: ", player.name)

    # Liberando um nó
    # goblin.queue_free()
```

#### 2.1.5. Dicas e Boas Práticas

*   **Organização Hierárquica:** Use nós para criar uma hierarquia lógica e fácil de entender para sua cena.
*   **`queue_free()`:** Sempre use `queue_free()` para remover nós da árvore de cenas. Nunca use `free()` diretamente, pois pode causar erros se o nó ainda estiver sendo processado.
*   **`@onready`:** Utilize `@onready var node_ref = $NodePath` para obter referências a nós filhos de forma segura e eficiente no `_ready()`.
*   **Sinais:** Prefira o sistema de sinais e slots para comunicação entre nós, pois ele promove o desacoplamento.

### 2.2. `SceneTree`

O `SceneTree` é o gerenciador central de todas as cenas e nós em seu jogo. Ele não é um nó visível na árvore de cenas, mas é um singleton global que controla o fluxo do jogo, a transição entre cenas, o processamento de entrada e muito mais.

#### 2.2.1. Descrição

A `SceneTree` é a representação da árvore de cenas ativa do jogo. Ela gerencia a ordem de processamento dos nós, a entrada de eventos, a pausa do jogo e a transição entre diferentes cenas. Cada jogo Godot tem apenas uma `SceneTree` ativa.

#### 2.2.2. Uso Comum

*   **Gerenciamento de Cenas:** Carregar, mudar e descarregar cenas.
*   **Controle de Pausa:** Pausar e despausar o jogo.
*   **Entrada de Eventos:** Propagar eventos de entrada para os nós.
*   **Acesso Global:** Fornecer acesso a informações globais do jogo.

#### 2.2.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `root`: O `Viewport` raiz da árvore de cenas.
    *   `current_scene`: A cena atualmente ativa.
    *   `paused`: Um booleano que indica se o jogo está pausado.
*   **Métodos:**
    *   `change_scene_to_file(path: String)`: Muda para uma nova cena carregada de um arquivo.
    *   `reload_current_scene()`: Recarrega a cena atual.
    *   `quit()`: Sai do jogo.
    *   `set_pause(enable: bool)`: Define o estado de pausa do jogo.
    *   `get_root()`: Retorna o `Viewport` raiz.
    *   `get_nodes_in_group(group: String)`: Retorna uma lista de todos os nós em um grupo específico.

#### 2.2.4. Exemplos de Código

```gdscript
# Exemplo: Mudando de cena e pausando o jogo
extends Node

func _ready():
    print("Cena atual: ", get_tree().current_scene.name)

func _input(event):
    if event.is_action_pressed("ui_cancel"):
        if get_tree().paused:
            get_tree().set_pause(false)
            print("Jogo despausado.")
        else:
            get_tree().set_pause(true)
            print("Jogo pausado.")
    
    if event.is_action_pressed("change_scene"):
        # Certifique-se de que "res://scenes/game_over.tscn" exista
        get_tree().change_scene_to_file("res://scenes/game_over.tscn")
```

#### 2.2.5. Dicas e Boas Práticas

*   **Acesso Global:** Acesse a `SceneTree` usando `get_tree()`.
*   **Transições de Cena:** Para transições mais suaves, considere usar um nó de transição de cena ou um singleton para gerenciar o carregamento assíncrono.
*   **Pausa:** Ao pausar o jogo, lembre-se de que alguns nós podem precisar ter seu `process_mode` definido como `PROCESS_MODE_ALWAYS` para continuar funcionando (ex: menus de pausa).

### 2.3. `Resource`

O `Resource` é uma classe fundamental para a Programação Orientada a Resources (ROP) na Godot. Ele permite encapsular dados e comportamentos em arquivos reutilizáveis, que podem ser carregados e configurados no editor.

#### 2.3.1. Descrição

Um `Resource` é um objeto que pode ser salvo em disco (como arquivos `.tres` ou `.res`) e carregado em tempo de execução. Diferente dos `Node`s, os `Resource`s não fazem parte da árvore de cenas e não possuem uma representação visual ou física direta. Eles são usados para armazenar dados, configurações e até mesmo lógica de comportamento de forma modular e reutilizável.

#### 2.3.2. Uso Comum (ROP - Programação Orientada a Resources)

*   **Dados de Itens/Habilidades:** Definir propriedades para itens de inventário, habilidades de personagens, etc.
*   **Configurações de Jogo:** Armazenar configurações de dificuldade, opções de áudio, etc.
*   **Comportamentos de IA:** Criar diferentes estratégias de IA como `Resource`s.
*   **Materiais e Shaders:** `Material` e `Shader` são exemplos de `Resource`s embutidos.
*   **`PackedScene`:** Cenas salvas são, na verdade, `PackedScene`s, que são um tipo de `Resource`.

#### 2.3.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `resource_path`: O caminho do arquivo do recurso.
    *   `resource_name`: O nome do recurso.
*   **Métodos:**
    *   `duplicate(subresources: bool = false)`: Cria uma cópia do recurso.
    *   `setup_local_to_scene()`: Configura o recurso para ser local à cena.
    *   `take_over_path(path: String)`: Assume a propriedade de um caminho de arquivo.

#### 2.3.4. Exemplos de Código

```gdscript
# item_data.gd (Resource customizado)
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

# Em outro script (ex: player.gd)
extends CharacterBody2D

@export var equipped_item: ItemData

func _ready():
    if equipped_item:
        print("Item equipado: ", equipped_item.item_name)

func _input(event):
    if event.is_action_pressed("use_item") and equipped_item:
        equipped_item.use(self)
```

#### 2.3.5. Dicas e Boas Práticas

*   **ROP:** Adote a Programação Orientada a Resources para criar sistemas modulares e configuráveis.
*   **`duplicate()`:** Ao usar um `Resource` que será modificado em tempo de execução (ex: um item que tem sua durabilidade reduzida), sempre duplique-o (`.duplicate()`) para evitar modificar o `Resource` original salvo em disco.
*   **`@export`:** Use `@export` para expor propriedades do seu `Resource` no Inspector, permitindo que designers configurem os dados facilmente.

### 2.4. `Object`

O `Object` é a classe base mais fundamental de toda a Godot Engine. Quase tudo na Godot, incluindo `Node`s e `Resource`s, herda de `Object`. Ele fornece funcionalidades básicas como gerenciamento de propriedades, sinais, grupos e metadados.

#### 2.4.1. Descrição

`Object` é a classe raiz de todos os tipos de dados que podem ser inspecionados, serializados e que participam do sistema de sinais e slots da Godot. Ele não possui funcionalidades visuais ou de cena, mas estabelece a base para a maioria das interações e estruturas de dados no motor.

#### 2.4.2. Uso Comum

*   **Base para Classes Customizadas:** Ao criar classes GDScript que não precisam ser nós ou recursos, mas se beneficiam do sistema de propriedades e sinais da Godot, você pode estender `Object`.
*   **Gerenciamento de Sinais:** Todos os objetos podem emitir e conectar sinais.
*   **Grupos:** Objetos podem ser adicionados a grupos para gerenciamento e acesso em massa.

#### 2.4.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `script`: O script anexado ao objeto.
*   **Métodos:**
    *   `add_to_group(group: String)`: Adiciona o objeto a um grupo.
    *   `remove_from_group(group: String)`: Remove o objeto de um grupo.
    *   `is_in_group(group: String)`: Verifica se o objeto está em um grupo.
    *   `set_meta(name: String, value: Variant)`: Define um metadado para o objeto.
    *   `get_meta(name: String, default: Variant = null)`: Obtém um metadado.
    *   `has_meta(name: String)`: Verifica se o objeto tem um metadado.
    *   `connect(signal: String, callable: Callable)`: Conecta um sinal.
    *   `emit_signal(signal: String, ...)`: Emite um sinal.
    *   `call(method: String, ...)`: Chama um método por nome.

#### 2.4.4. Exemplos de Código

```gdscript
# Exemplo: Usando metadados e grupos
extends Node

class_name MyCustomObject

var value: int = 0

func _init(initial_value: int = 0):
    value = initial_value
    add_to_group("my_objects")
    set_meta("creation_time", Time.get_unix_time_from_system())

func _ready():
    var obj = MyCustomObject.new(10)
    obj.add_to_group("special_objects")
    print("Objeto no grupo 'my_objects': ", obj.is_in_group("my_objects"))
    print("Tempo de criação: ", obj.get_meta("creation_time"))

    # Acessando todos os objetos em um grupo
    for node in get_tree().get_nodes_in_group("my_objects"):
        if node is MyCustomObject:
            print("Objeto customizado no grupo: ", node.value)
```

#### 2.4.5. Dicas e Boas Práticas

*   **Base Universal:** Lembre-se de que a maioria das classes que você usa herda de `Object`, então as funcionalidades básicas como sinais e grupos estão amplamente disponíveis.
*   **Metadados:** Use metadados para armazenar informações adicionais em objetos sem a necessidade de criar novas propriedades no script.

### 2.5. `PackedScene`

A classe `PackedScene` é um tipo de `Resource` que representa uma cena salva no disco (arquivos `.tscn` ou `.scn`). Ela permite que você carregue e instancie cenas dinamicamente em tempo de execução, o que é fundamental para criar jogos modulares e eficientes.

#### 2.5.1. Descrição

Uma `PackedScene` é essencialmente um "modelo" de uma cena. Ela contém a estrutura de nós, suas propriedades e scripts anexados, mas não é uma instância ativa na árvore de cenas. Para usar uma `PackedScene`, você precisa instanciá-la.

#### 2.5.2. Uso Comum

*   **Criação de Inimigos/Projéteis:** Instanciar múltiplos inimigos ou projéteis a partir de uma única cena base.
*   **Carregamento de Níveis:** Carregar diferentes níveis do jogo como cenas separadas.
*   **Elementos de UI Reutilizáveis:** Criar componentes de UI (ex: barras de vida, botões) como cenas e instanciá-los onde for necessário.

#### 2.5.3. Propriedades e Métodos Chave

*   **Métodos:**
    *   `instantiate()`: Cria uma nova instância da cena empacotada. Retorna o nó raiz da nova instância.
    *   `can_instantiate()`: Verifica se a cena pode ser instanciada.

#### 2.5.4. Exemplos de Código

```gdscript
# Exemplo: Instanciando um inimigo
extends Node2D

const ENEMY_SCENE: PackedScene = preload("res://scenes/enemy.tscn") # Carrega a cena uma vez

func _ready():
    # Instancia um novo inimigo
    var new_enemy = ENEMY_SCENE.instantiate() as CharacterBody2D
    if new_enemy:
        new_enemy.position = Vector2(randf_range(100, 500), randf_range(100, 300))
        add_child(new_enemy)
        print("Inimigo instanciado: ", new_enemy.name)

# Exemplo: Carregamento dinâmico (se a cena não for pré-carregada)
func load_level(level_path: String):
    var level_scene = load(level_path) as PackedScene
    if level_scene:
        var new_level_instance = level_scene.instantiate()
        get_tree().root.add_child(new_level_instance)
        get_tree().current_scene.queue_free() # Remove a cena anterior
```

#### 2.5.5. Dicas e Boas Práticas

*   **`preload` vs `load`:** Use `preload()` para cenas que são sempre necessárias e `load()` para cenas que são carregadas sob demanda (ex: níveis diferentes), para otimizar o tempo de inicialização.
*   **`instantiate()`:** Lembre-se de que `instantiate()` retorna uma nova instância da cena. Você precisa adicioná-la à árvore de cenas com `add_child()` para que ela se torne ativa.
*   **Tipagem:** Use `as Type` ao instanciar para garantir a tipagem correta e aproveitar o autocompletar e a verificação de erros.

## 3. Tipos Essenciais de Nós (Base)

Esta seção aborda as classes base mais importantes que servem como fundamentos para a criação de elementos visuais e interativos em 2D e 3D, bem como interfaces de usuário.

### 3.1. `CanvasItem`

`CanvasItem` é a classe base para todos os nós 2D que podem ser desenhados na tela. Se um nó precisa ter uma representação visual em 2D, ele provavelmente herda de `CanvasItem`.

#### 3.1.1. Descrição

`CanvasItem` fornece as funcionalidades básicas para renderização 2D, como transformação (posição, rotação, escala), visibilidade, cores, e a capacidade de desenhar formas e texturas. Ele é a base para nós como `Node2D` e `Control`.

#### 3.1.2. Uso Comum

*   **Desenho Personalizado:** Sobrescrever o método `_draw()` para desenhar formas, linhas, polígonos ou texturas personalizadas.
*   **Efeitos Visuais:** Controlar a visibilidade, opacidade e transformação de elementos 2D.
*   **Base para Nós Visuais:** Serve como a base para `Sprite2D`, `TextureRect`, `Label`, etc.

#### 3.1.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `visible`: Se o item é visível.
    *   `modulate`: Cor de modulação (multiplica a cor do item).
    *   `self_modulate`: Cor de modulação que afeta apenas o próprio item, não os filhos.
    *   `material`: Material customizado para renderização.
    *   `light_mask`: Máscara de luz para interação com `Light2D`.
    *   `z_index`: Ordem de desenho (maior valor desenha por cima).
*   **Métodos:**
    *   `update()`: Força o redesenho do item (chama `_draw()`).
    *   `draw_line(...)`, `draw_rect(...)`, `draw_texture(...)`, etc.: Métodos para desenho dentro de `_draw()`.
    *   `set_as_top_level(enable: bool)`: Faz com que o item não seja afetado pela transformação do pai.

#### 3.1.4. Exemplos de Código

```gdscript
# Exemplo: Desenho personalizado de um círculo
extends Node2D

func _draw():
    # Desenha um círculo vermelho no centro do nó
    draw_circle(Vector2.ZERO, 20, Color.RED)

func _ready():
    # Força o redesenho para que o círculo apareça
    update()
```

#### 3.1.5. Dicas e Boas Práticas

*   **`_draw()`:** Use `_draw()` para lógica de desenho. Chame `update()` sempre que precisar redesenhar o item.
*   **Performance:** Evite chamar `update()` a cada frame se o desenho não mudar. Desenhos complexos em `_draw()` podem impactar a performance.
*   **`z_index`:** Use `z_index` para controlar a ordem de sobreposição de elementos 2D.

### 3.2. `Node2D`

`Node2D` é a classe base para todos os nós 2D que possuem uma posição, rotação e escala no espaço 2D. Ele herda de `CanvasItem` e adiciona as funcionalidades de transformação.

#### 3.2.1. Descrição

Um `Node2D` representa um objeto no espaço 2D com sua própria transformação local. Ele pode ser movido, girado e escalado independentemente de seu pai, e essas transformações são aplicadas a seus filhos.

#### 3.2.2. Uso Comum

*   **Personagens e Inimigos:** Base para `CharacterBody2D`, `RigidBody2D`, `Sprite2D`.
*   **Elementos de Cena:** Posicionar objetos como plataformas, obstáculos, itens coletáveis.
*   **Agrupamento de Elementos 2D:** Agrupar vários `Node2D`s para movê-los ou transformá-los juntos.

#### 3.2.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `position`: Posição local do nó (Vector2).
    *   `rotation`: Rotação local do nó (em radianos).
    *   `rotation_degrees`: Rotação local do nó (em graus).
    *   `scale`: Escala local do nó (Vector2).
    *   `global_position`: Posição global do nó.
    *   `global_rotation`: Rotação global do nó.
    *   `global_scale`: Escala global do nó.
    *   `transform`: A transformação completa (posição, rotação, escala) do nó.
*   **Métodos:**
    *   `move_local_x(delta: float)`, `move_local_y(delta: float)`: Move o nó em seu eixo local.
    *   `look_at(point: Vector2)`: Gira o nó para olhar para um ponto.
    *   `to_global(local_point: Vector2)`: Converte uma coordenada local para global.
    *   `to_local(global_point: Vector2)`: Converte uma coordenada global para local.

#### 3.2.4. Exemplos de Código

```gdscript
# Exemplo: Movendo e girando um Node2D
extends Node2D

@export var speed: float = 100.0
@export var rotation_speed: float = 90.0 # Graus por segundo

func _process(delta: float):
    # Mover para a direita
    position.x += speed * delta

    # Girar
    rotation_degrees += rotation_speed * delta

    # Olhar para o mouse (exemplo)
    # look_at(get_global_mouse_position())
```

#### 3.2.5. Dicas e Boas Práticas

*   **Transformações Locais vs. Globais:** Entenda a diferença entre `position`/`rotation`/`scale` (locais, relativas ao pai) e `global_position`/`global_rotation`/`global_scale` (globais, relativas à viewport).
*   **`_process` para Movimento:** Use `_process` para movimentos baseados em frames e `_physics_process` para movimentos que interagem com o sistema de física.
*   **`look_at()`:** Útil para fazer um personagem ou objeto "olhar" para outro ponto ou alvo.

### 3.3. `Control`

`Control` é a classe base para todos os nós de interface do usuário (UI) na Godot. Ele herda de `CanvasItem` e adiciona funcionalidades específicas para layout, interação com o usuário e temas.

#### 3.3.1. Descrição

Um `Control` é um nó 2D que gerencia seu próprio layout, tamanho e posição dentro de seu pai `Control`. Ele é projetado para construir interfaces de usuário interativas, como botões, rótulos, barras de progresso e menus.

#### 3.3.2. Uso Comum

*   **Construção de UI:** Criar menus, HUDs, inventários, telas de opções.
*   **Interação do Usuário:** Lidar com cliques de mouse, eventos de teclado e foco.
*   **Layout Responsivo:** Utilizar contêineres (`HBoxContainer`, `VBoxContainer`, `GridContainer`) para criar layouts que se adaptam a diferentes tamanhos de tela.

#### 3.3.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `rect_position`: Posição do canto superior esquerdo do nó `Control`.
    *   `rect_size`: Tamanho do nó `Control`.
    *   `anchor_left`, `anchor_right`, `anchor_top`, `anchor_bottom`: Âncoras para posicionamento responsivo.
    *   `margin_left`, `margin_right`, `margin_top`, `margin_bottom`: Margens em relação às âncoras.
    *   `mouse_filter`: Como o nó `Control` interage com eventos do mouse.
    *   `focus_mode`: Como o nó pode receber foco.
    *   `theme`: O tema visual aplicado ao nó e seus filhos.
*   **Métodos:**
    *   `grab_focus()`: Dá o foco de entrada ao nó.
    *   `release_focus()`: Libera o foco de entrada.
    *   `get_minimum_size()`: Retorna o tamanho mínimo que o nó `Control` pode ter.
    *   `set_anchors_and_offsets_preset(preset: int)`: Define um preset de âncoras e offsets (ex: `PRESET_FULL_RECT`).
    *   `_gui_input(event: InputEvent)`: Callback para eventos de entrada GUI.

#### 3.3.4. Exemplos de Código

```gdscript
# Exemplo: Criando um botão e um rótulo
extends Control

func _ready():
    # Criar um Label
    var label = Label.new()
    label.text = "Pontuação: 0"
    label.set_anchors_and_offsets_preset(Control.PRESET_TOP_LEFT)
    label.set_position(Vector2(20, 20))
    add_child(label)

    # Criar um Button
    var button = Button.new()
    button.text = "Iniciar Jogo"
    button.set_anchors_and_offsets_preset(Control.PRESET_CENTER)
    button.set_position(Vector2(-50, 50)) # Ajuste manual para centralizar
    button.set_size(Vector2(100, 30))
    add_child(button)

    # Conectar o sinal 'pressed' do botão
    button.pressed.connect(_on_start_button_pressed)

func _on_start_button_pressed():
    print("Botão 'Iniciar Jogo' pressionado!")
    # get_tree().change_scene_to_file("res://scenes/game_level.tscn")
```

#### 3.3.5. Dicas e Boas Práticas

*   **Contêineres:** Use contêineres (como `HBoxContainer`, `VBoxContainer`, `GridContainer`) para gerenciar o layout de sua UI de forma responsiva.
*   **Âncoras e Margens:** Domine o sistema de âncoras e margens para criar UIs que se adaptam a diferentes resoluções.
*   **Temas:** Utilize o sistema de temas (`Theme`) para manter a consistência visual de sua UI.
*   **`_gui_input()`:** Use `_gui_input()` para lidar com eventos de entrada específicos da UI, como cliques e arrastos.

### 3.4. `Node3D`

`Node3D` é a classe base para todos os nós 3D que possuem uma posição, rotação e escala no espaço 3D. Ele é o equivalente 3D do `Node2D`.

#### 3.4.1. Descrição

Um `Node3D` representa um objeto no espaço 3D com sua própria transformação local. Ele pode ser movido, girado e escalado, e essas transformações são aplicadas a seus filhos, permitindo a construção de cenas 3D complexas.

#### 3.4.2. Uso Comum

*   **Objetos 3D:** Base para `MeshInstance3D`, `Camera3D`, `Light3D`, `CharacterBody3D`, `RigidBody3D`.
*   **Organização de Cenas 3D:** Agrupar elementos 3D para gerenciamento e transformação conjunta.
*   **Posicionamento:** Definir a posição de objetos no mundo 3D.

#### 3.4.3. Propriedades e Métodos Chave

*   **Propriedades:**
    *   `position`: Posição local do nó (Vector3).
    *   `rotation`: Rotação local do nó (Vector3, em radianos).
    *   `rotation_degrees`: Rotação local do nó (Vector3, em graus).
    *   `scale`: Escala local do nó (Vector3).
    *   `global_position`: Posição global do nó.
    *   `global_rotation`: Rotação global do nó.
    *   `global_scale`: Escala global do nó.
    *   `transform`: A transformação completa (posição, rotação, escala) do nó.
    *   `quaternion`: Rotação do nó como um quatérnio.
*   **Métodos:**
    *   `translate(offset: Vector3)`: Move o nó por um vetor de offset.
    *   `rotate_x(angle: float)`, `rotate_y(angle: float)`, `rotate_z(angle: float)`: Gira o nó em torno de seus eixos locais.
    *   `look_at(target: Vector3, up: Vector3 = Vector3.UP)`: Gira o nó para olhar para um ponto no espaço 3D.
    *   `to_global(local_point: Vector3)`: Converte uma coordenada local para global.
    *   `to_local(global_point: Vector3)`: Converte uma coordenada global para local.

#### 3.4.4. Exemplos de Código

```gdscript
# Exemplo: Movendo e girando um Node3D
extends Node3D

@export var speed: float = 5.0
@export var rotation_speed: float = 1.0 # Radianos por segundo

func _process(delta: float):
    # Mover para frente (no eixo Z local)
    translate(Vector3(0, 0, -speed * delta))

    # Girar em torno do eixo Y global
    rotate_y(rotation_speed * delta)

    # Olhar para um ponto (exemplo)
    # look_at(Vector3(0, 0, 0))
```

#### 3.4.5. Dicas e Boas Práticas

*   **Transformações 3D:** Entenda os conceitos de posição, rotação (Euler vs. Quatérnios) e escala em 3D.
*   **Eixos:** Lembre-se de que o eixo Y geralmente aponta para cima no Godot 3D.
*   **`look_at()`:** Muito útil para câmeras, inimigos ou qualquer objeto que precise "encarar" um alvo.

