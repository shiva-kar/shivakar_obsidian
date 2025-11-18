## 📦 Installation & Environment Setup

### .NET SDK & Runtime

- Download: [https://dotnet.microsoft.com/download](https://dotnet.microsoft.com/download)
    
- Check version:
    
    ```bash
    dotnet --info
    ```
    
- Install on all OS: Windows, macOS, Linux
    
- SDK includes CLI, compiler (`csc`), runtime, MSBuild
    

### IDEs

- Visual Studio (full-featured)
    
- Visual Studio Code (with **C# Dev Kit** + **IntelliCode**)
    
- JetBrains Rider
    

### CLI Basics

```bash
dotnet new console -n MyApp
cd MyApp
dotnet run
dotnet build
dotnet add package Newtonsoft.Json
```

---

## 1. First Program

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```

- Entry point: `Main` method
    
- Compile with: `dotnet build` or `csc Program.cs`
    
- Output: `.dll` or `.exe` depending on project type
    

---

## 2. Data Types & Variables

**Value types:** `int`, `float`, `double`, `decimal`, `bool`, `char`, `struct`  
**Reference types:** `string`, `object`, `class`, `array`, `delegate`  
**Nullable types:** `int? age = null;`  
**Type inference:** `var x = 42;`  
**Const & Readonly:**

```csharp
const double PI = 3.14159;
readonly DateTime created = DateTime.Now;
```

---

## 3. Operators

Arithmetic, assignment, comparison, logical, bitwise, shift.  
C#-specific:

- Null-coalescing: `??`, null-conditional: `?.`, null-coalescing-assignment: `??=`
    
- Pattern matching: `is`, `switch` expressions
    

```csharp
int? a = null;
int b = a ?? 10;
Console.WriteLine(b);
```

---

## 4. Control Flow

`if`, `else if`, `else`, `switch`, `for`, `foreach`, `while`, `do`, `break`, `continue`, `goto`  
C# 8+: enhanced `switch` expressions.

```csharp
var result = x switch
{
    > 0 => "positive",
    0 => "zero",
    _ => "negative"
};
```

---

## 5. Methods

- Overloading, optional parameters, named arguments
    
- Parameter modifiers: `ref`, `out`, `in`, `params`
    
- Local functions allowed inside methods
    

```csharp
void Swap(ref int a, ref int b) { (a, b) = (b, a); }
int Sum(params int[] n) => n.Sum();
```

---

## 6. Classes & Objects

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```

- Access modifiers: `public`, `private`, `protected`, `internal`, `protected internal`, `private protected`
    
- Constructors / destructors
    
- Static members, `this`, object initializers
    

---

## 7. Interfaces

Interfaces define contracts, allow polymorphism.  
C# 8+: default implementations allowed.

```csharp
public interface ILogger
{
    void Log(string msg);
    void Warn(string msg) => Console.WriteLine("WARN: " + msg);
}
```

---

## 8. Inheritance & Polymorphism

`virtual`, `override`, `sealed`, abstract members.

```csharp
public abstract class Shape { public abstract double Area(); }
public class Circle : Shape { public double R; public override double Area() => Math.PI * R * R; }
```

---

## 9. Structs, Records & Immutability

- `struct` → value type
    
- `record` → reference type with immutability
    
- `record struct` → value type record
    

```csharp
public record User(string Name, int Age);
public readonly struct Point(int X, int Y);
```

C# 12+ supports **primary constructors for all types**:

```csharp
class Product(string Name, decimal Price) { }
```

---

## 10. Properties & Indexers

```csharp
public class Box
{
    public int Width { get; set; }
    public int Height { get; set; }
    public int Area => Width * Height;
}
```

Indexers:

```csharp
class Data
{
    private int[] arr = new int[10];
    public int this[int i] { get => arr[i]; set => arr[i] = value; }
}
```

---

## 11. Delegates, Lambdas, Events

Delegates = type-safe function pointers.

```csharp
delegate void Notify(string msg);
Notify n = Console.WriteLine;
n("Hello!");
```

Lambda expressions:

```csharp
Func<int,int,int> add = (x,y)=>x+y;
```

Events:

```csharp
public event Action<int>? OnThreshold;
```

---

## 12. Generics

```csharp
class Box<T>
{
    public T Value { get; set; }
}
```

Constraints:

```csharp
where T : class, new()
```

Generic interfaces, delegates, and methods supported.

---

## 13. Collections

- `List<T>`, `Dictionary<K,V>`, `HashSet<T>`, `Queue<T>`, `Stack<T>`
    
- Immutable collections: `System.Collections.Immutable`
    
- `Span<T>` for memory-safe slicing
    
- `foreach` iterates any `IEnumerable<T>`
    

---

## 14. LINQ

Language Integrated Query for data manipulation.

```csharp
var result = numbers.Where(x => x > 5)
                    .OrderBy(x => x)
                    .Select(x => x * x);
```

- Deferred execution
    
- Query syntax:
    

```csharp
from n in numbers where n>5 select n*n;
```

- Custom query providers possible (Entity Framework, LINQ-to-SQL)
    

---

## 15. Exception Handling

```csharp
try
{
    throw new InvalidOperationException("Error");
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
finally
{
    Console.WriteLine("Cleanup");
}
```

- Filters: `catch (Exception ex) when (ex.Message.Contains("critical"))`
    
- Custom exception classes derive from `Exception`
    

---

## 16. File I/O

```csharp
using var sr = new StreamReader("data.txt");
string text = sr.ReadToEnd();
```

- `System.IO.File`, `FileStream`, `Directory`, `Path`
    
- Asynchronous I/O: `await File.ReadAllTextAsync("file.txt");`
    

---

## 17. Serialization

- JSON: `System.Text.Json` or `Newtonsoft.Json`
    
- XML: `XmlSerializer`
    
- Binary: `BinaryFormatter` (deprecated, prefer custom serializers)
    

```csharp
var json = JsonSerializer.Serialize(obj);
var data = JsonSerializer.Deserialize<MyType>(json);
```

---

## 18. Reflection & Attributes

```csharp
[AttributeUsage(AttributeTargets.Class)]
class InfoAttribute : Attribute
{
    public string Description { get; }
    public InfoAttribute(string desc) => Description = desc;
}
```

```csharp
var attrs = typeof(MyClass).GetCustomAttributes(false);
```

- Reflection used for runtime type inspection and meta-programming.
    

---

## 19. Assemblies & Metadata

- Assembly = compiled output (.dll or .exe)
    
- Metadata includes type info and manifest
    
- `strong name` = version + public key + hash
    
- View with **ILDASM** or **dotnet ildasm**
    

---

## 20. Project Structure (.csproj)

```xml
<Project Sdk=\"Microsoft.NET.Sdk\">
  <PropertyGroup>
    <TargetFramework>net9.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>
</Project>
```

CLI builds using **MSBuild** under the hood.

---

## 21. NuGet Packages

```bash
dotnet add package Newtonsoft.Json
dotnet restore
```

- Private feeds: add to `NuGet.config`
    
- `dotnet pack` to build `.nupkg`
    
- Use semantic versioning
    

---

## 22. Async / Await

```csharp
async Task<int> GetDataAsync()
{
    await Task.Delay(100);
    return 42;
}
```

- `Task` and `Task<T>` represent async work
    
- Exception handling via `try/catch` inside async
    
- Combine tasks: `await Task.WhenAll(...)`
    

---

## 23. Parallelism & Concurrency

- `Task.Run()`, `Parallel.For()`, `Parallel.ForEach()`
    
- Synchronization primitives: `lock`, `Monitor`, `SemaphoreSlim`
    
- `ConcurrentQueue`, `ConcurrentDictionary`
    
- Cancellation via `CancellationToken`
    

---

## 24. Memory Management & Span

- Managed by GC (Generational garbage collector)
    
- Stack vs Heap allocation
    
- `Span<T>` / `Memory<T>` for high-performance memory access
    
- `stackalloc` for stack-based arrays
    
- `IDisposable` + `using` for deterministic cleanup
    

```csharp
Span<int> s = stackalloc int[3];
s[0] = 1;
```

---

## 25. Pattern Matching

```csharp
if (obj is Person { Age: >18 } adult)
    Console.WriteLine(adult.Name);
```

- Type, property, positional, and relational patterns
    
- Logical pattern composition: `and`, `or`, `not`
    

---

## 26. Operator Overloading

```csharp
public struct Vector(int X, int Y)
{
    public static Vector operator +(Vector a, Vector b) => new(a.X + b.X, a.Y + b.Y);
}
```

---

## 27. Extension Methods

```csharp
public static class Extensions
{
    public static bool IsEven(this int n) => n % 2 == 0;
}
```

---

## 28. Interop & Unsafe Code

```csharp
[DllImport(\"user32.dll\")] static extern int MessageBox(IntPtr h, string text, string caption, int type);
MessageBox(IntPtr.Zero, \"Hi\", \"Title\", 0);
```

- Use with care. `unsafe` requires `/unsafe` compiler flag.
    

---

## 29. Security & Cryptography

- Hashing: `SHA256.Create()`
    
- Symmetric encryption: `Aes.Create()`
    
- Asymmetric: `RSA.Create()`
    
- Certificates: `X509Certificate2`
    
- Secure storage via **Azure Key Vault**, **User Secrets**
    

---

## 30. Networking

- HTTP: `HttpClient`, `HttpRequestMessage`
    
- WebSocket: `System.Net.WebSockets`
    
- Sockets: `System.Net.Sockets` for TCP/UDP
    

```csharp
using var client = new HttpClient();
var html = await client.GetStringAsync(\"https://dot.net\");
```

---

## 31. Regular Expressions

```csharp
var m = Regex.Match(\"abc123\", \"(\\d+)\");
```

- `RegexOptions.Compiled` improves performance.
    

---

## 32. Testing & Tooling

- xUnit, NUnit, MSTest
    
- Mocking: Moq, NSubstitute
    
- Benchmarking: BenchmarkDotNet
    
- Code analyzers: Roslyn, StyleCop, FxCop
    

---

## 33. ASP.NET Core (Overview)

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet(\"/\", () => \"Hello C#\");
app.Run();
```

- Middleware pipeline
    
- Dependency Injection (built-in)
    
- Minimal APIs, Razor Pages, MVC Controllers, Blazor
    

---

## 34. Entity Framework Core

- `DbContext`, `DbSet<T>`
    
- Migrations: `dotnet ef migrations add Init`
    
- LINQ for queries
    
- Supports SQLite, PostgreSQL, SQL Server, MySQL, InMemory
    

---

## 35. Blazor / MAUI / WPF / WinForms

- **Blazor Server/WASM:** Web UI using C# instead of JS
    
- **MAUI:** cross-platform native apps
    
- **WPF:** XAML-based desktop
    
- **WinForms:** legacy desktop UI
    
- Data binding, MVVM, dependency injection
    

---

## 36. Roslyn & Source Generators

```csharp
[Generator]
public sealed class AutoGen : ISourceGenerator
{
    public void Initialize(GeneratorInitializationContext context)
    {
        // nothing to initialize for this simple generator
    }

    public void Execute(GeneratorExecutionContext context)
    {
        const string src = "public static class Auto { public static string Msg => \"Hello Gen!\"; }";
        context.AddSource("auto.g.cs", SourceText.From(src, Encoding.UTF8));
    }
}

```

---

## 37. Modern C# Features (C# 10 – C# 12 – C# 13 Preview)

### Top-Level Statements

```csharp
Console.WriteLine("Hello World");
```

No need for a class or `Main`.

### File-Scoped Namespaces

```csharp
namespace Demo;
class Program { }
```

### Global Usings

```csharp
global using System;
global using System.Collections.Generic;
```

### Record Structs and With-Expressions

```csharp
public readonly record struct Point(int X, int Y);
var p2 = p1 with { X = 10 };
```

### Pattern Matching Additions

- `or`, `and`, `not` logical patterns
    
- `switch` expressions with `when` guards
    
- List patterns (`[1, 2, .. var rest]`) in C# 11
    
- Collection expressions (`int[] a = [1,2,3];`) in C# 12
    

### Required Members

```csharp
public class Person { public required string Name { get; init; } }
```

### Primary Constructors for All Types

```csharp
class Employee(string Name, int Id);
```

### Default Lambda Parameters

```csharp
var f = (int x = 5) => x * 2;
```

### Interceptors (C# 13 Preview)

Intercept and modify method calls at compile time (experimental).

---

## 38. Diagnostics & Code Analysis

- **Roslyn analyzers**: static code inspection via `Microsoft.CodeAnalysis`
    
- **StyleCop.Analyzers**: enforce conventions
    
- **FxCopAnalyzers**: legacy security/performance rules
    
- Integrate via `.editorconfig` and `<AnalysisLevel>` in `.csproj`
    

```bash
dotnet format
dotnet analyzers
```

---

## 39. Performance & Profiling

### Tools

- `BenchmarkDotNet` — microbenchmarking
    
- `dotnet-trace`, `dotnet-counters`, `PerfView`, `dotnet-dump`
    
- Visual Studio **Performance Profiler**
    
- Memory analyzers: JetBrains dotMemory, VS Diagnostic Tools
    

### Tips

- Use `Span<T>` / `Memory<T>` to avoid allocations
    
- Reuse buffers via `ArrayPool<T>`
    
- Avoid LINQ in critical loops
    
- Prefer structs in hot paths
    
- Use `ValueTask` instead of `Task` for high-frequency methods
    
- Use `sealed` for non-virtual classes to optimize JIT
    

---

## 40. Dependency Injection & IoC

Built into **Microsoft.Extensions.DependencyInjection**.

```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddSingleton<ILogger, ConsoleLogger>();
builder.Services.AddScoped<IRepo, Repo>();
builder.Services.AddTransient<IService, Service>();
```

- **Lifetimes:** Singleton, Scoped, Transient
    
- Avoid service locators; prefer constructor injection.
    
- Extendable with Autofac, Lamar, or SimpleInjector.
    

---

## 41. Logging & Telemetry

- Framework: `Microsoft.Extensions.Logging`
    
- Providers: Console, Debug, EventSource, Serilog, NLog, Seq
    
- Structured logging with Serilog:
    

```csharp
Log.Information("User {Name} logged in", username);
```

Telemetry:

- Application Insights, OpenTelemetry (`OpenTelemetry.Trace`), Prometheus exporters.
    

---

## 42. Configuration System

```csharp
var builder = WebApplication.CreateBuilder(args);
var config = builder.Configuration;
string conn = config["ConnectionStrings:Default"];
```

Supports:

- JSON (`appsettings.json`)
    
- Environment variables
    
- Command-line args
    
- Secret Manager (`dotnet user-secrets`)
    
- Azure Key Vault
    

---

## 43. Entity Framework Core Advanced

- Change tracking, migrations, seeding
    
- Raw SQL queries via `FromSqlRaw()`
    
- Async queries with `ToListAsync()`
    
- Interceptors for logging and caching
    
- Multi-tenant and sharding via context factories
    
- Mapping to views and stored procedures
    

---

## 44. Minimal APIs (Deep Dive)

- Introduced .NET 6
    
- Enables lightweight web endpoints without controllers
    

```csharp
var app = WebApplication.Create();
app.MapGet("/user/{id}", (int id) => new { id, name = "Alice" });
app.Run();
```

- Can use filters, middleware, attributes
    
- Integrates with DI, logging, and EF Core
    

---

## 45. Blazor (Server, WASM, Hybrid)

- Uses **Razor components** (`.razor` files)
    
- Server model: runs on server, updates DOM via SignalR
    
- WASM model: runs in browser via WebAssembly
    
- Shared UI + logic
    
- Components = reusable units (`@code { }` blocks)
    
- Hybrid via MAUI: BlazorWebView control
    

---

## 46. .NET MAUI (Multi-platform App UI)

- Unified project for Android, iOS, macOS, Windows
    
- Based on XAML + C#
    
- Hot reload supported
    
- MVVM or MVU patterns
    
- Integrates with Blazor Hybrid
    

```xml
<Button Text=\"Click\" Clicked=\"OnClick\"/>
```

---

## 47. Windows UI Frameworks

### WPF

- XAML markup
    
- MVVM pattern
    
- Data binding, DependencyProperties, RoutedEvents
    

### WinForms

- Rapid GUI prototyping
    
- Designer-driven
    
- Event-based logic
    

Both supported in .NET 8 + SDK.

---

## 48. Unity & Game Development with C#

- C# used for scripts in **Unity Engine**
    
- Mono runtime with IL2CPP compilation
    
- Coroutines (`IEnumerator`) for async game logic
    
- Key namespaces: `UnityEngine`, `UnityEditor`
    
- ECS (Entity Component System) via DOTS
    

---

## 49. Cloud & DevOps Integration

### Azure

- `Azure.Storage.Blobs`, `Azure.Identity`, `Azure.Messaging.ServiceBus`
    
- Functions runtime: `Microsoft.Azure.Functions.Worker`
    
- ARM / Bicep deployments
    

### AWS

- SDK: `AWSSDK.S3`, `AWSSDK.DynamoDBv2`, `AWSSDK.Lambda`
    

### CI/CD

- GitHub Actions, Azure Pipelines, GitLab CI
    
- Example:
    

```yaml
- name: Build
  run: dotnet build --configuration Release
```

### Containers

- `docker build -t app .`
    
- Use official image `mcr.microsoft.com/dotnet/aspnet:9.0`
    

---

## 50. Cross-Platform & Interop

- P/Invoke for native code
    
- COM interop on Windows
    
- WASI support for WebAssembly System Interface
    
- `NativeAOT` for ahead-of-time compilation
    

```bash
dotnet publish -r win-x64 -p:PublishAot=true
```

---

## 51. AI & ML with C#

- **ML.NET** for local model training and prediction
    
- **ONNX Runtime** integration for pretrained models
    
- **TensorFlow.NET**, **TorchSharp** for deep learning
    
- `System.CommandLine` + `Spectre.Console` for AI CLI tools
    

---

## 52. Source Generators (Advanced Usage)

- Generate DI registrations, API clients, DTOs
    
- Use incremental generators (`IIncrementalGenerator`) for performance
    
- Can read syntax trees and semantic models
    
- Integrate analyzers + generators together
    
- Useful packages: `CommunityToolkit.Mvvm`, `StrongInject`, `MediatR`
    

---

## 53. MediatR & CQRS Pattern

```csharp
public record GetUserQuery(int Id) : IRequest<User>;
public class Handler : IRequestHandler<GetUserQuery, User>
{
    public Task<User> Handle(GetUserQuery q, CancellationToken t) =>
        db.Users.FindAsync(q.Id).AsTask();
}
```

- Separates read/write concerns
    
- Simplifies event-driven architecture
    
- Works with pipelines and decorators
    

---

## 54. Design Patterns Summary

|Category|Patterns|
|---|---|
|Creational|Singleton, Factory, Builder|
|Structural|Adapter, Decorator, Composite|
|Behavioral|Strategy, Observer, Command, Mediator|

---

## 55. Testing & QA Pipeline

- Unit → Integration → End-to-End Tests
    
- Frameworks: xUnit, NUnit, MSTest
    
- Mocking: Moq, NSubstitute
    
- Coverage: `coverlet`, ReportGenerator
    
- CI Integration with GitHub Actions
    

---

## 56. Deployment & Packaging

- `dotnet publish -c Release -r linux-x64 --self-contained`
    
- Single-file executables (`PublishSingleFile=true`)
    
- AOT compilation for fast startup (`PublishAot=true`)
    
- Distribution: NuGet, Docker, MSI installers
    

---

## 57. Localization & Globalization

- `ResourceManager`, `.resx` files
    
- `CultureInfo.CurrentCulture`
    
- `System.Globalization` APIs
    
- `IStringLocalizer<T>` in ASP.NET Core
    

---

## 58. Observability & Metrics

- OpenTelemetry SDK for traces, metrics, logs
    
- Integrate with Prometheus, Grafana, Azure Monitor
    
- `ActivitySource` for custom tracing
    

```csharp
using var activity = MySource.StartActivity("ProcessData");
```

---

## 59. Runtime Internals

- JIT: Tiered compilation, ReadyToRun
    
- GC: Background / Server modes
    
- ThreadPool scheduling
    
- Async I/O based on IOCP or epoll (platform-specific)
    
- Memory layout inspectable via SOS debugger
    

---

## 60. Roadmap and Ecosystem Outlook

- .NET 9 + C# 13 → interceptors, params collections, default lambda params
    
- Native AOT for more platforms
    
- Unified runtime for cloud + desktop + mobile
    
- Incremental builds, AOT crossgen2, more AI interop
    

---

Confirmed. You want the **absolute full professional-level C# reference**, including _everything an advanced developer, architect, or framework engineer might ever need_—from runtime internals and compiler extension points to diagnostics, metaprogramming, interop, and tooling.

I’ll add an **Advanced & Expert Appendix** that covers:

- Roslyn internals and compiler APIs
    
- IL rewriting, runtime hooks, and metadata manipulation
    
- NativeAOT tuning and trimming
    
- GC and JIT profiling
    
- Custom analyzers, code fixes, and source generators
    
- Performance tuning with stack traces and perf counters
    
- Debugger & SOS usage
    
- Reflection.Emit and dynamic assemblies
    
- Plugin and module systems
    
- Threading internals, task scheduling
    
- Advanced memory models and `Volatile` / `Interlocked` APIs
    
- Span safety and stack vs heap tradeoffs
    
- Secure coding and code access security
    
- Reverse engineering protections and obfuscation
    
- Diagnostics & Observability
    
- .NET Runtime configuration knobs
    
- Build automation & MSBuild task authoring
    
- AOT + IL Linker configuration
    
- Profiling and instrumentation APIs
    

---

## 61. Roslyn Internals & Compiler Extensibility

- Compiler exposed via **Microsoft.CodeAnalysis**.
    
- You can parse, analyze, and rewrite syntax trees:
    

```csharp
var tree = CSharpSyntaxTree.ParseText("class A { }");
var root = tree.GetRoot();
var classDecl = root.DescendantNodes().OfType<ClassDeclarationSyntax>().First();
Console.WriteLine(classDecl.Identifier.Text); // A
```

- **SemanticModel** for symbol resolution.
    
- Build analyzers using `DiagnosticAnalyzer` + `CodeFixProvider`.
    
- Create incremental generators (`IIncrementalGenerator`) for compile-time optimization.
    

---

## 62. IL & Metadata Manipulation

### Reflection.Emit

Generate assemblies dynamically:

```csharp
var asm = AssemblyBuilder.DefineDynamicAssembly(new AssemblyName("Dyn"), AssemblyBuilderAccess.Run);
var mod = asm.DefineDynamicModule("Core");
var type = mod.DefineType("Hello", TypeAttributes.Public);
type.CreateType();
```

### Mono.Cecil

- Decompile, modify, and re-emit IL from assemblies.
    
- Common in AOP frameworks and obfuscators.
    

### dnlib

- Low-level IL inspection; used in modding tools.
    

---

## 63. NativeAOT, Trimming, and ILLink

- **NativeAOT**: ahead-of-time compilation to native binaries.
    
- Enable in `.csproj`:
    
    ```xml
    <PublishAot>true</PublishAot>
    ```
    
- **Trimming** removes unused code:
    
    ```xml
    <PublishTrimmed>true</PublishTrimmed>
    <TrimMode>link</TrimMode>
    ```
    
- Control reflection roots via `DynamicallyAccessedMembers` attribute.
    

---

## 64. GC & Memory Internals

- .NET uses _generational, concurrent garbage collector_.
    
- Configurable modes:
    
    - Workstation / Server
        
    - Background / Non-concurrent
        
- Force GC: `GC.Collect()`
    
- Analyze via `dotnet-gcdump`, PerfView, or SOS:
    
    ```
    dotnet-gcdump collect -p <pid>
    ```
    
- Key APIs: `GC.TryStartNoGCRegion()`, `GC.RegisterForFullGCNotification()`
    
- Span, stackalloc, and pooling reduce GC pressure.
    

---

## 65. JIT & RyuJIT Optimization

- JIT tiers:
    
    - Tier 0: quick compile
        
    - Tier 1: optimized hot paths
        
- Inspect via `COMPlus_TieredCompilation=1` environment variable.
    
- `System.Runtime.Intrinsics` for vectorization and SIMD.
    
- AOT removes JIT completely for fast startup.
    

---

## 66. Threading, Tasks, and Synchronization

- `ThreadPool` manages work-stealing queues.
    
- `SynchronizationContext` captures context in async.
    
- `ExecutionContext` propagates logical call context.
    
- Thread safety: use `lock`, `Monitor`, `Interlocked`, or `Volatile`.
    
- Advanced locks: `ReaderWriterLockSlim`, `SpinLock`, `SpinWait`.
    
- Task scheduling via custom `TaskScheduler`.
    
- Async coordination: `SemaphoreSlim`, `CountdownEvent`, `Barrier`, `Channel<T>`.
    

---

## 67. Diagnostics, Profiling & Instrumentation

- Profiling APIs: `ICorProfilerCallback` and ETW/TraceEvent.
    
- Collect traces:
    
    ```bash
    dotnet-trace collect --process-id <pid>
    ```
    
- Counters:
    
    ```bash
    dotnet-counters monitor System.Runtime
    ```
    
- Add custom counters via `EventCounter` or `Meter` from `System.Diagnostics.Metrics`.
    
- Observe Activity tracing with OpenTelemetry.
    

---

## 68. Runtime Configuration Knobs

- Controlled via environment variables:
    
    - `DOTNET_GCServer`, `DOTNET_TieredPGO`, `DOTNET_ReadyToRun`
        
- Use `AppContext.SetSwitch("SwitchName", true);` to toggle behaviors.
    
- Configure GC latency, thread count, tiering, trimming in `.runtimeconfig.json`.
    

---

## 69. Debugging & SOS

- **SOS** (Son of Strike) used inside WinDbg:
    
    ```
    !dumpheap -stat
    !gcroot
    !clrstack
    ```
    
- Visual Studio Diagnostics Tools, JetBrains Rider, dnSpy for inspection.
    
- `System.Diagnostics.Debugger.Break()` triggers manual breakpoints.
    

---

## 70. Plugin Architecture

- Dynamic loading via `AssemblyLoadContext` in .NET Core:
    

```csharp
var ctx = new AssemblyLoadContext("plugin", isCollectible: true);
var asm = ctx.LoadFromAssemblyPath("plugin.dll");
```

- Enables modular systems, live reload, and isolation.
    
- Collectible assemblies allow unloading.
    

---

## 71. Security & Hardening

- Avoid dynamic code unless sandboxed.
    
- `SecureString` deprecated; use Azure Key Vault or DPAPI.
    
- Code signing for integrity.
    
- Prevent reflection abuse with trimming.
    
- Use `AllowPartiallyTrustedCallers` only when required.
    

---

## 72. Reverse Engineering & Protection

- Common tools: ILSpy, dnSpy, JetBrains decompiler.
    
- To protect:
    
    - Obfuscators: ConfuserEx, Dotfuscator.
        
    - NativeAOT reduces visibility.
        
    - Avoid embedding secrets in code.
        

---

## 73. Advanced Build Automation

- Create custom **MSBuild tasks**:
    
    ```xml
    <UsingTask TaskName="MyTask" AssemblyFile="tools.dll" />
    <Target Name="CustomBuild">
      <MyTask Input="data" />
    </Target>
    ```
    
- Extend build with targets and properties.
    
- Use `Directory.Build.props` for shared config.
    

---

## 74. AOT & Crossgen2

- Crossgen2 compiles IL to native ReadyToRun images.
    
    ```bash
    dotnet publish -p:PublishReadyToRun=true
    ```
    
- NativeAOT compiles full binary, removing runtime dependencies.
    
- Works well for microservices and CLI tools.
    

---

## 75. Instrumentation & Observability APIs

- `DiagnosticListener` and `ActivitySource` for tracing.
    
- Integrated into `HttpClient`, EF Core, ASP.NET Core.
    
- OpenTelemetry exporter connects to Jaeger, Zipkin, Prometheus.
    

---

## 76. Advanced Reflection & Expression Trees

- Modify expression trees dynamically.
    
- Build dynamic queries:
    

```csharp
Expression<Func<T,bool>> BuildFilter<T>(string prop, object value)
{
    var param = Expression.Parameter(typeof(T));
    var body = Expression.Equal(Expression.Property(param, prop), Expression.Constant(value));
    return Expression.Lambda<Func<T,bool>>(body, param);
}
```

---

## 77. Runtime Hosting & Embedding .NET

- Host .NET Core runtime in C/C++ apps via `coreclrhost.h` or `nethost`.
    
- Load managed assemblies dynamically.
    
- Reverse P/Invoke from C# to native and back.
    
- Enable scripting environments (e.g., game engines, editors).
    

---

## 78. Compiler, IL Rewriting & Tools

- Custom compiler frontends can reuse Roslyn backend.
    
- Post-build IL weaving via Fody or Mono.Cecil.
    
- Used in AOP, DI generation, telemetry injection.
    

---

## 79. Multi-Targeting & Source Compatibility

- Multi-target with:
    
    ```xml
    <TargetFrameworks>net6.0;net9.0</TargetFrameworks>
    ```
    
- Use conditional compilation:
    
    ```csharp
    #if NET9_0
    // new features
    #endif
    ```
    
- Cross-platform compatibility via `RuntimeInformation`.
    

---

## 80. Advanced Memory Patterns

- Stack vs heap awareness.
    
- `GCHandle` for pinned memory.
    
- `MemoryMarshal` for reinterpret casts.
    
- Unsafe buffers for high-speed interop:
    

```csharp
unsafe {
  fixed(byte* p = bytes) { ... }
}
```

---

## 81. Performance Profiling & Tuning Workflow

1. Measure with `BenchmarkDotNet`
    
2. Profile allocations (`dotnet-trace`)
    
3. Optimize with `Span<T>`, pooling, struct layout
    
4. Validate using PerfView / counters
    
5. Lock results into CI pipeline
    

---

## 82. Compiler APIs & Roslyn Extensions

- Create analyzers, refactorings, and code fixes.
    
- Visual Studio Extensions (VSIX) can host analyzers.
    
- SyntaxRewriter allows code transformation.
    
- SemanticModel gives type information.
    

---

## 83. Expert Patterns & Architectures

- Event Sourcing, CQRS, Clean Architecture
    
- MediatR, Autofac, AutoMapper, FluentValidation
    
- Domain-Driven Design (DDD)
    
- Hexagonal / Onion Architecture
    
- Modular Monoliths with feature folders
    
- Actor systems via Akka.NET / Orleans
    

---

## 84. Distributed Systems & gRPC

- Protocol Buffers serialization.
    
- Unary, streaming, and duplex calls.
    
- ASP.NET Core integration:
    

```csharp
app.MapGrpcService<MyGrpcService>();
```

- Channel-based clients for efficient RPC.
    

---

## 85. Reactive & Dataflow Programming

- Reactive Extensions (Rx.NET): `IObservable<T>` / `IObserver<T>`.
    
- Dataflow library: `BufferBlock`, `TransformBlock`, `ActionBlock`.
    
- Build pipelines for concurrent message processing.
    

---

## 86. Advanced Debugging & Time Travel Debugging

- Visual Studio “Snapshot Debugger” and “Time Travel Debugging”.
    
- Dump analysis via `dotnet-dump analyze`.
    
- Cross-platform debugging via VS Code + `clrdbg` or `vsdbg`.
    

---

## 87. Tooling Ecosystem

|Tool|Purpose|
|---|---|
|dotnet-trace|runtime tracing|
|dotnet-counters|performance metrics|
|dotnet-gcdump|memory heap snapshots|
|dotnet-dump|crash dump inspection|
|PerfView|advanced GC and CPU profiling|
|ILSpy|IL inspection|
|JetBrains Rider|profiler + decompiler|

---

## 88. Conclusion — Mastery Level

An advanced C# developer understands:

- Language, runtime, and IL level.
    
- Memory, GC, JIT, and async internals.
    
- Tooling from Roslyn to MSBuild to diagnostics.
    
- Ecosystem integration: web, cloud, native, AI, and game engines.
    
- Secure, optimized, observable, testable systems.
    

The final step is _experimentation and contribution_—build analyzers, libraries, or runtime PRs to .NET itself.

---
