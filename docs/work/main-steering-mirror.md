# Main Steering Mirror

## Summary

The Main Steering Mirror provides the coarse pointing layer of the optical tracking system. Instead of requiring the spacecraft body to continuously align with a moving target, the mirror redirects the payload line of sight independently. This decouples payload pointing from spacecraft attitude, allowing the vehicle to satisfy other constraints such as power generation, thermal orientation, communication geometry, reaction wheel management, and attitude stability while still maintaining optical target visibility.

The result is a system that behaves more like a stabilized sensing instrument than a rigidly body-pointed spacecraft payload. Spacecraft guidance provides the broader state context, the main steering mirror keeps the target within the optical acquisition envelope, and downstream perception and fine stabilization refine the image-plane pointing error.

## How It Works

The Main Steering Mirror receives roll and nod commands derived from the coarse pointing estimate. These commands reposition the optical line of sight so the predicted target location falls within the camera field of view. The mirror does not need to center the target precisely; its job is to absorb larger pointing offsets, compensate for slower geometry changes, and keep the acquisition problem small enough for camera-based perception to take over.

![](../assets/images/main-steering-mirror.svg)

This architecture separates large-angle optical steering from high-bandwidth stabilization. Spacecraft attitude control remains responsible for global vehicle orientation, the Main Steering Mirror provides larger line-of-sight authority, and the Fast Steering Mirror removes residual image-plane motion after the target is acquired. That separation is important because a single actuator optimized for large angular travel usually cannot also provide the bandwidth and precision needed for fine optical stabilization.

## Engineering Considerations 

The main engineering challenge is preserving correct geometry across the spacecraft body frame, payload alignment frame, mirror coordinate frame, and camera frame. Small sign errors, axis swaps, calibration offsets, or mirror convention mistakes can command motion in the wrong direction and make acquisition unreliable. The coarse steering layer also needs to respect mirror range limits, slew-rate constraints, actuator dynamics, and saturation behavior while still responding gracefully to target uncertainty or transient tracking loss.

## Key Takeaways

- The Main Steering Mirror decouples payload pointing from spacecraft attitude.
- It provides large-angle optical steering rather than precision stabilization.
- The architecture separates coarse pointing authority from fine correction bandwidth.
- It improves acquisition robustness, target visibility, and operational flexibility.
- The mirror bridges geometric estimation and image-based optical tracking.

## Back to System Summary

<div style="display:flex; justify-content:space-between; align-items:center; margin-top:1rem;">

  <div>
    <a href="coarse-pointing-estimate.md">
      ← Coarse Pointing Estimate
    </a>
  </div>

  <div style="text-align:right;">
    <a href="camera-observation.md">
      Continue to Camera Observation →
    </a>
  </div>

</div>