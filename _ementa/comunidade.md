# Guia de Recursos Comunitários para Godot

Este documento é uma lista curada de plugins, templates, assets e extensões de alta qualidade para o Godot Engine, com o objetivo de acelerar o desenvolvimento e adicionar funcionalidades poderosas aos seus projetos.

## Plugins e Extensões Essenciais

Plugins que estendem o editor ou o motor com novas funcionalidades.

### Interface e Diálogo

-   **Dialogic:** Um sistema de diálogo completo e rico em recursos, com um editor visual de linhas do tempo, variáveis, condições e integração com GDScript. Essencial para jogos com narrativa.
    -   **Link:** [https://github.com/coppolaemilio/dialogic](https://github.com/coppolaemilio/dialogic)

### Ferramentas de Desenvolvimento

-   **Godot Git Plugin:** Integra o controle de versão Git diretamente no editor do Godot, permitindo visualizar diffs, fazer stage, commit e push sem sair do motor.
    -   **Link:** [https://github.com/godotengine/godot-git-plugin](https://github.com/godotengine/godot-git-plugin)
-   **GUT (Godot Unit Test):** A ferramenta padrão da comunidade para testes unitários em GDScript. Permite criar, rodar e depurar testes para garantir a estabilidade do código.
    -   **Link:** [https://github.com/bitwes/Gut](https://github.com/bitwes/Gut)
-   **TODO Manager:** Encontra comentários com palavras-chave (TODO, FIXME, BUG) no seu código e os organiza em uma lista dentro do editor, ajudando a rastrear tarefas pendentes.
    -   **Link:** [https://github.com/n-p-day/godot-todo-manager](https://github.com/n-p-day/godot-todo-manager)

### Gráficos e Animação

-   **Aseprite Wizard:** Automatiza a importação de arquivos `.aseprite`, criando `SpriteFrames` e `AnimationPlayer` com todas as animações, tags e durações de frames configuradas corretamente.
    -   **Link:** [https://github.com/viniciusgerevini/godot-aseprite-wizard](https://github.com/viniciusgerevini/godot-aseprite-wizard)
-   **Phantom Camera:** Inspirado no Cinemachine do Unity, este plugin oferece ferramentas avançadas para criar comportamentos de câmera 2D e 3D complexos e cinematográficos.
    -   **Link:** [https://github.com/ramokz/phantom-camera-for-godot](https://github.com/ramokz/phantom-camera-for-godot)
-   **SmartShape2D:** Uma ferramenta poderosa para criar terrenos 2D e outras formas texturizadas de maneira intuitiva e flexível.
    -   **Link:** [https://github.com/SirRamEsq/SmartShape2D](https://github.com/SirRamEsq/SmartShape2D)

### 3D e Terrenos

-   **Terrain3D:** Uma extensão GDExtension de alta performance para criar e editar terrenos 3D, com suporte a sculpting, pintura de texturas e vegetação.
    -   **Link:** [https://github.com/TokisanGames/Terrain3D](https://github.com/TokisanGames/Terrain3D)
-   **ProtonScatter:** Uma ferramenta para popular cenas 3D com assets de forma procedural, ideal para criar florestas, campos e ambientes detalhados.
    -   **Link:** [https://github.com/protongraph/protontools](https://github.com/protongraph/protontools)

### Físicas e IA

-   **Godot Jolt:** Substitui o motor de física 3D padrão do Godot pelo Jolt Physics, oferecendo maior performance e estabilidade para simulações complexas.
    -   **Link:** [https://github.com/godot-jolt/godot-jolt](https://github.com/godot-jolt/godot-jolt)
-   **LimboAI / Beehave:** Duas excelentes opções para criar IAs baseadas em Árvores de Comportamento (Behavior Trees) com editores visuais.
    -   **LimboAI:** [https://github.com/limbonaut/limboai](https://github.com/limbonaut/limboai)
    -   **Beehave:** [https://github.com/bitbrain/beehave](https://github.com/bitbrain/beehave)

### Integração de Rede

-   **GodotSteam:** A implementação GDExtension mais popular para integrar a API da Steamworks, permitindo o uso de conquistas, leaderboards, multiplayer, etc.
    -   **Link:** [https://github.com/GodotSteam/GodotSteam](https://github.com/GodotSteam/GodotSteam)

## Templates de Projetos

Projetos pré-configurados que servem como um ponto de partida para gêneros específicos.

-   **Godot FPS Template:** Um template robusto para jogos de tiro em primeira pessoa.
    -   **Link:** [https://github.com/jasonswearingen/godot-fps-template](https://github.com/jasonswearingen/godot-fps-template)
-   **Godot Third Person Controller:** Um template para jogos de ação e aventura em terceira pessoa.
    -   **Link:** [https://github.com/J-F-Evans/Godot-Third-Person-Controller](https://github.com/J-F-Evans/Godot-Third-Person-Controller)
-   **Godot Platformer Template:** Um ponto de partida para jogos de plataforma 2D com mecânicas comuns já implementadas.
    -   **Link:** [https://github.com/T-T-R/Godot-Platformer-Template](https://github.com/T-T-R/Godot-Platformer-Template)

## Recursos de Assets

Coleções de assets de arte e áudio de alta qualidade, muitos deles gratuitos e com licenças permissivas.

### Arte 2D e 3D

-   **Kenney.nl:** Conhecido como "Asset Jesus", Kenney oferece uma vasta coleção de assets 2D e 3D de alta qualidade e de domínio público (CC0), perfeitos para prototipagem e jogos completos.
    -   **Link:** [https://www.kenney.nl/assets](https://www.kenney.nl/assets)
-   **KayKit:** Coleções de assets 3D low-poly e vibrantes, ideais para jogos com um estilo mais cartunesco.
    -   **Link:** [https://kaylousberg.com/game-assets](https://kaylousberg.com/game-assets)
-   **OpenGameArt.org:** Uma enorme biblioteca de assets 2D e 3D, sons e músicas com licenças variadas (geralmente Creative Commons).
    -   **Link:** [https://opengameart.org/](https://opengameart.org/)
-   **itch.io:** A seção de assets do itch.io é um tesouro de recursos de arte 2D e 3D, com muitos pacotes gratuitos e pagos de artistas independentes.
    -   **Link:** [https://itch.io/game-assets/free](https://itch.io/game-assets/free)

### Áudio

-   **Sonniss GDC Audio Bundles:** A cada ano, a Sonniss lança um pacote massivo de efeitos sonoros de alta qualidade (muitos gigabytes) de estúdios profissionais, totalmente gratuitos e com licença permissiva.
    -   **Link:** [https://sonniss.com/gameaudiogdc](https://sonniss.com/gameaudiogdc)
-   **Freesound.org:** Uma biblioteca colaborativa de sons com licenças Creative Commons. Ótima para encontrar efeitos sonoros específicos.
    -   **Link:** [https://freesound.org/](https://freesound.org/)
