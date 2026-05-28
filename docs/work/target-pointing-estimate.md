# Target Pointing Estimate

## How It Works

The target pointing estimate combines known target coordinates with the spacecraft state estimate to produce an initial prediction of where the optical payload should look. The spacecraft state is derived from multiple navigation and attitude sources, typically including inertial measurement units (IMUs), star trackers, GNSS/GPS receivers, onboard time references, and orbital propagation models maintained by the flight computer. Together, these systems estimate spacecraft position, velocity, attitude, and timing, providing the geometric context needed to predict where a known ground target should appear relative to the spacecraft body frame.

![](../assets/images/target-pointing-estimate-raster-wrapper.svg)

The target location, typically represented as a known latitude, longitude, and elevation, is transformed through a sequence of coordinate systems to determine an expected line of sight relative to the payload. Depending on system architecture, this transformation chain may include Earth-centered inertial (ECI), Earth-centered Earth-fixed (ECEF), orbital reference frames, spacecraft body coordinates, and payload-specific alignment frames. Timing accuracy becomes important because even small offsets between spacecraft state estimation, propagated orbit position, and camera exposure timing can translate into meaningful pointing error.

The resulting estimate is intentionally approximate rather than precise. Its purpose is not to close the tracking loop, but to narrow the search problem enough for the coarse steering system to place the target within the camera field of view. Once visual acquisition occurs, perception and closed-loop optical tracking progressively take over, refining pointing accuracy beyond what spacecraft state knowledge alone can provide.


## Key Takeaways

- Estimated ground track gives the system an initial search direction.
- It reduces the acquisition problem but does not solve precision tracking.
- The estimate must be useful without being over-trusted.
- Visual feedback is still required for final stabilization.

## Back to System Summary

<div style="display:flex; justify-content:space-between; align-items:center; margin-top:1rem;">

  <div>
    <a href="dual-mirror-optical-tracking.md">
      ← Dual-Mirror Optical Tracking
    </a>
  </div>

  <div style="text-align:right;">
    <a href="coarse-pointing-estimate.md">
      Continue to Coarse Pointing Estimate →
    </a>
  </div>

</div>