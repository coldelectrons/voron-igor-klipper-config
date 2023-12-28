# voron-igor-klipper-config

## Notes
### Huvud v0.62 with katapult (canboot)
Because `katapult` is larger than the original HID bootloader, the boot offsets are going to be different.
The `katapult.bin` ends up being 4.3k, so build **both** `katapult` and `klipper` firmwares to use "8k" bootloader offsets.
Yes, I know the `katapult` README has confusing language about "application start address", but it's the same thing.
It's helpful to build `klipper` to set `!PC13` (led) pin on statup, to give an indicator that the firmware did start.
The bootloader can be configured to use the same led pin, which does a slow blink when the bootloader is running.
Once the led goes solidly on, that indicates the `klipper` firmware started.
(I wish `klipper` had a heartbeat led effect, or at least a flicker for CAN activity.)

The only time you should need to configure `katapult` to use the old 2k (HID) bootloader offset is if you are using
the deployer app firmware, upload via that same HID bootloader, so that 2k offset applies only to the deployer app.

After getting `katapult` loaded, should you need to upgrade it, you can just upload `deployer.bin` with an 8k offset.
This lets you upgrade the bootloader over CAN.
