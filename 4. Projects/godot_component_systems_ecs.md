
# GODOT 4.x – 2D COMPONENT ARCHITECTURE MASTER MANUAL

### Production-Level System Design for Small → Medium Indie Games

---

# TABLE OF CONTENTS

1. Engine Execution Model
    
2. Responsibility Layering
    
3. Scene Composition Philosophy
    
4. Physics Architecture
    
5. Movement System Design
    
6. Combat System Architecture
    
7. Hitbox / Hurtbox Deep Dive
    
8. State Machine Architecture
    
9. AI Behavior Structuring
    
10. Animation System Integration
    
11. Signal Topology Design
    
12. Collision Layer Matrix Strategy
    
13. Data & Resource Architecture
    
14. Global Systems & Autoload Design
    
15. Projectile Systems
    
16. Interaction & UI Boundaries
    
17. Save/Load Architecture
    
18. Performance & Scaling Discipline
    
19. Folder Structure Blueprint
    
20. Production Architecture Checklist
    

This will be Part 1 (Sections 1–7).  
Say **“continue”** when ready for Part 2.

---

# 1. ENGINE EXECUTION MODEL

If you do not understand this, your architecture will collapse later.

## Scene Tree Reality

Godot is not entity-based.  
It is **hierarchical tree-based execution**.

Every node:

- Has exactly one parent
    
- Can have many children
    
- Inherits transforms
    
- Inherits pause state
    
- Is freed recursively
    

### Lifecycle Order

When a scene is instantiated:

1. `_enter_tree()` — top to bottom
    
2. `_ready()` — bottom to top
    
3. `_process(delta)` — every frame (if enabled)
    
4. `_physics_process(delta)` — fixed timestep
    

Key implication:

Parents can safely access children in `_ready()`  
Children should not assume parent initialization unless guaranteed.

---

## Transform Propagation

Child global position = parent global position + local offset

Therefore:

- Movement root must be the physics body.
    
- Visual nodes must be children.
    
- Combat zones must be children of the entity.
    

Hierarchy = behavior.

---

## Deletion Model

If you call:

```gdscript
queue_free()
```

On a parent, every component dies.

Therefore:

Never store external hard references to child nodes without checking validity.

---

# 2. RESPONSIBILITY LAYERING

A scalable game separates concerns into layers.

An entity should conceptually contain:

### Physical Layer

Movement, collision resolution.

### Detection Layer

Overlap-only trigger zones.

### Combat Layer

Damage logic, hit resolution.

### AI Layer

Decision-making state transitions.

### Rendering Layer

Animation and visuals.

### Feedback Layer

Particles, flash, sound triggers.

### Data Layer

Stats, configuration, tuning.

### Persistence Layer

Save/Load logic.

### Global Layer

GameManager, AudioManager, InputManager.

If two layers merge into one script, complexity explodes later.

---

# 3. SCENE COMPOSITION PHILOSOPHY

Godot scales through composition, not deep inheritance.

Bad:

Player.gd with 1500 lines controlling:

- Movement
    
- Animation
    
- Combat
    
- UI
    
- Audio
    
- Save
    
- AI
    

Good:

Player (CharacterBody2D)

- MovementComponent
    
- JumpComponent
    
- DashComponent
    
- HealthComponent
    
- HurtboxComponent
    
- StateMachineComponent
    
- AnimationComponent
    
- AttackComponent
    
- InventoryComponent
    

Each does one thing.

---

## Composition Rules

1. Components inherit from `Node` unless spatial.
    
2. Spatial logic uses `Node2D`, `Area2D`, or Body nodes.
    
3. Collision shapes belong to scene structure, not scripts.
    
4. Components emit signals upward.
    
5. Parent coordinates behavior.
    

---

# 4. PHYSICS ARCHITECTURE

## CharacterBody2D

This is your movement authority.

Responsibilities:

- Calls `move_and_slide()`
    
- Stores velocity
    
- Resolves collisions
    
- Tracks floor state
    

Must not:

- Apply damage
    
- Manage UI
    
- Control animation logic directly
    

---

## CollisionShape2D

Defines geometry.

Rules:

- Exactly one primary body shape per physical entity.
    
- Additional shapes only for specialized cases (ladders, sensors).
    
- Never create shapes in `_ready()` unless procedural.
    

---

## StaticBody2D

Used for:

- Walls
    
- Floors
    
- Obstacles
    

Should never contain gameplay logic.

---

## RigidBody2D

Used for:

- Physics crates
    
- Debris
    
- Dynamic objects
    

Avoid mixing manual control with rigid bodies.

---

# 5. MOVEMENT SYSTEM DESIGN

Movement should be modular.

## MovementComponent (Node)

Responsibilities:

- Read input
    
- Compute target velocity
    
- Apply acceleration curves
    
- Apply friction
    

Should not:

- Own collision shapes
    
- Call `move_and_slide()` directly
    
- Play animations
    

Instead:

- Emits signal `velocity_changed(new_velocity)`
    
- Parent applies movement
    

---

## JumpComponent

Handles:

- Jump force
    
- Coyote time
    
