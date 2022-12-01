# Congestion Control for Haptic Communication

## Exposé

Tactile Internet requires stringent latency while the data rates vary drastically, 
traditional approaches not fulfill the QoS and the bandwidth utilization requirement, 
for example, In-band Network Telemetry (INT[1]) model can reduce the congestion of the network, 
but haptic stream still not meet the latency demand.

Therefore, a dynamic and network-aware resource management strategy will be design with satisfying the QoS requirement while without wasting precious bandwidth. 
Reference the methodological design in article[2], 
by setting up virtual queues in the protocol independent switch architecture (PISA) network, 
in which different priorities are provided for different traffic streams to meet the requirements of the network. 
In anticipation, this method guarantees both high utilization by virtual queue and low latency by traffic priority.
The task of this thesis is to design, implement and evaluate a specially configured PISA network, 
which should meet the requirements of tactile internet. This includes the following aspects”


This includes the following aspects:

* Review of state of the art algorithms and approaches.
* Sketching out the solution approach with virtual queue and different traffic priority.
* Implementation the approach in ns3 using bmv2 switch.
* Modify and adjust the implementation according to the simulation results.
* The model performance comparison to the In-band Network Telemetry (INT) model.
* Evaluation of the virtual queues model.

This thesis is written in English. 
As for the timeline, I'm leaning towards three weeks for each of the above steps, 
with the rest of the time to complete the paper and presentation work.


[1] Kim C, Sivaraman A, Katta N, et al. In-band network telemetry via programmable dataplanes[C]//ACM SIGCOMM. 2015, 15.
[2] Lhamo O, Nguyen G T, Fitzek F H P. Virtual Queues for QoS Compliance of Haptic Data Streams in Teleoperation[J]. 2022.

##  Some plans and ideas

### About the simulator choose

System: Ubuntu 20.04.5 LTS (Focal Fossa) in virtual box
Hardware: CPU: i5-12400; MEM: 24GB;

There are mainly two ways for emulation/simulation: 

* Emulation: Using mininet with bmv2. It a proven solution, but the performance is poor.
    * It more suit for test the network topo or configure.
* Simulation: Using ns3 with P4 module, and the P4 module with push our configuration info into bmv2. Because of the simulation method, its probably possible to simulate the performance of Tifino.

In order to achieve high performance, ns3 was chosen to be used.

# Related papers or website

## Data plane programming/P4

For the related website

* [Official website for P4](https://p4.org/learn/), **gives some related github repositories**, easy for search.
* [P4~16~ Language Specification](https://p4.org/p4-spec/docs/P4-16-v-1.2.3.html#sec-terms-definitions-and-symbols)
* [ACM SIGCOMM 2017 Tutorial (Full-Day): P4→NetFPGA](https://conferences.sigcomm.org/sigcomm/2017/tutorial-P4-NetFPGA.html)
* [ACM SIGCOMM 2017 Tutorial (Full-Day): P4: Programming the Network Data Plane](https://conferences.sigcomm.org/sigcomm/2017/tutorial-p4.html)
* [ACM SIGCOMM 2018 Full-Day Tutorial on Programming the Network Data Plane (P4)](https://conferences.sigcomm.org/sigcomm/2018/tutorial-p4.html), this provides the virtual machine image for p4 env.
* [Github-p4_tutorials](https://github.com/Mingyumaz/p4-tutorials), the tutorials for p4, giving the vagrantfile and some examples with p4 in mininet.
* [Github-p4-guide](https://github.com/jafingerhut/p4-guide), @TODO

For the related papers
* Hauser F, Häberle M, Merling D, et al. A survey on data plane programming with p4: Fundamentals, advances, and applied research[J]. arXiv preprint arXiv:2101.10632, 2021.
* Bosshart P, Daly D, Gibb G, et al. P4: Programming protocol-independent packet processors[J]. ACM SIGCOMM Computer Communication Review, 2014, 44(3): 87-95.

## simulator
* Bai J, Bi J, Kuang P, et al. NS4: Enabling programmable data plane simulation[C]//Proceedings of the Symposium on SDN Research. 2018: 1-7.
* [Github-NS4-P4Simulator](https://github.com/P4Simulator/P4Simulator)
* [Github-PIFO-TM/ns3-bmv2](https://github.com/PIFO-TM/ns3-bmv2)

## congestion control algorithm
* Lhamo O, Nguyen G T, Fitzek F H P. Virtual Queues for QoS Compliance of Haptic Data Streams in Teleoperation[J]. 2022.

* Kim C, Sivaraman A, Katta N, et al. In-band network telemetry via programmable dataplanes[C]//ACM SIGCOMM. 2015, 15.
  * In paper gives a idea: In-band Network Telemetry (INT), it is a new abstraction that allows data packets to query switch-internal state such as queue size, link utilization, and queuing latency. But It only briefly describes the idea and implementation demos, without detailed testing of its performance.

* Turkovic B, Biswal S, Vijay A, et al. P4QoS: QoS-based packet processing with P4[C]//2021 IEEE 7th International Conference on Network Softwarization (NetSoft). IEEE, 2021: 216-220.
  * To deal with the flows with varying QoS, this method embedding QoS requirements in the packets themselves and leveraging P4-programmable network switches to process the traffic based on them. This can significantly improve the performance in the network also fulfill the QoS. But it does not take into account that the data flow may change drastically(haptic flow).
  
* Michel O, Keller E. Policy Routing using Process-Level Identifiers[C]//2016 IEEE International Conference on Cloud Engineering Workshop (IC2EW). IEEE, 2016: 7-12.
  * By embedding process-level information such as user ID and process ID into packets through hashing operations, programmable switches use process-level information to achieve more intelligent packet processing.
  * Again, it has some problems : The implementation of PRPL[5] every packet being sent out to the network needs to be processed in user space and annotated with a token, that will become a performance bottleneck.

* Beshley M, Kryvinska N, Beshley H, et al. Virtual router design and modeling for future networks with QoS guarantees[J]. Electronics, 2021, 10(10): 1139. 
  * Through dynamic and static virtualized routers and three classifications of traffic: video, voice, and data with four types virtual router in one device. Different traffic is routed through different virtual routes, each with specific algorithms to guarantee QoS.
  * What’s more, Its simulation results conclude that: the priority service system of information flows is not able to provide all the flows of the guaranteed level of QoS by the criterion of minimum delay and is less effective in comparison with the system of dynamic virtualization of computing router resources.

* Harkous H, Papagianni C, De Schepper K, et al. Virtual queues for P4: A poor man’s programmable traffic manager[J]. IEEE Transactions on Network and Service Management, 2021, 18(3): 2860-2872.
* Nichols K, Jacobson V, McGregor A, et al. Controlled delay active queue management[R]. 2018.
* Carlucci G, De Cicco L, Holmer S, et al. Congestion control for web real-time communication[J]. IEEE/ACM Transactions on Networking, 2017, 25(5): 2629-2642.
* Carlucci G, De Cicco L, Holmer S, et al. Analysis and design of the google congestion control for web real-time communication (WebRTC)[C]//Proceedings of the 7th International Conference on Multimedia Systems. 2016: 1-12.
  * Low latency high bandwidth algorithm for video conferencing. using the delay gradient to infer congestion, and the algorithm limits the transmission rate dynamically by estimating the congestion. It is mainly for video streaming processing, not relevant with haptic flow