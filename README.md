# Crazyflie Custom Firmware

Crazyflie 2.X firmware with a custom Out-of-Tree controller for flight with OptiTrack.
This repository is used together with the [crazyflie-optitrack](https://github.com/covenant-tec/crazyflie-optitrack) workspace, which provides the ROS 2 packages to connect to the drone and stream OptiTrack data.
The controller code and build files are located in `examples/app_out_of_tree_controller/`.

## Parameters

Controller gains and physical constants are registered under the `ootParams` parameter group:

* `trans_kp_x`, `trans_kp_y`, `trans_kp_z`: Translational proportional gains.
* `trans_kd_x`, `trans_kd_y`, `trans_kd_z`: Translational derivative gains.
* `trans_ki_x`, `trans_ki_y`, `trans_ki_z`: Translational integral gains.
* `trans_emax`, `trans_mu`, `trans_gamma`: Translational homogeneous nonlinear terms.
* `rot_kp_x`, `rot_kp_y`, `rot_kp_z`: Rotational proportional gains.
* `rot_kd_x`, `rot_kd_y`, `rot_kd_z`: Rotational derivative gains.
* `rot_ki_x`, `rot_ki_y`, `rot_ki_z`: Rotational integral gains.
* `rot_emax`, `rot_mu`, `rot_gamma`: Rotational homogeneous nonlinear terms.
* `mass`: Physical vehicle mass in kilograms, defaulting to 0.029 kg when unconfigured.
* `thrust_max`, `thrust_min`: Dynamic saturation limits for collective thrust (defaults to 1.5 and 0.0).
* `torque_max`: Dynamic saturation limit for attitude control torque (defaults to 0.5).

> **Note:** The internal default values in the firmware are tuned for a single marker configuration. If the ROS 2 bridge fails to push parameter overrides from the `.conf` files, the drone will safely fall back to these single-marker bounds.

## Build & Flash

Navigate to the application directory:

```bash
cd examples/app_out_of_tree_controller
```

Compile the application binary:

```bash
make clean && make
```

Flash the compiled binary over radio by specifying the address of your drone in the `RADIO` parameter:

```bash
make cload RADIO=<your-crazyflie-uri>
```

Example:

```bash
make cload RADIO=radio://0/80/2M/E7E7E7E7E7
```

## Credits

The custom Out-of-Tree controller architecture, homogeneous nonlinear control formulation, and Crazyflie firmware integration were designed and implemented by [Kevin Martinez](https://github.com/Fairbrook) as part of doctoral research.
