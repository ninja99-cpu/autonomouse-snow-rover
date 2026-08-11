# Build Log

## Chassis and Mechanical

- Built on the RC Snowcat open-source design by RCTestFlight
- All structural parts printed in PLA
- Tracks assembled using music wire cut into 100mm segments (~35 per track, 8 lengths of 36" wire total)
- Bearings and axles installed; 8mm hardened steel rods used as main chassis rails
- 5010 360KV motors mounted to drive gearboxes and impeller

## Electronics and Wiring

- Omnibus F4 chosen for ArduPilot Rover compatibility
- PDB installed; regulated 5V line powers the FC
- ESC BEC red wires left disconnected to avoid voltage conflict with PDB
- FlySky receiver wired via IBUS (single signal wire to FC UART)
- BE-220 GPS wired to FC UART

## Firmware and Configuration

- Started with QGroundControl on macOS — ran into limited ArduPilot support and difficulty with motor testing
- Switched to Mission Planner on Windows, which has full ArduPilot support
- Vehicle type set to Rover, drive type set to Skid Steering
- Output functions assigned: SERVO1 = Left Motor, SERVO2 = Right Motor, SERVO3 = Impeller

## Challenges

**ESC beeping on startup**
ESCs beeped continuously on power-up. Power and signal were both present. After investigating output assignments, PWM ranges, and arming settings, the issue came down to incorrect SERVO_FUNCTION parameters and ESC calibration not being completed. Corrected in Mission Planner and resolved after working through calibration.

**Motors not spinning during testing**
Motors would not respond during early motor tests. Investigated arming restrictions, output assignments, and PWM configuration across both QGroundControl and Mission Planner before finding the correct combination of settings that allowed manual motor testing.

**ESC bidirectional mode**
The drive ESCs did not arrive pre-configured for bidirectional operation. It took a while to figure out that BLHeli ESCs need to be reprogrammed for bidirectional mode using BLHeliSuite before they would reverse direction for skid steering.

**GPS and heading**
The BE-220 GPS module was wired and configured but autonomous navigation has not yet been field tested. GPS alone provides position but not heading — a compass or magnetometer would be needed for reliable waypoint navigation. In a future revision a different GPS module would be used, ideally one with a built-in compass.

## Next Steps

- [ ] Field test GPS autonomous navigation
- [ ] Add compass / magnetometer
- [ ] Test impeller in real snow conditions
- [ ] Add camera system for remote monitoring
- [ ] Explore obstacle avoidance (ultrasonic or LiDAR)
