# Mechanical, electrical and control calculations

## 1. Mechanical, electrical, and control calculations for wheel-motor-driver mechatronic system {#mechanical-electrical-and-control-calculations-for-wheel-motor-driver-mechatronic-system}

### 1.1 Motor and gearbox overview {#motor-and-gearbox-overview}

| **Parameter**  | **Value**          |
|----------------|--------------------|
| Motor Model    | ZDBLD60-24GN-30S   |
| Rated Power    | 60 W               |
| Rated Voltage  | 24 V DC            |
| Rated Speed    | 3000 RPM (no load) |
| Gearbox Model  | 4GN 25K            |
| Gear Ratio     | 1 : 25             |
| Wheel Diameter | 200 mm             |
| Drive Type     | Differential drive |
| Driver         | ZBLD C20 120L2R    |

### 1.2 Definitions of main terms {#definitions-of-main-terms}

| **Term**         | **Definition**                                                                |
|------------------|-------------------------------------------------------------------------------|
| RPM              | Revolutions per minute - the number of full rotations completed in one minute |
| Torque (T)       | Rotational force output, measured in Newton-meters (Nm)                       |
| Gear Ratio (GR)  | The ratio of motor speed to output speed, or torque multiplication factor     |
| Wheel Radius (r) | Half of the wheel diameter, in meters                                         |
| Linear Speed (v) | Speed of vehicle movement on the ground surface (m/s)                         |
| Current (I)      | Electric current drawn by the motor, measured in Amperes (A)                  |
| Power (P)        | The rate of energy use or work done, measured in Watts (W)                    |

## 2. Motor output calculations {#motor-output-calculations}

### 2.1 Output RPM after gearbox {#output-rpm-after-gearbox}

**Formula:**

RPM_output = Motor_RPM / Gear_Ratio

**Substituting:**

RPM_output = 3000 / 25

**Result:**

RPM_output = 120 RPM

### 2.2 Torque at wheel after gearbox {#torque-at-wheel-after-gearbox}

**Formula:**

T_output = (P × t_sec) / (2 × π × Motor_RPM) × Gear_Ratio

Where:

- P is motor power (W)

- t_sec is the time conversion constant (60 seconds per minute)

- Motor_RPM is motor shaft speed before gearbox

- Gear_Ratio increases torque after gearbox

**Substituting:**

T_output = (60 × 60) / (2 × 3.1416 × 3000) × 25

**Result:**

T_output ≈ 4.77 Nm

### 2.3 Wheel peripheral speed {#wheel-peripheral-speed}

First, calculate wheel radius:

**Formula:**

r = Wheel_Diameter / 2

**Substituting:**

r = 0.2 m / 2

r = 0.1 m

Peripheral (linear) speed at output RPM:

**Formula:**

v = (2 × π × r × RPM_output) / t_sec

**Substituting:**

v = (2 × 3.1416 × 0.1 × 120) / 60

**Result:**

v ≈ 1.26 m/s

## 3. Electrical calculations {#electrical-calculations}

### 3.1 Rated current estimation {#rated-current-estimation}

Formula:

I = P / V

**Substituting:**

I = 60 / 24

**Result:**

I = 2.5 A

**Note:  
**Actual working current will be higher under load due to system
inefficiencies (e.g., friction, heat losses).

### 3.2 Current at peak load {#current-at-peak-load}

Startup or full-load current is typically 2× to 3× rated current:

**Estimated peak:**

Peak_Current ≈ 5 A to 7.5 A

## 4. Control system summary {#control-system-summary}

| **Component**          | **Function**                                         |
|------------------------|------------------------------------------------------|
| Teensy microcontroller | Low-level motor control and sensor feedback          |
| RS485 bus              | Communication with ESC driver (control + feedback)   |
| Raspberry Pi 5 (ROS2)  | High-level control (navigation, SLAM, teleoperation) |
| Motor driver modes     | RS485-based, optional PWM fallback                   |

## 5. Additional control-related calculations {#additional-control-related-calculations}

### 5.1 Encoder feedback via Hall sensors {#encoder-feedback-via-hall-sensors}

- Built-in Hall sensors inside the BLDC motor.

- Motor controller reads the Hall sensors and provides RPM data via
  > RS485 to Teensy.

