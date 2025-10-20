# Escopo dos Projetos Práticos do Curso

Este documento detalha todos os projetos práticos e desafios que compõem a trilha de aprendizagem do curso "Café com Godot". Ele serve como o pilar para o design curricular: ao definir o escopo e os requisitos de cada projeto final, podemos derivar (fazer "back-propagate") o conteúdo teórico e prático necessário para os módulos que os antecedem.

Cada projeto é projetado para aplicar, reforçar e expandir os conceitos de arquitetura de software e design de jogos ensinados nos manuais técnicos.

---

## **Módulo 02: Projeto Guiado - O Laboratório de Mecânicas**

- **Tipo:** Projeto Guiado
- **Conceito:** Em vez de construir um jogo completo, este módulo foca na criação de uma "sandbox" ou "laboratório de testes". É um ambiente interativo onde cada aula adiciona um novo sistema de jogo modular. Esta abordagem espelha o processo de desenvolvimento profissional, onde sistemas são prototipados e testados de forma isolada.
- **Gênero e Perspectiva:** Ação Top-Down.
- **Sistemas Centrais a Serem Aplicados:**
  - **Arquitetura Fundamental:** Estrutura de Autoloads (`GameManager`, `SceneManager`, `AudioManager`), Arquitetura com `Resource` (`WeaponData`, `EnemyData`), Máquina de Estados (FSM) para inimigos, Sistema de Save/Load.
  - **Gameplay e Jogador:** Sistema de UI (HUD, Menus), Sistema de Combate (Hitbox/Hurtbox com `AttackData`), Feedback de Dano (`FloatingTextManager`), Sistema de Loot (`LootTable`), Sistema de Interação, Sistema de Diálogo (básico), Sistema de Missões (básico).
  - **Assets e Polimento:** "Juice" (Camera Shake, Partículas), Animação com `AnimationPlayer` e `AnimationTree`, Áudio Espacial (`AudioStreamPlayer2D`).
- **Foco de Aprendizagem:** Dominar a implementação da arquitetura de software principal do curso. Entender na prática como sistemas desacoplados (Player, Inimigo, UI, Loot) se comunicam através de Sinais e Autoloads. Construir uma base de código robusta e reutilizável para os desafios futuros.

---

## **Módulo 03: Desafio - Primeiro Jogo (Top-Down)**

- **Tipo:** Desafio
- **Conceito:** Aplicar os sistemas do Módulo 02 para construir um jogo pequeno, mas completo, escolhendo uma das quatro especializações. O aluno deve focar em polir um loop de gameplay específico.
- **Perspectiva:** Top-Down.

### **Opções de Projeto 1:**

1. **Sobrevivência na Arena ("Bullet Heaven")**
    - **Foco de Aprendizagem:** Gerenciamento de hordas, otimização de performance (muitos objetos), design de sistemas de power-ups e "game feel".
    - **Sistemas-Chave:** `LootSystem` (para XP e power-ups), FSM (para múltiplos inimigos simples), `Spawner` baseado em tempo, `ExperienceManager`.

2. **Explorador de Dungeon (Ação/Aventura)**
    - **Foco de Aprendizagem:** Level design, script de eventos, gerenciamento de estado do mundo e atmosfera.
    - **Sistemas-Chave:** `WorldStateManager` (flags para portas e puzzles), `InteractionSystem`, `TileMap` para level design, `DialogueSystem`.

3. **Invasão Tática (Ação Furtiva)**
    - **Foco de Aprendizagem:** Design de combate desafiador, IA reativa e polimento extremo do "game feel".
    - **Sistemas-Chave:** FSM avançada (estados de Alerta, Patrulha, Investigação), `CombatSystem` (alta letalidade), `Path2D` e `NavigationServer2D` para IA.

4. **Aventureiro de Plataforma (Ação/Plataforma 2D)**
    - **Foco de Aprendizagem:** Provar a modularidade da arquitetura, adaptando-a para uma nova perspectiva e conjunto de físicas.
    - **Sistemas-Chave:** Adaptação de todos os sistemas para um `CharacterBody2D` com gravidade, `TileMap` para design de níveis vertical, IA adaptada para plataformas.

---

## **Módulo 05: Projeto Guiado - Plataforma de Mineração (*Dome Keeper*-like)**

- **Tipo:** Projeto Guiado
- **Conceito:** Um jogo de plataforma onde o jogador defende uma base de ondas de inimigos na superfície enquanto minera recursos no subsolo para comprar upgrades. O ciclo de jogo é dividido entre defesa (ação) e mineração/progressão (gerenciamento).
- **Gênero e Perspectiva:** Ação / Gerenciamento, Side-scroller 2D.
- **Sistemas Centrais a Serem Aplicados:**
  - **Gameplay:** `TileMap` destrutível, Sistema de Ondas de Inimigos (`Spawner` avançado), `InventorySystem` (para recursos minerais), `ShopSystem` e `CurrencySystem` (para a tela de upgrades), `EquipmentSystem` (para os upgrades da base e do jogador).
  - **Progressão:** `Resource`-based upgrades, `ExperienceManager` (pode ser adaptado para a progração da base).
- **Foco de Aprendizagem:** Implementar mecânicas de jogo com ciclos de gameplay duplos. Gerenciar a economia do jogo e a progressão do jogador através de sistemas de gerenciamento de recursos e lojas.

---

## **Módulo 06: Desafio - Jogo de Plataforma com Sistemas de RPG**

