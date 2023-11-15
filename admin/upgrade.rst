.. index:: Upgrade your old Security Center

Upgrade your Security Center from v1 to v2
==========================================

In this chapter we will explain how to upgrade your
Security Center v1 to the newest version. Since we
mainly focus on the new Version 2 of the Security
Center in this document, we want to help you through
the upgrade process from your older Version 1 of
Security Center the newest one, so you can make use
of the newest features.

If you are running your Security Center Frontend and
Backend on two separate servers, you will have to
do the steps below for both servers. You can
upgrade them at the same time to reduce downtime.

New Update Servers
~~~~~~~~~~~~~~~~~~

We are using a new update server for the new versions
of the Security Center. Please make sure the following
server is reachable by both your Frontend and Backend
server:

.. list-table:: 
   :header-rows: 1
   :widths: 20, 15, 25, 40

   * - Description
     - Port
     - Source
     - Destination
   * - Product Updates
     - 443/tcp
     - Security Center Frontend & Backend
     - update-301.nextron-systems.com

Please make sure your local firewall allows the connection
to the new update server, otherwise the upgrade will not
work.

Preparing for the Upgrade
~~~~~~~~~~~~~~~~~~~~~~~~~

To prepare for the upgrade, make sure that you have
an up to date backup of both your Security Center backend
(sometimes referred to as "model") and the frontend.
We advise to take a snapshot of the VMs with your
hypervisor.

After you created a backup/snapshot, we need to update
both frontend and backend servers to the newest version.
If you have the frontend and backend installed on the same
system, you need to run the next commands only once. If you
have two separate servers, repeat the next steps for each
of them.

Connect to your Security Center v1 via SSH. Update your
current Security Center v1 to the newest version:

.. code-block:: console

    nextron@seccenter:~$ sudo apt update && sudo apt dist-upgrade
    [...]
    Do you want to continue? [Y/n] y

Please confirm the linux upgrade by pressing **y** and **enter**.
This will not upgrade your Security Center, only the underlying
linux operating system.

.. hint::
   This process might take a while.

Performing the Upgrade
~~~~~~~~~~~~~~~~~~~~~~

After we prepared the system(s) for the update, we can run
the following command to install the version 2 of the Security
Center. Please note that this step can not be reversed, and your
Security Center will be running with the newest version after
the update has finished.

.. code-block:: console

    nextron@seccenter:~$ start-asgard-update 
    Created symlink /etc/systemd/system/multi-user.target.wants/asgard-updater.service → /lib/systemd/system/asgard-updater.service.
    Successfully started the ASGARD update process.
    To monitor the update progress and view log files, you can use the following command:
    sudo tail -f /var/log/asgard-updater/update.log

.. warning:: 
    Your server will restart multiple times during the upgrade process.
    Do not restart the server manually. You can log into the
    server and run the following command to monitor the progress:

    .. code-block:: console

        nextron@seccenter:~$ sudo tail -f /var/log/asgard-updater/update.log

Once your update is finished, you should find the following
message in the update log:

.. code-block:: console

    nextron@seccenter:~$ sudo tail /var/log/asgard-updater/update.log
    [...]
    2023-10-31T08:57:14.834079+01:00 security-center asgard-updater[731]: Upgrade finished. Deactivating service...
    2023-10-31T08:57:14.843136+01:00 security-center asgard-updater[731]: Removed "/etc/systemd/system/multi-user.target.wants/asgard-updater.service".

You can now connect to your Security Center's Web UI as usual.