- Jump buffering
    

Coyote time = allow jump shortly after leaving ground.  
Jump buffering = allow input slightly before landing.

These are movement layer enhancements.

---

## DashComponent

Handles:

- Temporary velocity override
    
- Invulnerability frames (optional)
    
- Cooldown timers
    

Must:

- Disable itself cleanly
    
- Not permanently modify base velocity logic
    

---

# 6. COMBAT SYSTEM ARCHITECTURE

Combat is overlap-driven, not physics-driven.

Movement collision ≠ damage detection.

---

## HealthComponent (Node)

Pure logic.

Stores:

- max_health
    
- current_health
    

Emits:

- damage_taken(amount)
    
- died()
    

Should not:

- Know about hitboxes
    
- Query physics
    
- Access animation
    

---

## AttackComponent (Node)

Controls:

- Attack timing
    
- Cooldown
    
- Combo logic
    
- Spawning hitboxes
    

It does NOT own shapes.

It instantiates hitbox scenes.

---

# 7. HITBOX / HURTBOX DEEP DIVE

This is where many beginners destroy architecture.

## HurtboxComponent

Base node: `Area2D`

Purpose:

- Detect incoming hitboxes
    
- Forward damage to HealthComponent
    

Must:

- Be separate from body collision
    
- Have its own collision layer
    
- Not block movement
    

### Why not reuse body shape?

Because:

- Body collision resolves physics
    
- Hurtbox detects combat overlap
    
- Different collision masks required
    

---

## HitboxComponent

Base node: `Area2D`

Purpose:

- Detect hurtboxes
    
- Apply damage
    

Often:

- Spawned dynamically
    
- Temporary
    
- Destroyed after duration
    

---

## Boss Edge Case

Boss may contain:

- Head hurtbox (2x damage)
    
- Body hurtbox (1x damage)
    
- Shield hurtbox (0x damage)
    

This requires multiple Area2D nodes.

If hurtbox script hardcodes shape, flexibility is destroyed.

---

## Collision Matrix Example

|Layer|Collides With|
|---|---|
|Player Body|World, Enemy Body|
|Enemy Body|World, Player Body|
|Player Hitbox|Enemy Hurtbox|
|Enemy Hitbox|Player Hurtbox|
|Pickup|Player Body|

Never let hitboxes collide with world geometry unless intentional.

---

Good. Now we go deeper.

This will be dense.  
No filler.  
No artificial section padding.  
Pure architecture.

We continue and expand heavily.

---

# 8. STATE MACHINE ARCHITECTURE (PRODUCTION LEVEL)

A state machine is not “just switching animations”.

It is your **behavior control system**.

If designed badly:

- Combat becomes unmanageable.
    
- Movement becomes inconsistent.
    
- Bugs multiply.
    

---

## 8.1 What a State Machine Actually Is

A state machine enforces:

> At any time, the entity is in exactly one primary state.

Example states:

- Idle
    
- Move
    
- Jump
    
- Fall
    
- Dash
    
- Attack
    
- Hurt
    
- Dead
    

Without a state machine:

- Jump logic fights dash logic.
    
- Attack interrupts movement unpredictably.
    
- Animation desynchronizes from logic.
    

---

## 8.2 Proper Godot Structure

**Do NOT** put 300 if-statements in `_physics_process`.

Instead:

Player

- StateMachineComponent (Node)
    
    - IdleState (Node)
        
    - MoveState (Node)
        
    - JumpState (Node)
        
    - AttackState (Node)
        
    - HurtState (Node)
        

Each state:

- Has `enter()`
    
- Has `exit()`
    
- Has `update(delta)`
    
- Has `physics_update(delta)`
    

The StateMachine:

- Holds current_state
    
- Delegates calls
    
- Controls transitions
    

---

## 8.3 Transition Discipline

Transitions must be:

- Explicit
    
- Predictable
    
- Guarded
    

Bad:

State checks input and directly changes sibling component states.

Good:

State emits `request_transition("Attack")`  
StateMachine validates and switches.

---

## 8.4 Interrupt Rules

Define clearly:

- Can dash interrupt attack?
    
- Can hurt interrupt dash?
    
- Can death interrupt everything?
    

You must define priority hierarchy:

Dead > Hurt > Attack > Dash > Jump > Move > Idle

If you do not define priority, you will get race conditions.

---

## 8.5 Common Anti-Pattern

Bad:

MovementComponent sets animation.  
AttackComponent sets animation.  
StateMachine sets animation.

Now animation is controlled by three systems.

Correct:

StateMachine sets animation state.  
AnimationComponent reacts to state change.

One authority.

---

# 9. AI BEHAVIOR STRUCTURING

AI is just automated state transitions.

Do NOT separate AI system from StateMachine entirely.  
AI feeds transitions.

---

## 9.1 Basic Enemy Structure

Enemy (CharacterBody2D)

- MovementComponent
    
- HealthComponent
    
- HurtboxComponent
    
- DetectionComponent
    
- StateMachine
    
- AnimationComponent
    
- AttackComponent
    

DetectionComponent emits:

- player_detected
    
