cmake_minimum_required(VERSION 3.0.2)  
project(beginner_tutorials)  
find_package(catkin REQUIRED COMPONENTS
   roscpp
   rospy   
   std_msgs   
   genmsg   
   message_generation )   

add_message_files(DIRECTORY msg FILES Num.msg) 
add_service_files(DIRECTORY srv FILES AddTwoInts.srv)    

generate_messages(DEPENDENCIES std_msgs)    

catkin_package(  

)  

include_directories( include ${catkin_INCLUDE_DIRS} )  

catkin_install_python(PROGRAMS scripts/talker.py scripts/listener.py   
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION} )    

add_executable(talker src/talker.cpp) 
target_link_libraries(talker ${catkin_LIBRARIES}) 
 
add_executable(listener src/listener.cpp) 
target_link_libraries(listener ${catkin_LIBRARIES}) 

add_executable(add_two_ints_server src/add_two_ints_server.cpp)
target_link_libraries(add_two_ints_server ${catkin_LIBRARIES})
add_dependencies(add_two_ints_server beginner_tutorials_gencpp)

add_executable(add_two_ints_client src/add_two_ints_client.cpp)
target_link_libraries(add_two_ints_client ${catkin_LIBRARIES})
add_dependencies(add_two_ints_client beginner_tutorials_gencpp)

