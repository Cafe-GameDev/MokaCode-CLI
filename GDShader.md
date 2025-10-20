GDShader.md

# GDShader para Efeitos Visuais na Godot Engine

Este documento aborda o uso do GDShader para criar efeitos visuais otimizados e personalizados no desenvolvimento de plugins para a Godot Engine. O GDShader é a linguagem de shader nativa da Godot, permitindo um controle granular sobre a renderização de materiais e objetos, essencial para alcançar a fidelidade visual desejada em jogos modernos.

## 1. O que é GDShader?

GDShader é uma linguagem de sombreamento (shader language) inspirada em GLSL (OpenGL Shading Language), mas adaptada para o ecossistema da Godot Engine. Ele permite que você escreva código que é executado diretamente na GPU, possibilitando a criação de efeitos visuais complexos, otimização de renderização e manipulação de pixels e vértices em tempo real. Ao contrário do GDScript, que roda na CPU, o GDShader aproveita o paralelismo massivo da GPU para processar milhões de pixels e vértices simultaneamente, tornando-o ideal para tarefas gráficas intensivas.

## 2. Tipos de Shaders e Estrutura Básica

No Godot, você pode criar diferentes tipos de shaders com GDShader, cada um com um propósito específico e um conjunto de variáveis e funções embutidas:

*   **`shader_type spatial;` (3D):** Usado para renderizar objetos 3D, manipulando vértices, normais, cores, texturas e iluminação no espaço 3D. É o tipo mais comum para materiais de objetos 3D.
*   **`shader_type canvas_item;` (2D):** Usado para renderizar objetos 2D, como sprites, UI e elementos de interface, manipulando pixels no espaço 2D. Ideal para efeitos em UI ou sprites.
*   **`shader_type particles;`:** Usado para controlar o comportamento e a renderização de sistemas de partículas, permitindo efeitos visuais dinâmicos e complexos.
*   **`shader_type sky;`:** Usado para criar céus procedurais e ambientes de fundo dinâmicos.

### Estrutura Básica de um Shader

Um shader GDShader é dividido em funções principais que são executadas em diferentes estágios do pipeline de renderização:

*   **`vertex()`:** Executada para cada vértice do objeto. Usada para manipular a posição, normais, UVs, cores por vértice, etc. É onde as transformações de modelo e projeção ocorrem.
*   **`fragment()`:** Executada para cada pixel (ou fragmento) do objeto. Usada para calcular a cor final do pixel, aplicar texturas, iluminação, reflexos, refrações, etc. É a parte mais computacionalmente intensiva do shader.
*   **`light()`:** (Apenas para `spatial` e `canvas_item`) Executada para cada fonte de luz que afeta o objeto. Usada para calcular como a luz interage com o material, aplicando modelos de iluminação (Phong, PBR).

```gdshader
shader_type spatial; // Ou canvas_item, particles, sky

// Uniforms são variáveis que podem ser modificadas do GDScript ou do editor
uniform vec4 albedo_color : source_color = vec4(1.0);
uniform sampler2D albedo_texture : source_color;
uniform float metallic : hint_range(0.0, 1.0) = 0.0;
uniform float roughness : hint_range(0.0, 1.0) = 1.0;

void vertex() {
    // Lógica do vértice: manipulação de posição, UVs, etc.
    // Exemplo: mover vértices com base no tempo
    VERTEX.y += sin(TIME + VERTEX.x * 0.5) * 0.1;
}

void fragment() {
    // Lógica do fragmento: cálculo da cor final do pixel
    vec4 albedo_tex = texture(albedo_texture, UV);
    ALBEDO = albedo_color.rgb * albedo_tex.rgb;
    METALLIC = metallic;
    ROUGHNESS = roughness;
    // Exemplo: adicionar um brilho simples
    EMISSION = ALBEDO * 0.1; 
}

void light() {
    // Lógica da luz: como a luz interage com o material
    // Para shaders spatial, LIGHT_COLOR, LIGHT_DIRECTION, etc. estão disponíveis
    // Para canvas_item, LIGHT_COLOR, LIGHT_POSITION, etc.
}
```