- player_lost
    

StateMachine reacts.

---

## 9.2 DetectionComponent (Area2D)

Responsibilities:

- Detect player proximity
    
- Maintain internal list of overlapping bodies
    
- Emit events
    

Must not:

- Directly modify enemy velocity
    
- Directly attack
    

---

## 9.3 Simple AI States

IdleState  
ChaseState  
AttackState  
ReturnState

ChaseState:

- Uses MovementComponent
    
- Moves toward player
    
- Transitions to Attack if within range
    

AttackState:

- Triggers AttackComponent
    
- Waits for cooldown
    
- Returns to Chase
    

---

## 9.4 Scaling AI

For roguelike enemies:

Add:

- WanderState
    
- FleeState
    
- StunnedState
    

Never embed decision logic directly into MovementComponent.

---

# 10. ANIMATION DECOUPLING

Animation must not drive logic.  
Logic drives animation.

---

## 10.1 AnimationComponent

Responsibilities:

- Play animations
    
- Flip sprite
    
- Emit animation_finished
    

Must not:

- Change states
    
- Detect damage
    
- Apply physics
    

---

## 10.2 State → Animation Mapping

StateMachine emits:

state_changed("Attack")

AnimationComponent listens:

play("attack")

---

## 10.3 Root Motion?

In 2D pixel games, usually avoid root motion.

Movement should be physics-driven.

Animation should follow movement, not control it.

---

# 11. SIGNAL TOPOLOGY DESIGN

Signals are powerful.  
Signals are dangerous.

---

## 11.1 Correct Signal Direction

Component → Parent

Never:

Sibling → Sibling direct calls.

---

## 11.2 Example Flow

Hitbox detects hurtbox  
Hurtbox emits `damage_received(damage)`  
Parent listens → calls HealthComponent.apply_damage()

HealthComponent emits `died()`  
Parent transitions state to Dead

Everything flows upward.

---

## 11.3 Event Bus (Autoload)

Use only for:

- Global pause
    
- Global damage events (rare)
    
- Scene transitions
    

Do NOT use event bus for basic combat.

---

# 12. DATA & RESOURCE ARCHITECTURE

Never hardcode values in scripts.

Use Resources.

---

## 12.1 StatsResource

Contains:

- max_health
    
- move_speed
    
- jump_force
    
- damage
    
- cooldown
    

Entity loads resource.

This allows:

- Easy balancing
    
- Enemy variants
    
- JSON loading
    
- Procedural generation
    

---

## 12.2 Why Resources Matter

Without resources:

- You duplicate numbers in scripts.
    
- Tuning becomes painful.
    
- Designers cannot adjust values easily.
    

---

# 13. PROJECTILE SYSTEM ARCHITECTURE

Projectiles must be self-contained.

Projectile Scene:

Projectile (Area2D or CharacterBody2D)

- CollisionShape2D
    
- HitboxComponent
    
- MovementComponent
    
- LifetimeTimer
    

---

## 13.1 Lifetime Discipline

Projectiles must:

- Self-destruct after time
    
- Disable collision after hit
    
- Avoid multiple damage triggers unless intentional
    

---

## 13.2 Pooling (Production)

Instead of instantiating 100 bullets per second:

Use object pool.

Deactivate:

- hide
    
- disable collision
    
- stop processing
    

Reuse later.

---

# 14. INTERACTION SYSTEM DESIGN

Interaction ≠ combat.

Use InteractableComponent (Area2D).

Detect player.

Show prompt via UIManager.

On input:

- Interactable emits activated
    
- Parent handles effect
    

Never let UI logic inside InteractableComponent.

---

# 15. SAVE/LOAD ARCHITECTURE

Saving must be centralized.

Do NOT let each component write files.

Pattern:

GameManager:

- Collects state from SaveComponents
    
- Serializes to JSON
    
- Writes to file
    

Load:

- Deserialize
    
- Inject values into components
    

---

# 16. PERFORMANCE DISCIPLINE

Performance problems come from:

- Too many nodes
    
- Too many signals
    
- Too many instantiations
    
- Unnecessary `_process()`
    

Rules:

- Disable processing if unused
    
- Use `_physics_process` only for physics
    
- Avoid logic in `_process` if possible
    
- Use groups for batch operations
    

---

# 17. FOLDER STRUCTURE BLUEPRINT

res://

- core/
    
- player/
    
- enemies/
    
- components/
    
- systems/
    
- ui/
    
- projectiles/
    
- data/
    
- scenes/
    

Components should be reusable across entities.

---

# 18. FULL PLAYER BLUEPRINT (REFERENCE)

Player (CharacterBody2D)

- CollisionShape2D
    
- MovementComponent
    
- JumpComponent
    
- DashComponent
    
- HealthComponent
    
- HurtboxComponent (Area2D)
    
    - CollisionShape2D
        
- AttackComponent
    
- StateMachine
    
- AnimationComponent
    
- InventoryComponent
    

This scales.

---

# 19. BOSS ARCHITECTURE

Boss (CharacterBody2D)

- CollisionShape2D
    
