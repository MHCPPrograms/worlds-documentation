# World Performance Optimization in Horizon Worlds

Creating compelling art and smooth mechanics is what makes a Horizon World memorable. But even the most beautiful scene can lose its magic if performance lags. A single hiccup can break immersion, frustrate players, and reduce the chances of your world being revisited.

Performance optimization isn’t just technical—it’s emotional. It’s the difference between a magical experience and a forgettable one.

---

## Why Optimization Matters

For beginners, performance tuning can feel messy and overwhelming. But once you crack it, it becomes your secret weapon—eliminating stutters, improving responsiveness, and making your world feel alive.

Think of it like stage lighting: if the spotlight flickers, the audience loses focus. In Horizon Worlds, optimization is your spotlight.

---

## Decoupling Performance: Frame Time vs. Frame Rate

Gamers often talk about **frames per second (FPS)**, but as a world creator, it’s better to think in **frame time**—measured in milliseconds per frame.

Here’s why:

Imagine your game *Enchanted City* renders 70 frames in one second. That’s 70 FPS—great, right? But what if 69 frames take 10ms each, and the last one takes 100ms? The average still looks like 70 FPS, but the player will feel that 100ms lag. It’s like watching a smooth movie that suddenly freezes for a moment. That moment breaks the flow.

So instead of chasing average FPS, aim for **consistent frame time**.

---

## Frame Budgeting

Every frame has a time budget based on your target FPS.

For example:
- If your world targets **72 FPS** (like Quest displays at 72Hz), your frame time budget is:
  
  ```
  1000 ms / 72 fps = ~13.88 ms per frame
  ```

That means all rendering, logic, and interactions must complete in under **13.88 milliseconds**—every single frame.

Setting this budget helps you benchmark and prioritize what’s worth rendering.

---

## Real-Time Metrics Panel in VR

The best way to analyze performance is **on the target device**—inside VR.

Horizon Worlds offers a **Real-Time Metrics Panel** to help you monitor frame time, memory usage, and more.

### How to Enable It:
1. Visit your world in any mode.
2. Turn either wrist toward you to activate the wearable.
3. Open the PUI and go to **Settings**.
4. Click the **Utilities** tab and enable the **Utilities Menu**.

Once enabled, you’ll see live metrics while exploring your world—perfect for spotting bottlenecks.

---

## 🛠️ Optimizing World Content

Here are simple ways to reduce workload and improve performance:

- **Only enable necessary settings** for objects. Don’t use physics or collisions unless needed.
- **Make hidden items invisible.** If the player can’t see it, don’t render it.
- **Use one texture per object.** In Blender, you can bake multiple materials into a single texture map to reduce draw calls.

---

## Summary: Treat Workload Like Currency

Think of performance like a budget. Every object you add costs something.

Before placing a chair in your scene, ask:
> “Does this chair add emotional or functional value? Is it worth the rendering cost?”

If it’s just decoration, maybe it can be merged with other assets or simplified. If it’s interactive or symbolic, it might be worth the cost.

This mindset helps beginners prioritize wisely and build worlds that feel rich without being heavy.

---

## Final Thoughts

Performance optimization isn’t just about numbers—it’s about crafting an experience that feels smooth, intentional, and magical. With the right tools and mindset, you’ll turn technical tuning into creative empowerment.


