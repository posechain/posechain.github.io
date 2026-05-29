# Dual-Mirror Optical Tracking & Reference Stabilization

## Summary

A dual-stage optical tracking architecture for precision stabilization of a cooperative visual reference target.

The system combined:

- **Coarse optical steering** using a main steering mirror to maintain line-of-sight alignment to an estimated ground track
- **Fine optical stabilization** using a fast steering mirror (FSM) for high-bandwidth correction
- **Vision-based reference tracking** using a large ArUco fiducial as a geometric visual reference
- **Predictive control concepts** to improve tracking performance under latency and disturbances

The project explored how **perception, controls, estimation, and real-time software** interact in a precision optical system operating under imperfect knowledge and real-world constraints.

### Tracking Concept

The system performed closed-loop stabilization using a dual-mirror optical architecture.

<div class="system-flow">

  <div class="flow-card">
    <a class="flow-card-link" href="../target-pointing-estimate/">
      <img class="flow-icon-img"
           src="../../assets/icons/estimated-ground-track.svg"
           alt="Target Pointing Estimate">
      <span class="flow-title">Target Pointing Estimate</span> 
    </a>
  </div>

  <div class="flow-card">
    <a class="flow-card-link" href="../coarse-pointing-estimate/">
      <img class="flow-icon-img"
           src="../../assets/icons/coarse-pointing-estimate.svg"
           alt="Coarse Pointing Estimate">
      <span class="flow-title">Coarse Pointing Estimate</span>
    </a>
  </div>

  <div class="flow-card">
    <a class="flow-card-link" href="../main-steering-mirror/">
      <img class="flow-icon-img"
           src="../../assets/icons/main-steering-mirror-final-fixed.svg"
           alt="Main Steering Mirror">
      <span class="flow-title">Main Steering Mirror</span>
    </a>
  </div>

  <!-- intentionally swapped icon assignment -->
  <div class="flow-card">
    <a class="flow-card-link" href="../camera-observation/">
      <img class="flow-icon-img"
           src="../../assets/icons/aruco-fiducial-detection-offsetfixed.svg"
           alt="Camera Observation">
      <span class="flow-title">Camera Observation</span>
    </a>
  </div>

  <!-- intentionally swapped icon assignment -->
  <div class="flow-card">
    <a class="flow-card-link" href="../aruco-fiducial-detection/">
      <img class="flow-icon-img"
           src="../../assets/icons/image-plane-tracking-error-centered-thinborder.svg"
           alt="ArUco Fiducial Detection">
      <span class="flow-title">ArUco Fiducial Detection</span>
    </a>
  </div>

  <!-- intentionally swapped icon assignment -->
  <div class="flow-card">
    <a class="flow-card-link" href="../image-plane-tracking-error/">
      <img class="flow-icon-img"
           src="../../assets/icons/camera-observation-centered-thinborder.svg"
           alt="Image Plane Tracking Error">
      <span class="flow-title">Image Plane Tracking Error</span>
    </a>
  </div>

  <div class="flow-card">
    <a class="flow-card-link" href="../fast-steering-mirror/">
      <img class="flow-icon-img"
           src="../../assets/icons/fast-steering-mirror-literal.svg"
           alt="Fast Steering Mirror">
      <span class="flow-title">Fast Steering Mirror</span>
    </a>
  </div>

  <div class="flow-card">
    <a class="flow-card-link" href="../fine-optical-stabilization/">
      <img class="flow-icon-img"
           src="../../assets/icons/fine-optical-stabilization-normalized.svg"
           alt="Fine Optical Stabilization">
      <span class="flow-title">Fine Optical Stabilization</span>
    </a>
  </div>

</div>
---

## Problem Context

### Objective

Maintain precision alignment to a cooperative ground reference target despite:

- imperfect coarse pointing knowledge
- changing line-of-sight geometry
- vibration and disturbances
- camera latency
- limited field of view
- actuator bandwidth limitations

The system architecture separated large-angle pointing from high-bandwidth stabilization to improve robustness and tracking precision.

### Why It Was Hard

A single optical steering stage created competing requirements:

| Requirement | Design Pressure |
|---|---|
| Large pointing corrections | favors slower, large-range actuation |
| Fine stabilization | favors small, high-bandwidth actuation |
| Camera latency | reduces achievable control bandwidth |
| Disturbances and jitter | benefit from predictive compensation |
| Narrow field of view | increases acquisition sensitivity |

The result was a **coarse/fine dual-mirror architecture**, where each mirror solved a different part of the control problem.

---

## System Architecture




## Major System Elements

### Coarse Steering Layer

The main steering mirror maintained approximate line-of-sight alignment using estimated target geometry and lower-bandwidth corrections.

> **Focus:** acquisition, large-angle motion, target visibility, and reducing FSM authority demands.

### Fine Stabilization Layer

The fast steering mirror corrected residual image-plane tracking error.

> **Focus:** high-bandwidth stabilization, disturbance rejection, fine pointing correction, and maintaining precise target alignment.

<div style="display:flex; justify-content:flex-end; gap:1rem; margin-top:1rem;">

  <a class="md-button md-button--primary" href="../target-pointing-estimate/">
    Continue to Target Pointing Estimate →
  </a>

</div>