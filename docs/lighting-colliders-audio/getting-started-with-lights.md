# Lighting Documentation Suite

## Overview

This directory contains comprehensive documentation for implementing advanced lighting systems in Horizon Worlds.

## Documentation Structure

### 📚 **Start Here: Core Concepts**
- **[lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md)** - **Single source of truth** for lighting theory, gizmo types, and basic setup techniques

### 🎨 **Advanced Implementation**
- **[advanced-lighting-techniques.md](./advanced-lighting-techniques.md)** - Environment gizmo setup, glow materials, and practical techniques
- **[dynamic-lighting-systems.md](./dynamic-lighting-systems.md)** - Interactive lighting scripts and event-driven systems

### ⚡ **Performance & Optimization**
- **[lighting-performance-optimization.md](./lighting-performance-optimization.md)** - **Single source of truth** for performance monitoring, optimization, and troubleshooting

## Quick Start Guide

1. **Begin with Fundamentals**: Start with [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md) for core concepts
2. **Choose Your Path**:
   - **Static Lighting**: Continue with [advanced-lighting-techniques.md](./advanced-lighting-techniques.md)
   - **Interactive Lighting**: Jump to [dynamic-lighting-systems.md](./dynamic-lighting-systems.md)
3. **Optimize Performance**: Reference [lighting-performance-optimization.md](./lighting-performance-optimization.md) throughout development

## Key Topics & Where to Find Them

### 💡 **Light Types & Properties**
- **Complete Reference**: [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md#horizon-worlds-lighting-gizmo-types)
- **Advanced Usage**: [advanced-lighting-techniques](./advanced-lighting-techniques.md#dynamic-light-gizmo)

### 🎭 **Three-Point Lighting Setup**
- **Fundamentals**: [lighting-fundamentals-basics](./lighting-fundamentals-basics.md#three-point-lighting-principle)

### 🔧 **Environment & Atmosphere**
- **Primary Source**: [advanced-lighting-techniques](./advanced-lighting-techniques.md#environment-gizmo-for-atmosphere)

### ⚡ **Performance Guidelines**
- **Single Source**: [lighting-performance-optimization.md](./lighting-performance-optimization.md)
- **Quick Reference**: See performance section in each document for specific tips

## Best Practices

- ✅ Use appropriate light types for your scene
- ✅ Implement proper shadow settings
- ✅ Consider mobile performance limitations
- ✅ Create atmospheric depth with fog
- ✅ Use color temperature for mood
- ❌ Don't overuse lights (performance impact)
- ❌ Don't ignore shadow optimization
- ❌ Don't forget mobile considerations

## Performance Guidelines

### Light Count Limits
- **Desktop**: Up to 8 lights per scene
- **Mobile**: Up to 4 lights per scene

### Optimization Tips
- Use light culling for distant objects
- Implement LOD systems for lights
- Optimize shadow resolution
- Consider light pooling for dynamic scenes

**📊 For detailed performance analysis**: See [lighting-performance-optimization](./lighting-performance-optimization.md#performance-monitoring-with-real-time-metrics)

## Next Steps

After completing this documentation suite, consider exploring:
- Advanced shader techniques
- Custom lighting effects
- Real-time lighting changes
- Lighting for specific game genres

---

**Note**: Always balance visual quality with performance, especially for mobile platforms. Each document contains cross-references to related sections in other documents to help you navigate efficiently.
