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

## module for plot

```
sudo apt-get install wireshark
sudo apt-get install tshark

```