- **Tipo:** Desafio
- **Conceito:** Combinar as mecânicas de plataforma do Módulo 05 com os sistemas de RPG e gerenciamento de dados mais complexos.
- **Perspectiva:** Variada (Side-scroller, Top-Down, Isométrica).

### **Opções de Projeto 2:**

1. **Plataforma de Precisão (*Celeste*-like)**
    - **Foco de Aprendizagem:** Físicas de personagem avançadas, level design desafiador.
    - **Sistemas-Chave:** FSM do jogador extremamente polida (dash, wall-jump, coyote time, jump buffering).

2. **Metroidvania Compacto**
    - **Foco de Aprendizagem:** Level design interconectado, exploração baseada em habilidades.
    - **Sistemas-Chave:** `InventorySystem` e `EquipmentSystem` como chaves para novas áreas, `WorldStateManager` para persistir o estado do mapa, `Map/Minimap System`.

3. **Simulador de Fazenda (Top-Down)**
    - **Foco de Aprendizagem:** Gerenciamento de sistemas complexos e interconectados.
    - **Sistemas-Chave:** `CraftingSystem`, `InventorySystem` completo (arrastar e soltar), ciclo dia/noite, `TimeManager`.

---

## **Módulo 08: Projeto Guiado - Ação Multiplayer (*Overwatch 2D*-like)**

- **Tipo:** Projeto Guiado
- **Conceito:** Um jogo de ação em equipe baseado em heróis, onde cada personagem tem habilidades únicas. O projeto será construído para funcionar tanto em multiplayer local (split-screen) quanto online.
- **Gênero e Perspectiva:** Ação Multiplayer, Side-scroller 2D.
- **Sistemas Centrais a Serem Aplicados:**
  - **Multiplayer:** `MultiplayerSpawner`, `MultiplayerSynchronizer`, anotação `@rpc` para chamadas de procedimento remoto, arquitetura cliente-servidor.
  - **Arquitetura:** Heróis definidos por `Resource`s, FSM para gerenciamento de habilidades (cooldowns, estados).
  - **Servidor:** Construção de um servidor de jogo dedicado (headless) e comunicação com o cliente Godot.
- **Foco de Aprendizagem:** Dominar la API de multiplayer de alto nível da Godot. Entender os conceitos de autoridade de servidor e sincronização de estado. Estruturar um jogo para multiplayer online.

---

## **Módulo 09: Desafio - Jogo de Ação Online**

- **Tipo:** Desafio
- **Conceito:** Aplicar o conhecimento de multiplayer online em um gênero de ação específico, com foco em otimização de rede e design de jogo para um ambiente online.
- **Perspectiva:** Variada.

### **Opções de Projeto:**

1. **Ação Frenética Cooperativa (*Contra*-like Co-op)**
    - **Foco de Aprendizagem:** Sincronização de inimigos e chefes de fase em um ambiente cooperativo.
    - **Sistemas-Chave:** `MultiplayerSynchronizer` para múltiplos inimigos, RPCs para eventos de chefe.

2. **Luta em Plataforma Online (*Smash Bros.*-like)**
    - **Foco de Aprendizagem:** Combate baseado em física e sincronização de estado de alta precisão.
    - **Sistemas-Chave:** Sincronização de `RigidBody2D` ou `CharacterBody2D` com física customizada, autoridade do servidor para knockback e dano.

---

## **Módulo 11: Projeto Guiado - Bots com IA para o Jogo Multiplayer**

- **Tipo:** Projeto Guiado
- **Conceito:** Implementar um pipeline de Inteligência Artificial profissional para criar bots que possam jogar o jogo multiplayer do Módulo 08. A IA será treinada externamente e executada com alta performance dentro do jogo.
- **Gênero e Perspectiva:** IA para Jogo de Ação, Side-scroller 2D.
- **Sistemas Centrais a Serem Aplicados:**
  - **Pipeline de IA:** Ambiente de treinamento em Python (usando bibliotecas como PyTorch/TensorFlow), exportação do modelo para o formato **ONNX**.
  - **Integração:** Criação de uma **GDExtension em C++** para carregar e executar o modelo ONNX dentro do Godot em tempo real.
  - **Backend:** Implementação de um Leaderboard online usando um serviço de backend (ex: Nakama) para comparar o desempenho de jogadores e bots.
- **Foco de Aprendizagem:** Entender um pipeline de IA híbrido (treinamento em Python, execução em C++). Aprender a integrar código de baixo nível com Godot usando GDExtension. Conectar o jogo a serviços de backend para funcionalidades online.

---

## **Módulo 12: Desafio - Jogo com IA e Multiplayer**

- **Tipo:** Desafio
- **Conceito:** Combinar as habilidades de multiplayer e IA em um projeto final complexo, explorando a interação entre jogadores humanos e agentes de IA avançados.
- **Perspectiva:** Variada.

### **Opções de Projeto 3:**

1. **Jogo Cooperativo com um Diretor de IA (ML)**
    - **Foco de Aprendizagem:** Criar uma IA que gerencia a experiência de jogo em vez de apenas controlar um personagem.
    - **Sistemas-Chave:** A IA (pipeline Python/C++) ajusta dinamicamente a dificuldade, spawns e eventos com base no desempenho dos jogadores.

2. **Simulação com Agentes Inteligentes**
    - **Foco de Aprendizagem:** Criar comportamento emergente a partir da interação de múltiplos agentes de IA.
    - **Sistemas-Chave:** Múltiplos agentes de IA (controlados pelo pipeline) interagem entre si e com o jogador em um ecossistema (formigueiro, cidade).