**Odometry calculation basics:**

Formula for distance per wheel revolution:

Distance_per_revolution = 2 × π × r

Substituting:

Distance_per_revolution = 2 × 3.1416 × 0.1

Distance_per_revolution = 0.628 m

If the controller updates 100 times per second, each sample provides
partial movement estimation for odometry accumulation.

## 6. Summary table of key results {#summary-table-of-key-results}

| **Parameter**          | **Value**    |
|------------------------|--------------|
| Output wheel speed     | ≈ 120 RPM    |
| Output torque at wheel | ≈ 4.77 Nm    |
| Maximum ground speed   | ≈ 1.26 m/s   |
| Rated current          | 2.5 A        |
| Peak load current      | 5 A to 7.5 A |

## 7. Important notes {#important-notes}

- Real-world values may vary due to surface friction, payload, battery
  > state, etc.

- Proper safety margins (fuses, BMS limits) must be applied based on
  > peak current estimates.

- Odometry may use RPM data rather than physical encoders.

- Battery capacity must accommodate peak currents during acceleration
  > and emergency maneuvers.

## 8. Why these calculations matter {#why-these-calculations-matter}

| **Area**        | **Reason**                                                          |
|-----------------|---------------------------------------------------------------------|
| Mechanical      | Ensures correct motor sizing, gearbox matching, wheel performance   |
| Electrical      | Ensures correct wiring, battery choice, BMS setup, safety           |
| Control         | Accurate feedback loop tuning, stable autonomous operation          |
| Project success | Avoids overheating, overload, loss of control, and unsafe operation |

# Real world examples

## 1. Introduction {#introduction}

In robotics and mechatronics, calculations must be connected to
real-world operating conditions to ensure systems are:

- Safe

- Reliable

- Efficient

- Cost-effective

### 1.1 Delivery robot example {#delivery-robot-example}

A delivery robot must carry a **45 kg load** up a **10° slope**.  
Without correct motor torque sizing and battery estimation:

- It might **fail to climb**.

- It could **overload** the motors and electronics.

- It might **drain the battery too fast**.

Thus, precise force, torque, power, and control calculations are
essential before building.

### 1.2 Warehouse robot example {#warehouse-robot-example}

A robot operating on smooth surfaces (like tiles or polished concrete)
will:

- Require **lower starting torque** (less friction).

- Require **very accurate braking and steering** (to avoid sliding).

PID tuning and odometry corrections become critical.

### 1.3 Circle length calculation {#circle-length-calculation}

**Definition:** Circle circumference

**Circumference** is the total distance around the edge of a circle.

**Formula**:

C = 2 × π × r

Where:

- C = Circumference (meters, m)

- π ≈ 3.1416 (pi, a mathematical constant)

- r = Radius of the circle (meters)

**Example** (wheel radius 0.1 m):

C = 2 × 3.1416 × 0.1

C ≈ 0.628 m

**Meaning**:  
One complete wheel rotation moves the robot **62.8 cm forward**.

## 2. Torque and speed for real mass (45 kg) {#torque-and-speed-for-real-mass-45-kg}

### 2.1 Definition: Force (F) {#definition-force-f}

**Force** is an interaction that causes an object to change its motion
(accelerate).

**Formula**:

F = m × a

Where:

- F = Force (newtons, N)

- m = Mass (kilograms, kg)

- a = Acceleration (meters per second squared, m/s²)

**Calculation** (for 0.5 m/s² acceleration):

F = 45 × 0.5

F = 22.5 N

### 2.2 Definition: Torque (T) {#definition-torque-t}

**Torque** is the rotational equivalent of force. It measures how much a
force causes an object to rotate around an axis.

**Formula**:

T = F × r

Where:

- T = Torque (newton-meters, Nm)

- r = Lever arm (wheel radius in meters)

**Calculation**:

T = 22.5 × 0.1

T = 2.25 Nm

**Meaning**:  
[Each wheel must apply at least **2.25 Nm** of torque to accelerate the
robot at 0.5 m/s².]{.mark}

## 3. Power consumption calculation {#power-consumption-calculation}

### 3.1 Definition: Power (P) {#definition-power-p}

