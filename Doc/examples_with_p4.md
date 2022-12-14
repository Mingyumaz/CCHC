# examples with p4 and ns3


* @todo
* @notsure

# Why choose the `PIFO-TM/ns3-bmv2`

* `ns4-p4simulator` 
  * It is possible to send `ns3::packages` to `bmv2::packet` and convert back to `ns3`. Functionally its can be used as an simmulator for this project.
  * All modules are in the p4simulator module. All functions are too integrated.
  * There are tools dedicated to controlling the network topology.
  * With p4 language version 14(old version), but this will not have a major impact.

* `PIFO-TM/ns3-bmv2`
  * Functionally its can be used as an simulator for this project.
  * With better isolation, the module is divided into three modules, `p4-pipeline`, `traffic-control` and `network`.
  * Have modules related to the project.
    * The example `p4-queue-disc` ,which defines some functions on queue management, priority, etc., and has the structure data corresponding to the metatdata of p4 in ns3.
    * It contains some mods and examples related to virtual queues, for example: `pifo-queue`, `pifo-fast-queue` etc(but not with p4).
  * With p4 language version 16(Latest version).

# PIFO-TM/ns3-bmv2

## introduction for simple-p4-qdisc.cc

This is the introduction for example `simple-p4-qdisc` in [`PIFO-TM/ns3-bmv2`](https://github.com/PIFO-TM/ns3-bmv2), which I have made some small changes to the original.
Since the program doesn't have much of an introduction at the moment, I'm going to start by introducing it here.

* src: [`simple-p4-qdisc`](https://github.com/Mingyumaz/ns-3-dev-git/blob/p4dev/src/traffic-control/examples/simple-p4-qdisc.cc)

* Functional:

The program reduces network congestion by randomly dropping packets on the switch. 
The switch is controlled by the p4 program, which implements the probability of packet loss by relative queue length. The `UDP` flow will goes from n0 to n1.

```
 *  Network topology
 * 
 *     --------------
 *     |  (router)  |
 *     |            |
 *     | [p4-qdisc] |
 *     --------------
 *      |         | 
 *      n0        n1
 *
```
* with p4 configuring: 

P4 will control the switch's virtual queue, which corresponds to the setting of some relevant parameters.

* Notes: In you root ns3 directory, these should be the Directory "./trace-data/" for saving the trace file "./trace-data/tc-qsize.txt", if not: these will be an error.

## introduction for simple-p4-qdisc.p4

* src: [simple-p4-qdisc.p4](https://github.com/Mingyumaz/ns-3-dev-git/blob/p4dev/src/traffic-control/examples/p4-src/simple-p4-qdisc/simple-p4-qdisc.p4)

* Functional:

Random early detection(RED) algorithm implementation with p4: Set random drop for pkts by calculating the `avg_qdepth` in switch.

* build: build with Makefile.

* Possible difficulties for redesign with p4:

Typically, the use of p4 for configure requires the use of [`v1model.p4`](https://github.com/p4lang/p4c/blob/main/p4include/v1model.p4), which defines the generic switch model and some of its internal data formats, etc.
Some of the usual examples of p4 switches can be viewed at [p4-tutorials](https://github.com/Mingyumaz/p4-tutorials/tree/master/exercises).

But in this example `simple-p4-qdisc` uses a custom generic switch model: `simple_pipe.p4`, some of these data have been reprogrammed.
where the data format defined in p4 is defined in the module `p4-pipeline` of ns3 correspondingly.
This involves setting up and converting information in ns3 packages and p4 packages. 
Therefore, a generic p4 program may not be fully applicable, at least for the current tests. This is also very unfortunate.
So if we need new p4 function setting(@todo), for example add the queue ranking for different flow etc, the ns3 related module also need to make corresponding changes and setting.

## `basic-qdisc-congestion.cc`

The Push-In First-Out Queue (PIFO) is a priority queue data structure that allows packets to be "pushed" (enqueued) into an arbitrary location in the queue, but only dequeued from the head. PIFOs enable programmable packet scheduling: by programming how each packet's location in the PIFO is computed as it arrives, PIFOs allow network operators to express a wide variety of practical schedulers. Further, PIFOs are feasible in hardware at the high clock rates (1 GHz) typical of high-end switches today.



# `ns4` with `p4simulator`: 

The simulator set a `p4 Model` class for set p4 parameters, we instantiate one `P4 Model` using a json file compiled from P4 file. 
Also start the thrift to communicate with the controller.

`P4Model` is initialized along with `P4 Device`, and expose a public function called `receivePacket()` to the `P4 Device`. 
Whenever `P4 Device` has a packet needing handling, it call `receivePacket()` and wait for this function to return. 
`receivePacket()` puts the packet through P4 pipeline.

implemetation: ns3::packet --> bmv2::packet --> bmv2::process --> ns3::packet --> transport
So `ns4` differs from `PIFO-TM/ns3-bmv2`, which does not save the metadata in the `ns3` program, so if you need to use the custom data in the header of the data, you need to set it yourself.

## introduction for example: `p4-topo-test.cc`

* src: [p4-topo-test.cc](https://github.com/Mingyumaz/NS3-p4simulator-module/blob/master/examples/p4-topo-test.cc)

It is possible to complete the p4 program simulation without other "redundant" modules. Therefore, to use it, you need to configure the relevant module first.

The basic `ethernet`, `ipv4`, `udp`, `tcp` and `arp` protocols are implemented using the p4 language, and setted in the switch in network. 
In the examples, there is no processing for queues, etc.
But with the old version of the p4.

```
Network topology

 host   switch   switch  switch  switch  switch  host
  h0 ---- s3 ---- s1 ---- s0 ---- s2 ---- s4 ---- h1

Both flow table and p4 configuration
```

