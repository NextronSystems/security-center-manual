Password Reset
==============

Since the password for the admin user is stored only on the Backend,
you have to reset the password via console. To reset the password for
the ``admin`` user on the **Security Center Backend**, run the following
command via console:

.. code-block:: console

    nextron@sc-back:~$ sudo asgard-security-center-backend set-password
    {"LEVEL":"Info","MESSAGE":"LDAP disabled","MODULE":"LDAP","TIME":"2024-04-10T08:17:42Z"}
    Please enter password for user `admin`: 
    Please re-enter password for user `admin`: 
    Apr 10 08:17:49 sc-back THOR_UTIL: Info: SET_PASSWORD: password successfully updated