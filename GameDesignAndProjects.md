GameDesignAndProjects.md

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

# Gêneros de Jogos

Este documento descreve diferentes gêneros de jogos, organizados pela dimensão (2D/3D) e pela perspectiva da câmera, que é um elemento de design fundamental, mas não um gênero em si.

---

## Tópico: Jogos 2D

Jogos que operam em um plano bidimensional (eixos X e Y).

### Subtópico: Perspectiva Top-Down

A câmera é posicionada acima do mundo do jogo. Facilita a visão estratégica e a navegação.

#### Gêneros Comuns:
1.  **RPG (Role-Playing Game):** Foco em narrativa e evolução de personagens. Ex: *Chrono Trigger*.
2.  **Ação-Aventura:** Foco em exploração, combate e puzzles. Ex: *The Legend of Zelda: A Link to the Past*.
3.  **Shooter (Shoot 'em up / Shmup):** O objetivo é atirar em hordas de inimigos, geralmente com a tela em movimento. Ex: *Ikaruga*.
4.  **Twin-Stick Shooter:** O jogador controla o movimento com um analógico e a mira com outro. Ex: *Enter the Gungeon*.
5.  **Estratégia:** Gerenciamento de recursos e unidades. Ex: *Warcraft II*.
6.  **Simulação:** Gerenciamento de fazendas, colônias, etc. Ex: *Stardew Valley*.
7.  **Roguelike/Roguelite:** Morte permanente, níveis gerados proceduralmente e progressão entre as partidas. Ex: *Hades*, *The Binding of Isaac*.
8.  **Bullet Hell:** Subgênero de shooter com foco em desviar de uma quantidade esmagadora de projéteis inimigos. Ex: *Touhou Project*.
9.  **Tower Defense:** O jogador constrói torres para defender um caminho de ondas de inimigos. Ex: *Kingdom Rush*.
10. **Grand Strategy (2D):** Estratégia em larga escala com foco em gestão de impérios e diplomacia em um mapa 2D. Ex: *Crusader Kings II*.
11. **Tycoon (2D):** Jogos de gerenciamento e construção de negócios em perspectiva 2D. Ex: *Theme Hospital*.

### Subtópico: Perspectiva de Plataforma e Lateral

A câmera tem uma visão lateral (side-scrolling), e o gameplay é centrado em pular, lutar e navegar por obstáculos.

#### Gêneros Comuns:
1.  **Ação-Plataforma:** Combina saltos com combate intenso. Ex: *Mega Man X*.
2.  **Puzzle-Plataforma:** Foco em resolver quebra-cabeças com as mecânicas de pulo. Ex: *Celeste*, *Braid*.
3.  **Metroidvania:** Ação-aventura com um grande mapa interconectado explorado com novas habilidades. Ex: *Hollow Knight*.
4.  **Runner/Auto-Runner:** O personagem corre automaticamente, exigindo reações rápidas do jogador. Ex: *Geometry Dash*.
5.  **Beat 'em up:** Foco em combate corpo a corpo contra múltiplos inimigos em fases lineares. Ex: *Streets of Rage 4*.
6.  **Fighting Game (Jogo de Luta):** Combate um-contra-um focado em combos e técnicas. Ex: *Street Fighter 6*, *Mortal Kombat 1*.
7.  **Precision Platformer:** Plataforma com foco em saltos extremamente precisos e desafios de habilidade. Ex: *Super Meat Boy*.
8.  **Run and Gun:** Combina elementos de plataforma com tiro intenso. Ex: *Cuphead*.
9.  **Rhythm Platformer:** Plataforma onde as ações são sincronizadas com o ritmo da música. Ex: *Geometry Dash*.

### Subtópico: Perspectiva Fixa / Mista

A câmera é estática ou muda entre telas. Comum em gêneros que não dependem de scrolling contínuo.

#### Gêneros Comuns:
1.  **Point-and-Click Adventure:** Foco em narrativa e resolução de puzzles através da interação com o cenário. Ex: *The Secret of Monkey Island*.
2.  **Visual Novel:** Narrativa interativa com foco principal no texto e em escolhas do jogador. Ex: *Phoenix Wright: Ace Attorney*.
3.  **Card Game / Deck-Builder:** Jogo de cartas estratégico. Ex: *Slay the Spire*.
4.  **Hidden Object:** O jogador procura por itens específicos em cenas estáticas e detalhadas. Ex: *Mystery Case Files*.
5.  **Interactive Fiction:** Jogos baseados em texto onde o jogador interage digitando comandos. Ex: *Zork*.
6.  **Board Game Adaptation:** Adaptações digitais de jogos de tabuleiro. Ex: *Ticket to Ride*.

---

## Tópico: Jogos 3D

Jogos que operam em um espaço tridimensional (eixos X, Y e Z).

### Subtópico: Perspectiva em Primeira Pessoa

A visão é a partir dos olhos do personagem, promovendo alta imersão.

#### Gêneros Comuns:
1.  **FPS (First-Person Shooter):** Foco em combate com armas de fogo. Ex: *DOOM*, *Counter-Strike*.
2.  **Immersive Sim:** Grande liberdade para resolver problemas com sistemas interativos. Ex: *Deus Ex*, *BioShock*.
3.  **Aventura / Puzzle:** Foco em exploração e resolução de quebra-cabeças. Ex: *Portal 2*.
4.  **Terror (Survival Horror):** A perspectiva limitada aumenta a tensão. Ex: *Resident Evil 7*.
5.  **Walking Simulator:** Foco na narrativa e exploração, com pouca interação mecânica. Ex: *What Remains of Edith Finch*.
6.  **Looter Shooter:** Combina tiro em primeira pessoa com elementos de RPG, como coleta de loot e progressão de personagem. Ex: *Borderlands*.
7.  **Arena Shooter:** Foco em combate rápido e frenético em arenas fechadas. Ex: *Quake III Arena*.
8.  **Tactical Shooter:** Simulações de combate realistas com foco em estratégia e trabalho em equipe. Ex: *Rainbow Six Siege*.
9.  **Survival (First-Person):** Foco em sobrevivência em ambientes hostis, com coleta de recursos e construção. Ex: *Rust*.
10.  **Hero Shooter:** Combate baseado em equipes com personagens que possuem habilidades únicas. Ex: *Overwatch*.

### Subtópico: Perspectiva em Terceira Pessoa

A câmera segue o personagem, permitindo visão do personagem e do ambiente.

#### Gêneros Comuns:
1.  **Ação-Aventura:** O gênero mais comum, com exploração, combate e narrativa. Ex: *The Last of Us*.
2.  **RPG de Mundo Aberto:** Foco na exploração de vastos mundos e progressão. Ex: *The Witcher 3*, *Elden Ring*.
3.  **Plataforma 3D:** Desafios de pulo em ambiente tridimensional. Ex: *Super Mario Odyssey*.
4.  **Stealth (Furtividade):** O objetivo é evitar a detecção. Ex: *Metal Gear Solid V*.
5.  **Soulslike:** Subgênero de RPG de ação com alta dificuldade, combate metódico e narrativa ambiental. Ex: *Dark Souls*, *Bloodborne*.
6.  **Character Action / Spectacle Fighter:** Combate estiloso e exagerado focado em combos complexos. Ex: *Devil May Cry 5*.
7.  **Battle Royale:** Grande número de jogadores lutando para ser o último sobrevivente em um mapa que encolhe. Ex: *Fortnite*, *PUBG*.
8.  **Cover-Based Shooter:** Tiro em terceira pessoa com foco em usar cobertura para se proteger de ataques inimigos. Ex: *Gears of War*.
9. **Hack and Slash (3D):** Combate corpo a corpo rápido contra múltiplos inimigos, com foco em combos e habilidades. Ex: *God of War*.

### Subtópico: Perspectiva Isométrica / Top-Down 3D

A câmera tem uma visão angular e distante, oferecendo uma visão tática.

#### Gêneros Comuns:
1.  **ARPG (Action RPG) / Hack and Slash:** Combate rápido contra hordas e coleta de loot. Ex: *Diablo IV*.
2.  **CRPG (Computer RPG):** RPGs complexos, com muito texto, escolhas e sistemas. Ex: *Baldur's Gate 3*.
3.  **RTS (Real-Time Strategy):** Gerenciamento de base e exércitos em tempo real. Ex: *StarCraft II*.
4.  **MOBA (Multiplayer Online Battle Arena):** Batalhas de equipe 5v5 em um mapa definido. Ex: *League of Legends*.
5.  **Simulação / Gerenciamento:** Construção de cidades, parques, etc. Ex: *Cities: Skylines*.
6.  **Tactical RPG:** RPGs com combate baseado em turnos em um grid tático. Ex: *Final Fantasy Tactics*.
7.  **Dungeon Crawler (Isométrico):** Exploração de masmorras com foco em combate e coleta de tesouros. Ex: *Pillars of Eternity*.
8.  **City Builder:** Construção e gerenciamento de cidades. Ex: *SimCity*.
9.  **Grand Strategy (3D):** Estratégia em larga escala com foco em gestão de impérios e diplomacia em um mapa 3D. Ex: *Europa Universalis IV*.

---

## Tópico: Gêneros Transversais e Temáticos (Incluindo NSFW)

Gêneros que podem existir em qualquer perspectiva, definidos mais pela sua mecânica central ou tema.

### Subtópico: Simulação
1.  **Simulação de Veículos:** Foco no realismo de pilotar carros, aviões, etc. Ex: *Microsoft Flight Simulator*.
2.  **Simulação de Vida / Social:** Gerenciar a vida de personagens virtuais. Ex: *The Sims 4*.
3.  **Tycoon / Gerenciamento:** Construir e gerenciar um negócio. Ex: *RollerCoaster Tycoon*.

### Subtópico: Sandbox e Mundo Aberto
1.  **Sandbox Criativo:** Ferramentas para o jogador criar sua própria diversão. Ex: *Minecraft*, *Garry's Mod*.
2.  **Ação-Aventura de Crime em Mundo Aberto:** Exploração livre de uma cidade moderna com atividades criminosas. Ex: ***Grand Theft Auto V***, *Saints Row*.

### Subtópico: Conteúdo Adulto (NSFW)
Jogos que contêm elementos gráficos ou temáticos considerados maduros ou explícitos, geralmente restritos a um público adulto. A classificação "NSFW" (Not Safe For Work) indica que o conteúdo pode não ser apropriado para todos os ambientes ou idades.

#### Gêneros Comuns:
1.  **Violência Extrema / Gore:** Jogos que se destacam pelo alto nível de representação gráfica de violência, desmembramentos, sangue e ferimentos. O foco é frequentemente no impacto visual e na visceralidade do combate. A mecânica pode variar amplamente, abrangendo desde shooters a jogos de luta. Ex: ***Mortal Kombat 1*** (luta com fatalidades gráficas), *Postal 2* (shooter com liberdade para violência gratuita), *Hatred* (shooter isométrico com foco em violência).
2.  **Conteúdo Sexual Explícito (Eroge / Hentai / Adult Visual Novel - AVN):** Jogos cujo principal apelo e foco narrativo ou mecânico envolvem representações detalhadas de atos sexuais, nudez ou temas eróticos. Frequentemente encontrados nos formatos de Visual Novel ou Dating Sim, mas podem incorporar elementos de outros gêneros como RPG, puzzle ou simulação. Ex: *Doki Doki Literature Club!* (com elementos de terror psicológico e temas maduros), *Katawa Shoujo* (visual novel com foco em romance e deficiências físicas).
3.  **Dating Sim (Adulto) / Romance Explícito:** Subgênero de simulação de encontros onde o objetivo é construir relacionamentos românticos e/ou sexuais com personagens, culminando em cenas explícitas.
4.  **Temas Maduros / Conteúdo Perturbador:** Jogos que abordam temas sensíveis como abuso, trauma, doenças mentais, uso de drogas, ou que apresentam narrativas sombrias e psicologicamente perturbadoras, mesmo sem violência gráfica ou conteúdo sexual explícito. O impacto reside na profundidade e na seriedade dos temas explorados. Ex: *Detroit: Become Human* (aborda temas de discriminação e liberdade), *This War of Mine* (simulação de sobrevivência em guerra com foco nas dificuldades civis).
