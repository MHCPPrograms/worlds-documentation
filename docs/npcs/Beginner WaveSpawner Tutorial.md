#Goal
This importable script creates a **spawner** in Horizon Worlds that generates enemies at a fixed interval (every second by default). 
---
## 1. Understanding the Script Basics

### Importing Dependencies

```ts
import { Component, PropTypes, Asset } from 'horizon/core';
```

- `Component`: lets us define custom behavior for an entity.
- `PropTypes`: allows us to define **editable properties** (e.g., assigning a prefab in the editor).
- `Asset`: represents a prefab or saved object in Horizon Worlds.

---

### Defining the Component

```ts
export class WaveSpawner extends Component<typeof WaveSpawner> {
  static propsDefinition = {
    enemyPrefab: { type: PropTypes.Asset },
  };
```
