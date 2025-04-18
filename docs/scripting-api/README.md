# Unity 6 Scripting API

This section provides comprehensive documentation for the Unity 6 scripting API, including namespaces, classes, methods, and properties.

## Core Scripting Concepts

Unity 6 uses C# as its primary scripting language. Key scripting concepts include:

- MonoBehaviour lifecycle (Awake, Start, Update, etc.)
- Coroutines and async/await
- Events and delegates
- Unity's serialization system
- Prefab instantiation and management
- Scene management

## New in Unity 6

Unity 6 introduces several new scripting features and improvements:

### Enhanced C# Support
- Full C# 10.0 support
- Improved .NET compatibility
- Better IDE integration
- Enhanced runtime performance

### ECS Scripting
- JobSystem for multithreaded code
- Burst compiler for high-performance C# code
- Entity query system
- Component data manipulation

### Async/Await Integration
- First-class support for async/await
- Integration with Unity's event system
- Performance optimizations for async operations
- Background task management

## Namespaces

### UnityEngine
Core functionality for interacting with the Unity engine.

### UnityEngine.UI
Classes for creating and manipulating user interfaces.

### Unity.Entities
Core ECS functionality.

### Unity.Mathematics
High-performance math library optimized for SIMD operations.

### Unity.Collections
Data containers designed for high-performance scenarios.

### Unity.Jobs
Job system for multithreaded code execution.

### Unity.Physics
Physical simulation components and systems.

### Unity.Rendering
Rendering-related components and systems.

## Common Classes

### Transform
```csharp
// Get the position of a GameObject
Vector3 position = gameObject.transform.position;

// Set the position of a GameObject
gameObject.transform.position = new Vector3(1, 2, 3);

// Rotate a GameObject
gameObject.transform.Rotate(0, 30, 0);
```

### GameObject
```csharp
// Create a new GameObject
GameObject newObject = new GameObject("MyObject");

// Find a GameObject by name
GameObject foundObject = GameObject.Find("Player");

// Instantiate a prefab
GameObject instance = Instantiate(prefab, position, rotation);
```

### Component
```csharp
// Add a component to a GameObject
Rigidbody rb = gameObject.AddComponent<Rigidbody>();

// Get a component from a GameObject
Collider col = gameObject.GetComponent<Collider>();

// Check if a GameObject has a specific component
bool hasAnimator = gameObject.TryGetComponent(out Animator animator);
```

## ECS Example

```csharp
// Define a component (pure data)
public struct HealthComponent : IComponentData
{
    public float Value;
    public float MaxValue;
}

// Create a system to process entities with HealthComponent
public partial class HealthSystem : SystemBase
{
    protected override void OnUpdate()
    {
        float deltaTime = Time.DeltaTime;
        
        // Query for all entities with a HealthComponent
        Entities
            .ForEach((ref HealthComponent health) => 
            {
                // Regenerate health over time
                if (health.Value < health.MaxValue)
                {
                    health.Value = math.min(health.Value + (deltaTime * 5f), health.MaxValue);
                }
            })
            .ScheduleParallel();
    }
}
```

## Next Steps

- Explore [Animation](../animation/README.md) scripting
- Learn about [Physics](../physics/README.md) programming
- Check out [UI](../ui/README.md) development