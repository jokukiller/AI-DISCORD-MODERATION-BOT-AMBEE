cmake_minimum_required(VERSION 4.0)
project(AMBEE_rewrite)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(AMBEE_rewrite main.cpp)

find_package(dpp CONFIG REQUIRED)
find_package(cpr CONFIG REQUIRED)
find_package(nlohmann_json CONFIG REQUIRED)
find_package(mongocxx CONFIG REQUIRED)
find_package(bsoncxx CONFIG REQUIRED)

target_link_libraries(AMBEE_rewrite PRIVATE nlohmann_json::nlohmann_json)
target_link_libraries(AMBEE_rewrite PRIVATE cpr::cpr)
target_link_libraries(AMBEE_rewrite PRIVATE dpp::dpp)
target_link_libraries(AMBEE_rewrite PRIVATE mongo::mongocxx_shared)
target_link_libraries(AMBEE_rewrite PRIVATE mongo::bsoncxx_shared)
