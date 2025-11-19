# **1. Unity Fundamentals and Core Engine Architecture**

---

## **1.1 What Unity Actually Is**

Unity is:

- A real-time 3D game engine
    
- A C# scripting runtime
    
- A hybrid C#/C++ engine framework
    
- A component-based editor
    
- A scene-based development environment
    
- A tool ecosystem (Animator, Physics, UI, Audio, Navigation, Multiplayer, Rendering)
    

Unity **does NOT** behave like normal C#.  
Overview:

- Game logic runs inside Unity’s engine loop
    
- You don’t control the main program
    
- Unity calls **your** code, not the other way around
    
- You write scripts that plug into the engine
    
- The engine drives the rendering, physics, audio, etc.
    

---

## **1.2 The Unity Editor**

The Editor contains:

- **Scene View** – your 3D workspace
    
- **Game View** – what the player sees
    
- **Hierarchy** – objects in the current scene
    
- **Project Window** – assets, scripts, textures, prefabs
    
- **Inspector** – editable properties of selected objects
    
- **Console** – logs, errors, warnings
    

Everything in Unity happens in:

- Scenes
    
- GameObjects
    
- Components
    
- Assets
    

All scripting interacts with these.

---

# **2. GameObjects and the Component Model**

---

## **2.1 GameObject Overview**

A GameObject is an empty container that holds components.  
It has:

- A **Transform** (position, rotation, scale)
    
- **Any number of components** including your scripts, colliders, Rigidbody, renderers, audio sources, etc.
    

GameObjects can represent:

- Players
    
- Enemies
    
- UI elements
    
- Cameras
    
- Lights
    
- Invisible logic containers
    

---

## **2.2 Components**

A Component is a modular piece of behavior added to a GameObject.

Examples:

