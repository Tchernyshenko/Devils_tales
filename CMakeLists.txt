cmake_minimum_required(VERSION 3.16)

project(Devils_tales LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Добавляем внешний проект SFML
add_subdirectory(external/SFML)

# Основной проект
add_executable(Devils_tales src/main.cpp)

# Присоединяем библиотеки SFML
target_link_libraries(Devils_tales PRIVATE
    sfml-audio sfml-graphics sfml-network sfml-system sfml-window
    stdc++fs
)

# Платформенно-зависимые дополнения
if(WIN32)
    target_link_libraries(Devils_tales PRIVATE opengl32 winmm gdi32 user32)
endif()

include(GNUInstallDirs)
install(TARGETS Devils_tales
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
