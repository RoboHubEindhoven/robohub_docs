# Startup Suii

First turn on suii and enable the motors, make a map using  

```
 roslaunch suii_bringup mapping.launch
```

 Copy map to laptop * Edit one with obstacles (for navigation) and one with only the visible objects  (for localisation AMCL) * Copy the new maps to the maps folder on suii. * Edit the suii_low.launch to use the new maps 

```
 rosed suii_bringup suii_low.launch
```

 Start suii_low 

```
 roslaunch suii_bringup suii_low.launch
```

 Start vision (new terminal)  

```
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
