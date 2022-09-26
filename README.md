# Dynamic  Clay Shooting Project

Dynamic motor control and mechanism for shooting clay blobs.

Investigation of using brushless motor to directly drive a clay shooting wheel. 



# Hardware

## Design parameters

Bullet Dimension

| Properties                 | unit | Min  | Nominal | Max  |
| -------------------------- | ---- | ---- | ------- | ---- |
| Diameter                   | mm   |      | 70      |      |
| Length                     | mm   |      | 100     |      |
| Weight                     | kg   |      | 0.75    |      |
|                            |      |      |         |      |
| Intended Exit Velocity     | m/s  |      | 10      |      |
|                            |      |      |         |      |
| Current Belt Length        | mm   |      | 700     |      |
| Current Barrel Entry Width | mm   | 50   |         | 60   |
| Current Barrel Exit Width  | mm   | 20   |         | 30   |



## Calculations

### Kinetic Energy on Bullet

https://www.vcalc.com/equation/?uuid=d99b2190-c572-11e3-b7aa-bc764e2038f2

**K.E. = 1/2 m v2**

| Bullet Weight (kg)   | Velocity (m/s)      | Kinetic Energy (J) |
| -------------------- | ------------------- | ------------------ |
| 0.75 (Design Target) | 10  (Design Target) | 37.5               |
| 0.75                 | 12                  | 54.0               |
| 0.75                 | 15                  | 84.375             |
| 1.0                  | 10 (Design Target)  | 50.0               |
| 1.0                  | 12                  | 72.0               |
| 1.0                  | 15                  | 112.5              |

### Acceleration Time and Average Power 

Estimation based on existing belt length of 0.7m 

Estimation based on existing change of velocity of 10m/s

Apply formula **d = Δv * t / 2  **, **t = 0.14s**

Acceleration = **Δv / t** , **a =  71.4m/s^s**

- Distance = Δvelocity * time / 2
  - Time = 2 * distance / Δvelocity 
- Acceleration = Δvelocity / time
- Force = mass x acceleration  
- Kinetic Energy = force x distance
- Average Power = energy / time

Other potential acceleration values:

| Delta Velocity (m/s) | Accel Distance (m) | Time (s) | Acceleration (m/s^2) | Force (N)[^1] | Kinetic Energy (J) | Average Power (W) |
| -------------------- | ------------------ | -------- | -------------------- | ------------- | ------------------ | ----------------- |
| 10                   | 0.7                | 0.14     | 71.4                 | 53.55         | 37.5               | 268               |
| 10                   | 0.5                | 0.1      | 100                  | 75            | 37.5               | 375               |
| 10                   | 0.3                | 0.06     | 166.6                | 125           | 37.5               | 625               |
| 10                   | 0.2                | 0.04     | 250                  | 187           | 37.5               | 938               |

[^1]: Assume 0.75kg bullet

### Grip and Contact surface area

Assume

### Angular Velocity of drive wheel

Based on 10m/s 

https://planetcalc.com/556/

| Wheel Diameter (m)       | Exit Velocity (m/s)   | **Radians Per Second** | RPM  |
| ------------------------ | --------------------- | ---------------------- | ---- |
| 0.100 (Tentative Design) | 10 (Tentative Design) | 100                    | 956  |
| 0.120                    | 10 (Tentative Design) | 83.4                   | 796  |
| 0.140                    | 10 (Tentative Design) | 71.5                   | 683  |
| 0.100 (Tentative Design) | 15                    | 150.2                  | 1434 |
| 0.120                    | 15                    | 125.0                  | 1194 |
| 0.140                    | 15                    | 107.2                  | 1024 |





### 

### Weight and energy storage on flywheel



### 

## TMOTOR U8 II KV85

Purchased from [TaoBao](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.4bff2e8dVMO00u&id=554381733501&_u=fl5jjmh9e3f)

Official website: https://store.tmotor.com/goods.php?id=476



## X2212 Motor 

Purchased on TaoBao together with ODrive board

Motor Configuration and initialization file for ODrive: https://github.com/makerbase-mks/ODrive-MKS/blob/main/03_Makerbase%20ODrive%20related%20components/02_X2212%20Motor%20configuration/X2212%20Motor%20configuration.txt

Follow this tutorial to set up: https://www.youtube.com/watch?v=K4QkISL9Rqo&list=PLc2RScfrSFEDcQp6Qvc7mBNre8ABCoz9p&index=3

(line 41 to line 48 should be run line by line)

# Electronics / Controller 

## ODrive V3.6 Two Channel Board 

Purchased from [TaoBao](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.4bff2e8dVMO00u&id=639775367063&_u=fl5jjmhb818) (From MakerBase)