## 3. Integração com Materiais e Uniforms

Shaders GDShader são aplicados a objetos através de `Material`s. Você pode criar um `ShaderMaterial` e atribuir seu shader a ele. Isso permite que você use o mesmo shader com diferentes parâmetros (uniforms) em vários materiais, tornando-os altamente reutilizáveis.

*   **Uniforms:** São variáveis declaradas no shader que podem ser modificadas externamente (do editor ou via GDScript/C++). Eles permitem personalizar o comportamento do shader sem reescrevê-lo.
    *   `uniform vec4 color;`
    *   `uniform sampler2D texture_albedo;`
    *   `uniform float time;`
*   **Hints:** Podem ser adicionados a uniforms para fornecer dicas ao editor Godot sobre como exibir e manipular a variável (ex: `hint_range(0.0, 1.0)`, `source_color`).

## 4. Tutoriais Completos e Efeitos Complexos (Descritivo)

### 4.1. Shader de Água Simples

*   **Conceito:** Criar um efeito de água com ondulações e uma cor translúcida.
*   **Implementação:**
    *   No `vertex()`: Adicionar um deslocamento vertical aos vértices baseado em `sin(TIME)` para criar ondulações.
    *   No `fragment()`: Usar uma cor base para a água, adicionar transparência (`ALPHA`), e talvez um pouco de reflexão (`ROUGHNESS`, `METALLIC`).
    *   **Uniforms:** `water_color`, `wave_speed`, `wave_strength`.

### 4.2. Efeito de Cel Shading (Toon Shader)

*   **Conceito:** Renderizar objetos com um estilo de desenho animado, usando cores chapadas e contornos pretos.
*   **Implementação:**
    *   No `fragment()`: Calcular a iluminação de forma não-linear, quantizando os valores de luz para um número limitado de cores. Por exemplo, se a luz for > 0.8, cor clara; se > 0.4, cor média; senão, cor escura.
    *   **Contornos:** Pode ser feito com uma segunda passagem de renderização (renderizando o objeto ligeiramente maior e preto por trás) ou com técnicas de pós-processamento.
    *   **Uniforms:** `toon_colors` (array de cores), `light_thresholds`.

### 4.3. Efeitos de Pós-Processamento (Bloom, Blur)

*   **Conceito:** Aplicar efeitos à imagem renderizada final, não a objetos individuais.
*   **Implementação:** Geralmente feito com `canvas_item` shaders aplicados a um `ViewportTexture` ou a um `TextureRect` que cobre a tela inteira.
    *   **Bloom:** Identificar áreas brilhantes da imagem, desfocá-las e adicioná-las de volta à imagem original.
    *   **Blur:** Amostrar pixels vizinhos e calcular uma média ponderada para suavizar a imagem.
    *   **Uniforms:** `screen_texture`, `blur_strength`, `bloom_threshold`.

### 4.4. Shader de Distorção (Warp Effect)

*   **Conceito:** Distorcer a imagem renderizada, simulando calor, água ou campos de força.
*   **Implementação:**
    *   No `fragment()`: Modificar as coordenadas `UV` usadas para amostrar a `screen_texture` com base em uma função de tempo ou ruído. `UV += sin(TIME * speed) * strength;`
    *   **Uniforms:** `distortion_strength`, `distortion_speed`.

## 5. Integração com C++ e GDScript: Modificando Uniforms em Tempo Real

A capacidade de modificar uniforms de shaders via GDScript ou C++ em tempo de execução é poderosa, permitindo efeitos dinâmicos e interativos.

### 5.1. Via GDScript

```gdscript
# script_do_objeto.gd
extends Sprite2D

@export var distortion_strength: float = 0.05

func _process(delta: float):
    if material:
        material.set_shader_parameter("distortion_strength", distortion_strength * sin(Time.get_ticks_msec() / 1000.0))
```

### 5.2. Via C++ (GDExtension)