- Multiple Hurtboxes
    
- MovementComponent
    
- PatternController
    
- StateMachine
    
- AnimationComponent
    
- HealthComponent
    
- PhaseManager
    

PhaseManager triggers state transitions based on health percentage.

---

# 20. ROGUELIKE SCALING PATTERNS

Procedural enemies:

Use StatsResource variants.

Procedural rooms:

Scene instancing with random seeds.

Never hardcode enemy stats in scene.

---
# 21. PRODUCTION STATE MACHINE TEMPLATE

This is minimal but scalable.

## 21.1 Base State Class

Every state extends a base class.

State.gd:

```gdscript
extends Node
class_name State

var owner: Node
var state_machine: Node

func enter(previous_state: State) -> void:
	pass

func exit() -> void:
	pass

func update(delta: float) -> void:
	pass

func physics_update(delta: float) -> void:
	pass
```

No assumptions.  
No hard references.  
Pure interface.

---

## 21.2 StateMachineComponent

StateMachine.gd:

```gdscript
extends Node
class_name StateMachine

@export var initial_state: NodePath

var current_state: State

func _ready() -> void:
	for child in get_children():
		if child is State:
			child.owner = get_parent()
			child.state_machine = self
	
	current_state = get_node(initial_state)
	current_state.enter(null)

func transition_to(state_name: String) -> void:
	var new_state = get_node(state_name) as State
	if new_state == null:
		return
	
	if current_state:
		current_state.exit()
	
	var previous = current_state
	current_state = new_state
	current_state.enter(previous)

func _process(delta: float) -> void:
	if current_state:
		current_state.update(delta)

func _physics_process(delta: float) -> void:
	if current_state:
		current_state.physics_update(delta)
```

Notice:

- No movement logic here.
    
- No animation logic.
    
- No combat logic.
    
- Only delegation.
    

This scales infinitely.

---

# 22. MOVEMENT SYSTEM – CLEAN SEPARATION

## 22.1 MovementComponent

MovementComponent.gd:

```gdscript
extends Node
class_name MovementComponent

@export var max_speed: float = 200.0
@export var acceleration: float = 800.0
@export var friction: float = 900.0
@export var gravity: float = 900.0

var velocity: Vector2 = Vector2.ZERO

func apply_input(direction: float, delta: float) -> void:
	var target_speed = direction * max_speed
	velocity.x = move_toward(velocity.x, target_speed, acceleration * delta)

func apply_friction(delta: float) -> void:
	velocity.x = move_toward(velocity.x, 0, friction * delta)

func apply_gravity(delta: float) -> void:
	velocity.y += gravity * delta
```

This component does NOT move the body.

---

## 22.2 CharacterBody2D Integrates Movement

Player.gd (root body):

```gdscript
extends CharacterBody2D

@onready var movement = $MovementComponent

func _physics_process(delta: float) -> void:
	movement.apply_gravity(delta)
	
	var input_dir = Input.get_axis("move_left", "move_right")
	if input_dir != 0:
		movement.apply_input(input_dir, delta)
	else:
		movement.apply_friction(delta)
	
	velocity = movement.velocity
	move_and_slide()
	
	movement.velocity = velocity
```

Notice:

- MovementComponent calculates.
    
- Body executes physics.
    

Separation maintained.

---

# 23. HEALTH SYSTEM – SCALABLE

HealthComponent.gd:

```gdscript
extends Node
class_name HealthComponent

signal damaged(amount: int)
signal died()

@export var max_health: int = 100
var current_health: int

func _ready() -> void:
	current_health = max_health

func apply_damage(amount: int) -> void:
	current_health -= amount
	damaged.emit(amount)
	
	if current_health <= 0:
		died.emit()
```

No knowledge of hitboxes.  
No knowledge of animation.

---

# 24. HURTBOX IMPLEMENTATION (CORRECT)

HurtboxComponent.gd:

```gdscript
extends Area2D
class_name HurtboxComponent

signal hit_received(damage: int)

func _ready() -> void:
	area_entered.connect(_on_area_entered)

func _on_area_entered(area: Area2D) -> void:
	if area.has_method("get_damage"):
		var damage = area.get_damage()
		hit_received.emit(damage)
```

Important:

- No health logic here.
    
- No hardcoded shape.
    
- Shape defined in scene.
    

---

# 25. HITBOX IMPLEMENTATION

HitboxComponent.gd:

```gdscript
extends Area2D
class_name HitboxComponent

@export var damage: int = 10

func get_damage() -> int:
	return damage
```

Minimal.  
Clean.  
Reusable.

---

# 26. WIRING HURTBOX TO HEALTH

In Player.gd:

```gdscript
@onready var health = $HealthComponent
@onready var hurtbox = $HurtboxComponent

func _ready() -> void:
	hurtbox.hit_received.connect(_on_hit_received)
	health.died.connect(_on_died)

func _on_hit_received(damage: int) -> void:
	health.apply_damage(damage)

func _on_died() -> void:
	state_machine.transition_to("DeadState")
```

Notice flow:

Hitbox → Hurtbox → Player → Health → Player

