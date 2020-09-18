---
title: "Source of Truth"
slug: "source-of-truth"
---

* toc
{:toc}


{%
include callout.html
type="warning"
title="Advanced material ahead"
content="The following is a technical document for advanced developers who require performing high-precision data operations. The majority of developers can view the information below as an implementation detail and not a hard requirement for understanding the FarmBot software stack."
%}

The [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem) states that it is impossible for a distributed data store to simultaneously provide more than two out of the following three guarantees:

  * **Consistency**: Every read receives the most recent write or an error
  * **Availability**: Every request receives a response that is not an error
  * **Partition tolerance**: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

The FarmBot software system is a distributed data store, with at least the following nodes:
  * Frontend
  * API
  * FBOS
  * Firmware

By design, FarmBot must be partition tolerant so that it can continue taking care of the garden in the absence of a connection to the web app. This is especially important for FarmBots that are installed off-grid, where an internet connection may only be available every few months.

Abiding by the CAP theorem, this leaves a tradeoff we must make between consistency and availability of data resources. Luckily, we can make different choices as to which data guarantees we want for each resource in order to provide the best user experience

The table below shows which guarantees we have chosen for the various resources, and what that choice results in. Note that consistency is abbreviated as C, availability as A, partition tolerance as P, frontend as FE, and FarmBot OS as FBOS.

|Resource                      |Nodes That Write              |Source of Truth               |Guarantees                    |Result                        |
|------------------------------|------------------------------|------------------------------|------------------------------|------------------------------|
|Bot name<br>Bot timezone<br>Auto update<br>Beta opt-in<br>Auto factory reset<br>Connection attempt period<br>Camera<br>Auto sync<br>Tool slots<br>Tool status<br>Pin bindings<br>Webcam feeds<br>Peripherals<br>Sensors<br>User account settings<br>Sequences<br>Regimens<br>Events<br>Point groups<br>Installed farmwares (intent)<br>Installed firmware (intent)<br>Account credentials (intent)<br>MCU parameters (not including exceptions below)|API, FE                       |API                           |CP                            |These resources are not available to be changed by the FE when the FE is partitioned from the API <br><br>Availability is agnostic to whether FBOS is partitioned or not.
|Plant points<br>Weed points<br>Generic points<br>Mounted tool<br>Tool slot tool ID|API, FBOS, FE                 |API                           |AP for FBOS<br>CP for the FE  |These resources are:<br>  * Always available to be changed by FBOS<br>  * Only available to be changed by the FE when FBOS is online (unpartitioned)
|FBOS version (state)<br>Installed farmware (state)<br>Installed firmware (state)<br>Currently on beta (state)<br>Paired account credentials (state)|FBOS                          |FBOS                          |AP                            |These resources are always available to be changed by FBOS.
|Peripheral states<br>Event status|FBOS, FE                      |FBOS                          |AP for FBOS<br>CP for the FE  |These resources are:<br>  * Always available to be changed by FBOS<br>  * Only available to be changed by the FE when FBOS is online (unpartitioned)
|MCU parameter exceptions:<br>  * Axis length<br>  * Other self-calibration parameters|API, FBOS, FE                 |FBOS                          |AP for FBOS<br>CP for the FE  |These resources are:<br>  * Always available to be changed by FBOS<br>  * Only available to be changed by the FE when FBOS is online (unpartitioned)

# Source of truth

In addition to showing the CAP theorem guarantees, the table above also shows which node is the most authoritative (**source of truth**) for each data resource. Defining a source of truth allows us to determine what course of action to take to resolve data inconsistencies, which can happen for AP guaranteed data resources with multiple writers, especially during network partitions.

## A practical example

The peripheral resource needs to always be available to FBOS so that FarmBot can take care of the garden even when offline. This necessitates AP guarantees to that resource for FBOS. The FE also needs to be able to change peripheral resources for manual control. If we chose AP guarantees to the peripheral resource for the FE as well, it would be possible for the FE to show a peripheral state that is inconsistent with FBOS when FBOS is offline. Because FBOS will always be the more correct node (the source of truth) when it comes to peripheral state, it makes sense in this case to choose CP guarantees to the peripheral resource for the FE.

This choice results in preventing the user from using the peripheral toggles when the bot is offline.
