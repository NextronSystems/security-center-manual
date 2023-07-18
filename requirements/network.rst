.. index:: Network Requirements

Network Requirements
--------------------

The ASGARD components use the ports in the following chapters.
For a detailed and up to date list of our update and licensing
servers, please visit https://www.nextron-systems.com/hosts/.

Management Workstation
^^^^^^^^^^^^^^^^^^^^^^

.. list-table:: 
   :header-rows: 1
   :widths: 30 20 20 30

   * - Description
     - Port
     - Source
     - Destination
   * - CLI administration
     - 22/tcp
     - Workstation
     - Security Center Frontend
   * - CLI administration
     - 22/tcp
     - Workstation
     - Security Center Backend
   * - Web administration
     - 8443/tcp
     - Workstation
     - Security Center Backend

Customer Access
^^^^^^^^^^^^^^^

.. list-table:: 
   :header-rows: 1
   :widths: 30 20 20 30

   * - Description
     - Port
     - Source
     - Destination
   * - Customer Web Interface
     - 443/tcp
     - Workstation
     - Security Center Frontend

Analysis Cockpit
^^^^^^^^^^^^^^^^

.. list-table:: 
   :header-rows: 1
   :widths: 30, 20, 25, 25

   * - Description
     - Port
     - Source
     - Destination
   * - Event and Asset synchronization
     - 6443/tcp
     - ASGARD Analysis Cockpit
     - Security Center Backend

Security Center Frontend
^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table:: 
   :header-rows: 1
   :widths: 30, 20, 25, 25

   * - Description
     - Port
     - Source
     - Destination
   * - Event and Asset queries
     - 7443/tcp
     - Security Center Frontend
     - Security Center Backend

Internet
^^^^^^^^

The Security Center is configured to retrieve updates from the following URLs:

.. list-table:: 
   :header-rows: 1
   :widths: 25, 15, 25, 35

   * - Description
     - Port
     - Source
     - Destination
   * - Product and system updates
     - 443/tcp
     - Gatekeeper, Lobby, Broker
     - update3.nextron-systems.com
   * - NTP
     - 123/udp
     - Gatekeeper, Lobby, Broker
     - 0.debian.pool.ntp.org [1]_
   * - NTP
     - 123/udp
     - Gatekeeper, Lobby, Broker
     - 1.debian.pool.ntp.org [1]_
   * - NTP
     - 123/udp
     - Gatekeeper, Lobby, Broker
     - 2.debian.pool.ntp.org [1]_

.. [1]
  The NTP server configuration can be changed.

All proxy systems should be configured to allow access to these URLs without
TLS/SSL interception (ASGARD uses client-side SSL certificates for authentication).
It is possible to configure a proxy server, username and password during the setup
process of the Security Center. Only BASIC authentication is supported (no NTLM
authentication support).

.. hint:: 
   The Security Center installer requires Internet access during the setup. The
   installation process will fail if required packages cannot be loaded from our update
   servers (see table above).

DNS
^^^

All the components need to have a resolvable FQDN.

The Security Center needs to be able to resolve internal and external IP addresses.
Connection to the Analysis Cockpit MUST be done with a resolvable FQDN. IP addresses will not work.