**Power** is the rate of doing work, or transferring energy.

**Formula**:

P = F × v

Where:

- P = Power (watts, W)

- F = Force (newtons, N)

- v = Velocity (meters per second, m/s)

**Calculation** (target speed 1.26 m/s):

P = 22.5 × 1.26

P ≈ 28.35 W

**Meaning**:  
At full speed, the robot needs about **28.35 watts** to maintain its
motion against resistance.

## 4. Slopes (positive and negative) {#slopes-positive-and-negative}

### 4.1 Definition: Slope {#definition-slope}

A **slope** is an inclined surface. In physics, moving on a slope means
additional forces act along the direction of motion due to gravity.

### 4.2 Positive slope (climbing) {#positive-slope-climbing}

**Formula for slope force**:

F_slope = m × g × sin(θ)

Where:

- g = 9.81 m/s² (gravity acceleration)

- θ = Slope angle in degrees

**Example for 10° slope**:

F_slope = 45 × 9.81 × sin(10°) ≈ 45 × 9.81 × 0.1736 ≈ 76.6 N

**Meaning**:  
An additional **76.6 N** must be overcome by the motors when climbing a
10° incline.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><h3
id="additional-force-on-slope-torque-and-power-calculation">Additional
force on slope, torque, and power calculation</h3>
<h4 id="what-does-an-additional-76.6-n-must-be-overcome-mean">1. What
does "an additional 76.6 N must be overcome" mean?</h4>
<p>When a robot moves <strong>on flat ground</strong>, the motors must
overcome:</p>
<ul>
<li><blockquote>
<p><strong>Inertia</strong> (mass resisting change of motion).</p>
</blockquote></li>
<li><blockquote>
<p><strong>Rolling resistance</strong> (small friction at wheels).</p>
</blockquote></li>
<li><blockquote>
<p><strong>Small air resistance</strong> (negligible at low robot
speeds).</p>
</blockquote></li>
</ul>
<p>On flat ground, the <strong>required force to accelerate</strong> the
robot is:</p>
<p>F_flat = m × a</p>
<p>Where:</p>
<ul>
<li><blockquote>
<p>m = mass (kilograms, kg)</p>
</blockquote></li>
<li><blockquote>
<p>a = acceleration (meters per second squared, m/s²)</p>
</blockquote></li>
</ul>
<p>Given:</p>
<ul>
<li><blockquote>
<p>m = 45 kg</p>
</blockquote></li>
<li><blockquote>
<p>a = 0.5 m/s²</p>
</blockquote></li>
</ul>
<p>Calculation:</p>
<p>F_flat = 45 × 0.5 = 22.5 N</p>
<p>Thus, <strong>on a flat surface</strong>, <strong>22.5 N</strong> is
needed to start or accelerate the robot.</p>
<p>When <strong>climbing a slope</strong> (an inclined surface):</p>
<ul>
<li><blockquote>
<p>Gravity exerts an additional <strong>downward force</strong> along
the slope.</p>
</blockquote></li>
<li><blockquote>
<p>This additional force must be <strong>overcome by the motors</strong>
to prevent rolling backwards.</p>
</blockquote></li>
</ul>
<p>The <strong>slope force</strong> is:</p>
<p>F_slope = m × g × sin(θ)</p>
<p>Where:</p>
<ul>
<li><blockquote>
<p>g = 9.81 m/s² (gravitational acceleration),</p>
</blockquote></li>
<li><blockquote>
<p>θ = slope angle in degrees.</p>
</blockquote></li>
</ul>
<p>Given:</p>
<ul>
<li><blockquote>
<p>θ = 10°</p>
</blockquote></li>
<li><blockquote>
<p>sin(10°) ≈ 0.1736</p>
</blockquote></li>
</ul>
<p>Calculation:</p>
<p>F_slope = 45 × 9.81 × 0.1736</p>
<p>F_slope ≈ 76.6 N</p>
<h4 id="total-force-needed-when-climbing">2. Total force needed when
climbing</h4>
<p>The <strong>total force</strong> the robot motors must produce when
climbing is the <strong>sum</strong> of:</p>
<ul>
<li><blockquote>
<p>The normal force to accelerate horizontally (F_flat),</p>
</blockquote></li>
<li><blockquote>
<p>The additional force to overcome gravity (F_slope).</p>
</blockquote></li>
</ul>
<p>Thus:</p>
<p>F_total = F_flat + F_slope</p>
<p>Substituting:</p>
<p>F_total = 22.5 + 76.6</p>
<p>F_total ≈ 99.1 N</p>
<h4 id="why-an-additional-76.6-n">3. Why "an additional 76.6 N"?</h4>
<p><strong>Meaning</strong>:</p>
<ul>
<li><blockquote>
<p>Motors already must produce <strong>22.5 N</strong> to accelerate the
robot horizontally.</p>
</blockquote></li>
<li><blockquote>
<p><strong>When climbing</strong>, they must generate an <strong>extra
76.6 N</strong> to resist the gravitational pull downhill.</p>
</blockquote></li>
</ul>
<p>Thus, a total of <strong>99.1 N</strong> must be overcome to climb
while accelerating.</p>
<h4 id="torque-required-for-slope-climbing">4. Torque required for slope
climbing</h4>
<p><strong>Definition: Torque</strong></p>
<p><strong>Torque</strong> is a measure of the rotational force applied
around an axis (for example, the wheel axle).</p>
<p><strong>Formula</strong>:</p>
<p>T = F × r</p>
<p>Where:</p>
<ul>
<li><blockquote>
<p>T = Torque (newton-meters, Nm)</p>
</blockquote></li>
<li><blockquote>
<p>F = Force (newtons, N)</p>
</blockquote></li>
<li><blockquote>
<p>r = Wheel radius (meters, m)</p>
</blockquote></li>
</ul>
<p>Given:</p>
<ul>
<li><blockquote>
<p>F_total = 99.1 N</p>
</blockquote></li>
<li><blockquote>
<p>r = 0.1 m</p>
</blockquote></li>
</ul>
<p>Calculation:</p>
<p>T = 99.1 × 0.1</p>
<p>T ≈ 9.91 Nm</p>
<p><strong>Differential drive: two motors</strong></p>
<p>In a <strong>differential drive</strong> system:</p>
<ul>
<li><blockquote>
<p>Two wheels share the load.</p>
</blockquote></li>
<li><blockquote>
<p>Each wheel must provide <strong>half</strong> the total torque.</p>
</blockquote></li>
</ul>
<p>Thus, <strong>torque per wheel</strong>:</p>
<p>T_per_wheel = T_total / 2</p>
<p>Substituting:</p>
<p>T_per_wheel = 9.91 / 2</p>
<p>T_per_wheel ≈ 4.955 Nm</p>
<h4 id="power-required-for-slope-climbing">5. Power required for slope
climbing</h4>
<p><strong>Definition: Power</strong></p>
<p><strong>Power</strong> is the rate at which work is done or energy is
transferred.</p>
<p><strong>Formula</strong>:</p>
<p>P = F × v</p>
<p>Where:</p>
<ul>
<li><blockquote>
<p>P = Power (watts, W)</p>
</blockquote></li>
<li><blockquote>
<p>F = Force (newtons, N)</p>
</blockquote></li>
<li><blockquote>
<p>v = Velocity (meters per second, m/s)</p>
</blockquote></li>
</ul>
<p>Assume target velocity:</p>
<ul>
<li><blockquote>
<p>v = 1.26 m/s (as given earlier)</p>
</blockquote></li>
</ul>
<p>Calculation:</p>
<p>P = 99.1 × 1.26</p>
<p>P ≈ 124.9 W</p>
<p>Thus, total <strong>mechanical power required</strong> to climb at
1.26 m/s is <strong>about 125 W</strong>.</p>
<p>If divided equally between two motors:</p>
<p>P_per_motor ≈ 62.45 W</p>
<h4 id="summary-table">6. Summary table</h4>
<table>
<colgroup>
<col style="width: 35%" />
<col style="width: 13%" />
<col style="width: 51%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameter</strong></th>
<th><strong>Value</strong></th>
<th><strong>Explanation</strong></th>
</tr>
<tr class="odd">
<th>Force on flat ground</th>
<th>22.5 N</th>
<th>Force to accelerate horizontally.</th>
</tr>
<tr class="header">
<th>Additional force on 10° slope</th>
<th>76.6 N</th>
<th>Extra gravitational force to overcome.</th>
</tr>
<tr class="odd">
<th>Total force to climb</th>
<th>99.1 N</th>
<th>Combined force needed.</th>
</tr>
<tr class="header">
<th>Total torque required</th>
<th>9.91 Nm</th>
<th>Torque needed from both wheels combined.</th>
</tr>
<tr class="odd">
<th>Torque per wheel</th>
<th>4.955 Nm</th>
<th>Torque needed from each wheel.</th>
</tr>
<tr class="header">
<th>Total power required</th>
<th>124.9 W</th>
<th>Power needed to maintain speed uphill.</th>
</tr>
<tr class="odd">
<th>Power per motor</th>
<th>62.45 W</th>
<th>Power per wheel motor.</th>
</tr>
</thead>
<tbody>
</tbody>
</table>
<h4 id="final-explanation">7. Final explanation</h4>
<ul>
<li><blockquote>
<p>On flat ground, motors must provide <strong>only inertia-based
force</strong>.</p>
</blockquote></li>
<li><blockquote>
<p>On slopes, <strong>gravity adds extra load</strong>.</p>
</blockquote></li>
<li><blockquote>
<p>Motors must be sized not only for flat motion but also for
<strong>worst-case scenarios</strong> like climbing.</p>
</blockquote></li>
<li><blockquote>
<p>Correct calculation ensures the robot <strong>can climb
safely</strong> without overloading motors or batteries.</p>
</blockquote></li>
</ul></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### 4.3 Negative slope (descending) {#negative-slope-descending}

