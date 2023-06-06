cmake_minimum_required(VERSION 3.17)

project(UCLCodeReviewJune2023)

find_program(PANDOC pandoc)

add_custom_target(slides ALL
    COMMAND
    ${PANDOC} -s ${CMAKE_SOURCE_DIR}/slides.md -o ${CMAKE_BINARY_DIR}/slides.html
    -t revealjs
    --template ${CMAKE_SOURCE_DIR}/template.html
    -V revealjs-url=https://unpkg.com/reveal.js@^4
    -V theme=white
    -V transition=none
    -V backgroundTransition=none
    -V slideNumber=true
    -V height='\"100%\"'
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
    DEPENDS ${CMAKE_SOURCE_DIR}/slides.md
    BYPRODUCTS ${CMAKE_BINARY_DIR}/slides.html
    )

set(CMAKE_INSTALL_PREFIX ${CMAKE_BINARY_DIR})
install(FILES ${CMAKE_BINARY_DIR}/slides.html DESTINATION public)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/img DESTINATION public)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/lib DESTINATION public)
