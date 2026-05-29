# Coarse Pointing Estimate

## Summary

The Coarse Pointing Estimate stage converts the predicted target direction into an initial steering command for the optical system. It bridges the gap between geometric target awareness and physical optical motion, transforming a target line-of-sight estimate into mirror roll and nod angles that can place the target inside the camera field of view.

The spacecraft body frame does not directly define where the payload optics are pointing. Even when the system has a reasonable estimate of target location, that information must be transformed through spacecraft geometry, payload alignment, and mirror kinematics before it becomes a usable steering command. The objective is acquisition, not precision tracking. The system only needs to point accurately enough for visual feedback to begin refining the solution.

## How It Works

The process begins with the estimated target direction produced by the Target Pointing Estimate stage. That direction, represented relative to the spacecraft body frame, is transformed into the reference frame of the Main Steering Mirror. Depending on payload architecture, this may involve fixed alignment offsets, optical boresight calibration terms, and coordinate transformations between spacecraft, payload, and actuator coordinate systems. The resulting geometry defines where the mirror must steer in order to align the optical path toward the expected target location.

![](../assets/images/coarse-pointing-estimate-raster-wrapper.svg)

The transformed line-of-sight vector is then converted into mirror commands, typically represented as roll and nod angles or equivalent actuator coordinates. These commands are intentionally approximate and are designed to place the target somewhere within the camera field of view rather than perfectly centered. Once the target becomes visible, visual perception and image-plane tracking progressively replace geometric prediction as the dominant pointing reference.

## Engineering Considerations

Coarse pointing accuracy is important, but over-investing in precision at this stage provides diminishing returns because visual feedback ultimately closes the loop. More important are robust frame conventions, correct sign handling, actuator saturation behavior, mirror travel limits, and graceful degradation when spacecraft state uncertainty grows. Small mistakes in coordinate definitions or mirror-axis conventions can produce pointing commands that move the optics in the wrong direction, making target acquisition unreliable.

## Key Takeaways

- Coarse pointing converts target geometry into steering mirror commands.
- It maps spacecraft-state estimation into optical actuation.
- Its purpose is acquisition support rather than precision stabilization.
- Correct frame definitions and sign conventions are critical.

## Back to System Summary

<div style="display:flex; justify-content:space-between; gap:1rem; margin-top:1rem;">

  <a class="md-button" href="../target-pointing-estimate/">
    ← Target Pointing Estimate
  </a>

  <a class="md-button md-button--primary" href="../main-steering-mirror/">
    Continue to Main Steering Mirror →
  </a>

</div>