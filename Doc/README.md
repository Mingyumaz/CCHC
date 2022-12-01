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


