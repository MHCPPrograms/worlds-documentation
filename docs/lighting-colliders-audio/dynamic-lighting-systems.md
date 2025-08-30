# Dynamic Lighting Systems for Horizon Worlds

**Implement interactive and event-driven lighting systems in Horizon Worlds.** This guide focuses on scripting dynamic lighting, proximity-based triggers, and network events for lighting control.

**Creator Skill Level**
Intermediate to Advanced

**Recommended Background Knowledge**
Understanding of lighting fundamentals from [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md) and TypeScript scripting fundamentals.

**Estimated Time to Complete**
45-60 minutes for core concepts, 30 minutes for implementation

## Table of Contents

1. [Interactive Lighting Triggers](#interactive-lighting-triggers)
2. [Network Event Systems](#network-event-systems)
3. [Advanced Lighting Scripts](#advanced-lighting-scripts)
4. [Performance Considerations](#performance-considerations)

## Interactive Lighting Triggers

### Proximity-Based Lighting

Proximity-based lighting creates immersive experiences by responding to player movement and interaction.

![Proximity-Based Lighting Setup](./assets/DynamicGizmo.png)

**Implementation Steps:**

1. **Create Trigger Zone**
   - Add Trigger Gizmo to your world
   - Configure size and position for desired interaction area

2. **Set Up Light Entity**
   - Add Dynamic Light Gizmo
   - Configure initial properties (color, intensity, falloff)

3. **Connect with Scripts**
   - Use TriggerBroadcaster to detect player entry/exit
   - Use LightChanger to modify lighting properties

**📖 For basic lighting setup**: See [lighting-fundamentals-basics.md#using-dynamic-lights](./lighting-fundamentals-basics.md#using-dynamic-lights)

---

## Network Event Systems

### Trigger Broadcasting System

The TriggerBroadcaster component detects when players enter or exit trigger zones and sends network events.

```typescript
import { Component, PropTypes, NetworkEvent, CodeBlockEvents, Player, Entity } from 'horizon/core';

// Define the network event. This should match the event name used by the receiving script.
const PlayerEntered = new NetworkEvent('PlayerEntered');

export class TriggerBroadcaster extends Component<typeof TriggerBroadcaster> {
  static propsDefinition = {
    // The entity that will receive the network event.
    target: { type: PropTypes.Entity },
  };

  override preStart() {
    // Connect to the trigger event that fires when a player enters.
    this.connectCodeBlockEvent(
      this.entity,
      CodeBlockEvents.OnPlayerEnterTrigger,
      (player: Player) => {
        this.handlePlayerEnter(player);
      }
    );
  }

  override start() {
    // No initialization needed in start for this script.
  }

  private handlePlayerEnter(player: Player) {
    // Check if the target entity prop has been assigned in the editor.
    if (this.props.target) {
      // Send the 'PlayerEntered' network event to the target entity.
      this.sendNetworkEvent(this.props.target, PlayerEntered, {});
    } else {
      console.error("TriggerBroadcaster: 'target' prop is not set.");
    }
  }
}

Component.register(TriggerBroadcaster);
```

### Light Control System

The LightChanger component receives network events and modifies lighting properties accordingly.

```typescript
import { Component, PropTypes, NetworkEvent, DynamicLightGizmo, Color } from 'horizon/core';

// Define the network event that will trigger the light change.
const PlayerEntered = new NetworkEvent('PlayerEntered');

export class LightChanger extends Component<typeof LightChanger> {
  static propsDefinition = {
    // The light entity that will change color.
    light: { type: PropTypes.Entity },
  };

  override preStart() {
    // Listen for the 'PlayerEntered' network event.
    this.connectNetworkEvent(this.entity, PlayerEntered, () => {
      this.changeLightColor();
    });
  }

  override start() {
    // Initialization logic can go here.
  }

  private changeLightColor() {
    if (!this.props.light) {
      console.error("LightChanger: 'light' prop is not set.");
      return;
    }

    // Cast the entity to a DynamicLightGizmo.
    const lightGizmo = this.props.light.as(DynamicLightGizmo);

    if (lightGizmo) {
      // Change the light's color to red.
      lightGizmo.color.set(new Color(1, 0, 0));
    } else {
      console.error("LightChanger: The provided entity is not a DynamicLightGizmo.");
    }
  }
}

Component.register(LightChanger);
```

---

## Advanced Lighting Scripts

### Color Cycling System

Create dynamic color transitions for atmospheric effects:

```typescript
import { Component, PropTypes, DynamicLightGizmo, Color } from 'horizon/core';

export class ColorCycler extends Component<typeof ColorCycler> {
  static propsDefinition = {
    light: { type: PropTypes.Entity },
    cycleSpeed: { type: PropTypes.Number, defaultValue: 2000 },
  };

  private colorInterval?: number;
  private colors: Color[] = [
    new Color(1, 0, 0),    // Red
    new Color(0, 1, 0),    // Green
    new Color(0, 0, 1),    // Blue
    new Color(1, 1, 0),    // Yellow
    new Color(1, 0, 1),    // Magenta
    new Color(0, 1, 1),    // Cyan
  ];
  private currentColorIndex = 0;

  override start() {
    this.startColorCycle();
  }

  private startColorCycle() {
    this.colorInterval = this.async.setInterval(() => {
      this.cycleToNextColor();
    }, this.props.cycleSpeed);
  }

  private cycleToNextColor() {
    if (!this.props.light) return;

    const lightGizmo = this.props.light.as(DynamicLightGizmo);
    if (lightGizmo) {
      this.currentColorIndex = (this.currentColorIndex + 1) % this.colors.length;
      lightGizmo.color.set(this.colors[this.currentColorIndex]);
    }
  }

  override dispose() {
    if (this.colorInterval) {
      this.async.clearInterval(this.colorInterval);
    }
  }
}

Component.register(ColorCycler);
```

### Intensity Pulsing System

Create breathing or pulsing light effects:

```typescript
import { Component, PropTypes, DynamicLightGizmo } from 'horizon/core';

export class IntensityPulser extends Component<typeof IntensityPulser> {
  static propsDefinition = {
    light: { type: PropTypes.Entity },
    minIntensity: { type: PropTypes.Number, defaultValue: 1 },
    maxIntensity: { type: PropTypes.Number, defaultValue: 8 },
    pulseSpeed: { type: PropTypes.Number, defaultValue: 1000 },
  };

  private pulseInterval?: number;
  private increasing = true;
  private currentIntensity: number;

  override start() {
    this.currentIntensity = this.props.minIntensity;
    this.startPulsing();
  }

  private startPulsing() {
    this.pulseInterval = this.async.setInterval(() => {
      this.updateIntensity();
    }, this.props.pulseSpeed / 60); // 60 steps per pulse cycle
  }

  private updateIntensity() {
    if (!this.props.light) return;

    const lightGizmo = this.props.light.as(DynamicLightGizmo);
    if (lightGizmo) {
      if (this.increasing) {
        this.currentIntensity += (this.props.maxIntensity - this.props.minIntensity) / 60;
        if (this.currentIntensity >= this.props.maxIntensity) {
          this.increasing = false;
        }
      } else {
        this.currentIntensity -= (this.props.maxIntensity - this.props.minIntensity) / 60;
        if (this.currentIntensity <= this.props.minIntensity) {
          this.increasing = true;
        }
      }
      
      lightGizmo.intensity.set(this.currentIntensity);
    }
  }

  override dispose() {
    if (this.pulseInterval) {
      this.async.clearInterval(this.pulseInterval);
    }
  }
}

Component.register(IntensityPulser);
```

---

## Performance Considerations

### Dynamic Light Limits

- **Maximum 20 dynamic lights per world**
- Use static lights and glow materials for ambient lighting
- Reserve dynamic lights for interactive elements only

### Scripting Performance

- Avoid heavy loops in lighting scripts
- Use efficient event handling
- Monitor performance with Real-time Metrics panel

**📊 For comprehensive performance analysis**: See [lighting-performance-optimization.md](./lighting-performance-optimization.md)

---

## Next Steps

- **Advanced Techniques**: Explore [advanced-lighting-techniques.md](./advanced-lighting-techniques.md)
- **Performance Optimization**: Study [lighting-performance-optimization.md](./lighting-performance-optimization.md)
- **Complete Reference**: Review [mastering-horizon-worlds-lighting-complete-guide.md](./mastering-horizon-worlds-lighting-complete-guide.md)

---

**Summary**: This guide covers interactive lighting systems and scripting. For fundamentals, see [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md). For advanced techniques, see [advanced-lighting-techniques.md](./advanced-lighting-techniques.md).