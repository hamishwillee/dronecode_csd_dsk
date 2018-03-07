# Deploying on a Companion Computer

Typically the CSD is build on a Ubuntu development computer and then deployed to/run on a drone-based companion computer (a companion computer is typically resource constrained, and the the development toolchain is relatively heavy-weight).

This topic explains how you can set up your companion computer with the CSD dependencies and deploy CSD.

THIS IS WORK IN PROGRESS

The *csd* binary and *csd.system* files are generated in the root of the CSD source tree.

## CSD Binary Dependencies

<!-- What are they -->
<!-- How are they deployed? Is it a question of creating an "image"? -->

## Enabling Systemd

<!-- Should we cover this, or just state that it needs to be done -->
<!-- is the position of the csd.system "standard" - if not, should explain how set up -->
<!--
1.Place the csd.service file in /lib/system/system directory
1.Reload systemd daemon
  ```
  systemctl daemon-reload
  ```

1. Enable the service to start the service automatically on subsequent boot
   ```
   systemctl enable csd.service
   ```

1.Start the service for the current session (not required if rebooted after enable command)
   ```
   systemctl start csd.service
   ```
-->

## Deploy CSD to Companion Computer

To deploy CSD to Companion:

1. Copy the *csd* binary using *scp*:
   ```
   scp csd uname@ip-addr:/usr/bin/
   ```
   where:
   * `ip-addr` is IP address of Aero on the network (check using *ifconfig*)
   * `uname` is `root` (Yocto) or `<user-defined>` (Ubuntu)

1. Reboot Computer (to restart CSD on boot)

> **Note** The [CSD Configuration File](../guide/configuration_file.md) (**_yourplatform_.conf**) and [autostart file](../guide/autostart.md) (*csd.service*) typically do not change or need to be updated. If required, you could do so using the following commands:
  ```
  scp samples/files/yourplatform.conf uname@ip-addr:/etc/csd/main.conf
  scp csd.system uname@ip-addr:/lib/system/system/csd.system
  ```


## Verify Installation

1. Make sure CSD is running:
   ```sh
   systemctl status csd
   ```
1. Run the [Sanity Tests](../test/sanity_tests.md) to verify that CSD is working correctly.