Upward propagation.

---

# 27. PROJECTILE TEMPLATE

Projectile.gd:

```gdscript
extends Area2D

@export var speed: float = 400.0
@export var lifetime: float = 2.0
@onready var hitbox = $HitboxComponent

var direction: Vector2 = Vector2.RIGHT
var timer: float = 0.0

func _physics_process(delta: float) -> void:
	position += direction * speed * delta
	
	timer += delta
	if timer >= lifetime:
		queue_free()
```

Clean.  
Self-contained.

---

# 28. COLLISION LAYER DISCIPLINE (PRACTICAL)

Set:

Player Body:

- Layer: PlayerBody
    
- Mask: World, EnemyBody
    

Hurtbox:

- Layer: PlayerHurtbox
    
- Mask: EnemyHitbox
    

Hitbox:

- Layer: PlayerHitbox
    
- Mask: EnemyHurtbox
    

Never mix these.

If you mix them:

- Walls trigger damage.
    
- Projectiles hit unintended objects.
    
- Combat becomes chaotic.
    

---

# 29. FULL PLAYER SCENE STRUCTURE (FINAL)

Player (CharacterBody2D)

- CollisionShape2D
    
- MovementComponent
    
- JumpComponent
    
- DashComponent
    
- HealthComponent
    
- HurtboxComponent (Area2D)
    
    - CollisionShape2D
        
- StateMachine
    
    - IdleState
        
    - MoveState
        
    - JumpState
        
    - AttackState
        
    - HurtState
        
    - DeadState
        
- AnimationComponent
    
- AttackComponent
    

This is scalable to medium indie size.

---

# 30. COMBO ATTACK SYSTEM (SCALABLE)

Basic attacks are easy.  
Combos are where design explodes.

---

## 30.1 Problem

If AttackComponent directly chains animations based on input timing, logic becomes tangled.

Correct approach:

- AttackState controls combo progression.
    
- AttackComponent only executes attack logic.
    
- StateMachine controls timing windows.
    

---

## 30.2 Combo State Structure

AttackState must track:

- combo_index
    
- combo_timer
    
- combo_window_open
    

Example design:

AttackState.gd:

```gdscript
extends State

@export var combo_reset_time: float = 0.6

var combo_index: int = 0
var combo_timer: float = 0.0
var combo_window_open: bool = false

func enter(previous_state):
	combo_window_open = true
	combo_timer = 0.0
	owner.attack_component.execute_attack(combo_index)

func physics_update(delta):
	combo_timer += delta
	
	if combo_timer >= combo_reset_time:
		combo_index = 0
		state_machine.transition_to("IdleState")

func handle_attack_input():
	if combo_window_open:
		combo_index += 1
		state_machine.transition_to("AttackState")
```

Key idea:

State owns combo progression.  
AttackComponent only spawns hitboxes.

---

# 31. INVULNERABILITY FRAMES (I-FRAMES)

After taking damage, player should:

- Flash visually
    
- Ignore further damage
    
- Possibly disable hurtbox temporarily
    

---

## 31.1 Clean Implementation

Add to HealthComponent:

```gdscript
@export var invulnerability_time: float = 0.5
var invulnerable: bool = false
var invuln_timer: float = 0.0
```

Modify apply_damage:

```gdscript
func apply_damage(amount: int) -> void:
	if invulnerable:
		return
	
	current_health -= amount
	damaged.emit(amount)
	
	invulnerable = true
	invuln_timer = 0.0
	
	if current_health <= 0:
		died.emit()
```

Then update:

```gdscript
func _process(delta):
	if invulnerable:
		invuln_timer += delta
		if invuln_timer >= invulnerability_time:
			invulnerable = false
```

Important:

Do NOT disable CollisionShape unless necessary.  
Prefer logical invulnerability flag.

---

# 32. PROJECTILE POOLING (PRODUCTION READY)

Spawning and freeing 200 bullets per second causes GC pressure.

---

## 32.1 Pool Manager

ProjectilePool.gd:

```gdscript
extends Node
class_name ProjectilePool

@export var projectile_scene: PackedScene
@export var pool_size: int = 20

var pool: Array = []

func _ready():
	for i in pool_size:
		var projectile = projectile_scene.instantiate()
		projectile.visible = false
		projectile.set_physics_process(false)
		add_child(projectile)
		pool.append(projectile)

func get_projectile() -> Node:
	for projectile in pool:
		if not projectile.visible:
			projectile.visible = true
			projectile.set_physics_process(true)
			return projectile
	return null
```

Projectile must include reset() method.

This removes allocation spikes.

---

# 33. MULTI-PHASE BOSS ARCHITECTURE

Boss fights break architecture first.

---

## 33.1 Required Components

Boss:

- HealthComponent
    
- PhaseManager
    
- StateMachine
    
- Multiple Hurtboxes
    
- PatternController
    
- MovementComponent
    

---

## 33.2 PhaseManager

PhaseManager monitors health percentage.