```cpp
// my_shader_controller.h
#pragma once
#include <godot_cpp/classes/node.hpp>
#include <godot_cpp/classes/shader_material.hpp>

namespace godot {
class MyShaderController : public Node {
    GDCLASS(MyShaderController, Node)
private:
    Ref<ShaderMaterial> _target_material;
    double _distortion_strength;
protected:
    static void _bind_methods();
public:
    void set_target_material(const Ref<ShaderMaterial>& p_material);
    Ref<ShaderMaterial> get_target_material() const;
    void set_distortion_strength(double p_strength);
    double get_distortion_strength() const;
    void _process(double delta) override;
};
}

// my_shader_controller.cpp (trecho)
#include "my_shader_controller.h"
#include <godot_cpp/core/class_db.hpp>
#include <godot_cpp/classes/time.hpp>

namespace godot {
void MyShaderController::_bind_methods() {
    ClassDB::bind_method(D_METHOD("set_target_material", "material"), &MyShaderController::set_target_material);
    ClassDB::bind_method(D_METHOD("get_target_material"), &MyShaderController::get_target_material);
    ADD_PROPERTY(PropertyInfo(Variant::OBJECT, "target_material", PROPERTY_HINT_RESOURCE_TYPE, "ShaderMaterial"), "set_target_material", "get_target_material");

    ClassDB::bind_method(D_METHOD("set_distortion_strength", "strength"), &MyShaderController::set_distortion_strength);
    ClassDB::bind_method(D_METHOD("get_distortion_strength"), &MyShaderController::get_distortion_strength);
    ADD_PROPERTY(PropertyInfo(Variant::FLOAT, "distortion_strength"), "set_distortion_strength", "get_distortion_strength");
}

void MyShaderController::_process(double delta) {
    if (_target_material.is_valid()) {
        double time_val = Time::get_singleton()->get_ticks_msec() / 1000.0;
        _target_material->set_shader_parameter("distortion_strength", _distortion_strength * Math::sin(time_val));
    }
}
// ... (construtor, destrutor, getters/setters)
}
```

## 6. Checklist de Otimização para GDShader

Otimizar shaders é crucial para manter uma boa taxa de quadros. Aqui está um checklist:

*   **Minimize Cálculos Complexos:** Evite cálculos desnecessários ou complexos dentro do shader, especialmente na função `fragment()`, que é executada para cada pixel. Cada operação conta.
*   **Use `hint_range`:** Para uniforms, use `hint_range` para limitar os valores e otimizar o desempenho. Isso pode ajudar o driver da GPU a fazer otimizações.
*   **Evite `if`s e `for`s (Branching):** Condicionais e loops podem ser caros na GPU, pois podem forçar a execução de ambos os ramos em diferentes threads. Tente usar funções matemáticas (ex: `mix`, `step`, `smoothstep`) ou técnicas de branchless programming quando possível.
*   **Otimize Acesso a Texturas:** Minimize o número de amostragens de textura (`texture()`) e use texturas com formatos otimizados (ex: comprimidas, com mipmaps). Amostragens de textura são operações caras.
*   **Utilize `render_mode`:** Use `render_mode` para otimizar o comportamento do shader (ex: `unshaded` para shaders que não precisam de iluminação, `skip_vertex_transform` se você manipular `VERTEX` diretamente).
*   **Precisão:** Use `highp`, `mediump` ou `lowp` para variáveis float onde a precisão total não é necessária. `lowp` é o mais rápido, mas com menor precisão.
*   **Batching:** Para `canvas_item` shaders, o Godot tenta fazer batching de draw calls. Shaders complexos ou que modificam muito o estado de renderização podem quebrar o batching, impactando a performance.
*   **Evite `discard`:** A função `discard` (que descarta o pixel atual) pode ser cara, pois impede otimizações de early-Z. Use-a com moderação.
*   **Compreenda o Pipeline:** Entenda como o pipeline de renderização funciona para saber onde suas otimizações terão o maior impacto (vertex vs. fragment).

Ao dominar o GDShader, você pode elevar significativamente a qualidade visual dos seus projetos Godot e plugins, criando efeitos impressionantes e performáticos.

## 7. Licença

Este documento e o projeto ao qual ele se refere estão licenciados sob a Licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.

Copyright (c) 2025 MokaCode by Machi
