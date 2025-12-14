# -Interactive-B-zier-Curve-with-Physics-Sensor-Control
Interactive cubic Bézier rope simulation built from scratch. Implements manual Bézier math, analytical tangents, and spring–damping physics to create smooth, rope-like motion. Fully interactive via mouse/touch, rendered at ~60 FPS using HTML5 Canvas and vanilla JavaScript.
Interactive Cubic Bézier Rope Simulation

This project implements an interactive cubic Bézier curve that behaves like a springy rope.
The goal was to build the entire system from first principles, including Bézier mathematics,
tangent computation, and real-time spring-based motion, without relying on any built-in
Bézier or physics libraries.

The visualization responds interactively to user input and updates smoothly in real time.

--------------------------------------------------
Mathematical Model
--------------------------------------------------

The curve used is a cubic Bézier curve defined by four control points:

P₀ and P₃ : Fixed endpoints  
P₁ and P₂ : Dynamic control points  

The Bézier curve equation is:

B(t) = (1 − t)³ P₀ + 3(1 − t)² t P₁ + 3(1 − t) t² P₂ + t³ P₃

where t ∈ [0, 1].

The curve is sampled at small intervals (Δt = 0.01) and rendered as a polyline by connecting
successive sampled points. This ensures a smooth visual curve while keeping the implementation
fully manual.

--------------------------------------------------
Tangent Computation
--------------------------------------------------

To visualize the direction of the curve, tangent vectors are computed using the analytical
derivative of the cubic Bézier curve:

B′(t) = 3(1 − t)² (P₁ − P₀)
      + 6(1 − t) t (P₂ − P₁)
      + 3 t² (P₃ − P₂)

The derivative is normalized and short tangent line segments are drawn at regular intervals
along the curve. This provides a clear visual representation of the curve’s local direction.

--------------------------------------------------
Physics Model (Spring–Damping)
--------------------------------------------------

The dynamic control points P₁ and P₂ follow a simple mass–spring–damper system to achieve
smooth, natural motion:

a = −k (x − x_target) − c v

where:
- k is the spring stiffness
- c is the damping coefficient
- v is velocity

Velocity and position are updated each frame using semi-implicit Euler integration:

v ← v + a · Δt  
x ← x + v · Δt  

This model allows the curve to stretch, oscillate, and settle naturally when the user
interacts with it.

--------------------------------------------------
Interaction & Rendering
--------------------------------------------------

- The endpoints remain fixed.
- The control points are influenced by mouse or touch input via spring targets.
- Rendering is performed using HTML5 Canvas.
- The animation loop runs at approximately 60 FPS using requestAnimationFrame.
- All math, physics, and rendering logic is implemented manually.

--------------------------------------------------
Platform Notes
--------------------------------------------------

The web version is fully implemented and demonstrated.

An equivalent iOS (UIKit + CoreMotion) version was designed using the same math and physics
logic. Execution of the iOS version requires macOS and a physical iOS device; therefore, only
the web implementation is executed and recorded.

--------------------------------------------------
Files Submitted
--------------------------------------------------

- index.html  → Complete source code
- README.md   → Project explanation
- demo.mp4    → Screen recording of interaction (≤ 30 seconds)