```gdscript
extends Node

@onready var health = $"../HealthComponent"

func _ready():
	health.damaged.connect(_on_damaged)

func _on_damaged(amount):
	var ratio = float(health.current_health) / health.max_health
	
	if ratio < 0.5:
		get_parent().state_machine.transition_to("PhaseTwoState")
```

Important:

PhaseManager does NOT contain attack logic.

---

# 34. PLATFORMER EDGE CASES

Platformers are harder than top-down games.

---

## 34.1 Moving Platforms

Problem:

Player must inherit platform velocity.

Solution:

When colliding with platform:

```gdscript
if is_on_floor():
	var collider = get_last_slide_collision().get_collider()
	if collider.is_in_group("moving_platform"):
		velocity += collider.velocity
```

Platform must expose velocity.

---

## 34.2 Slopes

Use `floor_snap_length` in CharacterBody2D.  
Avoid manual vertical correction.

Never manually modify y position unless necessary.

---

## 34.3 Ladders

Use separate Area2D:

LadderZone (Area2D)

When inside:

- Disable gravity
    
- Allow vertical movement
    
- Ignore floor detection
    

This should be a separate LadderComponent.

---

# 35. ROGUELIKE PROCEDURAL ARCHITECTURE

Procedural systems must be data-driven.

---

## 35.1 Enemy Variants

Use StatsResource:

EnemyGoblin.tres  
EnemyGoblinElite.tres

Load resource into Enemy scene.

Do NOT duplicate scenes for stat variations.

---

## 35.2 Room Generation

RoomScene:

- SpawnPoints (Node2D markers)
    

DungeonManager:

- Instantiates room scenes
    
- Connects door positions
    
- Seeds RNG
    

Never let rooms manage global dungeon logic.

---

# 36. DEBUGGING DISCIPLINE (LARGE PROJECTS)

Use:

- Visible collision shapes
    
- Remote Scene Tree
    
- Node groups
    
- Print only when necessary
    
- Breakpoints in StateMachine
    

---

## 36.1 Signal Debugging Trick

Add logging in StateMachine:

```gdscript
print("Transition:", current_state.name, "->", new_state.name)
```

Log transitions early.  
Remove later.

---

# 37. ARCHITECTURE FAILURE PATTERNS

Common collapse points:

1. Player.gd exceeds 1000 lines
    
2. Animation drives logic
    
3. Hitboxes reuse body collision
    
4. Direct sibling node access
    
5. No collision layer documentation
    
6. No state machine priority rules
    
7. Too many autoload singletons
    
8. Hardcoded values everywhere
    

If you detect any of these early, refactor immediately.

---

# 38. MODULAR ABILITY SYSTEM (PLUG-IN DESIGN)

As your game grows, you cannot hardcode abilities into Player.

Dash, Fireball, Shield, Teleport — these must be modular.

---

## 38.1 Ability Architecture Goal

You want:

- Add/remove abilities without editing Player.gd
    
- Reuse abilities on enemies
    
- Control cooldown cleanly
    
- Allow stacking abilities (roguelike upgrades)
    

---

## 38.2 Ability Base Class

Ability.gd:

```gdscript
extends Node
class_name Ability

signal ability_used

@export var cooldown: float = 1.0
var cooldown_timer: float = 0.0
var ready: bool = true

func _process(delta):
	if not ready:
		cooldown_timer += delta
		if cooldown_timer >= cooldown:
			ready = true
			cooldown_timer = 0.0

func try_activate() -> void:
	if ready:
		activate()
		ready = false
		ability_used.emit()

func activate() -> void:
	pass
```

Abilities override `activate()`.

---

## 38.3 AbilityManager

AbilityManager.gd:

```gdscript
extends Node
class_name AbilityManager

var abilities: Dictionary = {}

func register_ability(name: String, ability: Ability):
	abilities[name] = ability

func activate(name: String):
	if abilities.has(name):
		abilities[name].try_activate()
```

Player only talks to AbilityManager.

Not individual abilities.

---

## 38.4 Why This Matters

Without this:

- Dash logic gets embedded in Player.
    
- Fireball logic modifies Player directly.
    
- Upgrades become impossible to scale.
    

With this:

- Abilities are plug-and-play.
    
- Roguelike modifiers become data-driven.
    

---

# 39. EVENT-DRIVEN UI ARCHITECTURE

UI must not query gameplay constantly.

Bad:

UI polls Player every frame for health.

Good:

HealthComponent emits signal.  
UI listens.

---

## 39.1 Health UI Flow

HealthComponent emits `damaged` and `died`.

UIManager connects once:

```gdscript
player.health.damaged.connect(_on_health_changed)
```

UI updates once per event.

No polling.

---

## 39.2 UI Boundaries

Gameplay should not:

- Reference UI nodes.
    
- Modify UI directly.
    

Instead:

Gameplay → emits event  
UI → reacts

---

# 40. PRODUCTION ANIMATION LAYERING

When animation complexity increases:

- Walking while shooting
    
- Hurt while attacking
    
- Casting spell while moving
    

You must separate layers.

---

## 40.1 Recommended Pattern

Use AnimationTree.

Separate blend spaces:

- Base locomotion
    
- Upper body attack
    
- Damage overlay
    

