cmake_minimum_required(VERSION 3.21)


if (ESP_PLATFORM)
idf_component_register(SRCS "src/json_generator.c"
INCLUDE_DIRS "include"
)
else()
    project(json_generator VERSION 1.1.2 LANGUAGES C)

    add_library(json_generator STATIC src/json_generator.c)
    target_include_directories(json_generator PUBLIC include)

    if (PROJECT_IS_TOP_LEVEL)
        add_executable(json_generator_test src/test.c)
        target_link_libraries(json_generator_test PRIVATE json_generator)
    endif()
endif()


