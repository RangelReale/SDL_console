add_executable(example
  ConsoleExample.c split.c
)

target_link_libraries(example
  SDL_console
  ${SDLIMAGE_LIBRARY} ${SDL_LIBRARY} ${SDLMAIN_LIBRARY}
)

if (BUILD_OPENGL AND OPENGL_FOUND)

  add_executable(exampleGL
    ConsoleExample.c split.c
  )

  target_compile_definitions(exampleGL PRIVATE HAVE_OPENGL)

  target_link_libraries(exampleGL
    SDL_console
    ${SDLIMAGE_LIBRARY} ${SDL_LIBRARY} ${SDLMAIN_LIBRARY}
    ${OPENGL_gl_LIBRARY} ${OPENGL_glu_LIBRARY} 
#    ${GLUT_LIBRARIES}
  )


endif()
