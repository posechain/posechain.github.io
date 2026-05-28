# Fast Steering Mirror (FSM)

## Summary

The Fast Steering Mirror (FSM) provides the **high-bandwidth stabilization layer** of the optical tracking system.

By the time control reaches the FSM, the Main Steering Mirror has already performed large-angle pointing and the perception system has established image-plane tracking error.

What remains are the smaller, faster disturbances that prevent precision tracking.

The FSM exists to remove this residual motion.

Rather than repositioning the optical line of sight over large angles, the FSM performs rapid fine corrections to stabilize the target inside the image.

This is where the dual-mirror architecture delivers its primary advantage:

**coarse steering maintains visibility**  
**fine steering maintains precision**

---

## Why It Exists

The Main Steering Mirror solves the large-angle problem.

It does not solve the fast disturbance problem.

Real systems experience motion from sources such as:

- platform vibration
- actuator disturbance
- structural dynamics
- pointing jitter
- estimation error
- environmental disturbances

Many of these effects occur at frequencies too high for coarse steering mechanisms to reject effectively.

Attempting to force a large steering mechanism to solve both coarse and fine control problems generally leads to poor performance in both.

The Fast Steering Mirror exists because:

**large authority and high bandwidth are fundamentally different engineering problems**

The architecture intentionally separates them.

---

## Engineering Challenge

The challenge is deceptively difficult:

**remove disturbances quickly without destabilizing the system**

High-bandwidth systems face competing demands:

### Responsiveness

The FSM must react quickly enough to suppress motion before image quality degrades.

Slow correction reduces stabilization effectiveness.

---

### Stability

Aggressive correction risks:

- oscillation
- overshoot
- amplified measurement noise
- actuator instability

High responsiveness without stability becomes unusable.

---

### Limited Authority

Unlike the Main Steering Mirror, the FSM typically operates over a relatively small range of motion.

It cannot recover from large pointing errors.

Its job is:

**small motion, extremely fast**

This creates a critical architectural dependency:

the coarse steering system must keep the target sufficiently close to center for the FSM to remain effective.

---

## How It Works

The FSM receives image-plane tracking error from the visual feedback system.

Rather than commanding large-angle repositioning, it applies rapid, fine steering corrections to minimize residual image motion.

Conceptually:

**target drifts from desired location**  
→ **image-space error increases**  
→ **FSM applies correction**  
→ **target returns toward center**

Because the FSM operates at higher bandwidth than the coarse steering layer, it can reject disturbances before they become visually significant.

In practice, the system behaves like two nested steering loops:

| Layer | Purpose |
|--------|---------|
| Main Steering Mirror | Keep target inside observable region |
| Fast Steering Mirror | Suppress residual image motion |

This separation of responsibilities is one of the defining architectural choices of the system.

---

## Why Use Two Steering Layers?

At first glance, using two mirrors may appear unnecessarily complex.

In practice, it is often the cleanest solution.

### One Mechanism Cannot Optimize Both Problems

Large-angle steering favors:

- wide motion range
- robustness
- acquisition support

Fine stabilization favors:

- low inertia
- fast response
- precision motion

Trying to combine both into one mechanism usually produces a compromise that performs neither task particularly well.

---

### Bandwidth Separation Improves Stability

Separating steering responsibilities reduces controller conflict.

The coarse system handles:

**slow, large corrections**

The fine system handles:

**fast, small corrections**

This reduces actuator contention and improves overall stability.

---

### Disturbance Rejection Becomes Practical

Many disturbances happen too quickly for spacecraft attitude or coarse optics to compensate.

The FSM allows the system to suppress these disturbances directly in the optical path.

This often produces dramatically better pointing performance.

---

## Key Tradeoffs

### Bandwidth vs Noise Sensitivity

Higher bandwidth improves disturbance rejection.

However, very aggressive control can amplify:

- sensor noise
- latency effects
- image jitter
- unstable dynamics

The optimal operating point balances responsiveness with robustness.

---

### Authority vs Precision

A larger steering range generally increases inertia and reduces responsiveness.

An FSM is intentionally designed around:

**precision over range**

This makes architecture coordination with the coarse steering layer essential.

---

### Complexity vs Performance

Adding a second steering stage increases:

- control complexity
- calibration requirements
- tuning effort
- integration burden

However, for demanding precision applications, the performance improvement often justifies the added complexity.

---

## Implementation Considerations

### Latency Matters

High-bandwidth stabilization is extremely sensitive to delay.

Latency can originate from:

- camera frame timing
- image processing
- communication paths
- actuator response
- filtering

Even modest delays can significantly reduce disturbance rejection performance.

---

### Controller Tuning

The FSM controller must balance:

- disturbance rejection
- stability margins
- measurement noise tolerance
- actuator limitations

In practice, tuning becomes highly dependent on the disturbance environment.

---

### Saturation and Handoff

The FSM cannot solve large errors indefinitely.

When disturbances exceed its authority, the system must coordinate with the Main Steering Mirror to recenter the operating point.

Robust systems treat this as a cooperative interaction rather than independent control loops.

---

## Key Takeaways

- The FSM provides **high-bandwidth residual stabilization**.
- It exists because coarse steering cannot reject fast disturbances effectively.
- The system separates **large-angle authority** from **fine precision bandwidth**.
- High-performance stabilization depends heavily on latency and tuning.
- The dual-mirror architecture enables both **robust acquisition** and **precision tracking**.

---

## Back to System Overview

[← Dual-Mirror Optical Tracking](dual-mirror-optical-tracking.md)
[Continue to Fine Optical Stabilization →](fine-optical-stabilization.md)