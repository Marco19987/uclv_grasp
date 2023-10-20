cmake_minimum_required(VERSION 3.8)
project(uclv_grasp)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(uclv_grasp_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(cv_bridge REQUIRED)
find_package(depth_optimization_interfaces REQUIRED)
find_package(uclv_utilities REQUIRED)


add_executable(pose_post_proc_server src/pose_post_proc_server.cpp)
ament_target_dependencies(pose_post_proc_server rclcpp 
                          uclv_grasp_interfaces geometry_msgs 
                          sensor_msgs std_msgs tf2_ros cv_bridge 
                          depth_optimization_interfaces uclv_utilities)

install(TARGETS
  pose_post_proc_server 
  DESTINATION lib/${PROJECT_NAME})


if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()

