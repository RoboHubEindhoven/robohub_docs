# Startup Suii

The startup of suii has multiple parts mainly divided in:

- [Hardware startup](#hardware-startup)
- [Control Suii](#control-suii)
- [Making a map](#making-a-map)

### Hardware startup:

* **!!! Get suii up off the ground !!!**
* Connect the battery with the yellow xt-90 connectors
* Press the green button
* When the blue button blinks press the blue button
* When the wheels are not moving anymore place the robot on the ground, (**This will take a minute**)
* Start the UR3 by pressing the tiny red button hanging out of the control box
* Connect to the Suii wifi network 
* Connect to the UR vnc on 192.168.2.204 with the [RealVNC viewer](https://www.realvnc.com/en/connect/download/vnc/)
* Now start up the robot in the UR interface on the vnc.
* After starting the UR you can move the robot arm into a more comfortable pose by pressing the button on the gripper.

### Control Suii:

To work with suii you have to login to her. 

Connect to the Suii wifi network or connect by ethernet cable to the switch on her back.

```bash
$ ssh suii@NUC.lan  # Login with password
```

To manually control suii:

```bash
$ rosrun rosbridge_server rosbridge_websocket
```

then go to [192.168.2.113:5000/drive](192.168.2.113:5000/drive)

if it is not working restart the server:

```bash
$ ssh suii@NUC.lan
$ cd workspace/server
$ ./Aguilegia
```

#### Setup ROS on your pc:

Setup some variables on your pc:

```bash
$ editor ~/.bashrc
# And add:
export ROS_IP=YOUR_IP_ADRESS  # check ifconfig eg.: 192.168.2.xxx
export ROS_MASTER_URI=http://192.168.2.113:11311
# save it 
$ source ~/.bashrc
```



### Making a map:

To start the software run in suii:  

```
 roslaunch suii_bringup mapping.launch
```

Drive around with the robot and visualize on you own with RViz.

```bash
# Save the map
$ rosrun map_server map_saver -f YOUR_MAP_NAME
```

Now copy the map to your pc and edit it with [Gimp](https://www.gimp.org/):

```bash
exit  # get out of the ssh session
scp suii@NUC.lan:maps/YOUR_MAP_NAME.pgm ./
gimp YOUR_MAP_NAME.pgm
```

Now edit in all the No Go Zones:

* Tables
* Closets 
* Chairs
* Non seeable objects

### Starting the rest:

Edit the suii_low.launch to use the new maps 

```
 rosed suii_bringup suii_low.launch
```

 Start suii_low 

```
 roslaunch suii_bringup suii_low.launch
```

 Start vision (new terminal)  

```bash
 source envpy3 && python3 ~/catkin_ws/src/suii/suii_vision/scripts/vision_core/vision_manager.py
```

 Start suii_high (new terminal) 

```
 roslaunch suii_bringup suii_high.launch
```

 Test navigation with the use of rviz (don`t forget to set suii at the right pose in the map) * use rviz to drive suii to the workstations and save the coordinates to the "waypoint_list.json" in the "suii_demo/config" folder * Edit the task_list.json to make a demo in the "suii_demo/config" folder *run the demo: 

```
 roslaunch suii_demo demo.launch
```