When descending:

- Gravity **accelerates** the robot downhill.

- Motors must provide **braking torque** to **control the descent**.

- PID controllers must be tuned to avoid **unstable behavior**.

## 5. PID controller definition {#pid-controller-definition}

### 5.1 What is a PID controller? {#what-is-a-pid-controller}

A **PID controller** is a control algorithm used in mechatronics to
automatically adjust motor output to reach and maintain a desired value
(e.g., speed, position).

**Components**:

| **Part**         | **Description**                                                                |
|------------------|--------------------------------------------------------------------------------|
| Proportional (P) | Corrects based on current error (fast response).                               |
| Integral (I)     | Corrects based on accumulated error over time (eliminates steady-state error). |
| Derivative (D)   | Predicts future errors (damps oscillations and overshoot).                     |

**Why use PID?**

- To control motor speed and position **smoothly and accurately**.

- To react dynamically to changes (slopes, friction).

## 6. Differential drive system total torque {#differential-drive-system-total-torque}

### 6.1 Definition: Differential drive {#definition-differential-drive}

A **differential drive** robot moves by varying the speed and direction
of two independently driven wheels.

- Moving straight: both wheels at the same speed.

- Turning: wheels at different speeds or opposite directions.

### 6.2 Calculating total torque {#calculating-total-torque}

