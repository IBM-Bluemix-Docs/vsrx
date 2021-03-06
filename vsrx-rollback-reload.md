---

copyright:
  years: 2019
lastupdated: "2020-09-16"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Rollback options
{: #rollback-options}

In the standalone environment a rollback is not supported.

In the high availability environment that is upgrading from vSRX version, a rollback is supported only after the first node has been OS Reloaded and before the second node has been OS Reloaded. The Gateway will be in an “Upgrade Active” state at this point. The following steps should be followed to rollback the first node to the previous version.

Please be aware, that a traffic disruption will occur while waiting for the secondary node to power on and for the traffic to failover to this node.
{: important}

1. Power off the vSRX on the node being rolled-back (primary node) using the command `virsh shutdown <domain>`.

  Wait for the node to be fully powered off before proceeding.

2. Power up the vSRX on the node that has not been rolled-back using the command `virsh start <domain>`. This will return the primary node back to the original vSRX version. 

  Before restoring the original vSRX image, rename the vSRX qcow2 file in `/var/lib/libvirt/images/vSRXvM2/vSRX_Image.qcow2.backup` to `/var/lib/libvirt/images/vSRXvM2/vSRX_Image.qcow2` so that `virsh` detects the original image.
  {: tip}

4.	Run the [OS reload readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness), if necessary, and resolve any issues.

5.	Perform an OS reload on the host you want to rollback to return it to the original vSRX version. 

The cluster will now be running with its original configuration.
