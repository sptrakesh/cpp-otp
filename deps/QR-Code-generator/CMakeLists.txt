set(Target_Name "qrcodegen")
file(GLOB_RECURSE qr-code-generator_SRCS *.cpp *.h)
add_library(${Target_Name} STATIC ${qr-code-generator_SRCS})

target_compile_definitions(${Target_Name}
  PRIVATE _FORTIFY_SOURCE=2
)

set_target_properties(${Target_Name} PROPERTIES OUTPUT_NAME qrcodegen)
install(TARGETS ${Target_Name} DESTINATION lib)
install (
    DIRECTORY ${CMAKE_SOURCE_DIR}/deps/QR-Code-generator/
    DESTINATION include/qrcodegen
    FILES_MATCHING PATTERN "*.hpp")
