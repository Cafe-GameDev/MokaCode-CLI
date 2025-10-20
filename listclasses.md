listclasses.md

# Classes Essenciais da Godot Engine para Desenvolvimento de Jogos

Esta é uma lista curada de classes e nós essenciais da Godot Engine, focada naquelas que são diretamente utilizadas no desenvolvimento de jogos e plugins.

## Fundamentos
*   `Object`
*   `RefCounted`
*   `Resource`
*   `Node`
*   `Node2D`
*   `Node3D`
*   `CanvasItem`
*   `Control`
*   `SceneTree`
*   `PackedScene`
*   `Variant`
*   `Callable`
*   `Signal`
*   `GDExtension`
*   `Shader`
*   `ShaderMaterial`
*   `ClassDB`

## Nós Visuais (2D)
*   `Sprite2D`
*   `AnimatedSprite2D`
*   `TextureRect`
*   `ColorRect`
*   `Line2D`
*   `Polygon2D`
*   `TileMap`
*   `CanvasLayer`
*   `CanvasModulate`
*   `ParallaxBackground`
*   `ParallaxLayer`
*   `Camera2D`
*   `Light2D`
*   `PointLight2D`
*   `DirectionalLight2D`
*   `LightOccluder2D`
*   `OccluderPolygon2D`
*   `VisibleOnScreenNotifier2D`
*   `MeshInstance2D`
*   `MultiMeshInstance2D`
*   `GPUParticles2D`
*   `CPUParticles2D`
*   `RemoteTransform2D`
*   `TouchScreenButton`

## Nós Visuais (3D)
*   `Node3D`
*   `MeshInstance3D`
*   `Sprite3D`
*   `AnimatedSprite3D`
*   `WorldEnvironment`
*   `Camera3D`
*   `Light3D`
*   `OmniLight3D`
*   `DirectionalLight3D`
*   `SpotLight3D`
*   `ReflectionProbe`
*   `FogVolume`
*   `Decal`
*   `VisibleOnScreenNotifier3D`
*   `GPUParticles3D`
*   `CPUParticles3D`
*   `MultiMeshInstance3D`
*   `CSGBox3D`
*   `CSGCylinder3D`
*   `CSGPolygon3D`
*   `CSGCombiner3D`
*   `CSGMesh3D`
*   `CSGPrimitive3D`
*   `CSGSphere3D`
*   `CSGTorus3D`
*   `GridMap`
*   `RootMotionView`
*   `SpringArm3D`
*   `RemoteTransform3D`

## Nós de Física e Colisão (2D)
*   `CollisionObject2D`
*   `Area2D`
*   `PhysicsBody2D`
*   `StaticBody2D`
*   `RigidBody2D`
*   `CharacterBody2D`
*   `AnimatableBody2D`
*   `CollisionShape2D`
*   `CollisionPolygon2D`
*   `RayCast2D`
*   `ShapeCast2D`
*   `Joint2D`
*   `PinJoint2D`
*   `GrooveJoint2D`
*   `DampedSpringJoint2D`

## Nós de Física e Colisão (3D)
*   `CollisionObject3D`
*   `Area3D`
*   `PhysicsBody3D`
*   `StaticBody3D`
*   `RigidBody3D`
*   `CharacterBody3D`
*   `AnimatableBody3D`
*   `VehicleBody3D`
*   `VehicleWheel3D`
*   `SoftBody3D`
*   `PhysicalBone3D`
*   `CollisionShape3D`
*   `CollisionPolygon3D`
*   `RayCast3D`
*   `ShapeCast3D`
*   `Joint3D`
*   `PinJoint3D`
*   `HingeJoint3D`
*   `SliderJoint3D`
*   `ConeTwistJoint3D`
*   `Generic6DOFJoint3D`

