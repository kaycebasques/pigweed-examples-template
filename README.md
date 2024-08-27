# Pigweed: minimal Bazel example

This repository contains a minimal example of a Bazel-based Pigweed project.
It is a LED-blinking service (featuring RPC control!) for the
[Raspberry Pi Pico](https://www.raspberrypi.com/products/raspberry-pi-pico/).
It can also be run on any computer using the included simulator.

## Getting the code

```
git clone https://pigweed.googlesource.com/pigweed/quickstart/bazel pw_bazel_quickstart
cd pw_bazel_quickstart
```

## Dependencies

The only dependency that must be installed is Bazelisk.

Bazelisk is a launcher for the Bazel build system that allows for easy
management of multiple Bazel versions.

[Instructions for installing Bazelisk can be found here.](https://github.com/bazelbuild/bazelisk/blob/master/README.md)

## Running on the simulator

To run the simulator, type:
`bazelisk run //apps/blinky:simulator_blinky`
Then, in a new console, connect to the simulator using:
`bazelisk run //apps/blinky:simulator_console`

## Running on hardware

To start, connect a Raspberry Pi Pico, Pico 2, or debug probe via USB.

To run on the Raspberry Pi Pico, type:
`bazelisk run //apps/blinky:flash_rp2040`
Then, in a new console, connect to the device using:
`bazelisk run //apps/blinky:rp2040_console`

## Controlling the LED

Once connected with a console, RPCs can be sent to control the LED.
Try running:

```
device.set_led(True)
device.set_led(False)
device.toggle_led()
device.blink(blink_count=3)
```

## Running unit tests on the host device

`bazelisk test //...` will run the unit tests defined in this project,
such as the ones in `modules/blinky/blinky_test.cc`.

## Running unit tests on hardware

`bazelisk run @pigweed//targets/rp2040/py:unit_test_server` in one console followed by
`bazelisk test //... --config=rp2040` will also allow running the unit tests on-device.

## Next steps

Try poking around the codebase for inspiration about how Pigweed projects can be
organized. Most of the relevant code in this quickstart (including RPC
definitions) is inside `modules/blinky`, with some client-side Python code in
`tools/console.py`.