- Movement script (C#)
    
- Collider (Physics)
    
- Renderer (Graphics)
    
- Audio Source (Sound)
    
- Animator (Animation)
    
- Rigidbody (Physics Simulation)
    

### The Component Pattern:

Unity’s architecture uses Composition > Inheritance.  
Instead of:

```csharp
class Enemy : MovingThing : LivingThing : GameThing
```

You do:

```csharp
AddComponent<Movement>();
AddComponent<Health>();
AddComponent<AIController>();
```

Everything is small, reusable building blocks.

---

# **3. MonoBehaviour: Unity’s Scripting Base Class**

---

## **3.1 What MonoBehaviour Does**

MonoBehaviour gives your script:

- Access to Unity’s engine loop
    
- Lifecycle events (Awake, Start, Update, etc.)
    
- Access to GameObject & Component system
    
- Coroutines
    
- Inspectable fields in the Editor
    
- Methods like `StartCoroutine`, `Invoke`, `GetComponent`, etc.
    

Without inheriting MonoBehaviour, your script cannot:

- Be attached to a GameObject
    
- Run in the scene
    
- Use engine callbacks
    
- Be visible in the Inspector
    

---

## **3.2 Creating a Unity Script**

Unity scripts must inherit from MonoBehaviour:

```csharp
using UnityEngine;

public class Player : MonoBehaviour
{
    void Update()
    {
        transform.Translate(Vector3.forward * Time.deltaTime);
    }
}
```

Attach this script to a GameObject:

1. Drag it onto the object in the Hierarchy
    
2. Or use “Add Component” in Inspector
    

---

# **4. Unity’s Script Lifecycle (Execution Order)**

---

## **4.1 Overview**

Unity automatically calls certain methods at specific times.

Here is the official order:

### Initialization Phase:

1. **Awake**
    
2. **OnEnable**
    
3. **Start**
    

### Game Loop Phase:

4. **Update**
    
5. **FixedUpdate** (physics)
    
6. **LateUpdate**
    

### Deactivation Phase:

7. **OnDisable**
    
8. **OnDestroy**
    

---

## **4.2 Awake()**

Runs when the script instance is loaded.

Use it to:

- Initialize variables
    
- Get component references
    
- Prepare internal data
    

Example:

```csharp
void Awake()
{
    rb = GetComponent<Rigidbody>();
}
```

---

## **4.3 Start()**

Runs **after Awake**, but only if the object is enabled.

Use it to:

- Communicate with other objects
    
- Initialize game logic after everything is ready
    

Example:

```csharp
void Start()
{
    health = stats.maxHealth;
}
```

---

## **4.4 Update()**

Runs every frame.

Use it for:

- Player input
    
- Game logic
    
- Smooth motion
    
- Checking conditions
    

Example:

```csharp
void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
        Jump();
}
```

---

## **4.5 FixedUpdate()**

Runs on a fixed physics timestep.

Used for:

- Rigidbody motion
    
- Physics forces
    
- Physics-based AI
    

NEVER modify transform directly here.  
Always use Rigidbody functions.

Example:

```csharp
void FixedUpdate()
{
    rb.AddForce(movement * speed);
}
```

---

## **4.6 LateUpdate()**

Runs after Update.

Used for:

- Camera follow
    
- Animation adjustments
    
- UI updates dependent on movement
    

Example:

```csharp
void LateUpdate()
{
    camera.transform.position = player.position + offset;
}
```

---

## **4.7 OnDestroy()**

Used for:

- Cleaning up
    
- Removing listeners
    
- Saving progress
    

---

# **5. Fields, Inspector, Serialization, and Engine Metadata**

---

## **5.1 Unity Serialization**

Unity’s serialization system is unique:

- It does not use .NET reflection serialization
    
- It stores data in native engine format
    
- It displays editable fields in the Inspector
    

Unity serializes:

- Public fields
    
- `[SerializeField]` private fields
    
- Primitive types
    
- UnityEngine.Objects
    
- Structs
    
- Lists
    

Unity does NOT serialize:

- Dictionaries
    
- Properties
    
- Static fields
    
- Events
    
- Interfaces
    
- Abstract classes (unless concrete subclass provided)
    

---

## **5.2 Exposing Fields in Inspector**

Example:

```csharp
public float speed;
[SerializeField] private int health;
```

---

## **5.3 Hide Flags**

Control how fields appear in Inspector.

```csharp
[HideInInspector] public int debugValue;
```

---

## **5.4 Tool Attributes**

### Tooltip

```csharp
[Tooltip("Speed of the character in m/s.")]
public float speed;
```

### Range

```csharp
[Range(0f, 100f)]
public float health;
```

### Header

```csharp
[Header("Movement Settings")]
public float speed;
```

### Space

```csharp
[Space(20)]
public float jumpHeight;
```

### Multiline

```csharp
[Multiline(5)]
public string description;
```

---

# **6. Coroutines, Yield Instructions, and Engine Scheduling**

---

## **6.1 Coroutine Basics**

A coroutine is a method that can pause and resume automatically.

Unity’s “task scheduler” runs coroutines on the main thread.

---

## **6.2 Creating and Starting a Coroutine**

```csharp
IEnumerator FlashLight()
{
    light.enabled = true;
    yield return new WaitForSeconds(0.5f);
    light.enabled = false;
}

void Start()
{
    StartCoroutine(FlashLight());
}
```

---

## **6.3 Yield Types**

### WaitForSeconds

Pause for time.

```csharp
yield return new WaitForSeconds(2);
```

### WaitForEndOfFrame

Runs after rendering is done.

### WaitForFixedUpdate

Runs on next physics update.

### CustomYieldInstruction

Create custom waiting conditions.

---

# **7. GameObject and Component Interaction**

---

## **7.1 Getting Components**

### GetComponent

```csharp
var rb = GetComponent<Rigidbody>();
```

### GetComponentInChildren

```csharp
var gun = GetComponentInChildren<Gun>();
```

### GetComponentInParent

```csharp
var container = GetComponentInParent<Inventory>();
```

### FindObjectOfType (slow)

```csharp
var enemy = FindObjectOfType<Enemy>();
```

### Best Practice:

**Cache** components in Awake.

---

# **8. Unity Input Systems (Old & New)**

---

## **8.1 Legacy Input System**

```csharp
if (Input.GetKey(KeyCode.W))
    MoveForward();
```

Supports:

- Keyboard
    
- Mouse
    
- Basic joystick
    

---

## **8.2 New Input System**

Fully action-based.

- Input Actions
    
- Rebindable keys
    
- Gamepad vibration
    
- Touch
    
- UI input
    

Example:

```csharp
public InputActionProperty jumpAction;

void Update()
{
    if (jumpAction.action.triggered)
        Jump();
}
```

---

# **9. Physics System**

---

## **9.1 Rigidbody**

Controls dynamic physics objects.

---

## **9.2 Applying Forces**

```csharp
rb.AddForce(Vector3.forward * 10f, ForceMode.Impulse);
```

---

## **9.3 Collisions**

### OnCollisionEnter

```csharp
void OnCollisionEnter(Collision collision)
```

### OnTriggerEnter

```csharp
void OnTriggerEnter(Collider other)
```

---

# **10. Prefabs**

Prefabs are reusable object templates.

They store:

- Components
    
- Properties
    
- Child objects
    

Used for:

- Enemies
    
- Bullets
    
- Structures
    
- UI
    
- Interactive objects
    

---

# **11. Scene Management**

Use SceneManager:

### Load Scene

```csharp
SceneManager.LoadScene("Level2");
```

### Load Scene Async

```csharp
StartCoroutine(LoadLevel("Level3"));
```

---

# **12. ScriptableObjects (Unity’s Data Assets)**

Used for:

- Inventory items
    
- Weapon stats
    
- Player stats
    
- Dialogue
    
- Game settings
    

---

# **13. Unity Events and Delegates**

Unity provides:

- UnityEvent (Inspector-based)
    
- C# events
    
- Messaging systems
    

---

# **14. UI Toolkit and Canvas UI**

Covers:

- Canvas
    
- RectTransform
    
- TextMeshPro
    
- UI events
    
- Buttons, sliders
    
- Worldspace UI
    

---

# **15. Animation System (Animator and Mecanim)**

Covers:

- Animator Controller
    
- State machine
    
- Animation events
    
- Blend trees
    

---

# **16. Audio System**

Covers:

- AudioSource
    
- AudioClip
    
- 2D vs 3D sound
    

---

# **17. Navigation and Pathfinding**

Covers:

- NavMesh
    
- NavMeshAgent
    
- NavMeshObstacle
    

---

# **18. Particle System**

Covers:

- Emission
    
- Shape
    
- Noise
    
- Trails
    
- Color over lifetime
    
---

# **19. Lighting and Rendering**

---

## **19.1 Lighting Types in Unity**

Unity supports multiple lighting modes, each affecting performance, mood, and realism.

### **Directional Light**

- Represents sunlight or moonlight
    
- Light rays are parallel
    
- Affects the entire scene
    

Example use:

- Outdoor daytime scenes
    
- Stylized platformers
    
- Open-world environments
    

### **Point Light**

- Emits light in all directions from a single point
    
- Useful for lamps, torches, glowing items
    

### **Spot Light**

- Emits a cone-shaped beam
    
- Used for flashlights, car headlights, stage lights
    

### **Area Light** (Editor-only, baked)

- Soft rectangular light source
    
- Used for interior lighting
    

---

## **19.2 Lighting Modes**

### **Realtime Lighting**

- Updates every frame
    
- Used for dynamic gameplay
    

### **Baked Lighting**

- Precomputed
    
- No runtime cost
    
- Used for static scenery
    

### **Mixed Lighting**

- Combination of realtime + baked
    
- Useful for scenes where static and dynamic objects interact
    

---

## **19.3 Render Pipelines**

Unity has 3 major render pipelines:

### **Built-in Render Pipeline**

- Default
    
- Works for most projects
    

### **Universal Render Pipeline (URP)**

- Fast
    
- Mobile-friendly
    
- Shader Graph support
    
- Good for stylized graphics
    

### **High Definition Render Pipeline (HDRP)**

- Realistic lighting
    
- Volumetrics
    
- High-end effects
    
- Used for PC/console AAA visuals
    

---

## **19.4 Materials and Shaders**

### **Material**

Defines how a surface looks.

### **Shader**

Code that tells the GPU how to render the material.

Unity supports:

- Standard Shader
    
- URP Lit Shader
    
- HDRP Lit Shader
    
- Shader Graph
    
- Custom HLSL shaders
    

---

# **20. Camera System**

---

## **20.1 Camera Basics**

The camera renders the game world.

Main settings:

- Field of View
    
- Projection (Perspective / Orthographic)
    
- Clipping planes
    
- Clear flags
    
- Viewport rect
    

Example:

```csharp
Camera.main.fieldOfView = 70f;
```

---

## **20.2 Cinemachine (Advanced Camera Tool)**

Cinemachine provides:

- Automatic follow camera
    
- Orbit camera
    
- Aim system
    
- Transitions
    
- Shake effects
    

Used in:

- FPS
    
- Third-person games
    
- Racing games
    
- Cutscenes
    

---

# **21. Input Systems — Deep Dive**

---

## **21.1 Legacy Input Use Cases**

Most indie games still use the legacy system for its simplicity.

Examples:

```csharp
float h = Input.GetAxis("Horizontal");
float v = Input.GetAxis("Vertical");
```

- Good for prototypes
    
- Good for simple games
    
- Limited for advanced input
    

---

## **21.2 New Input System — Action-Based**

You create **Input Actions**:

- Move
    
- Look
    
- Jump
    
- Shoot
    
- Menu controls
    

Then call them in code:

```csharp
public InputActionProperty moveAction;

void Update()
{
    Vector2 move = moveAction.action.ReadValue<Vector2>();
}
```

Supports:

- Rebinding
    
- Multiplayer input
    
- Gamepads
    
- Touch
    
- VR controllers
    
- UI
    

---

# **22. Physics — Advanced Workflow**

---

## **22.1 Rigidbody Deep Behavior**

Rigidbody properties:

- **Mass**
    
- **Drag**
    
- **Angular drag**
    
- **Use gravity**
    
- **Is kinematic**
    
- **Collision detection modes**
    

### Kinematic Rigidbody:

- Not affected by physics
    
- Ideal for controlled movement (platforms, elevators)
    

### Dynamic Rigidbody:

- Fully physics-driven
    
- Ideal for characters, vehicles, objects
    

---

## **22.2 Rigidbody Movement Methods**

### Use Velocity

```csharp
rb.velocity = moveDirection * speed;
```

### Use AddForce

```csharp
rb.AddForce(force, ForceMode.Impulse);
```

### Use MovePosition (for kinematic rigidbodies)

```csharp
rb.MovePosition(rb.position + move * Time.fixedDeltaTime);
```

### Use MoveRotation for rotation

```csharp
rb.MoveRotation(rb.rotation * Quaternion.Euler(rot));
```

---

## **22.3 Collision Messages**

### Collision-based

```csharp
void OnCollisionEnter(Collision col)
{
    Debug.Log("Hit " + col.gameObject.name);
}
```

### Trigger-based

```csharp
void OnTriggerEnter(Collider col)
{
    Debug.Log("Triggered with " + col.name);
}
```

Use triggers for:

- Pickups
    
- Doors
    
- Detection zones
    
- Damage zones
    

---

# **23. Prefabs — Advanced Uses**

---

## **23.1 Prefab Variants**

Useful for:

- Enemy types
    
- Different weapons
    
- Item versions
    

Variants inherit from a base prefab but override differences.

---

## **23.2 Nested Prefabs**

Allows:

- UI building
    
- Modular character designs
    
- Complex environment setup
    

Example:

- A UI Panel prefab contains a Button prefab
    
- A Door prefab contains a Lock prefab
    
- A character contains Weapon prefabs
    

---

## **23.3 Prefab Instantiation**

```csharp
Instantiate(projectilePrefab, firePoint.position, firePoint.rotation);
```

Options:

- Instantiate with parent
    
- Instantiate at runtime
    
- Instantiate UI elements
    

---

# **24. Scene Management — Full System**

---

## **24.1 Loading Scenes**

### Basic load:

```csharp
SceneManager.LoadScene("MainMenu");
```

### Additive load:

```csharp
SceneManager.LoadScene("HUD", LoadSceneMode.Additive);
```

Used for:

- HUD overlay
    
- Streaming world
    
- Multi-part environments
    

---

## **24.2 Async Loading**

```csharp
IEnumerator LoadSceneAsync(string name)
{
    AsyncOperation op = SceneManager.LoadSceneAsync(name);

    while (!op.isDone)
    {
        progressBar.fillAmount = op.progress;
        yield return null;
    }
}
```

---

## **24.3 Scene Unloading**

```csharp
SceneManager.UnloadSceneAsync("HUD");
```

Used for:

- Memory management
    
- Level transitions
    

---

# **25. ScriptableObjects — Detailed System**

---

## **25.1 ScriptableObject Advantages**

- Not attached to GameObjects
    
- Lives as an asset
    
- Can store reusable data
    
- Reduces memory duplication
    
- Editable in Inspector
    
- Serializable fields
    

---

## **25.2 Creating a ScriptableObject Type**

```csharp
[CreateAssetMenu(menuName = "Weapons/WeaponData")]
public class WeaponData : ScriptableObject
{
    public string weaponName;
    public int damage;
    public float fireRate;
}
```

---

## **25.3 Using ScriptableObjects in Game Code**

```csharp
public WeaponData weapon;

void Shoot()
{
    Debug.Log("Damage: " + weapon.damage);
}
```

---

## **25.4 Use Cases**

- Item databases
    
- Player stats
    
- AI behavior profiles
    
- Level configuration
    
- Animation sets
    
- Global settings
    

---

# **26. Audio System**

---

## **26.1 AudioSource**

```csharp
audioSource.Play();
audioSource.Stop();
audioSource.loop = true;
```

Settings:

- Volume
    
- Pitch
    
- Spatial blend
    
- 3D attenuation
    

---

## **26.2 AudioMixer**

Used for:

- Music
    
- SFX
    
- Voice
    
- Ambience
    

Can apply:

- Reverb
    
- Low-pass filters
    
- Pitch shift
    

---

## **26.3 Advanced Example — Footstep System**

```csharp
public AudioClip[] footsteps;

void PlayStep()
{
    audioSource.PlayOneShot(footsteps[Random.Range(0, footsteps.Length)]);
}
```

---

# **27. Animation System (Animator + Mecanim)**

---

## **27.1 Animator Controller**

Contains:

- Animation states
    
- Transitions
    
- Parameters
    
- Blend trees
    

---

## **27.2 Parameters**

- Float
    
- Int
    
- Bool
    
- Trigger
    

Example:

```csharp
animator.SetTrigger("Attack");
```

---

## **27.3 Animation Events**

Used for:

- Footstep sounds
    
- Attack hit events
    
- VFX triggers
    

---

## **27.4 Blend Trees**

Used for movement transitions:

- Idle → Walk → Run
    

---

# **28. User Interface (UI)**

---

## **28.1 Canvas**

Types:

- Screen Space - Overlay
    
- Screen Space - Camera
    
- World Space
    

---

## **28.2 TextMeshPro**

Used for:

- High-quality text
    
- Rich formatting
    
- Dynamic fonts
    

---

## **28.3 UI Events**

```csharp
public void OnButtonClick()
{
    Debug.Log("Button pressed!");
}
```

---

## **28.4 UI Scaling**

Use Canvas Scaler to adapt UI across resolutions.

---

# **29. Navigation System (NavMesh)**

---

## **29.1 NavMesh Baking**

Defines walkable surfaces.

---

## **29.2 NavMeshAgent**

Movement:

```csharp
agent.SetDestination(target.position);
```

Settings:

- Speed
    
- Angular speed
    
- Acceleration
    
- Stopping distance
    

---

## **29.3 OffMeshLinks**

Used for:

- Jumping gaps
    
- Climbing
    
- Ledges
    
---

# **30. Rendering, Shaders, Shader Graph, and Visual Effects**

---

## **30.1 Rendering Overview**

Unity’s rendering system controls:

- How objects appear
    
- Lighting behavior
    
- Shadows
    
- Materials
    
- Transparency
    
- Post-processing
    
- Special effects (glow, bloom, motion blur)
    

Different render pipelines change how Unity renders:

- **Built-In** — classic, simplest
    
- **URP (Universal Render Pipeline)** — optimized, flexible, great for mobile and indie
    
- **HDRP (High Definition Render Pipeline)** — photorealistic, heavy, AAA visuals
    

Each pipeline has:

- Its own shader types
    
- Lighting model
    
- Render settings
    

---

## **30.2 Materials**

### What a Material Does

A material tells Unity:

- How the surface should look
    
- How light should react
    
- Which textures to use
    
- Which shader defines the logic
    

Common material properties:

- Albedo (base color)
    
- Metallic
    
- Smoothness
    
- Normal map
    
- Emission
    
- Occlusion
    

### Example of setting a material in code:

```csharp
public Renderer rend;

void Start()
{
    rend.material.color = Color.red;
}
```

---

## **30.3 Shaders**

A **shader** is GPU code that determines how an object is visualized.

Types in Unity:

- Standard Shader
    
- Surface Shaders
    
- Vertex/Fragment Shaders
    
- URP/HDRP Lit Shaders
    
- Shader Graph shaders
    
- Custom HLSL shaders
    

### Use Cases:

- Water
    
- Fire
    
- Cartoon outlines
    
- Holograms
    
- Force fields
    
- Invisible triggers
    
- Custom terrain shaders
    

---

## **30.4 Shader Graph**

A node-based shader editor — no programming required.

Allows you to create:

- Dissolve effects
    
- Holograms
    
- Fresnel glow
    
- Scrolling UVs
    
- Custom lighting
    
- Animated materials
    

### Example nodes:

- Time → Sin → Multiply → Color
    
- UV → Panner node → Texture sample
    
- Normal · View → Fresnel effect
    

### Scenario:

You want your ghost enemy to glow around the edges.  
Use **Fresnel > Emission**.

---

# **31. Visual Effects (Particles, VFX Graph)**

---

## **31.1 Particle System**

Used for:

- Fire
    
- Smoke
    
- Rain
    
- Explosions
    
- Magic spells
    
- Dust trails
    
- Sparks
    

Main modules:

- Emission
    
- Shape
    
- Velocity over time
    
- Color over lifetime
    
- Size over lifetime
    
- Collision
    
- Lights
    
- Trails
    

### Example: enabling a particle burst

```csharp
particleSystem.Emit(50);
```

---

## **31.2 VFX Graph (Visual Effect Graph)**

High-performance GPU effects.  
Used for:

- Large-scale particle systems
    
- Force fields
    
- Aura effects
    
- Weather
    
- Magic
    
- Sci-fi VFX
    

Better than ParticleSystem for:

- Thousands of particles
    
- Heavy GPU simulations
    

---

# **32. Addressables (Modern Asset Management)**

---

## **32.1 What Addressables Solve**

- Scene-independent asset loading
    
- Async loading
    
- Memory management
    
- Remote content delivery
    
- Loading large levels smoothly
    

---

## **32.2 Basic Usage Example**

### Load an asset:

```csharp
Addressables.LoadAssetAsync<GameObject>("Enemy").Completed += handle =>
{
    Instantiate(handle.Result);
};
```

### Release:

```csharp
Addressables.Release(handle);
```

---

## **32.3 Use Cases**

- Inventory items
    
- Characters
    
- UI elements
    
- Huge environments
    
- Downloadable content
    

---

# **33. DOTS / ECS (Data-Oriented Technology Stack)**

---

## **33.1 What ECS Is**

ECS = Entity Component System.  
A performance-focused system for:

- Thousands of units
    
- Procedural worlds
    
- Large AI swarms
    
- High-speed simulation
    

Instead of MonoBehaviours, ECS splits things into:

- **Entities** — IDs
    
- **Components** — pure data
    
- **Systems** — logic
    

---

## **33.2 Entity Example (Simplified)**

```csharp
public struct MoveSpeed : IComponentData
{
    public float value;
}
```

Systems:

```csharp
public partial class MovementSystem : SystemBase
{
    protected override void OnUpdate()
    {
        float dt = Time.DeltaTime;

        Entities.ForEach((ref Translation t, in MoveSpeed speed) =>
        {
            t.Value.z += speed.value * dt;
        }).ScheduleParallel();
    }
}
```

---

## **33.3 When to Use ECS**

- 10,000+ NPCs
    
- Simulation-heavy games
    
- Tower defense swarms
    
- Procedural generation
    
- RTS unit control
    

---

# **34. Multiplayer Systems (Netcode for GameObjects)**

---

## **34.1 Basic Concepts**

Unity’s Netcode includes:

- NetworkManager
    
- NetworkObject
    
- NetworkVariable
    
- RPCs (Remote Procedure Calls)
    

---

## **34.2 NetworkObject**

Every networked object must have:

```csharp
public class Player : NetworkBehaviour
{
}
```

---

## **34.3 RPC Example**

### Server RPC

```csharp
[ServerRpc]
void ShootServerRpc()
{
    // server-side logic
}
```

### Client RPC

```csharp
[ClientRpc]
void ShowHitEffectClientRpc()
{
    // client VFX
}
```

---

## **34.4 NetworkVariables**

```csharp
public NetworkVariable<int> health = new NetworkVariable<int>(100);
```

Synchronizes automatically.

---

# **35. Editor Scripting (Professional Tools Development)**

---

## **35.1 Custom Editors**

Allows customizing the Inspector.

Example:

```csharp
[CustomEditor(typeof(PlayerStats))]
public class PlayerStatsEditor : Editor
{
    public override void OnInspectorGUI()
    {
        DrawDefaultInspector();
        GUILayout.Label("Custom UI Here!");
    }
}
```

---

## **35.2 EditorWindows**

Build entire custom tools.

```csharp
public class ToolWindow : EditorWindow
{
    [MenuItem("Tools/MyTool")]
    public static void ShowWindow()
    {
        GetWindow<ToolWindow>("My Tool");
    }
}
```

Used for:

- Level editors
    
- Dialogue editors
    
- Item databases
    
- Procedural tools
    

---

## **35.3 Handles & Scene Tools**

Used for:

- Custom gizmos
    
- Click-able tools in the Scene view
    
- Designers interacting visually with your scripts
    

---

# **36. Optimization**

---

## **36.1 Profiling Tools**

- Profiler
    
- Memory profiler
    
- Frame Debugger
    
- Rendering debugger
    

---

## **36.2 CPU Optimization**

- Cache components
    
- Avoid Find functions
    
- Avoid Update in many objects → use “manager” pattern
    
- Use coroutines instead of Update (when suitable)
    
- Use object pooling
    

---

## **36.3 GPU Optimization**

- Reduce material count
    
- Use texture atlases
    
- Avoid overdraw
    
- Limit realtime lights
    
- Use baked lighting
    
- Prefer URP for mobile
    

---

## **36.4 Memory Optimization**

- Use Addressables
    
- Pool objects
    
- Compress textures
    
- Unload unused assets
    
- Avoid large prefabs with unnecessary components
    

---

# **37. Architecture and Professional Patterns**

---

## **37.1 Component-Based Design**

Every script should do **one thing well**:

- Health script controls health
    
- Movement script controls movement
    
- AI script controls behavior
    
- Inventory script controls items
    

---

## **37.2 ScriptableObject Architecture**

Common pattern:

- Data in ScriptableObjects
    
- Logic in MonoBehaviours
    
- Events through C# or UnityEvents
    

---

## **37.3 Manager Pattern**

Examples:

- GameManager
    
- AudioManager
    
- UIManager
    
- LevelManager
    

Store global logic in a central class.

---

## **37.4 Event-Based Architecture**

Reduce direct dependencies:

- C# events
    
- UnityEvents
    
- ScriptableObject Events
    
- Observer pattern
    

---

# **38. Full Game Development Workflows**

---

## **38.1 Prototyping Workflow**

1. Block out gameplay
    
2. Use placeholder graphics
    
3. Create rapid prototypes
    
4. Establish feel first
    
5. Add real assets later
    

---

## **38.2 Production Workflow**

1. Level design
    
2. Character controllers
    
3. AI systems
    
4. Animation pipelines
    
5. UI development
    
6. Polishing
    
7. Optimization
    
8. Platform builds
    

---

## **38.3 Publishing Workflow**

1. Build Settings
    
2. Platform settings
    
3. Run device tests
    
4. Optimize textures
    
5. Set correct quality settings
    
6. Submit to store
    

---

# **39. Artificial Intelligence (AI) in Unity**

---

## **39.1 Overview of Unity AI Approaches**

Unity does not include a single built-in “AI system.”  
Instead, developers build AI using combinations of:

- Finite State Machines (FSMs)
    
- Behaviour Trees
    
- Utility AI
    
- ScriptableObject-driven AI profiles
    
- NavMesh pathfinding
    
- Physics-based sensing
    
- Animation-based responses
    
- Custom decision-making systems
    

Each approach has different strengths depending on the type of game.

---

## **39.2 Finite State Machines (FSM)**

The most common and easiest AI structure.

### **What an FSM Looks Like**

An enemy can be in one of these states:

- Idle
    
- Patrol
    
- Chase
    
- Attack
    
- Flee
    

Each state has:

- **Enter logic**
    
- **Update logic**
    
- **Exit logic**
    

### **Basic FSM Example**

```csharp
public enum EnemyState
{
    Idle,
    Chase,
    Attack
}

public class EnemyAI : MonoBehaviour
{
    public EnemyState state;
    public Transform player;
    public float attackRange = 2f;

    void Update()
    {
        switch(state)
        {
            case EnemyState.Idle:
                if (CanSeePlayer())
                    state = EnemyState.Chase;
                break;

            case EnemyState.Chase:
                transform.position = Vector3.MoveTowards(
                    transform.position,
                    player.position,
                    Time.deltaTime * 3f);

                if (Vector3.Distance(transform.position, player.position) < attackRange)
                    state = EnemyState.Attack;
                break;

            case EnemyState.Attack:
                AttackPlayer();
                break;
        }
    }

    bool CanSeePlayer() => Vector3.Distance(transform.position, player.position) < 10f;
    void AttackPlayer() => Debug.Log("Attacking!");
}
```

### **When to Use FSM**

- Simple enemies
    
- Platformers
    
- RPG NPCs
    
- Boss fight phases
    

---

# **40. Behaviour Trees (Advanced AI)**

---

## **40.1 What Behaviour Trees Solve**

Behaviours trees allow AI to:

- Select actions intelligently
    
- Execute complex logic
    
- Retry until success
    
- Run sequences
    
- Run parallel checks
    

Used in:

- AAA games
    
- Stealth mechanics
    
- Complex NPC behavior
    

---

## **40.2 Behaviour Tree Structure**

Tree nodes:

- **Selector** (OR)
    
- **Sequence** (AND)
    
- **Decorator** (conditional)
    
- **Actions**
    

### **Visual Breakdown**

```
Selector
 ├── Attack sequence
 │     ├── InRange?
 │     ├── Aim
 │     └── Shoot
 └── Chase sequence
       ├── SeePlayer?
       └── MoveToPlayer
```

---

## **40.3 Basic Behaviour Tree Example**

```csharp
// Pseudo-code for explanation
if (CanAttack())
{
    AimAtPlayer();
    Shoot();
}
else if (CanSeePlayer())
{
    ChasePlayer();
}
else
{
    Patrol();
}
```

### **Use Cases**

- Stealth AI
    
- Tactical shooters
    
- Companion AIs
    
- Monsters with complex reactions
    

---

# **41. Sensor Systems and Detection**

---

## **41.1 Raycasting for Vision**

```csharp
if (Physics.Raycast(transform.position, transform.forward, out RaycastHit hit, 10f))
{
    if (hit.collider.CompareTag("Player"))
        Chase();
}
```

Used for:

- Enemy vision
    
- Laser sensors
    
- Line-of-sight detection
    

---

## **41.2 OverlapSphere for Proximity**

```csharp
Collider[] colliders = Physics.OverlapSphere(transform.position, 5f);
```

Used for:

- Aggro radius
    
- Explosions
    
- Triggering area-based events
    

---

## **41.3 Field of View Checking**

```csharp
Vector3 dir = (player.position - transform.position).normalized;
float angle = Vector3.Angle(transform.forward, dir);

if (angle < 45f)
{
    // Player in FOV
}
```

Used for:

- Cone vision
    
- Security cameras
    
- Enemy stealth detection
    

---

# **42. Physics — Advanced Topics**

---

## **42.1 Layers and Collision Matrix**

Unity allows specifying which layers collide with each other.

### Example Use Cases:

- Ignoring projectiles hitting the player
    
- Making enemies ignore each other
    
- Preventing floor triggers from colliding with props
    

---

## **42.2 Continuous Collision Detection**

Used for:

- Fast bullets
    
- Fast-moving vehicles
    
- Objects tunneling through walls
    

```csharp
rb.collisionDetectionMode = CollisionDetectionMode.ContinuousDynamic;
```

---

## **42.3 Rigidbody Interpolation**

Smooths movement when physics updates cause jitter.

```
rb.interpolation = RigidbodyInterpolation.Interpolate;
```

---

## **42.4 Joints**

Used for:

- Ragdolls
    
- Hinges
    
- Suspensions
    
- Physics ropes
    

Joint types:

- Hinge Joint
    
- Spring Joint
    
- Configurable Joint
    
- Fixed Joint
    

---

# **43. Terrain System**

---

## **43.1 Terrain Tools**

Unity includes a terrain editor with:

- Height painting
    
- Texture painting
    
- Tree placement
    
- Grass placement
    
- Terrain layers
    

---

## **43.2 Terrains at Runtime**

### Access height map:

```csharp
float height = terrainData.GetHeight(x, y);
```

### Modify terrain:

```csharp
terrainData.SetHeight(x, y, newHeight);
```

---

## **43.3 Terrain LOD (Level of Detail)**

Automatically adjusts resolution based on distance.

---

# **44. Pathfinding and Navigation — Advanced**

---

## **44.1 NavMesh Obstacle**

Blocks pathfinding.

Types:

- Car
    
- Moving obstacle
    
- Dynamic barricade
    

---

## **44.2 Carving**

Allows dynamic environment changes.

Example:

```csharp
navMeshObstacle.carving = true;
```

Use cases:

- Doors opening
    
- Moving crates
    
- Shifting terrain
    

---

# **45. Player Controllers (FPS, TPS, Platformer, Top-Down)**

---

## **45.1 FPS Controller — Basic Structure**

- Handle mouse input for camera rotation
    
- Handle WASD movement
    
- Use CharacterController for collision detection
    

### Example:

```csharp
CharacterController controller;
Vector3 velocity;

void Update()
{
    float x = Input.GetAxis("Horizontal");
    float z = Input.GetAxis("Vertical");

    Vector3 move = transform.right * x + transform.forward * z;
    controller.Move(move * speed * Time.deltaTime);
}
```

---

## **45.2 Platformer Controller**

Requires:

- Raycasting to detect ground
    
- Jump logic
    
- Variable jump height
    
- Coyote time (jump forgiveness)
    

---

## **45.3 Top-Down Controller**

```csharp
Vector3 input = new Vector3(Input.GetAxis("Horizontal"), 0, Input.GetAxis("Vertical"));
transform.position += input * speed * Time.deltaTime;
```

---

# **46. Complete Combat Systems**

---

## **46.1 Melee Combat**

Core elements:

- Hitboxes
    
- Animations
    
- Cooldowns
    
- Combo logic
    

---

## **46.2 Ranged Combat**

Requires:

- Bullet prefabs
    
- Muzzle flash
    
- Recoil
    
- Shooting sounds
    
- Enemy hit detection
    

---

# **47. Inventory & Item Systems**

---

## **47.1 ScriptableObject-based Items**

```csharp
[CreateAssetMenu(menuName = "Items/Item")]
public class Item : ScriptableObject
{
    public string itemName;
    public Sprite icon;
}
```

---

## **47.2 Inventory Controller**

```csharp
List<Item> items = new List<Item>();
```

Supports:

- Adding items
    
- Using items
    
- Dropping items
    

---

# **48. Dialogue Systems**

---

## **48.1 Basic Structure**

- Dialogue database (ScriptableObject)
    
- Dialogue UI
    
- NPC triggers
    

---

# **49. Saving & Loading Systems**

---

## **49.1 JSON Save System**

```csharp
string json = JsonUtility.ToJson(data);
File.WriteAllText(path, json);
```

---

## **49.2 PlayerPrefs**

Small data only:

```csharp
PlayerPrefs.SetInt("HighScore", 100);
```

---

# **50. Level Design Tools & Editor Automation**

---

## **50.1 Custom Level Tools**

- Placement tools
    
- Auto-tiling
    
- Prefab painters
    
- Random object spawners
    

---

# **51. State Machines for Animation (Animator)**

---

## **51.1 Animator Layers**

Used for:

- Upper-body animations
    
- Aiming rigs
    
- Blending walking & attacking
    

---

## **51.2 Animation Rigging**

Used for:

- IK (inverse kinematics)
    
- Procedural aiming
    
- Foot placement
    

---

# **52. Production-Ready Architecture**

---

## **52.1 Folder Structure**

```
Assets/
  Scripts/
  Prefabs/
  Scenes/
  Art/
  Audio/
  UI/
  Data/
  Materials/
```

---

## **52.2 Script Structure Template**

```
Fields  
Initialization  
Update loop  
Public APIs  
Private helpers  
Events  
```

---

# **53. Object Pooling (High-Performance Object Reuse)**

---

## **53.1 Why Object Pooling Matters**

Instantiating and destroying GameObjects at runtime is expensive because Unity must:

- Allocate memory
    
- Register components
    
- Initialize transforms
    
- Sync with physics
    
- Rebuild internal engine lists
    

Pooling avoids this by **reusing** inactive objects.

Used in:

- Bullet systems
    
- Particle bursts
    
- Enemy spawning
    
- Loot drops
    
- Footsteps
    
- Decals (bullet holes, blood)
    
- Breakable objects
    

---

## **53.2 Basic Object Pool Implementation**

### Pool Manager Script

```csharp
using UnityEngine;
using System.Collections.Generic;

public class ObjectPool : MonoBehaviour
{
    public GameObject prefab;
    public int size = 10;

    private Queue<GameObject> pool = new Queue<GameObject>();

    void Awake()
    {
        for (int i = 0; i < size; i++)
        {
            GameObject obj = Instantiate(prefab);
            obj.SetActive(false);
            pool.Enqueue(obj);
        }
    }

    public GameObject Get()
    {
        if (pool.Count == 0)
            ExpandPool();

        GameObject obj = pool.Dequeue();
        obj.SetActive(true);
        return obj;
    }

    public void Return(GameObject obj)
    {
        obj.SetActive(false);
        pool.Enqueue(obj);
    }

    void ExpandPool()
    {
        GameObject obj = Instantiate(prefab);
        obj.SetActive(false);
        pool.Enqueue(obj);
    }
}
```

### Using the Pool

```csharp
GameObject bullet = pool.Get();
bullet.transform.position = firePoint.position;
bullet.transform.forward = firePoint.forward;
```

### Returning an Object

```csharp
pool.Return(gameObject);
```

---

## **53.3 When NOT to Pool**

- Very complex objects (huge animations, advanced shaders)
    
- Objects created only once per session
    
- UI elements that exist permanently
    

---

# **54. Procedural Generation Systems**

---

## **54.1 Types of Procedural Systems in Unity**

- Level generation
    
- Terrain generation
    
- Item loot rolls
    
- Enemy spawns
    
- Weather patterns
    
- Dialogue generation
    
- Dungeon generation
    

---

## **54.2 Noise Functions**

Unity supports:

- Perlin Noise
    
- Simplex Noise
    
- Custom fractal noise
    

### Example: Generating Terrain Heights

```csharp
float height = Mathf.PerlinNoise(x * scale, y * scale) * maxHeight;
```

Uses:

- Hills
    
- Mountains
    
- Clouds
    
- Procedural textures
    

---

## **54.3 Procedural Dungeon Generation (Example)**

Simple algorithm:

1. Start at a position
    
2. Randomly choose a direction
    
3. Place a room
    
4. Continue until room count met
    

---

## **54.4 Procedural Spawning Example**

```csharp
int count = Random.Range(minEnemies, maxEnemies);

for (int i = 0; i < count; i++)
{
    Vector3 position = Random.insideUnitSphere * spawnRadius;
    Instantiate(enemyPrefab, position, Quaternion.identity);
}
```

---

# **55. Scene Streaming and Massive Worlds**

---

## **55.1 Why Scene Streaming?**

For large games:

- RPGs
    
- Open-world games
    
- Survival games
    
- MMOs
    

You can’t load everything at once.

Unity supports:

- Additive scenes
    
- Async loading
    
- Streaming terrain
    
- Unloading sections
    

---

## **55.2 Additive Scene Loading**

```csharp
SceneManager.LoadSceneAsync("Forest", LoadSceneMode.Additive);
```

Unload:

```csharp
SceneManager.UnloadSceneAsync("Forest");
```

---

## **55.3 Use Cases**

- Open world chunk loading
    
- Loading interior scenes
    
- Loading UI as a separate scene
    
- Maintaining persistent GameManager
    

---

# **56. Game Framework and Code Architecture**

---

## **56.1 Manager Structure**

Highly recommended managers:

- GameManager
    
- AudioManager
    
- InputManager
    
- SpawnManager
    
- UIManager
    

Use a “Manager Scene” and mark it:

```csharp
DontDestroyOnLoad(gameObject);
```

---

## **56.2 Event-Based Design**

Avoid spaghetti dependencies.

Use either:

- C# events
    
- UnityEvents
    
- ScriptableObject Events
    
- Event buses
    

### Example: Global Event

```csharp
public static event Action OnPlayerDeath;
```

---

## **56.3 Service Locator Pattern**

Used for global access to systems.

---

## **56.4 Dependency Injection**

Used in:

- Large games
    
- Modular systems
    
- Testable architecture
    

Popular DI frameworks:

- Zenject
    
- Extenject
    

---

# **57. Advanced Animation Systems**

---

## **57.1 Animation Rigging Package**

Features:

- Two-bone IK
    
- Multi-aim constraint
    
- Multi-position constraint
    
- Procedural aiming
    
- Dynamic defensive poses
    
- Foot placement (anti-floating effect)
    

### Example: Making a gun aim at the cursor

Use **Aim Constraint** and update target via script.

---

## **57.2 Root Motion**

Root motion means animation drives movement.

Used in:

- Fighting games
    
- Souls-like games
    
- Motion matching
    
- Cinematics
    

Disable when movement should be script-controlled.

---

## **57.3 Animation Events**

Used to trigger:

- Footstep sounds
    
- Weapon swing hits
    
- Spell cast effects
    
- Camera shake
    

Example:

```csharp
public void OnHitFrame()
{
    SpawnHitEffect();
}
```

---

# **58. Camera Systems & Cinematics**

---

## **58.1 Cinemachine**

Virtual cameras automatically:

- Follow targets
    
- Look at targets
    
- Smooth transitions
    
- Add shake
    
- Limit rotation
    
- Orbit characters
    

---

## **58.2 Camera Shake Example**

```csharp
CinemachineImpulseSource impulse;
impulse.GenerateImpulse();
```

---

## **58.3 Timeline Tool**

Used for:

- Cutscenes
    
- Scripted sequences
    
- Camera paths
    
- Character animation events
    

---

# **59. Dialogue and Narrative Systems**

---

## **59.1 Dialogue Layout**

- Dialogue database (ScriptableObjects)
    
- Dialogue UI displayed via Canvas
    
- NPC interaction zones
    
- Next-line logic
    
- Branching dialogue
    

---

## **59.2 Branching Dialogue Example**

```csharp
public class DialogueLine
{
    public string text;
    public DialogueLine[] choices;
}
```

---

# **60. Save & Load Systems (Advanced)**

---

## **60.1 JSON + Encryption**

```csharp
string json = JsonUtility.ToJson(data);
string encrypted = Convert.ToBase64String(Encoding.UTF8.GetBytes(json));
```

---

## **60.2 Binary Saving**

Used for:

- Faster saving
    
- Larger data
    
- Encrypted data
    

---

## **60.3 Auto-Save Systems**

Trigger saves on:

- Completing quests
    
- Entering a new area
    
- After a combat encounter
    
- On quit
    

---

# **61. Audio – Advanced Techniques**

---

## **61.1 AudioLayers**

Use separate layers:

- Music
    
- SFX
    
- UI sounds
    
- Ambience
    

---

## **61.2 Crossfading Music**

```csharp
StartCoroutine(Crossfade(oldTrack, newTrack));
```

Used for:

- Entering dungeons
    
- Boss fights
    
- Calm → tension transitions
    

---

## **61.3 Environmental Reverb Zones**

Automatically change sound in:

- Caves
    
- Forests
    
- Cities
    
- Underwater
    

---

# **62. Multiplayer – Advanced Topics**

---

## **62.1 Client Prediction**

To smooth movement in multiplayer.

---

## **62.2 Lag Compensation**

Ensures hits register correctly based on player latency.

---

## **62.3 Network Object Spawning**

```csharp
var obj = Instantiate(prefab);
obj.GetComponent<NetworkObject>().Spawn();
```

---

# **63. Full Game Template Systems**

---

## **63.1 FPS Template**

- Gun system
    
- Ammo
    
- Recoil
    
- Crosshair
    
- Enemy AI
    
- Health system
    
- Footsteps
    
- Level streaming
    

---

## **63.2 RPG Template**

- Inventory
    
- Quests
    
- XP and leveling
    
- Stat modifiers
    
- Combat logic
    
- Dialogue system
    

---

## **63.3 Platformer Template**

- Coyote time
    
- Jump buffering
    
- Wall jumps
    
- Slopes
    
- Moving platforms
    
- Enemy patterns
    

---

# **64. Code Quality & Industry Practices**

---

## **64.1 Clean Code**

- Small scripts
    
- One responsibility per class
    
- Descriptive names
    
- Comments only when needed
    

---

## **64.2 Data-Driven Design**

Put data in ScriptableObjects, not hardcoded.

---

## **64.3 Avoid Hard Dependencies**

Use events or interfaces.

---

## **64.4 Testability**

- Keep logic separate from MonoBehaviours
    
- Use pure C# classes for rules
    

---

# **65. Real-World Complete Systems (Fully Explained and Expandable)**

These sections cover **full, production-ready systems** used in professional Unity games.  
Each system includes purpose, architecture, example code, and expansion ideas.

---

# **65.1 Full Player Controller Architecture (Advanced & Modular)**

This is a **clean, scalable** structure used in FPS, RPG, action, survival, or open-world games.

---

## **65.1.1 Recommended Folder Structure**

```
Player/
  Movement/
  Combat/
  Animation/
  Inventory/
  Interaction/
  Data/
```

---

## **65.1.2 Core Player Script (Entry Point)**

```csharp
public class Player : MonoBehaviour
{
    public PlayerMovement movement;
    public PlayerCombat combat;
    public PlayerInventory inventory;
    public PlayerAnimation anim;
    public PlayerInteractor interactor;

    void Awake()
    {
        movement = GetComponent<PlayerMovement>();
        combat = GetComponent<PlayerCombat>();
        inventory = GetComponent<PlayerInventory>();
        anim = GetComponent<PlayerAnimation>();
        interactor = GetComponent<PlayerInteractor>();
    }
}
```

This organizes the player into **modules**, preventing giant “god scripts”.

---

# **65.2 Movement Module (FPS/TPS Hybrid)**

---

## **65.2.1 PlayerMovement Script**

```csharp
using UnityEngine;

[RequireComponent(typeof(CharacterController))]
public class PlayerMovement : MonoBehaviour
{
    CharacterController controller;

    public float speed = 6f;
    public float gravity = -9.81f;
    public float jumpHeight = 2f;

    Vector3 velocity;
    bool isGrounded;

    void Awake()
    {
        controller = GetComponent<CharacterController>();
    }

    void Update()
    {
        // Detect ground
        isGrounded = controller.isGrounded;
        if (isGrounded && velocity.y < 0)
            velocity.y = -2f;

        // Basic WASD movement
        float x = Input.GetAxis("Horizontal");
        float z = Input.GetAxis("Vertical");

        Vector3 move = transform.right * x + transform.forward * z;
        controller.Move(move * speed * Time.deltaTime);

        // Jump
        if (Input.GetButtonDown("Jump") && isGrounded)
            velocity.y = Mathf.Sqrt(jumpHeight * -2f * gravity);

        // Apply gravity
        velocity.y += gravity * Time.deltaTime;
        controller.Move(velocity * Time.deltaTime);
    }
}
```

---

## **65.2.2 Features Provided**

- Smooth FPS/TPS movement
    
- Jumping
    
- Gravity
    
- Ground snapping
    
- Air control
    

---

## **65.2.3 Expansion Ideas**

Add:

- Slope detection
    
- Sprinting
    
- Crouching
    
- Parkour / vaulting
    
- Wall running
    
- Swimming
    

---

# **65.3 Combat System (Melee + Ranged)**

---

## **65.3.1 Ranged Weapon Script**

```csharp
public class Gun : MonoBehaviour
{
    public float damage = 15f;
    public float range = 100f;
    public Camera cam;
    public ParticleSystem muzzleFlash;

    void Update()
    {
        if (Input.GetButtonDown("Fire1"))
            Shoot();
    }

    void Shoot()
    {
        muzzleFlash.Play();

        if (Physics.Raycast(cam.transform.position, cam.transform.forward, out RaycastHit hit, range))
        {
            if (hit.collider.TryGetComponent(out Health health))
                health.TakeDamage(damage);
        }
    }
}
```

---

## **65.3.2 Melee Weapon Script**

```csharp
public class Sword : MonoBehaviour
{
    public float damage = 25f;

    void OnTriggerEnter(Collider other)
    {
        if (other.TryGetComponent(out Health health))
            health.TakeDamage(damage);
    }
}
```

---

## **65.3.3 Health Component**

```csharp
public class Health : MonoBehaviour
{
    public float maxHealth = 100f;
    float current;

    void Awake()
    {
        current = maxHealth;
    }

    public void TakeDamage(float amount)
    {
        current -= amount;

        if (current <= 0)
            Die();
    }

    void Die()
    {
        Destroy(gameObject);
    }
}
```

---

# **65.4 Interaction System (Universal Interactor)**

A flexible interaction system used for:

- Doors
    
- Items
    
- NPCs
    
- Loot
    
- Switches
    
- Crafting tables
    

---

## **65.4.1 Interactable Interface**

```csharp
public interface IInteractable
{
    void Interact(Player player);
}
```

---

## **65.4.2 Player Interactor Script**

```csharp
public class PlayerInteractor : MonoBehaviour
{
    public float range = 3f;
    public Camera cam;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.E))
            TryInteract();
    }

    void TryInteract()
    {
        if (Physics.Raycast(cam.transform.position, cam.transform.forward,
            out RaycastHit hit, range))
        {
            if (hit.collider.TryGetComponent(out IInteractable interactable))
            {
                interactable.Interact(GetComponent<Player>());
            }
        }
    }
}
```

---

## **65.4.3 Example Interactable: Door**

```csharp
public class Door : MonoBehaviour, IInteractable
{
    public void Interact(Player player)
    {
        Debug.Log("Door opened!");
        // Insert animation logic here
    }
}
```

---

# **65.5 Inventory System — Scalable and Data-Driven**

---

## **65.5.1 Item Definition (ScriptableObject)**

```csharp
[CreateAssetMenu(menuName="Items/Item")]
public class ItemData : ScriptableObject
{
    public string itemName;
    public Sprite icon;
    public GameObject prefab;
}
```

---

## **65.5.2 PlayerInventory Script**

```csharp
using System.Collections.Generic;

public class PlayerInventory : MonoBehaviour
{
    public List<ItemData> items = new List<ItemData>();

    public void AddItem(ItemData item)
    {
        items.Add(item);
        Debug.Log("Picked up: " + item.itemName);
    }
}
```

---

## **65.5.3 Pickup Object Script**

```csharp
public class ItemPickup : MonoBehaviour, IInteractable
{
    public ItemData item;

    public void Interact(Player player)
    {
        player.inventory.AddItem(item);
        Destroy(gameObject);
    }
}
```

---

# **65.6 Dialogue System — Full, Branching, Expandable**

---

## **65.6.1 Dialogue Line Data (ScriptableObject)**

```csharp
[CreateAssetMenu(menuName="Dialogue/Line")]
public class DialogueLine : ScriptableObject
{
    public string text;
    public DialogueLine[] choices;
}
```

---

## **65.6.2 Dialogue Manager**

Manages conversation state.

```csharp
public class DialogueManager : MonoBehaviour
{
    public DialogueUI ui;
    DialogueLine current;

    public void StartDialogue(DialogueLine start)
    {
        current = start;
        ui.Display(start);
    }

    public void Choose(int index)
    {
        current = current.choices[index];
        ui.Display(current);
    }
}
```

---

## **65.6.3 Dialogue UI**

Renders dialogue text and choices.

```csharp
public class DialogueUI : MonoBehaviour
{
    public TMPro.TextMeshProUGUI textUI;
    public Transform buttonContainer;
    public GameObject buttonPrefab;

    public void Display(DialogueLine line)
    {
        textUI.text = line.text;

        foreach (Transform child in buttonContainer)
            Destroy(child.gameObject);

        for (int i = 0; i < line.choices.Length; i++)
        {
            int idx = i;
            GameObject button = Instantiate(buttonPrefab, buttonContainer);
            button.GetComponentInChildren<TMPro.TextMeshProUGUI>().text = line.choices[i].text;
            button.GetComponent<UnityEngine.UI.Button>().onClick.AddListener(() =>
            {
                FindObjectOfType<DialogueManager>().Choose(idx);
            });
        }
    }
}
```

---

# **65.7 Save System — Complete JSON Save/Load**

---

## **65.7.1 Save Data Structure**

```csharp
[System.Serializable]
public class SaveData
{
    public Vector3 playerPos;
    public float playerHealth;
    public List<string> inventory;
}
```

---

## **65.7.2 Save Manager**

```csharp
public static class SaveManager
{
    static string path => Application.persistentDataPath + "/save.json";

    public static void Save(SaveData data)
    {
        string json = JsonUtility.ToJson(data, true);
        File.WriteAllText(path, json);
    }

    public static SaveData Load()
    {
        if (!File.Exists(path))
            return null;

        string json = File.ReadAllText(path);
        return JsonUtility.FromJson<SaveData>(json);
    }
}
```

---

# **65.8 VFX System — Modular Effects**

---

## **65.8.1 Hit Effect Manager**

```csharp
public class VFXManager : MonoBehaviour
{
    public static VFXManager I;
    public GameObject hitEffect;

    void Awake() => I = this;

    public void PlayHitEffect(Vector3 pos)
    {
        GameObject fx = Instantiate(hitEffect, pos, Quaternion.identity);
        Destroy(fx, 2f);
    }
}
```

---

## **65.8.2 Calling VFX on Damage**

```csharp
VFXManager.I.PlayHitEffect(hit.point);
```

---

# **65.9 Audio Manager (Centralized System)**

---

```csharp
public class AudioManager : MonoBehaviour
{
    public static AudioManager I;

    public AudioSource music;
    public AudioSource sfx;

    void Awake() => I = this;

    public void PlaySFX(AudioClip clip)
    {
        sfx.PlayOneShot(clip);
    }

    public void PlayMusic(AudioClip track)
    {
        music.clip = track;
        music.Play();
    }
}
```

---

# **66. Rendering Techniques, Lighting Tricks, and Professional Visual Polish**

---

# **66.1 Advanced Lighting Techniques**

---

## **66.1.1 Baked vs Realtime vs Mixed Lighting (Professional Use Cases)**

### **Baked Lighting**

- Precomputed, no runtime cost
    
- Looks soft and natural
    
- Best for static scenes
    

Used in:

- Indoor levels
    
- Stylized games
    
- Large environments where performance matters
    

### **Realtime Lighting**

- Changes every frame
    
- Required for dynamic lights (flashlights, torches, spells)
    

Used in:

- FPS games
    
- Action combat
    
- Night/day cycles
    

### **Mixed Lighting**

- Static objects baked
    
- Dynamic objects receive realtime shadows
    

Used in:

- Survival games
    
- RPGs
    
- Semi-open worlds
    

---

## **66.1.2 Lightmapping Tips**

Best settings:

- Use **Directional Lightmaps** for outdoor scenes
    
- Use **Shadowmask** for mixed lighting
    
- Keep texel density consistent across rooms
    
- Set “Important lights” manually
    

---

## **66.1.3 Reflection Probes**

Reflection probes capture surrounding environment.

Used for:

- Shiny armor
    
- Wet floors
    
- Metal surfaces
    
- Glass reflections
    

Place them in:

- Hallways
    
- Rooms
    
- Areas with different lighting conditions
    

---

# **66.2 Post-Processing Stack (URP/HDRP/Built-in)**

---

## **66.2.1 Core Effects**

### **Bloom**

- Adds glow to bright areas
    
- Use for magical VFX, neon signs, sci-fi
    

### **Motion Blur**

- Makes movement smoother
    
- Good for fast-paced action
    

### **Vignette**

- Darkens edges
    
- Used for immersion or dramatic feel
    

### **Chromatic Aberration**

- Subtle lens distortion
    
- Don't overuse
    

### **Color Grading**

- Most important effect
    
- Defines the style of your entire game
    

---

## **66.2.2 Creating a Post-Processing Volume**

URP example:

- Add **Global Volume**
    
- Add **Bloom** component
    
- Add **Color Adjustments**
    

In code:

```csharp
volume.profile.TryGet(out ColorAdjustments adjust);
adjust.postExposure.value = 0.8f;
```

---

# **66.3 Shader Effects (Professional-Level Examples)**

---

## **66.3.1 Outline Shader (Shader Graph)**

Nodes involved:

- Fresnel
    
- Multiply
    
- Add emission
    
- Color
    

Used for:

- Item highlighting
    
- Enemy detection
    
- Interactable outlines
    

---

## **66.3.2 Dissolve Shader**

Used for:

- Enemy death effects
    
- Teleportation
    
- Disappearing walls
    
- Phase transitions
    

Core idea:

- Use a noise texture
    
- Compare noise value with a threshold
    

Shader Graph logic:

```
NoiseTexture → Sample  
Time → Add  
Compare → Lerp Emission
```

---

## **66.3.3 Hologram Shader**

Features:

- Scrolling UV
    
- Blue glow
    
- Fresnel ring
    
- Scanline effect
    

Used for:

- Sci-fi UI
    
- Robot projections
    
- Quest indicators
    

---

# **67. UI Systems — Complete Architecture**

---

# **67.1 UI Types in Unity**

- **Canvas UI** (RectTransform-based)
    
- **World-Space UI** (floating UI in gameplay world)
    
- **UI Toolkit** (Editor-like UI system)
    

Most games combine:

- Canvas for menus
    
- World-space UI for health bars
    

---

# **67.2 Canvas Setup for Multi-Resolution Games**

Use **Canvas Scaler**:

- UI Scale Mode → Scale with Screen Size
    
- Reference Resolution:
    
    ```
    1920 × 1080
    ```
    
- Match = 0.5 (balanced)
    

---

# **67.3 UI Manager Pattern**

Recommended structure:

```csharp
public class UIManager : MonoBehaviour
{
    public GameObject inventoryUI;
    public GameObject pauseMenu;

    public void ToggleInventory()
    {
        inventoryUI.SetActive(!inventoryUI.activeSelf);
    }

    public void TogglePauseMenu()
    {
        pauseMenu.SetActive(!pauseMenu.activeSelf);
    }
}
```

---

# **67.4 World-Space UI (Health Bars, Names, Damage Indicators)**

Example: Floating health bar

```csharp
public class Billboard : MonoBehaviour
{
    void LateUpdate()
    {
        transform.LookAt(Camera.main.transform);
    }
}
```

Attach this to:

- Enemy health bar
    
- NPC name tags
    
- Quest markers
    

---

# **67.5 TextMeshPro (Required for Modern UI)**

Always prefer TMP over default Text.

TMP Benefits:

- Sharper text
    
- Rich text tags
    
- GPU-friendly
    

---

# **67.6 UI Animation Methods**

### **Using Animator**

- UI fades
    
- Scale punch effects
    
- Reward screens
    

### **Using DOTween** (best approach)

```csharp
panel.DOFade(1f, 0.5f);
button.transform.DOScale(1.2f, 0.2f).SetLoops(2, LoopType.Yoyo);
```

(If DOTween is not used, Unity's LeanTween or Animations are alternatives.)

---

# **68. Advanced Performance Optimization**

---

# **68.1 CPU Optimizations**

---

## **68.1.1 Avoid “Update Hell”**

Bad:

```csharp
void Update()  
{
    DoThing();
}
```

Better approaches:

- Manager updates multiple objects
    
- Event-driven updates
    
- Coroutines
    
- InvokeRepeating
    
- Fixed update intervals
    

---

## **68.1.2 Cache Component References**

Bad:

```csharp
GetComponent<Rigidbody>().AddForce(...);
```

Good:

```csharp
rb = GetComponent<Rigidbody>();
rb.AddForce(...);
```

---

## **68.1.3 Use Object Pooling for Frequent Objects**

Avoid Instantiate/Destroy loops.

---

# **68.2 GPU Optimizations**

---

## **68.2.1 Reduce Overdraw**

Avoid:

- Excess transparency
    
- Particles overlapping
    
- Big UI canvases
    

---

## **68.2.2 Use SRP Batcher (URP/HDRP)**

In URP:

- Enable “SRP Batcher” in Project Settings
    

Improves draw call batching.

---

## **68.2.3 Reduce Real-Time Lights**

Lights are expensive.  
Use:

- Baked lighting
    
- Light probes
    
- Reflection probes
    

---

# **68.3 Memory Optimizations**

- Compress textures
    
- Use Addressables for large assets
    
- Unload unused assets:
    

```csharp
Resources.UnloadUnusedAssets();
```

- Avoid storing huge lists in memory
    
- Pool objects
    

---

# **69. Game Templates — Complete Systems**

---

# **69.1 First-Person Shooter Template (Full Breakdown)**

### Systems included:

- Player Controller
    
- Gun System
    
- Damage System
    
- Enemy AI
    
- Hit Effects
    
- Inventory
    
- Ammo & Reloading
    
- Sway & Recoil
    
- Crosshair System
    

---

# **69.2 RPG Template**

Components:

- Player movement & controller
    
- Quest manager
    
- Dialogue system
    
- Inventory
    
- Stats & attributes
    
- Enemy AI
    
- Turn-based or action combat
    

---

# **69.3 Platformer Template**

Mechanics:

- Coyote time
    
- Jump buffering
    
- Variable jump
    
- Enemy patterns
    
- Moving platforms
    
- Checkpoint system
    

---

# **69.4 Survival / Open-World Template**

Features:

- Hunger / thirst
    
- Day-night cycle
    
- Crafting System
    
- Resource nodes
    
- Procedural generation
    
- Weather
    
- Animals / AI
    
- Save system
    
- Base building
    

---

# **70. Advanced Shading & VFX Techniques**

---

# **70.1 Screen-Space Effects**

Examples:

- SSAO
    
- SSR
    
- Screen Space Reflections
    
- Fullscreen distortion
    

Used for water, portals, etc.

---

# **70.2 Special Effects Patterns**

### **Energy Shield Hit Effect**

- Mesh-based distortion
    
- Temporary glow
    
- Fresnel shader
    

### **Teleportation**

- Dissolve out
    
- Move
    
- Dissolve in
    

### **Hologram NPC Dialogue**

- Scanning lines
    
- Noise-based distortion
    
- Glow
    

---

# **71. Full Production Workflow**

---

## **71.1 Pre-production**

- Game design document
    
- Gameplay prototype
    
- Concept art
    
- Technical prototypes
    

---

## **71.2 Production**

- Systems coding
    
- Art pipeline
    
- Animation pipeline
    
- Scene building
    
- Level design
    
- Audio integration
    
- Playtesting
    
- Optimization
    

---

## **71.3 Post-production**

- Polishing
    
- Bug fixing
    
- Optimization passes
    
- Platform building
    
- QA testing
    

---

## **71.4 Publishing**

- Build for platform
    
- Player settings
    
- Quality settings
    
- Store metadata
    
- Upload builds
    
- Patch updates
    

---

# **72. Industry-Level Code Practices**

---

## **72.1 Avoid Monolithic Scripts**

Split functionality into systems.

---

## **72.2 Use ScriptableObjects for Data**

- Weapon stats
    
- Enemy stats
    
- Dialogue
    
- Skill trees
    
- Level settings
    

---

## **72.3 Modular Architecture Patterns**

- Event-driven
    
- ECS (when scaling)
    
- Manager pattern
    
- Service locator
    
- Dependency injection
    

---

# **73. FULL WORKING GAME SYSTEMS — COMPLETE, EXPANDABLE, PRODUCTION-LEVEL IMPLEMENTATIONS**

The following sections are **full game-ready systems**—not demos, not partials.  
These are clean, modular, reusable Unity C# architectures designed to be copied, modified, and extended into complete games.

Everything is Unity-specific C#, built using:

- MonoBehaviours
    
- ScriptableObjects
    
- Coroutines
    
- UnityEvents
    
- Unity Physics
    
- NavMesh
    
- UI
    
- Animation
    
- Prefabs
    
- Addressables (when needed)
    

---

# **73.1 COMPLETE FIRST PERSON SYSTEM (FPS CONTROLLER + CAMERA + WEAPON SYSTEM)**

This is a **full FPS setup** used in:

- Shooters
    
- Horror games
    
- Survival games
    
- Adventure games
    

---

# **73.1.1 Folder Structure**

```
FPS/
  Player/
    Player.cs
    PlayerMovement.cs
    PlayerLook.cs
    PlayerHealth.cs
  Weapons/
    Gun.cs
    WeaponData.cs
  Camera/
    PlayerCamera.cs
  Effects/
    MuzzleFlash.prefab
    HitEffect.prefab
  UI/
    Crosshair.cs
```

---

# **73.1.2 Player Movement (CharacterController-based)**

```csharp
[RequireComponent(typeof(CharacterController))]
public class PlayerMovement : MonoBehaviour
{
    CharacterController controller;

    public float speed = 6f;
    public float gravity = -9.81f;
    public float jumpHeight = 2f;

    Vector3 velocity;
    bool isGrounded;

    void Awake()
    {
        controller = GetComponent<CharacterController>();
    }

    void Update()
    {
        isGrounded = controller.isGrounded;

        if (isGrounded && velocity.y < 0)
            velocity.y = -2f;

        float x = Input.GetAxisRaw("Horizontal");
        float z = Input.GetAxisRaw("Vertical");

        Vector3 move = transform.right * x + transform.forward * z;
        controller.Move(move * speed * Time.deltaTime);

        if (Input.GetButtonDown("Jump") && isGrounded)
            velocity.y = Mathf.Sqrt(jumpHeight * -2f * gravity);

        velocity.y += gravity * Time.deltaTime;
        controller.Move(velocity * Time.deltaTime);
    }
}
```

---

# **73.1.3 Player Camera (Mouse Look System)**

```csharp
public class PlayerLook : MonoBehaviour
{
    public float sensitivity = 250f;
    public Transform body;

    float xRotation;

    void Update()
    {
        float mouseX = Input.GetAxis("Mouse X") * sensitivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * sensitivity * Time.deltaTime;

        xRotation -= mouseY;
        xRotation = Mathf.Clamp(xRotation, -80f, 80f);

        transform.localRotation = Quaternion.Euler(xRotation, 0, 0);
        body.Rotate(Vector3.up * mouseX);
    }
}
```

---

# **73.1.4 Weapon Data (ScriptableObject)**

```csharp
[CreateAssetMenu(menuName = "FPS/Weapon Data")]
public class WeaponData : ScriptableObject
{
    public string weaponName;
    public float damage;
    public float fireRate;
    public float range;
    public AudioClip shotSound;
    public GameObject projectilePrefab;
}
```

---

# **73.1.5 Gun Logic (Hitscan Shooting)**

```csharp
public class Gun : MonoBehaviour
{
    public WeaponData data;
    public Camera cam;
    public ParticleSystem muzzleFlash;

    float nextTimeToFire;

    void Update()
    {
        if (Input.GetButton("Fire1") && Time.time >= nextTimeToFire)
        {
            nextTimeToFire = Time.time + 1f / data.fireRate;
            Shoot();
        }
    }

    void Shoot()
    {
        muzzleFlash.Play();
        AudioManager.I.PlaySFX(data.shotSound);

        if (Physics.Raycast(cam.transform.position, cam.transform.forward, out RaycastHit hit, data.range))
        {
            if (hit.collider.TryGetComponent(out Health health))
                health.TakeDamage(data.damage);

            VFXManager.I.PlayHitEffect(hit.point);
        }
    }
}
```

---

# **73.1.6 Player Health**

```csharp
public class PlayerHealth : MonoBehaviour
{
    public float maxHealth = 100;
    float current;

    void Awake() => current = maxHealth;

    public void TakeDamage(float amount)
    {
        current -= amount;
        if (current <= 0) Die();
    }

    void Die()
    {
        Debug.Log("Player Dead");
    }
}
```

---

# **73.1.7 Enemy AI (Simple Chase + Attack FSM)**

```csharp
using UnityEngine.AI;

public class EnemyAI : MonoBehaviour
{
    public float attackDistance = 2f;
    public float damage = 10f;

    NavMeshAgent agent;
    Transform player;

    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
        player = GameObject.FindWithTag("Player").transform;
    }

    void Update()
    {
        agent.SetDestination(player.position);

        if (Vector3.Distance(transform.position, player.position) < attackDistance)
        {
            player.GetComponent<PlayerHealth>()?.TakeDamage(damage);
        }
    }
}
```

---

# **73.1.8 Crosshair UI System**

```csharp
public class Crosshair : MonoBehaviour
{
    public RectTransform crosshair;

    void Update()
    {
        crosshair.localScale = Vector3.one * (1f + Mathf.Abs(Input.GetAxis("Mouse X") + Input.GetAxis("Mouse Y")) * 0.1f);
    }
}
```

---

# **74. SURVIVAL GAME SYSTEM (Crafting + Hunger + Thirst + Day/Night)**

A survival game requires:

- Stats
    
- Time system
    
- Crafting
    
- Inventory
    
- Interactable environment
    
- UI
    

---

# **74.1 Player Stats: Hunger, Thirst, Energy**

```csharp
public class SurvivalStats : MonoBehaviour
{
    public float hunger = 100f;
    public float thirst = 100f;
    public float energy = 100f;

    void Update()
    {
        hunger -= 0.1f * Time.deltaTime;
        thirst -= 0.15f * Time.deltaTime;
        energy -= 0.05f * Time.deltaTime;

        if (hunger <= 0 || thirst <= 0)
            GetComponent<PlayerHealth>().TakeDamage(5 * Time.deltaTime);
    }
}
```

---

# **74.2 Day/Night Cycle**

```csharp
public class DayNightCycle : MonoBehaviour
{
    public float dayLength = 120f;  // seconds
    float rotationSpeed;

    void Start()
    {
        rotationSpeed = 360f / dayLength;
    }

    void Update()
    {
        transform.Rotate(Vector3.right * rotationSpeed * Time.deltaTime);
    }
}
```

---

# **74.3 Crafting System (ScriptableObject Recipes)**

### **Recipe Data**

```csharp
[CreateAssetMenu(menuName = "Survival/Crafting Recipe")]
public class CraftingRecipe : ScriptableObject
{
    public ItemData[] ingredients;
    public ItemData result;
}
```

---

### **Crafting Manager**

```csharp
public class CraftingManager : MonoBehaviour
{
    public List<CraftingRecipe> recipes;

    public ItemData TryCraft(List<ItemData> inventory)
    {
        foreach (var recipe in recipes)
        {
            if (recipe.ingredients.All(i => inventory.Contains(i)))
            {
                foreach (var item in recipe.ingredients)
                    inventory.Remove(item);

                return recipe.result;
            }
        }
        return null;
    }
}
```

---

# **74.4 Resource Nodes (Trees, Rocks, Plants)**

```csharp
public class ResourceNode : MonoBehaviour, IInteractable
{
    public ItemData drop;

    public void Interact(Player player)
    {
        player.inventory.AddItem(drop);
        Destroy(gameObject);
    }
}
```

---

# **75. RPG GAME SYSTEM (Stats + Skills + Quests + Dialogue + Items)**

---

# **75.1 Character Stats (ScriptableObject + Runtime Copy)**

### **Stat Template**

```csharp
[CreateAssetMenu(menuName="RPG/Stats")]
public class CharacterStats : ScriptableObject
{
    public int strength;
    public int agility;
    public int intelligence;
    public int health;
}
```

---

### **Runtime Stats System**

```csharp
public class StatsRuntime : MonoBehaviour
{
    public CharacterStats baseStats;

    public int strength;
    public int agility;
    public int intelligence;
    public int health;

    void Awake()
    {
        strength = baseStats.strength;
        agility = baseStats.agility;
        intelligence = baseStats.intelligence;
        health = baseStats.health;
    }
}
```

---

# **75.2 Skill System**

```csharp
[CreateAssetMenu(menuName="RPG/Skill")]
public class Skill : ScriptableObject
{
    public string skillName;
    public int manaCost;
    public int damage;
}
```

---

### Skill Usage

```csharp
public void UseSkill(Skill skill)
{
    if (mana < skill.manaCost) return;

    mana -= skill.manaCost;
    enemy.TakeDamage(skill.damage);
}
```

---

# **75.3 Quest System (Simple & Expandable)**

### Quest Data

```csharp
[CreateAssetMenu(menuName="RPG/Quest")]
public class Quest : ScriptableObject
{
    public string title;
    public string description;
    public ItemData reward;
}
```

---

### Quest Manager

```csharp
public class QuestManager : MonoBehaviour
{
    public List<Quest> activeQuests;

    public void AddQuest(Quest quest)
    {
        activeQuests.Add(quest);
    }

    public void CompleteQuest(Quest quest)
    {
        activeQuests.Remove(quest);
        // Give reward
    }
}
```

---

# **76. ADVANCED CAMERA RIGS (FPS, TPS, Platformer, Top-Down)**

---

## **76.1 Third-Person Camera (Orbit Camera)**

```csharp
public class OrbitCamera : MonoBehaviour
{
    public Transform target;
    public float distance = 5f;
    public float sensitivity = 120f;

    float yaw;
    float pitch;

    void LateUpdate()
    {
        yaw += Input.GetAxis("Mouse X") * sensitivity * Time.deltaTime;
        pitch -= Input.GetAxis("Mouse Y") * sensitivity * Time.deltaTime;

        pitch = Mathf.Clamp(pitch, -30f, 60f);

        Vector3 direction = new Vector3(0, 0, -distance);
        Quaternion rotation = Quaternion.Euler(pitch, yaw, 0);

        transform.position = target.position + rotation * direction;
        transform.LookAt(target);
    }
}
```

---

# **77. EXTENDED AI SYSTEMS (PATROL, COVER, COMBAT, SQUAD AI)**

---

# **77.1 Patrol System**

```csharp
public class PatrolAI : MonoBehaviour
{
    public Transform[] points;
    int index;
    NavMeshAgent agent;

    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
        agent.SetDestination(points[index].position);
    }

    void Update()
    {
        if (!agent.pathPending && agent.remainingDistance < 0.5f)
        {
            index = (index + 1) % points.Length;
            agent.SetDestination(points[index].position);
        }
    }
}
```

---

# **77.2 Cover System (Take Cover Automatically)**

### Detect Cover Points

```csharp
public class CoverPoint : MonoBehaviour {}
```

### Enemy Finds Nearest Cover

```csharp
public class TakeCoverAI : MonoBehaviour
{
    NavMeshAgent agent;

    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
    }

    public void MoveToCover()
    {
        CoverPoint[] covers = FindObjectsOfType<CoverPoint>();
        Transform best = covers.OrderBy(c => Vector3.Distance(transform.position, c.transform.position)).First().transform;

        agent.SetDestination(best.position);
    }
}
```

---

# **78. EDITOR TOOLS (CUSTOM WINDOWS, AUTOMATION, PROCEDURAL GENERATORS)**

---

# **78.1 Custom Editor Window Example**

```csharp
using UnityEditor;
using UnityEngine;

public class LevelTool : EditorWindow
{
    [MenuItem("Tools/Level Tool")]
    public static void ShowWindow()
    {
        GetWindow<LevelTool>("Level Tool");
    }

    void OnGUI()
    {
        if (GUILayout.Button("Spawn Trees"))
        {
            foreach (GameObject obj in Selection.gameObjects)
                Instantiate(Resources.Load<GameObject>("Tree"), obj.transform.position, Quaternion.identity);
        }
    }
}
```

---

# **78.2 Gizmos to Visualize Systems**

```csharp
void OnDrawGizmos()
{
    Gizmos.color = Color.yellow;
    Gizmos.DrawWireSphere(transform.position, 5f);
}
```

---

# **79. NETWORKING (SINGLE-PLAYER, CO-OP, MULTIPLAYER, SERVER AUTH, LOBBIES, SYNCING, RPCs)**

This section covers **Unity-specific C# networking systems** using:

- **Unity Netcode for GameObjects (NGO)**
    
- **Unity Transport**
    
- **Server Authoritative design**
    
- **NetworkVariables**
    
- **RPCs**
    
- **Player spawning**
    
- **Object ownership**
    
- **Sync transforms**
    
- **Hit detection in multiplayer**
    
- **Multiplayer lobbies**
    
- **Matchmaking logic**
    

This is **not** general networking theory.  
Everything here is **Unity C# only**, fully practical.

---

# **79.1 Multiplayer Concepts You MUST Understand**

---

## **79.1.1 Client vs Server**

Unity NGO supports 3 modes:

- **Host** = client + server in one player
    
- **Client** = connects to server
    
- **Dedicated Server** = no graphics
    

Most indie devs use Host mode during development.

---

## **79.1.2 Authoritative vs Non-Authoritative**

### **Authoritative Server**

The server decides:

- Player positions
    
- Health
    
- Damage
    
- Shooting
    
- Movement validation
    

Clients only _request_ actions.

This prevents:

- Speed hacks
    
- Fly hacks
    
- Aimbots (partially)
    
- Damage manipulation
    

---

### **Non-Authoritative**

Clients control everything.

Good for:

- Co-op
    
- LAN games
    
- Casual multiplayer
    

Not good for PvP.

---

# **79.2 Setting Up Netcode (NGO)**

---

## **79.2.1 NetworkManager in Scene**

1. Create GameObject: **NetworkManager**
    
2. Add component: **NetworkManager**
    
3. Add **Unity Transport**
    
4. Create Prefab for Player with:
    
    - NetworkObject
        
    - Player scripts
        
5. Assign Player prefab to:
    

```
NetworkManager → Player Prefab
```

---

## **79.2.2 Starting the Network**

Add a script to UI buttons:

```csharp
using Unity.Netcode;
using UnityEngine;

public class StartupNetwork : MonoBehaviour
{
    public void StartHost()
    {
        NetworkManager.Singleton.StartHost();
    }

    public void StartClient()
    {
        NetworkManager.Singleton.StartClient();
    }

    public void StartServer()
    {
        NetworkManager.Singleton.StartServer();
    }
}
```

---

# **79.3 Spawning Multiplayer Players**

Unity spawns players automatically when:

```
Player Prefab is assigned in NetworkManager
```

Player must have:

```
NetworkObject
```

Example script:

```csharp
public class PlayerNetwork : NetworkBehaviour
{
    public override void OnNetworkSpawn()
    {
        if (IsOwner)
            Debug.Log("This is *my* player.");
    }
}
```

---

# **79.4 NetworkVariable — Syncing Data**

NetworkVariables sync automatically from server → client.

Example:

```csharp
using Unity.Netcode;

public class PlayerStats : NetworkBehaviour
{
    public NetworkVariable<float> health =
        new NetworkVariable<float>(100f, 
        NetworkVariableReadPermission.Everyone,
        NetworkVariableWritePermission.Server);

    [ServerRpc]
    public void DamageServerRpc(float amount)
    {
        health.Value -= amount;
        if (health.Value <= 0)
            Die();
    }

    void Die()
    {
        GetComponent<NetworkObject>().Despawn();
    }
}
```

---

# **79.5 RPCs: ClientRpc and ServerRpc**

---

## **79.5.1 ServerRpc**

Executed **on the server**.

Used for:

- Apply damage
    
- Request pickup
    
- Request movement action
    
- Join a match
    

Example:

```csharp
[ServerRpc]
void FireServerRpc()
{
    Debug.Log("Server processed shooting request");
}
```

---

## **79.5.2 ClientRpc**

Executed **on all clients** (except or including sender)

Used for:

- Visual effects
    
- UI notifications
    
- Playing sounds
    
- Hit markers
    

Example:

```csharp
[ClientRpc]
void PlayShootFXClientRpc()
{
    muzzleFlash.Play();
}
```

---

# **79.6 Full Multiplayer Shooting System**

---

# **79.6.1 Hit Detection (Server-Side)**

Client requests shooting → Server validates → Server applies damage

```csharp
public class GunNetwork : NetworkBehaviour
{
    public Camera cam;

    void Update()
    {
        if (!IsOwner) return;

        if (Input.GetButtonDown("Fire1"))
            RequestShootServerRpc(cam.transform.position, cam.transform.forward);
    }

    [ServerRpc]
    void RequestShootServerRpc(Vector3 origin, Vector3 direction)
    {
        if (Physics.Raycast(origin, direction, out RaycastHit hit, 100f))
        {
            if (hit.collider.TryGetComponent(out PlayerStats targetStats))
                targetStats.DamageServerRpc(20f);

            PlayShootFXClientRpc(hit.point);
        }
    }

    [ClientRpc]
    void PlayShootFXClientRpc(Vector3 hitPoint)
    {
        VFXManager.I.PlayHitEffect(hitPoint);
    }
}
```

---

## **79.6.2 Anti-Cheat Notes**

Server controls:

- Damage
    
- Position
    
- Fire rate
    
- Hit detection
    

Clients cannot:

- Increase fire rate
    
- Edit damage
    
- Teleport
    
- Modify health
    

---

# **79.7 Syncing Player Movement**

Unity NGO includes:

- **NetworkTransform**
    
- **NetworkRigidbody**
    

### Recommended:

- Use **NetworkTransform** for normal movement
    
- Use **NetworkRigidbody** for physics characters
    

Example:

```csharp
[RequireComponent(typeof(NetworkTransform))]
public class PlayerMovementNet : NetworkBehaviour
{
    public float speed = 5f;

    void Update()
    {
        if (!IsOwner) return;

        float x = Input.GetAxis("Horizontal");
        float z = Input.GetAxis("Vertical");

        transform.position += (transform.right * x + transform.forward * z) * speed * Time.deltaTime;
    }
}
```

---

# **79.8 Multiplayer Interactions (Pickups, Doors, Items)**

---

## **79.8.1 Item Pickup**

```csharp
public class NetworkItem : NetworkBehaviour, IInteractable
{
    [ServerRpc(RequireOwnership = false)]
    public void PickupServerRpc(ulong playerId)
    {
        PlayerInventory inv = NetworkManager.Singleton.ConnectedClients[playerId]
            .PlayerObject.GetComponent<PlayerInventory>();

        inv.AddItem(itemData);
        GetComponent<NetworkObject>().Despawn();
    }

    public void Interact(Player player)
    {
        PickupServerRpc(player.OwnerClientId);
    }
}
```

---

# **79.9 Multiplayer UI — Syncing Data**

UI runs **only on local client**.

UI listens to NetworkVariable changes:

```csharp
void Start()
{
    stats.health.OnValueChanged += OnHealthChanged;
}

void OnHealthChanged(float oldValue, float newValue)
{
    healthBar.fillAmount = newValue / stats.maxHealth;
}
```

---

# **79.10 Multiplayer Lobbies & Matchmaking**

Unity has:

- **Unity Lobby**
    
- **Relay**
    
- **Vivox (Voice)**
    

Core steps:

1. Create lobby
    
2. Wait for players
    
3. Create relay allocation
    
4. Send join code to clients
    
5. Start game scene
    

---

# **80. Addressables System (Streaming, Performance, Dynamic Loading)**

This is essential for:

- Open world games
    
- Mobile games
    
- Online games
    
- Procedural maps
    
- Large assets
    
- Modular weapons
    
- Cosmetics
    

---

# **80.1 Converting Prefabs to Addressables**

Right-click asset →

```
Addressables → Convert to Addressable
```

---

## **80.2 Loading Addressables by Code**

```csharp
using UnityEngine.AddressableAssets;
using UnityEngine.ResourceManagement.AsyncOperations;

public class Loader : MonoBehaviour
{
    public string key;

    void Start()
    {
        Addressables.LoadAssetAsync<GameObject>(key).Completed += HandleLoad;
    }

    void HandleLoad(AsyncOperationHandle<GameObject> obj)
    {
        Instantiate(obj.Result);
    }
}
```

---

## **80.3 Unloading**

```csharp
Addressables.Release(obj);
```

---

# **80.4 Runtime Streaming**

Used for:

- Large worlds
    
- MMO-style zones
    
- Procedural levels
    

Example: Load a chunk when player enters trigger.

```csharp
public class ZoneLoader : MonoBehaviour
{
    public string zoneKey;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
            Addressables.InstantiateAsync(zoneKey);
    }
}
```

---

# **81. ECS / DOTS (Entity Component System)**

For massive performance requirements:

- Thousands of enemies
    
- Massive projectiles
    
- Complex simulations
    
- Large open worlds
    

---

# **81.1 ECS Concepts**

|Old Unity (OOP)|ECS (DOTS)|
|---|---|
|GameObject|Entity|
|MonoBehaviour|Component|
|Update()|System|
|Per-object code|Burst optimized SIMD|

---

# **81.2 Component Example (Pure DOTS)**

```csharp
public struct MoveSpeed : IComponentData
{
    public float value;
}
```

---

# **81.3 System Example**

```csharp
partial struct MovementSystem : ISystem
{
    public void OnUpdate(ref SystemState state)
    {
        foreach (var (speed, transform) in 
            SystemAPI.Query<RefRW<MoveSpeed>, RefRW<LocalTransform>>())
        {
            transform.ValueRW.Position.x += speed.ValueRW.value * SystemAPI.Time.DeltaTime;
        }
    }
}
```

---

# **81.4 When to Use DOTS**

Use ECS ONLY if:

- You need 10,000+ entities
    
- Need max CPU performance
    
- Systems are simple but high volume
    
- Game is simulation-heavy
    

Avoid ECS if:

- Your game is small
    
- You are new to Unity
    
- You need MonoBehaviour features
    
- You rely on asset store packages
    

---

# **82. ADVANCED SHADERS & VFX (BUILT-IN PIPELINE, URP, HDRP, SHADER GRAPH)**

This section teaches **Unity-specific shader programming and VFX systems** used in real games.  
Everything is written clean, clearly structured, and tied directly to Unity’s C# + rendering pipeline.

The focus:

- Shader Graph (URP + HDRP)
    
- HLSL Shader code (Built-in)
    
- VFX Graph
    
- Full production-level VFX systems
    
- Practical examples: outlines, holograms, portals, dissolves, fire, water, forcefields
    

---

# **82.1 SHADER GRAPH — PROFESSIONAL WORKFLOWS**

---

# **82.1.1 Shader Graph Basics**

Unity Shader Graph lets you create shaders visually.  
Nodes → Compile → Generate GPU shader.

Core node groups:

- **Math** (Add, Multiply, Sine, Lerp)
    
- **Procedural** (Noise, Voronoi)
    
- **Fresnel**
    
- **UV nodes** (Tiling/Offset)
    
- **Time**
    
- **Texture Sampling**
    

---

# **82.1.2 Required Pipeline Settings**

You must enable:

```
URP/HDRP → Quality → Allow Shader Graph
URP/HDRP → Render Pipeline Asset → Enable Depth Texture
URP/HDRP → Enable Opaque Texture
```

Depth texture = allows outlines, blur, fog  
Opaque texture = allows screen-space effects

---

# **82.2 OUTLINE SHADER (Shader Graph)**

---

# **82.2.1 What This Shader Does**

- Adds an outline around objects
    
- Works for item highlighting
    
- Works for enemy detection
    
- Can be animated, colorized, pulsed
    

---

# **82.2.2 Shader Graph Setup**

Nodes needed:

- **Normal Vector**
    
- **View Direction**
    
- **Fresnel Effect**
    
- **Multiply**
    
- **Emission**
    

Formula:

```
Outline = Fresnel(outlineStrength)
FinalColor = BaseColor + Outline * OutlineColor
```

---

## **82.2.3 Common Issues**

If outline doesn't show:

- Object must be opaque
    
- Emission must be enabled
    
- Ensure no post-processing clamps brightness
    

---

# **82.3 DISSOLVE SHADER (Shader Graph)**

---

# **82.3.1 Purpose**

Used for:

- Enemy death animation
    
- Teleportation
    
- Fade out objects
    
- Magic effects
    
- Doors fading open
    
- Summoning / despawning
    

---

## **82.3.2 Dissolve Core Logic**

1. Sample a **Noise Texture**
    
2. Compare noise to **DissolveAmount** slider
    
3. If Noise < Amount → show
    
4. If Noise > Amount → hide
    
5. Add edge emission
    

Pseudo:

```
float n = noiseTexture(UV)
clip(n - dissolveAmount)
emission = step(n, dissolveAmount + edgeWidth)
```

---

## **82.3.3 Unity Shader Graph Implementation**

Nodes:

- Texture 2D Asset (Noise)
    
- Sample Texture 2D
    
- Tiling/Offset
    
- Subtract (Noise – DissolveAmount)
    
- **Clip** node
    
- Edge emission:
    
    ```
    Smoothstep(DissolveAmount, DissolveAmount + EdgeThickness, Noise)
    ```
    
- Add Emission Strength
    

---

# **82.3.4 Material Control Script**

```csharp
public class DissolveController : MonoBehaviour
{
    Material mat;
    public float speed = 1f;
    float amount = 0f;

    void Start()
    {
        mat = GetComponent<Renderer>().material;
    }

    void Update()
    {
        amount += Time.deltaTime * speed;
        mat.SetFloat("_DissolveAmount", amount);
    }
}
```

---

# **82.4 HOLOGRAM SHADER (URP/HDRP)**

---

# **82.4.1 Visual Features**

- Scrolling noise
    
- Glow edges
    
- Transparent interior
    
- Flicker effect
    
- Scanlines
    

Used in:

- Sci-fi NPC projections
    
- Quest points
    
- Cameras and drones
    
- Terminals and displays
    

---

## **82.4.2 Shader Graph Node Breakdown**

Nodes:

- **Simple Noise** → Distortion
    
- **Time** → Panner
    
- **Fresnel** → Blue glow
    
- **Multiply** → Control intensity
    
- **Alpha** → Increase transparency
    

Workflow:

```
BaseColor → Multiply(Fresnel * GlowStrength)
Alpha = Noise + Flicker
```

---

# **82.5 PORTAL SHADER (RENDER TEXTURE-BASED)**

This effect creates a “portal window” into another world.

---

# **82.5.1 Requirements**

- Camera that renders only the other world
    
- RenderTexture
    
- Plane with a custom shader
    

---

## **82.5.2 Portal Setup Script**

```csharp
public class PortalView : MonoBehaviour
{
    public Camera portalCam;
    public Transform playerCam;
    public Transform portal;
    public Transform linkedPortal;

    void LateUpdate()
    {
        Vector3 relativePos = portal.InverseTransformPoint(playerCam.position);
        Vector3 newPos = linkedPortal.TransformPoint(relativePos);
        portalCam.transform.position = newPos;

        Quaternion difference = linkedPortal.rotation * Quaternion.Inverse(portal.rotation);
        portalCam.transform.rotation = difference * playerCam.rotation;
    }
}
```

---

# **82.5.3 Portal Shader (Shader Graph)**

Use:

- **Sample Texture 2D**
    
- Plug RenderTexture into shader
    
- No lighting
    
- Transparent edges if needed
    

---

# **82.6 FORCEFIELD SHADER (ENERGY SHIELD)**

---

# **82.6.1 Visual Features**

- Ripple effect
    
- Impact point pulse
    
- Fresnel glow
    
- Distortion
    
- UV movement
    

Used for:

- Enemy shields
    
- Player shields
    
- Sci-fi force barriers
    
- Magic domes
    

---

# **82.6.2 Impact Shader Logic**

When hit → send hit position → shader draws ripple.

```csharp
public class ShieldHitFX : MonoBehaviour
{
    Material mat;
    Vector4 point;

    void Start()
    {
        mat = GetComponent<Renderer>().material;
    }

    public void Hit(Vector3 pos)
    {
        point = transform.InverseTransformPoint(pos);
        mat.SetVector("_HitPosition", point);
        mat.SetFloat("_HitTime", Time.time);
    }
}
```

Shader Graph uses:

- **Distance** node
    
- **Time - HitTime**
    
- **Smoothstep**
    
- **Sine**
    

---

# **82.7 FIRE & SMOKE VFX (PARTICLE SYSTEM)**

---

# **82.7.1 Fire Setup**

Use particle systems:

- Main flame
    
- Sparks
    
- Smoke
    
- Glow planes
    

Settings:

```
Start Lifetime: 0.4 – 1.2
Start Speed: 1 – 3
Noise: Enabled (Strength: 0.4)
Emission: 30–50
Size over Lifetime: Curve up then down
Color over Lifetime: Yellow → Orange → Black
```

---

# **82.7.2 Smoke Trail**

- Soft particles
    
- Subtle turbulence
    
- Low alpha
    

---

# **82.7.3 Ember Particles**

- Add realism
    
- Use burst emissions
    
- Small glowing particles
    

---

# **82.8 VFX GRAPH — HIGH-END VFX (URP/HDRP)**

VFX Graph is GPU-based and faster than Unity particles.

---

# **82.8.1 What You Can Do With VFX Graph**

- Magic spells
    
- Lasers
    
- Projectile trails
    
- Electricity
    
- Explosions
    
- Weather systems
    
- Portals
    
- Black holes
    
- Smoke and fire
    

---

# **82.8.2 VFX Graph Workflow**

1. Create Visual Effect Graph
    
2. Set:
    
    - Spawn
        
    - Initialize
        
    - Update
        
    - Output
        
3. Add attributes:
    
    - Position
        
    - Velocity
        
    - Color
        
    - Lifetime
        

---

# **82.8.3 Magic Spell Example**

Nodes:

- Sphere Position
    
- Curl Noise
    
- Attribute Modifiers
    
- Color over life
    
- Size over life
    

---

# **82.8.4 Lightning Bolt Example**

Nodes:

- Line strip output
    
- Turbulence noise
    
- Random offset
    
- Jitter
    
- Glow
    

---

# **82.8.5 Projectile Trail**

Uses:

- GPU-based ribbon
    
- Velocity-smeared effect
    
- Emissive glow
    

---

# **83. ANIMATION MASTERCLASS (MECHANIM, ANIMATION RIGGING, IK, ADVANCED CONTROLLERS)**

Now we move into **complete professional animation architectures** used in Unity.

This includes:

- Animator controller structure
    
- Sub-state machines
    
- Blend trees
    
- Root motion
    
- Animation events
    
- Procedural animation
    
- Unity Animation Rigging package
    
- IK (Inverse Kinematics)
    
- FPS arms
    
- Third-person combat
    
- Parkour systems
    

---

# **83. ADVANCED ANIMATION SYSTEMS (MECHANIM, RIGGING, IK, PROCEDURAL MOVEMENT, COMBAT SYSTEMS)**

This section teaches **every animation system Unity uses**, including:

- Animator Controllers
    
- State Machines
    
- Blend Trees
    
- Root Motion
    
- Layers & Masks
    
- Animation Events
    
- Animation Rigging (full IK + constraints)
    
- Procedural animation
    
- Dynamic bone-like motion
    
- Foot planting
    
- Weapon IK
    
- FPS hand rigs
    
- Third-person combat animation graphs
    
- Parkour animations
    
- Advanced camera/animation syncing
    

Everything is Unity-specific C# + Unity’s Animator / Rigging tools.  
Follow the exact structure even AAA studios use.

---

# **83.1 THE ANIMATOR CONTROLLER (FULL BREAKDOWN)**

Unity’s Animator Controller is a **state machine**.  
Every animation system you ever build is based on these pieces:

- **States**
    
- **Transitions**
    
- **Parameters**
    
- **Blend Trees**
    
- **Sub-State Machines**
    
- **Layers**
    
- **Avatar Masks**
    

---

# **83.1.1 Animator Parameters Explained Clearly**

Parameter types:

- **Float** – blend amounts (speed, aiming angle)
    
- **Int** – rare; state indexing
    
- **Bool** – triggers for actions (isJumping, isSprinting)
    
- **Trigger** – single-use signal
    

Example Animator Parameters for a Player:

```
Speed (float)
IsGrounded (bool)
IsJumping (bool)
IsAttacking (trigger)
AimAngle (float)
WeaponEquipped (int)
```

---

# **83.1.2 Driving Animator From Code**

```csharp
public class PlayerAnimation : MonoBehaviour
{
    Animator anim;
    PlayerMovement movement;

    void Awake()
    {
        anim = GetComponent<Animator>();
        movement = GetComponent<PlayerMovement>();
    }

    void Update()
    {
        anim.SetFloat("Speed", movement.currentSpeed);
        anim.SetBool("IsGrounded", movement.isGrounded);
    }

    public void PlayAttack()
    {
        anim.SetTrigger("Attack");
    }
}
```

---

# **83.2 SUB-STATE MACHINES (PROFESSIONAL ANIMATOR STRUCTURE)**

For large projects, use the following structure:

```
Base Layer
  ├── Locomotion
  │     ├── Idle
  │     ├── Walk
  │     ├── Run
  │     └── Crouch
  ├── Jump
  │     ├── JumpStart
  │     ├── JumpLoop
  │     └── JumpLand
  ├── Combat
  │     ├── LightAttack1
  │     ├── LightAttack2
  │     ├── HeavyAttack
  │     └── Roll
  ├── Climbing
  └── Swimming
```

AAA animations ALWAYS break logic down this way.

---

# **83.3 BLEND TREES (ALL TYPES)**

Unity has **3 main types**:

- **1D Blend Tree**  
    Example: blend Walk → Run using Speed
    
- **2D Freeform Directional**  
    Example: strafing movement (idle → forward → left → right → back)
    
- **2D Cartesian**  
    Example: aiming up/down + left/right
    

---

# **83.3.1 1D Blend Tree Example (Movement)**

Parameters:

```
Speed
```

Animations:

- Idle (0)
    
- Walk (0.5)
    
- Run (1.0)
    

Driving code:

```csharp
anim.SetFloat("Speed", velocity.magnitude);
```

---

# **83.3.2 2D Blend Tree Example (Strafing Movement)**

Parameters:

```
MoveX
MoveY
```

Animations blended:

- Forward
    
- Backward
    
- Left
    
- Right
    
- Diagonals
    

Driving code:

```csharp
anim.SetFloat("MoveX", input.x);
anim.SetFloat("MoveY", input.y);
```

---

# **83.3.3 Aim Offset Blend Tree (Two-Axis Aiming)**

Used in:

- TPS shooting
    
- Over-the-shoulder camera aiming
    

Parameter:

```
AimAngle
```

Animations:

- Aim down
    
- Aim forward
    
- Aim up
    

---

# **83.4 ROOT MOTION — WHEN TO USE IT & WHEN NOT TO**

---

# **83.4.1 When to Use Root Motion**

Use when **animation drives motion**:

- Cinematic / cutscenes
    
- Melee combat attacks
    
- Special movement
    
- Parkour
    
- Finishers
    

---

# **83.4.2 When NOT to Use Root Motion**

When code controls movement:

- FPS
    
- TPS shooter
    
- Platformer
    
- Racing
    
- Strategy
    

Most gameplay movement is **code-driven**, not animation-driven.

---

# **83.5 ANIMATION EVENTS (CALL FUNCTIONS FROM ANIMATION TIMELINE)**

Used for:

- Attack hit frames
    
- Footstep sounds
    
- Landing shake
    
- Camera recoil
    
- Ability triggers
    

---

## **83.5.1 Code Example**

```csharp
public class PlayerCombat : MonoBehaviour
{
    public void HitEvent()
    {
        Debug.Log("Hit triggered");
    }
}
```

On animation:

```
Add Event → Function = HitEvent
```

---

# **83.6 ADVANCED: ANIMATION RIGGING PACKAGE (IK, CONSTRAINTS, AIM, HAND POSES)**

---

# **83.6.1 Key Constraints**

Animation Rigging contains:

- **Two-Bone IK** (arms/legs)
    
- **Multi-Aim Constraint** (head/torso aiming)
    
- **Multi-Parent Constraint** (weapon parenting)
    
- **Chain IK**
    
- **Twist Correction**
    

These allow:

- Weapon aiming
    
- Foot placement
    
- Procedural look-at
    
- Realistic climbing
    
- Hand IK for holding objects
    
- Dynamic spine movement
    

---

# **83.6.2 Two-Bone IK for Weapon Aiming**

### **Setup**

1. Add **Rig Builder**
    
2. Add **Rig**
    
3. Add **Two-Bone IK Constraint** to arm
    
4. Add a target object (IK target)
    
5. Move target → arm follows
    

### **Driving IK from C#**

```csharp
public class AimIK : MonoBehaviour
{
    public Transform ikTarget;
    public Transform aimPoint;

    void LateUpdate()
    {
        ikTarget.position = aimPoint.position;
    }
}
```

---

# **83.6.3 Look IK With Multi-Aim Constraint**

Set target to player camera:

```csharp
lookConstraint.data.target = cameraTransform;
```

Character automatically looks where player aims.

---

# **83.6.4 FOOT IK (Foot Placement System)**

Used in:

- Walking on uneven terrain
    
- Locomotion polish
    
- AAA-quality character movement
    

---

### **Foot IK Raycast Logic**

```csharp
public class FootIK : MonoBehaviour
{
    public Transform leftFoot, rightFoot;
    public LayerMask ground;

    void LateUpdate()
    {
        UpdateFoot(leftFoot);
        UpdateFoot(rightFoot);
    }

    void UpdateFoot(Transform foot)
    {
        if (Physics.Raycast(foot.position + Vector3.up, Vector3.down, out RaycastHit hit, 1.5f, ground))
        {
            foot.position = hit.point;
        }
    }
}
```

---

# **83.7 FPS ARMS ANIMATION RIGS (FULL EXPLANATION)**

FPS arms rigs are **different** from third-person animation:

- Arms are separate models
    
- Arms often float independently of body
    
- Camera controls arm animations
    

### Features:

- 1st-person sway
    
- Bobbing
    
- Recoil
    
- Procedural movement
    
- IK for hands
    
- Weapon inspection animations
    

---

# **83.7.1 Weapon Sway Example**

```csharp
public class WeaponSway : MonoBehaviour
{
    public float amount = 0.05f;
    public float smooth = 6;

    void Update()
    {
        float x = -Input.GetAxis("Mouse X") * amount;
        float y = -Input.GetAxis("Mouse Y") * amount;

        Quaternion target = Quaternion.Euler(y, x, 0);
        transform.localRotation = Quaternion.Slerp(transform.localRotation, target, Time.deltaTime * smooth);
    }
}
```

---

# **83.7.2 Weapon Bobbing Example**

```csharp
public class WeaponBob : MonoBehaviour
{
    public float speed = 4f;
    public float amount = 0.05f;

    float timer;

    void Update()
    {
        float movement = new Vector3(Input.GetAxis("Horizontal"), 0, Input.GetAxis("Vertical")).magnitude;

        if (movement > 0)
        {
            timer += Time.deltaTime * speed;
            transform.localPosition = new Vector3(
                0,
                Mathf.Sin(timer) * amount,
                0
            );
        }
    }
}
```

---

# **83.8 THIRD-PERSON COMBAT ANIMATION SYSTEM**

This includes:

- Combo attacks
    
- Root motion attacks
    
- Roll/dodge
    
- Hit reaction animations
    
- Directional dodging
    
- Stun states
    

---

# **83.8.1 Combo System Logic**

```csharp
public class ComboSystem : MonoBehaviour
{
    Animator anim;
    int comboStep;

    void Start()
    {
        anim = GetComponent<Animator>();
    }

    public void Attack()
    {
        comboStep++;
        anim.SetInteger("Combo", comboStep);
    }

    public void ResetCombo()
    {
        comboStep = 0;
    }
}
```

Animator calls ResetCombo() using animation events at the end of combo windows.

---

# **83.8.2 Rolling/Dodging Logic**

```csharp
public class PlayerDodge : MonoBehaviour
{
    Animator anim;
    PlayerMovement move;

    void Awake()
    {
        anim = GetComponent<Animator>();
        move = GetComponent<PlayerMovement>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            anim.SetTrigger("Roll");
            move.enabled = false;  // Root motion controls movement
        }
    }

    public void EndRoll()
    {
        move.enabled = true;
    }
}
```

---

# **83.9 PROCEDURAL ANIMATION (ADVANCED)**

Used when animations are not enough.

Examples:

- Tentacle motion
    
- Snake movement
    
- Procedural aim offset
    
- Spine procedural rotation
    
- Head tracking
    
- Weapon alignment
    

---

# **83.9.1 Procedural Head Tracking**

```csharp
public class HeadFollow : MonoBehaviour
{
    public Transform target;
    public float speed = 5f;

    void LateUpdate()
    {
        Vector3 dir = target.position - transform.position;
        Quaternion rot = Quaternion.LookRotation(dir);
        transform.rotation = Quaternion.Slerp(transform.rotation, rot, Time.deltaTime * speed);
    }
}
```

---

# **83.9.2 Procedural Weapon Alignment**

```csharp
public class ProceduralWeaponAim : MonoBehaviour
{
    public Transform cameraTransform;

    void LateUpdate()
    {
        transform.rotation = Quaternion.Lerp(
            transform.rotation,
            cameraTransform.rotation,
            0.2f
        );
    }
}
```

---

# **84. CAMERA & ANIMATION SYNCING (AAA QUALITY)**

---

# **84.1 Camera Shake (Animation + Procedural)**

Procedural shake:

```csharp
public class CameraShake : MonoBehaviour
{
    public static CameraShake I;

    void Awake() => I = this;

    public IEnumerator Shake(float duration, float magnitude)
    {
        Vector3 original = transform.localPosition;
        float time = 0;

        while (time < duration)
        {
            float x = Random.Range(-1f, 1f) * magnitude;
            float y = Random.Range(-1f, 1f) * magnitude;

            transform.localPosition = new Vector3(x, y, original.z);

            time += Time.deltaTime;
            yield return null;
        }
        transform.localPosition = original;
    }
}
```

---

# **84.2 Camera Following Animation Root Motion**

Use for heavy attacks, dashes, boss hits.

Script:

```csharp
public class RootMotionCameraFollow : MonoBehaviour
{
    public Transform target;

    void LateUpdate()
    {
        transform.position = target.position;
    }
}
```

---

# **85. ADVANCED PARKOUR SYSTEM (LEDGE GRAB, CLIMB, VAULT, MANTLE, SLIDE, WALL RUN)**

This section is **full production-level parkour**, built entirely in Unity C#.  
It is structured to work with:

- CharacterController
    
- Rigidbody
    
- Third-person or first-person
    
- Animator
    
- Raycasts
    
- Animation Rigging (optional)
    

This system includes:

- Ledge detection
    
- Hanging
    
- Pull-up
    
- Mantling
    
- Vaulting
    
- Sliding
    
- Wall-running
    
- Environmental tagging
    
- Animation + code sync
    
- Full mechanics, triggers, movement states
    

---

# **85.1 CORE PARKOUR ARCHITECTURE (AAA STYLE)**

Folder structure:

```
Parkour/
  ParkourController.cs
  LedgeDetector.cs
  VaultDetector.cs
  WallRun.cs
  Slide.cs
  ParkourState.cs (optional enum)
  Animation/
  IK/
```

Parkour states (recommended):

```csharp
public enum ParkourState
{
    None,
    LedgeHang,
    LedgeClimb,
    Vault,
    Mantle,
    Slide,
    WallRun
}
```

This lets your entire movement controller know EXACTLY what action is happening.

---

# **85.2 LEDGE GRAB & CLIMB SYSTEM**

This is the foundation of all parkour.

---

# **85.2.1 Ledge Detection Logic (Raycast Method)**

Ledges are detected by:

1. **Forward check** (find wall)
    
2. **Upward check** (find free space above wall)
    
3. **Ledge height check**
    
4. **Snap to ledge hang position**
    

---

## **85.2.2 Ledge Detector Script**

```csharp
public class LedgeDetector : MonoBehaviour
{
    public LayerMask climbLayer;
    public float detectDistance = 1f;
    public float detectHeight = 1.5f;
    public float ledgeOffset = 0.5f;

    public bool DetectLedge(out Vector3 hangPoint)
    {
        hangPoint = Vector3.zero;

        // Step 1: forward ray
        if (Physics.Raycast(transform.position + Vector3.up * detectHeight,
                            transform.forward, out RaycastHit hit, detectDistance, climbLayer))
        {
            // Step 2: ray down from top of ledge
            Vector3 upperPoint = hit.point + Vector3.up * 1f;

            if (Physics.Raycast(upperPoint, Vector3.down, out RaycastHit downHit, 2f, climbLayer))
            {
                hangPoint = downHit.point - (transform.forward * ledgeOffset);
                return true;
            }
        }
        return false;
    }
}
```

---

# **85.2.3 ParkourController Handling Ledge Grab**

```csharp
public class ParkourController : MonoBehaviour
{
    public ParkourState state;
    public LedgeDetector ledgeDetector;
    public Animator anim;
    public CharacterController controller;

    Vector3 hangPosition;
    bool isHanging;

    void Update()
    {
        if (state == ParkourState.None)
        {
            if (ledgeDetector.DetectLedge(out Vector3 point))
                StartLedgeHang(point);
        }
        
        if (isHanging && Input.GetKeyDown(KeyCode.W))
            StartClimbUp();
    }

    void StartLedgeHang(Vector3 pos)
    {
        state = ParkourState.LedgeHang;
        isHanging = true;

        controller.enabled = false; // freeze position
        hangPosition = pos;

        transform.position = hangPosition;
        anim.SetTrigger("Hang");
    }

    void StartClimbUp()
    {
        state = ParkourState.LedgeClimb;
        anim.SetTrigger("ClimbUp");
    }

    // called from animation event at end of climb animation
    public void EndClimb()
    {
        transform.position += transform.forward * 1.2f + Vector3.up * 1.0f;
        controller.enabled = true;
        isHanging = false;
        state = ParkourState.None;
    }
}
```

---

# **85.2.4 Animator Requirements**

Animations needed:

- Hang Idle
    
- Pull Up
    
- Climb Up Finish
    
- Drop Down
    

These animations need **root motion ON**.

---

# **85.3 MANTLING SYSTEM (SMOOTH CLIMB UP SHORT OBSTACLES)**

Mantle is used for obstacles around waist height.

Examples:

- Climbing onto a table
    
- Getting over a barrier
    
- Climbing onto a box
    
- Smooth small obstacle traversal
    

---

# **85.3.1 Mantle Detection**

Check for:

1. Wall close to player
    
2. Surface on top
    
3. Enough space to stand
    

---

## **85.3.2 Mantle Detector Script**

```csharp
public class MantleDetector : MonoBehaviour
{
    public float forwardCheckDistance = 1f;
    public float mantleHeight = 1f;
    public LayerMask mantleLayer;

    public bool DetectMantle(out Vector3 mantlePoint)
    {
        mantlePoint = Vector3.zero;

        if (Physics.Raycast(transform.position + Vector3.up * 0.5f,
                            transform.forward, out RaycastHit wallHit,
                            forwardCheckDistance, mantleLayer))
        {
            // Check if surface above exists
            Vector3 topCheckOrigin = wallHit.point + Vector3.up * mantleHeight;
            if (Physics.Raycast(topCheckOrigin, Vector3.down, out RaycastHit topHit, mantleHeight + 0.5f))
            {
                mantlePoint = topHit.point;
                return true;
            }
        }
        return false;
    }
}
```

---

# **85.3.3 Mantle Implementation**

```csharp
public void TryMantle()
{
    if (state != ParkourState.None) return;

    if (mantleDetector.DetectMantle(out Vector3 mantlePoint))
        StartCoroutine(MantleRoutine(mantlePoint));
}

IEnumerator MantleRoutine(Vector3 point)
{
    state = ParkourState.Mantle;
    controller.enabled = false;

    anim.SetTrigger("Mantle");

    // Move player smoothly
    float t = 0;
    Vector3 start = transform.position;
    Vector3 end = point + transform.forward * 0.5f;

    while (t < 1)
    {
        t += Time.deltaTime * 2f;
        transform.position = Vector3.Lerp(start, end, t);
        yield return null;
    }

    controller.enabled = true;
    state = ParkourState.None;
}
```

---

# **85.4 VAULTING SYSTEM**

Vaulting is when you:

- Move fast
    
- Hit waist height obstacle
    
- Slide over it fluidly
    

Used in:

- Action games
    
- Shooters
    
- Parkour games
    

---

# **85.4.1 Vault Detection**

```csharp
public class VaultDetector : MonoBehaviour
{
    public LayerMask vaultLayer;
    public float detectDistance = 1f;
    public float vaultHeight = 1f;

    public bool DetectVault(out Vector3 vaultPoint)
    {
        vaultPoint = Vector3.zero;

        Vector3 origin = transform.position + Vector3.up * vaultHeight;
        if (Physics.Raycast(origin, transform.forward, out RaycastHit hit, detectDistance, vaultLayer))
        {
            vaultPoint = hit.point + transform.forward * 1.2f;
            return true;
        }
        return false;
    }
}
```

---

# **85.4.2 Vault Logic**

```csharp
public void TryVault()
{
    if (vaultDetector.DetectVault(out Vector3 point))
        StartCoroutine(VaultRoutine(point));
}

IEnumerator VaultRoutine(Vector3 point)
{
    state = ParkourState.Vault;
    controller.enabled = false;

    anim.SetTrigger("Vault");

    // Smooth vault movement
    float t = 0;
    Vector3 start = transform.position;

    while (t < 1)
    {
        t += Time.deltaTime * 2f;
        transform.position = Vector3.Lerp(start, point, t);
        yield return null;
    }

    controller.enabled = true;
    state = ParkourState.None;
}
```

---

# **85.5 SLIDING SYSTEM**

Used in:

- Sprinting
    
- Crouch-to-slide transition
    
- Modern shooters
    

---

# **85.5.1 Slide Start Logic**

```csharp
public class Slide : MonoBehaviour
{
    public float slideSpeed = 8f;
    public float slideDuration = 1f;
    CharacterController controller;

    void Awake()
    {
        controller = GetComponent<CharacterController>();
    }

    public IEnumerator SlideRoutine()
    {
        float timer = 0;
        while (timer < slideDuration)
        {
            Vector3 move = transform.forward * slideSpeed;
            controller.Move(move * Time.deltaTime);
            timer += Time.deltaTime;
            yield return null;
        }
    }
}
```

---

# **85.6 WALL RUNNING SYSTEM**

Games using this:

- Titanfall
    
- Warframe
    
- Mirror’s Edge
    
- Doom Eternal (in some cases)
    

---

# **85.6.1 Wall Detection (Raycast)**

```csharp
public class WallRun : MonoBehaviour
{
    public LayerMask wallLayer;
    public float rayDist = 1f;
    public float wallRunGravity = -2f;
    public float wallSpeed = 7f;

    public bool IsWallOnLeft()
    {
        return Physics.Raycast(transform.position, -transform.right, rayDist, wallLayer);
    }

    public bool IsWallOnRight()
    {
        return Physics.Raycast(transform.position, transform.right, rayDist, wallLayer);
    }
}
```

---

# **85.6.2 Wall Run Logic**

```csharp
public void TryWallRun()
{
    if (IsWallOnLeft() || IsWallOnRight())
        StartWallRun();
}

void StartWallRun()
{
    state = ParkourState.WallRun;
    movement.gravity = wallRunGravity; // reduce gravity
    anim.SetBool("WallRun", true);
}

void StopWallRun()
{
    state = ParkourState.None;
    movement.gravity = -9.81f;
    anim.SetBool("WallRun", false);
}
```

---

# **85.6.3 Movement During Wall Run**

```csharp
void Update()
{
    if (state == ParkourState.WallRun)
    {
        controller.Move(transform.forward * wallSpeed * Time.deltaTime);

        if (!IsWallOnLeft() && !IsWallOnRight())
            StopWallRun();
    }
}
```

---

# **86. COMPLETE THIRD-PERSON CONTROLLER (AAA QUALITY)**

This is a **full production-ready, industry-level third-person controller** used in open-world, action, RPG, shooter, survival, Souls-like, and adventure games.

This system includes:

- CharacterController-based movement
    
- Full directional locomotion
    
- Acceleration / deceleration curves
    
- Sprinting, crouching, sliding
    
- Smooth rotation system
    
- Jump, fall, landing detection
    
- Air control
    
- Roll/Dodge
    
- Root-motion attack support
    
- Camera-aligned movement
    
- Animation integration (with Blend Trees)
    
- Input buffering
    
- State machine structure
    
- Data-driven movement parameters
    

Everything is Unity-specific C# + Animator + physics.

---

# **86.1 Folder Structure (AAA Standard)**

Use this exact structure for professional scalability:

```
ThirdPerson/
  Controller/
    ThirdPersonController.cs
    Movement.cs
    Jump.cs
    Fall.cs
    Dodge.cs
    CameraAlign.cs
  Animation/
    ThirdPersonAnimation.cs
  Data/
    MovementSettings.cs
  Input/
    PlayerInput.cs
```

---

# **86.2 Movement Settings (ScriptableObject Driven)**

All movement tuning values should come from a data file.

```csharp
using UnityEngine;

[CreateAssetMenu(menuName = "TPController/MovementSettings")]
public class MovementSettings : ScriptableObject
{
    public float walkSpeed = 2f;
    public float runSpeed = 5f;
    public float sprintSpeed = 8f;

    public float rotationSpeed = 12f;

    public float acceleration = 8f;
    public float deceleration = 10f;

    public float jumpForce = 7f;
    public float gravity = -20f;
    public float airControl = 0.5f;

    public float rollSpeed = 9f;
}
```

This allows designers to tune player feel **without touching code**.

---

# **86.3 Core Third-Person Controller**

This is the central script that:

- Reads input
    
- Calls movement modules
    
- Updates animator parameters
    
- Handles state transitions
    

```csharp
using UnityEngine;

[RequireComponent(typeof(CharacterController))]
public class ThirdPersonController : MonoBehaviour
{
    public MovementSettings settings;
    public Transform cameraTransform;

    CharacterController controller;
    Animator anim;

    Vector3 velocity;
    float speed;

    bool isSprinting;
    bool isGrounded;

    void Awake()
    {
        controller = GetComponent<CharacterController>();
        anim = GetComponent<Animator>();
    }

    void Update()
    {
        GroundCheck();
        Movement();
        Gravity();
        Jump();
        ApplyMovement();
        Animate();
    }
```

---

# **86.4 Camera-Aligned Movement (Industry Standard)**

Movement is relative to camera orientation:

```csharp
Vector3 GetCameraRelativeMove(Vector2 input)
{
    Vector3 forward = cameraTransform.forward;
    Vector3 right   = cameraTransform.right;

    forward.y = 0;
    right.y = 0;

    forward.Normalize();
    right.Normalize();

    return forward * input.y + right * input.x;
}
```

This is how ALL modern games control movement.

---

# **86.5 Movement Logic (Acceleration + Deceleration)**

```csharp
void Movement()
{
    Vector2 input = new Vector2(
        Input.GetAxis("Horizontal"),
        Input.GetAxis("Vertical")
    );

    Vector3 direction = GetCameraRelativeMove(input);

    float targetSpeed =
        isSprinting ? settings.sprintSpeed :
        input.magnitude > 0.1f ? settings.runSpeed :
        0;

    // Acceleration
    speed = Mathf.MoveTowards(speed, targetSpeed,
        (targetSpeed > speed ? settings.acceleration : settings.deceleration)
        * Time.deltaTime
    );

    // Rotate to movement direction
    if (direction.magnitude > 0.1f)
    {
        Quaternion targetRot =
            Quaternion.LookRotation(direction);

        transform.rotation = Quaternion.Slerp(
            transform.rotation,
            targetRot,
            settings.rotationSpeed * Time.deltaTime
        );
    }

    // Movement
    Vector3 move = direction * speed;
    controller.Move(move * Time.deltaTime);
}
```

This creates smooth, responsive AAA-level movement.

---

# **86.6 Jump System**

```csharp
void Jump()
{
    if (Input.GetButtonDown("Jump") && isGrounded)
    {
        velocity.y = settings.jumpForce;
        anim.SetTrigger("Jump");
    }
}
```

---

# **86.7 Fall + Landing Detection**

```csharp
void Gravity()
{
    if (isGrounded && velocity.y < 0)
        velocity.y = -2f;

    velocity.y += settings.gravity * Time.deltaTime;
}

void GroundCheck()
{
    Ray ray = new Ray(transform.position + Vector3.up * 0.2f, Vector3.down);
    isGrounded = Physics.Raycast(ray, 0.4f);
}
```

---

# **86.8 Apply Movement**

```csharp
void ApplyMovement()
{
    controller.Move(velocity * Time.deltaTime);
}
```

---

# **86.9 Sprinting Logic**

```csharp
void Update()
{
    isSprinting = Input.GetKey(KeyCode.LeftShift) && isGrounded;
}
```

---

# **86.10 Roll/Dodge (Directional Dodge System)**

```csharp
public void Dodge()
{
    if (!isGrounded) return;

    anim.SetTrigger("Roll");

    Vector3 dodgeDir = transform.forward;
    StartCoroutine(DodgeRoutine(dodgeDir));
}

IEnumerator DodgeRoutine(Vector3 dir)
{
    float t = 0;
    while (t < 0.5f)
    {
        controller.Move(dir * settings.rollSpeed * Time.deltaTime);
        t += Time.deltaTime;
        yield return null;
    }
}
```

---

# **86.11 Complete Animator Integration**

Animator Parameters:

```
Speed (float 0–1)
Grounded (bool)
VerticalSpeed (float)
Roll (trigger)
Jump (trigger)
```

Script:

```csharp
void Animate()
{
    anim.SetFloat("Speed", speed / settings.sprintSpeed);
    anim.SetBool("Grounded", isGrounded);
    anim.SetFloat("VerticalSpeed", velocity.y);
}
```

---

# **86.12 Blend Tree Setup (AAA Standard)**

### Locomotion 1D Blend Tree:

- Idle ← 0
    
- Walk ← 0.4
    
- Run ← 0.8
    
- Sprint ← 1.0
    

Parameter: **Speed**

---

# **86.13 Root Motion Attacks + Movement Disable**

Root-motion attacks:

- Control movement via animation
    
- Movement script must disable itself
    

```csharp
public void StartAttack()
{
    anim.SetTrigger("Attack");
    canMove = false;
}

public void EndAttack() // called from Animation Event
{
    canMove = true;
}
```

---

# **86.14 Input Buffering for Responsiveness (Souls-like Standard)**

```csharp
bool bufferedAttack;

void Update()
{
    if (Input.GetMouseButtonDown(0))
        bufferedAttack = true;

    if (canAttack && bufferedAttack)
    {
        Attack();
        bufferedAttack = false;
    }
}
```

Ensures attack still triggers even if pressed early.

---

# **86.15 Air Control**

```csharp
if (!isGrounded)
{
    Vector3 horizontalMove = direction * settings.runSpeed * settings.airControl;
    controller.Move(horizontalMove * Time.deltaTime);
}
```

---

# **86.16 Movement State Machine**

Optional but highly recommended:

```
Idle / Move → Jump → Fall → Land
           → Dodge
           → Attack
           → Climb (parkour)
           → Slide
```

This ensures controlled transitions.

---

# **87. RAGDOLL SYSTEMS — BLENDING, HIT REACTIONS, AND GET-UP ANIMATIONS**

This section provides a complete, production-ready Unity C# guide for ragdolls: how to author them, how to blend between animated and physics-driven states, how to play hit reactions, and how to do believable get-up/transitions. Includes setup, scripts, animator integration, joint tuning, network considerations, pooling, and optimization.

---

## **87.1 Overview & Use Cases**

**What a ragdoll is:** a hierarchy of rigidbodies + colliders connected by joints that let a character physically react under physics forces.

**When to use ragdolls:**

- Death physics (character falls naturally)
    
- Knockback / stagger physics realism
    
- Dynamic responses to explosions or impacts
    
- Physical interactions (pushed by vehicles)
    
- Temporary hit-reaction physics before blending back to animation
    

**Common goals:**

- Realistic, non-robotic reactions
    
- Seamless transitions to/from keyframed animation
    
- Deterministic behavior for networked games (if required)
    
- Good performance (for many characters)
    

---

## **87.2 Authoring a Ragdoll (Unity Editor Steps)**

1. **Prepare the animated skeleton** (Humanoid or Generic rig) in a character model import.
    
2. **Add colliders** (capsule/box/sphere) per main bone: pelvis, spine, head, upper/lower arms, hands, upper/lower legs, feet.
    
3. **Add Rigidbody** to each bone that will simulate. Set mass distribution (center mass on pelvis).
    
4. **Add ConfigurableJoint / CharacterJoint** to connect child bone rigidbodies to parent.
    
5. **Tune joint limits** (swing/twist) to avoid unnatural flopping.
    
6. **Use Rigidbody interpolation** (Interpolate) for smoother visuals when animated → physics changes occur.
    
7. **Test in Play** by enabling physics and dropping the model.
    

Unity’s **Ragdoll Wizard** (Component → Ragdoll...) auto-generates colliders/joints—start there then refine.

---

## **87.3 Basic Ragdoll Script Pattern**

Two modes: **Animated** and **Ragdoll (Physics)**. At runtime you switch between them.

### **Key ideas**

- When animated: set all child Rigidbodies `isKinematic = true` (or disable physics), enable Animator.
    
- When ragdolling: set `isKinematic = false`, disable Animator so physics drives bones.
    
- For blending back to animation: sample ragdoll pose to drive animation parameters or use a physics-to-animation blend.
    

### **Simple enable/disable script**

```csharp
using UnityEngine;

public class RagdollController : MonoBehaviour
{
    Rigidbody[] rbs;
    Animator animator;

    void Awake()
    {
        animator = GetComponent<Animator>();
        rbs = GetComponentsInChildren<Rigidbody>();
        SetRagdoll(false);
    }

    public void SetRagdoll(bool on)
    {
        animator.enabled = !on;
        foreach (var rb in rbs)
        {
            rb.isKinematic = !on;
            rb.detectCollisions = on;
        }

        // optional: enable colliders only during ragdoll
        var colliders = GetComponentsInChildren<Collider>();
        foreach (var col in colliders) col.enabled = on;
    }

    // simple timed ragdoll for death
    public void Die()
    {
        SetRagdoll(true);
        // disable other gameplay scripts here (AI, controllers)
    }
}
```

**Notes:**

- Use `rb.WakeUp()` after enabling physics if needed.
    
- When disabling ragdoll, you often need to blend back to a standing pose rather than abruptly re-enabling Animator.
    

---

## **87.4 Blending Back from Ragdoll to Animation (Smooth Get-Up)**

Abruptly toggling Animator back causes snapping. Use a blend routine:

### **Approach A — Match pose and crossfade**

1. Capture ragdoll bone transforms (world space).
    
2. Disable physics and set bones to remembered pose.
    
3. Crossfade to a “getUp” animation that assumes certain starting pose.
    
4. Use Animation Rigging or an IK montage to refine.
    

### **Approach B — Physics-to-Animator blend (recommended)**

- Keep physics-enabled but drive Animator using IK that follows ragdoll pose, then gradually increase Animator weight, freeze physics when done.
    

### **Practical Implementation — capture & blend**

```csharp
using System.Collections;
using UnityEngine;

public class RagdollToAnim : MonoBehaviour
{
    Animator animator;
    Rigidbody[] rbs;
    Transform[] bones;
    Vector3[] storedPositions;
    Quaternion[] storedRotations;

    void Awake()
    {
        animator = GetComponent<Animator>();
        rbs = GetComponentsInChildren<Rigidbody>();
        bones = new Transform[rbs.Length];
        for (int i = 0; i < rbs.Length; i++) bones[i] = rbs[i].transform;
    }

    public void EnterRagdoll()
    {
        SetRagdoll(true);
    }

    public void StartGetUp()
    {
        StartCoroutine(BlendToAnimator(0.5f));
    }

    IEnumerator BlendToAnimator(float blendTime)
    {
        // 1. store ragdoll pose
        storedPositions = new Vector3[bones.Length];
        storedRotations = new Quaternion[bones.Length];
        for (int i = 0; i < bones.Length; i++)
        {
            storedPositions[i] = bones[i].position;
            storedRotations[i] = bones[i].rotation;
        }

        // 2. make bodies kinematic but keep bone transforms
        foreach (var rb in rbs) { rb.isKinematic = true; rb.detectCollisions = false; }

        // 3. force bones to stored pose (world space)
        for (int i = 0; i < bones.Length; i++)
        {
            bones[i].position = storedPositions[i];
            bones[i].rotation = storedRotations[i];
        }

        // 4. enable animator and crossfade to getup anim
        animator.enabled = true;
        animator.CrossFade("GetUp", 0.1f);

        // 5. blend IK/animation influence if necessary (example uses simple wait)
        float t = 0f;
        while (t < blendTime)
        {
            t += Time.deltaTime;
            float alpha = t / blendTime;
            // Interpolate bones from stored pose to animated pose
            for (int i = 0; i < bones.Length; i++)
            {
                Transform bone = bones[i];
                Vector3 targetPos = bone.position; // animator-driven target after enabling
                Quaternion targetRot = bone.rotation;

                bone.position = Vector3.Lerp(storedPositions[i], targetPos, alpha);
                bone.rotation = Quaternion.Slerp(storedRotations[i], targetRot, alpha);
            }
            yield return null;
        }

        // cleanup: ensure animator fully controls
        // enable colliders as needed
        foreach (var col in GetComponentsInChildren<Collider>()) col.enabled = true;
        foreach (var rb in rbs) rb.isKinematic = true;
        SetRagdoll(false);
    }

    void SetRagdoll(bool on)
    {
        animator.enabled = !on;
        foreach (var rb in rbs)
        {
            rb.isKinematic = !on;
            rb.detectCollisions = on;
        }
        foreach (var col in GetComponentsInChildren<Collider>())
            col.enabled = on;
    }
}
```

**Important:** the exact sequence depends on animator rig complexity. Using `Animator.Update()` and forcing bone transforms may be necessary to align targets.

---

## **87.5 Hit Reactions — Local and Physics-Based**

Two main patterns:

### **Pattern 1 — Procedural hit reaction + short ragdoll impulse**

- Play a brief animation blend (0.1–0.4s) using Animator with additive layers (upper-body).
    
- At hit time, apply impulse to nearby ragdoll bones (chest, pelvis) to add weight.
    
- Optionally enable partial ragdoll (only lower body physics) for more realism.
    

### **Pattern 2 — Full ragdoll on strong hits**

- If force > threshold or lethal, transition to ragdoll using `SetRagdoll(true)` and apply `rb.AddForce()` to the hit bone.
    

### **Applying Impulse to a bone:**

```csharp
public void ApplyHitForce(Transform hitBone, Vector3 force)
{
    var rb = hitBone.GetComponent<Rigidbody>();
    if (rb != null && !rb.isKinematic)
        rb.AddForce(force, ForceMode.Impulse);
}
```

### **Upper-body additive reaction sample (Animator layer):**

- Add an **UpperBody** layer to Animator with `AvatarMask` to only affect spine/arms/head.
    
- Trigger `Hit` parameter to play a blendable reaction clip.
    
- Optionally use `Animator.CrossFadeInFixedTime("Hit_Reaction", 0.05f, layerIndex);`
    

---

## **87.6 Ragdoll Joint Tuning (Practical Tips)**

- **Mass distribution:** make pelvis heavier than limbs (pelvis ~ 20–30% total mass). Use mass scaling on joints.
    
- **Damping:** add angular/linear damping to limit jitter.
    
- **Joint limits:** limit twist & swing to plausible ranges (common cause of explosive joints).
    
- **Breakable joints:** optionally use `Joint.breakForce` / `breakTorque` for dramatic breakage (e.g., limb sever).
    
- **Contact materials:** set PhysicMaterial with appropriate friction/bounciness.
    

Example joint setup using `ConfigurableJoint`:

```csharp
var joint = child.AddComponent<ConfigurableJoint>();
joint.connectedBody = parentRB;
joint.angularXMotion = ConfigurableJointMotion.Limited;
joint.angularYMotion = ConfigurableJointMotion.Limited;
joint.angularZMotion = ConfigurableJointMotion.Limited;
SoftJointLimit limit = new SoftJointLimit { limit = 45f };
joint.lowAngularXLimit = limit;
joint.highAngularXLimit = limit;
joint.angularYLimit = limit;
joint.angularZLimit = limit;

JointDrive drive = new JointDrive { positionSpring = 1000f, maximumForce = 1000f };
joint.angularXDrive = drive;
joint.angularYZDrive = drive;
```

Tune `positionSpring` and `maximumForce` to get the desired stiffness.

---

## **87.7 Partial Ragdolls and Layered Physics**

**Partial ragdolls** enable physics only on a subset of bones (spine+arms) while keeping legs animated—useful to avoid falling through the floor or to enable usable get-ups.

Implementation: maintain a mapping of bones to enable/disable physics. Example use: when hit in torso, enable ragdoll only for spine+arms+head.

---

## **87.8 Ragdoll Pooling & Reuse**

Creating/destroying ragdoll objects can be expensive (GC, engine registration). Pool deaths and reuse prefabs:

- Pre-instantiate a pool of ragdoll prefabs (disabled)
    
- On death: detach from AI controller, activate ragdoll instance, copy transforms, apply impulse, schedule return after X seconds
    
- For player characters (single instance) no pooling needed; for many NPCs, do pooling
    

Pseudo pooling pattern:

```csharp
public class RagdollPool : MonoBehaviour
{
    public GameObject ragdollPrefab;
    Queue<GameObject> pool = new Queue<GameObject>();

    public GameObject Get()
    {
        if (pool.Count == 0) Expand();
        var g = pool.Dequeue();
        g.SetActive(true);
        return g;
    }

    public void Return(GameObject g)
    {
        g.SetActive(false);
        pool.Enqueue(g);
    }

    void Expand() { var g = Instantiate(ragdollPrefab); g.SetActive(false); pool.Enqueue(g); }
}
```

When using pooled ragdolls, copy the animated transform hierarchy into the pooled object before enabling physics to match the instantaneous pose.

---

## **87.9 Ragdolls + Animation Rigging Techniques**

To create believable transitions and corrections:

- Use **Animation Rigging** to drive hands/feet alignment while the body is physics-driven.
    
- Use a **two-way hybrid**: physics drives bones, but constraints steer joints to prevent penetration.
    
- Use `Multi-Parent` or `Multi-Aim` constraints to anchor ragdoll to environment (e.g., grabbing a ledge).
    

---

## **87.10 Get-Up Animations: Detecting Face-Up vs Face-Down**

Decide which get-up animation to use by comparing the ragdoll’s chest/up vector vs world up.

```csharp
Vector3 chestUp = chestBone.up;
float dot = Vector3.Dot(chestUp, Vector3.up);
if (dot > 0.5f) // face up
    animator.Play("GetUpFaceUp");
else
    animator.Play("GetUpFaceDown");
```

Blend from stored ragdoll pose into the get-up animation (see 87.4).

---

## **87.11 Networking Ragdolls — Determinism and Authority**

**Best practice:** Server-authoritative ragdolls.

- On death, server spawns a ragdoll network object and simulates physics on server (or uses deterministic server physics).
    
- Clients display ragdoll via replication: transmit transforms or use physics snapshot interpolation.
    
- For authoritative servers with many ragdolls, consider server-side playback + baked animation on clients to save server CPU.
    

**Sync options:**

- **Full transform sync**: send positions & rotations of bones (heavy).
    
- **Approximation**: send root transform + key bone rotations; clients simulate physics locally for visuals.
    
- **Replay**: server records impulse events and lets each client apply local physics with same impulses (nondeterministic).
    

Network sample: spawn ragdoll prefab with NetworkObject, set initial bone transforms on spawn, apply impulse via ServerRpc, and let clients simulate.

---

## **87.12 Performance & Stability Checklist**

- Limit ragdoll lifetime (auto-despawn after x seconds).
    
- Use simplified colliders (capsules) instead of mesh colliders.
    
- Set collision layers to prevent ragdolls colliding with many things (e.g., ragdoll layer collides only with world).
    
- Reduce joints per ragdoll when many are active (e.g., use fewer simulated bones at distance).
    
- Use interpolation on Rigidbodies for smoothness.
    
- Use Quality settings to scale physics iteration counts per platform.
    
- Use `Physics.autoSimulation = false` to manually step physics for deterministic control when necessary (advanced).
    

```csharp
Physics.autoSimulation = false;
Physics.Simulate(Time.fixedDeltaTime);
```

---

## **87.13 Edge Cases & Troubleshooting**

- **Exploding ragdoll**: joints too loose; increase joint constraints and damping.
    
- **Limb jitter**: increase rigidbody mass or set angular/linear drag.
    
- **Bones sinking**: root/character controller collision conflicts — ensure character controller disabled when ragdoll enabled.
    
- **Animator snapping after disable**: ensure bones are explicitly set to ragdoll pose before re-enabling Animator (use blend routine).
    
- **Ragdoll through terrain**: confirm colliders are correctly placed and not penetrating the ground; use collision detection mode ContinuousDynamic for fast moving parts.
    

---

## **87.14 Example: Full Death Flow (Code)**

```csharp
public class CharacterDeath : MonoBehaviour
{
    RagdollController ragdoll;
    Animator anim;
    CapsuleCollider capsule;
    CharacterController cc;

    void Awake()
    {
        ragdoll = GetComponent<RagdollController>();
        anim = GetComponent<Animator>();
        capsule = GetComponent<CapsuleCollider>();
        cc = GetComponent<CharacterController>();
    }

    public void Die(Vector3 hitPoint, Vector3 force)
    {
        // disable gameplay systems
        GetComponent<AIController>()?.enabled = false;
        GetComponent<Health>()?.enabled = false;

        // prepare ragdoll pool instance or self
        ragdoll.SetRagdoll(true);

        // apply force to nearest bone
        Rigidbody hitRb = ragdoll.GetClosestRigidbody(hitPoint);
        if (hitRb != null) hitRb.AddForce(force, ForceMode.Impulse);

        // disable controller/collider
        capsule.enabled = false;
        if (cc != null) cc.enabled = false;

        // schedule cleanup
        StartCoroutine(CleanupAfterSeconds(10f));
    }

    IEnumerator CleanupAfterSeconds(float sec)
    {
        yield return new WaitForSeconds(sec);
        // if pooled, hand back to pool; else Destroy(gameObject)
        Destroy(gameObject);
    }
}
```

`GetClosestRigidbody` simply iterates `rbs` and returns nearest by distance to hit point.

---

## **87.15 Advanced Techniques**

- **Blend Shapes on ragdolls:** use blend shapes for facial reaction while body is ragdolled by physics.
    
- **Weighted ragdoll:** use joint drives to partially keep pose (blend factor), enabling “limp but controlled” feels.
    
- **Active ragdoll (simulation-driven animation):** use physics to drive animations—complex, requires PD controllers and is used in advanced locomotion research.
    
- **Ragdoll posing tools:** create Editor windows to capture ragdoll poses and author transition animations matching them.
    
- **Ragdoll-to-anim matching via pose assets:** export a get-up animation that matches popular ragdoll resting poses to avoid visible snap.
    

---

## **87.16 Summary — Production Tips**

- Design two workflows: **death ragdolls** (one-shot, poolable) and **reaction ragdolls** (brief physics with blend back to animation).
    
- Test on target platforms and scale joint complexity per LOD.
    
- Use collision layers and PhysicMaterials to prevent ragdoll performance cliffs.
    
- For networked games, prefer server authority; send impulses, not bone-by-bone streams, when feasible.
    
- Build editor tools to preview ragdoll transitions and tune joint limits quickly.
    

---

# **88. CLIMBING SYSTEM — UNCHARTED / ZELDA STYLE (FULL PRODUCTION IMPLEMENTATION)**

Complete Unity-specific C# design: detection, state machine, animations, IK, transitions, ledge traversal, rope/ladder, climb surfaces, stamina, editor tooling, networking notes, performance considerations.

---

## **88.1 Goals & Design Requirements**

- Support multiple climb types: ledge grab, mantle, full climbing surfaces, ladders, ropes, vines.
    
- Smooth transitions: run → grab → climb → pull up → drop.
    
- Animation-driven with root motion where applicable.
    
- Procedural alignment using IK for hand/foot placement.
    
- Stamina system to limit climb duration.
    
- Editor tools to tag climbable surfaces and adjust parameters per-surface.
    
- Network-safe: server authoritative state and interpolation for clients.
    

---

## **88.2 High-Level Flow (State Machine)**

```
Grounded
  └→ Vault/Mantle (short obstacles)
  └→ LedgeGrab → Hang → ClimbUp → PullUp → Grounded
  └→ SurfaceClimb → MoveOnWall → ClimbJump / Drop → Grounded
  └→ Ladder/Rope → ClimbUp/Down → Dismount
```

States are exclusive; movement controller delegates to ClimbingController while in climbing state.

---

## **88.3 Scene Setup & Surface Tagging**

- Add a `Climbable` component to surfaces (mesh/collider).
    
- Expose parameters:
    
    - `maxGripAngle`
        
    - `stepHeight`
        
    - `handSnapPoints` (optional child transforms)
        
    - `movementDirection` (free or constrained)
        
    - `staminaDrainPerSecond`
        
    - `isLadder` / `isRope` flags
        

```csharp
public class Climbable : MonoBehaviour
{
    public float maxGripAngle = 60f;
    public float stepHeight = 0.3f;
    public bool isLadder = false;
    public bool isRope = false;
    public float staminaDrain = 5f;
    public Transform[] handPoints; // optional anchors
}
```

Use layers for detection (ClimbLayer) to avoid unnecessary raycasts.

---

## **88.4 Input & Activation**

Player triggers climb by:

- Pressing `Grab` near a ledge
    
- Pressing `Climb` when facing a climbable wall within reach
    
- Interacting with ladder/rope by pressing `Interact`
    

Provide context sensitive prompts in UI.

---

## **88.5 Detection Primitives**

- **Forward capsule / box cast** for walls.
    
- **Upper ray / lower ray** for ledge top check.
    
- **Sphere overlaps** to detect ladders/ropes.
    
- **Surface normal & angle** check (`Vector3.Angle`).
    

Example ledge detection (robust):

```csharp
public bool DetectLedge(out Vector3 hangPoint, out Vector3 ledgeNormal)
{
    hangPoint = Vector3.zero; ledgeNormal = Vector3.up;
    Vector3 origin = transform.position + Vector3.up * ledgeCheckHeight;
    if (Physics.SphereCast(origin, sphereRadius, transform.forward, out RaycastHit hit, forwardMaxDistance, climbLayer))
    {
        // validate top surface exists
        Vector3 topCheck = hit.point + hit.normal * 0.1f + Vector3.up * topCheckHeight;
        if (Physics.Raycast(topCheck, Vector3.down, out RaycastHit topHit, topCheckHeight + 0.5f, climbLayer))
        {
            // ensure the top surface is not too steep
            float slope = Vector3.Angle(topHit.normal, Vector3.up);
            if (slope <= maxGripAngle)
            {
                hangPoint = topHit.point;
                ledgeNormal = hit.normal;
                return true;
            }
        }
    }
    return false;
}
```

---

## **88.6 Ledge Grab & Hang Implementation**

- Snap player to hang position (slightly offset from ledge to prevent clipping).
    
- Disable CharacterController during hang or use kinematic mode.
    
- Play `HangIdle` animation; allow player to climb up, shimmy left/right, or drop.
    

Key code:

```csharp
void StartLedgeHang(Vector3 hangPoint, Vector3 normal)
{
    state = ClimbState.Hang;
    controller.enabled = false;
    // position and orientation
    Vector3 offset = -normal * hangOffset + Vector3.up * hangHeightOffset;
    transform.position = hangPoint + offset;
    transform.rotation = Quaternion.LookRotation(-normal);
    animator.CrossFade("HangIdle", 0.05f);
}
```

Allow **shimmy**:

```csharp
void Shimmy(float dir)
{
    Vector3 right = transform.right;
    transform.position += right * dir * shimmySpeed * Time.deltaTime;
    animator.SetFloat("Shimmy", dir);
}
```

---

## **88.7 Pull Up / Climb Up**

- Triggered by forward or jump input while hanging.
    
- Play `PullUp` animation (root motion) and move player to top.
    
- Use animation event at end to enable controller and set grounded state.
    

```csharp
public void EndPullUp()
{
    controller.enabled = true;
    state = ClimbState.Grounded;
}
```

---

## **88.8 Surface Climbing (Wall Movement)**

- Use hand & foot IK to place limbs against surface.
    
- Movement along the surface uses projected movement vectors.
    

Projection example:

```csharp
Vector3 moveDir = (camera.forward * input.y + camera.right * input.x);
Vector3 projected = Vector3.ProjectOnPlane(moveDir, surfaceNormal).normalized;
transform.position += projected * climbSpeed * Time.deltaTime;
```

Prevent climbing past edges by rechecking top/bottom boundaries.

---

## **88.9 Ladder & Rope**

- Ladder: constrain movement along ladder’s up axis; snap to rungs if needed.
    
- Rope: allow swing physics (optional) or constrain movement along rope with lateral sway visuals.
    

Ladder logic:

```csharp
void ClimbLadder(float verticalInput)
{
    Vector3 up = ladderTransform.up;
    transform.position += up * verticalInput * ladderSpeed * Time.deltaTime;
    animator.SetFloat("LadderSpeed", verticalInput);
}
```

---

## **88.10 Stamina & Exhaustion**

- Drain stamina while climbing; show UI.
    
- If stamina <= 0, start slip timer → forced drop.
    
- Regain stamina when grounded.
    

```csharp
stamina -= climbable.staminaDrain * Time.deltaTime;
if (stamina <= 0) StartCoroutine(SlipAndDrop());
```

---

## **88.11 Animation & IK Integration**

- Use **Animation Rigging**: two-bone IK for hands, aim constraints for torso.
    
- While on surface, set IK targets from `handPoints` or sampled surface contact points.
    
- Smooth IK weight with `Mathf.Lerp` for transition.
    

Example hand IK update:

```csharp
void UpdateHandIK()
{
    for (int i=0;i<2;i++)
    {
        ikWeights[i] = Mathf.Lerp(ikWeights[i], targetWeight, Time.deltaTime * ikSmooth);
        rigBuilder.Build(); // or set constraint weights
    }
}
```

---

## **88.12 Editor Tools**

Provide a custom `ClimbableEditor`:

- Visualize `handPoints` and top edges.
    
- Bake snap points automatically using mesh sampling.
    
- Allow painting of climbable areas.
    

---

## **88.13 Networking Considerations**

- Server authoritative: server validates ledge detection and climb start events.
    
- Clients send `RequestStartClimbServerRpc` with hit info; server responds with confirmed position and spawns climb state.
    
- Interpolate transform locally for smooth visuals.
    

---

## **88.14 Edge Cases & Robustness**

- Multiple ledges in quick succession: queue actions and block conflicting transitions.
    
- Moving platforms: use parent transform or compensate final position by adding platform velocity.
    
- Animator mismatches: use root motion blending to align world-space transforms.
    
- Wall normals with concave geometry: sample multiple points to find stable hang region.
    

---

## **88.15 Example: Full Climb Controller (Simplified)**

```csharp
public class ClimbController : MonoBehaviour
{
    public LayerMask climbLayer;
    public float climbSpeed = 2f;
    public float hangOffset = 0.5f;
    public float ledgeCheckHeight = 1.5f;
    public float sphereRadius = 0.3f;
    public float maxGripAngle = 60f;

    CharacterController controller;
    Animator animator;
    ClimbState state = ClimbState.None;

    void Awake() { controller = GetComponent<CharacterController>(); animator = GetComponent<Animator>(); }

    void Update()
    {
        if (state == ClimbState.None && Input.GetButtonDown("Grab"))
        {
            if (DetectLedge(out Vector3 hangPoint, out Vector3 normal))
                StartLedgeHang(hangPoint, normal);
        }
        else if (state == ClimbState.Hang)
        {
            if (Input.GetButtonDown("Jump")) StartClimbUp();
            if (Input.GetAxis("Horizontal") != 0) Shimmy(Input.GetAxis("Horizontal"));
            if (Input.GetButtonDown("Drop")) DropFromLedge();
        }
        else if (state == ClimbState.Surface)
        {
            float v = Input.GetAxis("Vertical"), h = Input.GetAxis("Horizontal");
            MoveOnSurface(h, v);
        }
    }

    // DetectLedge/StartLedgeHang/StartClimbUp/... (implementations as above)
}
```

---

## **88.16 Testing & Tuning**

- Playtest with multiple geometry shapes and scales.
    
- Provide designer-exposed values for reach distance and offsets.
    
- Use debug draw to visualize detection rays and snap points (`Debug.DrawLine`, `Gizmos`).
    
- Profile stamina drain and climbing physics on target hardware.
    

---

## **88.17 Extensions**

- Add **climbable enemies** (grab and throw mechanics).
    
- Add **parkour combos** chaining wall run → ledge grab → mantle.
    
- Add **grappling hook** integration (see later section).
    
- Procedural pathfinding for AI to climb surfaces.
    

---

# **89. ADVANCED MOVEMENT PHYSICS (GRAPPLING HOOK, ZIPLINE, GRAVITY MANIPULATION, GRAPPLING SWING)**

---

## **89.1 Grappling Hook Overview**

Core mechanics:

- Aim and shoot grappling hook
    
- Detect hit point
    
- Attach rope (visually and physically)
    
- Pull player or swing around anchor
    
- Detach and recover
    

Two implementation flavors:

1. **Kinematic pull** — move player toward point with physics-like trajectory
    
2. **Physics swing** — use `Rigidbody` + `ConfigurableJoint` or `DistanceJoint` for pendulum physics
    

---

## **89.2 Simple Grapple (Kinematic Pull)**

```csharp
public class Grapple : MonoBehaviour
{
    public LineRenderer rope;
    public float speed = 20f;
    public Transform cam;
    bool isGrappling;
    Vector3 grapplePoint;

    void Update()
    {
        if (Input.GetButtonDown("Fire2"))
            TryGrapple();

        if (isGrappling)
            GrappleMove();
    }

    void TryGrapple()
    {
        if (Physics.Raycast(cam.position, cam.forward, out RaycastHit hit, 50f))
        {
            grapplePoint = hit.point;
            isGrappling = true;
            rope.positionCount = 2;
        }
    }

    void GrappleMove()
    {
        Vector3 dir = (grapplePoint - transform.position).normalized;
        controller.Move(dir * speed * Time.deltaTime);

        rope.SetPosition(0, transform.position);
        rope.SetPosition(1, grapplePoint);

        if (Vector3.Distance(transform.position, grapplePoint) < 2f)
            StopGrapple();
    }

    void StopGrapple() { isGrappling = false; rope.positionCount = 0; }
}
```

Pros: simple, deterministic.  
Cons: feels less dynamic than swinging.

---

## **89.3 Physics Grapple (Pendulum Swing)**

Use `Rigidbody` + `SpringJoint/ConfigurableJoint`:

```csharp
void StartPhysicsGrapple(Vector3 point)
{
    GameObject hook = new GameObject("GrappleJoint");
    var joint = hook.AddComponent<ConfigurableJoint>();
    joint.connectedAnchor = point;
    joint.xMotion = joint.yMotion = joint.zMotion = ConfigurableJointMotion.Limited;
    var linearLimit = new SoftJointLimit { limit = Vector3.Distance(transform.position, point) };
    joint.linearLimit = linearLimit;
    // attach to player rigidbody
    joint.connectedBody = null;
    joint.anchor = Vector3.zero;
    // apply initial velocity for swing
    rb.AddForce((transform.right + transform.forward) * initialImpulse, ForceMode.Impulse);
}
```

Use a `LineRenderer` to draw rope; optionally simulate slack with multiple segments or a Verlet rope.

---

## **89.4 Zipline**

- When player attaches to zipline node, constrain movement along spline between nodes.
    
- Use parametric t 0→1 to move player along line.
    
- Allow jump-off with momentum preserved.
    

```csharp
IEnumerator UseZipline(Vector3 a, Vector3 b)
{
    float t = 0;
    while (t < 1f)
    {
        t += Time.deltaTime * zipSpeed;
        transform.position = Vector3.Lerp(a, b, t);
        yield return null;
    }
    EndZipline();
}
```

---

## **89.5 Grapple Physics Considerations**

- Adjust physics `drag` while swinging to avoid runaway velocities.
    
- Use collision layers to prevent rope colliding with player.
    
- Snapshot anchor positions for moving anchors (e.g., swinging from moving crane).
    

---

## **89.6 Input & Camera Assistance**

- Slow motion while aiming grapple for precision (optional).
    
- Auto-align camera toward grapple target.
    
- Provide visual indicator for valid grapple targets.
    

---

## **89.7 Safety & Edge Cases**

- If grapple hits thin geometry, ignore and find closest solid point.
    
- If anchor point moves (e.g., vehicle), update joint anchor.
    
- Allow cancel with detachment input; re-enable player control and preserve momentum.
    

---

## **89.8 Hook Return & Reuse**

- Implement hook prefab pooling.
    
- Attach hook with a simulated projectile (rigidbody) to allow hitting moving targets.
    

---

# **90. MELEE COMBAT SYSTEM (SOULS-LIKE / ACTION RPG FULL DESIGN)**

---

## **90.1 Goals**

- Responsive inputs with buffered commands.
    
- Combo chains with window timing.
    
- Parry & riposte.
    
- Stamina gating and exhaustion.
    
- Hit detection with precise frames.
    
- Root motion attacks & collision-driven hit detection.
    
- Hit reaction blending and stagger thresholds.
    
- Weapon stats driven by ScriptableObjects.
    
- Blocking and directional blocking.
    

---

## **90.2 Data-Driven Weapon System**

```csharp
[CreateAssetMenu(menuName="Combat/Weapon")]
public class WeaponData : ScriptableObject
{
    public string weaponName;
    public float damage;
    public float staminaCost;
    public float attackCooldown;
    public AnimationClip[] comboClips;
    public bool usesRootMotion;
}
```

---

## **90.3 Weapon Hit Detection Approaches**

1. **Collider-based hitboxes** (enable during swing) — accurate and simple.
    
2. **Raycast / CapsuleCast** from weapon origin — good for fast projectiles.
    
3. **Animation Events** to spawn hit checks at specific frames — tight synchronization.
    

Collider-based example:

- Weapon has child `Hitbox` collider (disabled).
    
- On attack, enable hitbox at hit frames; on trigger, apply damage.
    

```csharp
void EnableHitbox() { hitbox.enabled = true; }
void DisableHitbox() { hitbox.enabled = false; }

void OnTriggerEnter(Collider col)
{
    if (col.TryGetComponent<Health>(out var h))
    {
        h.TakeDamage(currentWeapon.damage);
    }
}
```

---

## **90.4 Combo & Input Buffering**

```csharp
float lastInputTime;
float comboTimer = 0f;
int comboIndex = 0;

void Update()
{
    if (Input.GetMouseButtonDown(0))
    {
        lastInputTime = Time.time;
        TryQueueAttack();
    }

    if (comboIndex > 0)
    {
        if (Time.time - lastAttackTime > comboWindow) ResetCombo();
    }
}

void TryQueueAttack()
{
    if (canAttack)
    {
        StartAttack();
    }
    else
    {
        buffered = true;
    }
}
```

Animation events call `OnAttackWindow()` to accept buffered inputs.

---

## **90.5 Parry & Riposte**

- Parry window: short window after block input; successful parry staggers enemy.
    
- On success: play riposte animation; apply heavy damage.
    

---

## **90.6 Blocking & Damage Reduction**

- Blocking reduces incoming damage; directional blocking uses shield orientation.
    
- Use collision normals + block facing to determine effective block.
    

```csharp
Vector3 toAttacker = (attacker.position - transform.position).normalized;
float angle = Vector3.Angle(transform.forward, toAttacker);
if (angle < blockAngle) // successful block
    damage *= blockDamageMultiplier;
```

---

## **90.7 Stamina Gate**

- Every attack uses stamina.
    
- Exhaustion prevents actions; triggers stagger.
    
- Regenerate stamina over time.
    

---

## **90.8 Hit Reactions & Knockback**

- Apply additive hit reaction animation on upper-body layer with mask.
    
- For strong hits, transition to partial ragdoll or full ragdoll using routines from Ragdoll section.
    
- Use physics impulse on root or hit bone.
    

---

## **90.9 Lock-On & Camera Assist**

- Lock-on system selects target; camera orients to maintain view.
    
- Lock-on affects attack direction and combo targeting.
    

---

## **90.10 AI Combat Considerations**

- AI uses attack windows, telegraphed animations.
    
- Use utility AI to choose attack based on distance, stamina, and state.
    
- Use NavMesh for positioning + tactical movement (sidestep, flank, retreat).
    

---

## **90.11 Example: Simple Melee Attack Flow**

```csharp
public void StartAttack()
{
    if (stamina < currentWeapon.staminaCost) return;
    stamina -= currentWeapon.staminaCost;
    animator.SetTrigger("Attack");
    canAttack = false;
    StartCoroutine(AttackCooldown(currentWeapon.attackCooldown));
}

IEnumerator AttackCooldown(float cd)
{
    yield return new WaitForSeconds(cd);
    canAttack = true;
}
```

`EnableHitbox`/`DisableHitbox` are called via animation events during swing frames.

---

## **90.12 Balancing & Tools**

- Provide editor windows for testing combo timings.
    
- Expose curves for stamina drain and recovery.
    
- Use ScriptableObjects for weapon sets; designer can tweak without code.
    

---

# **91. DYNAMIC LOCOMOTION & PROCEDURAL FOOTSTEP/FOOT PLACEMENT**

---

## **91.1 Dynamic Foot Placement (IK)**

- Raycast from foot to ground to find proper target.
    
- Use two-bone IK to place foot transform.
    
- Adjust pelvis height to prevent leg over-extension.
    

Example (simplified):

```csharp
void UpdateFoot(Transform foot, ref float footIKWeight)
{
    if (Physics.Raycast(foot.position + Vector3.up, Vector3.down, out RaycastHit hit, footMaxCheck, groundLayer))
    {
        Vector3 targetPos = hit.point + Vector3.up * footOffset;
        Quaternion targetRot = Quaternion.FromToRotation(Vector3.up, hit.normal);
        foot.position = Vector3.Lerp(foot.position, targetPos, Time.deltaTime * footIKSpeed);
        foot.rotation = Quaternion.Slerp(foot.rotation, targetRot, Time.deltaTime * footIKSpeed);
        footIKWeight = 1f;
    }
    else footIKWeight = 0f;
}
```

---

## **91.2 Procedural Turning & Pivot**

- Detect when player changes direction while moving.
    
- Play pivot animation when angle > threshold.
    
- Smoothly blend root rotation with animation.
    

---

## **91.3 Footstep System with Surface Detection**

- Use `Physics.Raycast` to sample surface under foot.
    
- Play different sounds for different materials via `PhysicMaterial` or `TerrainLayer`.
    

```csharp
void PlayFootstep()
{
    RaycastHit hit;
    if (Physics.Raycast(transform.position, Vector3.down, out hit, 1.5f))
    {
        var mat = hit.collider.sharedMaterial;
        AudioManager.I.PlayFootstepSound(mat);
    }
}
```

---

# **92. TESTING, DEBUGGING, TOOLS & EDITOR WIZARDS**

---

## **92.1 Debug Visualizations**

- `Gizmos` for detection rays, hang points, anchor points.
    
- Runtime toggles to visualize internal states.
    
- `OnDrawGizmosSelected` for per-object debugging.
    

Example:

```csharp
void OnDrawGizmos()
{
    Gizmos.color = Color.green;
    Gizmos.DrawSphere(hangPoint, 0.05f);
}
```

---

## **92.2 Automated Playtesting Tools**

- Create automated test harnesses that run gameplay loops and record metrics.
    
- Use headless play mode or editor tests via Unity Test Runner.
    

---

## **92.3 Editor Tools to Quilt Level Geometry**

- Create paint tools for `Climbable` areas.
    
- Bake common grab points per prefab.
    
- Bulk assign PhysicMaterials and layer masks.
    

---

## **92.4 Profiling & Optimization Checklist**

- Use Unity Profiler for CPU/GPU hotspots.
    
- Use Frame Debugger for draw call and batching issues.
    
- For physics-heavy movement (grapples, ropes), limit joint counts and use simplified colliders.
    
- Pool temporary objects (hooks, VFX, ragdolls).
    
- Limit animator layers & masked blend weights on mobile.
    

---

# **93. PRODUCTION NOTES, QA, & Polishing**

- Gather playtest feedback on feel: input latency, responsiveness, edge-case reliability.
    
- Add assistive systems: ledge auto-grab tuning, elasticity for forgiven grabs.
    
- Implement tutorial prompts for complex moves.
    
- Provide robust fallback behavior when stuck (teleport to nearest safe point).
    
- Implement undo safety for editor tools.
    

---

Understood.  
I will now **finish the entire document** by adding **Section 94 → Section 100**, covering **the MOST IMPORTANT Unity C# and Unity-specific topics** that any real developer must know before calling the document complete.

These will be deep, structured, professional, practical, and Unity-specific—not generic C#.

This will **wrap up the full document**.

---

# **94. UNITY EVENT SYSTEMS, SCRIPTABLE ARCHITECTURE, AND DECOPLED GAMEPLAY CODE**

---

## **94.1 Why Events Matter**

Unity beginners write everything in Update() and drag references into fields.  
This causes:

- messy dependencies
    
- spaghetti architecture
    
- hard-to-scale systems
    

Event-driven systems solve this.

Unity supports:

- C# events
    
- UnityEvents
    
- ScriptableObject events (GameEvent pattern)
    
- Messaging systems
    
- Observer pattern
    
- Interface-based callbacks
    
- Custom event buses
    

---

## **94.2 C# Events in Unity**

```csharp
public static class GameEvents
{
    public static event System.Action<int> OnEnemyKilled;

    public static void EnemyKilled(int id)
    {
        OnEnemyKilled?.Invoke(id);
    }
}
```

Usage:

```csharp
void OnEnable()
{
    GameEvents.OnEnemyKilled += HandleDeath;
}

void HandleDeath(int id)
{
    score++;
}
```

---

## **94.3 UnityEvent — Editor-attachable events**

```csharp
[System.Serializable]
public class HealthEvent : UnityEngine.Events.UnityEvent<float> { }

public class Health : MonoBehaviour
{
    public HealthEvent OnHealthChanged;
}
```

Allows designers to attach functions in the inspector.

---

## **94.4 ScriptableObject Event System**

Create “GameEvent” asset:

```csharp
[CreateAssetMenu]
public class GameEvent : ScriptableObject
{
    private readonly List<GameEventListener> listeners = new();

    public void Raise()
    {
        for (int i = listeners.Count - 1; i >= 0; i--)
            listeners[i].OnEventRaised();
    }

    public void Register(GameEventListener listener) => listeners.Add(listener);
    public void Unregister(GameEventListener listener) => listeners.Remove(listener);
}
```

Listener:

```csharp
public class GameEventListener : MonoBehaviour
{
    public GameEvent gameEvent;
    public UnityEvent response;

    void OnEnable() => gameEvent.Register(this);
    void OnDisable() => gameEvent.Unregister(this);

    public void OnEventRaised() => response.Invoke();
}
```

Used to entirely remove dependencies.

---

## **94.5 Interface Events (High-performance)**

Combat example:

```csharp
public interface IDamageable
{
    void TakeDamage(float amount);
}
```

Any object can implement this.  
Use:

```csharp
if (hit.collider.TryGetComponent<IDamageable>(out var dmg))
    dmg.TakeDamage(50);
```

Clean, fast, scalable.

---

## **94.6 The “Game Architecture Triangle”**

Any system in Unity should use:

**Events → ScriptableObjects → Components**

This produces:

- clean architecture
    
- complete decoupling
    
- maximum reusability
    

---

# **95. ADDRESSABLES, ASSET MANAGEMENT, & STREAMING CONTENT**

---

## **95.1 Why Addressables Matter**

Addressables allow:

- runtime loading/unloading assets
    
- asset versioning
    
- remote CDN content
    
- reducing build size
    
- reducing memory usage
    
- loading screens/async scenes
    
- multi-platform compatible packaging
    

Absolutely REQUIRED for:

- large games
    
- asset-heavy projects
    
- mobile games
    
- modding support
    

---

## **95.2 Basic Addressable Loading**

```csharp
using UnityEngine.AddressableAssets;

public class EnemyLoader : MonoBehaviour
{
    public AssetReference enemyPrefab;

    async void Start()
    {
        GameObject enemy = await enemyPrefab.InstantiateAsync(transform.position, Quaternion.identity).Task;
    }
}
```

---

## **95.3 Releasing Assets**

```csharp
Addressables.ReleaseInstance(enemy);
```

Not releasing causes memory leaks.

---

## **95.4 Labels**

Tag groups of content:

- “Characters”
    
- “Enemies”
    
- “Weapons”
    
- “Maps”
    

Load entire sets:

```csharp
Addressables.LoadAssetsAsync<GameObject>("Enemies", null);
```

---

## **95.5 Remote Content**

Allows updates without pushing game patches.

Configuration:

- Build → Addressables Groups → Remote Build Path / Load Path
    
- Upload to CDN
    
- Update catalog via versioning
    

Then game loads new content automatically.

---

## **95.6 Asset Bundles vs Addressables**

- Asset bundles = manual
    
- Addressables = automated & production ready  
    Use Addressables always.
    

---

# **96. MOBILE DEVELOPMENT (PERFORMANCE, MEMORY, TOUCH INPUT)**

---

## **96.1 Optimization Rules for Mobile**

1. Limit draw calls (use SRP batcher, GPU instancing).
    
2. Use compressed textures (ASTC).
    
3. Avoid large physics simulations.
    
4. Avoid Garbage Collection spikes (Object pooling).
    
5. Prefer baked lighting.
    
6. Use simple shaders (mobile-friendly).
    
7. Limit real-time lights.
    
8. Reduce bone counts in characters.
    

---

## **96.2 Touch Controls**

Touch input example:

```csharp
if (Input.touchCount > 0)
{
    Touch t = Input.GetTouch(0);
    if (t.phase == TouchPhase.Began)
        OnTouchStart(t.position);
}
```

Swipe detection:

```csharp
Vector2 delta = t.position - startPos;
```

Pinch detection:

```csharp
float dist = Vector2.Distance(t1.position, t2.position);
```

---

## **96.3 Mobile Build Settings**

- Use IL2CPP + ARM64
    
- Enable “Strip Engine Code”
    
- Enable “Managed Stripping Level: High”
    
- Avoid multi-threaded rendering on some older devices
    
- Use texture streaming
    

---

## **96.4 Memory Debugging**

Use:

- Memory Profiler
    
- Frame Debugger
    
- Unity Profiler
    

Look for:

- Unreleased addressables
    
- Large textures
    
- Unnecessary audio clips
    
- Mesh duplication
    

---

# **97. CONSOLE/PC OPTIMIZATION, PLATFORM TARGETING, AND BUILD CONFIGURATIONS**

---

## **97.1 PC vs Console Differences**

PC:

- unlimited resolutions
    
- variable frame rate
    
- GPU heavy
    
- lots of RAM
    

Consoles:

- fixed resolution targets
    
- strict memory limits
    
- strict CPU budgets
    
- strict certification requirements
    

---

## **97.2 Memory Limits**

Examples:

- Nintendo Switch: ~3 GB usable
    
- PS4: ~5–6 GB usable
    

You must test memory aggressively.

---

## **97.3 Graphics Optimization**

- Avoid complex shaders on Switch
    
- Use single directional light
    
- Baked shadows
    
- Low poly count meshes
    
- Use GPU instancing
    

---

## **97.4 Build Configurations**

Use preprocessor directives:

```csharp
#if UNITY_PS4
    // PS4 code
#elif UNITY_SWITCH
    // Switch code
#endif
```

Used for platform-specific logic.

---

# **98. BUILD PIPELINES, AUTOMATION, CI/CD, CLOUD BUILDS**

---

## **98.1 Build Automation**

Use Unity’s CLI:

```bash
unity -quit -batchmode -projectPath PROJECT -executeMethod BuildScript.PerformBuild
```

Build script example:

```csharp
public static class BuildScript
{
    public static void PerformBuild()
    {
        BuildPipeline.BuildPlayer(
            new[] {"Assets/Scenes/Main.unity"},
            "Build/Game.exe",
            BuildTarget.StandaloneWindows64,
            BuildOptions.None
        );
    }
}
```

---

## **98.2 Automatic Versioning**

Increment version:

```csharp
PlayerSettings.bundleVersion = "1.0." + buildNumber;
```

---

## **98.3 Unity Cloud Build**

Advantages:

- Multiple platforms simultaneously
    
- Automatic builds per commit
    
- Artifact storage
    
- Automated testing
    

---

## **98.4 GitHub Actions**

Automate builds using Docker Unity images.

---

# **99. AUTOMATED TESTING, QA, AND DEBUGGING**

---

## **99.1 Unit Tests**

Use NUnit:

```csharp
[Test]
public void HealthTest()
{
    var h = new Health();
    h.ApplyDamage(10);
    Assert.AreEqual(90, h.hp);
}
```

---

## **99.2 PlayMode Tests**

Automated gameplay sequences:

- Player movement tests
    
- UI flow tests
    
- Level-loading tests
    

---

## **99.3 Tools**

- Debug overlays
    
- Frame rate display
    
- Hitbox visualization
    
- Physics debug toggles
    
- Logging systems with color coding
    

---

## **99.4 Bug Categories in Unity**

- Race conditions in Update/LateUpdate
    
- Animation desync
    
- Physics tunneling
    
- Incorrect layer masks
    
- Script execution order issues
    
- Memory leaks from addressables
    
- GC spikes from allocations
    

---

# **100. FINAL PRODUCTION CHECKLIST & COMPLETE SUMMARY**

---

## **100.1 Production Checklist**

### **Core Systems**

☑ Complete movement system  
☑ Climbing / Parkour  
☑ Combat  
☑ Animation system  
☑ Camera system  
☑ UI  
☑ Saving/Loading  
☑ Game state management  
☑ Scene management  
☑ Audio

---

### **Code Architecture**

☑ Event-driven architecture  
☑ ScriptableObject data layers  
☑ Component decoupling  
☑ No circular dependencies  
☑ No hard-coded references  
☑ Object pooling

---

### **Optimization**

☑ GPU batch-friendly setup  
☑ Audio compression  
☑ Texture compression  
☑ Culling systems  
☑ Physics optimization  
☑ Remove unused assets  
☑ Addressables enabled

---

### **Platform Prep**

☑ Platform dependent compilation  
☑ Memory usage within limits  
☑ Platform-specific input handling

---

### **Testing**

☑ Automated tests  
☑ Manual functional tests  
☑ Device tests (mobile)  
☑ Console certification tests (if applicable)

---

### **Build Pipeline**

☑ Auto versioning  
☑ Cloud build  
☑ CI/CD  
☑ Deployment packaging

---