## Nós de UI (Control)
*   `Control`
*   `Label`
*   `RichTextLabel`
*   `Panel`
*   `Button`
*   `BaseButton`
*   `CheckBox`
*   `CheckButton`
*   `MenuButton`
*   `OptionButton`
*   `TextureButton`
*   `LinkButton`
*   `LineEdit`
*   `TextEdit`
*   `ProgressBar`
*   `TextureProgressBar`
*   `HBoxContainer`
*   `VBoxContainer`
*   `GridContainer`
*   `MarginContainer`
*   `ScrollContainer`
*   `PanelContainer`
*   `AspectRatioContainer`
*   `CenterContainer`
*   `FlowContainer`
*   `HFlowContainer`
*   `VFlowContainer`
*   `TabContainer`
*   `Tabs`
*   `SplitContainer`
*   `HSplitContainer`
*   `VSplitContainer`
*   `GraphEdit`
*   `GraphNode`
*   `Tree`
*   `TreeItem`
*   `ItemList`
*   `Range`
*   `ScrollBar`
*   `HScrollBar`
*   `VSScrollBar`
*   `Slider`
*   `HSlider`
*   `VSlider`
*   `SpinBox`
*   `ColorPicker`
*   `ColorPickerButton`
*   `ColorRect`
*   `TextureRect`
*   `ReferenceRect`
*   `Separator`
*   `HSeparator`
*   `VSeparator`
*   `Window`
*   `Popup`
*   `PopupMenu`
*   `PopupPanel`
*   `AcceptDialog`
*   `ConfirmationDialog`
*   `FileDialog`
*   `VideoStreamPlayer`
*   `SubViewportContainer`

## Nós de Animação
*   `AnimationPlayer`
*   `AnimationTree`
*   `AnimationMixer`
*   `AnimatedTexture`
*   `Skeleton2D`
*   `Skeleton3D`
*   `Bone2D`
*   `Bone3D`
*   `SkeletonIK3D`
*   `Tween`
*   `Tweeners` (e.g., `PropertyTweener`, `IntervalTweener`, `CallbackTweener`, `MethodTweener`)

## Nós de Áudio
*   `AudioStreamPlayer`
*   `AudioStreamPlayer2D`
*   `AudioStreamPlayer3D`
*   `AudioStreamMicrophone`
*   `AudioStreamGenerator`
*   `AudioStreamGeneratorPlayback`

## Nós Miscelâneos
*   `Timer`
*   `Path2D`
*   `PathFollow2D`
*   `Path3D`
*   `PathFollow3D`
*   `NavigationRegion2D`
*   `NavigationRegion3D`
*   `NavigationAgent2D`
*   `NavigationAgent3D`
*   `NavigationLink2D`
*   `NavigationLink3D`
*   `NavigationObstacle2D`
*   `NavigationObstacle3D`
*   `Viewport`
*   `SubViewport`
*   `RandomNumberGenerator`
*   `ButtonGroup`

## Classes de Singleton (AutoLoads Globais)
*   `OS`
*   `Engine`
*   `ProjectSettings`
*   `Input`
*   `InputMap`
*   `TranslationServer`
*   `Time`
*   `Performance`
*   `EngineDebugger`

## Classes de Acesso e Manipulação de Dados
*   `FileAccess`
*   `DirAccess`
*   `ResourceLoader`
*   `ResourceSaver`
*   `ConfigFile`
*   `JSON`
*   `JSONParser`
*   `XMLParser`
*   `HashingContext`
*   `Crypto`
*   `X509Certificate`
*   `CryptoKey`
*   `HMACContext`

## Classes de Rede
*   `HTTPClient`
*   `HTTPRequest`
*   `TCPServer`
*   `StreamPeerTCP`
*   `UDPServer`
*   `PacketPeerUDP`
*   `WebRTCConnection`
*   `WebRTCMultiplayerPeer`
*   `WebSocketClient`
*   `WebSocketPeer`
*   `WebSocketServer`
*   `MultiplayerAPI`
*   `MultiplayerPeer`
*   `ENetConnection`
*   `ENetMultiplayerPeer`

