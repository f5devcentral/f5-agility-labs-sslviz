Appendix 3 - Configuring SSLO for High Availability
===================================================

SSL Orchestrator HA presents a different model for HA sync/failover than normal
BIG-IP HA. Specifically, SSLO relies on a separate REST-based process to
perform internal sync between the peers and does not rely on BIG-IP mcpd. It is
therefore important to understand the conditions and caveats of this separate
process.

- An SSL Orchestrator system must be configured for **MANUAL with INCREMENTAL
  SYNC**. The REST operations take care of synchronizing the SSLO
  configurations. This will also, at times, trigger a warning on the BIG-IP
  that the boxes are out of sync, though they are not. It is acceptable to
  ignore these warnings, though it is also possible to manually sync the boxes
  **AFTER** the SSLO sync process.

- HA must be configured and stable **BEFORE** deploying SSLO. Any SSLO upgrade
  process must first break HA before continuing. Therefore, to upgrade an SSLO
  system, break HA, upgrade the systems independently, re-establish HA, then
  re-configure/re-deploy SSLO. When upgrading the BIG-IP itself, break HA,
  upgrade the systems independently, and then re-establish HA. The BIG-IP ISO
  comes with a base version of SSLO that may not be the one needed. **BEFORE**
  accessing the SSLO menu, remove and replace the SSLO RPM package to prevent
  the base package from deploying itself.

.. note:: the extra BIG-IP in this lab environment is perfectly suited to
   demonstrate SSLO HA. Simply configure identical networking, floating
   self-IPs, resource provisioning, and set up as an HA peer. Use the ICAP/DLP
   or TAP service VLAN for the sync channel (whichever won’t be needed).

To deploy SSLO in a High Availability pair, perform the following operations.

- Confirm that you have administrative access to the BIG-IP UI and to the shell
  (SSH).

- Perform the typical BIG-IP HA setup process and confirm that the boxes are in
  a good HA state.

  - Confirm HA state by reviewing logs (restnoded, restjavad, and tmm) for any
    errors relating to HA/sync.
  - Navigate to https://<management-ip>/mgmt/shared/gossip on both HA devices.
    Verify that the “status” value indicated “ACTIVE”.
  - Navigate to https://<management-ip>/mgmt/tm/cm/device on both HA devices.
    Verify that the item count returned is the same on both. Verify that the
    “configsyncip” attribute exists and matches the HA VLAN IP on each
    corresponding device. And also verify that the “unicastAddress” exists, and
    that “configsyncip” is contained in this value. Usually the management IP
    should also be an antryu of “unicastAddress”.
  - Navigate to https://management-ip/mgmt/shared/resolver/device-groups/tm-shared-all-bigips/
    devices on both HA devices. Verify that the returned information is the
    same on both boxes. Specifically, validate the “address” attribute exists
    and matches the corresponding “configsyncip”. 
  - Check port lockdown settings on both HA devices and verify that the
    designated sync and failover VLANs use either “Allow All” or
    “Allow Default” in their Self-IP configurations.
  - Navigate to https://management-ip/mgmt/tm/shared/bigip-failover-state on
    both HA devices. Verify that the “failoverState” value is “active” for the
    active device, and “standby” for the standby device.
  - Check HA sync failover group settings (Device Management – Device Groups).
    Verify that a device group exists, that the device group type is
    “Sync-Failover”, that all HA devices are in the “includes” field, and that
    sync type is “Manual with Incremental Sync”.
  - Verify that the BIG-IP .iso and SSLO .rpm are the same on both devices.
  - Verify that NTP and DNS settings match on both HA devices.
  - Verify that overview status (Device Management – Overview Status) shows no
    warnings or errors.

- If upgrading the BIG-IP:

  - Perform a manual config sync and take UCS backups on both boxes.
  - Disable HA by removing both devices from the device group (from the standby
    box).
  - Follow normal procedures to install a new BIG-IP ISO on both boxes.

- Navigate to the iApps Package Management menu and verify that the correct
  .rpm package is installed or replace if not.
- Re-enable HA (if previously disabled for upgrade) by adding both devices back
  to the device group.
- Initiate a config sync.
- Deploy SSL Orchestrator. The SSLO peers will sync their configs via REST
  calls between them. This may at times present a warning in the UI that the
  boxes are out of sync, though they are not. Review both devices to verify
  like settings. It is also acceptable to perform a manual sync AFTER the SSLO
  sync process.
- If any errors are encountered in the steps above, restore from the UCS
  backup.
