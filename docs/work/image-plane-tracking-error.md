# Image Plane Tracking Error

## Summary

Detecting the target is not enough.

The system must convert visual observation into a control signal.

The Image Plane Tracking Error stage transforms the detected marker position into a measurable deviation from where the target is intended to appear in the image. In this system, the desired location is assumed to be the center of the image plane for simplicity, though other reference locations could be used depending on mission objectives or optical constraints.

This stage forms the architectural bridge between **perception and control**. The output is no longer simply an observation of where the marker exists in the image. Instead, it becomes an actionable feedback signal used to command the steering mirrors and stabilize the optical line of sight.

## How It Works

The ArUco fiducial detector provides a measured marker position in image coordinates. Because the marker contains a center corner, the system can identify a stable geometric reference point rather than relying on intensity centroids or ambiguous feature locations. The detected center is compared against a desired reference location, typically the image center, producing a horizontal and vertical image-space error.

![](../assets/images/image-plane-tracking-error.svg)

The resulting tracking error is represented in image coordinates:

\[
\Delta u = u_m - u_0
\]

\[
\Delta v = v_m - v_0
\]

where:

- \(u_m, v_m\) are the measured marker center coordinates
- \(u_0, v_0\) are the desired reference coordinates

The total image-plane tracking error can be represented as a vector:

\[
\mathbf{e} =
\begin{bmatrix}
\Delta u \\
\Delta v
\end{bmatrix}
\]

with magnitude:

\[
|\mathbf{e}| =
\sqrt{
(\Delta u)^2 +
(\Delta v)^2
}
\]

The controller uses these error components to determine how the mirrors should move to drive the marker back toward the reference point.

## Why Image-Space Error Matters

A key architectural decision in this system is that control occurs in **image space**, not solely in predicted physical pointing coordinates.

This approach offers an important practical advantage:

> If the image looks correct, the system is correct.

Rather than relying entirely on spacecraft geometry, calibration models, or actuator estimates, the controller responds to what the camera actually observes. This naturally compensates for many real-world effects that are difficult to model perfectly, including:

- pointing estimation error
- alignment offsets
- thermal distortion
- structural flex
- vibration
- actuator nonlinearities
- calibration drift

Many different disturbance sources ultimately appear the same to the controller:

**motion of the target inside the image**

This creates a unified feedback framework that allows the system to reject disturbances without explicitly modeling every disturbance source.

## Engineering Tradeoffs

### Stability vs Responsiveness

Image measurements contain noise, quantization effects, timing uncertainty, and occasional detection loss.

A controller reacting too aggressively can amplify noise and oscillate.

A controller reacting too slowly allows tracking error to grow.

## Back to System Summary

<div style="display:flex; justify-content:space-between; gap:1rem; margin-top:1rem;">

  <a class="md-button" href="../aruco-fiducial-detection/">
    ← ArUco Fiducial Detection
  </a>

  <a class="md-button md-button--primary" href="../fast-steering-mirror/">
    Continue to Fast Steering Mirror →
  </a>

</div>