# Advanced Lighting Techniques for Horizon Worlds

**Master advanced lighting techniques and environment setup in Horizon Worlds.** This guide focuses on environment gizmo configuration, static lights, and practical implementation techniques.

**Creator Skill Level**
Intermediate to Advanced

**Recommended Background Knowledge**
Understanding of lighting fundamentals from [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md) and basic TypeScript scripting.

**Estimated Time to Complete**
45-60 minutes for core concepts, 30 minutes for advanced techniques

## Table of Contents

1. [Environment Gizmo for Atmosphere](#environment-gizmo-for-atmosphere)
2. [Dynamic Light Gizmo Advanced Usage](#dynamic-light-gizmo-advanced-usage)
3. [Static Lighting](#static-lighting-with-glow-materials)
4. [Practical Lighting Techniques](#practical-lighting-techniques)
5. [TypeScript Implementation](#typescript-implementation)
6. [Performance Considerations](#performance-considerations)

## Environment Gizmo for Atmosphere

The Environment Gizmo is your primary tool for setting the overall mood and atmosphere of your world.

<iframe width="1378" height="775" src="https://www.youtube.com/embed/-eByBYkd2U0" title="Creating a Custom Skybox in the Worlds Desktop Editor ☁️🌈" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### **Setting Up Environment Lighting:**

1. **Add Environment Gizmo**

   - Go to **Gizmos** menu
   - Select **Environment Gizmo**
   - Place in your world

2. **Configure Environment Properties**
   - **Skydome**: Choose from preset environments (Daytime, Night, Sunrise, etc.)
   - **Fog Density**: Adjust atmospheric fog (0.0-1.0, use very low values like 0.1)
   - **Custom Gradient**: Create custom sky colors
   - **Grid Visibility**: Show/hide floor grid

### **Environment Presets Available:**

- **Daytime**: Bright, natural lighting
- **Night**: Dark atmosphere with subtle ambient light
- **Sunrise/Sunset**: Warm, golden lighting
- **Various themed environments**: Space, underwater, fantasy settings

### **Fog Density Guidelines:**

- **0.0**: Crystal clear visibility
- **0.01-0.05**: Subtle depth enhancement
- **0.1**: Noticeable atmospheric effect
- **0.2+**: Heavy fog (use sparingly)

**Important**: Fog density is extremely sensitive. Values above 0.1 can make building difficult as it affects visibility in build mode.

---

## Dynamic Light Gizmo Advanced Usage

Dynamic lights provide interactive, scriptable lighting with real-time shadows and color changes.

### **Dynamic Light Properties:**

- **Type**: Point light (360°) or Spot light (directional)
- **Color**: Full RGB color range
- **Intensity**: Light brightness
- **Falloff Distance**: How far light travels
- **Spread** (Spot lights only): Cone angle of light beam

### **Critical Limitation:**

**Maximum 20 dynamic lights per world**. Plan your lighting carefully as this limit includes all dynamic lights, whether scripted or not.

### **Setting Up Dynamic Lights:**

1. **Add Dynamic Light Gizmo**

   - Go to **Gizmos** menu
   - Select **Dynamic Light Gizmo**
   - Position where needed

2. **Configure Properties**
   - Set initial color and intensity in editor
   - Adjust falloff distance for desired coverage
   - Configure spread angle for spot lights

**📖 For basic dynamic light setup**: Click [here](https://developers.meta.com/horizon-worlds/learn/documentation/code-blocks-and-gizmos/dynamic-light-gizmo).

---

## Static Lighting

Static lighting provide unlimited lighting without performance impact.

### **Static Lighting Properties:**

- **Emission Color**: The color of light emitted
- **Emission Intensity**: Brightness of the glow
- **Emission Map**: Texture-based emission patterns

### **Best Practices:**

- Use for ambient lighting and atmospheric effects
- Combine with environment gizmo for complete world lighting
- Perfect for neon signs, magical effects, and mood lighting

**📖 For basic static light setup**: Click [here](https://developers.meta.com/horizon-worlds/learn/documentation/code-blocks-and-gizmos/static-light-gizmo).
---

## Practical Lighting Techniques

### **Layered Lighting Approach:**

1. **Base Layer**: Environment gizmo for overall world lighting
2. **Static Layer**: Glow materials for ambient and decorative lighting
3. **Dynamic Layer**: Dynamic lights for interactive elements
4. **Accent Layer**: Strategic lighting for focal points

### **Mood Lighting Techniques:**

- **Warm Lighting**: Use orange/yellow tones for cozy, intimate spaces
- **Cool Lighting**: Blue tones for mysterious, dramatic atmospheres
- **Neutral Lighting**: White lighting for realistic, balanced scenes

---

## TypeScript Implementation

### **Advanced Light Control Script:**

```typescript
import { Component, PropTypes, DynamicLightGizmo, Color, Vector3 } from 'horizon/core';

export class AdvancedLightController extends Component<typeof AdvancedLightController> {
  static propsDefinition = {
    light: { type: PropTypes.Entity },
    targetIntensity: { type: PropTypes.Number, defaultValue: 5 },
    targetColor: { type: PropTypes.Color, defaultValue: new Color(1, 1, 1) },
  };

  override start() {
    this.setupLight();
  }

  private setupLight() {
    if (!this.props.light) return;

    const lightGizmo = this.props.light.as(DynamicLightGizmo);
    if (lightGizmo) {
      // Set initial properties
      lightGizmo.intensity.set(this.props.targetIntensity);
      lightGizmo.color.set(this.props.targetColor);
    }
  }

  public fadeLight(targetIntensity: number, duration: number) {
    // Implement smooth intensity transitions
    // This is a simplified example - implement proper tweening
    if (this.props.light) {
      const lightGizmo = this.props.light.as(DynamicLightGizmo);
      if (lightGizmo) {
        lightGizmo.intensity.set(targetIntensity);
      }
    }
  }
}

Component.register(AdvancedLightController);
```

**📖 For basic scripting examples**: See [dynamic-lighting-systems.md](./dynamic-lighting-systems.md)

---

## Performance Considerations

### **Light Count Optimization:**

- **Static Lights**: Unlimited (use freely)
- **Dynamic Lights**: Maximum 20 per world
- **Glow Materials**: Unlimited (preferred for static lighting)

### **Performance Monitoring:**

- Use Real-time Metrics panel in VR
- Monitor FPS, CPU, and GPU usage
- Test on target platforms (VR, mobile, web)

**📊 For comprehensive performance analysis**: See [lighting-performance-optimization.md](./lighting-performance-optimization.md)

---

## Next Steps

- **Interactive Systems**: Explore [dynamic-lighting-systems.md](./dynamic-lighting-systems.md)
- **Performance Optimization**: Study [lighting-performance-optimization.md](./lighting-performance-optimization.md)

---

**Summary**: This guide covers advanced lighting techniques and environment setup. For fundamentals, see [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md). For performance optimization, see [lighting-performance-optimization.md](./lighting-performance-optimization.md).
