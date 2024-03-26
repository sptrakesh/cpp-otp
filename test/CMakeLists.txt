set(Target_Name "cotp_test")
FILE(GLOB_RECURSE cotp-test_SRCS *.cpp *.cc *.hpp *.h)
set(cotp-test_SRCS ${cotp-test_SRCS})
add_executable(${Target_Name} ${cotp-test_SRCS} )

target_compile_definitions(${Target_Name}
  PRIVATE _FORTIFY_SOURCE=2
)

include_directories(
  ../src
)

if (UNIX)
  if (APPLE)
    target_link_libraries(${Target_Name}
      PRIVATE cotp qrcodegen ${OPENSSL_LIBRARIES} ${JEMALLOC_LIBRARY}
    )
  else()
    target_link_libraries(${Target_Name}
      PRIVATE cotp qrcodegen ${OPENSSL_LIBRARIES} jemalloc
    )
  endif(APPLE)
else()
  target_link_libraries(${Target_Name}
    PRIVATE cotp qrcodegen ${OPENSSL_LIBRARIES}
  )
endif(UNIX)

install(TARGETS ${Target_Name} DESTINATION bin)
