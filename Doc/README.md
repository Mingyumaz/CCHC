Docs for project

## week 49

1. Create the project in Github.
2. Complete the `Expose`.
3. Setting up for env in one go:
   1. mininet with bmv2;
   2. ns3 with bmv2, implementation by [p4simulator](https://github.com/P4Simulator/P4Simulator);
   3. ns3 with bmv2, implementation by [PIFO-TM](https://github.com/PIFO-TM/ns3-bmv2);

## week 50

1. env [ns3-p4simulator](https://github.com/Mingyumaz/ns-3-dev-git/tree/p4simulator) branch `p4simulator`
2. env [ns3-PIFO-TM](https://github.com/Mingyumaz/ns-3-dev-git/tree/p4dev) branch `p4dev`
3. Understand the architecture and how it works:

![Architecture of ns3-PIFO-TM](https://github.com/Mingyumaz/CCHC/blob/main/Doc/figures/ns3_bmv2_architecture.png)

1. Try the examples in two method:
   1. `ns3-p4simulator` goes well.
   2. `ns3-PIFO-TM` goes well also (by 27.12.2022).

## week 51

tasks:
   1. finish the demo and test with some result and capture the data.
   2. for example with `.pcap` file: plot the captured data.(this may using python or wireshark tools)
   3. I have tryed the [PcapXray](https://github.com/Srinivas11789/PcapXray), but It cannot be analyzed normally because our package is *customized*, see result figure: "Doc\figures\pcap_xray_result.png"\
   4. Therefore, we need to deal with the packages visualization by ourself.

## week 1

   1. Choose `ns3-PIFO-TM` as the simulator, because it can do with the queue management.
   2. Test the simulation in `ns3-PIFO-TM` with `p4-queue`.
   3. with the topo.
   ```
      * n0------->-------|                    |-------->-------n4
      *                  |                    |
      *                  n2------>------------n3
      *                  |                    |
      * n1------->-------|                    |-------->-------n5
   ```

## week 2

### The architecture of the simulator

   ![Figure: Architecture of the two simulators.](https://github.com/Mingyumaz/CCHC/blob/main/Doc/figures/architecture_of_simulators.png)

   1. The architecture of `ns3-PIFO-TM` is: bmv2 as `traffic-controller`
      1. `ns3-PIFO-TM` because its in the traffic controller, so its easier to manage and control the queue. But the p4 script used for its emulation is **not generic, but customized**. It doesn't work with hardware and also can not work with Tofino.
      2. Part of its queue management functions, etc., is done in ns3.
   2. But `ns4-P4simulator`'s architecture: bmv2 as `net-device`. This will make a very big difference.
      1. Currently only p4-version14 can be used for control. But the compiler only supports automatic conversion of p4 from version14 to version16.
      2. Try to contact the author of the paper, because the paper claims: "NS4 could support all features and both two versions of P4."
      3. Because of the lack of documentation help and other information, and the test p4-16 is not the whole error, try gdb trace found the problem.

PS: [what-is-the-queue-management-approach-in-p4?](https://forum.p4.org/t/what-is-the-queue-management-approach-in-p4/273)

What have done?
   1. The simulator is determined to use `ns4-P4simulator`

Next Step:
   1. Find the solution for the queue management. 
      1. There is the new paper about the coordination between priority queues and the controlled delay protocol.
   2. Try to using the system slurm for later simulation with high performance.
   3. Take tracing for the `packet delay` and `packet loss` and visualization.