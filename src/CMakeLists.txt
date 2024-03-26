set(Target_Name "cotp")
file(GLOB_RECURSE cpp-otp_SRCS *.cpp *.hpp)
add_library(${Target_Name} STATIC ${cpp-otp_SRCS})

target_compile_definitions(${Target_Name}
  PRIVATE _FORTIFY_SOURCE=2
)

set_target_properties(${Target_Name} PROPERTIES OUTPUT_NAME cotp)
install(TARGETS ${Target_Name} DESTINATION lib)
install (
  DIRECTORY ${CMAKE_SOURCE_DIR}/src/cotp
  DESTINATION include
  FILES_MATCHING PATTERN "*.hpp*")