StateMachine drives animation parameters.

Never let animation change gameplay state automatically unless intentional.

---

# 41. LARGE-SCALE ENEMY COMPOSITION SYSTEM

In roguelike projects, enemies multiply fast.

You must avoid duplicating scenes.

---

## 41.1 Enemy Template Scene

EnemyBase.tscn

Contains:

- MovementComponent
    
- HealthComponent
    
- Hurtbox
    
- StateMachine
    
- AnimationComponent
    
- DetectionComponent
    
- AttackComponent
    

Stats loaded from Resource.

---

## 41.2 Variant Strategy

Create different `.tres` stat files.

Goblin.tres  
GoblinElite.tres  
GoblinMage.tres

Same scene.  
Different data.

Never duplicate the scene.

---

# 42. DEPENDENCY DIRECTION BLUEPRINT

Dependency must always flow inward.

Allowed:

Component → Parent  
State → StateMachine  
Parent → Component

Not allowed:

Component → Sibling  
Component → UI  
Component → Global Manager directly

This prevents circular logic.

---

# 43. MOBILE & WEB ARCHITECTURAL IMPACT

Mobile constraints:

- Lower CPU budget
    
- Limited draw calls
    
- Avoid heavy physics queries
    

Implications:

- Pool projectiles
    
- Disable processing when offscreen
    
- Reduce signal spam
    
- Use fewer nodes
    

Web constraints:

- Memory tighter
    
- Threading limited
    
- Long frame spikes noticeable
    

Architectural impact:

- Avoid dynamic allocation bursts
    
- Avoid excessive scene instancing
    
- Use object pools early
    

---

# 44. MULTIPLAYER-SAFE PREPARATION (FUTURE PROOFING)

Even if multiplayer is years away:

Design safely now.

---

## 44.1 Deterministic Logic

Do not rely on:

- Random() without seed
    
- Frame-dependent behavior
    

Encapsulate randomness via RNG class.

---

## 44.2 Authority Separation

Keep:

- Input layer
    
- Simulation layer
    

Separate.

Future multiplayer requires simulation authority separation.

If logic tightly couples to input nodes, conversion becomes painful.

---

# 45. PRODUCTION FOLDER STRUCTURE (FINAL FORM)

res://

- core/
    
    - state_machine/
        
    - ability/
        
    - components/
        
- entities/
    
    - player/
        
    - enemies/
        
    - bosses/
        
- projectiles/
    
- systems/
    
    - dungeon/
        
    - game_manager/
        
    - audio_manager/
        
- ui/
    
- data/
    
    - stats/
        
    - abilities/
        
- scenes/
    
    - levels/
        
- effects/
    

Keep components centralized.

Never duplicate component scripts in entity folders.

---

# 46. DEPENDENCY GRAPH (MENTAL MODEL)

GameManager  
↓  
Level Scene  
↓  
Entities  
↓  
Components  
↓  
States  
↓  
Abilities

Data Resources feed into components.

UI sits beside gameplay, listening only.

---

# 47. LONG-TERM MAINTAINABILITY STRATEGY

Every 2–3 months:

Refactor.

Checklist:

- Any script > 400 lines?
    
- Any direct sibling calls?
    
- Any hardcoded collision layers?
    
- Any duplicated stats?
    
- Any state transitions hidden in random components?
    

Refactor early.

---

# 48. FINAL PRODUCTION ENTITY TEMPLATE

Player:

CharacterBody2D

- CollisionShape2D
    
- MovementComponent
    
- JumpComponent
    
- AbilityManager
    
    - DashAbility
        
    - FireballAbility
        
- HealthComponent
    
- HurtboxComponent
    
- StateMachine
    
- AnimationTree
    
- InventoryComponent
    
- Camera2D
    

This is production scalable.

---

# 49. DETERMINISTIC SYSTEM DESIGN

Even in single-player games, determinism matters.

## 49.1 Why?

Because:

- Debugging becomes easier.
    
- Multiplayer becomes possible later.
    
- Replay systems become possible.
    
- Procedural generation becomes stable.
    

---

## 49.2 Randomness Discipline

Never call:

```gdscript
randi()
randf()
```

Directly in gameplay logic.

Instead:

Create RNGManager:

```gdscript
extends Node
class_name RNGManager

var rng := RandomNumberGenerator.new()

func seed_with(value: int):
	rng.seed = value

func randf():
	return rng.randf()

func randi_range(a, b):
	return rng.randi_range(a, b)
```

Now:

- Dungeon generation uses seeded RNG.
    
- Enemy behaviors use controlled randomness.
    
- Runs can be reproduced.
    

This is production discipline.

---

# 50. FRAME PACING & MICRO-STUTTER

Pixel games look simple.  
They are not.

## 50.1 Sources of Micro-Stutter

- Massive instantiation in one frame
    
- Freeing many nodes at once
    
- Expensive physics queries
    
- Too many active `_process()` nodes
    

---

## 50.2 Discipline Rules

- Use pooling for projectiles.
    
- Avoid spawning particle scenes repeatedly.
    
- Disable `_process()` unless required.
    
