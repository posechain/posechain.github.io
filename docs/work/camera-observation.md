# Camera Observation

## Summary

The Camera Observation stage marks the transition from geometric prediction to direct visual sensing. Up to this point, the system relies primarily on spacecraft state knowledge, target geometry, and mirror pointing estimates to place the expected target within the camera field of view. Once the target becomes visible, the optical system can begin observing the real scene and refining pointing based on measured image data rather than prediction alone.

In this system, the cooperative visual target is an ArUco fiducial marker. ArUco markers are patterned visual targets designed for reliable detection and pose estimation using a camera. Because the geometry of the marker is known in advance, the system can estimate both target location and orientation relative to the camera. This makes them especially useful in controlled or well-lit environments where deterministic tracking performance is more important than broad environmental robustness.

## How It Works

The Main Steering Mirror places the expected target location within the camera field of view using the coarse pointing estimate. Once visible, the camera provides direct image measurements of the scene, allowing the system to begin correcting for uncertainty in spacecraft state estimation, mirror calibration, timing offsets, and other geometric assumptions that accumulate through the upstream pointing process.

![](../assets/icons/aruco-fiducial-detection-offsetfixed.svg){ width="25%" }

Rather than immediately performing precision stabilization, the camera observation layer establishes whether the target has been successfully acquired and supplies visual information for downstream perception algorithms. In this implementation, the system uses an ArUco fiducial marker because it enables robust target localization and relative pose estimation with comparatively lightweight computation. The detailed detection process, marker identification, and pose-solving pipeline are handled in the following stage.

## Engineering Considerations

Camera observation sits at an important systems boundary between prediction and perception. Acquisition performance depends not only on camera quality, but also on optical field of view, exposure settings, target visibility, illumination, motion blur, and the accuracy of upstream coarse pointing. Even a strong perception algorithm performs poorly if the target never enters the camera field of view or appears too small, blurred, or poorly illuminated for reliable detection.

## Key Takeaways

- Camera observation transitions the system from prediction to visual sensing.
- The Main Steering Mirror places the target inside the camera field of view.
- ArUco markers were selected for reliable detection and pose estimation in cooperative, well-lit environments.
- Visual measurements progressively replace geometric prediction as the dominant pointing reference.

## Back to System Summary

<div style="display:flex; justify-content:space-between; align-items:center; margin-top:1rem;">

  <div>
    <a href="main-steering-mirror.md">
      ← Main Steering Mirror
    </a>
  </div>

  <div style="text-align:right;">
    <a href="aruco-fiducial-detection.md">
      Continue to ArUco Fiducial Detection →
    </a>
  </div>

</div>