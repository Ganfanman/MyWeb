cmake_minimum_required(VERSION 3.1)

set(PROJECT_NAME my_web)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

##add_compile_options(-Wall -Wextra -Wpedantic)

project(${PROJECT_NAME} VERSION 0.1
                        DESCRIPTION "Web backend project base on OATPP"
                        HOMEPAGE_URL "https://github.com/Ganfanman/MyWeb"
                        LANGUAGES CXX)

set(INCLUDE_DIR backend/component/include backend/controller/include backend/DTOs/include)

set(INCLUDE backend/component/include/web_component.h backend/controller/include/web_controller.h backend/DTOs/include/dtos.h)
set(SOURCE backend/component/src/web_component.cpp backend/controller/src/web_controller.cpp backend/DTOs/src/dtos.cpp)

add_library(${PROJECT_NAME}_lib
        ${SOURCE}
        ${INCLUDE}
)

find_package(oatpp 1.3.0 REQUIRED)

target_link_libraries(${PROJECT_NAME}_lib
        PUBLIC oatpp::oatpp
)

target_include_directories(${PROJECT_NAME}_lib PUBLIC 
        ${INCLUDE_DIR}
)

add_executable(${PROJECT_NAME}_exe
        backend/webapp.cpp
)

target_link_libraries(${PROJECT_NAME}_exe ${PROJECT_NAME}_lib)

target_include_directories(${PROJECT_NAME}_exe PUBLIC
        ${INCLUDE_DIR}
)