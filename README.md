# Crazyflie Firmware (Custom Out-of-Tree Controller Fork)

Custom fork of the Bitcraze Crazyflie firmware implementing an Out-of-Tree controller for closed-loop flight with OptiTrack motion capture feedback.

## Context

This repository is the onboard firmware component of the [crazyflie-optitrack](https://github.com/covenant-tec/crazyflie-optitrack) workspace. The companion ROS 2 packages in that repository handle OptiTrack communication, state logging, and parameter injection.

## Application Location

The custom controller source code, parameters, and build configuration are located in:

`examples/app_out_of_tree_controller/`

All compilation and flashing commands must be executed from within that directory.

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
