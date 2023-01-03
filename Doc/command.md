## python version control

system self with py2.7 
Moudle ns3 needs py3.8
Module [PcapXray](https://github.com/Srinivas11789/PcapXray) needs py3.7

```
sudo apt-get install libpython3.7
sudo apt-get install libpython3.7-dev
python3.7 -m pip install cffi
sudo apt-get install python3.7-tk # sudo add-apt-repository ppa:deadsnakes

sudo rm -rf  /usr/bin/python3
sudo  ln  -s  /usr/bin/python3.7 /usr/bin/python3

sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.7 4
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 3

sudo update-alternatives --config python
```


### Problem: The python version

The package install with version python3.8 but not with python3.7, even in manual mode with python3.7.

`sudo apt --reinstall install python3-tk`.

```
p4@p4:~/mmy/src/PcapXray$ sudo update-alternatives --config python
There are 3 choices for the alternative python (providing /usr/bin/python).

  Selection    Path                Priority   Status
------------------------------------------------------------
* 0            /usr/bin/python3.7   4         auto mode
  1            /usr/bin/python2.7   2         manual mode
  2            /usr/bin/python3.7   4         manual mode
  3            /usr/bin/python3.8   3         manual mode

Press <enter> to keep the current choice[*], or type selection number: 

```

And the python version switch will occer the error in `ns3`: the `./waf build` will call the python script and then `raise StopIteration`.

Solution: taken from [Fix generators](https://discuss.ardupilot.org/t/waf-crashes-on-copter-3-6-5/48682/3)

```
1.1. in ardupilot/modules/waf/waflib/Node.py
replace yield <object> (note that <object> is a placeholder for the object that is to be yielded) with

 try:
     yield <object>
 except StopIteration:
     return
within Node.ant_iter method (ca. line 590).
This occurs 3 times, 2 times with node as , 1 time with k as .
Then replace raise StopIteration with return in the method’s last line.
```

## module for plot

```
sudo apt-get install wireshark
sudo apt-get install tshark

```

## ns3

```
616 of 627 tests passed (616 passed, 10 skipped, 0 failed, 1 crashed, 0 valgrind errors)
List of SKIPped tests:
    examples/routing/simple-routing-ping6.py
    examples/tutorial/first.py
    examples/wireless/mixed-wired-wireless.py
    examples/wireless/wifi-ap.py
    ns3-tcp-cwnd
    ns3-tcp-interoperability
    nsc-tcp-loss
    src/bridge/examples/csma-bridge.py
    src/core/examples/sample-simulator.py
    src/flow-monitor/examples/wifi-olsr-flowmon.py
List of CRASHed tests:
    pifo-tree-queue-disc



./test.py --suite=pifo-tree-queue-disc
```

## gdb

```
set print pretty on
p *(NetDevice *) 0x55555559ec20

export NS_LOG='PifoQueueDisc=function'
```