Each wheel must provide torque individually.

**Formula**:

T_total = 2 × T_single_wheel

Example:

T_total = 2 × 2.25 = 4.5 Nm

**Meaning**:  
For straight acceleration, the **robot needs 4.5 Nm total** distributed
equally between the two motors.

## 7. Encoder and resolution calculation {#encoder-and-resolution-calculation}

### 7.1 Definition: Encoder {#definition-encoder}

An **encoder** is a sensor that generates a number of pulses or signals
for every rotation of a shaft, enabling precise measurement of rotation.

### 7.2 Effective encoder resolution {#effective-encoder-resolution}

If an encoder outputs **500 pulses per motor revolution**, and the
gearbox has **25:1 reduction**:

Wheel_PPR = 500 × 25 = 12,500 pulses per wheel revolution

**Distance per pulse**:

Distance_per_pulse = Circumference / Wheel_PPR

Distance_per_pulse = 0.628 / 12,500 ≈ 0.00005024 m ≈ 0.05 mm

**Meaning**:  
Each encoder pulse corresponds to **about 0.05 mm** of wheel movement.

## 8. PWM definition {#pwm-definition}

8.1 What is PWM?

**Pulse width modulation (PWM)** is a technique to control the amount of
power delivered to an electrical device by switching it ON and OFF
rapidly.

