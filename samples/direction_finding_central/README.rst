.. _samples-bluetooth_direction_finding_central:

bluetooth_direction_finding_central
###################################

Connect to a Bluetooth LE Direction Finding peripheral and request Constant Tone Extension.

Overview
********

A simple application demonstrating the Bluetooth LE Direction Finding CTE reception in
connected mode by requesting transmission of a packet containing Constant
Tone Extension by connected peer device.

Requirements
************

* Nordic nRF SoC based board with Direction Finding support (example boards:
  `nrf52833dk <https://docs.zephyrproject.org/latest/boards/nordic/nrf52833dk/doc/index.html#nrf52833dk>`__,
  `nrf5340dk <https://docs.zephyrproject.org/latest/boards/nordic/nrf5340dk/doc/index.html#nrf5340dk>`__)
* Antenna matrix for AoA (optional)

Check your SoC's product specification for Direction Finding support if you are
unsure.

Building and Running
********************

By default the application supports Angle of Arrival and Angle of Departure mode.

To use Angle of Departure mode only, build this application as follows,
changing ``nrf52833dk/nrf52833`` as needed for your board::

  west build -b nrf52833dk/nrf52833 samples/bluetooth/direction_finding_central -- -DEXTRA_CONF_FILE=overlay-aod.conf
  west flash

To run the application on nRF5340DK, a Bluetooth controller application must
also run on the network core. The :ref:`samples-bluetooth_hci_ipc` sample
application may be used. To build this sample with direction finding support
enabled:

* Copy
  :file:`samples/bluetooth/direction_finding_central/boards/nrf52833dk_nrf52833.overlay`
  to a new file,
  :file:`samples/bluetooth/hci_ipc/boards/nrf5340dk_nrf5340_cpunet.overlay`.
* Make sure the same GPIO pins are assigned to Direction Finding Extension in file
  :file:`samples/bluetooth/direction_finding_central/boards/nrf5340dk_nrf5340_cpuapp.overlay`.
  as those in the created file  :file:`samples/bluetooth/hci_ipc/boards/nrf5340dk_nrf5340_cpunet.overlay`.
* Copy
  :file:`samples/bluetooth/direction_finding_central/boards/nrf52833dk_nrf52833.conf`
  to a new file,
  :file:`samples/bluetooth/hci_ipc/boards/nrf5340dk_nrf5340_cpunet.conf`.

Antenna matrix configuration
****************************

To use this sample with Angle of Arrival enabled on Nordic SoCs, additional
configuration must be provided via `devicetree <https://docs.zephyrproject.org/latest/build/dts/index.html>`__ to enable
control of the antenna array.

An example devicetree overlay is in
:file:`samples/bluetooth/direction_finding_central/boards/nrf52833dk_nrf52833.overlay`.
You can customize this overlay when building for the same board, or create your
own board-specific overlay in the same directory for a different board. See
`nordic,nrf-radio <https://docs.zephyrproject.org/latest/build/dts/api/bindings/net/wireless/nordic%2Cnrf-radio.html#std-dtcompatible-nordic-nrf-radio>`__
for documentation on the properties used in
this overlay. See `Set devicetree overlays <https://docs.zephyrproject.org/latest/build/dts/howtos.html#set-devicetree-overlays>`__ for information on setting up
and using overlays.

Note that antenna matrix configuration for the nRF5340 SoC is part of the
network core application. When :ref:`samples-bluetooth_hci_ipc` is used as the
network core application, the antenna matrix configuration should be stored in
the file
:file:`samples/bluetooth/hci_ipc/boards/nrf5340dk_nrf5340_cpunet.overlay`
instead.