Makerbase [Odrive Tutorials on Youtube](https://www.youtube.com/playlist?list=PLc2RScfrSFEDcQp6Qvc7mBNre8ABCoz9p) [Tutorial on Blog](https://blog.csdn.net/gjy_skyblue/category_10813011.html)

Firmware version 0.5.1.1

Software Menu: https://docs.odriverobotics.com/v/0.5.5/getting-started.html

Software troubleshooting Doc : https://docs.odriverobotics.com/v/0.5.5/troubleshooting.html

### Error

```
dump_errors(odrv0)
odrv0.axis0.clear_errors()

odrv0.reboot()
```



### Live Plotter

https://docs.odriverobotics.com/v/0.5.5/odrivetool.html#liveplotter

```
// Start Live Plotter
odrivetool liveplotter

start_liveplotter(lambda:[odrv0.axis0.encoder.pos_estimate, odrv0.axis0.controller.pos_setpoint])

# If you want to plot different values, change them here.

# Plotting Velocity and Torque
cancellation_token = start_liveplotter(lambda: [
    (odrv0.axis0.encoder.vel_estimate), # turns/s
    (odrv0.axis0.motor.current_control.Iq_setpoint), # Current
])

# Stop Plotter
cancellation_token.set()
```

### Axis State / Calibration States

```
ODrive.Axis.AxisState

UNDEFINED = 0
IDLE= 1
STARTUP_SEQUENCE= 2 
FULL_CALIBRATION_SEQUENCE= 3
MOTOR_CALIBRATION= 4
ENCODER_INDEX_SEARCH= 6
ENCODER_OFFSET_CALIBRATION= 7
CLOSED_LOOP_CONTROL= 8  
- The action depends on the controller.config.control_mode.
- Can only be entered if the motor is calibrated
LOCKIN_SPIN= 9
ENCODER_DIR_FIND= 10
HOMING= 11
ENCODER_HALL_POLARITY_CALIBRATION= 12
ENCODER_HALL_PHASE_CALIBRATION= 13

odrv0.axis0.requested_state = AXIS_STATE_CLOSED_LOOP_CONTROL
```

### Close Loop Control Mode

```
// Position Control (Mode 3)
odrv0.axis0.controller.config.control_mode = CONTROL_MODE_POSITION_CONTROL
odrv0.axis0.requested_state = AXIS_STATE_CLOSED_LOOP_CONTROL
odrv0.axis0.controller.input_pos = 10

// Position Control with filtering
odrv0.axis0.controller.config.input_mode = INPUT_MODE_POS_FILTER
odrv0.save_configuration()

// Position control with Trapezoidial Motion Profile
odrv0.axis0.controller.config.input_mode = INPUT_MODE_TRAP_TRAJ
odrv0.save_configuration()


// Velocity Control (Mode 2) (need save and reboot)
odrv0.axis0.controller.config.control_mode = CONTROL_MODE_VELOCITY_CONTROL
odrv0.axis0.requested_state = AXIS_STATE_CLOSED_LOOP_CONTROL
odrv0.axis0.controller.input_vel = 10

odrv0.axis0.controller.config.vel_ramp_rate
```

#### ODrive.Controller.ControlMode

```
odrv0.axis0.controller.config.control_mode = 

VOLTAGE_CONTROL= 0
TORQUE_CONTROL= 1
VELOCITY_CONTROL= 2
POSITION_CONTROL= 3
```

#### ODrive.Controller.InputMode

```
odrv0.axis0.controller.config.input_mode = 

INACTIVE= 0
PASSTHROUGH= 1
VEL_RAMP= 2 
POS_FILTER= 3
TRAP_TRAJ= 5
TORQUE_RAMP= 6
```

#### 

### Config from X2212 Motor



```
odrv0.axis0.controller.config.control_mode = CONTROL_MODE_POSITION_CONTROL
odrv0.axis0.controller.config.vel_limit = 50
odrv0.axis0.controller.config.pos_gain = 30
odrv0.axis0.controller.config.vel_gain = 0.02
odrv0.axis0.controller.config.vel_integrator_gain = 0.2
odrv0.axis0.controller.config.input_mode = INPUT_MODE_TRAP_TRAJ
odrv0.axis0.trap_traj.config.vel_limit = 30
odrv0.axis0.trap_traj.config.accel_limit = 5
odrv0.axis0.trap_traj.config.decel_limit = 5
odrv0.save_configuration()
```

Some tuning result using position control according to https://docs.odriverobotics.com/v/0.5.5/control.html#control-tuning

```

odrv0.axis0.controller.config.vel_limit = 50
odrv0.axis0.controller.config.pos_gain = 100
odrv0.axis0.controller.config.vel_gain = 0.004
odrv0.axis0.controller.config.vel_integrator_gain = 0.01

```



## TMotor Flame 60A 12S ESC

[TaoBao](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.4bff2e8dc9Kd8n&id=596745619360&_u=fl5jjmh1e7f)