- **Duty cycle**: the proportion of time the signal is ON during one
  > cycle.

- **Higher duty cycle** = **more power** to the motor.

**Example**:

- 50% duty cycle → motor receives half the full voltage.

- 80% duty cycle → motor receives 80% of full voltage.

## 9. Real robot velocity vs estimated one, feedback, odometry {#real-robot-velocity-vs-estimated-one-feedback-odometry}

### 9.1 Definition: Odometry {#definition-odometry}

**Odometry** is the process of using data from sensors (like wheel
encoders) to estimate a robot's position and orientation over time.

### 9.2 Real world vs estimated {#real-world-vs-estimated}

- **Estimated position** comes from calculated wheel movement.

- **Real position** may differ due to:

  - Slippage

  - Uneven floor

  - Wheel deformation

  - Encoder errors

### 9.3 Feedback mechanisms {#feedback-mechanisms}

| **Sensor**                      | **Purpose**                                |
|---------------------------------|--------------------------------------------|
| Wheel encoder                   | Measure rotation and distance.             |
| Hall sensor                     | Measure motor shaft speed.                 |
| Inertial Measurement Unit (IMU) | Measure acceleration and rotation.         |
| Visual odometry                 | Use cameras to correct position estimates. |

## 10. Conclusion {#conclusion}

With these advanced calculations, definitions, and considerations:

- Mechanical design is validated for forces, torques, and slopes.

- Electrical system sizing (current, power) is validated.

- Control system design (PID, PWM, odometry) is fully prepared.

- Real-world operating conditions are considered for accuracy and
  > safety.

## Diagram 1: Forces on flat ground

Top view - Robot moving forward on flat ground

(Front of robot)

↑

\| (Force F_flat = m × a)

\|

+\-\-\--+\-\-\--+

\| \| \-\-\-\--\> Direction of motion

\| ROBOT \|

\| \|

+\-\-\--+\-\-\--+

\|

v

(Rear of robot)

Forces:

\- F_flat: needed to accelerate mass.

\- Minor frictional forces oppose motion (small).

\- No gravity component along the ground.

**Key points**:

- Only acceleration force and rolling friction matter.

- Motors must produce enough torque to create F_flat.

## Diagram 2: Forces when climbing a slope

Side view - Robot climbing a slope

      (Gravity force m×g)    
               ↓    
            +----+    
           /      \    
          /  ROBOT \    
         +----------+    
        θ (slope angle)    

Forces:

\- Gravity splits into two components:

\- Perpendicular to slope (presses robot against slope).

\- Parallel to slope (tries to pull robot downwards):

F_slope = m × g × sin(θ)

\- Motors must overcome:

\- F_flat (for acceleration)

\- F_slope (gravity component)

Resulting Force:

F_total = F_flat + F_slope

**Key Points**:

- Slopes introduce significant additional force requirements.

- Steeper slopes = larger sin(θ) = larger F_slope.

- Motors must deliver both torque for acceleration **and** additional
  > torque for gravity.

## Diagram 3: Torque generation at the wheel

Side view of one drive wheel    

        [Motor Shaft]---->[Gearbox]---->[Wheel]    
                                 |    
                                 v    
                                (r)    
                                 |    
                                [Ground]    


**Forces:**

\- Torque T = F × r

\- Force F is exerted by wheel against ground.

\- Radius r is the lever arm.

\- Ground applies reaction force to move robot forward.

**How it works:**

\- Motor produces torque T.

\- Torque T pushes the wheel rim.

\- Wheel transfers force to ground, robot moves.

*Bigger radius → More force needed.*

*Bigger force → More torque needed.*

**Key points**:

- The larger the wheel, the larger torque needed.

- Torque is rotational force; it directly defines a robot\'s ability to
  > start moving or climb slopes.

**Summary**

| **Diagram** | **Represents**          | **Key Forces/Concepts**            |
|-------------|-------------------------|------------------------------------|
| Diagram 1   | Flat ground motion      | Only F_flat needed to accelerate.  |
| Diagram 2   | Uphill motion           | F_flat + F_slope must be overcome. |
| Diagram 3   | Wheel torque generation | T = F × r relationship explained.  |


