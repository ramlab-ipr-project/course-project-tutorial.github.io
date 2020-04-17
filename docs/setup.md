# Setup
Author: Yuxuan, Liu
Date: 2020.04.17


## Enviroment
The newest version of regarding softwares is recommended.<br>
[ROS: Kinetic]<br>
[V-REP: 3.5.0 PRO EDU] <br>
Plugins(Please git clone them from the latest master): <br>
[vrep_ros_bridge] <br>
[vrep_ros_interface] <br>
Platform: Ubuntu 16.04 LTS 

The above environment was tested before. If you have any problems, please contact yliuhb@connect.ust.hk

I personally tested the raw [V-REP: 3.5.0 PRO EDU] on ROS-Melodic/Ubuntu 18.04 **without** [vrep_ros_bridge] or [vrep_ros_interface], and the rostopics also work fine for me.


## Demo
After configuring the environment, run
```bash
roscore
```
And in another terminal, run(under the unzipped VREP_ROOT)
```
./vrep.sh
```
In V-REP, load the scene file [*env.ttt*](resourcres/env.ttt).
**After pressing the start button**, you can use
```
rostopic list
```
to see the Topics of vrep.

Topics we need: <br>
/vrep/camera_switch<br>
/vrep/cmd_vel<br>
/vrep/image<br>
/vrep/laser_switch<br>
/vrep/scan<br>
/tf


Check the meta-info of a topic:
```
rostopic info /vrep/cmd_vel
```
For controling the Pioneer p3dx robot, type the following in terminal
```
## Translation
rostopic pub -r 10 /vrep/cmd_vel geometry_msgs/Twist  '{linear:  {x: 1.0, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 0.0}}' 

## Rotation
rostopic pub -r 10 /vrep/cmd_vel geometry_msgs/Twist  '{linear:  {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 1.0}}' 
```
where $x$ in "linear" stands for the velocity of the robot (forward as positive), and $z$ in "angular" for the rotation (counter clockwise observed from top as positive).

Make sure you can receive lidar scanner output (/vrep/scan), camera output (/vrep/image) and the coordinate transform from base_link to camera_link/laser_link (/tf) on ROS side. You can verify these with ros commands/rviz or your own codes.

Getting more familiar with ROS is part of the project, you could contact me for help while you are encouraged to solve them your own first.


[ROS: Kinetic]:http://wiki.ros.org/kinetic
[V-REP: 3.5.0 PRO EDU]:http://coppeliarobotics.com/files/V-REP_PRO_EDU_V3_5_0_Linux.tar.gz
[vrep_ros_bridge]:https://github.com/lagadic/vrep_ros_bridge
[vrep_ros_interface]:https://github.com/CoppeliaRobotics/v_repExtRosInterface