.. index:: Updates

Updates
=======

Since the Security Center does not contains an
"Update" menu in your Web UI, you need to update
the verions via the command line.

To do this, connect to your Security Center Frontend
and Backend via SSH. If you are running the Frontend
and Backend on the same server, you only need to perform
the next step once.

We run the following command to update the minor version
of your Security Center:

.. code-block:: console

    nextron@asgard-sc:~$ sudo apt update
    nextron@asgard-sc:~$ sudo apt dist-upgrade

After the updates have been installed, you can check
if the services are up and running again. Make sure
the status is in the ``active (running)`` state:

Frontend:

.. code-block:: console
    :emphasize-lines: 4

    nextron@asgard-sc:~$ sudo systemctl status asgard-security-center-frontend.service 
    ● asgard-security-center-frontend.service - ASGARD Security Center Frontend
         Loaded: loaded (/lib/systemd/system/asgard-security-center-frontend.service; enabled; preset: enabled)
         Active: active (running) since Thu 2023-11-16 12:42:47 CET; 38s ago
    [...]

Backend:

.. code-block:: console
    :emphasize-lines: 4

    nextron@asgard-sc:~$ sudo systemctl status asgard-security-center-backend.service 
    ● asgard-security-center-backend.service - ASGARD Security Center Backend
         Loaded: loaded (/lib/systemd/system/asgard-security-center-backend.service; enabled; preset: enabled)
         Active: active (running) since Thu 2023-11-16 12:42:47 CET; 31s ago                                                                                                                      
    [...]