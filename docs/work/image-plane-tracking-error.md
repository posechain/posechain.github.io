# Image Plane Tracking Error

## Summary

Detecting the target is not enough.

The system must convert visual observation into something a control system can act on.

The Image Plane Tracking Error stage transforms geometric target measurements into a control-oriented signal by calculating how far the observed target deviates from the desired image location.

This is the point where:

**perception becomes control**

The output is no longer simply an observation.

It becomes an actionable error signal used to stabilize the optical line of sight.

---

## Why It Exists

Even with reliable target detection, the system still faces a practical question:

**How should the platform respond?**

A detected target position alone does not directly tell the system what correction to make.

The control system instead needs:

- direction of error
- magnitude of error
- stability of measurement
- update timing
- confidence in observation

The Image Plane Tracking Error stage converts visual geometry into a measurable deviation from the desired target location.

In simple terms:

**where the target is**  
minus  
**where the target should be**

becomes:

**the correction signal**

Without this step, downstream steering systems would have no meaningful feedback signal.

---

## Engineering Challenge

The challenge is converting image measurements into a signal that is both:

**stable enough to control**  
and  
**responsive enough to correct disturbances**

Real image measurements are imperfect.

They contain:

- noise
- frame-to-frame variation
- latency
- temporary detection loss
- quantization effects
- environmental disturbances

A controller reacting too aggressively to noisy measurements can create instability.

A controller reacting too slowly allows tracking error to grow.

The image-plane error stage therefore becomes a balancing act between:

**responsiveness**  
and  
**measurement stability**

---

## How It Works

The fiducial detector produces a measured target location in image coordinates.

The system also defines a **desired target position**, typically near the center of the camera field of view.

The tracking error is computed as the offset between these two locations.

Conceptually:

**desired image location**  
minus  
**measured target location**

produces:

**tracking error**

The resulting signal is typically represented in image-space coordinates, such as:

- horizontal image offset
- vertical image offset

These measurements become the feedback signal for downstream steering systems.

When the target moves away from the desired location:

- the error grows
- corrective steering is commanded
- the target is driven back toward the desired position

The goal is not simply keeping the target visible.

The goal is keeping it **stable and centered**.

---

## Why Image-Space Error Matters

An important architectural decision is that the controller operates in **image space**, not only physical pointing coordinates.

This provides several advantages.

### Direct Measurement of What Matters

The system directly controls observed target placement rather than relying entirely on predicted geometry.

In practice:

**if the image looks correct, the system is correct**

This makes the controller naturally tolerant of:

- model inaccuracies
- alignment error
- calibration drift
- platform disturbances

---

### Unified Error Representation

Many disturbance sources ultimately appear the same in image space.

For example:

- pointing error
- vibration
- estimation drift
- structural flex
- actuator imperfections

All become:

**target movement inside the image**

This creates a unified correction framework.

---

### Improved Robustness

Because feedback comes from actual observation, the system can compensate for effects that were never explicitly modeled.

This often improves real-world performance compared with purely predictive approaches.

---

## Key Tradeoffs

### Stability vs Responsiveness

A highly responsive controller reacts quickly to disturbances.

However, aggressive response can amplify noise and create oscillation.

A more conservative controller improves stability but may allow larger residual error.

This trade becomes especially important when visual measurements are noisy or delayed.

---

### Precision vs Field-of-View Margin

Keeping the target tightly centered improves pointing precision.

However, aggressive centering behavior may increase the chance of temporary target loss during disturbances.

In many systems:

**stable tracking beats fragile perfection**

---

### Filtering vs Latency

Filtering improves measurement stability.

But filtering also introduces delay.

In a closed-loop tracking system, even modest latency can meaningfully affect disturbance rejection performance.

Choosing how much filtering to apply becomes a control problem as much as a perception problem.

---

## Implementation Considerations

### Coordinate Conventions

Sign conventions matter.

A simple coordinate mismatch between image axes and steering commands can invert control behavior and destabilize tracking.

Careful frame definition becomes essential.

---

### Pixel-to-Command Mapping

The system must relate image error to steering authority.

Questions include:

- how many pixels correspond to meaningful correction?
- when should correction saturate?
- how aggressively should motion be commanded?

These relationships often evolve through testing.

---

### Measurement Confidence

Not every frame should be trusted equally.

The controller may reduce authority or transition to degraded modes when:

- confidence drops
- measurements disappear
- tracking quality degrades

Reliable systems assume imperfect perception.

---

## Key Takeaways

- Image Plane Tracking Error transforms **observation into feedback**.
- This is the architectural bridge between **perception and control**.
- The controller responds to **image-space deviation**, not only predicted geometry.
- Real systems balance responsiveness, filtering, and robustness.
- Stable tracking often matters more than mathematically perfect centering.

---

## Back to System Overview

[← Dual-Mirror Optical Tracking](dual-mirror-optical-tracking.md)
[Continue to Fast Steering Mirror →](fast-steering-mirror.md)