- Use `_physics_process()` only for physics.
    

---

## 50.3 Visual Smoothness Rule

For pixel art:

- Snap positions to integers.
    
- Avoid subpixel jitter.
    

Example:

```gdscript
global_position = global_position.round()
```

Only if necessary.

Camera smoothing must be consistent.

---

# 51. MEMORY DISCIPLINE IN NODE-HEAVY GAMES

Godot uses reference counting and garbage collection.

Memory leaks usually happen when:

- Signals are connected but never disconnected.
    
- Nodes are stored in global arrays and never freed.
    
- Autoload managers hold stale references.
    

---

## 51.1 Signal Cleanup Rule

If a component connects to something outside parent:

Disconnect in `_exit_tree()`.

---

## 51.2 Object Pool Strategy

Pool:

- Projectiles
    
- Damage numbers
    
- Particle bursts
    

Do not pool everything.  
Only high-frequency objects.

---

# 52. STATE MACHINE VS BEHAVIOR TREE

State Machines work best when:

- Behavior is finite and discrete.
    
- Enemies are not highly complex.
    

Behavior Trees are better when:

- Many layered decisions.
    
- Conditional branching grows exponentially.
    

For roguelike indie scale:

State Machine + PatternController is usually enough.

Switch only if:

- Enemy decision tree becomes unmanageable.
    
- Too many conditional transitions.
    

---

# 53. ANIMATIONTREE PARAMETER ARCHITECTURE

When using AnimationTree:

Never directly set animations in multiple places.

Instead:

StateMachine sets parameters:

```gdscript
animation_tree.set("parameters/conditions/is_moving", true)
animation_tree.set("parameters/conditions/is_attacking", false)
```

AnimationTree handles blending.

Important:

AnimationTree must not:

- Call gameplay functions.
    
- Trigger damage directly.
    

Keep gameplay authoritative.

---

# 54. ROGUELIKE RUN GENERATOR DESIGN

Procedural system must be layered.

## 54.1 Layers

- Seed
    
- Dungeon layout generation
    
- Room content generation
    
- Enemy stat variation
    
- Loot distribution
    

Each layer uses same RNG seed chain.

---

## 54.2 DungeonManager Responsibilities

- Generate room graph
    
- Instantiate room scenes
    
- Assign doors
    
- Populate enemies
    

Rooms must not:

- Know about global dungeon structure.
    
- Modify other rooms.
    

---

## 54.3 Content Variability Strategy

Instead of:

Multiple enemy scenes

Use:

One scene + different StatsResources.

Instead of:

Hardcoded loot

Use:

LootTable Resource:

- List of items
    
- Drop weights
    
- Roll via RNGManager
    

---

# 55. DEBUGGING LARGE SCENE TREES

As your game grows:

SceneTree becomes deep.

Use:

- Groups for tagging enemies.
    
- Print transitions in StateMachine.
    
- Enable “Visible Collision Shapes”.
    
- Use Remote Scene Tree during runtime.
    

Never debug by guessing.

---

# 56. LONG-TERM HOBBY STRATEGY

You said this is hobby mastery, not career.

That means:

You are building depth, not speed.

Follow this loop:

1. Build small system.
    
2. Stress it.
    
3. Refactor.
    
4. Add feature.
    
5. Refactor again.
    

Every major system should survive refactoring without collapsing.

---

# 57. ARCHITECTURAL MATURITY CHECKLIST

When your project is stable, you should be able to say:

- Player.gd < 300 lines.
    
- No component knows about siblings directly.
    
- Collision layers are documented.
    
- Stats are resource-driven.
    
- Abilities are plug-in modules.
    
- State transitions are centralized.
    
- No logic is animation-driven.
    
- No geometry is hardcoded in scripts.
    
- Projectiles are pooled.
    
- UI listens to events only.
    

If all true — you are in production architecture territory.

---

# 58. FINAL STRUCTURAL MENTAL MODEL

Everything reduces to this:

Physics layer handles movement.

Detection layer handles overlap.

Combat layer handles damage.

StateMachine coordinates behavior.

Animation reflects state.

Abilities extend behavior.

Resources configure data.

Managers coordinate global flow.

Signals propagate upward.

Dependencies flow inward.

If you respect these flows, your architecture scales.

If you violate them, entropy grows.

---

# 59. WHERE YOU STAND NOW

You now understand:

- Clean 2D component architecture
    
- Scalable combat systems
    
- Modular abilities
    
- Roguelike procedural design
    
- Platformer edge cases
    
- Performance discipline
    
- Production folder structure
    
- Debugging strategy
    
- Future multiplayer-safe thinking
    

This is beyond beginner.  
This is early engine-architect level.

---

# 60. WRAP-UP

Godot is simple at the surface.

But real mastery is not:

- Knowing nodes.
    
- Knowing signals.
    
- Knowing how to move a sprite.
    

Real mastery is:

Designing systems that survive growth.

You now have a structural blueprint for:

- Roguelike
    
- Platformer
    
- Combat-heavy pixel game
    
- Medium indie scale
    

Without architectural collapse.

---