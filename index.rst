.. title:: Nutanix AOS, AHV Bootcamp and Prism Central Bootcamp

.. toctree::
  :maxdepth: 2
  :caption: Nutanix Configuration
  :name: _nutanix_configuration
  :hidden:

  lab_nutanix_tech_overview/lab_nutanix_tech_overview
  lab_storage_configuration/lab_storage_configuration
  lab_network_configuration/lab_network_configuration

.. toctree::
  :maxdepth: 2
  :caption: Deploying and Managing Workloads
  :name: _deploying_and_managing_workloads
  :hidden:

  lab_deploy_workloads/lab_deploy_workloads
  lab_manage_workloads/lab_manage_workloads
  lab_data_protection/lab_data_protection
  prismops/prismops_capacity_lab/prismops_capacity_lab
  prismops/prismops_rightsize_lab/prismops_rightsize_lab

.. This will all be hidden from the TOC Removing this line and removing the indent before ".. toctree" will bring this item back
  .. toctree::
  :maxdepth: 2
  :caption: Optional Labs
  :name: _optional_labs
  :hidden:

  image_create/image_create
  lab_image_configuration/lab_image_configuration


.. toctree::
  :maxdepth: 2
  :caption: Appendix
  :name: _appendix
  :hidden:

  tools_vms/windows_tools_vm
  tools_vms/linux_tools_vm
  appendix/glossary

.. _getting_started:

---------------
Getting Started
---------------

Welcome to the Nutanix AOS and AHV Bootcamp! This workbook accompanies an instructor-led session that introduces Nutanix Core technologies and many common management tasks.

You will explore Prism Element and become familiar with its features and navigation. You will use Prism to perform basic cluster administration tasks, including storage and networking. You will also walk through basic VM deployment and management tasks with Prism and AHV. Finally, you will explore VM data protection, including snapshots and replication. The instructor explains the exercises and answers any additional questions that you may have.

At the end of the bootcamp, attendees should understand the Core concepts and technologies that make up the Nutanix Enterprise Cloud stack and should be well prepared for a hosted or onsite proof-of-concept (POC) engagement.

What's New
++++++++++

- Workshop updated for the following software versions:
    - AOS 5.16.x & PC 5.17.x

Agenda
++++++

- Introductions
- Nutanix Presentation
- Nutanix Configuration Labs
- Deploying and Managing Workloads Labs

Introductions
+++++++++++++

- Name
- Familiarity with Nutanix

Initial Setup
+++++++++++++

- Take note of the *Passwords* being used.
- Log into your virtual desktops (connection info below)

Environment Details
+++++++++++++++++++

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises.

Networking
..........

POC clusters follow a standard naming convention:

- **Data Center** - *X*
- **Cluster Name** - POC\ *Y*
- **Subnet** - 10.\ *X*\.\ *Y*\ .0
- **Cluster IP** - 10.\ *X*\.\ *Y*\ .37

For example:

- **Data Center** - Phoenix
- **Cluster Name** - POC055
- **Subnet** - 10.42.55.0
- **Cluster IP** - 10.42.55.37

Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:

.. list-table::
   :widths: 25 75
   :header-rows: 1

   * - IP Address
     - Description
   * - 10.\ *X*\ .\ *Y*\ .37
     - Nutanix Cluster Virtual IP
   * - 10.\ *X*\ .\ *Y*\ .39
     - **PC** VM IP, Prism Central
   * - 10.\ *X*\ .\ *Y*\ .40
     - **DC** VM IP, NTNXLAB.local Domain Controller

Each cluster is configured with 2 VLANs which can be used for VMs:

.. list-table::
  :widths: 25 25 10 40
  :header-rows: 1

  * - Network Name
    - Address
    - VLAN
    - DHCP Scope
  * - Primary
    - 10.\ *X*\ .\ *Y*\ .1/25
    - 0
    - 10.\ *X*\ .\ *Y*\ .50-10.\ *X*\ .\ *Y*\ .124
  * - Secondary
    - 10.\ *X*\ .\ *Y*\ .129/25
    - *Y1* or *Y3*
    - 10.\ *X*\ .\ *Y*\ .132-10.\ *X*\ .\ *Y*\ .253

Credentials
...........

.. note::

  The *<Cluster Password>* is unique to each cluster and will be provided by the leader of the Workshop.

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Credential
     - Username
     - Password
   * - Prism Element
     - admin
     - *<Cluster Password>*
   * - Prism Central
     - admin
     - *<Cluster Password>*
   * - Controller VM
     - nutanix
     - *<Cluster Password>*
   * - Prism Central VM
     - nutanix
     - *<Cluster Password>*

Each cluster has a dedicated domain controller VM, **DC**, responsible for providing AD services for the **NTNXLAB.local** domain. The domain is populated with the following Users and Groups:

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Group
     - Username(s)
     - Password
   * - Administrators
     - Administrator
     - nutanix/4u
   * - SSP Admins
     - adminuser01-adminuser25
     - nutanix/4u
   * - SSP Developers
     - devuser01-devuser25
     - nutanix/4u
   * - SSP Consumers
     - consumer01-consumer25
     - nutanix/4u
   * - SSP Operators
     - operator01-operator25
     - nutanix/4u
   * - SSP Custom
     - custom01-custom25
     - nutanix/4u
   * - Bootcamp Users
     - user01-user25
     - nutanix/4u

Access Instructions
+++++++++++++++++++

The Nutanix Hosted POC environment can be accessed a number of different ways:

Lab Access User Credentials
...........................

PHX Based Clusters:
**Username:** PHX-POCxxx-User01 (up to PHX-POCxxx-User20), **Password:** *<Provided by Instructor>*

RTP Based Clusters:
**Username:** RTP-POCxxx-User01 (up to RTP-POCxxx-User20), **Password:** *<Provided by Instructor>*

Frame VDI
.........

Login to: https://frame.nutanix.com/x/labs

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Parallels VDI
.................

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Employee Pulse Secure VPN
..........................

Download the client:

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Install the client.

In Pulse Secure Client, **Add** a connection:

For PHX:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - PHX
- **Server URL** - xlv-uswest1.nutanix.com

For RTP:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - RTP
- **Server URL** - xlv-useast1.nutanix.com


Nutanix Version Info
++++++++++++++++++++

- **AHV Version** - AHV 20190916.158
- **AOS Version** - 5.16.1.2
- **PC Version** - 5.17.0.3
