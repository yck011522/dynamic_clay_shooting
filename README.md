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



## X2212 Motor 

Purchased on TaoBao together with ODrive board

Motor Configuration and initialization file for ODrive: https://github.com/makerbase-mks/ODrive-MKS/blob/main/03_Makerbase%20ODrive%20related%20components/02_X2212%20Motor%20configuration/X2212%20Motor%20configuration.txt

Follow this tutorial to set up: https://www.youtube.com/watch?v=K4QkISL9Rqo&list=PLc2RScfrSFEDcQp6Qvc7mBNre8ABCoz9p&index=3

(line 41 to line 48 should be run line by line)

# Electronics / Controller 

## ODrive V3.6 Two Channel Board 

Purchased from [TaoBao](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.4bff2e8dVMO00u&id=639775367063&_u=fl5jjmhb818) (From MakerBase)

Makerbase [Odrive Tutorials on Youtube](https://www.youtube.com/playlist?list=PLc2RScfrSFEDcQp6Qvc7mBNre8ABCoz9p)

Firmware version 0.5.1.1

Software Menu: https://docs.odriverobotics.com/v/0.5.5/getting-started.html
