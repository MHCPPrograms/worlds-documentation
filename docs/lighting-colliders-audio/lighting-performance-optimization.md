# Lighting Performance Optimization for Horizon Worlds

**Optimize your Horizon Worlds lighting for smooth performance across VR, mobile, and web platforms.** This guide covers real performance monitoring tools, optimization techniques, and troubleshooting based on actual Horizon Worlds capabilities.

**Creator Skill Level**
Intermediate to Advanced

**Recommended Background Knowledge**
Understanding of lighting fundamentals from [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md) and basic optimization concepts.

**Estimated Time to Complete**
1 hour for core optimization techniques, 30 minutes for mobile-specific optimizations

## Table of Contents

1. [Performance Monitoring with Real-time Metrics](#performance-monitoring-with-real-time-metrics)
2. [Memory Management and Limits](#memory-management-and-limits)
3. [Cross-Platform Optimization](#cross-platform-optimization)
4. [Mobile and Web Optimization](#mobile-and-web-optimization)
5. [Performance Troubleshooting](#performance-troubleshooting)
6. [Best Practices](#best-practices)

## Performance Monitoring with Real-time Metrics

Horizon Worlds provides a built-in Real-time Metrics panel to monitor your world's performance.

### **Accessing Real-time Metrics:**

**In VR:**

1. Enable **Utilities** menu in Settings
2. Open wrist menu and select **Real-time Metrics**

**On Web:**

- Press **P** key to toggle metrics panel

**Not Available:**

- Desktop editor (use VR or web for testing)
- Mobile (testing must be done in VR or web)

### **Key Performance Metrics:**

| Metric         | Target            | Description                              |
| -------------- | ----------------- | ---------------------------------------- |
| **FPS**        | 72 (VR), 60 (Web) | Frames per second - most critical metric |
| **CPU**        | <13.8ms (VR)      | CPU processing time per frame            |
| **GPU**        | <13.8ms (VR)      | GPU rendering time per frame             |
| **Memory**     | <6.25 GB          | Total memory usage (hard limit)          |
| **Draw Calls** | Minimize          | Number of render batches                 |
| **Vertices**   | Monitor           | Total vertices rendered per frame        |
| **Physics**    | Monitor           | Physics simulation time                  |
| **Scripting**  | Monitor           | TypeScript execution time                |

### **Application Space Warp (ASW):**

- **ASW Value 0**: Off (normal performance targets)
- **ASW Value 1**: On (doubles frame budget, relaxes targets)
- Automatically enabled when **Frame Budget Boost** is on
- Helps maintain smooth experience when performance drops

### **Phase Sync Time:**

- **High value**: World performing well (generating frames faster than needed)
- **0ms**: World struggling to maintain target FPS
- Acts as performance buffer

---

## Memory Management and Limits

**Critical**: Horizon Worlds enforces a **6 GB memory limit** per world.

### **Memory Limit Enforcement:**

- Worlds exceeding 6 GB **cannot be published**
- Cannot add new objects/assets when limit is reached
- Existing worlds must be optimized to stay under limit
- System may crash worlds that exceed memory limits

### **Memory Optimization Strategies:**

**Reduce Asset Size:**

- Use compressed textures appropriate for target resolution
- Optimize 3D models (reduce polygon count)
- Remove unused materials and textures
- Use texture atlasing to combine materials

**Efficient Asset Usage:**

- Reuse materials across multiple objects
- Share geometries when possible
- Remove duplicate assets
- Use appropriate LOD (Level of Detail) models

**Monitor Memory Usage:**

- Use Real-time Metrics panel to track memory
- Set memory target alerts (e.g., 5.5 GB warning)
- Test memory usage throughout development

---

## Cross-Platform Optimization

### **VR Platform Optimization:**

**Quest 2/3/Pro:**
- Target 72 FPS for smooth experience
- Limit dynamic lights to 15-18 per scene
- Use efficient shadow settings
- Optimize for mobile GPU architecture

**PC VR:**
- Target 90+ FPS for high-end headsets
- Can handle more complex lighting setups
- Monitor CPU/GPU balance
- Test with different hardware configurations

### **Web Platform Optimization:**

**Browser Performance:**
- Target 60 FPS for smooth web experience
- Limit dynamic lights to 10-12 per scene
- Use compressed textures and optimized models
- Test across different browsers and devices

---

## Mobile and Web Optimization

### **Mobile-Specific Considerations:**

**Performance Targets:**
- **FPS**: 60 FPS minimum, 72 FPS target
- **Dynamic Lights**: Maximum 4-6 per scene
- **Memory**: Stay under 4 GB for mobile devices
- **Draw Calls**: Minimize to reduce GPU overhead

**Optimization Techniques:**

1. **Light Culling:**
   - Disable lights for distant objects
   - Use LOD systems for lighting
   - Implement light pooling for dynamic scenes

2. **Shadow Optimization:**
   - Limit shadow-casting lights
   - Use lower resolution shadows
   - Implement shadow distance culling

3. **Material Optimization:**
   - Use efficient shaders
   - Minimize texture sizes
   - Implement material instancing

### **Web Platform Optimization:**

**Browser Compatibility:**
- Test on Chrome, Firefox, Safari, Edge
- Use WebGL 2.0 features when available
- Implement progressive loading for large worlds
- Optimize for different screen resolutions

---

## Performance Troubleshooting

### **Common Performance Issues:**

**Low FPS:**
- Reduce dynamic light count
- Optimize shadow settings
- Check for heavy scripting loops
- Monitor CPU/GPU usage

**Memory Issues:**
- Remove unused assets
- Compress textures
- Optimize 3D models
- Use asset streaming for large worlds

**VR Discomfort:**
- Maintain consistent 72 FPS
- Avoid rapid lighting changes
- Test comfort settings
- Monitor frame timing

### **Troubleshooting Steps:**

1. **Identify the Problem:**
   - Use Real-time Metrics panel
   - Monitor specific performance metrics
   - Test on target platforms

2. **Isolate the Cause:**
   - Test with different lighting setups
   - Remove components one by one
   - Check for script performance issues

3. **Apply Solutions:**
   - Implement optimization techniques
   - Test performance improvements
   - Iterate and refine

---

## Best Practices

### **Lighting Optimization:**

- **Use Static Lights**: Prefer static lights for world lighting
- **Limit Dynamic Lights**: Reserve for interactive elements only
- **Optimize Shadows**: Use efficient shadow settings
- **Monitor Performance**: Test regularly with Real-time Metrics

### **Asset Optimization:**

- **Compress Textures**: Use appropriate compression for target platforms
- **Optimize Models**: Reduce polygon count where possible
- **Reuse Assets**: Share materials and geometries
- **Remove Unused**: Clean up unused assets regularly

### **Scripting Optimization:**

- **Efficient Loops**: Avoid heavy loops in lighting scripts
- **Event Handling**: Use efficient event handling patterns
- **Memory Management**: Clean up resources properly
- **Performance Testing**: Test scripts on target platforms

---

## Next Steps

- **Lighting Fundamentals**: Review [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md)
- **Advanced Techniques**: Explore [advanced-lighting-techniques.md](./advanced-lighting-techniques.md)
- **Dynamic Systems**: Study [dynamic-lighting-systems.md](./dynamic-lighting-systems.md)
- **Complete Reference**: Review [mastering-horizon-worlds-lighting-complete-guide.md](./mastering-horizon-worlds-lighting-complete-guide.md)

---

**Summary**: This guide covers comprehensive performance optimization for Horizon Worlds lighting. For fundamentals, see [lighting-fundamentals-basics.md](./lighting-fundamentals-basics.md). For implementation techniques, see [advanced-lighting-techniques.md](./advanced-lighting-techniques.md).