#Goal
This importable script creates a **spawner** in Horizon Worlds that generates enemies at a fixed interval (every second by default). Yes, I know the moral reprocussions of generating more enemies into the world, but corporate required it... 

---
## 1. Understanding the Script Basics

### Importing Dependencies

```ts
import { Component, PropTypes, Asset } from 'horizon/core';
```
Depending on your editor settings, this could also have an ampersand symbol like: 
```ts
import { Component, PropTypes, Asset } from '@horizon/core';
```

- `Component`: lets us define custom behavior for an entity.
- `PropTypes`: allows us to define **editable properties** (e.g., assigning a prefab in the editor).
- `Asset`: represents a prefab or saved object in Horizon Worlds. It's a saved <i>template</i> that can be referenced by scripts.

---

### Defining the Component

```ts
export class WaveSpawner extends Component<typeof WaveSpawner> {
  static propsDefinition = {
    enemyPrefab: { type: PropTypes.Asset },
  };
```
- Creates a new component in your project called `WaveSpawner`.
- Adds **one property**: `enemyPrefab`, which must be an **Asset** (your enemy prefab). This is essentially telling the spawner thing - what is the monster you want me to spawn. Suggested monster name = Charles. 

---

### Start Method
```ts
override start() {
  // checks to ensure that the component was setup with an enemy to spawn
  if (!this.props.enemyPrefab) {
    console.error("WaveSpawner: 'enemyPrefab' property is not set.");
    return;
  }

  // This is where we define the interval of spawn rate in millisecons adjustments are totally cool
  this.async.setInterval(() => {
    this.spawnEnemy();
  }, 1000);
}
```

- This method runs when the component starts. Hence the "override start()" bit at the beginning.
- Checks if `enemyPrefab` has been assigned. It'll get mad at you if you forget to tell the enemy spawner what enemy--Charles--to spawn.
- If yes, sets up a **timer** to call `spawnEnemy()` every 1000 ms (1 sec).
- Also, don't forget, if the spawner is somehow despawned then it won't make more monsters. If Charles's mama goes to heaven, then she can't create more Charlies. 
Still tracking? Great!!! Let's get into the spawning logic next, and don't worry we don't need a doula. 

---

### Spawn Logic

```ts
private spawnEnemy() {
  // where do we create this beautiful enemy of yours?
  const spawnPosition = this.entity.position.get();
  const spawnRotation = this.entity.rotation.get();

  this.world.spawnAsset(
    this.props.enemyPrefab!,
    spawnPosition,
    spawnRotation
  ).then(entities => {
    if (entities && entities.length > 0) {
      // console.log(`Spawned entity with ID: ${entities[0].id}`);
    }
  }).catch(error => {
    console.error("Failed to spawn enemy prefab:", error);
  });
}
```

- Uses the **entity’s position and rotation** as the spawn point. And by entity we mean the "spawner asset thing." 
- Spawns the assigned enemy asset prefab in the world. I.E. Charles is born where his mama "the Charles Spawner" was placed.
- Logs errors if spawning fails.

---

Register the Component

```ts
Component.register(WaveSpawner);
```

- Makes the component available in Horizon Worlds’ editor. Meaning this becomes a reusable building block in the editor and in your game!
- Next time you go to the "Add Component" menu, you'll see a new, custom component, and if you're smart, you'll name it "Charlie's Mama."

---
