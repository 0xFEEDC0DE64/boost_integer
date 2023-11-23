# Copyright 2018 Peter Dimov
# Copyright 2018 Andrey Semashev
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at https://www.boost.org/LICENSE_1_0.txt

if(NOT DEFINED IDF_TARGET)

cmake_minimum_required(VERSION 3.5...3.20)

project(boost_integer VERSION "${BOOST_SUPERPROJECT_VERSION}" LANGUAGES CXX)

add_library(boost_integer INTERFACE)
add_library(Boost::integer ALIAS boost_integer)

target_include_directories(boost_integer INTERFACE include)

target_link_libraries(boost_integer
    INTERFACE
        Boost::assert
        Boost::config
        Boost::core
        Boost::static_assert
        Boost::throw_exception
)

else()

FILE(GLOB_RECURSE headers include/*.h include/*.hpp)

idf_component_register(
    SRCS
        ${headers}
    INCLUDE_DIRS
        include
    REQUIRES
        boost_assert
        boost_config
        boost_core
        boost_static_assert
        boost_throw_exception
)

endif()
