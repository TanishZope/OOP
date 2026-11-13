
cmake_minimum_required(VERSION 3.20)
project(HospitalAppointmentSystem)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Crow CONFIG REQUIRED)

add_executable(hospital_backend backend/main.cpp)

target_link_libraries(hospital_backend PRIVATE Crow::Crow ws2_32 mswsock)
