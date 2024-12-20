sudo apt install ros-humble-xacro ros-humble-joint-state-publisher-gui
sudo apt install ros-humble-gazebo-ros-pkgs
added lidar xacro containing lidar_frame adn joint as lidar_joint which publishes to /scan (topic),sensor_msgs/LaserScan

sudo apt install ros-humble-slam-toolbox
/opt/ros/humble/share/slam_toolbox/config/mapper_params_online_async.yaml place this in config dir to modify
ros2 launch slam_toolbox online_async_launch.py slam_params_file:=./src/diff_bot/config/mapper_params_online_async.yaml

//for mapping
# ROS Parameters
    odom_frame: odom
    map_frame: map
    base_frame: base_footprint
    scan_topic: /scan
    use_map_saver: true
    mode: mapping #localization

    # if you'd like to immediately start continuing a map at a given pose
    # or at the dock, but they are mutually exclusive, if pose is given
    # will use pose
    #map_file_name: test_steve
    # map_start_pose: [0.0, 0.0, 0.0]
    # map_start_at_dock: true

//for localisation
# ROS Parameters
    odom_frame: odom
    map_frame: map
    base_frame: base_footprint
    scan_topic: /scan
    use_map_saver: true
    mode: localization

    # if you'd like to immediately start continuing a map at a given pose
    # or at the dock, but they are mutually exclusive, if pose is given
    # will use pose
    map_file_name: /home/paradox-ubuntu/dev_ws/src/diff_bot/maps/maze_map_serial
    # map_start_pose: [0.0, 0.0, 0.0]
    map_start_at_dock: true


sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup ros-humble-turtlebot3*
// create a nav2 map_server with map.yaml loaded
ros2 run nav2_map_server map_server --ros-args -p yaml_filename:=./src/diff_bot/maps/maze_map_save.yaml -p use_sim_time:=true
// to activate the node
ros2 run nav2_util lifecycle_bringup map_server


// now run nav2 amcl (localization algo )
ros2 run nav2_amcl amcl --ros-args -p use_sim_time:=true
// to activate the node
ros2 run nav2_util lifecycle_bringup amcl
// now set the fixed frame in **rviz** to "map"

sudo apt install ros-humble-twist-mux
        