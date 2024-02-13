# Unity MainThread Job

> [!IMPORTANT]
> Works in release builds only!

```
[BurstCompile]
public struct Job1 : IJob {
  public void Execute() { ... }
}

public struct Job2MainThread : IJobMainThread {
  public void Execute() {
    // force main thread for this execute
    var go = new GameObject();
    go...
  }
}

[BurstCompile]
public struct Job3 : IJob {
  public void Execute() { ... }
}

dependsOn = new Job1().Schedule(dependsOn);
dependsOn = new Job2MainThread().Schedule(dependsOn); // do some work in main thread with Unity API inside job (no burst)
dependsOn = new Job3().Schedule(dependsOn);
```
