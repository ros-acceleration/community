# ROS 2 Hardware Acceleration Working Group

This document defines the scope and governance of the Working Group (WG).

| Item | Description |
|------|-------------|
| **Mission** | Drive creation, maintenance and testing of acceleration kernels on top of open standards (C++ and OpenCL) for optimized ROS 2 and Gazebo interactions over different compute substrates (including FPGAs, GPUs and ASICs). |
| **Scope** | hardware acceleration in a) embedded (edge) devices, b) workstations, c) data centers and d) cloud |
| **Objectives** | 1) Design tools and conventions to seamlessly integrate acceleration kernels and related embedded binaries into the ROS 2 computational graphs leveraging its existing build system (ament) and meta build tools (colcon). |
|  |  2) Provide reference examples and blueprints for acceleration architectures used in ROS 2 and Gazebo. |
|  |  3) Facilitate testing environments that allow to benchmark accelerators with special focus on power consumption and time. |
|  |  4) Survey the community interests on acceleration for ROS 2 and Gazebo. |
|  |  5) Produce demonstrators with robot components, real robots and fleets that include acceleration to meet their targets |


- [ROS 2 Hardware Acceleration Working Group](#ros-2-hardware-acceleration-working-group)
  - [Architecture](#architecture)
  - [Reference hardware platforms](#reference-hardware-platforms)
    - [Official](#official)
    - [Community](#community)
    - [Adding your board](#adding-your-board)
  - [Subprojects](#subprojects)
    - [Subproject List](#subproject-list)
    - [Standards for subprojects](#standards-for-subprojects)
    - [Adding new subprojects](#adding-new-subprojects)
    - [Subproject changes](#subproject-changes)
    - [Deprecating subprojects](#deprecating-subprojects)
  - [Governance](#governance)
    - [Meetings](#meetings)
    - [Communication Channels](#communication-channels)
    - [Membership, Roles and Organization Management](#membership-roles-and-organization-management)
    - [Modifying this governance document](#modifying-this-governance-document)


## Architecture

```
  ROS 2 stack                   HAWG @ ROS 2 stack

+-------------+             +--------------------+
|             |             |  xilinx_examples   |
| user land   |  +-------------------+-----------+-------+--------------+
|             |  |       Drivers     |     Libraries     |    Cloud     |
+-------------+  +---------------+---+--------+-------------------------+
|             |  |   ament_vitis | ament_rocm |          |  accel_fw    |
|             |  +---------------+----------+-+----------+-+------------+
|  tooling    |  |     ament_acceleration   | colcon_accel |  accel_fw  |
|             |  +------------------------------------------------------+
|             |  |      build system        |   meta build |  firmware  |
+-------------+  +--------------------------+--------------+------------+
|     rcl     |
+-------------+
|     rmw     |
+-------------+
|   adapter   |
+-------------+
|             |
| middleware  |
|             |
|             |
+-------------+
```

Join the [first WG meeting (or check the recording)](https://discourse.ros.org/t/announcing-the-hardware-acceleration-wg-meeting-1/20826) for more details on the architecture.

## Reference hardware platforms

### Official
The following boards are supported:

| Board | Picture | Description |
|------------|-------|-------------|
| [Kria `K26` Adaptive System-on-Module](https://www.xilinx.com/products/som/kria/k26c-commercial.html) | ![](https://www.xilinx.com/content/dam/xilinx/imgs/products/som/som-k26-main.png) | The Kria™ K26 SOM is the first adaptive Single Board Computer, a production-grade and tiny System-on-Module for edge vision and robotics applications. Available in Commercial and Industrial Grade variants.  |
| [Kria `KV260` Vision AI Starter Kit](https://www.xilinx.com/products/som/kria/kv260-vision-starter-kit.html) | ![](https://www.xilinx.com/content/dam/xilinx/imgs/products/som/som-kv260-4.png) | The Kria™ KV260 starter kit is a development platform for the K26, the first adaptive Single Board Computer. KV260 offers a compact production-grade board for edge vision and robotics applications.  |

### Community

The following list includes boards that have been validated and have unofficial community support. *No guarantees provided since no CI jobs are run on on these boards*.

<details><summary>Community supported boards</summary>

| Board | Picture | Description |
|------------|-------|-------------|
| [Xilinx Zynq UltraScale+ MPSoC `ZCU102` Evaluation Kit](https://www.xilinx.com/products/boards-and-kits/ek-u1-zcu102-g.html) | ![](https://www.xilinx.com/content/dam/xilinx/imgs/kits/whats-inside/zcu102-evaluation-board-w.jpg) | The ZCU102 Evaluation Kit enables designers to jumpstart designs for automotive, industrial, video, and communications applications. This kit features a Zynq® UltraScale+™ MPSoC with a quad-core Arm® Cortex®-A53, dual-core Cortex-R5F real-time processors, and a Mali™-400 MP2 graphics processing unit  |
| [Zynq UltraScale+ MPSoC `ZCU104` Evaluation Kit](https://www.xilinx.com/products/boards-and-kits/zcu104.html) | ![](https://www.xilinx.com/content/dam/xilinx/imgs/kits/whats-inside/zcu104-evaluation-board-w.jpg) |  The ZCU104 Evaluation Kit enables designers to jumpstart designs for embedded vision applications such as surveillance, Advanced Driver Assisted Systems (ADAS), machine vision, Augmented Reality (AR), drones and medical imaging. This kit features a Zynq® UltraScale+™ MPSoC EV device with video codec and supports many common peripherals and interfaces for embedded vision use case. |

</details>

### Adding your board
We're working with the community on a plan to add new boards to the lists above. Create an issue if you'd like to show interest before we come up with a formal community plan.

## Subprojects

This Working Group owns and maintains the following Subprojects.
Its meetings and membership are largely focused on the direction, design, and work on the projects.

### Subproject List

The following subprojects are owned by the Working Group:

<!-- {{

* template-project
  * Description: Brief description of project. Remove this item and add new projects using this format.
  * Repositories
    * link-to-repository

}} -->

### Standards for subprojects

Subprojects must meet the following criteria (and the WG agrees to maintain them upon adoption).

* Build passes against ROS 2 master
* The ROS 2 standard linter set is enabled and adhered to
* If packages are part of nightly builds on the ROS build farm, there are no reported warnings or test failures
* Issues and pull requests receive prompt responses
* Releases go out regularly when bugfixes or new features are introduced
* The backlog is maintained, avoiding longstanding stale issues
* Quality builds are green (address sanitizer, thread sanitizer, clang thread safety analysis)
* Test suite passes
* Code coverage is measured, and non-decreasing level is enforced in PRs

### Adding new subprojects

To request introduction of a new subproject, add a list item to the "Subprojects" section and open a Pull Request to this repository, following the default Pull Request Template to populate the text of the PR.

PR will be merged on unanimous approval from Approvers.

### Subproject changes

Modify the relevant list item in the "Subprojects" section and open a Pull Request to this repository, following the default Pull Request Template to populate the text of the PR.

PR will be merged on unanimous approval from Approvers.

### Deprecating subprojects

Projects cease to be useful, or the WG can decide it is no longer in their interest to maintain.
We do not commit to maintaining every subproject in perpetuity.

To suggest removal of a subproject, remove the relevant list item in the "Subprojects" section and open a Pull Request in this repository, following instructions in the Pull Request Template to populate the text of the PR.

PR will be merged on unanimous approval from Approvers.

If the repositories of the subproject are under the WG's GitHub organization, they will be transferred out of the organization or deleted at this time.

## Governance

### Meetings

* Regular WG Meeting: TBD
  * {{when and where will meetings be announced}}
  * {{what artifacts will be posted after the meetings, e.g. Minutes, Recordings}}

### Communication Channels

* Meeting invite group: [Meeting invite group](https://groups.google.com/g/ros-2-hardware-acceleration-wg)
* Github organization: [ros-acceleration](https://github.com/ros-acceleration)
* Discourse tag: [wg-acceleration](https://discourse.ros.org/tag/wg-acceleration)


<!-- {{How can members communicate with each other? Discourse, Discord, IRC, email list, etc.}} -->

<!--
### Backlog Management

{{Is any project management software/site used to track work for this Working Group? How can new members discover the highest impact tasks they could take on? GitHub Projects, ZenHub, etc.}} -->

### Membership, Roles and Organization Management

Working Group members may act in one or more of the following roles:

* **Member**
  * Prerequisite: Attend at least one out of the last three Working Group meetings
  * Responsible for triaging issues
* **Reviewer**
  * All reviewers are members
  * Prerequisite: Proven track record of high-quality reviews to WG Subprojects
  * Responsible for reviewing pull requests
* **Approver**
  * All approvers are reviewers
  * Prerequisite: Proven track record of high-quality contributions and reviews to WG Subprojects
  * Responsible for approving and merging pull requests
  * Responsible for vetting and accepting new projects into the Working Group
* **Lead**
  * TSC member or their delegate
  * Responsible for organizing and moderating working group meetings
  * Responsible for posting meeting materials (minutes, recordings, etc.)
  * Responsible for breaking ties

To become a member or change role, create an issue in this repository using the appropriate issue template.
Such applications are accepted upon unanimous agreement from Approvers, and are typically based on the applicant's history with the subprojects of the Working Group.
The Lead role cannot be applied for, as it is an appointee of the ROS 2 TSC.

### Modifying this governance document

Changes to this document will be made via Pull Request. The PR will be merged on unanimous agreement from Approvers.
