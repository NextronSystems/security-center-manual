ASC#001: Backend is down after Upgrade to v2
============================================

.. list-table::
    :header-rows: 1
    :widths: 50, 50
    
    * - Introduced Version
      - Fixed Version
    * - 2.x
      - N/A

There is currently a rare issue where the backend is not starting
after upgrading to v2. This is due to insufficient permissions for
the MySQL Trigger.

If you upgraded your Security Center to version 2 and everything
seems to be working fine, you can ignore this advisory.

We are currently working on a more robust upgrade process to prevent
this from happening in the future.

ASC#001: Workaround
-------------------

After a successful upgrade to version 2 ("Upgrade finished" message can be
seen, see :ref:`admin/upgrade:performing the upgrade`), you might encounter
the following error message in ``/var/log/asgard-security-center-backend/server.log``:

.. code-block:: json

  {
    "level": "FATAL",
    "time": "2024-04-03T18:49:16+02:00",
    "message": "failed to init database schema",
    "error": "Error 1142 (42000): TRIGGER command denied to user 'securitycenter-model'@'localhost' for table `asgard-security-center-backend`.`assets`"
  }

To fix this problem, run the following commands on your backend.

Drop the MySQL trigger (no data will be lost):

.. code-block:: console

  nextron@backend:~$ sudo mysql asgard-security-center-backend -e "DROP TRIGGER IF EXISTS assets_updated_fields;"

Restart the backend service. This will recreate the trigger with the correct permissions
automatically:

.. code-block:: console

  nextron@backend:~$ sudo systemctl restart asgard-security-center-backend.service

Check if the service is running:

.. code-block:: console

  nextron@backend:~$ sudo systemctl status asgard-security-center-backend.service