## Classes de Threading
*   `Mutex`
*   `Semaphore`
*   `Thread`
*   `WorkerThreadPool`

## Classes de Scripting
*   `Script`
*   `GDScript`
*   `CSharpScript`

## Classes de GDExtension
*   `GDExtension`
*   (Nota: A classe `ClassDB` é fundamental para registrar classes C++ e está listada em Conceitos Fundamentais)

## Classes de Shader e Materiais
*   `Shader`
*   `ShaderMaterial`
*   `VisualShader`
*   `VisualShaderNode`
*   `VisualShaderNodeInput`
*   `VisualShaderNodeOutput`
*   `VisualShaderNodeTexture`
*   `VisualShaderNodeVectorOp`
*   `VisualShaderNodeFloatOp`
*   `VisualShaderNodeColorOp`
*   `VisualShaderNodeBooleanOp`
*   `VisualShaderNodeIntOp`
*   `VisualShaderNodeTransformOp`
*   `VisualShaderNodeScalarFunc`
*   `VisualShaderNodeVectorFunc`
*   `VisualShaderNodeColorFunc`
*   `VisualShaderNodeTransformFunc`
*   `VisualShaderNodeScalarConstant`
*   `VisualShaderNodeVectorConstant`
*   `VisualShaderNodeColorConstant`
*   `VisualShaderNodeBooleanConstant`
*   `VisualShaderNodeIntConstant`
*   `VisualShaderNodeTransformConstant`
*   `VisualShaderNodeGlobalExpression`
*   `VisualShaderNodeExpression`
*   `VisualShaderNodeCustom`
*   `VisualShaderNodeGroup`
*   `VisualShaderNodePort`
*   `VisualShaderNodeUniform`
*   `VisualShaderNodeTextureParameter`

## Classes de Eventos de Entrada (InputEvent)
*   `InputEvent`
*   `InputEventWithModifiers`
*   `InputEventKey`
*   `InputEventMouseButton`
*   `InputEventMouseMotion`
*   `InputEventJoypadButton`
*   `InputEventJoypadMotion`
*   `InputEventScreenTouch`
*   `InputEventScreenDrag`
*   `InputEventGesture`
*   `InputEventMagnify`
*   `InputEventPan`
*   `InputEventMIDI`
*   `InputEventAction`

## Classes de UI (Tema e Estilo)
*   `Theme`
*   `StyleBox`
*   `StyleBoxFlat`
*   `StyleBoxTexture`
*   `StyleBoxLine`
*   `StyleBoxEmpty`

## Editor Only
*   `EditorPlugin`
*   `EditorInterface`
*   `EditorFileSystem`
*   `EditorResourcePreview`
*   `EditorSettings`
*   `EditorSelection`
*   `EditorUndoRedoManager`
*   `EditorScript`
*   `EditorUtilityPlugin`
*   `EditorFileDialog`
*   `EditorInspector`
*   `EditorInspectorPlugin`
*   `EditorProperty`
*   `EditorPropertyPlugin`
*   `EditorResourcePicker`
*   `EditorScenePostImport`
*   `EditorSceneFormatImporter`
*   `EditorExportPlugin`
*   `EditorExportPlatform`
*   `EditorExportPreset`
*   `EditorFeatureProfile`
*   `EditorFileSystemDirectory`
*   `EditorImportPlugin`
*   `EditorNode`
*   `EditorPaths`
*   `EditorResourceConversionPlugin`
*   `EditorResourcePreviewGenerator`
*   `EditorResourceTooltipPlugin`
*   `EditorSpinSlider`
*   `EditorVCSInterface`
*   `EditorViewport`
*   `EditorDebuggerPlugin`
*   `EditorScenePostImportPlugin`
*   `EditorTranslationParserPlugin`
*   `EditorFileSystemImportFormat`
